##Web pages
In a website, there are multiple html document available. Whenever, we connect any website, this will connect "index.html" file. This should be a home page of that website and it is stored at root level.
Other html documents are stored under public folder. All the images are stored under assets/images folder.

If we wanted to navigate other html document, those html documents are linked in index.html page using `"<a href>"` tags and attribute.

##`HTML Boiler Plate`

###`<!DOCTYPE html>`  

- We are letting know the browser that this document code contains HTML code and the version of HTML. By default, it will consider the latest version and current latest version is HTML5
###`<html lang="en>`  

- This is the root level element of HTML document. It means all other elements should be child element of this HTML element.
- `"en"` defines the language of the text content in that element
###`<head>`  

- This is the place where we have all the information about this website. Remember, this information is NOT visible to users.
- Basically, it helps website to render its content
###`<meta>`  
```html
<head>
    <meta charset="UTF-8">
</head>
```
- Under `<head>`, `<meta>` tag for the character set should be always present.
- This ensures all the characters used in the website display properly.

###`<title>`  
``` html
<title>
    My website
</title>
```
- Under `<head>`, `<title>` tag will tell you the title of the document, and it will be displayed in the browser, NOT in web page.


###`<body>`  
```html
<body>
    CONTENT
</body>
```
- Creating content and structure of the document goes in between `<body>` and `</body>` tag
- All other tags should come under `<body>` tag
- The content updated under this tag is visible to users.

