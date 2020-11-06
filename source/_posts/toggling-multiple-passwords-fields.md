---
title: 02. Toggling multiple passwords fields
date: 2020-10-14
---

<div class="output-container">

  <style type="text/css">
    .label {
      display: block;
      width: 100%;
      margin-bottom: 6px;
    }

    .input {
      margin-bottom: 1em;
      border: none;
      border-radius: 3px;
      padding: 3px 4px;
      min-width: 100px;
    }

    .input:focus {
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .checkbox:focus {
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .button {
      border-color: white;
      outline: none;
      border: none;
      margin-top: 5px;
      padding: 5px 10px;
      border-radius: 3px;
      font-weight: 600px;
      cursor: pointer;
    }

    .button:focus {
      border: red;
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .button:active {
      color: #8e45ff;
    }

    [type="checkbox"] {
      margin-bottom: 0;
      margin-right: 0.25em;
      cursor: pointer;
    }
  </style>

  <p>Enter your current password and new password below.</p>

  <form>
    <div>
      <label class="label" for="username">Username:</label>
      <input autocomplete="off" class="input" type="text" name="username" id="username">
    </div>
    <div>
      <label class="label" for="current-password">Current Password:</label>
      <input autocomplete="off" class="input password" type="password" name="password" id="current-password">
    </div>
    <div>
      <label class="label" for="new-password">New Password:</label>
      <input autocomplete="off" class="input password" type="password" name="password" id="new-password">
    </div>
    <div>
      <label class="label" for="show-password">
        <input class="checkbox" type="checkbox" name="show-passwords" id="show-passwords">
        Show passwords
      </label>
    </div>
    <button class="button" type="submit">Log In</button>
  </form>

  <script>
    const togglePswrd = document.querySelector('#show-passwords');
    const passInputs = document.querySelectorAll('.password');

    togglePswrd.addEventListener('click', function () {
      if (togglePswrd.checked) {
        Array.prototype.slice.call(passInputs).forEach(passInput => {
          passInput.type = "text";
        });
      } else {
        Array.prototype.slice.call(passInputs).forEach(passInput => {
          passInput.type = "password";
        });
      }
    })
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>Enter your current password and new password below.</p>

<form>
  <div>
    <label class="label" for="username">Username:</label>
    <input autocomplete="off" class="input" type="text" name="username" id="username">
  </div>
  <div>
    <label class="label" for="current-password">Current Password:</label>
    <input autocomplete="off" class="input password" type="password" name="password" id="current-password">
  </div>
  <div>
    <label class="label" for="new-password">New Password:</label>
    <input autocomplete="off" class="input password" type="password" name="password" id="new-password">
  </div>
  <div>
    <label class="label" for="show-password">
      <input class="checkbox" type="checkbox" name="show-passwords" id="show-passwords">
      Show passwords
    </label>
  </div>
  <button class="button" type="submit">Log In</button>
</form>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* When a user clicks on the #show-passwords checkbox, 
it should show the text for the #current-password and #new-password fields 
if it’s checked, and mask it if it’s unchecked. */

const togglePswrd = document.querySelector('#show-passwords');
const passInputs = document.querySelectorAll('.password');

togglePswrd.addEventListener('click', function () {
  if (togglePswrd.checked) {
    Array.prototype.slice.call(passInputs).forEach(passInput => {
      passInput.type = "text";
    });
  } else {
    Array.prototype.slice.call(passInputs).forEach(passInput => {
      passInput.type = "password";
    });
  }
})
```

</dvi>
