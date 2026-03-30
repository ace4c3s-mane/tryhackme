
If our injected XSS payload gets stored in the back-end database and retrieved upon visiting the page, this means that our XSS attack is persistent and may affect any user that visits the page.

Stored cross-site scripting (also known as second-order or persistent XSS) arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way. 

This makes this type of XSS the most critical, as it affects a much wider audience since any user who visits the page would be a victim of this attack.

Stored XSS may not be easily removable and the payload may need removing from the back-end database.

Many modern websites don't put actual form/input directly on their main page. Instead they load the form inside an invisible IFrame that comes from a different domain.

If someone finds an XSS vuln in that form, (inside the IFrame) the malicious code only runs inside the IFrame, not on the main website.

So alert(1) would still pop up, but you wouldn't know which form or which domain is actually vulnerable.

By using window.origin, in the alert, the popup tells us exactly which website/domain the vulnerable code is running on.

Normal XSS test:

```javascript
alert(1) - just shows a box with a number 1
```

![[Pasted image 20260323214035.png]]

Windows.origin

```javascript
alert(windows.origin) - shows a box with the actual URL/domain where the XSS is executing
```

![[Pasted image 20260323213950.png]]

This is super useful when the site uses IFrames, because it clearly tells you "Hey, the vulnerability is in this specific iframe coming from this domain".


Real World example

Main Site: https://bank.com (looks secure)
- It loads the login form  inside an IFrame from https://forms.bank.com

Your test for XSS on the login form and inject:

```javascript
<script>alert(window.origin)</script>
```

An alert box pops up saying: https://forms.bank.com
Now you know the vulnerable part is not the main bank.com but the forms.bank.com subdomain (the IFrame)

Without window.origin, you would just see alert(1) and might think the main bank.com is vulnerable, which would be wrong and very confusing.


IFrame (inline frame) is a way to embed another webpage (or document inside your current webpage). It's like a little window or mini-browser cut into your main page. The content inside the iframe loads from its own URL and runs almost independently from the main page.

```javascript
<iframe src="https://example.com/form.html" width="600" height="400" </iframe>
```

Common examples include:
Google maps embedded on websites
YouTube videos - the video play you see on a blog is usually inside an iframe.
Advertisements - many ads load in iframes.


Sometimes, the classic alert(1) popup gets blocked by modern browsers (especially in iframes or certain input fields)

So instead of relying only on alert(), we can rely on:

```html
<plaintext>
```

It tells the browser:
From now on, stop interpreting HTML and just show everything as plain text.

If it works, you will suddenly see all the HTML code that comes after your payload displayed as raw text on the page (instead of being rendered normally) this proves XSS.


```html
<script>print()</script>
```

This tries to open the browser's Print dialog. This is useful because, almost no browser blocks the print() function by default. It's very noticeble.

If this works, the browser will immediately show the "print" dialog. That confirms XSS is working, even if alert() was blocked.

The following can also be used:

```javascript
<script>alert(window.origin)</script>
<script>prompt(window.origin)</script>
<script>confirm(window.origin)</script>
<img src=x onerror=alert(window.origin)>
<svg><desc><![CDATA[</desc><script>alert(window.origin)</script>]]></svg>
```


