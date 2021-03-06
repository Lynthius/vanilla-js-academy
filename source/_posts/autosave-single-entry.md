---
title: 25. Autosave - Single Entry
date: 2020-11-29 16:45:14
---

<div class="output-container">

  <style type="text/css">
    .label {
      display: block;
      margin-bottom: 6px;
    }

    .input {
      margin-bottom: 1em;
      width: 100%;
      border: none;
      border-radius: 3px;
      padding: 3px 4px;
      min-width: 100px;
      height: 20px;
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

    .textarea {
      border-radius: 3px;
      width: 100%;
      height: 8em;
    }

    .textarea:focus {
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }
  </style>
  <p>Fill the form below.</p>
  <form class="save-me" id="save-me" autocomplete="off">
    <label class="label" for="name">Name</label>
    <input data-type="input" class="input" type="text" name="name" id="name" autocomplete="off">
    <label class="label" for="address">Address</label>
    <input data-type="input" class="input" type="text" name="address" id="address">
    <label class="label" for="email">Email</label>
    <input data-type="input" class="input" type="email" name="email" id="email">
    <label class="label" for="more">Additional thoughts?</label>
    <textarea data-type="input" class="textarea" name="more" id="more"></textarea>
    <p>
      <button class="button" type="submit">Submit</button>
    </p>
  </form>
  <script>
    const form = document.querySelector('#save-me');
    function saveInputValue (e) {
      let savedInputs = localStorage.getItem('form-inputs');
      savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
      savedInputs[e.target.id] = `${e.target.value}`;
      localStorage.setItem('form-inputs', JSON.stringify(savedInputs));
    }
    function getInputsFromLocalStorage () {
      let inputs = Array.prototype.slice.call(document.querySelectorAll('[data-type="input"]'));
      let savedInputs = localStorage.getItem('form-inputs');
      savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
      inputs.forEach(function(input) {
      if (!savedInputs[input.id]) return;
        input.value = savedInputs[input.id];
      })
    }
    function clearDataOnSubmit () {
      localStorage.clear();
    }
    form.addEventListener('input', saveInputValue);
    form.addEventListener('submit', clearDataOnSubmit);
    getInputsFromLocalStorage ();
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>Fill the form below.</p>
<form class="save-me" id="save-me" autocomplete="off">
  <label class="label" for="name">Name</label>
  <input class="input" type="text" name="name" id="name" autocomplete="off">
  <label class="label" for="address">Address</label>
  <input class="input" type="text" name="address" id="address">
  <label class="label" for="email">Email</label>
  <input class="input" type="email" name="email" id="email">
  <label class="label" for="more">Additional thoughts?</label>
  <textarea class="textarea" name="more" id="more"></textarea>
  <p>
    <button class="button" type="submit">Submit</button>
  </p>
</form>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Modify the script to store all of the fields into a single array or object
that you save and retrieve from locationStorage. To avoid conflicts with yesterday’s project,
you might want to give the localStorage item a different key name. */

const form = document.querySelector('#save-me');
function saveInputValue (e) {
  let savedInputs = localStorage.getItem('form-inputs');
  savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
  savedInputs[e.target.id] = `${e.target.value}`;
  localStorage.setItem('form-inputs', JSON.stringify(savedInputs));
}
function getInputsFromLocalStorage () {
  let inputs = Array.prototype.slice.call(document.querySelectorAll('[data-type="input"]'));
  let savedInputs = localStorage.getItem('form-inputs');
  savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
  inputs.forEach(function(input) {
  if (!savedInputs[input.id]) return;
    input.value = savedInputs[input.id];
  })
}
function clearDataOnSubmit () {
  localStorage.clear();
}
form.addEventListener('input', saveInputValue);
form.addEventListener('submit', clearDataOnSubmit);
getInputsFromLocalStorage ();
```

</div>
