# Lesson 1: CSS Basics & Syntax

## Learning Objectives

By the end of this lesson, you should be able to:
- Understand CSS syntax structure (selector, property, value)
- Know the three ways to add CSS to HTML
- Write basic CSS selectors (element, class, ID)
- Use browser DevTools to inspect and debug CSS

## Key Concepts

### CSS Syntax

CSS rules consist of:
```css
selector {
    property: value;
}
```

- **Selector**: Targets the HTML element(s) to style
- **Property**: The aspect you want to change (color, font-size, etc.)
- **Value**: How you want to change it

### Three Ways to Add CSS

1. **Inline CSS**: Directly in HTML elements
   ```html
   <p style="color: red;">Red text</p>
   ```

2. **Internal CSS**: In a `<style>` tag in the `<head>`
   ```html
   <style>
       p { color: red; }
   </style>
   ```

3. **External CSS**: In a separate `.css` file
   ```html
   <link rel="stylesheet" href="styles.css">
   ```

### Basic Selectors

- **Element selector**: Targets all elements of a type
  ```css
  p { color: blue; }
  ```

- **Class selector**: Targets elements with a specific class
  ```css
  .highlight { background: yellow; }
  ```

- **ID selector**: Targets a single element with a specific ID
  ```css
  #header { font-size: 24px; }
  ```

## Exercises

Complete the exercises in `index.html`:

1. Change the body background color to a light gray (#f0f0f0)
2. Change the h1 color to navy blue
3. Add a red color to all paragraphs
4. Make the text in the div with class "highlight" bold and green
5. Challenge: Style the paragraph with class "challenge" using inline CSS

## Tips

- Open `index.html` in your browser
- Press F12 to open DevTools
- Use the Elements/Inspector tab to see your CSS in action
- Experiment and have fun!

## Next Steps

Once you complete this lesson, move on to Lesson 2: Selectors & Specificity to learn more advanced ways to target elements.
