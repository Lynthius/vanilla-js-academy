---
title: 24. Autosave
date: 2020-11-27 16:45:14
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
    let inputs = Array.prototype.slice.call(document.querySelectorAll('[data-type="input"]'));
    function saveInputValue (e) {
      if (e.target.length < 0 ) return;
      localStorage.setItem(`form-${e.target.id}`, e.target.value);
    }
    function getInputsFromLocalStorage () {
      inputs.forEach(function (input){
        input.value = localStorage.getItem(`form-${input.id}`);
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
/* For today’s project, we’re going to write a script
that automatically saves form field data as a user types. */

const form = document.querySelector('#save-me');
let inputs = Array.prototype.slice.call(document.querySelectorAll('[data-type="input"]'));
function saveInputValue (e) {
  if (e.target.length < 0 ) return;
  localStorage.setItem(`form-${e.target.id}`, e.target.value);
}
function getInputsFromLocalStorage () {
  inputs.forEach(function (input){
    input.value = localStorage.getItem(`form-${input.id}`);
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
