---
title: 26. Autosave - Other Field Types
date: 2020-12-01 16:45:14
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

    .select {
      border-radius: 3px;
      height: 22px;
      padding: 3px 4px;
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
    <label for="hear-about-us">How did you hear about us?</label>
	  <select data-type="input" class="select" name="hear-about-us" id="hear-about-us">
      <option value=""></option>
      <option value="google">Google</option>
      <option value="referral">Referred by a Friend</option>
      <option value="tv">A TV Ad</option>
      <option value="radio">A Radio Ad</option>
	  </select>
    <br><br>
    <label class="label" for="more">Additional thoughts?</label>
    <textarea data-type="input" class="textarea" name="more" id="more"></textarea>
    <p><strong>Do you agree to our terms of service?</strong></p>
	<label class="label" for="tos">
		<input data-type="input" type="radio" name="tos" value="yes">
		Yes
		<input data-type="input" type="radio" name="tos" value="no">
		No
	</label>
	<p><strong>Pick your favorite super heros.</strong></p>
	<label>
		<input data-type="input" type="checkbox" name="spiderman">
		Spiderman
	</label>
	<label>
		<input data-type="input" type="checkbox" name="wonderwoman">
		Wonder Woman
	</label>
	<label>
		<input data-type="input" type="checkbox" name="blackpanther">
		Black Panther
	</label>
    <p>
      <button class="button" type="submit">Submit</button>
    </p>
  </form>
  <script>
    const form = document.querySelector('#save-me');
    function saveInputValue(e) {
      let savedInputs = localStorage.getItem('autosave-form-inputs');
      savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
      if (e.target.type === "checkbox") {
        savedInputs[e.target.name] = e.target.checked ? "on" : "off";
      } else {
        savedInputs[e.target.name] = e.target.value;
      }
      localStorage.setItem('autosave-form-inputs', JSON.stringify(savedInputs));
    }
    function getInputsFromLocalStorage() {
      let inputs = Array.prototype.slice.call(document.querySelectorAll('[data-type="input"]'));
      let savedInputs = localStorage.getItem('autosave-form-inputs');
      savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
      inputs.forEach(function (input) {
        if (!savedInputs[input.name]) return;
        if (input.type === "checkbox") {
          input.checked = savedInputs[input.name] === "on" ? true : false;
        } else if (input.type === "radio") {
          input.checked = savedInputs[input.name] === input.value ? true : false;
        } else {
          input.value = savedInputs[input.name];
        }
      })
    }
    function clearDataOnSubmit() {
      localStorage.clear();
    }
    form.addEventListener('input', saveInputValue);
    form.addEventListener('submit', clearDataOnSubmit);
    getInputsFromLocalStorage();
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>Fill the form below.</p>
<form class="save-me" id="save-me" autocomplete="off">
  <label class="label" for="name">Name</label>
  <input data-type="input" class="input" type="text" name="name" id="name" autocomplete="off">
  <label class="label" for="address">Address</label>
  <input data-type="input" class="input" type="text" name="address" id="address">
  <label class="label" for="email">Email</label>
  <input data-type="input" class="input" type="email" name="email" id="email">
  <label for="hear-about-us">How did you hear about us?</label>
  <select data-type="input" class="select" name="hear-about-us" id="hear-about-us">
    <option value=""></option>
    <option value="google">Google</option>
    <option value="referral">Referred by a Friend</option>
    <option value="tv">A TV Ad</option>
    <option value="radio">A Radio Ad</option>
  </select>
  <br><br>
  <label class="label" for="more">Additional thoughts?</label>
  <textarea data-type="input" class="textarea" name="more" id="more"></textarea>
  <p><strong>Do you agree to our terms of service?</strong></p>
<label class="label" for="tos">
  <input data-type="input" type="radio" name="tos" value="yes">
  Yes
  <input data-type="input" type="radio" name="tos" value="no">
  No
</label>
<p><strong>Pick your favorite super heros.</strong></p>
<label>
  <input data-type="input" type="checkbox" name="spiderman">
  Spiderman
</label>
<label>
  <input data-type="input" type="checkbox" name="wonderwoman">
  Wonder Woman
</label>
<label>
  <input data-type="input" type="checkbox" name="blackpanther">
  Black Panther
</label>
  <p>
    <button class="button" type="submit">Submit</button>
  </p>
</form>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* In today’s project, we’re going to modify our form saver script
to handle field types beyond text inputs. */

const form = document.querySelector('#save-me');
function saveInputValue(e) {
  let savedInputs = localStorage.getItem('autosave-form-inputs');
  savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
  if (e.target.type === "checkbox") {
    savedInputs[e.target.name] = e.target.checked ? "on" : "off";
  } else {
    savedInputs[e.target.name] = e.target.value;
  }
  localStorage.setItem('autosave-form-inputs', JSON.stringify(savedInputs));
}
function getInputsFromLocalStorage() {
  let inputs = Array.prototype.slice.call(document.querySelectorAll('[data-type="input"]'));
  let savedInputs = localStorage.getItem('autosave-form-inputs');
  savedInputs = savedInputs ? JSON.parse(savedInputs) : {};
  inputs.forEach(function (input) {
    if (!savedInputs[input.name]) return;
    if (input.type === "checkbox") {
      input.checked = savedInputs[input.name] === "on" ? true : false;
    } else if (input.type === "radio") {
      input.checked = savedInputs[input.name] === input.value ? true : false;
    } else {
      input.value = savedInputs[input.name];
    }
  })
}
function clearDataOnSubmit() {
  localStorage.clear();
}
form.addEventListener('input', saveInputValue);
form.addEventListener('submit', clearDataOnSubmit);
getInputsFromLocalStorage();
```

</div>
