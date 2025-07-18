# CSS Custom Properties (Variables) Cheatsheet

This repository provides a comprehensive guide to CSS Custom Properties (CSS Variables), a powerful feature for creating reusable, dynamic styles. From beginner-friendly variable declarations to advanced theming and JavaScript integration, this cheatsheet includes practical examples to help developers of all levels build scalable and maintainable CSS.

## Table of Contents
1. [Introduction to CSS Custom Properties](#introduction-to-css-custom-properties)
2. [Beginner Concepts](#beginner-concepts)
   - [Defining and Using Variables](#defining-and-using-variables)
   - [Scope of Variables](#scope-of-variables)
3. [Intermediate Concepts](#intermediate-concepts)
   - [Fallback Values](#fallback-values)
   - [Dynamic Updates with JavaScript](#dynamic-updates-with-javascript)
4. [Advanced Concepts](#advanced-concepts)
   - [Theming with Variables](#theming-with-variables)
   - [Responsive Design with Variables](#responsive-design-with-variables)
   - [Using calc() with Variables](#using-calc-with-variables)
   - [Inheritance and Specificity](#inheritance-and-specificity)
5. [Best Practices](#best-practices)
6. [Example Project](#example-project)
7. [Resources](#resources)

## Introduction to CSS Custom Properties
CSS Custom Properties, also known as CSS Variables, allow you to define reusable values that can be updated dynamically. They use the syntax `--variable-name` for declaration and `var(--variable-name)` for usage, making it easier to manage styles across a project.

## Beginner Concepts

### Defining and Using Variables
Custom properties are defined with a `--` prefix, typically in the `:root` pseudo-class for global scope, and accessed with the `var()` function.

**Example: Basic variable usage**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    :root {
      --primary-color: #3498db;
      --padding: 20px;
    }
    .box {
      background-color: var(--primary-color);
      padding: var(--padding);
    }
  </style>
</head>
<body>
  <div class="box">This box uses CSS variables for styling.</div>
</body>
</html>
```

### Scope of Variables
Variables can be defined globally (`:root`) or locally within a specific selector. Local variables override global ones for elements within their scope.

**Example: Local vs. global scope**
```css
:root {
  --text-color: black;
}
.card {
  --text-color: blue; /* Local override */
  color: var(--text-color);
}
.card p {
  color: var(--text-color); /* Inherits blue from .card */
}
```

## Intermediate Concepts

### Fallback Values
The `var()` function accepts a fallback value, used if the variable is undefined or invalid.

**Example: Fallback values**
```css
.box {
  background-color: var(--main-bg, #f0f0f0); /* Fallback to light gray */
  color: var(--text-color, red); /* Fallback to red */
}
```

### Dynamic Updates with JavaScript
CSS Variables can be updated dynamically using JavaScript, enabling real-time style changes.

**Example: JavaScript update**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    :root {
      --accent-color: #e74c3c;
    }
    .button {
      background-color: var(--accent-color);
      padding: 10px;
      border: none;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button class="button">Click Me</button>
  <script>
    document.querySelector('.button').addEventListener('click', () => {
      document.documentElement.style.setProperty('--accent-color', '#2ecc71');
    });
  </script>
</body>
</html>
```
Clicking the button changes the button’s background color dynamically.

## Advanced Concepts

### Theming with Variables
CSS Variables are ideal for creating themes (e.g., light/dark modes) by defining sets of variables and switching them.

**Example: Light and dark themes**
```css
:root {
  --bg-color: #ffffff;
  --text-color: #000000;
}
[data-theme="dark"] {
  --bg-color: #222222;
  --text-color: #ffffff;
}
body {
  background-color: var(--bg-color);
  color: var(--text-color);
}
```
```html
<button onclick="document.documentElement.setAttribute('data-theme', 'dark')">Switch to Dark Mode</button>
```

### Responsive Design with Variables
Combine variables with media queries to create responsive designs with reusable values.

**Example: Responsive font size**
```css
:root {
  --base-font-size: 16px;
}
@media screen and (max-width: 600px) {
  :root {
    --base-font-size: 14px;
  }
}
p {
  font-size: var(--base-font-size);
}
```

### Using calc() with Variables
Combine variables with `calc()` for dynamic calculations.

**Example: Calculated spacing**
```css
:root {
  --base-spacing: 10px;
}
.container {
  margin: calc(var(--base-spacing) * 2);
  padding: calc(var(--base-spacing) + 5px);
}
```

### Inheritance and Specificity
Variables inherit through the DOM tree and interact with CSS specificity. Local variables override global ones, and specificity determines which rule applies.

**Example: Specificity and variables**
```css
:root {
  --border-color: gray;
}
#special .box {
  --border-color: blue; /* Overrides for #special .box */
}
.box {
  border: 2px solid var(--border-color);
}
```

## Best Practices
- **Use Descriptive Names**: Name variables clearly (e.g., `--primary-color` instead of `--color1`).
- **Define Globally in :root**: Place reusable variables in `:root` for accessibility.
- **Provide Fallbacks**: Include fallback values in `var()` for robustness.
- **Minimize JavaScript Updates**: Use CSS for static styles to reduce runtime overhead.
- **Test Across Browsers**: Ensure compatibility, as older browsers may not support variables.

## Example Project
Below is a sample webpage showcasing CSS Variables for theming and responsive design.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS Variables Example</title>
  <style>
    :root {
      --primary-color: #3498db;
      --secondary-color: #2ecc71;
      --base-font-size: 16px;
      --spacing: 15px;
    }
    [data-theme="dark"] {
      --primary-color: #2980b9;
      --secondary-color: #27ae60;
      --bg-color: #222222;
      --text-color: #ffffff;
    }
    body {
      font-family: Arial, sans-serif;
      background-color: var(--bg-color, #f0f0f0);
      color: var(--text-color, #000000);
      margin: calc(var(--spacing) * 2);
    }
    .card {
      background-color: var(--primary-color);
      padding: var(--spacing);
      border-radius: 8px;
      border: 2px solid var(--secondary-color);
    }
    @media screen and (max-width: 600px) {
      :root {
        --base-font-size: 14px;
        --spacing: 10px;
      }
    }
    button {
      padding: var(--spacing);
      background-color: var(--secondary-color);
      border: none;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button onclick="document.documentElement.setAttribute('data-theme', 'dark')">Toggle Dark Mode</button>
  <div class="card">
    <h2>Dynamic Card</h2>
    <p style="font-size: var(--base-font-size)">This card uses CSS variables for theming and responsive styling.</p>
  </div>
  <script>
    document.querySelector('button').addEventListener('click', () => {
      const root = document.documentElement;
      const currentTheme = root.getAttribute('data-theme');
      root.setAttribute('data-theme', currentTheme === 'dark' ? '' : 'dark');
    });
  </script>
</body>
</html>
```

This example demonstrates CSS Variables for theming, responsive design, and dynamic updates via JavaScript.

## Resources
- [MDN Web Docs: CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [CSS Tricks: Guide to CSS Variables](https://css-tricks.com/a-complete-guide-to-custom-properties/)
- [W3C: CSS Custom Properties Specification](https://www.w3.org/TR/css-variables-1/)