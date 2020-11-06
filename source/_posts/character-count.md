---
title: 04. Character Count
date: 2020-10-18
---

<div class="output-container">

  <style type="text/css">
    .label {
    display: block;
    width: 100%;
    margin-bottom: 6px;
    }

    .textarea {
      min-width: 400px;
      min-height: 80px;
    }

     .textarea:focus {
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }
  </style>

  <label class="label" for="text">Enter your text below.</label>
  <textarea class="textarea" id="text"></textarea>

  <p>You've written <strong><span id="character-count">0</span> characters</strong>.</p>

  <script>
    let textArea = document.getElementById('text');
    let letterCounter = document.getElementById('character-count');
    
    textArea.addEventListener('input', function (e) {
      letterCounter.textContent = e.target.value.length
    })
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<label class="label" for="text">Enter your text below.</label>
<textarea class="textarea" id="text"></textarea>

<p>You've written <strong><span id="character-count">0</span> characters</strong>.</p>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* As the user types or pastes text into the #text field, 
the #character-count content should get updated in real time 
to display how many characters are in the field. */

let textArea = document.getElementById('text');
let letterCounter = document.getElementById('character-count');

textArea.addEventListener('input', function (e) {
  letterCounter.textContent = e.target.value.length
})
```

</dvi>
