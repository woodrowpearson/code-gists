# JavaScript

```javascript
// Click on buttons in a page
// https://twitter.com/brian_lovin/status/1240662440666222597

let buttons = document.getElementsByClassName("unfollow");

for (let [i, v] of [...buttons].entries()) {
  setTimeout(() => {
    buttons[i].click();
  }, i * 500);
}
```

```javascript
// Go to specific URL
window.location.href = "https://www.google.com";
```

