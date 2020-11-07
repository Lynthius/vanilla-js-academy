---
title: 05. Character and Word Count
date: 2020-10-20
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

  <p>You've written <strong><span id="word-count">0</span> words</strong> and <strong><span id="character-count">0</span> characters</strong>.</p>

  <script>
    const textArea = document.querySelector('#text');
    const countCharOutput = document.querySelector('#character-count');
    const countWordOutput = document.querySelector('#word-count');

    function counter() {
      const wordsArr = textArea.value.split(/[\n\r\s]+/g).filter(item => {
        return item.length > 0;
      });
      countCharOutput.textContent = textArea.value.length;
      countWordOutput.textContent = wordsArr.length;
    };

    textArea.addEventListener('input', counter);
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<label class="label" for="text">Enter your text below.</label>
<textarea class="textarea" id="text"></textarea>

<p>You've written <strong><span id="word-count">0</span> words</strong> and <strong><span id="character-count">0</span> characters</strong>.</p>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* As the user types or pastes content in, the text of the #word-count
and #character-count elements should be updated to show how many words
and characters are in the #text field. */

const textArea = document.querySelector('#text');
const countCharOutput = document.querySelector('#character-count');
const countWordOutput = document.querySelector('#word-count');

function counter() {
  const wordsArr = textArea.value.split(/[\n\r\s]+/g).filter(item => {
    return item.length > 0;
  });
  countCharOutput.textContent = textArea.value.length;
  countWordOutput.textContent = wordsArr.length;
};

textArea.addEventListener('input', counter);
```

</div>
