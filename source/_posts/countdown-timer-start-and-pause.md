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
    let timer;
    const Rue = function (selector, options) {
      this.elem = document.querySelector(selector);
      this.data = options.data;
      this.template = options.template;
    };
    Rue.prototype.render = function () {
      this.elem.innerHTML = this.template(this.data);
    };
    const formatTime = function (time) {
      let minutes = Math.floor(time / 60);
      let seconds = time % 60;
      return `${(minutes.toString())}:${seconds.toString().padStart(2,'0')}`;
    }
    const startTimer = function (e) {
      if (!e.target.hasAttribute('data-start-timer')) return;
      if (app.data.time < 1) {
        app.data.time = timeValue;
      }
      app.data.paused = false;
      app.render();
      stopTimer();
      timer = setInterval(countdown, 1000);
    };
    const countdown = function () {
      app.data.time--
      if (app.data.time < 1) {
        stopTimer();
        app.data.paused = true;
      }
      app.render();
    }
    const stopTimer = function () {
      clearInterval(timer)
    }
    const pauseTimer = function (e) {
      if (!e.target.hasAttribute('data-pause-timer')) return;
      stopTimer();
      app.data.paused = true;
      app.render();
    }
    const restartTimer = function (e) {
      if (!e.target.hasAttribute('data-restart-timer') || app.data.time === timeValue) return;
      stopTimer();
      app.data.time = timeValue;
      app.data.paused = false;
      app.render();
      timer = setInterval(countdown, 1000);
    }
    const clickHandler = function (e) {
      startTimer(e);
      restartTimer(e);
      pauseTimer(e);
    }
    const app = new Rue('#app', {
      data: {
        time: timeValue,
        paused: true,
        altMsg: true
      },
      template: function (props) {
        if (!props) return;
        if (props.time === 0 && props.altMsg) {
          let html = `<h2>It's over, start again:</h2><button data-restart-timer class="button stop">Restart</button></div>`
          return html;
        }
        let html = `<h2>You've got only <span class="counter">${formatTime(props.time)}</span> seconds!</h2>` +
          (props.paused ? `<div class="buttons-container"><button data-start-timer class="button start">Start</button>` : `<div class="buttons-container"><button data-pause-timer class="button start">Pause</button>`) + `<button data-restart-timer class="button stop">Restart</button></div>`
        return html;
      }
    })
    app.render();
    document.addEventListener('click', clickHandler);
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
/* For this project, we’re going to add two always-present buttons
below the countdown in the timer.
One button will say Start when the timer is stopped, and Pause when it’s running.
Clicking it starts or stops the timer without resetting the time. */

const timeValue = 120;
let timer;
const Rue = function (selector, options) {
  this.elem = document.querySelector(selector);
  this.data = options.data;
  this.template = options.template;
};
Rue.prototype.render = function () {
  this.elem.innerHTML = this.template(this.data);
};
const formatTime = function (time) {
  let minutes = Math.floor(time / 60);
  let seconds = time % 60;
  return `${(minutes.toString())}:${seconds.toString().padStart(2,'0')}`;
}
const startTimer = function (e) {
  if (!e.target.hasAttribute('data-start-timer')) return;
  if (app.data.time < 1) {
    app.data.time = timeValue;
  }
  app.data.paused = false;
  app.render();
  stopTimer();
  timer = setInterval(countdown, 1000);
};
const countdown = function () {
  app.data.time--
  if (app.data.time < 1) {
    stopTimer();
    app.data.paused = true;
  }
  app.render();
}
const stopTimer = function () {
  clearInterval(timer)
}
const pauseTimer = function (e) {
  if (!e.target.hasAttribute('data-pause-timer')) return;
  stopTimer();
  app.data.paused = true;
  app.render();
}
const restartTimer = function (e) {
  if (!e.target.hasAttribute('data-restart-timer') || app.data.time === timeValue) return;
  stopTimer();
  app.data.time = timeValue;
  app.data.paused = false;
  app.render();
  timer = setInterval(countdown, 1000);
}
const clickHandler = function (e) {
  startTimer(e);
  restartTimer(e);
  pauseTimer(e);
}
const app = new Rue('#app', {
  data: {
    time: timeValue,
    paused: true,
    altMsg: true
  },
  template: function (props) {
    if (!props) return;
    if (props.time === 0 && props.altMsg) {
      let html = `<h2>It's over, start again:</h2><button data-restart-timer class="button stop">Restart</button></div>`
      return html;
    }
    let html = `<h2>You've got only <span class="counter">${formatTime(props.time)}</span> seconds!</h2>` +
      (props.paused ? `<div class="buttons-container"><button data-start-timer class="button start">Start</button>` : `<div class="buttons-container"><button data-pause-timer class="button start">Pause</button>`) + `<button data-restart-timer class="button stop">Restart</button></div>`
    return html;
  }
})
app.render();
document.addEventListener('click', clickHandler);
```

</div>
