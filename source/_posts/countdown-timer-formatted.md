---
title: 30. Countdown Timer - Formatted
date: 2020-12-09 18:25:46
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
  const timeValue = 120;
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
  Rue.prototype.formatTime = function (time) {
    let minutes = Math.floor(time / 60);
    let seconds = time % 60;
    return `${(minutes.toString())}:${seconds.toString().padStart(2,'0')}`;
  }
  const app = new Rue('#app', {
    data: {
      time: timeValue,
    },
    template: function (props) {
      if (!props) return;
      let html = `<h2>You've got only <span class="counter">${app.formatTime(props.time)}</span> seconds!</h2>`;
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
/* Before rendering the time into the UI, convert it into M:SS format. For example, the starting time should be displayed at 2:00. When the remaining time is 5 seconds, it should be displayed as 0:05. */

const timeValue = 120;
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
Rue.prototype.formatTime = function (time) {
  let minutes = Math.floor(time / 60);
  let seconds = time % 60;
  return `${(minutes.toString().padStart(2,'0'))}:${seconds.toString().padStart(2,'0')}`;
}
const app = new Rue('#app', {
  data: {
    time: timeValue,
  },
  template: function (props) {
    if (!props) return;
    let html = `<h2>You've got only <span class="counter">${app.formatTime(props.time)}</span> seconds!</h2>`;
    return html;
  }
})
app.timer();
```

</div>
