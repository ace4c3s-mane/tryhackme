There are two main types of Non-persistent XSS vulns. Reflected XSS, which gets processed by the backend server and DOM-based XSS which is completely processed on the client-side and never reaches the backend server.

Unlike Persistent XSS, Non-Persistent XSS vulnerabilities are temporary and are not persistent through page refreshes. Hence our attacks only affect the targeted user and will not affect other users who visit the page.


Reflected XSS occurs when our input reaches the back-end server and gets returned to us without being filtered and sanitized.

There are many cases in which our entire input might get returned to us, like error messages or confirmation messages. In these cases, we may attempt using XSS payloads to see whether they execute. However, as these are usually temporary messages, once we move from the page, they would not execute again, and hence they are Non-Persistent


But if the XSS vulnerability is Non-Persistent, how would we target victims with it?


As we can see, the first row shows that our request was a `GET` request. `GET` request sends their parameters and data as part of the URL. 

So, `to target a user, we can send them a URL containing our payload`. To get the URL, we can copy the URL from the URL bar in Firefox after sending our XSS payload, or we can right-click on the `GET` request in the `Network` tab and select `Copy>Copy URL`. 

Once the victim visits this URL, the XSS payload would execute:
