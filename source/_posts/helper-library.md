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
    <button class="btn-blue button" id="button-4">Button 4</button>
    <button class="btn-blue button" id="button-5">Button 5</button>
    <button class="btn-blue button here-is-johnny" id="button-6">Button 6</button>
  </p>

  <script>
    const btns = document.querySelectorAll('.button');
    const btn2 = document.querySelector('#button-2');

    const helperMethod = (function () {

      // Hold public methdos here
      const methods = {};

      // Private methods
      const nodeToArr = function (node) {
        return Array.prototype.slice.call(node);
      };

      const getFirstMatch = function (element, match) {
        return element.closest(match);
      };

      const getAllMatches = function (match) {
        return nodeToArr(document.querySelectorAll(match));
      };

      const addClassToElem = function (elements, newClass) {
        if (nodeToArr(elements).length == 0) {
        return elements.classList.add(newClass);
        } else {
          return nodeToArr(elements).map(element => {
            element.classList.add(newClass);
          })
        }
      };

      const removeClassFromElement = function (elements, newClass) {
        if (nodeToArr(elements).length == 0) {
        return elements.classList.remove(newClass);
        } else {
          return nodeToArr(elements).map(element => {
            element.classList.remove(newClass);
          })
        }
      };

      // Public methods
      methods.transformToArray = function (node) {
        return nodeToArr(node);
      };

      methods.firstMatch = function (element, match) {
        return getFirstMatch(element, match);
      };

      methods.allMatches = function (match) {
        return getAllMatches(match);
      };

      methods.addClass = function (elements, newClass) {
        return addClassToElem(elements, newClass);
      };

      methods.removeClass = function (elements, newClass) {
        return removeClassFromElement(elements, newClass);
      }

      return methods;
    })();

    // Check the console logs in dev tools
    console.log('helperMethod.transformToArray(btns)', helperMethod.transformToArray(btns));
    console.log('helperMethod.firstMatch(btn2, ".here-is-johnny")', helperMethod.firstMatch(btn2, '.here-is-johnny'));
    console.log('helperMethod.allMatches(".here-is-johnny")', helperMethod.allMatches('.here-is-johnny'));

    // Add and remove classes
    helperMethod.addClass(btns, 'btn-purple');
    helperMethod.removeClass(btn2, 'btn-purple');
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>
  <button class="btn-blue button" id="button-1">Button 1</button>
  <button class="btn-blue button here-is-johnny" id="button-2">Button 2</button>
  <button class="btn-blue button" id="button-3">Button 3</button>
  <button class="btn-blue button" id="button-4">Button 4</button>
  <button class="btn-blue button" id="button-5">Button 5</button>
  <button class="btn-blue button here-is-johnny" id="button-6">Button 6</button>
</p>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* In today’s project, we’re going to create a helper library. */

const btns = document.querySelectorAll('.button');
const btn2 = document.querySelector('#button-2');

const helperMethod = (function () {

  // Hold public methdos here
  const methods = {};

  // Private methods
  const nodeToArr = function (node) {
    return Array.prototype.slice.call(node);
  };

  const getFirstMatch = function (element, match) {
    return element.closest(match);
  };

  const getAllMatches = function (match) {
    return nodeToArr(document.querySelectorAll(match));
  };

  const addClassToElem = function (elements, newClass) {
    if (nodeToArr(elements).length == 0) {
    return elements.classList.add(newClass);
    } else {
      return nodeToArr(elements).map(element => {
        element.classList.add(newClass);
      })
    }
  };

  const removeClassFromElement = function (elements, newClass) {
    if (nodeToArr(elements).length == 0) {
    return elements.classList.remove(newClass);
    } else {
      return nodeToArr(elements).map(element => {
        element.classList.remove(newClass);
      })
    }
  };

  // Public methods
  methods.transformToArray = function (node) {
    return nodeToArr(node);
  };

  methods.firstMatch = function (element, match) {
    return getFirstMatch(element, match);
  };

  methods.allMatches = function (match) {
    return getAllMatches(match);
  };

  methods.addClass = function (elements, newClass) {
    return addClassToElem(elements, newClass);
  };

  methods.removeClass = function (elements, newClass) {
    return removeClassFromElement(elements, newClass);
  }

  return methods;
})();

// Check the console logs in dev tools
console.log('helperMethod.transformToArray(btns)', helperMethod.transformToArray(btns));
console.log('helperMethod.firstMatch(btn2, ".here-is-johnny")', helperMethod.firstMatch(btn2, '.here-is-johnny'));
console.log('helperMethod.allMatches(".here-is-johnny")', helperMethod.allMatches('.here-is-johnny'));

// Add and remove classes
helperMethod.addClass(btns, 'btn-purple');
helperMethod.removeClass(btn2, 'btn-purple');
```

</div>
