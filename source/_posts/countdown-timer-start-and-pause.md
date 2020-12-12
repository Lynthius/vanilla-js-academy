---
title: 31. Countdown Timer - Start and Pause
date: 2020-12-11 18:25:46
---

<div class="output-container">

  <style type="text/css">
    #app {
      margin-top: 20px;
    }

    .buttons-container {
      display: flex;
      justify-content: space-between;
      max-width: 130px;
    }

    .button {
        border-color: white;
        outline: none;
        border: none;
        margin-top: 5px;
        min-width: 60px;
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
  const timeValue = 10;
  const clickHandler = function (e) {
    startTimer(e);
    }
  const Rue = function (selector, options) {
    this.elem = document.querySelector(selector);
    this.data = options.data;
    this.template = options.template;
  };
  Rue.prototype.render = function () {
    this.elem.innerHTML = this.template(this.data);
  };
  // Rue.prototype.stopTimer = function () {
  //   this.elem.innerHTML = `<h2>It's over, start again:</h2><button onclick="app.restartTimer()" class="button">Start Again</button>`
  // }
  const startTimer = function (e) {
    if (!e.target.hasAttribute('data-start-timer')) return;
    app.data.paused = false;
      app.render();
      timer = setInterval(countdown, 1000);
  };
  Rue.prototype.formatTime = function (time) {
    let minutes = Math.floor(time / 60);
    let seconds = time % 60;
    return `${(minutes.toString())}:${seconds.toString().padStart(2,'0')}`;
  }
  const stopTimer = function () {
    clearInterval(timer)
  }
  const restartTimer = function () {
    if (!event.target.hasAttribute('data-restart-timer')) return;
    app.data.time = timeValue;
    app.data.paused = true;
    app.render();
    timer = setInterval(countdown, 1000);
  }
  const countdown = function () {
    app.data.time--
    if (app.data.time < 1) {
      stopTimer();
    }
    app.render();
  }
  const app = new Rue('#app', {
    data: {
      time: timeValue,
      paused: true
    },
    template: function (props) {
      if (!props) return;
      let html = `<h2>You've got only <span class="counter">${app.formatTime(props.time)}</span> seconds!</h2>` + 
      (props.paused ? `<div class="buttons-container"><button data-start-timer class="button start">Start</button>` : `<div class="buttons-container"><button data-pause-timer class="button start">Pause</button>`) + `<button data-restart-timer class="button stop">Restart</button></div>`
      return html;
    }
  })
  app.render();
  document.addEventListener('click', clickHandler)
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
/* For this project, we’re going to add two always-present buttons below the countdown in the timer.
One button will say Start when the timer is stopped, and Pause when it’s running.
Clicking it starts or stops the timer without resetting the time. */

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
