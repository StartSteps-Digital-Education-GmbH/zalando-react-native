# 🧑‍🏫 Flexbox Fundamentals

> *Lesson Duration: \~1 hour*
> This lesson teaches students how to **arrange UI elements** using **Flexbox**, the core layout system used in **React Native**.

---

## 🔸 What Is Flexbox?

**Flexbox** (short for *Flexible Box Layout*) is a CSS layout system that helps you **align, position, and distribute** space among items in a container — even when their size is unknown or dynamic.

React Native also uses Flexbox under the hood, so this skill **directly transfers** to mobile UI.

---

## 🔹 Flexbox Terminology

* **Flex Container** → The parent element (`display: flex`)
* **Flex Items** → The children inside it

```html
<div style="display: flex;">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

---

## 🔸 Main Flexbox Properties

| Property          | Role                                                    |
| ----------------- | ------------------------------------------------------- |
| `flex-direction`  | Direction of items: `row` (default), `column`           |
| `justify-content` | Align items on the **main axis**                        |
| `align-items`     | Align items on the **cross axis**                       |
| `flex-wrap`       | Whether items should wrap to the next line              |
| `gap` (web only)  | Space between items (not supported in React Native yet) |

---

## 🔹 Visual Explanation (with Web Code)

```html
<style>
  .container {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    height: 200px;
    background-color: #e0f7fa;
  }

  .item {
    background-color: #00796b;
    color: white;
    padding: 20px;
    border-radius: 5px;
  }
</style>

<div class="container">
  <div class="item">A</div>
  <div class="item">B</div>
  <div class="item">C</div>
</div>
```

### 🧠 What this does:

* **`flex-direction: row`** → Items are placed left to right
* **`justify-content: space-around`** → Even spacing on main axis
* **`align-items: center`** → Vertically centered in container

---

## 🔹 Translating to React Native

Here's how the same logic looks in **React Native** (JSX + `StyleSheet.create()`):

```tsx
<View style={styles.container}>
  <Text style={styles.item}>A</Text>
  <Text style={styles.item}>B</Text>
  <Text style={styles.item}>C</Text>
</View>
```

```ts
const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    alignItems: 'center',
    height: 200,
    backgroundColor: '#e0f7fa',
  },
  item: {
    backgroundColor: '#00796b',
    color: 'white',
    padding: 20,
    borderRadius: 5,
  },
});
```

> 🎯 **Key Insight**: React Native uses `flexDirection: 'column'` by default (unlike web where `'row'` is default). This is important for mobile-first layouts.

---

## 🔸 Common Values Cheat Sheet

### ✅ `flex-direction`

* `'row'`: left to right
* `'column'`: top to bottom (default in React Native)

### ✅ `justify-content` (main axis)

* `'flex-start'`: start of axis
* `'center'`: centered
* `'flex-end'`: end
* `'space-between'`: space between items
* `'space-around'`: equal spacing around

### ✅ `align-items` (cross axis)

* `'flex-start'`
* `'center'`
* `'flex-end'`
* `'stretch'`

---

## 🧪 Mini Practice for Students

Ask students to:

1. Create a container with 3 boxes (A, B, C).
2. Try these one by one:

   * `flexDirection: 'column'`
   * `justifyContent: 'space-between'`
   * `alignItems: 'flex-end'`
3. Replace `<Text>` with `<View>` and apply different background colors and sizes.

This helps them visualize spacing and alignment in a React Native-like way.

---

## 🧠 Why This Is Crucial for React Native

React Native UIs often rely **entirely on Flexbox** for layout:

* Navigation bars
* Lists
* Buttons
* Centering content
* Responsive UIs

Flexbox is your **main layout tool** — no CSS Grid, floats, or media queries.

---

## 🔗 Practice Exercises

Here are some excellent exercises to master Flexbox visually:

* [🌐 Flexbox Froggy (fun game)](https://flexboxfroggy.com/)
* [📚 FreeCodeCamp Flexbox Guide](https://www.freecodecamp.org/learn/responsive-web-design/css-flexbox/)
* [📐 Flexbox Defense (game)](https://www.flexboxdefense.com/)
