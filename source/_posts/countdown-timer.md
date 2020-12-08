---
title: 29. Countdown Timer
date: 2020-12-07 18:25:46
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 20px;
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

      .counter {
        color: #8e45ff;
      }
  </style>
  <div id="app" aria-live="polite"></div>
  <script>
  const duration = 6;
  const Rue = function (selector, options) {
    this.elem = document.querySelector(selector);
    this.data = options.data;
    this.template = options.template;
  };
  Rue.prototype.render = function () {
    this.elem.innerHTML = this.template(this.data);
  };
  Rue.prototype.counting = function () {
    this.data.time = 6;
    this.data.counter = setInterval(function () {
      app.render();
    }, 1000);
  };
  const app = new Rue('#app', {
    data: {
      time: duration,
    },
    template: function (props) {
      if (!props) return;
      let html = `<h2>You've got only <span class="counter">${props.time}</span> seconds!</h2>`;
      if (props.time < 0) {
        clearInterval(props.counter)
        let html = `<h2>It's over, start again:</h2><button onclick="app.counting()" class="button">Start Again</button>`
        return html;
      }
      props.time--
      return html;
    }
  })
  app.counting();
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<div id="app" aria-live="polite"></div>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Use state-based UI to create the timer, and countdown from 60 seconds to 0 once a second. 
When the timer is done, stop the countdown and provide a way for users to start it again. */

const Rue = function (selector, options) {
  this.elem = document.querySelector(selector);
  this.data = options.data;
  this.template = options.template;
};
Rue.prototype.render = function () {
  this.elem.innerHTML = this.template(this.data);
};
Rue.prototype.counting = function () {
  this.data.count = 6;
  this.data.counter = setInterval(function () {
    app.render();
  }, 1000);
};
const app = new Rue('#app', {
  data: {
    count: 6,
  },
  template: function (props) {
    if (!props) return;
    let html = `<h2>You've got only <span class="counter">${props.count}</span> seconds!</h2>`;
    if (props.count < 0) {
      clearInterval(props.counter)
      let html = `<h2>It's over, start again:</h2><button onclick="app.counting()" class="button">Start Again</button>`
      return html;
    }
    props.count--
    return html;
  }
})
app.counting();
```

</div>
