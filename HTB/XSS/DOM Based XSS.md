DOM stands for Document Object Model

It's a way for web browsers to represent a webpage as a structured, organized tree of objects that Javascript and other languages can easily read and change.

While reflected XSS sends the input data to the back-end server through HTTP requests, DOM XSS is completely processed on the client-side though JS. 

DOM XSS occurs when JS is used to change the page source through the DOM.


## Source & Sink

To further understand the nature of the DOM-based XSS vulnerability, we must understand the concept of the `Source` and `Sink` of the object displayed on the page. The `Source` is the JavaScript object that takes the user input, and it can be any input parameter like a URL parameter or an input field

On the other hand, the Sink is the function that writes the user input to a DOM Object on the page. If the Sink function does not properly sanitize the user input, it would be vulnerable to an XSS attack. Some of the commonly used JavaScript functions to write to DOM objects are:

    document.write()
    DOM.innerHTML
    DOM.outerHTML

Furthermore, some of the `jQuery` library functions that write to DOM objects are:

- `add()`
- `after()`
- `append()`

If a `Sink` function writes the exact input without any sanitization (like the above functions), and no other means of sanitization were used, then we know that the page should be vulnerable to XSS.

We can look at the source code of the To-Do web application, and check script.js, and we will see that the Source is being taken from the task= parameter:

```javascript
var pos = document.URL.indexOf("task=");
var task = document.URL.substring(pos + 5, document.URL.length);
```

Right below these lines, we see that the page uses the innerHTML function to write the task variable in the todo DOM:

```javascript
document.getElementById("todo").innerHTML = "<b>Next Task:</b> " + decodeURIComponent(task);
```


DOM Attacks

If we try the XSS payload we have been using previously, we will see that it will not execute. This is because the innerHTML function does not allow the use of the 
<script> tags within it as a security feature. Still, there are many other XSS payloads we use that do not contain <script> tags, like the following XSS payload:

<img src="" oneerror=alert(window.origin)>

The above line creates a new HTML image object, which has a `onerror` attribute that can execute JavaScript code when the image is not found. So, as we provided an empty image link (`""`), our code should always get executed without having to use `<script>` tags:


To target a user with this DOM XSS vulnerability, we can once again copy the URL from the browser and share it with them, and once they visit it, the JavaScript code should execute. Both of these payloads are among the most basic XSS payloads. There are many instances where we may need to use various payloads depending on the security of the web application and the browser, which we will discuss in the next section.