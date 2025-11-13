# 📘 Complete HTML Learning & Interview Guide

**From Beginner to Expert | Syntax Reference | Interview Prep | Quick Revision**

---

## 📑 Table of Contents

1. [Introduction](#introduction)
2. [HTML Foundations](#html-foundations)
3. [HTML Document Structure](#html-document-structure)
4. [Complete HTML Tags Reference](#complete-html-tags-reference)
5. [HTML Attributes (Global & Specific)](#html-attributes-global--specific)
6. [HTML Forms & Input Types](#html-forms--input-types)
7. [HTML Media Elements](#html-media-elements)
8. [HTML Tables](#html-tables)
9. [Semantic HTML](#semantic-html)
10. [SEO Basics & Meta Tags](#seo-basics--meta-tags)
11. [Accessibility (ARIA)](#accessibility-aria)
12. [HTML Best Practices](#html-best-practices)
13. [Deprecated Tags](#deprecated-tags)
14. [Stair-Wise Micro-Learning Drills](#stair-wise-micro-learning-drills)
15. [Interview Questions (Easy/Medium/Hard)](#interview-questions)
16. [Debugging Challenges](#debugging-challenges)
17. [Real-World Mini Projects](#real-world-mini-projects)
18. [Quick Revision Cheatsheet](#quick-revision-cheatsheet)
19. [Conclusion](#conclusion)

---

## 🎯 Introduction

### What is HTML?

**HTML (HyperText Markup Language)** is the standard markup language for creating web pages. It provides the structure and content of websites.

### Key Points:
- **Not a programming language** - It's a markup language
- **Defines structure** - Headers, paragraphs, links, images, etc.
- **Works with CSS & JavaScript** - HTML (structure), CSS (style), JS (behavior)
- **Browser interprets** - Browsers render HTML into visual web pages

### HTML History Timeline:

```
HTML 1.0 (1991)  →  HTML 2.0 (1995)  →  HTML 4.01 (1999)
  ↓
XHTML 1.0 (2000)  →  HTML5 (2014)  →  HTML Living Standard (Current)
```

### How HTML Works:

```
1. Write HTML code → 2. Save as .html file → 3. Open in browser → 4. Browser renders page
```

---

## 🏗️ HTML Foundations

### Basic HTML Syntax

```html
<tagname attribute="value">Content</tagname>
```

**Components:**
- `<tagname>` - Opening tag
- `attribute="value"` - Optional attributes
- `Content` - Text or nested elements
- `</tagname>` - Closing tag

### Self-Closing Tags

Some tags don't need closing tags:

```html
<img src="image.jpg" alt="Description">
<br>
<hr>
<input type="text">
<meta charset="UTF-8">
```

### Nested Elements

```html
<div>
  <p>This is a <strong>nested</strong> structure.</p>
</div>
```

**Rules:**
- Inner tags must close before outer tags
- Proper nesting: `<p><strong>text</strong></p>` ✅
- Improper nesting: `<p><strong>text</p></strong>` ❌

### HTML Comments

```html
<!-- This is a comment -->
<!-- 
  Multi-line
  comment
-->
```

**Best Practices:**
- Use comments to explain complex sections
- Don't overuse - keep HTML clean
- Remove comments before production

---

## 📄 HTML Document Structure

### Basic HTML5 Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Page description">
    <title>Document Title</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <nav>Navigation</nav>
    </header>
    
    <main>
        <article>Main content</article>
    </main>
    
    <footer>Footer content</footer>
    
    <script src="script.js"></script>
</body>
</html>
```

### Breaking Down Each Part:

#### 1. `<!DOCTYPE html>`
- **Purpose:** Tells browser this is HTML5
- **Must be first line**
- **Not case-sensitive**

#### 2. `<html lang="en">`
- **Root element** - Contains all HTML
- **lang attribute** - Specifies language (important for SEO & accessibility)

#### 3. `<head>` Section
- **Contains metadata** - Not visible on page
- **Title, links, scripts, meta tags**

#### 4. `<body>` Section
- **Visible content**
- **All displayable elements**

---

## 📚 Complete HTML Tags Reference

### Document Metadata Tags

| Tag | Description | Example |
|-----|-------------|---------|
| `<!DOCTYPE>` | Document type declaration | `<!DOCTYPE html>` |
| `<html>` | Root element | `<html lang="en">` |
| `<head>` | Contains metadata | `<head>...</head>` |
| `<title>` | Document title | `<title>My Page</title>` |
| `<base>` | Base URL for relative URLs | `<base href="https://example.com/">` |
| `<link>` | External resource link | `<link rel="stylesheet" href="style.css">` |
| `<meta>` | Metadata | `<meta charset="UTF-8">` |
| `<style>` | Internal CSS | `<style>body{margin:0;}</style>` |

### Content Sectioning Tags

| Tag | Description | Example | When to Use |
|-----|-------------|---------|-------------|
| `<body>` | Document body | `<body>...</body>` | Always (once) |
| `<header>` | Header section | `<header><h1>Title</h1></header>` | Top of page/section |
| `<nav>` | Navigation links | `<nav><a href="/">Home</a></nav>` | Navigation menus |
| `<main>` | Main content | `<main>...</main>` | Primary content (once per page) |
| `<section>` | Generic section | `<section><h2>About</h2></section>` | Thematic grouping |
| `<article>` | Independent content | `<article>Blog post</article>` | Self-contained content |
| `<aside>` | Sidebar content | `<aside>Related links</aside>` | Tangential content |
| `<footer>` | Footer section | `<footer>© 2024</footer>` | Bottom of page/section |
| `<h1>` to `<h6>` | Headings | `<h1>Main Title</h1>` | Hierarchical headings |
| `<address>` | Contact information | `<address>Email: info@example.com</address>` | Contact details |

### Text Content Tags

| Tag | Description | Example | Visual Effect |
|-----|-------------|---------|---------------|
| `<p>` | Paragraph | `<p>Text here</p>` | Block, spacing |
| `<div>` | Generic container | `<div>Content</div>` | Block container |
| `<span>` | Inline container | `<span>Text</span>` | Inline container |
| `<hr>` | Horizontal rule | `<hr>` | Horizontal line |
| `<br>` | Line break | `Text<br>New line` | Line break |
| `<pre>` | Preformatted text | `<pre>  Spaces preserved  </pre>` | Monospace, preserves whitespace |
| `<blockquote>` | Block quotation | `<blockquote>Quote</blockquote>` | Indented quote |
| `<ol>` | Ordered list | `<ol><li>First</li></ol>` | Numbered list |
| `<ul>` | Unordered list | `<ul><li>Item</li></ul>` | Bulleted list |
| `<li>` | List item | `<li>Item</li>` | List entry |
| `<dl>` | Description list | `<dl><dt>Term</dt><dd>Definition</dd></dl>` | Term-definition pairs |
| `<dt>` | Description term | `<dt>HTML</dt>` | Term in dl |
| `<dd>` | Description details | `<dd>Markup language</dd>` | Definition in dl |
| `<figure>` | Figure with caption | `<figure><img><figcaption></figcaption></figure>` | Self-contained content |
| `<figcaption>` | Figure caption | `<figcaption>Image caption</figcaption>` | Caption for figure |

### Inline Text Semantics

| Tag | Description | Example | Semantic Meaning |
|-----|-------------|---------|------------------|
| `<a>` | Anchor/Link | `<a href="url">Link</a>` | Hyperlink |
| `<strong>` | Strong importance | `<strong>Important</strong>` | Strong emphasis (bold) |
| `<b>` | Bold text | `<b>Bold</b>` | Stylistic bold (no emphasis) |
| `<em>` | Emphasis | `<em>Emphasized</em>` | Stressed emphasis (italic) |
| `<i>` | Italic text | `<i>Italic</i>` | Stylistic italic |
| `<mark>` | Marked/highlighted | `<mark>Highlighted</mark>` | Highlighted text |
| `<small>` | Small text | `<small>Fine print</small>` | Side comments |
| `<del>` | Deleted text | `<del>Removed</del>` | Strikethrough |
| `<ins>` | Inserted text | `<ins>Added</ins>` | Underlined |
| `<sub>` | Subscript | `H<sub>2</sub>O` | Subscript |
| `<sup>` | Superscript | `X<sup>2</sup>` | Superscript |
| `<code>` | Code snippet | `<code>console.log()</code>` | Inline code |
| `<kbd>` | Keyboard input | `<kbd>Ctrl</kbd>` | Keyboard key |
| `<samp>` | Sample output | `<samp>Output text</samp>` | Program output |
| `<var>` | Variable | `<var>x</var> = 5` | Mathematical variable |
| `<abbr>` | Abbreviation | `<abbr title="HyperText Markup Language">HTML</abbr>` | Abbreviation with tooltip |
| `<cite>` | Citation | `<cite>Book Title</cite>` | Reference to work |
| `<q>` | Inline quotation | `<q>Quote</q>` | Inline quote with quotes |
| `<dfn>` | Definition term | `<dfn>HTML</dfn> is...` | Defining instance |
| `<time>` | Date/Time | `<time datetime="2024-01-01">Jan 1, 2024</time>` | Machine-readable time |
| `<data>` | Machine-readable | `<data value="123">Item</data>` | Machine-readable value |
| `<bdi>` | Bi-directional isolation | `<bdi>نص عربي</bdi>` | Isolates text direction |
| `<bdo>` | Bi-directional override | `<bdo dir="rtl">Text</bdo>` | Overrides text direction |
| `<wbr>` | Word break opportunity | `VeryLong<wbr>Word` | Optional line break |

### Image and Multimedia Tags

| Tag | Description | Example | Key Attributes |
|-----|-------------|---------|----------------|
| `<img>` | Image | `<img src="image.jpg" alt="Description">` | src, alt, width, height |
| `<audio>` | Audio content | `<audio src="audio.mp3" controls></audio>` | src, controls, autoplay, loop |
| `<video>` | Video content | `<video src="video.mp4" controls></video>` | src, controls, autoplay, loop, poster |
| `<source>` | Media source | `<source src="video.mp4" type="video/mp4">` | src, type |
| `<track>` | Text tracks | `<track src="subtitles.vtt" kind="subtitles">` | src, kind, srclang |
| `<picture>` | Responsive images | `<picture><source srcset="img.webp"><img src="img.jpg"></picture>` | Multiple sources |
| `<canvas>` | Graphics canvas | `<canvas id="myCanvas"></canvas>` | width, height |
| `<svg>` | SVG graphics | `<svg><circle cx="50" cy="50" r="40"/></svg>` | width, height, viewBox |
| `<map>` | Image map | `<map name="imagemap">` | name |
| `<area>` | Image map area | `<area shape="rect" coords="0,0,100,100" href="link.html">` | shape, coords, href |

### Embedded Content Tags

| Tag | Description | Example |
|-----|-------------|---------|
| `<iframe>` | Inline frame | `<iframe src="https://example.com"></iframe>` |
| `<embed>` | External content | `<embed src="file.pdf" type="application/pdf">` |
| `<object>` | External object | `<object data="file.pdf" type="application/pdf"></object>` |
| `<param>` | Object parameter | `<param name="autoplay" value="true">` |
| `<portal>` | Portal (experimental) | `<portal src="https://example.com"></portal>` |

### Scripting Tags

| Tag | Description | Example |
|-----|-------------|---------|
| `<script>` | JavaScript | `<script src="script.js"></script>` |
| `<noscript>` | No script fallback | `<noscript>Please enable JavaScript</noscript>` |
| `<template>` | HTML template | `<template id="myTemplate"><p>Content</p></template>` |
| `<slot>` | Web component slot | `<slot name="content"></slot>` |

### Table Tags

| Tag | Description | Example |
|-----|-------------|---------|
| `<table>` | Table | `<table>...</table>` |
| `<caption>` | Table caption | `<caption>Table Title</caption>` |
| `<thead>` | Table header group | `<thead><tr><th>Header</th></tr></thead>` |
| `<tbody>` | Table body group | `<tbody><tr><td>Data</td></tr></tbody>` |
| `<tfoot>` | Table footer group | `<tfoot><tr><td>Footer</td></tr></tfoot>` |
| `<tr>` | Table row | `<tr><td>Cell</td></tr>` |
| `<th>` | Table header cell | `<th>Header</th>` |
| `<td>` | Table data cell | `<td>Data</td>` |
| `<col>` | Table column | `<col span="2">` |
| `<colgroup>` | Table column group | `<colgroup><col><col></colgroup>` |

### Form Tags

| Tag | Description | Example |
|-----|-------------|---------|
| `<form>` | Form | `<form action="/submit" method="POST">` |
| `<input>` | Input field | `<input type="text" name="username">` |
| `<textarea>` | Multi-line text | `<textarea rows="4" cols="50"></textarea>` |
| `<button>` | Button | `<button type="submit">Submit</button>` |
| `<select>` | Dropdown list | `<select><option>Option 1</option></select>` |
| `<option>` | Dropdown option | `<option value="1">Option 1</option>` |
| `<optgroup>` | Option group | `<optgroup label="Group 1">` |
| `<label>` | Input label | `<label for="username">Username:</label>` |
| `<fieldset>` | Group form elements | `<fieldset><legend>Personal Info</legend></fieldset>` |
| `<legend>` | Fieldset caption | `<legend>Login Details</legend>` |
| `<datalist>` | Autocomplete options | `<datalist id="browsers"><option value="Chrome"></datalist>` |
| `<output>` | Calculation result | `<output name="result"></output>` |
| `<progress>` | Progress bar | `<progress value="70" max="100"></progress>` |
| `<meter>` | Scalar measurement | `<meter value="6" min="0" max="10"></meter>` |

### Interactive Elements

| Tag | Description | Example |
|-----|-------------|---------|
| `<details>` | Disclosure widget | `<details><summary>Click to expand</summary>Content</details>` |
| `<summary>` | Details summary | `<summary>More info</summary>` |
| `<dialog>` | Dialog box | `<dialog open>This is a dialog</dialog>` |
| `<menu>` | Menu | `<menu><li>Item 1</li></menu>` |

### Web Components

| Tag | Description | Example |
|-----|-------------|---------|
| `<template>` | Reusable template | `<template id="myTemplate"><p>Template content</p></template>` |
| `<slot>` | Content placeholder | `<slot name="content"></slot>` |

---

## 🏷️ HTML Attributes (Global & Specific)

### Global Attributes

**Global attributes** can be used on **any HTML element**.

| Attribute | Description | Example |
|-----------|-------------|---------|
| `id` | Unique identifier | `<div id="header">` |
| `class` | CSS class(es) | `<p class="intro highlight">` |
| `style` | Inline CSS | `<p style="color: red;">` |
| `title` | Tooltip text | `<abbr title="HyperText Markup Language">HTML</abbr>` |
| `lang` | Language | `<p lang="es">Hola</p>` |
| `dir` | Text direction | `<p dir="rtl">Arabic text</p>` |
| `hidden` | Hide element | `<div hidden>` |
| `tabindex` | Tab order | `<div tabindex="0">` |
| `accesskey` | Keyboard shortcut | `<button accesskey="s">Save</button>` |
| `contenteditable` | Editable content | `<div contenteditable="true">` |
| `draggable` | Draggable element | `<img draggable="true">` |
| `spellcheck` | Spell checking | `<textarea spellcheck="true">` |
| `translate` | Translation behavior | `<p translate="no">` |
| `data-*` | Custom data | `<div data-user-id="123">` |

### Event Attributes

| Attribute | Event | Example |
|-----------|-------|---------|
| `onclick` | Click event | `<button onclick="alert('Clicked')">` |
| `onchange` | Change event | `<input onchange="handleChange()">` |
| `onsubmit` | Form submit | `<form onsubmit="return validate()">` |
| `onload` | Page/Image load | `<body onload="init()">` |
| `onmouseover` | Mouse over | `<div onmouseover="highlight()">` |
| `onmouseout` | Mouse out | `<div onmouseout="unhighlight()">` |
| `onkeydown` | Key down | `<input onkeydown="handleKey()">` |
| `onkeyup` | Key up | `<input onkeyup="handleKey()">` |
| `onfocus` | Focus | `<input onfocus="showHelp()">` |
| `onblur` | Blur | `<input onblur="validate()">` |

### Link-Specific Attributes (`<a>`)

| Attribute | Description | Example |
|-----------|-------------|---------|
| `href` | Link URL | `<a href="https://example.com">` |
| `target` | Where to open | `<a target="_blank">` (new tab) |
| `rel` | Relationship | `<a rel="nofollow">` |
| `download` | Download file | `<a href="file.pdf" download>` |
| `hreflang` | Link language | `<a hreflang="es">` |
| `type` | MIME type | `<a type="application/pdf">` |

**Target Values:**
- `_blank` - New window/tab
- `_self` - Same frame (default)
- `_parent` - Parent frame
- `_top` - Full window

### Image Attributes (`<img>`)

| Attribute | Description | Example |
|-----------|-------------|---------|
| `src` | Image source | `<img src="image.jpg">` |
| `alt` | Alternative text | `<img alt="Description">` |
| `width` | Image width | `<img width="300">` |
| `height` | Image height | `<img height="200">` |
| `loading` | Lazy loading | `<img loading="lazy">` |
| `srcset` | Responsive sources | `<img srcset="small.jpg 480w, large.jpg 800w">` |
| `sizes` | Image sizes | `<img sizes="(max-width: 600px) 480px, 800px">` |
| `crossorigin` | CORS settings | `<img crossorigin="anonymous">` |
| `decoding` | Decode timing | `<img decoding="async">` |
| `ismap` | Server-side map | `<img ismap>` |
| `usemap` | Client-side map | `<img usemap="#map1">` |

### Form Attributes (`<form>`)

| Attribute | Description | Example |
|-----------|-------------|---------|
| `action` | Submit URL | `<form action="/submit">` |
| `method` | HTTP method | `<form method="POST">` |
| `enctype` | Encoding type | `<form enctype="multipart/form-data">` |
| `target` | Where to display response | `<form target="_blank">` |
| `autocomplete` | Autocomplete | `<form autocomplete="off">` |
| `novalidate` | Disable validation | `<form novalidate>` |
| `name` | Form name | `<form name="loginForm">` |
| `accept-charset` | Character encoding | `<form accept-charset="UTF-8">` |

### Input Attributes (`<input>`)

| Attribute | Description | Example |
|-----------|-------------|---------|
| `type` | Input type | `<input type="text">` |
| `name` | Input name | `<input name="username">` |
| `value` | Default value | `<input value="Default">` |
| `placeholder` | Hint text | `<input placeholder="Enter name">` |
| `required` | Required field | `<input required>` |
| `disabled` | Disable input | `<input disabled>` |
| `readonly` | Read-only | `<input readonly>` |
| `maxlength` | Max characters | `<input maxlength="10">` |
| `minlength` | Min characters | `<input minlength="3">` |
| `pattern` | Regex pattern | `<input pattern="[0-9]{3}">` |
| `min` | Minimum value | `<input type="number" min="0">` |
| `max` | Maximum value | `<input type="number" max="100">` |
| `step` | Value steps | `<input type="number" step="0.5">` |
| `autocomplete` | Autocomplete | `<input autocomplete="email">` |
| `autofocus` | Auto focus | `<input autofocus>` |
| `multiple` | Multiple values | `<input type="file" multiple>` |
| `accept` | File types | `<input type="file" accept="image/*">` |
| `checked` | Checked (checkbox/radio) | `<input type="checkbox" checked>` |
| `size` | Visible characters | `<input size="20">` |
| `list` | Datalist ID | `<input list="browsers">` |
| `form` | Form ID | `<input form="form1">` |

### Table Attributes

| Attribute | Element | Description | Example |
|-----------|---------|-------------|---------|
| `colspan` | `<td>`, `<th>` | Span columns | `<td colspan="2">` |
| `rowspan` | `<td>`, `<th>` | Span rows | `<td rowspan="3">` |
| `headers` | `<td>`, `<th>` | Header IDs | `<td headers="h1 h2">` |
| `scope` | `<th>` | Header scope | `<th scope="col">` |

### Media Attributes

| Attribute | Element | Description | Example |
|-----------|---------|-------------|---------|
| `src` | `<audio>`, `<video>` | Media source | `<video src="video.mp4">` |
| `controls` | `<audio>`, `<video>` | Show controls | `<video controls>` |
| `autoplay` | `<audio>`, `<video>` | Auto play | `<video autoplay>` |
| `loop` | `<audio>`, `<video>` | Loop playback | `<audio loop>` |
| `muted` | `<audio>`, `<video>` | Muted | `<video muted>` |
| `preload` | `<audio>`, `<video>` | Preload | `<video preload="auto">` |
| `poster` | `<video>` | Poster image | `<video poster="thumb.jpg">` |

### Meta Tag Attributes

| Attribute | Description | Example |
|-----------|-------------|---------|
| `charset` | Character encoding | `<meta charset="UTF-8">` |
| `name` | Metadata name | `<meta name="description">` |
| `content` | Metadata content | `<meta content="Page description">` |
| `http-equiv` | HTTP header | `<meta http-equiv="refresh">` |
| `property` | Open Graph | `<meta property="og:title">` |

---

## 📝 HTML Forms & Input Types

### Basic Form Structure

```html
<form action="/submit" method="POST" id="myForm">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
    
    <button type="submit">Submit</button>
</form>
```

### All Input Types

#### 1. Text Input Types

```html
<!-- Plain text -->
<input type="text" name="firstname" placeholder="First name">

<!-- Email with validation -->
<input type="email" name="email" placeholder="email@example.com" required>

<!-- Password (hidden characters) -->
<input type="password" name="password" minlength="8">

<!-- Search field -->
<input type="search" name="query" placeholder="Search...">

<!-- Telephone number -->
<input type="tel" name="phone" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}">

<!-- URL with validation -->
<input type="url" name="website" placeholder="https://example.com">
```

#### 2. Number Input Types

```html
<!-- Number -->
<input type="number" name="age" min="18" max="100" step="1">

<!-- Range slider -->
<input type="range" name="volume" min="0" max="100" value="50">
```

#### 3. Date & Time Input Types

```html
<!-- Date picker -->
<input type="date" name="birthdate" min="1900-01-01" max="2024-12-31">

<!-- Month picker -->
<input type="month" name="month">

<!-- Week picker -->
<input type="week" name="week">

<!-- Time picker -->
<input type="time" name="appointment">

<!-- Date and time -->
<input type="datetime-local" name="meeting">
```

#### 4. Selection Input Types

```html
<!-- Checkbox -->
<input type="checkbox" name="subscribe" id="sub" checked>
<label for="sub">Subscribe to newsletter</label>

<!-- Radio buttons (single choice) -->
<input type="radio" name="gender" value="male" id="male">
<label for="male">Male</label>
<input type="radio" name="gender" value="female" id="female">
<label for="female">Female</label>

<!-- Dropdown select -->
<select name="country">
    <option value="">Select country</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
    <option value="ca">Canada</option>
</select>

<!-- Multiple select -->
<select name="skills" multiple size="4">
    <option value="html">HTML</option>
    <option value="css">CSS</option>
    <option value="js">JavaScript</option>
    <option value="python">Python</option>
</select>
```

#### 5. File & Color Input Types

```html
<!-- File upload -->
<input type="file" name="document" accept=".pdf,.doc,.docx">

<!-- Multiple files -->
<input type="file" name="photos" multiple accept="image/*">

<!-- Color picker -->
<input type="color" name="theme" value="#ff0000">
```

#### 6. Button Types

```html
<!-- Submit button -->
<button type="submit">Submit Form</button>
<input type="submit" value="Submit Form">

<!-- Reset button -->
<button type="reset">Reset Form</button>

<!-- Regular button (for JavaScript) -->
<button type="button" onclick="doSomething()">Click Me</button>

<!-- Image button -->
<input type="image" src="submit.png" alt="Submit">
```

#### 7. Hidden & Special Types

```html
<!-- Hidden field -->
<input type="hidden" name="user_id" value="12345">
```

### Form Validation

#### HTML5 Built-in Validation

```html
<form>
    <!-- Required field -->
    <input type="text" name="username" required>
    
    <!-- Email validation -->
    <input type="email" name="email" required>
    
    <!-- Pattern matching -->
    <input type="text" name="zipcode" pattern="[0-9]{5}" 
           title="5-digit zip code">
    
    <!-- Length constraints -->
    <input type="text" name="username" 
           minlength="3" maxlength="20">
    
    <!-- Number constraints -->
    <input type="number" name="age" min="18" max="100">
    
    <!-- Custom validation message -->
    <input type="text" name="custom" 
           oninvalid="this.setCustomValidity('Custom error')"
           oninput="this.setCustomValidity('')">
    
    <button type="submit">Submit</button>
</form>
```

#### Common Patterns

```html
<!-- Email -->
<input type="email" pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$">

<!-- Phone (US) -->
<input type="tel" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}">

<!-- Zip Code (US) -->
<input type="text" pattern="[0-9]{5}">

<!-- Credit Card -->
<input type="text" pattern="[0-9]{16}">

<!-- Username (alphanumeric) -->
<input type="text" pattern="[A-Za-z0-9]{3,20}">

<!-- URL -->
<input type="url" pattern="https?://.+">
```

### Advanced Form Elements

#### Datalist (Autocomplete)

```html
<label for="browser">Choose a browser:</label>
<input list="browsers" id="browser" name="browser">
<datalist id="browsers">
    <option value="Chrome">
    <option value="Firefox">
    <option value="Safari">
    <option value="Edge">
</datalist>
```

#### Fieldset & Legend

```html
<form>
    <fieldset>
        <legend>Personal Information</legend>
        <label for="fname">First name:</label>
        <input type="text" id="fname" name="fname"><br>
        <label for="lname">Last name:</label>
        <input type="text" id="lname" name="lname">
    </fieldset>
    
    <fieldset>
        <legend>Contact Information</legend>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email"><br>
        <label for="phone">Phone:</label>
        <input type="tel" id="phone" name="phone">
    </fieldset>
</form>
```

#### Output Element

```html
<form oninput="result.value=parseInt(a.value)+parseInt(b.value)">
    <input type="range" id="a" value="50"> +
    <input type="number" id="b" value="50"> =
    <output name="result" for="a b">100</output>
</form>
```

#### Progress & Meter

```html
<!-- Progress bar -->
<label for="progress">Upload progress:</label>
<progress id="progress" value="70" max="100">70%</progress>

<!-- Meter (gauge) -->
<label for="disk">Disk usage:</label>
<meter id="disk" value="6" min="0" max="10" 
       low="3" high="7" optimum="2">6 out of 10</meter>
```

### Form Best Practices

1. **Always use labels**
   ```html
   <label for="email">Email:</label>
   <input type="email" id="email" name="email">
   ```

2. **Group related fields**
   ```html
   <fieldset>
       <legend>Shipping Address</legend>
       <!-- Address fields -->
   </fieldset>
   ```

3. **Use appropriate input types**
   - Better mobile experience
   - Built-in validation
   - Semantic meaning

4. **Provide helpful placeholders**
   ```html
   <input type="text" placeholder="e.g., John Doe">
   ```

5. **Add validation and feedback**
   ```html
   <input type="email" required 
          title="Please enter a valid email">
   ```

---

## 🎬 HTML Media Elements

### Images

#### Basic Image

```html
<img src="image.jpg" alt="Description of image" width="300" height="200">
```

#### Responsive Images

```html
<!-- Using srcset for different resolutions -->
<img src="small.jpg"
     srcset="small.jpg 480w,
             medium.jpg 800w,
             large.jpg 1200w"
     sizes="(max-width: 600px) 480px,
            (max-width: 1000px) 800px,
            1200px"
     alt="Responsive image">

<!-- Using picture element -->
<picture>
    <source media="(min-width: 800px)" srcset="large.jpg">
    <source media="(min-width: 400px)" srcset="medium.jpg">
    <img src="small.jpg" alt="Responsive image">
</picture>

<!-- WebP with fallback -->
<picture>
    <source srcset="image.webp" type="image/webp">
    <source srcset="image.jpg" type="image/jpeg">
    <img src="image.jpg" alt="Image with format fallback">
</picture>
```

#### Lazy Loading

```html
<img src="image.jpg" alt="Lazy loaded image" loading="lazy">
```

#### Image with Figure

```html
<figure>
    <img src="photo.jpg" alt="Beautiful sunset">
    <figcaption>Sunset over the ocean, 2024</figcaption>
</figure>
```

### Audio

#### Basic Audio

```html
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    Your browser does not support the audio element.
</audio>
```

#### Audio Attributes

```html
<audio controls autoplay loop muted preload="auto">
    <source src="song.mp3" type="audio/mpeg">
</audio>
```

**Attributes:**
- `controls` - Show playback controls
- `autoplay` - Start playing automatically
- `loop` - Loop playback
- `muted` - Muted by default
- `preload` - "auto", "metadata", "none"

### Video

#### Basic Video

```html
<video width="640" height="360" controls>
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    Your browser does not support the video tag.
</video>
```

#### Video with Poster

```html
<video width="640" height="360" controls poster="thumbnail.jpg">
    <source src="video.mp4" type="video/mp4">
</video>
```

#### Video with Subtitles

```html
<video controls>
    <source src="movie.mp4" type="video/mp4">
    <track src="subtitles-en.vtt" kind="subtitles" 
           srclang="en" label="English">
    <track src="subtitles-es.vtt" kind="subtitles" 
           srclang="es" label="Spanish">
</video>
```

**Track Kinds:**
- `subtitles` - Translations
- `captions` - Transcription with sound effects
- `descriptions` - Visual descriptions
- `chapters` - Chapter titles
- `metadata` - Metadata

### Iframe

```html
<!-- Embed external page -->
<iframe src="https://www.example.com" 
        width="600" height="400"
        title="Example Website"></iframe>

<!-- Embed YouTube video -->
<iframe width="560" height="315"
        src="https://www.youtube.com/embed/VIDEO_ID"
        title="YouTube video"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen></iframe>

<!-- Embed Google Maps -->
<iframe src="https://www.google.com/maps/embed?..."
        width="600" height="450"
        style="border:0;"
        allowfullscreen=""
        loading="lazy"></iframe>
```

### Canvas

```html
<canvas id="myCanvas" width="400" height="200">
    Your browser does not support the canvas element.
</canvas>

<script>
    var canvas = document.getElementById('myCanvas');
    var ctx = canvas.getContext('2d');
    ctx.fillStyle = 'blue';
    ctx.fillRect(10, 10, 100, 100);
</script>
```

### SVG

```html
<!-- Inline SVG -->
<svg width="100" height="100">
    <circle cx="50" cy="50" r="40" 
            stroke="black" stroke-width="3" fill="red" />
</svg>

<!-- SVG as image -->
<img src="graphic.svg" alt="SVG graphic">

<!-- SVG with object -->
<object data="graphic.svg" type="image/svg+xml"></object>
```

---

## 📊 HTML Tables

### Basic Table Structure

```html
<table>
    <caption>Monthly Sales Report</caption>
    <thead>
        <tr>
            <th>Month</th>
            <th>Sales</th>
            <th>Revenue</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>January</td>
            <td>100</td>
            <td>$10,000</td>
        </tr>
        <tr>
            <td>February</td>
            <td>120</td>
            <td>$12,000</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Total</td>
            <td>220</td>
            <td>$22,000</td>
        </tr>
    </tfoot>
</table>
```

### Table with Colspan and Rowspan

```html
<table border="1">
    <tr>
        <th>Name</th>
        <th colspan="2">Contact</th>
    </tr>
    <tr>
        <td>John</td>
        <td>Email</td>
        <td>Phone</td>
    </tr>
    <tr>
        <td>Jane</td>
        <td colspan="2">jane@example.com | 123-456-7890</td>
    </tr>
</table>

<table border="1">
    <tr>
        <th rowspan="2">Name</th>
        <th colspan="2">Details</th>
    </tr>
    <tr>
        <td>Age</td>
        <td>City</td>
    </tr>
    <tr>
        <td>John</td>
        <td>25</td>
        <td>New York</td>
    </tr>
</table>
```

### Accessible Table

```html
<table>
    <caption>Student Grades</caption>
    <thead>
        <tr>
            <th scope="col" id="name">Name</th>
            <th scope="col" id="math">Math</th>
            <th scope="col" id="science">Science</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row" headers="name">John</th>
            <td headers="name math">85</td>
            <td headers="name science">90</td>
        </tr>
        <tr>
            <th scope="row" headers="name">Jane</th>
            <td headers="name math">92</td>
            <td headers="name science">88</td>
        </tr>
    </tbody>
</table>
```

### Column Groups

```html
<table>
    <colgroup>
        <col style="background-color: #f0f0f0;">
        <col span="2" style="background-color: #e0e0e0;">
    </colgroup>
    <tr>
        <th>Name</th>
        <th>Q1</th>
        <th>Q2</th>
    </tr>
    <tr>
        <td>Sales</td>
        <td>$10k</td>
        <td>$15k</td>
    </tr>
</table>
```

---

## 🎨 Semantic HTML

### Why Semantic HTML?

1. **Accessibility** - Screen readers understand structure
2. **SEO** - Search engines prioritize semantic tags
3. **Maintainability** - Easier to read and maintain
4. **Standardization** - Universal understanding

### Semantic vs Non-Semantic

```html
<!-- ❌ Non-Semantic -->
<div id="header">
    <div id="nav">
        <a href="/">Home</a>
    </div>
</div>
<div id="main">
    <div class="article">
        <div class="title">Article Title</div>
        <div class="content">Content here</div>
    </div>
</div>
<div id="footer">Footer</div>

<!-- ✅ Semantic -->
<header>
    <nav>
        <a href="/">Home</a>
    </nav>
</header>
<main>
    <article>
        <h1>Article Title</h1>
        <p>Content here</p>
    </article>
</main>
<footer>Footer</footer>
```

### Complete Semantic Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Semantic Example</title>
</head>
<body>
    <header>
        <h1>Website Title</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <article>
            <header>
                <h2>Article Title</h2>
                <p>Published on <time datetime="2024-01-01">January 1, 2024</time></p>
                <address>By <a href="mailto:author@example.com">Author Name</a></address>
            </header>
            
            <section>
                <h3>Introduction</h3>
                <p>Content here...</p>
            </section>
            
            <section>
                <h3>Main Points</h3>
                <p>More content...</p>
            </section>
            
            <footer>
                <p>Article footer information</p>
            </footer>
        </article>
        
        <aside>
            <h3>Related Articles</h3>
            <ul>
                <li><a href="#">Article 1</a></li>
                <li><a href="#">Article 2</a></li>
            </ul>
        </aside>
    </main>
    
    <footer>
        <p>&copy; 2024 Company Name. All rights reserved.</p>
        <nav>
            <a href="#privacy">Privacy</a> |
            <a href="#terms">Terms</a>
        </nav>
    </footer>
</body>
</html>
```

### Semantic Tag Usage Guide

| Tag | Purpose | When to Use |
|-----|---------|-------------|
| `<header>` | Introductory content | Top of page/section |
| `<nav>` | Navigation links | Main menu, breadcrumbs |
| `<main>` | Main content | Primary content (once) |
| `<article>` | Independent content | Blog posts, news articles |
| `<section>` | Thematic grouping | Chapters, tabs |
| `<aside>` | Tangential content | Sidebars, related info |
| `<footer>` | Closing content | Bottom of page/section |
| `<figure>` | Self-contained media | Images with captions |
| `<time>` | Date/time | Dates, timestamps |
| `<mark>` | Highlighted text | Search results |
| `<address>` | Contact info | Author/owner details |

---

## 🔍 SEO Basics & Meta Tags

### Essential Meta Tags

```html
<head>
    <!-- Character encoding -->
    <meta charset="UTF-8">
    
    <!-- Viewport for responsive design -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- Title (very important for SEO) -->
    <title>Page Title - Site Name | 50-60 characters</title>
    
    <!-- Meta description -->
    <meta name="description" content="Concise description of page content. 150-160 characters recommended.">
    
    <!-- Keywords (less important now) -->
    <meta name="keywords" content="keyword1, keyword2, keyword3">
    
    <!-- Author -->
    <meta name="author" content="Author Name">
    
    <!-- Robots (search engine crawling) -->
    <meta name="robots" content="index, follow">
    
    <!-- Canonical URL -->
    <link rel="canonical" href="https://example.com/page">
    
    <!-- Language -->
    <meta http-equiv="content-language" content="en-US">
</head>
```

### Open Graph (Social Media)

```html
<!-- Open Graph for Facebook, LinkedIn -->
<meta property="og:title" content="Page Title">
<meta property="og:description" content="Page description">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:url" content="https://example.com/page">
<meta property="og:type" content="website">
<meta property="og:site_name" content="Site Name">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@username">
<meta name="twitter:title" content="Page Title">
<meta name="twitter:description" content="Page description">
<meta name="twitter:image" content="https://example.com/image.jpg">
```

### Favicon

```html
<!-- Standard favicon -->
<link rel="icon" type="image/x-icon" href="/favicon.ico">

<!-- PNG favicon -->
<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">

<!-- Apple Touch Icon -->
<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">

<!-- Android -->
<link rel="manifest" href="/site.webmanifest">
```

### Structured Data (Schema.org)

```html
<!-- JSON-LD structured data -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Article Title",
  "author": {
    "@type": "Person",
    "name": "Author Name"
  },
  "datePublished": "2024-01-01",
  "image": "https://example.com/image.jpg",
  "publisher": {
    "@type": "Organization",
    "name": "Publisher Name",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.jpg"
    }
  }
}
</script>
```

### SEO Best Practices

1. **Heading Hierarchy**
   ```html
   <h1>Main Title (one per page)</h1>
     <h2>Section Title</h2>
       <h3>Subsection</h3>
   ```

2. **Alt Text for Images**
   ```html
   <img src="image.jpg" alt="Descriptive text for SEO and accessibility">
   ```

3. **Descriptive URLs**
   ```
   ✅ /articles/html-guide
   ❌ /page?id=123
   ```

4. **Internal Linking**
   ```html
   <a href="/related-article">Related Article Title</a>
   ```

5. **Mobile-Friendly**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

---

## ♿ Accessibility (ARIA)

### ARIA Basics

**ARIA (Accessible Rich Internet Applications)** helps make web content accessible to people with disabilities.

### ARIA Roles

```html
<!-- Landmark roles -->
<header role="banner">
<nav role="navigation">
<main role="main">
<aside role="complementary">
<footer role="contentinfo">
<form role="search">

<!-- Widget roles -->
<div role="button">Click me</div>
<div role="tab">Tab 1</div>
<div role="tabpanel">Tab content</div>
<div role="dialog">Modal content</div>
<div role="alert">Important message</div>
<div role="progressbar" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">

<!-- Document structure roles -->
<div role="article">
<div role="list">
<div role="listitem">
```

### ARIA Attributes

#### aria-label & aria-labelledby

```html
<!-- aria-label: Provides accessible name -->
<button aria-label="Close dialog">×</button>

<!-- aria-labelledby: References another element -->
<h2 id="dialog-title">Confirm Action</h2>
<div role="dialog" aria-labelledby="dialog-title">
    Content here
</div>
```

#### aria-describedby

```html
<input type="email" aria-describedby="email-help">
<span id="email-help">We'll never share your email</span>
```

#### aria-hidden

```html
<!-- Hide decorative elements from screen readers -->
<span aria-hidden="true">🎉</span>
<span class="sr-only">Celebration icon</span>
```

#### aria-expanded & aria-controls

```html
<button aria-expanded="false" aria-controls="menu">
    Menu
</button>
<ul id="menu" hidden>
    <li>Item 1</li>
    <li>Item 2</li>
</ul>
```

#### aria-live

```html
<!-- Announce dynamic content changes -->
<div aria-live="polite" aria-atomic="true">
    Loading...
</div>

<!-- aria-live values: off, polite, assertive -->
```

#### aria-required & aria-invalid

```html
<input type="text" aria-required="true" aria-invalid="false">
```

### Complete Accessible Form Example

```html
<form>
    <div>
        <label for="username">Username:</label>
        <input type="text" 
               id="username" 
               name="username"
               aria-required="true"
               aria-describedby="username-help"
               aria-invalid="false">
        <span id="username-help">Must be 3-20 characters</span>
        <span id="username-error" role="alert" aria-live="polite"></span>
    </div>
    
    <fieldset>
        <legend>Select your plan</legend>
        <label>
            <input type="radio" name="plan" value="basic">
            Basic Plan
        </label>
        <label>
            <input type="radio" name="plan" value="pro">
            Pro Plan
        </label>
    </fieldset>
    
    <button type="submit" aria-label="Submit registration form">
        Submit
    </button>
</form>
```

### Accessible Navigation

```html
<nav aria-label="Main navigation">
    <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

### Skip Links

```html
<a href="#main-content" class="skip-link">Skip to main content</a>

<main id="main-content">
    <!-- Main content -->
</main>

<style>
.skip-link {
    position: absolute;
    top: -40px;
    left: 0;
    background: #000;
    color: #fff;
    padding: 8px;
}
.skip-link:focus {
    top: 0;
}
</style>
```

### Accessibility Checklist

- [ ] Use semantic HTML
- [ ] Provide alt text for images
- [ ] Use proper heading hierarchy
- [ ] Ensure sufficient color contrast
- [ ] Make interactive elements keyboard accessible
- [ ] Provide focus indicators
- [ ] Use ARIA when HTML semantics aren't enough
- [ ] Test with screen readers
- [ ] Ensure form inputs have labels
- [ ] Provide text alternatives for non-text content

---

## ✅ HTML Best Practices

### 1. Document Structure

```html
<!-- ✅ Good -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Descriptive Title</title>
</head>
<body>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
</body>
</html>

<!-- ❌ Bad -->
<html>
<head>
    <title>Title</title>
</head>
<body>
    <div id="header">...</div>
    <div id="content">...</div>
    <div id="footer">...</div>
</body>
</html>
```

### 2. Use Semantic Tags

```html
<!-- ✅ Good -->
<article>
    <h2>Article Title</h2>
    <p>Content...</p>
</article>

<!-- ❌ Bad -->
<div class="article">
    <div class="title">Article Title</div>
    <div class="content">Content...</div>
</div>
```

### 3. Proper Nesting

```html
<!-- ✅ Good -->
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
</ul>

<!-- ❌ Bad -->
<ul>
    <div>Item 1</div>
    <div>Item 2</div>
</ul>
```

### 4. Close Tags Properly

```html
<!-- ✅ Good -->
<p>Paragraph</p>
<img src="image.jpg" alt="Description">
<br>

<!-- ❌ Bad -->
<p>Paragraph
<img src="image.jpg">
<br></br>
```

### 5. Use Lowercase

```html
<!-- ✅ Good -->
<div class="container">
    <p>Content</p>
</div>

<!-- ❌ Bad -->
<DIV CLASS="container">
    <P>Content</P>
</DIV>
```

### 6. Quote Attribute Values

```html
<!-- ✅ Good -->
<img src="image.jpg" alt="Description">

<!-- ❌ Bad -->
<img src=image.jpg alt=Description>
```

### 7. Always Include Alt Text

```html
<!-- ✅ Good -->
<img src="logo.png" alt="Company Logo">
<img src="decorative.png" alt="">

<!-- ❌ Bad -->
<img src="logo.png">
```

### 8. Use Labels with Form Inputs

```html
<!-- ✅ Good -->
<label for="email">Email:</label>
<input type="email" id="email" name="email">

<!-- ❌ Bad -->
<input type="email" name="email">
```

### 9. Avoid Inline Styles

```html
<!-- ✅ Good -->
<p class="highlight">Text</p>

<!-- ❌ Bad -->
<p style="color: red; font-size: 16px;">Text</p>
```

### 10. Keep HTML Clean

```html
<!-- ✅ Good -->
<div class="container">
    <p>Content</p>
</div>

<!-- ❌ Bad -->
<div class="container">
    
    
    <p>Content</p>
    
    
</div>
```

### 11. External CSS and JavaScript

```html
<!-- ✅ Good -->
<link rel="stylesheet" href="styles.css">
<script src="script.js"></script>

<!-- ❌ Bad -->
<style>
    /* CSS here */
</style>
<script>
    // JavaScript here
</script>
```

### 12. Validate Your HTML

Use validators:
- W3C Markup Validation Service
- Browser DevTools
- Online validators

---

## 🚫 Deprecated Tags

These tags are **no longer supported** in HTML5. Use CSS instead.

### Deprecated Tags List

| Tag | Use Instead | Example |
|-----|-------------|---------|
| `<acronym>` | `<abbr>` | `<abbr title="World Wide Web">WWW</abbr>` |
| `<applet>` | `<object>` or `<embed>` | `<object data="app.swf"></object>` |
| `<basefont>` | CSS `font` | `body { font-family: Arial; }` |
| `<big>` | CSS `font-size` | `.big { font-size: larger; }` |
| `<center>` | CSS `text-align` | `.center { text-align: center; }` |
| `<dir>` | `<ul>` | `<ul><li>Item</li></ul>` |
| `<font>` | CSS `font` | `.custom { font-family: Arial; color: red; }` |
| `<frame>` | `<iframe>` or CSS | `<iframe src="page.html"></iframe>` |
| `<frameset>` | CSS layout | Use Flexbox/Grid |
| `<noframes>` | Remove | Not needed |
| `<strike>` | CSS or `<del>` | `.strike { text-decoration: line-through; }` |
| `<tt>` | CSS or `<code>` | `.monospace { font-family: monospace; }` |
| `<u>` | CSS `text-decoration` | `.underline { text-decoration: underline; }` |
| `<marquee>` | CSS animations | Use `@keyframes` |
| `<blink>` | CSS animations | Use `@keyframes` |

### Migration Examples

#### Font Tag → CSS

```html
<!-- ❌ Deprecated -->
<font color="red" face="Arial" size="3">Text</font>

<!-- ✅ Modern -->
<span class="styled-text">Text</span>
<style>
.styled-text {
    color: red;
    font-family: Arial;
    font-size: 16px;
}
</style>
```

#### Center Tag → CSS

```html
<!-- ❌ Deprecated -->
<center>Centered text</center>

<!-- ✅ Modern -->
<div class="centered">Centered text</div>
<style>
.centered {
    text-align: center;
}
</style>
```

---

## 🎓 Stair-Wise Micro-Learning Drills

### Level 1: HTML Basics

#### Exercise 1.1: Create Your First HTML Page

**Task:** Create a basic HTML page with title and heading.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My First Page</title>
</head>
<body>
    <h1>Welcome to HTML!</h1>
    <p>This is my first webpage.</p>
</body>
</html>
```

**Common Mistakes:**
- Forgetting `<!DOCTYPE html>`
- Not closing tags properly
- Missing `<meta charset="UTF-8">`

**Practice Task:**
Create a page about yourself with:
- A main heading with your name
- 3 paragraphs about your hobbies
- A subheading for each hobby

---

#### Exercise 1.2: Working with Headings

**Concept:** HTML has 6 heading levels (h1-h6).

```html
<h1>Main Title</h1>
<h2>Section</h2>
<h3>Subsection</h3>
<h4>Sub-subsection</h4>
<h5>Minor heading</h5>
<h6>Smallest heading</h6>
```

**Rules:**
- Only ONE `<h1>` per page
- Don't skip levels (h1 → h3 ❌)
- Use for structure, not styling

**Practice Task:**
Create a table of contents structure for a book:
- Book title (h1)
- Chapter titles (h2)
- Section titles (h3)

**Interview Q&A:**

**Q: Why use only one h1 per page?**
**A:** For SEO and accessibility. The h1 represents the main topic of the page and helps search engines and screen readers understand page structure.

---

#### Exercise 1.3: Text Formatting

**Concept:** Format text with semantic meaning.

```html
<!-- Bold (strong importance) -->
<strong>Important text</strong>

<!-- Italic (emphasis) -->
<em>Emphasized text</em>

<!-- Mark/Highlight -->
<mark>Highlighted text</mark>

<!-- Small print -->
<small>Fine print</small>

<!-- Deleted text -->
<del>Removed text</del>

<!-- Inserted text -->
<ins>Added text</ins>

<!-- Subscript -->
H<sub>2</sub>O

<!-- Superscript -->
X<sup>2</sup>
```

**Practice Task:**
Create a document showing:
- A mathematical formula with subscript/superscript
- Highlighted important terms
- Deleted and inserted text (like tracking changes)

---

### Level 2: Links and Images

#### Exercise 2.1: Creating Links

**Concept:** Links connect web pages.

```html
<!-- External link -->
<a href="https://www.google.com">Google</a>

<!-- Internal link -->
<a href="/about.html">About Us</a>

<!-- Open in new tab -->
<a href="https://www.google.com" target="_blank">Google</a>

<!-- Email link -->
<a href="mailto:info@example.com">Email Us</a>

<!-- Phone link -->
<a href="tel:+1234567890">Call Us</a>

<!-- Link to section -->
<a href="#section1">Go to Section 1</a>
<h2 id="section1">Section 1</h2>
```

**Practice Task:**
Create a navigation menu with:
- Home link
- About page link (opens in same tab)
- Contact email link
- Phone number link
- Links to 3 sections on the same page

**Interview Q&A:**

**Q: What's the difference between absolute and relative URLs?**
**A:** 
- Absolute: `https://example.com/page.html` (full URL)
- Relative: `/page.html` or `../page.html` (relative to current page)

**Q: When should you use target="_blank"?**
**A:** When linking to external sites or documents that users might want to reference while staying on your site. Always add `rel="noopener noreferrer"` for security.

---

#### Exercise 2.2: Working with Images

**Concept:** Display images on your page.

```html
<!-- Basic image -->
<img src="photo.jpg" alt="Description">

<!-- With dimensions -->
<img src="photo.jpg" alt="Description" width="300" height="200">

<!-- Lazy loading -->
<img src="photo.jpg" alt="Description" loading="lazy">

<!-- Image with figure -->
<figure>
    <img src="photo.jpg" alt="Sunset">
    <figcaption>Beautiful sunset in Hawaii</figcaption>
</figure>
```

**Common Mistakes:**
- Missing alt attribute
- Using wrong image format
- Not optimizing image size
- Missing width/height (causes layout shift)

**Practice Task:**
Create a photo gallery with:
- 6 images in a grid
- Each with descriptive alt text
- Use figure/figcaption for 3 of them
- Add captions

---

### Level 3: Lists and Tables

#### Exercise 3.1: Lists

**Concept:** Organize content in lists.

```html
<!-- Unordered list -->
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<!-- Ordered list -->
<ol>
    <li>First step</li>
    <li>Second step</li>
    <li>Third step</li>
</ol>

<!-- Nested lists -->
<ul>
    <li>Fruits
        <ul>
            <li>Apple</li>
            <li>Banana</li>
        </ul>
    </li>
    <li>Vegetables
        <ul>
            <li>Carrot</li>
            <li>Broccoli</li>
        </ul>
    </li>
</ul>

<!-- Description list -->
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language</dd>
    <dt>CSS</dt>
    <dd>Cascading Style Sheets</dd>
</dl>
```

**Practice Task:**
Create:
1. A to-do list (ordered)
2. A shopping list with categories (nested unordered)
3. A glossary of 5 web terms (description list)

---

#### Exercise 3.2: Tables

**Concept:** Display tabular data.

```html
<table>
    <caption>Student Grades</caption>
    <thead>
        <tr>
            <th>Name</th>
            <th>Math</th>
            <th>Science</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>John</td>
            <td>85</td>
            <td>90</td>
        </tr>
        <tr>
            <td>Jane</td>
            <td>92</td>
            <td>88</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Average</td>
            <td>88.5</td>
            <td>89</td>
        </tr>
    </tfoot>
</table>
```

**Practice Task:**
Create a table showing:
- Weekly schedule (days vs time slots)
- Use colspan for lunch break
- Use rowspan for multi-hour classes

---

### Level 4: Forms

#### Exercise 4.1: Basic Form

```html
<form action="/submit" method="POST">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="4"></textarea>
    
    <button type="submit">Submit</button>
</form>
```

**Practice Task:**
Create a registration form with:
- Username (text, required, 3-20 characters)
- Email (email, required)
- Password (password, required, min 8 characters)
- Confirm password (password, required)
- Age (number, 18-100)
- Terms agreement (checkbox, required)
- Submit button

---

#### Exercise 4.2: Advanced Form Elements

```html
<form>
    <!-- Radio buttons -->
    <fieldset>
        <legend>Gender</legend>
        <label><input type="radio" name="gender" value="male"> Male</label>
        <label><input type="radio" name="gender" value="female"> Female</label>
    </fieldset>
    
    <!-- Checkboxes -->
    <fieldset>
        <legend>Interests</legend>
        <label><input type="checkbox" name="interests" value="sports"> Sports</label>
        <label><input type="checkbox" name="interests" value="music"> Music</label>
    </fieldset>
    
    <!-- Select dropdown -->
    <label for="country">Country:</label>
    <select id="country" name="country">
        <option value="">Select...</option>
        <option value="us">United States</option>
        <option value="uk">United Kingdom</option>
    </select>
    
    <!-- Date -->
    <label for="birthdate">Birthdate:</label>
    <input type="date" id="birthdate" name="birthdate">
    
    <!-- File upload -->
    <label for="photo">Photo:</label>
    <input type="file" id="photo" name="photo" accept="image/*">
</form>
```

**Practice Task:**
Create a job application form with:
- Personal info section
- Education section (dropdown for degree)
- Skills (multiple checkboxes)
- Resume upload
- Preferred interview date

---

### Level 5: Semantic HTML

#### Exercise 5.1: Page Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Blog Post</title>
</head>
<body>
    <header>
        <h1>My Blog</h1>
        <nav>
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">About</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <article>
            <header>
                <h2>Article Title</h2>
                <p>Published on <time datetime="2024-01-01">Jan 1, 2024</time></p>
            </header>
            
            <section>
                <h3>Introduction</h3>
                <p>Content...</p>
            </section>
            
            <section>
                <h3>Main Points</h3>
                <p>Content...</p>
            </section>
        </article>
        
        <aside>
            <h3>Related Posts</h3>
            <ul>
                <li><a href="#">Post 1</a></li>
                <li><a href="#">Post 2</a></li>
            </ul>
        </aside>
    </main>
    
    <footer>
        <p>&copy; 2024 My Blog</p>
    </footer>
</body>
</html>
```

**Practice Task:**
Create a complete blog homepage with:
- Site header with logo and navigation
- Main section with 3 article previews
- Sidebar with categories
- Footer with social links

---

## 🎤 Interview Questions

### Easy Level

#### Q1: What is HTML?
**Answer:** HTML (HyperText Markup Language) is the standard markup language for creating web pages. It describes the structure and content of a webpage using elements represented by tags.

#### Q2: What is the difference between HTML and HTML5?
**Answer:** 
- HTML5 is the latest version of HTML
- Adds new semantic elements (header, nav, article, etc.)
- Introduces new input types and form features
- Supports multimedia (audio, video) without plugins
- Includes APIs for geolocation, drag-and-drop, local storage
- Better mobile support

#### Q3: What is a tag and an element?
**Answer:**
- **Tag:** The markup itself, e.g., `<p>` or `</p>`
- **Element:** The complete structure: `<p>Content</p>`
- Tags are the building blocks that create elements

#### Q4: What is an attribute?
**Answer:** An attribute provides additional information about an element. It's placed in the opening tag and consists of a name and value.
```html
<img src="image.jpg" alt="Description">
     ↑                ↑
  attribute       attribute
```

#### Q5: What is the difference between `<strong>` and `<b>`?
**Answer:**
- `<strong>` - Semantic emphasis, indicates importance
- `<b>` - Presentational, just bold styling
- Screen readers treat `<strong>` as important
- Prefer `<strong>` for meaningful emphasis

#### Q6: What is the difference between `<em>` and `<i>`?
**Answer:**
- `<em>` - Semantic emphasis, stress emphasis
- `<i>` - Presentational, just italic styling
- Use `<em>` for emphasis, `<i>` for technical terms, foreign words

#### Q7: What is semantic HTML?
**Answer:** Semantic HTML uses tags that convey meaning about the content they contain. Examples: `<header>`, `<nav>`, `<article>`, `<footer>`. Benefits include better SEO, accessibility, and maintainability.

#### Q8: What is the purpose of the `DOCTYPE` declaration?
**Answer:** `<!DOCTYPE html>` tells the browser which version of HTML the page is using. It must be the first line and ensures the browser renders the page in standards mode.

#### Q9: What is the difference between inline and block elements?
**Answer:**
- **Block:** Takes full width, starts on new line (div, p, h1)
- **Inline:** Takes only needed width, flows with text (span, a, strong)

#### Q10: What is the alt attribute used for?
**Answer:** The `alt` attribute provides alternative text for images. It's used when images can't load, by screen readers for accessibility, and by search engines for SEO.

---

### Medium Level

#### Q11: Explain the difference between `<section>`, `<article>`, and `<div>`.
**Answer:**
- `<div>` - Generic container, no semantic meaning
- `<section>` - Thematic grouping of content, usually with a heading
- `<article>` - Independent, self-contained content (blog post, news article)

**When to use:**
- Use `<article>` when content makes sense on its own
- Use `<section>` to group related content
- Use `<div>` for styling/layout without semantic meaning

#### Q12: What is the purpose of the `data-*` attribute?
**Answer:** Custom data attributes allow you to store extra information on HTML elements without using non-standard attributes or DOM properties.
```html
<div data-user-id="12345" data-role="admin">
```
Accessed in JavaScript: `element.dataset.userId`

#### Q13: Explain the different input types in HTML5.
**Answer:**
Text types: text, email, password, search, tel, url
Numbers: number, range
Date/Time: date, time, datetime-local, month, week
Selection: checkbox, radio, select
Others: file, color, hidden

Each provides:
- Built-in validation
- Appropriate mobile keyboards
- Better UX

#### Q14: What is the purpose of the `<meta>` tag?
**Answer:** Meta tags provide metadata about the HTML document. Common uses:
```html
<meta charset="UTF-8"> <!-- Character encoding -->
<meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- Responsive -->
<meta name="description" content="Page description"> <!-- SEO -->
<meta name="keywords" content="html, css"> <!-- SEO -->
```

#### Q15: What are void elements?
**Answer:** Void elements don't have closing tags and can't contain content. Examples:
```html
<br>, <hr>, <img>, <input>, <meta>, <link>, <area>, <base>, <col>, <embed>, <source>, <track>, <wbr>
```

#### Q16: Explain `colspan` and `rowspan` in tables.
**Answer:**
- `colspan` - Cell spans multiple columns
- `rowspan` - Cell spans multiple rows
```html
<table>
    <tr>
        <td colspan="2">Spans 2 columns</td>
    </tr>
    <tr>
        <td rowspan="2">Spans 2 rows</td>
        <td>Cell 1</td>
    </tr>
    <tr>
        <td>Cell 2</td>
    </tr>
</table>
```

#### Q17: What is the difference between `GET` and `POST` methods?
**Answer:**
**GET:**
- Data in URL
- Limited data size
- Bookmarkable
- Cached
- Use for retrieving data

**POST:**
- Data in request body
- Unlimited data size
- Not bookmarkable
- Not cached
- Use for submitting data

#### Q18: What is the purpose of `<meta name="viewport">`?
**Answer:** Controls how the page is displayed on mobile devices.
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
- `width=device-width` - Use device width
- `initial-scale=1.0` - Initial zoom level
- Essential for responsive design

#### Q19: Explain the difference between `<link>` and `<script>` placement.
**Answer:**
**CSS (link):**
- Place in `<head>`
- Prevents unstyled content flash
- Doesn't block rendering

**JavaScript (script):**
- Place before `</body>` or use `defer`/`async`
- Can block HTML parsing
- `defer` - Downloads in parallel, executes after HTML
- `async` - Downloads and executes immediately

#### Q20: What are semantic tags for forms?
**Answer:**
- `<form>` - Form container
- `<label>` - Input label (accessibility)
- `<fieldset>` - Group related inputs
- `<legend>` - Fieldset title
- `<datalist>` - Autocomplete options
- `<output>` - Calculation result

---

### Hard Level

#### Q21: Explain the Critical Rendering Path and how HTML affects it.
**Answer:** The Critical Rendering Path is the sequence of steps browsers take to render a page:
1. DOM Construction (parse HTML)
2. CSSOM Construction (parse CSS)
3. Render Tree (combine DOM + CSSOM)
4. Layout (calculate positions)
5. Paint (draw pixels)

**HTML optimizations:**
- Minimize HTML size
- Place CSS in `<head>`
- Place JS before `</body>` or use `defer`
- Avoid render-blocking resources
- Use lazy loading for images

#### Q22: What is the Shadow DOM?
**Answer:** Shadow DOM is part of Web Components that allows encapsulation of HTML, CSS, and JavaScript.
```html
<div id="host"></div>
<script>
const host = document.getElementById('host');
const shadow = host.attachShadow({mode: 'open'});
shadow.innerHTML = '<p>Shadow DOM content</p>';
</script>
```
**Benefits:**
- Style encapsulation
- DOM encapsulation
- Reusable components

#### Q23: Explain HTML validation and its importance.
**Answer:** HTML validation checks if markup follows W3C standards.

**Importance:**
- Cross-browser compatibility
- Better SEO
- Easier maintenance
- Fewer bugs
- Accessibility

**Tools:**
- W3C Markup Validation Service
- Browser DevTools
- Build tools (HTMLHint, etc.)

#### Q24: What is the difference between `localStorage`, `sessionStorage`, and cookies?
**Answer:**
| Feature | localStorage | sessionStorage | Cookies |
|---------|-------------|----------------|---------|
| Capacity | 5-10MB | 5-10MB | 4KB |
| Lifetime | Permanent | Session | Set expiry |
| Sent to server | No | No | Yes |
| Accessibility | All tabs | Same tab | All requests |

#### Q25: Explain ARIA and its role in accessibility.
**Answer:** ARIA (Accessible Rich Internet Applications) provides additional semantic information for screen readers.

**ARIA attributes:**
- `role` - Define element purpose
- `aria-label` - Accessible name
- `aria-labelledby` - Reference label
- `aria-describedby` - Additional description
- `aria-hidden` - Hide from screen readers
- `aria-live` - Announce dynamic changes

**Example:**
```html
<button aria-label="Close dialog" aria-pressed="false">
    ×
</button>
```

#### Q26: What are Web Components?
**Answer:** Web Components are reusable custom elements with encapsulated functionality.

**Technologies:**
1. Custom Elements
2. Shadow DOM
3. HTML Templates
4. ES Modules

**Example:**
```html
<template id="my-component">
    <style>p { color: blue; }</style>
    <p>Component content</p>
</template>

<script>
class MyComponent extends HTMLElement {
    constructor() {
        super();
        const template = document.getElementById('my-component');
        const clone = template.content.cloneNode(true);
        this.attachShadow({mode: 'open'}).appendChild(clone);
    }
}
customElements.define('my-component', MyComponent);
</script>

<my-component></my-component>
```

#### Q27: Explain Content Security Policy (CSP) in HTML.
**Answer:** CSP is a security layer that helps prevent XSS attacks by controlling which resources can be loaded.

```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; img-src 'self' https:; script-src 'self'">
```

**Directives:**
- `default-src` - Default policy
- `script-src` - JavaScript sources
- `style-src` - CSS sources
- `img-src` - Image sources
- `connect-src` - AJAX/WebSocket sources

#### Q28: What is Progressive Enhancement vs Graceful Degradation?
**Answer:**
**Progressive Enhancement:**
- Start with basic HTML (works everywhere)
- Add CSS for styling
- Add JavaScript for interactivity
- Ensures baseline functionality

**Graceful Degradation:**
- Build for modern browsers first
- Add fallbacks for older browsers
- May not work without features

**Example:**
```html
<!-- Progressive Enhancement -->
<a href="/search?q=term">Search</a>
<script>
    // Enhance with JavaScript
    document.querySelector('a').addEventListener('click', function(e) {
        e.preventDefault();
        // AJAX search
    });
</script>
```

#### Q29: Explain the Picture element and responsive images.
**Answer:** `<picture>` provides art direction for responsive images.

```html
<picture>
    <!-- Desktop: landscape -->
    <source media="(min-width: 800px)" srcset="landscape.jpg">
    
    <!-- Tablet: square -->
    <source media="(min-width: 400px)" srcset="square.jpg">
    
    <!-- Mobile: portrait -->
    <img src="portrait.jpg" alt="Responsive image">
</picture>
```

**vs `srcset`:**
- `<picture>` - Different images (art direction)
- `srcset` - Same image, different resolutions

#### Q30: What are microdata, RDFa, and JSON-LD?
**Answer:** Structured data formats for search engines.

**Microdata:**
```html
<div itemscope itemtype="http://schema.org/Person">
    <span itemprop="name">John Doe</span>
</div>
```

**RDFa:**
```html
<div vocab="http://schema.org/" typeof="Person">
    <span property="name">John Doe</span>
</div>
```

**JSON-LD (Recommended):**
```html
<script type="application/ld+json">
{
    "@context": "http://schema.org",
    "@type": "Person",
    "name": "John Doe"
}
</script>
```

---

## 🐛 Debugging Challenges

### Challenge 1: Find the Error

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Test Page
</head>
<body>
    <h1>Welcome</h1>
    <p>This is a paragraph
    <div>
        <p>Nested paragraph</p>
    </div>
</body>
</html>
```

**Errors:**
1. Missing `</title>`
2. Missing `</p>`
3. `<div>` inside `<p>` (invalid nesting)

**Corrected:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Test Page</title>
</head>
<body>
    <h1>Welcome</h1>
    <p>This is a paragraph</p>
    <div>
        <p>Nested paragraph</p>
    </div>
</body>
</html>
```

---

### Challenge 2: Accessibility Issues

```html
<form>
    <input type="text" placeholder="Username">
    <input type="password" placeholder="Password">
    <button>Submit</button>
</form>

<img src="logo.png">

<div onclick="handleClick()">Click me</div>
```

**Issues:**
1. Missing labels for inputs
2. Missing alt attribute on image
3. Non-semantic button (should use `<button>` instead of `<div>`)

**Corrected:**
```html
<form>
    <label for="username">Username:</label>
    <input type="text" id="username" placeholder="Username" required>
    
    <label for="password">Password:</label>
    <input type="password" id="password" placeholder="Password" required>
    
    <button type="submit">Submit</button>
</form>

<img src="logo.png" alt="Company Logo">

<button onclick="handleClick()">Click me</button>
```

---

### Challenge 3: Semantic Issues

```html
<div class="header">
    <div class="logo">Logo</div>
    <div class="nav">
        <span><a href="/">Home</a></span>
        <span><a href="/about">About</a></span>
    </div>
</div>

<div class="main">
    <div class="post">
        <div class="title">Post Title</div>
        <div class="content">Content here</div>
    </div>
</div>

<div class="footer">
    Copyright 2024
</div>
```

**Issues:**
1. Non-semantic structure
2. Using `<span>` in navigation
3. Using `<div>` for headings

**Corrected:**
```html
<header>
    <div class="logo">Logo</div>
    <nav>
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/about">About</a></li>
        </ul>
    </nav>
</header>

<main>
    <article>
        <h2>Post Title</h2>
        <p>Content here</p>
    </article>
</main>

<footer>
    <p>&copy; 2024</p>
</footer>
```

---

## 🚀 Real-World Mini Projects

### Project 1: Personal Portfolio Page

**Requirements:**
- Responsive layout
- Header with navigation
- About section
- Skills section (list)
- Projects section (grid of 3 projects)
- Contact form
- Footer with social links

**HTML Structure:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="John Doe - Web Developer Portfolio">
    <title>John Doe | Web Developer</title>
</head>
<body>
    <header>
        <h1>John Doe</h1>
        <nav>
            <ul>
                <li><a href="#about">About</a></li>
                <li><a href="#skills">Skills</a></li>
                <li><a href="#projects">Projects</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <section id="about">
            <h2>About Me</h2>
            <img src="profile.jpg" alt="John Doe" width="200">
            <p>I'm a passionate web developer...</p>
        </section>
        
        <section id="skills">
            <h2>Skills</h2>
            <ul>
                <li>HTML5 & CSS3</li>
                <li>JavaScript</li>
                <li>React</li>
                <li>Node.js</li>
            </ul>
        </section>
        
        <section id="projects">
            <h2>Projects</h2>
            <article>
                <h3>Project 1</h3>
                <img src="project1.jpg" alt="Project 1" width="300">
                <p>Description of project 1</p>
                <a href="#">View Project</a>
            </article>
            <article>
                <h3>Project 2</h3>
                <img src="project2.jpg" alt="Project 2" width="300">
                <p>Description of project 2</p>
                <a href="#">View Project</a>
            </article>
            <article>
                <h3>Project 3</h3>
                <img src="project3.jpg" alt="Project 3" width="300">
                <p>Description of project 3</p>
                <a href="#">View Project</a>
            </article>
        </section>
        
        <section id="contact">
            <h2>Contact Me</h2>
            <form action="/submit" method="POST">
                <label for="name">Name:</label>
                <input type="text" id="name" name="name" required>
                
                <label for="email">Email:</label>
                <input type="email" id="email" name="email" required>
                
                <label for="message">Message:</label>
                <textarea id="message" name="message" rows="5" required></textarea>
                
                <button type="submit">Send Message</button>
            </form>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2024 John Doe. All rights reserved.</p>
        <nav>
            <a href="https://github.com/johndoe">GitHub</a>
            <a href="https://linkedin.com/in/johndoe">LinkedIn</a>
            <a href="https://twitter.com/johndoe">Twitter</a>
        </nav>
    </footer>
</body>
</html>
```

---

### Project 2: Blog Post Page

**Requirements:**
- Article with proper semantic structure
- Author information
- Publication date
- Table of contents
- Related articles sidebar
- Comments section

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Learn HTML in 2024">
    <title>Complete HTML Guide | My Blog</title>
</head>
<body>
    <header>
        <h1>My Tech Blog</h1>
        <nav>
            <a href="/">Home</a>
            <a href="/blog">Blog</a>
            <a href="/about">About</a>
        </nav>
    </header>
    
    <main>
        <article>
            <header>
                <h2>Complete HTML Guide for Beginners</h2>
                <p>
                    Published on <time datetime="2024-01-15">January 15, 2024</time>
                    by <address><a href="/author/john">John Doe</a></address>
                </p>
            </header>
            
            <nav>
                <h3>Table of Contents</h3>
                <ul>
                    <li><a href="#intro">Introduction</a></li>
                    <li><a href="#basics">HTML Basics</a></li>
                    <li><a href="#advanced">Advanced Topics</a></li>
                </ul>
            </nav>
            
            <section id="intro">
                <h3>Introduction</h3>
                <p>HTML is the foundation of web development...</p>
            </section>
            
            <section id="basics">
                <h3>HTML Basics</h3>
                <p>Let's start with the fundamentals...</p>
            </section>
            
            <section id="advanced">
                <h3>Advanced Topics</h3>
                <p>Now let's explore advanced concepts...</p>
            </section>
            
            <footer>
                <p>Tags: <a href="/tag/html">HTML</a>, <a href="/tag/web-dev">Web Development</a></p>
            </footer>
        </article>
        
        <aside>
            <h3>Related Articles</h3>
            <ul>
                <li><a href="/article/css-guide">CSS Guide</a></li>
                <li><a href="/article/js-basics">JavaScript Basics</a></li>
                <li><a href="/article/responsive-design">Responsive Design</a></li>
            </ul>
        </aside>
        
        <section id="comments">
            <h3>Comments</h3>
            <article>
                <h4>Jane Smith</h4>
                <time datetime="2024-01-16">January 16, 2024</time>
                <p>Great article! Very helpful.</p>
            </article>
            <article>
                <h4>Bob Johnson</h4>
                <time datetime="2024-01-17">January 17, 2024</time>
                <p>Thanks for sharing!</p>
            </article>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2024 My Tech Blog</p>
    </footer>
</body>
</html>
```

---

### Project 3: Product Landing Page

**Requirements:**
- Hero section with CTA
- Features section
- Pricing table
- Testimonials
- Sign-up form

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Best project management tool">
    <title>TaskMaster - Project Management Tool</title>
</head>
<body>
    <header>
        <h1>TaskMaster</h1>
        <nav>
            <a href="#features">Features</a>
            <a href="#pricing">Pricing</a>
            <a href="#testimonials">Testimonials</a>
            <a href="#signup">Sign Up</a>
        </nav>
    </header>
    
    <main>
        <section id="hero">
            <h2>Manage Your Projects Effortlessly</h2>
            <p>The ultimate tool for team collaboration</p>
            <a href="#signup" class="cta-button">Get Started Free</a>
        </section>
        
        <section id="features">
            <h2>Features</h2>
            <article>
                <h3>Task Management</h3>
                <p>Organize tasks efficiently</p>
            </article>
            <article>
                <h3>Team Collaboration</h3>
                <p>Work together seamlessly</p>
            </article>
            <article>
                <h3>Real-time Updates</h3>
                <p>Stay in sync with your team</p>
            </article>
        </section>
        
        <section id="pricing">
            <h2>Pricing Plans</h2>
            <table>
                <thead>
                    <tr>
                        <th>Plan</th>
                        <th>Price</th>
                        <th>Features</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Free</td>
                        <td>$0/month</td>
                        <td>5 projects, 3 users</td>
                    </tr>
                    <tr>
                        <td>Pro</td>
                        <td>$29/month</td>
                        <td>Unlimited projects, 10 users</td>
                    </tr>
                    <tr>
                        <td>Enterprise</td>
                        <td>Custom</td>
                        <td>Everything + custom support</td>
                    </tr>
                </tbody>
            </table>
        </section>
        
        <section id="testimonials">
            <h2>What Our Customers Say</h2>
            <blockquote>
                <p>"TaskMaster transformed how our team works!"</p>
                <footer>— Sarah Johnson, CEO at TechCorp</footer>
            </blockquote>
            <blockquote>
                <p>"Best project management tool we've used."</p>
                <footer>— Mike Chen, Product Manager</footer>
            </blockquote>
        </section>
        
        <section id="signup">
            <h2>Start Your Free Trial</h2>
            <form action="/signup" method="POST">
                <label for="fullname">Full Name:</label>
                <input type="text" id="fullname" name="fullname" required>
                
                <label for="email">Email:</label>
                <input type="email" id="email" name="email" required>
                
                <label for="password">Password:</label>
                <input type="password" id="password" name="password" minlength="8" required>
                
                <label for="plan">Choose Plan:</label>
                <select id="plan" name="plan">
                    <option value="free">Free</option>
                    <option value="pro">Pro</option>
                    <option value="enterprise">Enterprise</option>
                </select>
                
                <label>
                    <input type="checkbox" name="terms" required>
                    I agree to the terms and conditions
                </label>
                
                <button type="submit">Sign Up</button>
            </form>
        </section>
    </main>
    
    <footer>
        <p>&copy; 2024 TaskMaster. All rights reserved.</p>
        <nav>
            <a href="/privacy">Privacy Policy</a>
            <a href="/terms">Terms of Service</a>
            <a href="/contact">Contact</a>
        </nav>
    </footer>
</body>
</html>
```

---

## 📋 Quick Revision Cheatsheet

### Common Tags Quick Reference

```html
<!-- Document Structure -->
<!DOCTYPE html>
<html lang="en">
<head>...</head>
<body>...</body>

<!-- Semantic Layout -->
<header>, <nav>, <main>, <article>, <section>, <aside>, <footer>

<!-- Headings -->
<h1> to <h6>

<!-- Text -->
<p>, <span>, <div>, <br>, <hr>

<!-- Formatting -->
<strong>, <em>, <mark>, <small>, <del>, <ins>, <sub>, <sup>

<!-- Links & Media -->
<a href="">, <img src="" alt="">, <audio>, <video>

<!-- Lists -->
<ul><li></li></ul>
<ol><li></li></ol>
<dl><dt></dt><dd></dd></dl>

<!-- Tables -->
<table>
  <thead><tr><th></th></tr></thead>
  <tbody><tr><td></td></tr></tbody>
  <tfoot><tr><td></td></tr></tfoot>
</table>

<!-- Forms -->
<form action="" method="">
  <label for=""></label>
  <input type="" id="" name="">
  <textarea></textarea>
  <select><option></option></select>
  <button type="submit"></button>
</form>
```

### Common Attributes

```html
<!-- Global -->
id, class, style, title, lang, dir, hidden, tabindex

<!-- Links -->
href, target, rel, download

<!-- Images -->
src, alt, width, height, loading

<!-- Forms -->
type, name, value, placeholder, required, disabled, readonly
maxlength, minlength, pattern, min, max, step

<!-- Tables -->
colspan, rowspan, scope

<!-- Media -->
src, controls, autoplay, loop, muted, poster
```

### Form Input Types

```
text, email, password, search, tel, url,
number, range,
date, time, datetime-local, month, week,
checkbox, radio, file, color, hidden,
submit, reset, button
```

### Semantic Tag Usage

```
<header>     - Top of page/section
<nav>        - Navigation menus
<main>       - Main content (once)
<article>    - Independent content
<section>    - Thematic grouping
<aside>      - Sidebar content
<footer>     - Bottom of page/section
<figure>     - Media with caption
<time>       - Dates/times
<address>    - Contact info
```

### SEO Essentials

```html
<title>50-60 characters</title>
<meta name="description" content="150-160 chars">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="canonical" href="">
<meta property="og:title" content="">
<img src="" alt="descriptive text">
<h1>One per page</h1>
```

### Accessibility Checklist

```
☐ Use semantic HTML
☐ Alt text for images
☐ Labels for form inputs
☐ Proper heading hierarchy (h1-h6)
☐ ARIA attributes when needed
☐ Keyboard navigation support
☐ Sufficient color contrast
☐ Focus indicators visible
☐ Skip links for navigation
☐ Test with screen readers
```

### Common Mistakes to Avoid

```
❌ Missing DOCTYPE
❌ No alt attribute on images
❌ Improper nesting
❌ Using div/span instead of semantic tags
❌ Multiple h1 tags
❌ Skipping heading levels
❌ Missing form labels
❌ Using deprecated tags
❌ Inline styles everywhere
❌ Not closing tags
❌ Missing meta viewport
```

### HTML5 New Features

```
• Semantic elements (header, nav, etc.)
• New input types (email, date, etc.)
• Audio & Video support
• Canvas & SVG
• Geolocation API
• Local Storage
• Drag and Drop
• Web Workers
• Form validation
• Placeholder attribute
```

---

## 🎓 Conclusion

### What You've Learned

✅ **HTML Fundamentals**
- Complete understanding of HTML structure
- All HTML tags and their usage
- Attributes and their purposes

✅ **Semantic HTML**
- Proper use of semantic elements
- Better structure and accessibility
- SEO optimization

✅ **Forms & Validation**
- All input types
- Form validation techniques
- Best practices for user input

✅ **Accessibility**
- ARIA roles and attributes
- Creating inclusive web experiences
- Testing for accessibility

✅ **Best Practices**
- Writing clean, maintainable HTML
- SEO optimization
- Performance considerations

✅ **Interview Preparation**
- Common interview questions
- Practical coding challenges
- Real-world scenarios

### Next Steps

1. **Practice Regularly**
   - Build real projects
   - Clone existing websites
   - Participate in coding challenges

2. **Learn CSS**
   - Style your HTML
   - Responsive design
   - CSS frameworks

3. **Add JavaScript**
   - Interactivity
   - Dynamic content
   - Modern frameworks

4. **Build Portfolio**
   - Showcase projects
   - Document your learning
   - Share on GitHub

5. **Keep Learning**
   - Stay updated with HTML Living Standard
   - Follow web development blogs
   - Join developer communities

### Resources

**Documentation:**
- MDN Web Docs (developer.mozilla.org)
- W3C HTML Specification
- HTML Living Standard (whatwg.org)

**Validation Tools:**
- W3C Markup Validation Service
- Browser DevTools
- Lighthouse (Chrome)

**Practice Platforms:**
- freeCodeCamp
- CodePen
- Codecademy
- Frontend Mentor

**Communities:**
- Stack Overflow
- Dev.to
- Reddit (r/webdev)
- Discord servers

---

## 🙏 Thank You

Thank you for using this HTML guide! Remember:

> "The best way to learn HTML is by building things. Start small, practice consistently, and gradually tackle more complex projects."

**Happy Coding! 🚀**

---

**Version:** 1.0  
**Last Updated:** 2024  
**Author:** AI Learning Guide

*This guide is open for contributions and improvements.*
Response
Created file /home/user/HTML_Complete_Guide.md (84825 characters)
