
# 🧑‍🏫 HTML & CSS 

> This lesson introduces students to the fundamentals of HTML and CSS. Though React Native doesn’t use HTML/CSS directly, JSX and `StyleSheet.create()` concepts mirror them closely. This lesson builds that core mental model.

---

## 🔸 What Is HTML?

HTML stands for **HyperText Markup Language**. It’s the **skeleton** of every webpage — used to define the **structure** of content.

### Example HTML Elements:

```html
<h1>Hello, World!</h1>      <!-- Heading -->
<p>This is a paragraph.</p> <!-- Paragraph -->
<a href="https://example.com">Visit Example</a> <!-- Link -->
<img src="profile.jpg" alt="Profile picture" /> <!-- Image -->
```

### Basic Structure of an HTML Document:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Page</title>
  </head>
  <body>
    <h1>Welcome!</h1>
    <p>This is my first webpage.</p>
  </body>
</html>
```

---

## 🔹 What Is CSS?

CSS stands for **Cascading Style Sheets**. It controls how HTML elements **look** — fonts, colors, spacing, layout, and more.

### Ways to Use CSS:

1. **Inline** (inside the element)
2. **Internal** (in a `<style>` block in `<head>`)
3. **External** (in a separate `.css` file)

---

## 🔸 Let's Style an HTML Page (Internal CSS)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Styled Page</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        background-color: #f5f5f5;
        text-align: center;
        padding: 30px;
      }

      h1 {
        color: #333;
      }

      p {
        color: #666;
        font-size: 18px;
      }

      img {
        width: 120px;
        border-radius: 50%;
        margin-top: 20px;
      }
    </style>
  </head>
  <body>
    <h1>Hello, I'm Alex!</h1>
    <p>I’m learning to build apps using React Native!</p>
    <img src="https://via.placeholder.com/120" alt="Profile Picture" />
  </body>
</html>
```

### 🧠 Explanation:

* `body`: Styling the entire page
* `h1`, `p`, `img`: Targeting specific elements
* `border-radius: 50%`: Makes the image round

---

## 🔹 Optional: Class Selectors

You can also give elements a **class** and apply styles that way.

```html
<p class="bio">This is my bio text.</p>
```

```css
.bio {
  color: #444;
  font-style: italic;
}
```

---

## 🤝 How This Connects to React Native

| HTML/CSS                     | React Native Equivalent      |
| ---------------------------- | ---------------------------- |
| `<div>`                      | `<View />`                   |
| `<p>`                        | `<Text />`                   |
| CSS                          | `StyleSheet.create({ ... })` |
| `class="container"`          | `style={styles.container}`   |
| Inline style (`style="..."`) | `style={{ color: 'blue' }}`  |

> 💬 You’ll be writing UI in JSX (which looks like HTML), and styling using JS objects. This intro helps build intuition.

---

## 🧩 Summary

* **HTML** = Structure
* **CSS** = Style
* React Native doesn’t use HTML/CSS directly, but JSX + `StyleSheet` work similarly.
* Understanding this will help you transition smoothly to React Native.
