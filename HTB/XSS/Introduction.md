XSS vulnerabilities take advantage of a flaw in user sanitization to "write" Javascript code to the page and execute it on the client side, leading to several types of attacks.

A typical web app works by receiving the HTML code from the backend server and rendering it on the client-side internet browser.

When a web app does not properly sanitize user input, a malicious user can inject extra JS  code in an input (e.g comment/reply) so once another user views the same page, they unknowingly execute the malicious JS code.

XSS vulnerabilities are solely executed on the client-side and hence do not directly affect the back-end server. They can only affect the user executing the vulnerability.

Impact on the backend server may be relatively low, but they are very commonly found in web apps.

A basic example of XSS is having the target user unwittingly send their session cookie to the attacker's web server.

Another example is having the target's browser execute API calls that lead to a malicious action, like changing the user's password to a password of the attacker's choosing.

There are many types of XSS attacks, from Bitcoin mining to displaying ads.

As XSS attack execute Javascript code within the browser, they are limited to the browser's JS engine (i.e., V8 in Chrome)

They cannot execute system-wide Javascript code to do something like system-level code execution.  In modern websites, they are also limited to the same domain of the vulnerable website.


**Types of XSS**

- Stored (Persistent)
- Reflected (Non-Persistent)
- DOM-based XSS

