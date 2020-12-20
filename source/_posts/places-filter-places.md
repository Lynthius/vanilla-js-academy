---
title: 35. Places - Filter Places
date: 2020-12-19 17:55:05
---

<div class="output-container">

  <style type="text/css">
  .article-entry ul, .article-entry ol, .article-entry dl {
      margin-top: 0;
    }

    .category {
      margin-top: 10px;
    }

    .title {
      margin-top: 0;
      margin-bottom: 0;
      font-weight: 600;
      font-size: 20px;
    }

    .post-container {
      display: flex;
      flex-direction: row;
      margin: 20px 0;
    }

    @media screen and (max-width: 860px) {
      .post-container {
        flex-direction: column;
        margin: 20px auto;
        text-align: center;
      }
    }

    .info-container {
      margin-left: 40px;
    }

     @media screen and (max-width: 860px) {
      .info-container {
        margin-left: 0;
      }
    }

    .header {
      display: flex;
      justify-content: space-between;
    }

    .miniature-container {
      max-width: 380px;
    }

    .minature {
      height: auto;
      max-width: 100%;
    }

    .add-btn {
      color: #ffffff;
      font-size: 26px;
      font-family: "system-ui";
      background-color: transparent;
      border: none;
      height: 40px;
      width: 40px;
      border-radius: 50%;
      cursor: pointer;
      outline: none;
    }

    .add-btn[aria-pressed="true"] {
      color: #8e45ff;
    }

    .add-btn:focus {
      border: red;
      outline: none;
      box-shadow: 0 0 3px 1px #8e45ff;
    }

    .add-btn:active {
      color: #8e45ff;
    }
  </style>

  <p>Explore cool, quirky places in your own backyard.</p>
  <div class="filters">
	<strong>Filter:</strong>
	<label>
		<input type="radio" name="view" value="all" checked>
		All Places
	</label>
	<label>
		<input type="radio" name="view" value="faves">
		Favorites
	</label>
	<label>
		<input type="radio" name="view" value="visited">
		Visited
	</label>
	<label>
		<input type="radio" name="view" value="not-visited">
		Not Visited
	</label>
</div>
  <div id="app">Loading...</div>

  <script src="https://cdn.jsdelivr.net/npm/reefjs@7/dist/reef.js"></script>
  <script>
    const favesID = "favoritePlace";
    const app = new Reef('#app', {
      data: {},
      template: function (props) {
        if (props.posts && props.posts.length) {
          let html = '<div class="container">' + props.posts.map(function (post) {
            return `<div class="post-container"><div class="miniature-container"><img class="minature" src="${post.img}" /></div><div class="info-container"><div class="header"><h2 class="title">${post.place}</h2>
            <div class="buttons">
              <button data-type="faves" data-id="${post.id}" class="add-btn" aria-label="add ${post.place} to favorite" aria-pressed="${props.faves[post.id]}" title="Add to favorite!">&#x2665;</button>
              <button data-type="visited" data-id="${post.id}" class="add-btn" aria-label="add ${post.place} to visited" aria-pressed="${props.visited[post.id]}" title="Add to visited!">&#9745;</button>
            </div></div><p>${post.description}</p><p><em>${post.location}</em></p><a href=${post.url} target="_blank">Read more</a></div></div>`;
          }).join('') + '</div>';
          return html;
        }
        let html = '<p>Unable to find any places right now.</p>'
        return html;
      }
    });
    const getFromLocal = function (prop) {
      const faves = localStorage.getItem(favesID);
      const faves = localStorage.getItem(favesID);
      const favesObj = faves ? JSON.parse(faves) : {};
      return favesObj;
    }
    const saveFaves = function (faves) {
      localStorage.setItem(favesID, JSON.stringify(faves));
    }
    const getPosts = function () {
      fetch('https://vanillajsacademy.com/api/places.json').then(function (response) {
        if (response.ok) {
          return response.json();
        }
        return Promise.reject(response);
      }).then(function (data) {
        app.data.faves = getFromLocal(favesID);
        app.data.visited = getFromLocal(visitedID);
        app.data.filter = 'all';
        app.data.posts = data;
      }).catch(function (error) {
        console.warn(error);
        app.data.posts = null;
      })
    }
    const clickHandler = function (e) {
      const postType = e.target.getAttribute('data-type');
      const postID = e.target.getAttribute('data-id');
      if (!postType || !postID) return;
      app.data.postType[postID] = app.data.postType[postID] ? false : true;
    }
    getPosts();
    document.addEventListener('click', clickHandler);
  </script>

</div>

<div class="html-container" style="border-top: .5px solid grey; margin-top: 30px;">

## HTML

```HTML
<p>Explore cool, quirky places in your own backyard.</p>
<div class="filters">
	<strong>Filter:</strong>
	<label>
		<input type="radio" name="view" value="all" checked>
		All Places
	</label>

	<label>
		<input type="radio" name="view" value="faves">
		Favorites
	</label>

	<label>
		<input type="radio" name="view" value="visited">
		Visited
	</label>

	<label>
		<input type="radio" name="view" value="not-visited">
		Not Visited
	</label>
</div>
<div id="app">Loading...</div>
```

</div>
<div class="js-container">

## JavaScript

```JS
/* Add a “Visited” button for users to mark off locations they’ve already been to.
Like the “Favorites” button, visited locations should be saved between visits.
When the user selects one of the filters,
change the UI to only show locations that match the filter criteria. */

```

</div>
