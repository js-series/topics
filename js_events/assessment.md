# Interactive JS
## Assessment

### Show Hint - Lv. 1

Create a Codepen for the following assessment.

* Create some CSS for the `showHint`.

  ```CSS
    .hint {
      border: solid 1px black;
      width: 200px;
      padding: 10px;
    }
  ```
* Add a `<div>` with the following content.

  ```html
  <div class="hint" id="showHint">
    Find your Zen with coding!
  </div>
  ```
* Add a `<button>`.

  ```html
  <button id="showHintBtn">
    Show
  </button>
  ```

When the `showHintBtn` button is clicked display the `showHint` element.

> Hint: Add a CSS rule called `.hidden` with `display: none`.

### Toggle Hint - Lv. 2

Create a new Codepen for the following assessment.

* Create some CSS for the `toggleHint`.

  ```CSS
  .hint {
    border: solid 1px black;
    width: 200px;
    padding: 10px;
  }
  ```
* Add a `<div>` with the following content.

  ```html
  <div class="hint" id="toggleHint">
    Find your Zen with coding!
  </div>
  ```
* Add a `<button>`.

  ```html
  <button id="toggleHintBtn">
    Show
  </button>
  ```

When the `toggleHintBtn` button is clicked then display the `toggleHint` element and change the "toggleHintBtn" to "Hide". When the `toggleHint` is displaying and the `toggleHintBtn` is clicked then hide the `toggleHint`.


### Progressive Hints - Lv. 3

Create a new Codepen for the following assessment.

Using the following HTML and CSS create a series of hints where after each you reveal the button for to show the next hint.

* Use the following HTML.

  ```html
  <div class="hints">
    <div class="hint-content hidden" id="hint-1">
      See Hint 2!
    </div>

    <button class="hint-btn" id="hint-btn-1">
      Show Hint 1
    </button>

    <div class="hint-content hidden" id="hint-2">
      See Hint 2
    </div>

    <button class="hint-btn hidden" id="hint-btn-2">
      Show Hint 2
    </button>

    <div class="hint-content hidden" id="hint-3">
      No more hints!
    </div>

    <button class="hint-btn hidden" id="hint-btn-3">
      Show Hint 3
    </button>
  </div>
  ```
* Use the following CSS

  ```css
  body, html {
    height: 100%;
  }

  .hints {
    background-color: #446CB3;
    width: 500px;
    height: 100%;
    margin: 10px auto;
  }

  .hint-content {
    color: white;
    background-color: #DB0A5B;
    border: solid 1px black;
    padding: 10px;
    margin: 10px auto;
    width: 200px;
  }

  .hint-btn {
    display: block;
    width: 100px;
    height: 30px;
    margin: 0 auto;
  }

  .hidden {
    display: none;
  }
  ```
