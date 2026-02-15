Here is the **HTML learning / development–focused explanation** of the **difference between iframe and Shadow DOM**, with detailed examples.

---

# Difference between iframe and Shadow DOM (HTML / Web Development Perspective)

Both **iframe** and **Shadow DOM** are used to isolate content, but they serve different purposes and work differently.

---

# 1. Definition

## iframe

An **iframe (Inline Frame)** is an HTML element used to embed another **separate webpage** inside the current webpage.

It creates a completely independent browsing context with its own:

* DOM
* CSS
* JavaScript
* URL

**Syntax:**

```html
<iframe src="https://example.com"></iframe>
```

---

## Shadow DOM

Shadow DOM is a browser feature that allows developers to create **encapsulated DOM inside an element**, mainly used for **Web Components**.

It hides internal structure and prevents CSS and JS conflicts.

**Syntax (JavaScript):**

```javascript
const element = document.querySelector("#host");
const shadowRoot = element.attachShadow({ mode: "open" });
shadowRoot.innerHTML = `<input type="text">`;
```

---

# 2. Real-world purpose

| iframe                           | Shadow DOM                          |
| -------------------------------- | ----------------------------------- |
| Embed external website           | Create reusable UI components       |
| Load independent page            | Encapsulate component structure     |
| Used for YouTube, maps, payments | Used in Web Components, Material UI |
| Full page isolation              | Component-level isolation           |

---

# 3. HTML Example of iframe

## Main page:

```html
<html>
<body>

<h2>Main Page</h2>

<iframe src="child.html" width="300" height="200"></iframe>

</body>
</html>
```

## child.html:

```html
<html>
<body>

<h3>This is inside iframe</h3>
<input type="text" id="username">

</body>
</html>
```

Here:

* child.html runs independently
* Separate DOM created

---

# 4. HTML Example of Shadow DOM

## Main HTML:

```html
<html>
<body>

<div id="host"></div>

<script>
const host = document.getElementById("host");

const shadow = host.attachShadow({ mode: "open" });

shadow.innerHTML = `
  <style>
    input { color: red; }
  </style>
  <input type="text" id="username">
`;

</script>

</body>
</html>
```

Here:

* Input is inside shadow DOM
* CSS does not affect main DOM

---

# 5. DOM Structure Comparison

## iframe DOM structure

```html
<html>
  <body>
    <iframe>
      #document
        <html>
          <body>
            <input>
```

It loads completely separate document.

---

## Shadow DOM structure

```html
<html>
  <body>
    <div id="host">
      #shadow-root
        <input>
```

It is attached to existing element.

---

# 6. Key Differences Table (Very important for interview)

| Feature             | iframe                   | Shadow DOM                    |
| ------------------- | ------------------------ | ----------------------------- |
| Purpose             | Embed external webpage   | Create encapsulated component |
| Isolation level     | Full document isolation  | Component isolation           |
| Loads separate URL  | Yes                      | No                            |
| Separate DOM        | Yes                      | Yes                           |
| Separate CSS        | Yes                      | Yes                           |
| Separate JavaScript | Yes                      | No separate JS environment    |
| Performance         | Slower                   | Faster                        |
| Used for            | YouTube, Payment gateway | Web Components, UI libraries  |
| Access method       | Switch to iframe         | Access shadow root            |
| Part of same page   | No                       | Yes                           |

---

# 7. Developer access example

## iframe access (JavaScript)

```javascript
const iframe = document.querySelector("iframe");

const iframeDoc = iframe.contentDocument;

const input = iframeDoc.getElementById("username");

input.value = "Krishna";
```

---

## Shadow DOM access (JavaScript)

```javascript
const host = document.querySelector("#host");

const shadowRoot = host.shadowRoot;

const input = shadowRoot.getElementById("username");

input.value = "Krishna";
```

---

# 8. Real-world examples

## iframe examples:

* YouTube video embed
* Google Maps embed
* Payment gateway (Razorpay, Stripe)

Example:

```html
<iframe src="https://www.youtube.com/embed/videoid"></iframe>
```

---

## Shadow DOM examples:

* Salesforce Lightning components
* Material UI components
* Custom Web Components

Example:

```html
<custom-button></custom-button>
```

Internally uses shadow DOM.

---

# 9. Testing perspective (Cypress example)

## iframe handling

```javascript
cy.get('iframe')
  .its('0.contentDocument.body')
  .find('#username')
  .type('Krishna')
```

---

## Shadow DOM handling

```javascript
cy.get('#host')
  .shadow()
  .find('#username')
  .type('Krishna')
```

---

# 10. Interview best answer (Recommended)

**iframe is an HTML element used to embed another webpage inside the current page, creating a completely separate browsing context with its own DOM, CSS, and JavaScript. Shadow DOM is a browser feature used to create encapsulated DOM inside an element for building reusable components. iframe is used for embedding external content like YouTube or payment pages, while Shadow DOM is used for Web Components and UI encapsulation.**

---

# 11. Simple real-life analogy

iframe = Like opening another website inside your website

Shadow DOM = Like creating a private room inside your house

