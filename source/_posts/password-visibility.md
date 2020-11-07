---
title: 01. Password visibility
date: 2020-10-12
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

  <p>Enter your username and password below to login.</p>

  <form>
    <div>
      <label class="label" for="username">Username:</label>
      <input autocomplete="off" class="input" type="text" name="username" id="username">
    </div>
    <div>
      <label class="label" for="password">Password:</label>
      <input autocomplete="off" class="input" type="password" name="password" id="password">
    </div>
    <div>
      <label class="label" for="show-password">
        <input class="checkbox" type="checkbox" name="show-passwords" id="show-password">
        Show password
      </label>
    </div>
    <button class="button" type="submit">Log In</button>
  </form>

  <script>
  const showPass = document.querySelector('#show-password');
  const passInput = document.querySelector('#password');

  showPass.addEventListener('click', function () {
    if (showPass.checked) {
      passInput.type = "text";
    } else {
      passInput.type = "password";
    };
  });
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>Enter your username and password below to login.</p>

<form>
  <div>
    <label for="username">Username:</label>
    <input type="text" name="username" id="username">
  </div>

  <div>
      <label for="password">Password:</label>
      <input type="password" name="password" id="password">
  </div>

  <div>
      <label for="show-password">
        <input type="checkbox" name="show-passwords" id="show-password">
        Show password
      </label>
  </div>

  <p>
    <button type="submit">Log In</button>
  </p>
</form>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* When a user clicks the #show-password checkbox, 
the #password field should display the password in plain text 
if the box is checked, or mask it if it’s not. */

const showPass = document.querySelector('#show-password');
const passInput = document.querySelector('#password');

showPass.addEventListener('click', function () {
  if (showPass.checked) {
    passInput.type = "text";
  } else {
    passInput.type = "password";
  };
});
```

</div>
