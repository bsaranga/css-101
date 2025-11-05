# Lesson 2: Selectors & Specificity

## Overview

Welcome to one of the most important lessons in CSS! Understanding selectors and specificity is like having a precision targeting system for your styles. In Lesson 1, you learned basic selectors (element, class, ID). Now we'll explore the full power of CSS selectors and understand how the browser decides which styles to apply when rules conflict.

Think of CSS selectors as a language for describing exactly which elements you want to style. The more fluent you become in this language, the more precise and efficient your CSS will be.

## Learning Objectives

By the end of this lesson, you will be able to:

1. Use all types of CSS selectors effectively
2. Understand and apply combinators to target element relationships
3. Calculate specificity to predict which styles will be applied
4. Explain how the cascade resolves style conflicts
5. Understand how inheritance works in CSS
6. Debug specificity conflicts using DevTools

---

## Part 1: The Foundation - Basic Selectors

Let's review and expand on what you learned in Lesson 1.

### 1.1 Universal Selector

The universal selector (`*`) targets **every element** on the page.

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

**When to use:**
- CSS resets (removing default browser styles)
- Applying box-sizing to all elements
- Debugging (adding borders to everything)

**Warning:** Can impact performance on very large pages. Use sparingly in production.

### 1.2 Element (Type) Selectors

Target all elements of a specific HTML type.

```css
p {
    line-height: 1.6;
}

h1 {
    font-size: 2.5rem;
}

a {
    text-decoration: none;
}
```

**Specificity:** Low (this is important for later!)

**When to use:**
- Setting default styles for all instances of an element
- Typography defaults
- Base styles before adding classes

### 1.3 Class Selectors

Target elements with a specific class attribute. Classes are **reusable** and can be applied to multiple elements.

```html
<div class="card">...</div>
<div class="card">...</div>
<article class="card">...</article>
```

```css
.card {
    background: white;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

**Key points:**
- Start with a dot (`.`)
- Case-sensitive
- Can apply to any element type
- An element can have multiple classes

**Multiple Classes:**

```html
<button class="btn btn-primary btn-large">Click me</button>
```

```css
.btn {
    padding: 10px 20px;
    border: none;
    cursor: pointer;
}

.btn-primary {
    background: blue;
    color: white;
}

.btn-large {
    font-size: 1.2rem;
}
```

### 1.4 ID Selectors

Target a **single, unique** element with a specific ID attribute.

```html
<header id="main-header">...</header>
```

```css
#main-header {
    background: navy;
    color: white;
}
```

**Key points:**
- Start with a hash (`#`)
- Should be unique on the page (only one element per ID)
- Very high specificity (more on this later)
- Generally avoid for styling (use classes instead)

**Best Practice:** Use IDs for:
- JavaScript selection
- Fragment links (`<a href="#section">`)
- Form labels (`<label for="input-id">`)

**Not recommended for:** Regular styling (too specific, not reusable)

### 1.5 Grouping Selectors

Apply the same styles to multiple selectors by separating them with commas.

```css
h1, h2, h3, h4, h5, h6 {
    font-family: Georgia, serif;
    font-weight: bold;
}

.header, .footer, .sidebar {
    background: #f5f5f5;
}
```

**Teaching Tip:** Each selector in a group is evaluated independently. If one is invalid, it doesn't break the others (in most browsers).

---

## Part 2: Attribute Selectors

Attribute selectors target elements based on their attributes and values. These are incredibly powerful!

### 2.1 Basic Attribute Selector

Target elements that have a specific attribute (regardless of value).

```css
/* Any element with a title attribute */
[title] {
    cursor: help;
    border-bottom: 1px dotted;
}

/* Any input with a required attribute */
input[required] {
    border: 2px solid red;
}
```

### 2.2 Exact Value Match

Target elements where an attribute equals a specific value exactly.

```css
/* Links to example.com */
a[href="https://example.com"] {
    color: green;
}

/* Text inputs only */
input[type="text"] {
    border: 1px solid gray;
}

/* Images with specific alt text */
img[alt="logo"] {
    width: 200px;
}
```

### 2.3 Contains Word Match (`~=`)

Target elements where the attribute contains a specific word (space-separated).

```css
/* Elements with "highlight" in their class list */
[class~="highlight"] {
    background: yellow;
}
```

**HTML example:**
```html
<div class="card highlight featured">This will match</div>
<div class="highlighted">This won't match (not a separate word)</div>
```

### 2.4 Starts With Match (`^=`)

Target elements where the attribute value **starts with** a specific string.

```css
/* External links (starting with http) */
a[href^="http"] {
    color: blue;
}

a[href^="https"] {
    color: green;
}

/* Image files */
img[src^="/images/"] {
    border: 2px solid gray;
}
```

**Real-world use case:** Styling external links differently from internal links.

### 2.5 Ends With Match (`$=`)

Target elements where the attribute value **ends with** a specific string.

```css
/* PDF links */
a[href$=".pdf"] {
    background: url('pdf-icon.png') no-repeat left center;
    padding-left: 25px;
}

/* Different icons for different file types */
a[href$=".doc"] { /* Word icon */ }
a[href$=".zip"] { /* Zip icon */ }
```

### 2.6 Contains Substring Match (`*=`)

Target elements where the attribute value **contains** a specific substring anywhere.

```css
/* Links containing "login" anywhere in the URL */
a[href*="login"] {
    color: orange;
}

/* Elements with "error" anywhere in class */
[class*="error"] {
    color: red;
}
```

### 2.7 Starts With or Followed by Hyphen (`|=`)

Target elements where the attribute value starts with a specific word or that word followed by a hyphen.

```css
/* Useful for language attributes */
[lang|="en"] {
    /* Matches lang="en", lang="en-US", lang="en-GB" */
    font-family: Arial, sans-serif;
}
```

### 2.8 Case-Insensitive Matching

Add `i` before the closing bracket to make the match case-insensitive.

```css
/* Match regardless of case */
a[href$=".PDF" i] {
    /* Matches .pdf, .PDF, .Pdf, etc. */
    background: red;
}
```

**Practical Example: Styling Different Input Types**

```css
/* Text inputs */
input[type="text"],
input[type="email"],
input[type="password"] {
    border: 1px solid #ddd;
    padding: 8px;
    border-radius: 4px;
}

/* Buttons */
input[type="submit"],
input[type="button"] {
    background: blue;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
}

/* Checkboxes and radios */
input[type="checkbox"],
input[type="radio"] {
    margin-right: 5px;
}
```

---

## Part 3: Combinators - Targeting Element Relationships

Combinators allow you to target elements based on their relationship to other elements. This is where CSS selectors become truly powerful!

### 3.1 Descendant Combinator (Space)

Target elements that are **descendants** (nested anywhere inside) another element.

```css
/* Any <p> inside <article>, at any nesting level */
article p {
    color: #333;
    line-height: 1.6;
}
```

**HTML that matches:**
```html
<article>
    <p>This matches</p>
    <div>
        <p>This also matches (nested deeper)</p>
    </div>
</article>
```

**Real-world example:**
```css
/* Style links only when they're inside navigation */
nav a {
    color: white;
    text-decoration: none;
    padding: 10px;
}

/* Different styling for links in article content */
article a {
    color: blue;
    text-decoration: underline;
}
```

### 3.2 Child Combinator (`>`)

Target elements that are **direct children** only (immediate descendants, not grandchildren).

```css
/* Only <p> that are direct children of <article> */
article > p {
    font-weight: bold;
}
```

**HTML example:**
```html
<article>
    <p>This matches (direct child)</p>
    <div>
        <p>This doesn't match (grandchild)</p>
    </div>
</article>
```

**When to use:** When you want precision and don't want to affect deeply nested elements.

**Real-world example:**
```css
/* Style only the immediate children of nav, not nested items */
nav > ul > li {
    display: inline-block;
}

/* First-level menu items */
.menu > li {
    font-weight: bold;
}

/* Second-level menu items */
.menu > li > ul > li {
    font-weight: normal;
    padding-left: 20px;
}
```

### 3.3 Adjacent Sibling Combinator (`+`)

Target an element that **immediately follows** another element (same parent, right after).

```css
/* <p> immediately after <h2> */
h2 + p {
    font-size: 1.2rem;
    font-weight: bold;
}
```

**HTML example:**
```html
<h2>Heading</h2>
<p>This matches (immediately after h2)</p>
<p>This doesn't match (not adjacent)</p>
```

**Real-world uses:**
```css
/* First paragraph after a heading (drop cap effect) */
h1 + p::first-letter {
    font-size: 3rem;
    float: left;
    margin-right: 5px;
}

/* Add spacing between consecutive sections */
section + section {
    margin-top: 40px;
}

/* Style label immediately after checkbox */
input[type="checkbox"] + label {
    margin-left: 5px;
    cursor: pointer;
}
```

### 3.4 General Sibling Combinator (`~`)

Target elements that are siblings (same parent) and **come after** another element (not necessarily immediately).

```css
/* All <p> that come after <h2> (same parent) */
h2 ~ p {
    color: gray;
}
```

**HTML example:**
```html
<div>
    <h2>Heading</h2>
    <p>This matches</p>
    <img src="image.jpg">
    <p>This also matches (sibling after h2)</p>
</div>
```

**Real-world example:**
```css
/* When a checkbox is checked, style all following siblings */
.toggle:checked ~ .content {
    display: block;
}

/* Highlight all form fields after an invalid one */
input:invalid ~ input {
    border-color: red;
}
```

### Combinator Comparison Table

| Combinator | Symbol | Relationship | Example |
|------------|--------|--------------|---------|
| Descendant | space | Any descendant | `div p` |
| Child | `>` | Direct child only | `div > p` |
| Adjacent Sibling | `+` | Immediately after | `h2 + p` |
| General Sibling | `~` | After (same parent) | `h2 ~ p` |

### Complex Selector Chains

You can combine multiple selectors and combinators:

```css
/* Paragraphs inside articles within main section */
section.main article p {
    line-height: 1.8;
}

/* Direct list items of unordered lists in nav */
nav > ul > li {
    display: inline-block;
}

/* Links in paragraphs within the main content area */
#content article p a {
    color: blue;
    text-decoration: underline;
}

/* Checkbox followed by a label with a specific class */
input[type="checkbox"] + label.custom {
    font-weight: bold;
}
```

---

## Part 4: Understanding Specificity

Now we arrive at one of the most important concepts in CSS: **specificity**. When multiple rules target the same element, specificity determines which style wins.

### 4.1 Why Specificity Matters

Consider this scenario:

```css
p {
    color: blue;
}

.intro {
    color: red;
}

#welcome {
    color: green;
}
```

```html
<p class="intro" id="welcome">What color is this text?</p>
```

Answer: **Green!** Why? Because ID selectors have the highest specificity.

### 4.2 The Specificity Hierarchy

Think of specificity as a scoring system. Each selector type has a different point value:

```
Inline styles:      1000 points
IDs:                100 points
Classes, attributes, pseudo-classes: 10 points
Elements, pseudo-elements: 1 point
Universal (*):      0 points
```

**More accurate representation (4-column system):**

```
[Inline, IDs, Classes/Attributes/Pseudo-classes, Elements/Pseudo-elements]
```

Examples:
- `p` → [0, 0, 0, 1]
- `.intro` → [0, 0, 1, 0]
- `#welcome` → [0, 1, 0, 0]
- `style="color: red"` → [1, 0, 0, 0]

### 4.3 Calculating Specificity

Let's calculate step by step:

**Example 1:**
```css
p {
    /* [0, 0, 0, 1] - 1 element */
}
```

**Example 2:**
```css
.intro {
    /* [0, 0, 1, 0] - 1 class */
}
```

**Example 3:**
```css
p.intro {
    /* [0, 0, 1, 1] - 1 element + 1 class */
}
```

**Example 4:**
```css
#welcome {
    /* [0, 1, 0, 0] - 1 ID */
}
```

**Example 5:**
```css
div#welcome {
    /* [0, 1, 0, 1] - 1 ID + 1 element */
}
```

**Example 6:**
```css
nav ul li a {
    /* [0, 0, 0, 4] - 4 elements */
}
```

**Example 7:**
```css
.menu .item .link {
    /* [0, 0, 3, 0] - 3 classes */
}
```

**Example 8:**
```css
#header nav ul.menu li a.active {
    /* [0, 1, 2, 4] - 1 ID + 2 classes + 4 elements */
}
```

**Example 9:**
```css
a[href^="http"] {
    /* [0, 0, 1, 1] - 1 attribute + 1 element */
}
```

**Example 10:**
```css
li:first-child {
    /* [0, 0, 1, 1] - 1 pseudo-class + 1 element */
}
```

### 4.4 Specificity Rules

**Rule 1: Higher specificity always wins**

```css
p { color: blue; }           /* [0,0,0,1] */
.text { color: red; }        /* [0,0,1,0] - WINS */
```

**Rule 2: If specificity is equal, the last rule wins (cascade)**

```css
p { color: blue; }
p { color: red; }  /* This wins - same specificity, comes last */
```

**Rule 3: Specificity doesn't care about order of different selectors**

```css
.text { color: red; }   /* [0,0,1,0] */
p { color: blue; }      /* [0,0,0,1] */

/* For <p class="text">, color is RED (higher specificity) */
```

**Rule 4: Combinators and universal selector don't add specificity**

```css
div > p { }          /* [0,0,0,2] - Only counts div and p */
div   p { }          /* [0,0,0,2] - Space doesn't count */
*     p { }          /* [0,0,0,1] - * doesn't count */
```

**Rule 5: !important overrides everything (but avoid it!)**

```css
p { color: blue !important; }

#welcome { color: red; }  /* Even this doesn't override !important */
```

### 4.5 Specificity Practice Problems

**Problem 1:** Which rule wins?
```css
div p { color: blue; }              /* A */
.content p { color: red; }           /* B */
```
Answer: B wins [0,0,1,1] > [0,0,0,2]

**Problem 2:** Which rule wins?
```css
#header .nav { color: blue; }        /* A */
.site-header .nav { color: red; }    /* B */
```
Answer: A wins [0,1,1,0] > [0,0,2,0]

**Problem 3:** Which rule wins?
```css
nav ul li a { color: blue; }                    /* A */
.menu .item .link { color: red; }               /* B */
```
Answer: B wins [0,0,3,0] > [0,0,0,4]

**Problem 4:** Which rule wins?
```css
a[href$=".pdf"] { color: blue; }                /* A */
.link { color: red; }                           /* B */
```
Answer: Both equal [0,0,1,1] = [0,0,1,0]? No! A is [0,0,1,1], B is [0,0,1,0]. A wins!

### 4.6 Specificity Visualization Tool

You can visualize specificity as stacked columns:

```
Selector: #header nav .menu li a.active

[0, 1, 2, 4]
 │  │  │  │
 │  │  │  └─ 4 elements (nav, li, a, and one more?)
 │  │  └──── 2 classes (.menu, .active)
 │  └─────── 1 ID (#header)
 └────────── 0 inline styles

Total: 0-1-2-4 (read left to right, highest wins)
```

### 4.7 When Specificity Goes Wrong

**Anti-pattern 1: Over-specific selectors**
```css
/* BAD: Too specific */
body div.container section.main article.post p.text {
    color: blue;
}

/* GOOD: Keep it simple */
.post-text {
    color: blue;
}
```

**Anti-pattern 2: ID-heavy selectors**
```css
/* BAD: IDs make everything hard to override */
#header #nav #menu #item {
    color: blue;
}

/* GOOD: Use classes */
.nav-item {
    color: blue;
}
```

**Anti-pattern 3: Abusing !important**
```css
/* BAD: !important should be last resort */
p {
    color: blue !important;
}

/* GOOD: Fix the specificity instead */
.content p {
    color: blue;
}
```

### 4.8 Best Practices for Specificity

1. **Keep specificity low:** Makes CSS easier to override and maintain
2. **Avoid IDs for styling:** Use classes instead
3. **Don't over-qualify selectors:** `.menu` instead of `ul.menu`
4. **Avoid !important:** It's a code smell (fix specificity instead)
5. **Use single classes when possible:** `.btn` instead of `div.button.clickable`

---

## Part 5: The Cascade

The "C" in CSS stands for "Cascading." The cascade is the algorithm browsers use to determine which styles apply when there are conflicts.

### 5.1 The Cascade Order

When multiple rules target the same element, the browser follows this order to decide which wins:

1. **Importance** (!important)
2. **Origin** (author styles vs browser defaults vs user styles)
3. **Specificity** (what we just learned)
4. **Order** (later rules override earlier ones)

### 5.2 Origin of Styles

Styles can come from three sources:

1. **User Agent (Browser) Styles:** Default styles browsers apply
2. **User Styles:** Custom styles users apply (accessibility settings)
3. **Author Styles:** Your CSS (what you write)

**Priority (highest to lowest):**
1. Author !important
2. User !important
3. Author styles
4. User styles
5. Browser defaults

### 5.3 Source Order

When specificity is equal, the **last rule** wins:

```css
.button { background: blue; }
.button { background: red; }   /* This wins */
```

**In linked stylesheets:**
```html
<link rel="stylesheet" href="first.css">
<link rel="stylesheet" href="second.css">  <!-- This wins conflicts -->
```

### 5.4 Cascade in Action

```css
/* Browser default */
p { margin: 16px 0; }

/* Your stylesheet (early) */
p { margin: 10px 0; color: black; }

/* Your stylesheet (later) */
p { margin: 20px 0; }

/* Result: margin is 20px (later wins), color is black (only one defined) */
```

---

## Part 6: Inheritance

Some CSS properties are **inherited** from parent to child elements, while others are not.

### 6.1 What is Inheritance?

Inheritance means child elements automatically receive certain CSS property values from their parent.

```html
<div style="color: blue;">
    <p>This text is blue (inherited from div)</p>
    <span>This is also blue (inherited)</span>
</div>
```

### 6.2 Inherited Properties

**Typically inherited properties:**
- Text properties: `color`, `font-family`, `font-size`, `font-weight`, `line-height`, `text-align`, `letter-spacing`
- List properties: `list-style`, `list-style-type`
- Cursor: `cursor`

**Typically NOT inherited:**
- Box model: `margin`, `padding`, `border`, `width`, `height`
- Positioning: `position`, `top`, `left`, `z-index`
- Layout: `display`, `float`
- Background: `background`, `background-color`

### 6.3 Why Inheritance Matters

Inheritance makes CSS efficient:

```css
/* Instead of: */
p { font-family: Arial; }
h1 { font-family: Arial; }
h2 { font-family: Arial; }
span { font-family: Arial; }
div { font-family: Arial; }
/* ...and so on */

/* Just do: */
body {
    font-family: Arial, sans-serif;
}
/* All text elements inherit it! */
```

### 6.4 Controlling Inheritance

You can explicitly control inheritance with keywords:

**`inherit`** - Force inheritance:
```css
.special-button {
    color: inherit;  /* Use parent's color, even though buttons don't normally inherit */
}
```

**`initial`** - Reset to browser default:
```css
.reset {
    color: initial;  /* Back to browser default (usually black) */
}
```

**`unset`** - Inherit if naturally inherited, otherwise initial:
```css
.flexible {
    color: unset;    /* Inherits color (naturally inherited) */
    border: unset;   /* Resets to initial (not naturally inherited) */
}
```

**`revert`** - Revert to user agent stylesheet:
```css
.revert {
    all: revert;  /* Undo all author styles */
}
```

### 6.5 The `all` Property

Reset all properties at once:

```css
.reset-everything {
    all: unset;    /* Reset all properties */
}

.inherit-everything {
    all: inherit;  /* Inherit all possible properties from parent */
}
```

---

## Part 7: Debugging Specificity Issues

### 7.1 Using DevTools

**Step 1:** Inspect the element
**Step 2:** Look at the Styles panel
- Overridden styles are struck through
- Styles are listed in specificity order (highest first)

**Step 3:** Hover over selectors to see specificity
- Chrome shows specificity on hover
- Firefox shows it in the Rules panel

### 7.2 Common Debugging Scenarios

**Problem: My style isn't applying**

1. Check if selector is correct (inspect element)
2. Check specificity (is another rule overriding?)
3. Check for typos in property names
4. Check if property is valid for that element

**Problem: Can't override a style**

1. Check specificity of both rules
2. Increase specificity of your selector
3. Check for !important in the original rule
4. Verify your stylesheet loads after the one you're trying to override

### 7.3 Specificity Calculator

When learning, use online specificity calculators:
- https://specificity.keegan.st/
- https://polypane.app/css-specificity-calculator/

---

## Part 8: Real-World Examples

### Example 1: Navigation Menu

```css
/* Base navigation styles (low specificity) */
nav a {
    color: gray;
    text-decoration: none;
    padding: 10px;
}

/* Active state (higher specificity) */
nav a.active {
    color: blue;
    font-weight: bold;
}

/* Hover state (same specificity as active, but comes later) */
nav a:hover {
    color: darkblue;
}

/* Active hover (highest specificity for this group) */
nav a.active:hover {
    color: navy;
}
```

### Example 2: Form Validation

```css
/* Default input style */
input[type="text"] {
    border: 1px solid #ddd;
}

/* Invalid state (higher specificity) */
input[type="text"]:invalid {
    border-color: red;
}

/* Valid state */
input[type="text"]:valid {
    border-color: green;
}

/* Focused invalid input (highest specificity) */
input[type="text"]:invalid:focus {
    border-color: darkred;
    box-shadow: 0 0 5px red;
}
```

### Example 3: Card Component

```css
/* Base card (low specificity) */
.card {
    background: white;
    padding: 20px;
    border-radius: 8px;
}

/* Card title (moderate specificity) */
.card h2 {
    margin-top: 0;
    color: navy;
}

/* Special card variant (same specificity as .card, must come after) */
.card-featured {
    background: lightyellow;
    border: 2px solid gold;
}

/* Featured card title (highest specificity) */
.card-featured h2 {
    color: darkgoldenrod;
}
```

---

## Practice Exercises

### Exercise 1: Selector Practice

Create an HTML page with various elements. Write selectors to target:
1. All paragraphs inside `<article>` elements
2. Only direct children `<li>` of `<ul>`
3. The first paragraph after any `<h2>`
4. All links ending in `.pdf`
5. All required form inputs
6. Every second list item (hint: you'll learn this in a future lesson!)

### Exercise 2: Specificity Calculation

Calculate the specificity for these selectors:
1. `div p`
2. `.container .content`
3. `#header nav ul li a`
4. `[type="text"]`
5. `article > p.intro`
6. `.card h2 + p`

### Exercise 3: Debugging Challenge

Given this CSS, predict what color the text will be:

```css
p { color: blue; }
.text { color: red; }
#intro { color: green; }
div p { color: orange; }
.container .text { color: purple; }
```

```html
<div class="container">
    <p class="text" id="intro">What color am I?</p>
</div>
```

### Exercise 4: Inheritance Experiment

Create a page and:
1. Set `color` on `<body>` - observe what inherits it
2. Set `border` on `<div>` - does it inherit to children?
3. Force inheritance of a property that normally doesn't inherit
4. Use `all: unset` on an element and observe the effects

### Exercise 5: Build a Component

Create a button component with these requirements:
- Base `.btn` class with default styles
- `.btn-primary`, `.btn-secondary` variants
- Hover and active states
- Disabled state
- Ensure proper specificity so variants can override base styles

---

## Key Takeaways

1. **Selectors are powerful:** Learn them well to target precisely what you need
2. **Specificity determines which rule wins:** [inline, IDs, classes, elements]
3. **Keep specificity low:** Makes CSS maintainable
4. **Avoid IDs and !important:** Use classes instead
5. **The cascade uses:** importance → specificity → order
6. **Inheritance is selective:** Some properties inherit, others don't
7. **DevTools is your friend:** Use it to debug specificity issues

## Common Mistakes to Avoid

1. Over-specific selectors (makes CSS hard to maintain)
2. Using IDs for styling (use classes)
3. Relying on !important (fix specificity instead)
4. Not understanding inheritance (wasting CSS)
5. Writing selectors without understanding specificity

## Next Steps

You're now equipped with powerful targeting tools! Next lesson:
- **Lesson 3: The Box Model** - Understanding how elements are sized and spaced

---

## Additional Resources

- [MDN CSS Selectors Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [Specificity Calculator](https://specificity.keegan.st/)
- [CSS Diner (Selector Game)](https://flukeout.github.io/)
- [Specificity Graph Generator](https://jonassebastianohlsson.com/specificity-graph/)

## Study Tips

1. **Practice selectors daily** - Try to write complex selectors
2. **Use CSS Diner** - Gamified way to learn selectors
3. **Inspect real websites** - See how others structure selectors
4. **Calculate specificity** - Do it manually until it becomes intuitive
5. **Debug in DevTools** - Watch which rules win and why
6. **Build projects** - Apply these concepts in real code

---

**Time to Complete:** 4-5 hours
**Difficulty:** Intermediate
**Prerequisites:** Lesson 1 - CSS Basics & Syntax

**Pro Tip:** Specificity becomes intuitive with practice. Don't memorize - understand the principles and practice regularly!
