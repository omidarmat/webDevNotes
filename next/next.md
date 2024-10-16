# NextJS essentials

- [NextJS essentials](#nextjs-essentials)
  - [Rendering in NextJS](#rendering-in-nextjs)
  - [Rendering in React](#rendering-in-react)
    - [Client-Side Rendering (CSR)](#client-side-rendering-csr)
    - [Server-Side Rendering (SSR)](#server-side-rendering-ssr)
      - [Suspense for SSR](#suspense-for-ssr)
    - [React Server Components (RSC)](#react-server-components-rsc)

This file is written based on the content produced by _Codevolution_ in videos available on youtube via the link below:

```
https://www.youtube.com/playlist?list=PLC3y8-rFHvwjOKd6gdf4QtV1uYNiQnruI
```

## Rendering in NextJS

Rendering is the process that transforms the code you write into user interfaces. However, choosing the **right time and place** to do this rendering is vital for building a **performant** application. In this regard, we will consider some concepts: **CSR**, **SSR** and **RSCs**.

Before diving into rendering in NextJS, let's first understand rendering in React. This will help us better grasp how rendering works in NextJS.

To fully understand Rendering in NextJS, it helps to know about the evolution of React's rendering over the last decade. So let's first understand how React has evolved its rendering strategies.

## Rendering in React

### Client-Side Rendering (CSR)

In a typical SPA, when a client sends a request, the server sends a single HTML page to the browser, containing a simple `<div>` tag and a reference to a JavaScript file. This JavaScript file contains everything your application needs to run, including React library itself and your application code. It is downloaded when the HTML file is parsed. The downloaded JavaScript code then generates the HTML on your computer and inserts it into the DOM under the root `<div>` element. This process is evident when you see the HTML in the DOM inspector, containing rendered HTML, but not in the 'View source' option which shows the HTML file sent by the server to the browser. This HTML file is basically empty.

This method of rendering, where the component code is transformed into a user interface directly within the browser (the client), is known as **Client-Side Rendering (CSR)**. However, developers soon noticed some inherent drawbacks to this approach:

1. **Negative impact on SEO:** Genering HTML that mainly contains a single `<div>` is not optimal for SEO, as it provides little content for search engines to index. Large bundle size and a waterfall of network requests for API responses from deeply nested components may result in meaningful content not being renderd fast enough for being indexed.
2. **Negative impact on Performance:** Having the browser handle all the work such as fetching data, computing the UI, and making the HTML interactive, can slow things down. Users might see a blank screen or a loading spinner while the page loads. Each new feature added to the application increases the size of the JavaScript bundle, prolonging the wait time for users to see the UI. This delay will be noticable for users with slow internet connections.

To overcome these drawbacks of CSR, modern React frameworks like Gatsby and NextJS moved toward Server-Side solutions (SSR). This approach fundamentally changes how content is delivered to the user.

### Server-Side Rendering (SSR)

when a request comes in, instead of sending a nearly empty HTML file that depends on client-side JavaScript to construct the page, the server takes charge of rendering the full HTML. This fully-formed HTML document is then sent directly to the browser. Since the HTML is generated on the server, the browser is able to quickly parse and display it, improving the initial page load time. The Server-Side approach effectively addresses the issues associated with CSR.

1. **Positive impact on SEO:** search engines can easily index the server-rendered content.
2. **Positive impact on performance:** users can immediately see the page HTML content, instead of a blank screen or a loading spinner.

However, SSR approach to immediately improving the visibility of content has its own complexity, particularly when it comes to page's **interactivity**.

The full interactivity of the page is on hold until the JavaScript bundle comprising React itself along with your application-specific code has been completely downloaded and executed by the browser. This important phase, known as **hydration**, is where the static HTML page initially served by the server is brought to life.

During Hydration, React takes control in the browser with constructing the component tree in memory based on the static HTML that was served. It carefully plans the placement of interactive elements within this tree. Then React proceeds to bind the necessary JavaScript logic to these elements. This involves, initializing the application state, attaching event handlers for actions such as clicks and mouseovers, and setting up any other dynamic functionalities required for a fully interactive user experience.

Server-side solutions can be categorized in two strategies:

1. **Static Site Generation (SSG):** this occures at build time, when the application is deployed on the server. This results in pages that are already rendered and ready to be served. It is ideal for content that does not change often, like blog posts.
2. **Server-Side Rendering(SSR):** renders pages on-demand in response to user requests. It is suitable for personalized content like social media feeds, where the HTML depends on the logged-in user.

SSR was a significant improvement over CSR providing faster initial page loads and better SEO. However, SSR introduced its own set of challenges:

1. **You have to fetch everything before you can show anything:** components cannot start rendering and wait while data is still being loaded. If a component needs to fetch data from a database or an API, this fetching must be completed before the server can begin rendering the page. This can delay the server's response time to the browser, as the server must finish collecting all necessary data before any part of the page can be sent to the client.
2. **You have to load everything before you can hydrate anything:** for successful hydration, where React adds interactivity to the server-rendered HTML, the component tree in the browser must exactly match the server-generated component tree. This means that all the JavaScript for the components must be loaded on the client before you can start hydrating any of them.
3. **You have to hydrate everything before you can interact with anything:** React hydrates the domponent tree in a single pass, meaning once it starts hydrating, it won't stop until it is finished with the entire tree. As a consequence, all components must be hydrated before you can interact with any of them.

These three problems create an _all or nothing_ waterfall problem that spans from the server to the client, where each issue must be resolved before moving to the next one. This is inefficient if some parts of the application are slower than others, as is often the case in real-world apps. As a result, the React team introduced a new and improved SSR architecture.

#### Suspense for SSR

The suspense SSR architecture allows you to use the `<Suspence>` component to unlock two major SSR features:

1. **HTML streaming on the server**
2. **Selective hydration on the client**

As we discussed before, SSR has been an all or nothing affair. The server sends to the client the complete HTML with a reference to a JavaScript file. The client displays this HTML and only after the complete JavaScript bundle is loaded, React proceeds to hydrate the entire application to add interactivity. Here is a similar visualization from a user interface perspective:

```jsx
<Layout>
  <Header />
  <Sidenav />
  <MainContent />
  <Footer />
<Layout />
```

First, you render all HTML, the cient eventually receives it, then you load all the code and hydrate the entire application. However, with React 18 we have a new possibility:

```jsx
<Layout>
  <Header />
  <Sidenav />
  <Suspense fallback={<Spinner />}>
    <MainContent />
  <Suspense />
  <Footer />
<Layout />
```

By wrapping a part of the page, such as the `<MainContent />` within the `<Suspence>` component, we instruct React that it does not need to wait for the main section data to be fetched to start streaming the HTML for the rest of the page. React will send a placeholder, like a spinner, instead of the complete component. Once the server is ready with the data for the main section, React sends additional HTML to the ongoing stream accompanied by an inline `script` tag containing the minimal JavaScript needed to correctly position that HTML. As a result, even before the full React library is loaded on the clinet-side, the HTML for the main section becomes visible to the user. This solves the first problem mentioned before: **now you don't have to fetch everything before you can show anything.** If a particular section delays the initial HTML, it can be seamlessly integrated into the stream later. This is the essence of how `<Suspence>` facilitates server-side HTML streaming.

We still have another challenge. Until the JavaScript for the main section is loaded, client-side app hydration cannot start. Now if the JavaScript bundle for the main section is large, this could significantly delay the process. To mitigate this, **code splitting** can be used. Code splitting allows you to mark specific code segments as not immediately necessary for loading, signaling your bundler to segregate them into separate `script` tags. Using React `lazy` for code splitting, enables you to separate the main section's code from the primary JavaScript bundle. As a result, the JavaScript containing React and the code for the entire application, excluding the main section, can now be downloaded by the client without having to wait for the main section's code. This is crucial because by wrapping the main section within `<Suspence>` you have indicated to React that it should not prevent the rest of the page from not just streaming, but also from hydrating. This feature, called **Sselective hydration** allows for the hydration of sections as they become available before the rest of the HTML and the JavaScript code are fully downloaded.

From the user's perspective, initially they see non-interactive content that streams in as HTML. Then you tell React to hydrate. The JavaScript code for the main section is not there yet, but it is ok as we can selectively hydrate other components. The main section is hydrated once its code is loaded. Thanks to selective hydration, a heavy piece of JavaScript does not prevent the rest of the page from becoming interactive. Moreover, selective hydration offers a solution to a third issue: **the neccessity to hydrate everything to interact with anything.** React begins hydrating as soon as possible enabling interactions with elements like the header and side navigation without waiting for the main content to be hydrated. This process is managed automatically by React. In scenarios where multiple components are awaiting hydration, **React prioritizes hydration based on user interactions**. For instance, if the `<Sidenav />` is about to be hydrated, and you click on the `<MainContent />` area, React will synchronously hydrate the clicked component during the capture phase of the click event. This ensures the component is ready to respond immediately to user interactions. `<Sidenav />` is hydrated later on.

So the 3 significant drawbacks of traditional SSR have all been addressed by the new Suspense SSR architecture. Despite these improvemenet, few challenges still remain:

1. Eventhough JavaScript code is streamed to the browser asynchronously, eventually the entire code for a webpage must be downloaded by the user. As applications add more features, the amount of code users need to download grows. This leads to an important question: **Should users really have to download so much data?**
2. The current approach requires that all React components undergo hydration on the client-side, irrespective of their actual need for interactivity. This process can inefficiently spend resources and extend loading time and time to interactivity for users as their devices need to process and render components that might not even require client-side interaction. This leads to another question: **Should all components be hydrated, even those that don't need interactivity?**
3. In spite of server's superior capacity for handling intensive processing tasks, the bulk of JavaScript execution still takes place on the user's device. This can slow down the performance, especially on devices that are not very powerful. This leads to another important question: **Should so much of the work be done on the user's device?**

These issues highlight the need for a better way to build faster applications that improve upon traditional rendering techniques while overcoming their limitations. Let's take a look at what the solution is.

### React Server Components (RSC)
