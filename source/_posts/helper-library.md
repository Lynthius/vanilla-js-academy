---
title: 20. Helper Library
date: 2020-11-19 20:27:19
---

<div class="output-container">

  <style type="text/css">
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

    .btn-blue {
      background-color: #0088cc;
      color: #ffffff;
    }

    .btn-purple {
      background-color: rebeccapurple;
      color: #ffffff;
    }
  </style>
  <p>
    <button class="btn-blue button" id="button-1">Button 1</button>
    <button class="btn-blue button here-is-johnny" id="button-2">Button 2</button>
    <button class="btn-blue button" id="button-3">Button 3</button>
  </p>

  <script>
    const btns = document.querySelectorAll('.button');

    const helperMethod = (function () {

      // Hold public methdos here
      const methods = {};

      // Private methods
      const nodeToArr = function (node) {
        return Array.prototype.slice.call(node);
      };

      const getFirstMatch = function (elements, match) {
        nodeToArr(elements).map(element => {
          if (element.matches(match)) {
            console.log(element);
            return element;
          } else {
            console.log('Not a match');
          };
        })
        };

      // Public methods
      methods.transformToArray = function (node) {
        return nodeToArr(node);
      };

      methods.firstMatch = function (element, match) {
        return getFirstMatch(element, match);
      }

      return methods;
    })();

    // Check the console logs in dev tools
    helperMethod.transformToArray(btns);
    helperMethod.firstMatch(btns, '.here-is-johnny');

  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML

```

</div>
<div class="js-container">

## JavaScript

```JS
/* In today’s project, we’re going to create a helper library. */

```

</div>
