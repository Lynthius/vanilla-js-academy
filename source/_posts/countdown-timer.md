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
  const timeValue = 60;
  const Rue = function (selector, options) {
    this.elem = document.querySelector(selector);
    this.data = options.data;
    this.template = options.template;
  };
  Rue.prototype.render = function () {
    this.elem.innerHTML = this.template(this.data);
  };
   Rue.prototype.restartTimer = function () {
     this.data.time = timeValue;
     app.timer()
  }
  Rue.prototype.stopTimer = function () {
    this.elem.innerHTML = `<h2>It's over, start again:</h2><button onclick="app.restartTimer()" class="button">Start Again</button>`
  }
  Rue.prototype.timer = function () {
    const intervalCount = window.setInterval(function () {
      if(!app) return;
      app.data.time--
      app.render();
      if (app.data.time < 1) {
        window.clearInterval(intervalCount)
        app.stopTimer()
      }
    }, 1000);
      app.render();
  };
  const app = new Rue('#app', {
    data: {
      time: timeValue,
    },
    template: function (props) {
      if (!props) return;
      let html = `<h2>You've got only <span class="counter">${props.time}</span> seconds!</h2>`;
      return html;
    }
  })
  app.timer();
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

const timeValue = 6;
const Rue = function (selector, options) {
  this.elem = document.querySelector(selector);
  this.data = options.data;
  this.template = options.template;
};
Rue.prototype.render = function () {
  this.elem.innerHTML = this.template(this.data);
};
  Rue.prototype.restartTimer = function () {
    this.data.time = timeValue;
    app.timer()
}
Rue.prototype.stopTimer = function () {
  this.elem.innerHTML = `<h2>It's over, start again:</h2><button onclick="app.restartTimer()" class="button">Start Again</button>`
}
Rue.prototype.timer = function () {
  const intervalCount = window.setInterval(function () {
    if(!app) return;
    app.data.time--
    app.render();
    if (app.data.time < 1) {
      window.clearInterval(intervalCount)
      app.stopTimer()
    }
  }, 1000);
    app.render();
};
const app = new Rue('#app', {
  data: {
    time: timeValue,
  },
  template: function (props) {
    if (!props) return;
    let html = `<h2>You've got only <span class="counter">${props.time}</span> seconds!</h2>`;
    return html;
  }
})
app.timer();
```

</div>
