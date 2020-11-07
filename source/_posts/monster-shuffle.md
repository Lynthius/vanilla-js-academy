---
title: 12. Monster Shuffle
date: 2020-11-03
---

<div class="output-container">

  <style type="text/css">
  </style>


  <script>

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
/* Each monster (or sock) has a matching SVG in the source code.
For example, there’s a monster3 in the array, and a monster3.svg in the source code.
Shuffle the array of monsters, and render the matching SVG files into the #app element. */

let textArea = document.getElementById('text');
let letterCounter = document.getElementById('character-count');

textArea.addEventListener('input', function (e) {
  letterCounter.textContent = e.target.value.length
})
```

</div>
