# HTML Star Rating Component

## HTML Structure

The HTML code provided creates a star rating system using radio buttons and labels. Here's the breakdown:

```html
<div class="rating">
    <input value="5" name="rate" id="star5" type="radio">
    <label title="text" for="star5"></label>
    <input value="4" name="rate" id="star4" type="radio">
    <label title="text" for="star4"></label>
    <input value="3" name="rate" id="star3" type="radio" checked="">
    <label title="text" for="star3"></label>
    <input value="2" name="rate" id="star2" type="radio">
    <label title="text" for="star2"></label>
    <input value="1" name="rate" id="star1" type="radio">
    <label title="text" for="star1"></label>
</div>
```

### Explanation:
- **`<div class="rating">`**: This is the container for the star rating component.
- **`<input>`**: Each star is represented by a radio button. The `value` attribute corresponds to the rating (1 to 5). The `name` attribute groups the radio buttons together, ensuring only one can be selected at a time. The `id` attribute uniquely identifies each radio button.
- **`<label>`**: Each label is associated with a radio button using the `for` attribute, which matches the `id` of the corresponding radio button. The `title` attribute can be used to provide additional information (e.g., tooltips).
- **`checked`**: The `checked` attribute on the third radio button (`id="star3"`) makes it the default selected option.

---

## How It Works

1. **Radio Buttons**: The radio buttons are used to capture the user's rating. Only one radio button can be selected at a time because they share the same `name` attribute (`name="rate"`).
2. **Labels**: The labels are used to create clickable areas for the stars. When a label is clicked, the associated radio button is selected.
3. **Default Selection**: The `checked` attribute on the third radio button ensures that the rating defaults to 3 stars.

---

## Customization

You can customize this component in several ways:

1. **Number of Stars**: Add or remove `<input>` and `<label>` pairs to change the number of stars.
2. **Default Selection**: Change the `checked` attribute to a different radio button to set a different default rating.
3. **Labels**: Update the `title` attribute of the `<label>` elements to provide custom tooltips.

---

## Styling with CSS

### Lets Understand these lines:
```css
 .rating{
    display: flex;
    justify-content: start;
    flex-direction: row-reverse;

}
```
Let’s break down the CSS line-by-line for the `.rating` class:

```css
.rating {
    display: flex;
    justify-content: start;
    flex-direction: row-reverse;
}
```

### 1. **`display: flex;`**
   - This property makes the `.rating` container a **flexbox container**. Flexbox is a CSS layout model that allows you to easily align and distribute space among items in a container.
   - By setting `display: flex;`, all the child elements (in this case, the `<input>` and `<label>` elements) become **flex items** and are laid out in a row by default.

---

### 2. **`justify-content: start;`**
   - This property aligns the flex items (the stars) along the **main axis** (horizontal axis in this case).
   - `justify-content: start;` means the items will be aligned to the **start** of the container (left side in a left-to-right language like English).
   - If you change this to `justify-content: center;`, the stars would be centered in the container, and if you use `justify-content: end;`, they would align to the right.

---

### 3. **`flex-direction: row-reverse;`**
   - This property defines the **direction** in which the flex items are placed in the container.
   - By default, `flex-direction: row;` places items in a **left-to-right** order.
   - `flex-direction: row-reverse;` reverses this order, placing the items in a **right-to-left** order.
   - In the context of the star rating component:
     - Without `row-reverse`, the stars would appear in the order: **1 star, 2 stars, 3 stars, 4 stars, 5 stars**.
     - With `row-reverse`, the stars appear in the order: **5 stars, 4 stars, 3 stars, 2 stars, 1 star**.

---

### Why is `flex-direction: row-reverse;` used here?
In a star rating system, it’s common to highlight **all stars up to and including the selected star**. For example:
- If you hover over or select the **3rd star**, stars 1, 2, and 3 should be highlighted.
- To achieve this effect using CSS sibling selectors (`~`), the stars need to be in **reverse order** in the HTML. This way, when you select a star, the CSS can target all the stars that come **after it** in the DOM (which are actually the lower-rated stars visually).

---

### Lets Understand these lines:
```css
 .rating:not(:checked) > input {
    position: absolute;
    appearance: none;
  }
  
  .rating:not(:checked) > label {
    float: right;
    cursor: pointer;
    font-size: 100px;
    color: #666;
  }
  
  .rating:not(:checked) > label:before {
    content: '★';
  }
```


Let’s break down these CSS rules step by step. These rules are used to style the star rating component when no star is selected (`:not(:checked)`). Here's the explanation:

---

### 1. **`.rating:not(:checked) > input`**
```css
.rating:not(:checked) > input {
    position: absolute;
    appearance: none;
}
```

#### Explanation:
- **`.rating:not(:checked)`**: This selector targets the `.rating` container when **none of the radio buttons are checked**.
- **`> input`**: This selects all the `<input>` elements (radio buttons) that are direct children of the `.rating` container.
- **`position: absolute;`**: This removes the radio buttons from the normal document flow and positions them absolutely within their containing block. This is often used to hide the radio buttons visually while keeping them functional.
- **`appearance: none;`**: This removes the default styling of the radio buttons (e.g., the circle) so they are not visible. This is necessary because we want to replace the radio buttons with custom star icons.

---

### 2. **`.rating:not(:checked) > label`**
```css
.rating:not(:checked) > label {
    float: right;
    cursor: pointer;
    font-size: 100px;
    color: #666;
}
```

#### Explanation:
- **`.rating:not(:checked)`**: Again, this targets the `.rating` container when no radio button is checked.
- **`> label`**: This selects all the `<label>` elements that are direct children of the `.rating` container.
- **`float: right;`**: This makes the labels float to the right. This is used to reverse the order of the stars visually (since the HTML structure is already reversed with `flex-direction: row-reverse;` in the parent container).
- **`cursor: pointer;`**: This changes the mouse cursor to a pointer (hand) when hovering over the labels, indicating that they are clickable.
- **`font-size: 100px;`**: This sets the size of the stars. The stars are created using the `★` character, and this property controls how large they appear.
- **`color: #666;`**: This sets the default color of the stars to a light gray (`#666`). This is the color of the stars when they are **not selected or hovered**.

---

### 3. **`.rating:not(:checked) > label:before`**
```css
.rating:not(:checked) > label:before {
    content: '★';
}
```

#### Explanation:
- **`.rating:not(:checked)`**: Targets the `.rating` container when no radio button is checked.
- **`> label:before`**: This uses the `:before` pseudo-element to insert content **before** each `<label>` element.
- **`content: '★';`**: This inserts the Unicode character for a star (`★`) as the content of the `:before` pseudo-element. This is how the stars are displayed visually.

---

### Why These Rules Are Used:
1. **Hide Radio Buttons**: The `input` elements are hidden using `position: absolute;` and `appearance: none;` because we don’t want the default radio buttons to be visible. Instead, we use custom star icons.
2. **Style Labels as Stars**: The `<label>` elements are styled to look like stars using the `★` character. The `font-size` and `color` properties control their appearance.
3. **Reverse Order**: The `float: right;` ensures the stars are displayed in the correct order (right to left) when no star is selected.
4. **Clickable Stars**: The `cursor: pointer;` makes it clear that the stars are interactive and can be clicked to select a rating.

---
#### Result:
- The radio buttons are hidden.
- The labels are displayed as stars (`★`) with a light gray color (`#666`).
- The stars are clickable, and hovering over them changes the cursor to a pointer.

---

### Summary:
- **`.rating:not(:checked) > input`**: Hides the radio buttons.
- **`.rating:not(:checked) > label`**: Styles the labels as stars and makes them clickable.
- **`.rating:not(:checked) > label:before`**: Inserts the star character (`★`) as the content of the labels.


### Lets Understand these lines:
```css
 .rating > input:checked + label:hover,
  .rating > input:checked + label:hover ~ label,
  .rating > input:checked ~ label:hover,
  .rating > input:checked ~ label:hover ~ label,
  .rating > label:hover ~ input:checked ~ label {
    color: #e58e09;
  }
```


This block of CSS is used to handle the **hover and selection states** of the star rating component. It ensures that when a user hovers over the stars or selects a star, the appropriate stars are highlighted with a specific color (`#e58e09`). Let’s break it down step by step:

---

### 1. **`.rating > input:checked + label:hover`**
```css
.rating > input:checked + label:hover {
    color: #e58e09;
}
```

#### Explanation:
- **`.rating > input:checked`**: Targets the radio button (`<input>`) that is currently checked (selected).
- **`+ label:hover`**: The `+` is the **adjacent sibling combinator**. It selects the `<label>` that immediately follows the checked radio button.
- **`label:hover`**: Applies the style when the user hovers over this specific label.
- **`color: #e58e09;`**: Changes the color of the hovered label to `#e58e09` (an orange color).

#### What It Does:
- When the user hovers over the label that corresponds to the **currently selected radio button**, it changes the color of that label to orange.

---

### 2. **`.rating > input:checked + label:hover ~ label`**
```css
.rating > input:checked + label:hover ~ label {
    color: #e58e09;
}
```

#### Explanation:
- **`.rating > input:checked`**: Targets the checked radio button.
- **`+ label:hover`**: Selects the label immediately following the checked radio button when hovered.
- **`~ label`**: The `~` is the **general sibling combinator**. It selects all the `<label>` elements that come after the hovered label.
- **`color: #e58e09;`**: Changes the color of all these labels to orange.

#### What It Does:
- When the user hovers over the label corresponding to the **currently selected radio button**, it changes the color of **that label and all the labels to its right** to orange.

---

### 3. **`.rating > input:checked ~ label:hover`**
```css
.rating > input:checked ~ label:hover {
    color: #e58e09;
}
```

#### Explanation:
- **`.rating > input:checked`**: Targets the checked radio button.
- **`~ label:hover`**: Selects any `<label>` that comes after the checked radio button when hovered.
- **`color: #e58e09;`**: Changes the color of the hovered label to orange.

#### What It Does:
- When the user hovers over any label that comes **after the checked radio button**, it changes the color of that label to orange.

---

### 4. **`.rating > input:checked ~ label:hover ~ label`**
```css
.rating > input:checked ~ label:hover ~ label {
    color: #e58e09;
}
```

#### Explanation:
- **`.rating > input:checked`**: Targets the checked radio button.
- **`~ label:hover`**: Selects any label that comes after the checked radio button when hovered.
- **`~ label`**: Selects all the labels that come after the hovered label.
- **`color: #e58e09;`**: Changes the color of these labels to orange.

#### What It Does:
- When the user hovers over a label that comes **after the checked radio button**, it changes the color of **that label and all the labels to its right** to orange.

---

### 5. **`.rating > label:hover ~ input:checked ~ label`**
```css
.rating > label:hover ~ input:checked ~ label {
    color: #e58e09;
}
```

#### Explanation:
- **`.rating > label:hover`**: Targets any label that is being hovered over.
- **`~ input:checked`**: Selects any checked radio button that comes after the hovered label.
- **`~ label`**: Selects all the labels that come after the checked radio button.
- **`color: #e58e09;`**: Changes the color of these labels to orange.

#### What It Does:
- When the user hovers over a label, it changes the color of **all the labels that come after the checked radio button** to orange.

---

### Why These Rules Are Needed:
These rules ensure that the star rating component behaves intuitively:
1. **Hover Effect**: When the user hovers over a star, it highlights that star and all the stars to its left (or right, depending on the order).
2. **Selection Effect**: When a star is selected, it highlights that star and all the stars to its left (or right).
3. **Combined Hover and Selection**: These rules handle cases where the user hovers over stars while a star is already selected, ensuring the correct stars are highlighted.

---

### Example Scenario:
#### HTML:
```html
<div class="rating">
    <input id="star5" type="radio">
    <label for="star5"></label>
    <input id="star4" type="radio">
    <label for="star4"></label>
    <input id="star3" type="radio">
    <label for="star3"></label>
    <input id="star2" type="radio">
    <label for="star2"></label>
    <input id="star1" type="radio">
    <label for="star1"></label>
</div>
```

#### Behavior:
1. If the user selects the **3rd star**:
   - The 3rd star and all stars to its left (1st and 2nd) are highlighted.
2. If the user hovers over the **4th star**:
   - The 4th star and all stars to its left (1st, 2nd, and 3rd) are highlighted.
3. If the user hovers over the **2nd star** while the **3rd star** is selected:
   - The 2nd star and all stars to its left (1st) are highlighted.

---

### Summary:
These CSS rules work together to create a smooth and intuitive hover and selection experience for the star rating component. They ensure that the correct stars are highlighted based on the user’s interactions, making the component visually appealing and user-friendly.


### Lets Understand these lines:
```css
 .rating:not(:checked) > label:hover,
  .rating:not(:checked) > label:hover ~ label {
    color: #ff9e0b;
  }
  
  .rating > input:checked ~ label {
    color: #ffa723;
  }
```
These CSS rules handle the **hover and selected states** of the star rating component. They ensure that the stars change color when hovered over or selected, providing visual feedback to the user. Let’s break them down:

---

### 1. **`.rating:not(:checked) > label:hover`**
```css
.rating:not(:checked) > label:hover {
    color: #ff9e0b;
}
```

#### Explanation:
- **`.rating:not(:checked)`**: Targets the `.rating` container when **no radio button is checked**.
- **`> label:hover`**: Selects any `<label>` element (star) that is being hovered over.
- **`color: #ff9e0b;`**: Changes the color of the hovered label to `#ff9e0b` (a bright orange color).

#### What It Does:
- When no star is selected, hovering over a star changes its color to `#ff9e0b`.

---

### 2. **`.rating:not(:checked) > label:hover ~ label`**
```css
.rating:not(:checked) > label:hover ~ label {
    color: #ff9e0b;
}
```

#### Explanation:
- **`.rating:not(:checked)`**: Targets the `.rating` container when no radio button is checked.
- **`> label:hover`**: Selects any label that is being hovered over.
- **`~ label`**: The `~` is the **general sibling combinator**. It selects all the `<label>` elements that come **after** the hovered label.
- **`color: #ff9e0b;`**: Changes the color of these labels to `#ff9e0b`.

#### What It Does:
- When no star is selected, hovering over a star changes the color of **that star and all the stars to its right** to `#ff9e0b`.

---

### 3. **`.rating > input:checked ~ label`**
```css
.rating > input:checked ~ label {
    color: #ffa723;
}
```

#### Explanation:
- **`.rating > input:checked`**: Targets the radio button (`<input>`) that is currently checked (selected).
- **`~ label`**: Selects all the `<label>` elements that come **after** the checked radio button.
- **`color: #ffa723;`**: Changes the color of these labels to `#ffa723` (a slightly different shade of orange).

#### What It Does:
- When a star is selected, it changes the color of **that star and all the stars to its left** to `#ffa723`.

---

### Why These Rules Are Needed:
1. **Hover Effect**:
   - When no star is selected, hovering over a star highlights **that star and all the stars to its right**.
   - This provides visual feedback to the user, indicating the rating they are about to select.

2. **Selected State**:
   - When a star is selected, it highlights **that star and all the stars to its left**.
   - This shows the user the current rating they have chosen.

---

### Example Scenario:
#### HTML:
```html
<div class="rating">
    <input id="star5" type="radio">
    <label for="star5"></label>
    <input id="star4" type="radio">
    <label for="star4"></label>
    <input id="star3" type="radio">
    <label for="star3"></label>
    <input id="star2" type="radio">
    <label for="star2"></label>
    <input id="star1" type="radio">
    <label for="star1"></label>
</div>
```

#### Behavior:
1. **No Star Selected**:
   - If the user hovers over the **3rd star**, the 3rd, 4th, and 5th stars change color to `#ff9e0b`.
   - This indicates that selecting the 3rd star would give a rating of 3.

2. **Star Selected**:
   - If the user selects the **3rd star**, the 1st, 2nd, and 3rd stars change color to `#ffa723`.
   - This shows that the current rating is 3.

---

### Visual Example:
#### Before Hover or Selection:
```
★ ★ ★ ★ ★ (all stars are gray)
```

#### On Hover (No Star Selected):
- Hovering over the 3rd star:
```
★ ★ ★ ★ ★ (3rd, 4th, and 5th stars turn orange)
```

#### After Selection:
- Selecting the 3rd star:
```
★ ★ ★ ★ ★ (1st, 2nd, and 3rd stars turn orange)
```

---

### Summary:
- **`.rating:not(:checked) > label:hover`**: Changes the color of the hovered star when no star is selected.
- **`.rating:not(:checked) > label:hover ~ label`**: Changes the color of the hovered star and all stars to its right when no star is selected.
- **`.rating > input:checked ~ label`**: Changes the color of the selected star and all stars to its left.

These rules work together to create a smooth and intuitive user experience for the star rating component!
