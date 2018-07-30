# Document Ready

## Problem Statement

When we first learned about events, it made sense to talk about events in terms
of things users do: clicking or mousing or typing.

But JavaScript events can also be less obvious.

* "When we fetched some data"
* "When the window appeared"
* "When the DOM's data finished updating the screen"

We're going to learn more about that last one. That event is called
`DOMContentLoaded`. It's a good way to set up learning more about the AJAX
technique (update the DOM based on fetched data) that we'll cover later.

## Objectives

1. Explain why `DOMContentLoaded` is important
2. Set up an event on `DOMContentLoaded`

## Explain Why `DOMContentLoaded` Is Important

We don't ever want to write our JavaScript inside our HTML files.  For the
same reasons that we want to separate out our CSS from our HTML, we want to
separate out our JavaScript from our HTML, too.

But let's suppose we write a file that needs to bind to the `<body>` element.
If our friend decides to use that file and includes it in the `<head>` tag, the
DOM will not have loaded, our code won't find a `<body>` to bind to, and our
friend will complain that our code doesn't work.

![Letting Down Obi-Wan](https://media.giphy.com/media/3ornjJSq2s9xznhO80/giphy.gif)

How can we make sure our code only runs _after_ the DOM has fully "resolved?"
Why, we listen for the `DOMContentLoaded` event!

## Set Up An Event On `DOMContentLoaded`

### Part I:

If you take a look at `index-demo.html`, you'll notice we have event-handling code
JavaScript code written at the bottom.

Fire up a web server with the `httpserver` command. Open the `index-demo.html`
(something like: `http://<address>/index-demo.html`), page in the browser and
open the DevTools console. Clicking anywhere in the body should trigger a
message to the console.

View the page and confirm the JavaScript code works.

### Part II:

Next, move this code into a new file called `script.js`. Include `script.js` in
the `<head>` of `index-demo.html`. Reload the page. Your click event won't
work. You might notice JavaScript giving an error in the DevTools console:

```text
Uncaught TypeError: Cannot read property 'addEventListener' of null
```

Here the browser is telling us it tried to add a listener to an event that
didn't exist, `<body>`.

Edit the code in `script.js` to "wrap" the code inside of an event handler for
`DOMContentLoaded`. As you can see, the wrapping code is the
same handler style you've used for all the other DOM elements. This time,
though, you're binding to the DOM itself.

```js
document.addEventListener("DOMContentLoaded", e => {
  document.querySelector("body")
   .addEventListener("click", e => console.log("Reggae, Reggae!"));
})
```

Once the `DOMContentLoaded` event fires, the event happens. Any events we set
up there will now have the required nodes to "listen on." Refresh the page and 
verify that the `click` event works.

## Moving On

In order to move on run, and satisfy the tests using `learn`. Once you're passing the
test, enter `learn submit` and move on.

## Conclusion

In this lesson you learned to bind events to DOM events that aren't user
controlled. This will allow you to operate on the DOM with the guarantee that
the DOM nodes you need are there.
