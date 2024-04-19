- [**Introduction to HTML**](#introduction-to-html)
  - [**Anatomy of an HTML element**](#anatomy-of-an-html-element)
    - [**Attributes**](#attributes)
  - [**HTML Document Structure**](#html-document-structure)
- [**HTML elements**](#html-elements)
  - [**Text elements**](#text-elements)
    - [**Headings**](#headings)
    - [**Paragraphs**](#paragraphs)
    - [**Bold and Italic text**](#bold-and-italic-text)
      - [**Bold text**](#bold-text)
      - [**Italic text**](#italic-text)
    - [**Lists**](#lists)
      - [**Ordered list**](#ordered-list)
      - [**Unordered list**](#unordered-list)
  - [**Images**](#images)
    - [**`src` and `alt`**](#src-and-alt)
    - [**`width` and `height`**](#width-and-height)
  - [**Hyperlinks**](#hyperlinks)
  - [**Container elements**](#container-elements)
    - [**Page navigation element**](#page-navigation-element)
    - [**Header**](#header)
    - [**Article element**](#article-element)
    - [**Footer**](#footer)
    - [**Aside element**](#aside-element)
  - [**Button element**](#button-element)
- [**HTML entities**](#html-entities)
- [**Introduction to CSS**](#introduction-to-css)
  - [**Anatomy of a CSS code**](#anatomy-of-a-css-code)
  - [**Different types of implementing CSS**](#different-types-of-implementing-css)
- [CSS selectors](#css-selectors)
  - [Combining selectors](#combining-selectors)
  - [Descendant selector](#descendant-selector)
- [**Styling text**](#styling-text)

# **Introduction to HTML**

HTML stands for Hyper-Text Markup Language. HTML is one of the core technologies of web along with CSS and JavaScript. HTML is a markup language that web developers use to structure and describe the entire content of any webpage.

Note that we call the HTML a markup language. However, HTML is not really a programmin language, but it is a markup language that we use to describe something, and in the case of HTML we use HTML elements that describe different types of content.

Browsers understand HTML and render HTML code as website.

## **Anatomy of an HTML element**

This is what an HTML element generally looks like:

```html
<p>Sample text</p>
```

An HTML element is usually made up of 3 parts:

1. Openning tag `<p>`: which is the name of the element wrapped between `< >`
2. Content: can be either a simple text or another element, which we call a child element.
3. Closing tag `</p>`: which is the name of the element wrapped between `</` and `>`.

> Some elements have only one tag which acts as both the openning and closing tags. These elements do not have any content, but they almost always have **attributes** in order to tell them what to do.

### **Attributes**

Attributes are pieces of data which we can use to describe elements. One of the common attributes used in HTML element is the `src` attribute.

## **HTML Document Structure**

Every HTML document needs to have a specific structure. An HTML file which is going to act as the main page of a website should be called `index.html`.

As the starting structure of this file, we should follow certain steps everytime.

1. **Doctype definition:** It is used to tell the browser that the document uses HTML.

```html
<!DOCTYPE html>
```

1. **`html`, `head` and `body` elements:**

Each and every HTML document needs to start with an `html` element. Then inside the `html` element we need one `head` element and a `body` element.

The `head` element are for things that are not visible on the webpage, such as page title, link to CSS files or other things. Then the `body` element is for all the elements that will be rendered visible on the page.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>The basic language of the web: HTML</title>
  </head>
  <body>
    <h1>The basic language of the web: HTML</h1>
  </body>
</html>
```

The `<html>` element accepts a very important attribute named `lang` which we should use to define the language that we are using for the HTML document.

```html
<html lang="en">
  <head></head>
  <body></body>
</html>
```

Another important attribute that should usually be included is `charset` which describes the character set that is used in the document. This is a piece of information that describes the document and therefore it should be placed in a `<meta />` element inside the `<head>` element.

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
  </head>
  <body></body>
</html>
```

> Note that the `<meta />` is another element that has no closing tag.

Another element that is usually used inside the `<head>` element is the `<title>` element which determines the main title of the whole webpage. This title is displayed in the browser tab.

```html
<head>
  <meta charset="UTF-8" />
  <title>The basic language of the web</title>
</head>
```

# **HTML elements**

## **Text elements**

We now want to learn how to markup text.

### **Headings**

The goal of heading is to break up big blocks of text into logical sections and add a title to each section. There are 6 different levels of heading.

```html
<body>
  <h1>The basic language of the web: HTML</h1>
  <h2>The basic language of the web: HTML</h2>
  <h3>The basic language of the web: HTML</h3>
  <h4>The basic language of the web: HTML</h4>
  <h5>The basic language of the web: HTML</h5>
  <h6>The basic language of the web: HTML</h6>
</body>
```

> Each and every page on a website should only have one `<h1>` heading. You can have more and it does not violate any HTML rules, but regarding the SEO guidelines, it is good to have only one.

### **Paragraphs**

We use the generic `<p>` element to markup bigger blocks of text.

```html
<body>
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Modi quae harum
    quam! Doloribus, non modi. Necessitatibus nemo sit, harum laudantium
    perspiciatis quo. Minima officia assumenda nihil, placeat laborum esse
    debitis!
  </p>
</body>
```

### **Bold and Italic text**

There are special elements that we use to make a piece of text bold or italic.

#### **Bold text**

In order to make a text bold we can use `<b>` element.

```html
<p>Posted by <b>Omid Armat</b> on Monday</p>
```

> Using `<b>` element is not a good practice. It is an old HTML element and starting from HTML 5 we should use the `<strong>` element. This is because `<b>` does not have any meaning, while `<strong>` is a semantic HTML element that can be interpretted by search engines as an important piece of information.

```html
<p>Posted by <strong>Omid Armat</strong> on Monday</p>
```

#### **Italic text**

Here also we have two ways of making a text italic. The older way is to use the `<i>` element:

```html
<p>Posted by <i>Omid Armat</i> on Monday</p>
```

> The `<i>` element is not a good one to use. Instead, you should use the `<em>` element and browsers will interpret it as an emphasize. So again, this is a semantic HTML element.

```html
<p>Posted by <em>Omid Armat</em> on Monday</p>
```

### **Lists**

We are now going to learn to create lists with bullet points, which is also called an unordered list, and list with numbers, which is called an ordered list.

#### **Ordered list**

To create an ordered list you should use `<ol>` element, and for each list item you should use the `<li>` element.

```html
<ol>
  <li>List item</li>
  <li>List item</li>
  <li>List item</li>
</ol>
```

#### **Unordered list**

To create an unordered list you should use `<ul>` element, and for each list item you should use the `<li>` element.

```html
<ul>
  <li>List item</li>
  <li>List item</li>
  <li>List item</li>
</ul>
```

## **Images**

To insert an image into your webpage you need to use the `<img />` element. This element has no closing tag and therefore no contact.

### **`src` and `alt`**

The element accepts an **attribute** named `src` which tells the image tag where to find the image file that shold be displayed on the webpage. Another important attributes that you should always remember to insert into the `<img />` element is the `alt` attribute, which is used to describe what the image is about. This is done for several reasons:

1. By using the `alt` attribute we can tell search engines what the image is about.
2. Blind people that use screen readers can hear the value of this `alt` attribute and understand the image.

```html
<img src="post-img.jpg" alt="HTML code on a screen" />
```

> The address inserted into the `src` attribute of the image element should not necessarily be an address in the local directory of your project. It can be a URL address on the web.

> The value of the `alt` attribute is not displayed on the page unless the browser cannot load the image for any reason.

### **`width` and `height`**

We can specify the dimensions of the image loaded into the screen by using the corresponding attributes. However, we usually manage the dimesions of an image element using CSS.

```html
<img src="post-img.jpg" alt="HTML code on a screen" width="500" />
```

> Specifying only the `width` or the `height` attribute of the image will cause the browser to maintain the image's aspect ratio. If you specify both attributes you can override the aspect ratio and distort the image.

## **Hyperlinks**

Links are actually the elements that enable the internet to be a worldwide web. We can devide links in 2 categories:

1. Links to another page of the same website
2. Links to somewhere outside the website

Both these types are created in the exact same way in HTML, but there are still some particularities that you should be aware of. To insert a hyperlink, we need to use the `<a>` element. This element accepts as content the text that should act as the link and also be displayed on the webpage. We should also define the `href` attribute for this element that as its value will hold the actual URL address that we want the link to guide the user to:

```html
<a href="https://developer.mozilla.org/en-US/">MDN web docs</a>
```

> This makes the link open in the same tab of the browser. If you need to make it so that the link is opened in a new tab, you need to insert the `target` attribute and give it `_blank` as value.

```html
<a href="https://developer.mozilla.org/en-US/" target="_blank">MDN web docs</a>
```

For the first scenario, where we use a link to another page in the same website, you should first create the other page of your website in your file structure. So for example, we create a `blog.html` file, and then include a link to this page in the homepage which corresponds to the `index.html` file.

```html
<!-- index.html file -->
<a href="blog.html">Blog</a>

<!-- blog.html file -->
<a href="index.html">Home</a>
```

> Inserting a `#` symbol as the value for the `href` attribute causes the anchor element to act as a link, but it does not lead to anywhere.

> What makes an `<a>` element really a link, is the `href` attribute. This actually enable us differentiate between regular anchor elements and link anchor elements and use this difference in styling these links in CSS.

## **Container elements**

By using HTML container elements we can give our webpage's content a logical structure. It is not a good practice to simply insert content elements one after another. We should always wrap related HTML elements together into one container element. There are several container elements available, but we should always keep in mind to use elements that match our logical purpose.

Using container elements does not make any visual difference in the webpage, but it is a good practice to use these since they can help a lot in managing your content and also to improve the SEO of the webpage.

### **Page navigation element**

We usually group all the links at the top of a webpage into a `<nav>` element.

```html
<nav>
  <a href="blog.html">Blog</a>
  <a href="shop.html">Shop</a>
  <a href="products.html">Products</a>
</nav>
```

### **Header**

We usually group navigation, logo, and other stuff that should always appear at the top of the webpage into a `<header>` element.

```html
<header>
  <h1>The code magazine</h1>
  <nav>
    <a href="blog.html">Blog</a>
    <a href="shop.html">Shop</a>
    <a href="products.html">Products</a>
  </nav>
</header>
```

> The header element should not necessarily be used for top part of the whole webpage, but it can also be used as the top part of any smaller unit of content in the page. For instance, the title of a blog post, the initial image, and the text representing the writer's name can all be grouped into the `<header>` element.

### **Article element**

In a webpage that displays blog posts, we usually wrap all the elements that are related to the main part of the article in an `<article>` element.

```html
<article>
  <h2>Post title</h2>
  <p>Post text content</p>
  <img src="post-img.jpg" />
</article>
```

### **Footer**

The content that comes at the very end of a webpage and that is repeated in all pages of a website is usually wrapped in a `<footer>` element.

```html
<footer>
  <p>Copyright &copy; 2024 by Omid Armat</p>
</footer>
```

> The `<footer>` element can also accept simple text as content without inserting any child element.

### **Aside element**

The `<aside>` element is usually used for some secondary information that somehow completes the information in the main part of the page. We usually use this element to render sidebars, but since it is just a container element, it should not necessarily be used that way.

```html
<aside>
  <p>Related articles</p>
  <ul>
    <li><a href="#">article 1</a></li>
    <li><a href="#">article 2</a></li>
    <li><a href="#">article 3</a></li>
  </ul>
</aside>
```

## **Button element**

The `<button>` element is usually used when you want to add some functionality for the user. The button element accepts as content the text that should be displayed inside the button. It also accepts a couple of attributes.

```html
<button></button>
```

# **HTML entities**

HTML entities are basically some symbols that we can insert them into our HTML text elements using a special syntax that always starts with `&` and ends with a `;`. There are whole tables provided on the web, providing you with a list of HTML entities that you can use.

For instance, the copyright symbol can be inserted into your text like:

```html
<p>Copyright &copy; 2024 by Omid Armat</p>
```

# **Introduction to CSS**

CSS stands for Cascading Style Sheet. It is another core technology of the web. We use HTML to describe the content of the page. On the other hand, we use CSS to describe the visual style and the presentation of the content that we wrote in HTML.

HTML consists of countless elements to insert content into the webpage, and CSS consists of countless properties that we use to format HTML content.

## **Anatomy of a CSS code**

Take this sample CSS code as an example:

```css
h1 {
  color: blue;
  text-align: center;
  font-size: 20px;
}
```

1. **Selector:** a CSS code always starts with a selector. In this example, `h1` is the selector. This makes the styles to be applied to all `h1` elements on the page.
2. **Style declaration**: each line of styles mentioned in the example above are called style declaration which consists of a **property** and a **value** for that property. So for instance, `font-size` is the property and `20px` is the value.
3. **Declaration block:** all style declarations together make up the declaration block. A declaration block always starts with `{` and ends with `}`.
4. **CSS rule**: the selector and the declaration block is called a CSS rule.

## **Different types of implementing CSS**

There are 3 places where we can write CSS.

1. Inline CSS: To insert inline CSS, you should use the `style` attribute on any element that you want to style. This attribute accepts a string of a style declaration.

```html
<p style="color: blue">Related articles</p>
```

> Inline styles should never be used for many reasons that you are aware of.

2. Internal CSS: To insert internal CSS, you go to the `<head>` element of your HTML document, and in there, you declare a `<style>` element. Inside the `<style>` element you can write the regular syntax of a CSS rule like the example mentioned above.

```html
<head>
  <meta charset="UTF-8" />
  <title>The basic language of the web</title>
  <style>
    h1 {
      color: blue;
      text-align: center;
      font-size: 20px;
    }
  </style>
</head>
```

> This is a better way of implementing CSS, but there is yet another better way. If you have a lot of CSS code this will make the HTML file unmanagable.

3. External CSS: In this way of implementing CSS, you create a new file in your project directoy, for instance, `style.css`. Then we need a way of connecting the HTML file to the CSS file. This is done by inserting a `<link>` element in the `head` element of the HTML document.

```html
<head>
  <meta charset="UTF-8" />
  <title>The basic language of the web</title>
  <style>
    h1 {
      color: blue;
      text-align: center;
      font-size: 20px;
    }
  </style>
  <link href="style.css" rel="stylesheet" />
</head>
```

# CSS selectors

Selectors help us manage the specificity of applying styles to elements. We can select multiple elements together. We can also select elements by their element name, their class names, their IDs, etc.

## Combining selectors

We can select multiple HTML elements to declarte certain styles that want to be applied to all of them.

```css
h1,
h2,
h3,
h4,
p {
  font-family: sans-serif;
}
```

## Descendant selector

# **Styling text**

We will now learn the CSS properties that you can use to style text.

```css
p {
  color: blue;
  font-size: 26px;
  font-family: sans-serif;
  /* you cannot simply use a font family that you have installed on your computer. Because that would not work for other users that come to your page from other computers  */
  text-transform: uppercase;
  font-style: italic;
  line-height: 1.5;
  /* line height will be 1.5 times the font size  */
  text-align: center;
  /* centers the text inside its parent element */
}
```

> When you style a `<p>` element just like the example above, all other text elements that exist inside this `<p>` element will **inherit** the styles you declared unless you delare styles for them specifically. For instance, if you have a `<strong>` element inside the `<p>` element, the text inside the `<strong>` element will follow the styles declarations that you made for the `<p>` element which is the parent element.
