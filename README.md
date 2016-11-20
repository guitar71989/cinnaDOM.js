## CinnaDOM

This tasty twist provides an original take on a classic DOM
manipulation flavor. Features include node manipulation, event handling,
document ready asynchronicity, and AJAX requests.

The cinnaDOM library's functionality is illustrated in my rendition
of the [classic game of Tetris][live].

[live]: https://guitar71989.github.io/Tetris.js/

Below please review some instructions on the implementation of the
cinnaDOM library as well as a brief explanation of its functionality with
some examples from my Tetris.js.

### How to Use

Download `./cinnaDOM/lib/` and add it to your project directory. Wherever cinnaDOM is used, include the following line at the top of the file:

```javascript

  const $cinnaDOM = require('./../cinnaDOM/lib/main');

```

### Methods

#### $cinnaDOM
#####   - Creates HTML elements
#####   - Retrieves DOM nodes from the page
#####   - Queues functions to be executed once the document is ready

```javascript

// $cinnaDOM('<tag>') will create an HTML element with the tag a return a DOMNodeCollection object, employing Javascript's native document.createElement() function.

  $cinnaDOM('<tag>')

// $cinnaDOM('tag') and $cinnaDOM('.class') will find all of the matching nodes already on the DOM and create a new DOMNodeCollection object, employing Javascript's native querySelectorAll() function.

  const $pause = $cinnaDOM(".pause-btn");

// If argument is a function, will push function into a queue to be executed on `document` `ready`

$cinnaDOM( () => {

  const $overlay = $cinnaDOM('div#overlay');
  const $modal = $cinnaDOM('div#modal');

  $cinnaDOM('#play').on('click', function () {
    $overlay.hide();
    $modal.hide();
    newGame.startGame();
  });

  const newGame = new View(rootEl);
});

```

### Methods for DOM manipulation

##### html()
  * Takes an optional string arguments
  * If there is an argument, then the method makes that string the `innerHTML` of each node.
  * If there is no argument, then the method returns the innerHTML of the first node.

  ```javascript

  $cinnaDOM(".lines-result").html(`${this.numLines}`);

  ```

  empty()
  ⋅⋅* Clears all the nodes of a collection array

  append()
  ⋅⋅* Adds the `outerHTML` of each element in argument to `innerHTML` of each element in the node collection

  attr()
  ⋅⋅* Takes one or two arguments
  ⋅⋅* If `attr()` receives one argument, the method gets the value of that attribute for the first node in the collection
  ⋅⋅* If `attr()` receives two arguments, the method sets the attribute (the first argument) to the value (second argument) for every node in the collection.

  addClass(args)
  ⋅⋅* Takes a class as an argument and adds the class to each element in the DOMNodeCollection



  removeClass(args)
  ⋅⋅* Takes a class as an argument and removes the class to each element in the DOMNodeCollection

  ```javascript

  occupyCell() {
    $cinnaDOM(`div.tetris-grid ul[data=\"${this.y}\"] li[data=\"${this.x}\"]`)
      .addClass(`${this.color}`);
    $cinnaDOM(`div.tetris-grid ul[data=\"${this.y}\"] li[data=\"${this.x}\"]`)
      .attr('empty', 'false');
  }

  unoccupyCell() {
    $cinnaDOM(`div.tetris-grid ul[data=\"${this.y}\"] li[data=\"${this.x}\"]`)
      .removeClass(`${this.color}`);
    $cinnaDOM(`div.tetris-grid ul[data=\"${this.y}\"] li[data=\"${this.x}\"]`)
      .attr('empty', 'true');
  }

  ```

Event Handling:

  on()
  ⋅⋅* Takes an event type as a string and a callback functino, and adds it on each node in the DOMNodeCollection, employing  Javascript's native `addEventListener` function.

  ```javascript

    $cinnaDOM(window).on('keydown', this.addKeydownListeners);

  ```

  off()
  ⋅⋅* Takes an event type as a string and a callback function, and removes it from each node in the DOMNodeCollection, employing  Javascript's native `removeEventListener` function.

  ```javascript

    $cinnaDOM(window).off('keydown', this.addKeydownListeners);

  ```

### Additional core functionality of cinnaDOM:

#### Document ready asynchronicity:

As seen above with `$cinnaDOM`, the core $cinnaDOM function provides a method to delay the invocation
of functions until the DOM fully renders.

#### AJAX Requests:

AJAX method takes an options hash (set of key/value pairs) and uses
the XMLHttpRequest API to send and receive data from a server.
