One of the main objective of JS is to provide dialogue boxes for interaction with users and dynamically update content on web pages.

It provides functions like alert, prompt and confirm to facilitate this interaction.

These functions allow devs to display messages, gather input and obtain user confirmation. If not implemented securely, attackers may exploit these features to execute attacks like XSS.

**Alert function** displays a message in a dialogue box with an 'OK' button, typically used to convey information or warnings to uers.

**Prompt function** displays a dialogue box that asks the user for input. It returns the entered value when the user clicks "OK" or null if the user clicks "Cancel"

**Confirm** function displays a dialogue box with a message and two buttons: "OK" and "Cancel". It returns true of the user clicks "OK" ad false if the user clicks "Cancel".

For example, to ask the user for confirmation, we would use confirm("Are you sure");.

### How Hackers Exploit the Functionality

```javascript
for (let i =0; i < 100; i++){

alert("Hacked")

}
```

Imagine the following code runs every time you fire up a browser. It disrupts the user experience with so many alert messages.