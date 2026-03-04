
Sample code for age verification in JS:

```javascript
<!DOCTYPE html>

  

<html lang="en">

<head>

<title>Age Verification</title>

</head>
  

<body>

<h1>Age Verification</h1>

<p id="message"></p>

<script>

age = prompt("What is your age: ")

if (age >= 18) {

document.getElementById("message").innerHTML = "You are old enough to vote"

} else{

document.getElementById("message").innerHTML = "You're too young to vote"

}

</script>

</body>
</html>
```


Suppose a developer has implemented authentication functionality in JS, where only users with the username "admin" and passwords matching a specific value are allowed to log in.

Look at this code:

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Login Page</title>
</head>
<body>
    <h2>Login Authentication</h2>

    <script>
        let username = prompt("Enter your username:");
        let password = prompt("Enter your password:");

        if (username === "admin" && password === "ComplexPassword") {
            document.write("You are successfully authenticated!");
        } else {
            document.write("Authentication failed. Incorrect username or password.");
        }
    </script>
</body>
</html>

```

All revealed by the source code.