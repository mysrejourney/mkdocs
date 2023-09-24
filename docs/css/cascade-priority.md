# Order of Style
Let's say, if there are two css implementation mentioned for one HTML document, then which css rule will be applied to that HTML element. The order of style implementation matters when you work with CSS.

`1. Type of the style`
1. inline style takes the highest priority
2. internal style takes next place
3. external style takes the least priority out of these three.

**Example**
```html
<html>

<head>
    <link rel="stylesheet" href="./style.css">
    <style>
        li {
            color: blue
        }
    </style>
</head>

<body>
    <ul>
        <li style="color:red">Satheesh</li>
        <li>Pandian</li>
        <li>Jeganathan</li>
    </ul>
</body>

</html>
```
```css
li {
  color: green;
}
```
![order](../assets/order.jpg)

**Explanation**

Though external CSS style rule for `li` component color is green, internal CSS style rule is applied for list # 2 and 3. This is because internal style takes more priority than external style.
At the sametime, list # 1 color is red because it takes inline style rule which is higher priority than internal and external style.

There are four other important rules to implement CSS rules in HTML document.

`2. Position :` The position where the rule defines matter. The latest CSS rule will be applied in the HTML document.
```html
<html>
<head>
    <link rel="stylesheet" href="./style.css">
    <style>
        li {
            color: blue;
            color:yellowgreen
        }
    </style>
</head>

<body>
    <ul>
        <li style="color:red">Satheesh</li>
        <li>Pandian</li>
        <li>Jeganathan</li>
    </ul>
</body>
</html>
```
In the above case, text color is two different colors (blue and yellowgreen). When we implement this rule, yellowgreen will be implemented as it is the latest rule (from TOP to BOTTOM approach)

![position](../assets/position.jpg)

Let us assume, if there are two rules created for same `li` component like below
```html
    <style>
        li {
            color: blue;
            color: yellowgreen
        }

        li {
            color: brown;
            color: orangered
        }
    </style>
```
In the above  case, orangered is the latest color (from TOP to BOTTOM) and it will be implemented in `li` HTML element.

![position_1](../assets/position_1.jpg)


`3. Specificity :` Based on how specific a selector is applied CSS rule.

**Priority order**
1. ID
2. Attribute
3. Class
4. HTML element

**Example**
```html
<html>
<head>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <ul>
        <li id="satheesh" draggable="true" class="satheesh-class">Satheesh</li>
        <li>Pandian</li>
        <li>Jeganathan</li>
    </ul>
</body>
</html>
```

```css
li {
  color: green;
}
li[draggable] {
  color: yellow;
}
#satheesh {
  color: red;
}
.satheesh-class {
  color: blue;
}
```
In the above example, there are 4 rules applied in list # 1 component. Out of these 4 rules, ID takes high priority. Hence, it is displaying in red color.

![specificity_id](../assets/specificity_id.jpg)

```html
<html>
<head>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <ul>
        <li draggable="true" class="satheesh-class">Satheesh</li>
        <li>Pandian</li>
        <li>Jeganathan</li>
    </ul>
</body>
</html>
```
In the above example, there are 3 rules applied in list # 1 component. Out of these 3 rules, Attribute (draggable) takes high priority. Hence, it is displaying in yellow color.

![specificity_attribute](../assets/specificity_attribute.jpg)


```html
<html>
<head>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <ul>
        <li class="satheesh-class">Satheesh</li>
        <li>Pandian</li>
        <li>Jeganathan</li>
    </ul>
</body>
</html>
```
In the above example, there are 2 rules applied in list # 1 component. Out of these 2 rules, class takes high priority. Hence, it is displaying in blue color.

![specificity_class](../assets/specificity_class.jpg)


`4. Importance`: When `important` keyword mentioned in the property, this takes the highest priority compared to all other cases.

```css
li[draggable] {
  color: yellow;
}
#satheesh {
  color: red;
}
.satheesh-class {
  color: blue;
}
li {
  color: brown;
  color:#17fa07a3 !important;
}
```

```html
<html>
<head>
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <ul>
        <li id="satheesh" class="satheesh-class" draggable="true">Satheesh</li>
        <li>Pandian</li>
        <li>Jeganathan</li>
    </ul>
</body>
</html>
```

In the above example, all the rules applied in list #1 component. Out of all these rules, `important` takes high priority. Hence, it is displaying in green color. Note, as `important` keyword applied in list component, it applies all the list values.


![importance](../assets/importance.jpg)

###Combining CSS selectors
We can select multiple selectors and apply the rule in single HTML element or group of elements.

`1. Group` : Apply both the selectors

**Syntax**
```css
 selector1, selector2 {
    color: firebrick;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Combining CSS Selectors</title>
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <h1>To Do List</h1>
  <h2>Monday</h2>
  <div class="box">
    <p class="done">Do these things today!</p>
    <ul class="list">
      <li>Wash Clothes</li>
      <li class="done">Read</li>
      <li class="done">Maths Questions</li>
    </ul>
  </div>
  <ul>
    <p class="done">Other items</p>
  </ul>
  <p>The best preparation for tomorrow is doing your best today.</p>
</body>
</html>
```
If I want to apply different color ONLY to h1 and h2. Note, you can select `n` number of selectors and group them.
```css
h1,h2 {
    color: blueviolet;
}
```
![group_selector](../assets/group_selector.jpg)


`2. Child` : This will apply the CSS rule to the direct child element

**Syntax**
```css
 Parent > Child {
    color: firebrick;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Combining CSS Selectors</title>
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <h1>To Do List</h1>
  <h2>Monday</h2>
  <div class="box">
    <p class="done">Do these things today!</p>
    <ul class="list">
      <li>Wash Clothes</li>
      <li class="done">Read</li>
      <li class="done">Maths Questions</li>
    </ul>
  </div>
  <ul>
    <p class="done">Other items</p>
  </ul>
  <p>The best preparation for tomorrow is doing your best today.</p>
</body>
</html>
```
If I want to apply different color ONLY to `p` which is under `div`. 

**Example**
```css
.box > .done {
  color: firebrick;
}
```

![child](../assets/child.jpg)


`3. Descendant` : This will apply the CSS rule to the all child elements under parent selector

**Syntax**
```css
 Parent Child {
    color: blue;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Combining CSS Selectors</title>
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <h1>To Do List</h1>
  <h2>Monday</h2>
  <div class="box">
    <p class="done">Do these things today!</p>
    <ul class="list">
      <li>Wash Clothes</li>
      <li class="done">Read</li>
      <li class="done">Maths Questions</li>
    </ul>
  </div>
  <ul>
    <p class="done">Other items</p>
  </ul>
  <p>The best preparation for tomorrow is doing your best today.</p>
</body>
</html>
```
If I want to apply different color ONLY to `li` under `div`.

**Example**
```css
.box li{
    color: blue;
}
```
![descendant](../assets/descendant.jpg)


`4. Chaining` : This will apply the CSS rule to the all selectors are TRUE. We can pick specific element using this selector

**Syntax**
```css
 selector1selector2 {
    color: seagreen;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Combining CSS Selectors</title>
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <h1>To Do List</h1>
  <h2>Monday</h2>
  <div class="box">
    <p class="done">Do these things today!</p>
    <ul class="list">
      <li>Wash Clothes</li>
      <li class="done">Read</li>
      <li class="done">Maths Questions</li>
    </ul>
  </div>
  <ul>
    <p class="done">Other items</p>
  </ul>
  <p>The best preparation for tomorrow is doing your best today.</p>
</body>
</html>
```
If I want to apply different color ONLY to `li` (last two items) under `div`. 

**Example**
```css
.box li{
    color: seagreen;
}
```
![chain](../assets/chain.jpg)

`5. Combine combiners` : This is similar to descendant. However, first one is ancestor(parent) and second one is chaining selector

**Syntax**
```css
 selector1 selector2selector3 {
    font-size: 0.5rem;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Combining CSS Selectors</title>
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <h1>To Do List</h1>
  <h2>Monday</h2>
  <div class="box">
    <p class="done">Do these things today!</p>
    <ul class="list">
      <li>Wash Clothes</li>
      <li class="done">Read</li>
      <li class="done">Maths Questions</li>
    </ul>
  </div>
  <ul>
    <p class="done">Other items</p>
  </ul>
  <p>The best preparation for tomorrow is doing your best today.</p>
</body>
</html>
```
If I want to apply different font size for `p` and class is `done`

**Example**
```css
ul p.done{
    font-size: 0.5rem;
}
```
![combiner.jpg](../assets/combiner.jpg)

