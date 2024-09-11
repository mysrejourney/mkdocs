Styling sheet will help to arrange the things in a specific way to look at our website more beautiful.
To do this, there are many languages are available. Some of them are below.

1. CSS (Cascading Style Sheet)
2. Sass (Syntactically Awesome Style Sheet)
3. Less (Leaner CSS)

#<span style="color:red">C</span>ascading <span style="color:red">S</span>tyle <span style="color:red">S</span>heet (CSS)
- It is a language to specify how the things should look in our website.
- It allowed us to attach the style such as colors, font, spacing, etc. to our HTML documents.

`TRIVIA: Who created CSS?`

`Answer: Hakon Wium Lie`

## How to add CSS
There are three ways we can add CSS into our HTML documents.
<ul>
<li>Inline</li>
</ul>

```html
<tag style="PROPERTY:VALUE"/>
```

<ul>
<li>Internal</li>
</ul>

```html
<style>css</style>
```

<ul>
<li>External</li>
</ul>

```html
<link href="style.css">
```

### 1. Inline

This will be applied in the same line as the HTML element.
It is <mark>useful when you work with a single HTML element.
However, this is NOT useful if you are dealing with multi page and multiple HTML elements </mark>.
Hence, it is NOT recommended for those cases.
```html
<body style="background-color:red">
<p>Satheesh Pandian</p>
</body>
```

![inline](../assets/inline.jpg)

### 2. Internal

This will be applied via `style` tag in the HTML document under `head` element. The main difference between inline and internal is that inline can be applied anywhere in the HTML document, whereas internal can be applied only under `head` element.
However, it can have the selector element that applies the internal CSS rule to that selector element.<br>
This can be <mark>useful if you are working in a single HTML document and NOT useful for multi page website. </mark>
``` html
<head>
    <style>
        body {
            background-color: blue;
        }
    </style>
</head>
<body>
    <p>Satheesh Pandian</p>
</body>
```

![internal](../assets/internal.jpg)

### 3. External

The main difference between internal and external is that all style components are stored in external file and will be invoked in HTML file and apply the style.
This will be applied using `link` element under `head` section in the HTML document. This is useful for multi page website.

```html
<head>
    <link href="style.css" rel="stylesheet" /> <! –– rel means relationship -->
</head>
<body>
    <p>Satheesh Pandian</p>
</body>
```

```
body{
    background-color: yellow
}
```

![external](../assets/external.jpg)
