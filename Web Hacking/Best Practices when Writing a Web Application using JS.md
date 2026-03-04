
### Avoid Relying on Client-Side Validation Only

One of JS's primary functions is performing client-side validation.  Developers sometimes use it for validating forms and rely entirely on it, which is not a good practice.

Since a user can disable/manipulate JS on the client side, performing validation on the server side is also essential.

### Refrain from Adding Untrusted Libraries
### Avoid Hardcoded Secrets

Never hardcode sensitive data like **API keys**, **access tokens**, or **credentials** into your JS code, as the user can easily check the source code and get the password.

### Minify and Obfuscate Your JavaScript Code

Minifying and obfuscating JS code reduces its size, improves load time, and makes it harder for attackers to understand the logic of the code. Therefore, always **minify** and **obfuscate** the code when using code in production. The attacker can eventually reverse engineer it, but getting the original code will take at least some effort.

