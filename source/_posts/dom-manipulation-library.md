---
title: 21. DOM Manipulation Library
date: 2020-11-21 20:27:19
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
    const $ = (function () {

      // Create Constructor function here
      const Constructor = function (selector) {
        this.elements = document.querySelectorAll(selector)
      };

      // Immutable copy of the matching elements
      Constructor.prototype.items = function () {
        return Array.prototype.slice.call(this.elements);
      };

      // Get first item
      Constructor.prototype.first = function () {
        return this.elements[0];
      }

      // Get last item
      Constructor.prototype.last = function () {
        return this.elements[this.elements.length - 1];
      }

      // Add class to element
      Constructor.prototype.addClass = function (newClass) {
        this.items().forEach(element => {
          element.classList.add(newClass)
        })
      };

      // Remove class from element
      Constructor.prototype.removeClass = function (newClass) {
        this.items().forEach(element => {
          element.classList.remove(newClass)
        })
      };

      return Constructor;
    })();

    // Create new instance
    const btns = new $('.button')

    // Check the console logs in dev tools
    console.log('$.items()', btns.items())
    console.log('$.first()', btns.first())
    console.log('$.last()', btns.last())

    // Add and remove class
    btns.addClass('btn-purple');
    btns.removeClass('btn-blue');
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
/* For today’s project, we’re going to build a small DOM manipulation library
(a bit like a small, personal jQuery). */

const $ = (function () {

  // Create Constructor function here
  const Constructor = function (selector) {
    this.elements = document.querySelectorAll(selector)
  };

  // Immutable copy of the matching elements
  Constructor.prototype.items = function () {
    return Array.prototype.slice.call(this.elements);
  };

  // Get first item
  Constructor.prototype.first = function () {
    return this.elements[0];
  }

  // Get last item
  Constructor.prototype.last = function () {
    return this.elements[this.elements.length - 1];
  }

  // Add class to element
  Constructor.prototype.addClass = function (newClass) {
    this.items().forEach(element => {
      element.classList.add(newClass)
    })
  };

  // Remove class from element
  Constructor.prototype.removeClass = function (newClass) {
    this.items().forEach(element => {
      element.classList.remove(newClass)
    })
  };

  return Constructor;
})();

// Create new instance
const btns = new $('.button')

// Check the console logs in dev tools
console.log('$.items()', btns.items())
console.log('$.first()', btns.first())
console.log('$.last()', btns.last())

// Add and remove class
btns.addClass('btn-purple');
btns.removeClass('btn-blue');
```
</div>
