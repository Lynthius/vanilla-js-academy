---
title: 03. Toggling passwords in multiple forms
date: 2020-10-16
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

  <h2>Change Username</h2>

  <p>Enter your username and password to change your username.</p>

  <form>
    <div>
      <label class="label" for="username">Username</label>
      <input autocomplete="off" class="input" type="text" name="username" id="username">
    </div>
    <div>
      <label class="label" for="password">Password</label>
      <input autocomplete="off" class="input" type="password" name="password" id="password">
    </div>
    <div>
      <label class="label" for="show-password">
        <input class="checkbox" type="checkbox" name="show-password" id="show-password" data-pw-toggle="#password">
        Show password
      </label>
    </div>
    <p>
      <button class="button" type="submit">Change Username</button>
    </p>
  </form>

  <h2>Change Password</h2>

  <p>Enter your current password and new password below.</p>

  <form>
    <div>
      <label class="label" for="current-password">Current Password</label>
      <input autocomplete="off" class="input" type="password" name="current-password" id="current-password">
    </div>
    <div>
      <label class="label" for="new-password">New Password</label>
      <input autocomplete="off" class="input" type="password" name="new-password" id="new-password">
    </div>
    <div>
      <label class="label" for="show-passwords">
        <input class="checkbox" type="checkbox" name="show-passwords" id="show-passwords"
          data-pw-toggle="#current-password, #new-password">
        Show passwords
      </label>
    </div>
    <p>
      <button class="button" type="submit">Change Passwords</button>
    </p>
  </form>

<script>
  document.addEventListener('click', function (e) {
    if (!e.target.matches('[data-pw-toggle]')) return;

    const passwords = Array.prototype.slice.call(document.querySelectorAll(e.target.getAttribute(
      'data-pw-toggle')));

    passwords.forEach(password => {
      if (e.target.checked) {
        password.type = 'text';
      } else {
        password.type = 'password';
      }
    })
  })
</script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<h2>Change Username</h2>

  <p>Enter your username and password to change your username.</p>

  <form>
    <div>
      <label class="label" for="username">Username</label>
      <input autocomplete="off" class="input" type="text" name="username" id="username">
    </div>
    <div>
      <label class="label" for="password">Password</label>
      <input autocomplete="off" class="input" type="password" name="password" id="password">
    </div>
    <div>
      <label class="label" for="show-password">
        <input class="checkbox" type="checkbox" name="show-password" id="show-password" data-pw-toggle="#password">
        Show password
      </label>
    </div>
    <p>
      <button class="button" type="submit">Change Username</button>
    </p>
  </form>

  <h2>Change Password</h2>

  <p>Enter your current password and new password below.</p>

  <form>
    <div>
      <label class="label" for="current-password">Current Password</label>
      <input autocomplete="off" class="input" type="password" name="current-password" id="current-password">
    </div>
    <div>
      <label class="label" for="new-password">New Password</label>
      <input autocomplete="off" class="input" type="password" name="new-password" id="new-password">
    </div>
    <div>
      <label class="label" for="show-passwords">
        <input class="checkbox" type="checkbox" name="show-passwords" id="show-passwords"
          data-pw-toggle="#current-password, #new-password">
        Show passwords
      </label>
    </div>
    <p>
      <button class="button" type="submit">Change Passwords</button>
    </p>
  </form>
```

</div>
<div class="js-container">

## JavaScript

```JS
document.addEventListener('click', function (e) {
  if (!e.target.matches('[data-pw-toggle]')) return;

  const passwords = Array.prototype.slice.call(document.querySelectorAll(e.target.getAttribute('data-pw-toggle')));

  passwords.forEach(password => {
    if (e.target.checked) {
      password.type = 'text';
    } else {
      password.type = 'password';
    }
  })
})
```

</dvi>
