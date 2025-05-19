# HTML / CSS Notes

### **Module: HTTP Orientation**

---

### **HTTP Introduction**

- **What is HTTP?**
    
    HTTP (Hypertext Transfer Protocol) is a protocol used for transferring hypertext (text, images, videos, etc.) over the web. It is the foundation of any data exchange on the Web and a protocol used for communication between clients (browsers) and servers.
    
- **How HTTP works**:
    
    When a user enters a URL in their browser:
    
    1. The browser sends an HTTP request to the server.
    2. The server processes the request and returns an HTTP response.
    3. The browser renders the response (HTML, CSS, JavaScript, etc.).

---

### **HTTP Methods**

- **GET**:
    - Retrieves data from a server. It is used to fetch a resource without causing any side effects.
    - Example: `GET /index.html`
- **POST**:
    - Sends data to the server (e.g., form submissions).
    - Example: `POST /submit_form`
- **PUT**:
    - Replaces all current representations of a resource with the provided data.
    - Example: `PUT /user/1`
- **DELETE**:
    - Removes a resource.
    - Example: `DELETE /user/1`
- **PATCH**:
    - Applies partial modifications to a resource.
    - Example: `PATCH /user/1`

---

### **HTTP Status Codes**

### 1. **1xx: Informational Responses**

These codes indicate that the request has been received and is being processed.

- **100 Continue**: The initial part of the request has been received, and the client should continue sending the rest.
- **101 Switching Protocols**: The server is switching protocols according to the client’s request.

### 2. **2xx: Successful Responses**

These codes indicate that the request was successfully received, understood, and processed.

- **200 OK**: The request was successful, and the server returned the requested data.
- **201 Created**: The request was successful, and a new resource was created as a result.
- **202 Accepted**: The request has been accepted for processing, but it is not yet completed.
- **204 No Content**: The request was successful, but there is no content to return.

### 3. **3xx: Redirection**

These codes indicate that further action is needed to fulfill the request, usually a redirection.

- **301 Moved Permanently**: The requested resource has been permanently moved to a new URL.
- **302 Found**: The requested resource is temporarily located at a different URL.
- **304 Not Modified**: The resource has not been modified since the last request.

### 4. **4xx: Client Errors**

These codes indicate that there is an issue with the request sent by the client.

- **400 Bad Request**: The server cannot process the request due to client-side issues (e.g., malformed request).
- **401 Unauthorized**: The request lacks proper authentication.
- **403 Forbidden**: The server refuses to fulfill the request.
- **404 Not Found**: The requested resource could not be found on the server.
- **405 Method Not Allowed**: The method specified in the request is not allowed for the resource.
- **409 Conflict**: The request could not be completed due to a conflict with the current state of the resource.

### 5. **5xx: Server Errors**

These codes indicate that the server failed to fulfill a valid request.

- **500 Internal Server Error**: A generic error when the server encounters an unexpected condition.
- **502 Bad Gateway**: The server received an invalid response from an upstream server.
- **503 Service Unavailable**: The server is temporarily unavailable, usually due to overload or maintenance.
- **504 Gateway Timeout**: The server did not receive a timely response from an upstream server.

---

### **Module: HTML Foundation**

---

### **Overview of HTML**

- HTML (Hypertext Markup Language) is the standard language used for creating web pages.
- It structures content using elements like headings, paragraphs, links, images, and forms.

---

### **HTML Tags**

HTML (HyperText Markup Language) is used to structure content on the web. Tags are the building blocks of HTML and typically come in pairs: an opening tag and a closing tag. Here’s an overview of common HTML tags and their usage:

### 1. **Basic Structure Tags**

- `<html>`: Defines the root of an HTML document.
- `<head>`: Contains meta-information, links to stylesheets, scripts, etc.
- `<title>`: Specifies the title of the document, shown in the browser tab.
- `<body>`: Contains the main content of the document.
- `<meta>`: Provides metadata like the character set or description (usually inside `<head>`).

### 2. **Text Formatting Tags**

- `<h1>` to `<h6>`: Header tags, where `<h1>` is the most important heading and `<h6>` the least.
- `<p>`: Paragraph, used to define text blocks.
- `<br>`: Line break, moves content to the next line (self-closing).
- `<b>`: Bold text (semantic: `<strong>` is preferred).
- `<i>`: Italic text (semantic: `<em>` is preferred).
- `<strong>`: Defines important text, typically rendered in bold.
- `<em>`: Defines emphasized text, typically rendered in italics.
- `<u>`: Underlined text.

### 3. **Linking and Embedding Tags**

- `<a>`: Defines a hyperlink. It uses the `href` attribute to specify the destination.
    - Example: `<a href="https://example.com">Click Here</a>`
- `<img>`: Embeds an image, using the `src` attribute for the image URL and `alt` for alternative text (self-closing).
    - Example: `<img src="image.jpg" alt="Description of Image">`
- `<iframe>`: Embeds another HTML page within the current page.
    - Example: `<iframe src="https://example.com"></iframe>`
- `<video>`: Embeds a video.
    - Example: `<video src="movie.mp4" controls></video>`
- `<audio>`: Embeds an audio file.
    - Example: `<audio src="audio.mp3" controls></audio>`

### 4. **List Tags**

- `<ul>`: Unordered list (bulleted).
    - Example:
        
        ```html
        <ul>
          <li>Item 1</li>
          <li>Item 2</li>
        </ul>
        
        ```
        
- `<ol>`: Ordered list (numbered).
    - Example:
        
        ```html
        <ol>
          <li>First item</li>
          <li>Second item</li>
        </ol>
        
        ```
        
- `<li>`: List item, used inside `<ul>` or `<ol>`.

### 5. **Table Tags**

- `<table>`: Defines a table.
- `<tr>`: Defines a table row.
- `<td>`: Defines a table cell (data).
- `<th>`: Defines a table header cell, typically bold and centered.
- `<caption>`: Provides a title or description for the table.

### 7. **Division and Grouping Tags**

- `<div>`: Defines a section or container for HTML elements, used for layout and styling.
- `<span>`: A small container for inline elements, used for styling or grouping small chunks of content.

### 8. **Semantic Tags**

- `<header>`: Represents a header section for a document or section.
- `<footer>`: Represents a footer for a document or section.
- `<article>`: Represents a self-contained piece of content.
- `<section>`: Represents a section of content, typically with a header.
- `<aside>`: Represents content tangentially related to the content around it (e.g., sidebars).
- `<main>`: Represents the main content of the document.

### 9. **Meta and Link Tags (inside `<head>`)**

- `<link>`: Specifies relationships between the current document and external resources, commonly used for linking stylesheets.
    - Example: `<link rel="stylesheet" href="styles.css">`
- `<meta>`: Provides metadata about the document, like character encoding.
    - Example: `<meta charset="UTF-8">`

### 10. **Other Common Tags**

- `<hr>`: Creates a horizontal rule (line) in the page (self-closing).
- `<code>`: Defines inline code.
- `<pre>`: Defines preformatted text, preserving spaces and line breaks.
- `<blockquote>`: Defines a block of text that is a quotation.
- `<cite>`: Defines a citation or reference to a source.

---

### **HTML Document Structure and DOM**

An **HTML document** consists of a structure that tells the browser how to display the content. Here's the basic structure of an HTML document:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
    <!-- External stylesheets or scripts can be linked here -->
  </head>
  <body>
    <header>
      <h1>Welcome to My Website</h1>
    </header>
    <main>
      <p>This is a paragraph of text.</p>
      <p>Another paragraph of text.</p>
    </main>
    <footer>
      <p>&copy; 2024 My Website</p>
    </footer>
  </body>
</html>

```

### Key Components:

1. **`<!DOCTYPE html>`**: This declaration defines the document type and version of HTML. `<!DOCTYPE html>` tells the browser that this document is written in HTML5.
2. **`<html>`**: The root element that wraps the entire HTML document.
3. **`<head>`**: Contains metadata about the document (such as title, links to external files like CSS, JavaScript, and meta information).
    - **`<meta charset="UTF-8">`**: Specifies the character encoding (UTF-8 is widely used for international characters).
    - **`<meta name="viewport" content="width=device-width, initial-scale=1.0">`**: Helps with responsive design, making the page look good on different screen sizes.
4. **`<title>`**: The title of the document that appears in the browser’s title bar or tab.
5. **`<body>`**: Contains the content of the document (the visible part that users see in the browser).
6. **`<header>`, `<main>`, and `<footer>`**: Semantic HTML elements used to structure the page into distinct sections: the header, the main content, and the footer.

### **The DOM (Document Object Model)**

The **DOM** is a programming interface for HTML and XML documents. It represents the structure of a document as a tree of nodes, with each node corresponding to a part of the document (elements, attributes, text, etc.). The DOM allows programs and scripts to access and update the document’s content and structure dynamically.

### **How the DOM Works:**

- When a browser loads an HTML document, it parses the HTML code and constructs the DOM tree in memory.
- Each HTML element becomes a node in the DOM, and these nodes are arranged in a hierarchical structure.
- The DOM can be accessed and manipulated using JavaScript, which enables dynamic changes to the content, structure, and style of the page.

### **Example of the DOM:**

Given this HTML:

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="main">
      <h1>Hello, World!</h1>
      <p>This is a paragraph.</p>
    </div>
  </body>
</html>

```

The corresponding DOM structure would look like this:

```
- Document
  - html
    - body
      - div (id="main")
        - h1
          - "Hello, World!"
        - p
          - "This is a paragraph."

```

---

### **Elements and Attributes**

- **Element**: A tag and its content, e.g., `<p>Hello World</p>`.
- **Attribute**: Provides additional information about an element, e.g., `<img src="image.jpg" alt="Description">`.
    - Common attributes: `id`, `class`, `src`, `href`.

---

### **Inline and Block Elements**

- **Block elements**: Take up the full width available, starting on a new line. E.g., `<div>`, `<p>`, `<h1>`.
- **Inline elements**: Take up only as much width as necessary, without breaking the flow. E.g., `<span>`, `<a>`, `<img>`.

---

### **Module: HTML Forms**

---

### **Form Elements and Attributes**

- Forms are used to collect user input.
    - `<form>`: Defines the form.
    - `<input>`: Defines an input field (text, radio, etc.).
    - `<label>`: Defines a label for an input field.

---

### **Input Elements and Input Types**

- **Text Input**: `<input type="text">`
- **Password Input**: `<input type="password">`
- **Radio Buttons**: `<input type="radio">`
- **Checkbox**: `<input type="checkbox">`
- **Button**: `<input type="submit">`

---

### **Select and Multiselect**

- **Select**:
    - `<select>`: Creates a dropdown list.
    - Example:
        
        ```html
        <select>
            <option value="volvo">Volvo</option>
            <option value="saab">Saab</option>
            <option value="mercedes">Mercedes</option>
        </select>
        
        ```
        
- **Multiselect**:
    - `<select multiple>` allows multiple selections.

---

### **Submitting Forms**

- Forms can be submitted using a submit button:
    
    ```html
    <form action="submit_form.php" method="POST">
        <input type="text" name="username">
        <input type="submit" value="Submit">
    </form>
    ```
    

---

### **HTML5 Validation**

- HTML5 offers built-in form validation using attributes like `required`, `min`, `max`, `pattern`.
    - Example:
        
        ```html
        <form>
            <input type="text" name="username" required>
            <input type="email" name="email" required>
            <input type="submit">
        </form>
        
        ```
        

---

### **Module: CSS Foundation**

---

### **Overview of CSS**

- CSS (Cascading Style Sheets) is used to style the presentation of HTML content.
- It controls layout, color, fonts, and spacing of elements.

---

### **Inline, Internal, and External Styling**

- **Inline**: Directly in the HTML element using the `style` attribute.
    
    ```html
    <p style="color: blue;">Hello World</p>
    
    ```
    
- **Internal**: Within the `<style>` tag in the `<head>` section.
    
    ```html
    <style>
        p { color: blue; }
    </style>
    
    ```
    
- **External**: In a separate CSS file.
    
    ```html
    <link rel="stylesheet" href="styles.css">
    
    ```
    

---

### **CSS Properties**

- Common CSS properties include `color`, `font-size`, `margin`, `padding`, `border`, `background-color`, and `width`.

---

### **Element Selectors**

- Selects elements by their tag name.
    
    ```css
    p {
        color: blue;
    }
    
    ```
    

---

### **Class and ID Selectors**

- **Class Selector**: Selects elements with a specific class.
    
    ```css
    .my-class {
        color: green;
    }
    
    ```
    
- **ID Selector**: Selects an element with a specific ID.
    
    ```css
    #my-id {
        color: red;
    }
    
    ```
    

---

### **CSS Box Model**

- The box model defines the structure of elements: `content`, `padding`, `border`, and `margin`.
    - `width` and `height` define the content area.
    - `padding` adds space inside the element.
    - `border` surrounds the element.
    - `margin` adds space outside the element.

---

### **Module: CSS Depth**

---

### **Sibling Selectors**

- Selects elements that are siblings of a specified element.
    - Example:
        
        ```css
        h1 + p {
            color: red;
        }
        
        ```
        

---

### **Advanced Selectors**

- **Attribute Selector**: Selects elements with a specific attribute.
    
    ```css
    input[type="text"] {
        border: 1px solid black;
    }
    
    ```
    
- **Pseudo-classes**: E.g., `:hover`, `:focus`.
    
    ```css
    a:hover {
        color: green;
    }
    
    ```
    

---

### **Cascading Nature of CSS**

- CSS applies styles based on specificity, inheritance, and the source order of rules.

---

### **Specificity**

- Specificity determines which CSS rule is applied when there are conflicting styles. Inline styles have the highest specificity, followed by IDs, classes, and then element selectors.

---

### **Responsive Web Design**

- Ensures that web content adapts to different screen sizes.
    - Use media queries:
        
        ```css
        @media (max-width: 600px) {
            body {
                background-color: lightblue;
            }
        }
        
        ```
        

---

### **Module: CSS3 Features**

### **CSS Flexbox vs. CSS Grid**

Both **Flexbox** and **Grid** are powerful CSS layout models used to create responsive and modern web layouts. Each is designed for specific use cases but can often complement each other.

---

### **1. Flexbox (Flexible Box Layout)**

The **Flexbox** layout is designed for **one-dimensional layouts**, where items are arranged in a row or column.

### **Key Features**:

1. **Single Axis Layout**:
    - Works along a single axis (row or column).
2. **Dynamic Space Allocation**:
    - Distributes available space among items based on their flex properties.
3. **Alignment and Distribution**:
    - Simplifies alignment of items within a container, both horizontally and vertically.

### **When to Use**:

- Aligning items in a single direction (e.g., navigation bars, buttons).
- Creating flexible containers where content resizes dynamically.

---

### **Basic Flexbox Example**:

```html
<div class="flex-container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>

```

**CSS**:

```css
.flex-container {
  display: flex;
  justify-content: space-around; /* Distribute items with space between */
  align-items: center;          /* Align items vertically in the center */
  height: 200px;
}

.item {
  background-color: lightblue;
  padding: 20px;
  text-align: center;
}

```

---

### **Key Flexbox Properties**:

| **Property** | **Description** | **Values** |
| --- | --- | --- |
| `display` | Turns the container into a flex container. | `flex`, `inline-flex` |
| `flex-direction` | Defines the direction of the main axis. | `row`, `row-reverse`, `column`, `column-reverse` |
| `justify-content` | Aligns items along the main axis. | `flex-start`, `flex-end`, `center`, `space-between`, `space-around` |
| `align-items` | Aligns items along the cross axis. | `stretch`, `center`, `flex-start`, `flex-end`, `baseline` |
| `align-self` | Aligns a single item along the cross axis. | Same values as `align-items`. |
| `flex-wrap` | Allows items to wrap onto multiple lines. | `nowrap`, `wrap`, `wrap-reverse` |
| `flex` | Sets flex-grow, flex-shrink, and flex-basis. | `<grow> <shrink> <basis>` |
| `order` | Specifies the order of items. | `<integer>` (default: `0`) |

---

### **2. CSS Grid**

The **Grid** layout is designed for **two-dimensional layouts**, where items are arranged in rows and columns.

### **Key Features**:

1. **Two Axis Layout**:
    - Works on both rows and columns simultaneously.
2. **Explicit Placement**:
    - Items can be placed precisely in grid cells.
3. **Complex Layouts**:
    - Ideal for building entire page layouts or grid-based designs.

### **When to Use**:

- Creating structured layouts with rows and columns (e.g., dashboards, photo galleries).
- Designing complex layouts that require precise positioning.

---

### **Basic Grid Example**:

```html
<div class="grid-container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
  <div class="item">Item 4</div>
</div>

```

**CSS**:

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr); /* Two columns of equal width */
  gap: 10px;                            /* Space between items */
}

.item {
  background-color: lightcoral;
  padding: 20px;
  text-align: center;
}

```

---

### **Key Grid Properties**:

| **Property** | **Description** | **Values** |
| --- | --- | --- |
| `display` | Turns the container into a grid container. | `grid`, `inline-grid` |
| `grid-template-columns` | Defines column sizes in the grid. | e.g., `100px 200px`, `repeat(3, 1fr)` |
| `grid-template-rows` | Defines row sizes in the grid. | e.g., `auto`, `repeat(2, 50px)` |
| `gap` | Defines the spacing between rows and columns. | e.g., `10px`, `row-gap`, `column-gap` |
| `grid-column` | Specifies how many columns an item spans. | e.g., `span 2`, `1 / 3` |
| `grid-row` | Specifies how many rows an item spans. | e.g., `span 2`, `2 / 4` |
| `align-items` | Aligns items along the cross axis. | Same as in Flexbox. |
| `justify-items` | Aligns items along the main axis. | `start`, `end`, `center`, `stretch` |
| `place-items` | Shorthand for `align-items` and `justify-items`. | e.g., `center` |

---

### **3. Flexbox vs. Grid**

| **Aspect** | **Flexbox** | **Grid** |
| --- | --- | --- |
| **Layout** | One-dimensional (row or column). | Two-dimensional (row and column). |
| **Alignment** | Best for aligning items along a single axis. | Best for defining structured, grid-based layouts. |
| **Content-Based** | Layout adapts to the content dynamically. | Layout adapts to the grid structure. |
| **Use Case** | Navigation bars, buttons, single-axis layouts. | Dashboards, galleries, structured layouts. |

---

### **CSS Variables**

CSS Variables, also known as **custom properties**, allow you to define reusable values in your CSS. They are declared using the `--` syntax and can be used throughout your stylesheet to improve maintainability and consistency.

---

### **1. Syntax of CSS Variables**

### **Declaring a Variable**:

```css
:root {
  --main-color: #3498db;
  --font-size: 16px;
}

```

- Variables are often declared in the `:root` selector for global scope.
- `:root` is the highest-level selector in CSS, representing the HTML document.

### **Using a Variable**:

```css
h1 {
  color: var(--main-color);
  font-size: var(--font-size);
}

```

### **Fallback Values**:

You can provide a fallback value in case the variable is undefined:

```css
h1 {
  color: var(--secondary-color, #2ecc71); /* Uses #2ecc71 if --secondary-color is not set */
}

```

---

### **2. Advantages of CSS Variables**

1. **Reusability**:
    - Define once, use multiple times, reducing duplication.
2. **Maintainability**:
    - Centralized updates to variables cascade throughout the stylesheet.
3. **Dynamic Updates**:
    - Variables can be updated dynamically with JavaScript.
4. **Theming**:
    - Easily create light/dark themes by modifying variable values.

---

### **3. Scoping CSS Variables**

CSS Variables are scoped, meaning they follow the CSS cascade and inherit rules:

### **Global Variables**:

Declared in `:root` to make them accessible globally.

```css
:root {
  --primary-color: #e74c3c;
}
body {
  color: var(--primary-color);
}

```

### **Local Variables**:

Declared inside specific selectors and only available within that scope.

```css
.container {
  --bg-color: #f5f5f5;
}
.container div {
  background-color: var(--bg-color);
}

```

---

### Bootstrap

- **Bootstrap** is a front-end framework for responsive, mobile-first websites.
- It includes pre-defined CSS and JavaScript components like grids, buttons, navigation, and modals.
- Example:

```html
<button class="btn btn-primary">Primary Button</button>

```

---