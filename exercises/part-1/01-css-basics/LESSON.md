# Lesson 1: CSS Basics & Syntax

## Overview

CSS (Cascading Style Sheets) is the language used to style and layout web pages. While HTML provides the structure and content, CSS controls the visual presentation. This lesson covers the fundamental syntax of CSS and the different methods of applying styles to your HTML documents.

## Learning Objectives

By the end of this lesson, you will be able to:

1. Understand and write CSS syntax correctly
2. Apply CSS using three different methods (inline, internal, and external)
3. Use CSS comments effectively for code organization
4. Utilize browser DevTools to inspect and debug CSS

---

## 1. CSS Syntax Structure

### The Anatomy of a CSS Rule

A CSS rule consists of two main parts: a **selector** and a **declaration block**.

```css
selector {
    property: value;
    property: value;
}
```

**Example:**
```css
h1 {
    color: blue;
    font-size: 24px;
}
```

Let's break this down:

- **Selector** (`h1`): Targets which HTML element(s) to style
- **Declaration Block** (everything inside `{}`): Contains one or more declarations
- **Property** (`color`, `font-size`): The aspect of the element you want to change
- **Value** (`blue`, `24px`): How you want to change it
- **Semicolon** (`;`): Separates each declaration (required after each property-value pair)

### Multiple Declarations

You can apply multiple styles to the same selector:

```css
p {
    color: #333333;
    font-size: 16px;
    line-height: 1.5;
    margin-bottom: 20px;
}
```

### Multiple Selectors

You can apply the same styles to multiple selectors by separating them with commas:

```css
h1, h2, h3 {
    font-family: Arial, sans-serif;
    color: navy;
}
```

---

## 2. How to Include CSS

There are three primary methods to add CSS to your HTML documents. Each has its use cases, advantages, and disadvantages.

### 2.1 Inline CSS

Inline CSS is applied directly to an HTML element using the `style` attribute.

**Syntax:**
```html
<element style="property: value; property: value;">
```

**Example:**
```html
<p style="color: red; font-size: 18px;">This is a red paragraph.</p>
```

**Advantages:**
- Quick for testing specific styles
- Highest specificity (overrides other CSS)
- Useful for dynamic styles applied via JavaScript

**Disadvantages:**
- Not reusable (must be repeated for each element)
- Makes HTML cluttered and hard to maintain
- Violates separation of concerns principle
- Cannot use certain CSS features (like pseudo-classes, media queries)

**When to Use:**
- Quick prototyping and testing
- Email HTML (where external/internal CSS may not work)
- Dynamically generated styles via JavaScript
- Overriding styles in specific edge cases

### 2.2 Internal CSS (Embedded CSS)

Internal CSS is placed within a `<style>` tag in the `<head>` section of your HTML document.

**Syntax:**
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        selector {
            property: value;
        }
    </style>
</head>
<body>
    <!-- HTML content -->
</body>
</html>
```

**Example:**
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            background-color: #f0f0f0;
            font-family: Arial, sans-serif;
        }

        h1 {
            color: navy;
            text-align: center;
        }

        p {
            color: #333;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <h1>Welcome</h1>
    <p>This is styled with internal CSS.</p>
</body>
</html>
```

**Advantages:**
- Styles are contained within the HTML file (good for single-page documents)
- Can use full CSS features (selectors, pseudo-classes, media queries)
- Loads with the HTML (no additional HTTP request)
- Good for page-specific styles

**Disadvantages:**
- Not reusable across multiple HTML pages
- Increases HTML file size
- Makes maintenance harder for multi-page sites
- Browser cannot cache the CSS separately

**When to Use:**
- Single-page websites or applications
- Page-specific styles that won't be reused
- Prototyping and development
- Email templates (more reliable than external CSS)

### 2.3 External CSS

External CSS is written in a separate `.css` file and linked to HTML documents using the `<link>` tag.

**CSS File (styles.css):**
```css
body {
    background-color: #f0f0f0;
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

h1 {
    color: navy;
    text-align: center;
}

p {
    color: #333;
    line-height: 1.6;
}
```

**HTML File:**
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Welcome</h1>
    <p>This is styled with external CSS.</p>
</body>
</html>
```

**Advantages:**
- **Best practice for most projects**
- Completely separates content from presentation
- Can be reused across multiple HTML pages
- Browser can cache the CSS file (faster page loads)
- Easier to maintain and update
- Smaller HTML file sizes

**Disadvantages:**
- Requires an additional HTTP request (can delay initial render)
- Path issues can break styling if file is moved

**When to Use:**
- Multi-page websites (ALWAYS use this)
- Any professional project
- When styles need to be shared across pages
- When working in teams

### The `<link>` Tag Explained

```html
<link rel="stylesheet" href="path/to/styles.css">
```

- `rel="stylesheet"`: Defines the relationship between HTML and linked file
- `href`: Specifies the path to the CSS file
  - Relative path: `href="styles.css"` or `href="css/styles.css"`
  - Absolute path: `href="/assets/css/styles.css"`
  - External URL: `href="https://example.com/styles.css"`

### Multiple External Stylesheets

You can link multiple CSS files. They are applied in order:

```html
<head>
    <link rel="stylesheet" href="reset.css">
    <link rel="stylesheet" href="typography.css">
    <link rel="stylesheet" href="layout.css">
    <link rel="stylesheet" href="components.css">
</head>
```

Later stylesheets can override earlier ones due to the cascade.

---

## 3. Comments and Code Organization

### CSS Comments

Comments help document your code and make it easier to understand. They are ignored by the browser.

**Syntax:**
```css
/* This is a CSS comment */
```

Comments can span multiple lines:
```css
/*
   This is a multi-line comment
   It can span several lines
   Very useful for documentation
*/
```

**Examples of Good Comments:**

```css
/* =================================
   Typography Styles
   ================================= */

body {
    font-family: Arial, sans-serif;
    font-size: 16px;
}

/* Main heading styles */
h1 {
    font-size: 2.5rem;
    color: navy;
}

/* TODO: Add responsive font sizing */
p {
    line-height: 1.6;
}

/*
   HACK: Temporary fix for IE11 compatibility
   Remove when IE11 support is dropped
*/
.legacy-support {
    display: block;
}
```

### Code Organization Best Practices

#### 1. Table of Contents

For large CSS files, add a table of contents at the top:

```css
/*
   CSS TABLE OF CONTENTS

   1. Reset/Normalize
   2. Typography
   3. Layout
   4. Components
   5. Utilities
   6. Media Queries
*/
```

#### 2. Logical Grouping

Group related styles together:

```css
/* =================================
   TYPOGRAPHY
   ================================= */

body { font-family: Arial, sans-serif; }
h1 { font-size: 2.5rem; }
h2 { font-size: 2rem; }
p { line-height: 1.6; }

/* =================================
   LAYOUT
   ================================= */

.container { max-width: 1200px; }
.grid { display: grid; }
```

#### 3. Consistent Formatting

Choose a formatting style and stick to it:

```css
/* Single-line format (for simple rules) */
.text-center { text-align: center; }
.text-bold { font-weight: bold; }

/* Multi-line format (for complex rules) */
.card {
    background: white;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

#### 4. Alphabetize Properties (Optional)

Some teams alphabetize properties for consistency:

```css
.button {
    background-color: blue;
    border: none;
    border-radius: 4px;
    color: white;
    cursor: pointer;
    padding: 10px 20px;
}
```

---

## 4. Browser DevTools Basics

Browser Developer Tools (DevTools) are essential for CSS development. They allow you to inspect, edit, and debug styles in real-time.

### Opening DevTools

- **Windows/Linux**: F12 or Ctrl + Shift + I
- **Mac**: Cmd + Option + I
- **Right-click** on any element and select "Inspect" or "Inspect Element"

### Key Features for CSS

#### 4.1 Elements/Inspector Panel

This shows the HTML structure and applied CSS.

**How to Use:**
1. Click the element selector tool (icon in top-left of DevTools)
2. Hover over elements on the page to highlight them
3. Click an element to inspect it
4. View applied styles in the Styles panel

#### 4.2 Styles Panel

Shows all CSS rules applied to the selected element:
- Rules are shown in order of specificity
- Overridden styles are struck through
- You can edit values in real-time
- Click the checkbox to toggle properties on/off
- Click the color swatch to open a color picker

#### 4.3 Computed Panel

Shows the final computed values for all CSS properties:
- Displays only the values actually applied
- Shows the box model visualization
- Useful for understanding what styles "won" the cascade

#### 4.4 Box Model Visualization

Displays the element's box model visually:
- **Blue**: Content area
- **Green**: Padding
- **Yellow/Orange**: Border
- **Orange/Brown**: Margin

You can click on values to edit them directly.

#### 4.5 Live Editing

You can edit CSS directly in DevTools:
- Changes are temporary (lost on refresh)
- Great for experimenting before updating your code
- Add new properties by clicking in empty space
- Add new rules using the "+" button

### DevTools Workflow

1. **Inspect** the element you want to style
2. **Experiment** with CSS in the Styles panel
3. **Copy** the working CSS
4. **Paste** into your actual CSS file
5. **Refresh** to verify it works

### Debugging CSS

Common debugging tasks:

**Problem: Style not applying**
- Check if the selector is correct
- Check specificity (is another rule overriding it?)
- Look for struck-through styles
- Verify the property name is spelled correctly

**Problem: Layout issues**
- Use the Box Model visualization
- Check for unexpected margin/padding
- Look for overflow issues
- Verify display and position properties

**Problem: Colors look wrong**
- Check color values in Computed panel
- Look for opacity settings
- Check for parent element colors affecting child

---

## Practice Exercises

### Exercise 1: Understanding Syntax

Create a simple HTML file and style it using internal CSS:

**Task:**
1. Create an HTML file with a heading, two paragraphs, and a div
2. In a `<style>` tag, add CSS to:
   - Change the body background color
   - Style the heading with a custom color and font size
   - Make paragraphs have different colors
   - Give the div a border and padding

### Exercise 2: Three Methods Comparison

**Task:**
1. Create three HTML files (inline.html, internal.html, external.html)
2. Style the same content three different ways
3. Observe the differences in maintainability

### Exercise 3: Using Comments

**Task:**
1. Create a CSS file with at least 10 rules
2. Add a table of contents comment at the top
3. Group rules by category with section comments
4. Add inline comments explaining complex properties

### Exercise 4: DevTools Exploration

**Task:**
1. Open any website
2. Open DevTools and inspect 5 different elements
3. For each element:
   - View its applied styles
   - Check the computed values
   - Visualize the box model
   - Temporarily change a color or size
4. Find an element where one style overrides another

---

## Key Takeaways

1. **CSS Syntax**: `selector { property: value; }`
2. **Three Methods**:
   - Inline: Fast but not reusable
   - Internal: Good for single pages
   - External: Best practice for most projects
3. **Comments**: Use `/* comment */` to document code
4. **DevTools**: Essential for debugging and learning CSS

## Common Mistakes to Avoid

1. Forgetting the semicolon after property values
2. Using the wrong selector syntax
3. Over-using inline styles
4. Not organizing CSS code
5. Not using DevTools to debug issues

## Next Steps

Now that you understand CSS basics, you're ready to move on to:
- **Lesson 2: Selectors & Specificity** - Learn more powerful ways to target elements

---

## Additional Resources

- [MDN CSS Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)
- [CSS Syntax Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax)
- [Chrome DevTools Documentation](https://developer.chrome.com/docs/devtools/)

## Study Tips

1. Practice writing CSS by hand (don't just copy-paste)
2. Use DevTools every day to inspect websites you visit
3. Experiment with different values to see what happens
4. Build small projects to reinforce concepts
5. Read other developers' CSS to learn different approaches

---

**Time to Complete:** 2-3 hours
**Difficulty:** Beginner
**Prerequisites:** Basic HTML knowledge
