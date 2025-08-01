---
title: "EventTarget: addEventListener() method"
short-title: addEventListener()
slug: Web/API/EventTarget/addEventListener
page-type: web-api-instance-method
browser-compat: api.EventTarget.addEventListener
---

{{APIRef("DOM")}}{{AvailableInWorkers}}

The **`addEventListener()`** method of the {{domxref("EventTarget")}} interface
sets up a function that will be called whenever the specified event is delivered to the target.

Common targets are {{domxref("Element")}}, or its children, {{domxref("Document")}}, and {{domxref("Window")}},
but the target may be any object that supports events (such as {{domxref("IDBRequest")}}).

> [!NOTE]
> The `addEventListener()` method is the _recommended_ way to register an event listener. The benefits are as follows:
>
> - It allows adding more than one handler for an event. This is particularly
>   useful for libraries, JavaScript modules, or any other kind of
>   code that needs to work well with other libraries or extensions.
> - In contrast to using an `onXYZ` property, it gives you finer-grained control of the phase when the listener is activated (capturing vs. bubbling).
> - It works on any event target, not just HTML or SVG elements.

The method `addEventListener()` works by adding a function, or an object that implements a `handleEvent()` function, to the list of event listeners for the specified event type
on the {{domxref("EventTarget")}} on which it's called. If the function or object is already in the list of event listeners for this target, the function or object is not added a second time.

> [!NOTE]
> If a particular anonymous function is in the list of event listeners registered for a certain target, and then later in the code, an identical anonymous function is given in an `addEventListener` call, the second function will _also_ be added to the list of event listeners for that target.
>
> Indeed, anonymous functions are not identical even if defined using
> the _same_ unchanging source-code called repeatedly, **even if in a loop**.
>
> Repeatedly defining the same unnamed function in such cases can be
> problematic. (See [Memory issues](#memory_issues), below.)

If an event listener is added to an {{domxref("EventTarget")}} from inside another listener —
that is, during the processing of the event —
that event will not trigger the new listener.
However, the new listener may be triggered during a later stage of event flow,
such as during the bubbling phase.

## Syntax

```js-nolint
addEventListener(type, listener)
addEventListener(type, listener, options)
addEventListener(type, listener, useCapture)
```

### Parameters

- `type`
  - : A case-sensitive string representing the [event type](/en-US/docs/Web/API/Document_Object_Model/Events) to listen for.
- `listener`
  - : The object that receives a notification (an object that implements the
    {{domxref("Event")}} interface) when an event of the specified type occurs. This must
    be `null`, an object with a `handleEvent()` method, or a JavaScript
    [function](/en-US/docs/Web/JavaScript/Guide/Functions). See
    [The event listener callback](#the_event_listener_callback) for details on the callback itself.
- `options` {{optional_inline}}
  - : An object that specifies characteristics about the event listener. The available
    options are:
    - `capture` {{optional_inline}}
      - : A boolean value indicating that events of this type will be dispatched
        to the registered `listener` before being dispatched to any
        `EventTarget` beneath it in the DOM tree. If not specified, defaults to `false`.
    - `once` {{optional_inline}}
      - : A boolean value indicating that the `listener`
        should be invoked at most once after being added. If `true`, the
        `listener` would be automatically removed when invoked. If not specified, defaults to `false`.
    - `passive` {{optional_inline}}
      - : A boolean value that, if `true`, indicates that the function specified by `listener` will never call {{domxref("Event.preventDefault", "preventDefault()")}}. If a passive listener calls `preventDefault()`, nothing will happen and a console warning may be generated.

        If this option is not specified it defaults to `false` – except that in browsers other than Safari, it defaults to `true` for {{domxref("Element/wheel_event", "wheel")}}, {{domxref("Element/mousewheel_event", "mousewheel")}}, {{domxref("Element/touchstart_event", "touchstart")}} and {{domxref("Element/touchmove_event", "touchmove")}} events. See [Using passive listeners](#using_passive_listeners) to learn more.

    - `signal` {{optional_inline}}
      - : An {{domxref("AbortSignal")}}. The listener will be removed when the {{domxref("AbortController/abort()", "abort()")}} method of the {{domxref("AbortController")}} which owns the `AbortSignal` is called. If not specified, no `AbortSignal` is associated with the listener.

- `useCapture` {{optional_inline}}
  - : A boolean value indicating whether events of this type will be dispatched to
    the registered `listener` _before_ being dispatched to
    any `EventTarget` beneath it in the DOM tree. Events that are bubbling
    upward through the tree will not trigger a listener designated to use capture. Event
    bubbling and capturing are two ways of propagating events that occur in an element
    that is nested within another element, when both elements have registered a handle for
    that event. The event propagation mode determines the order in which elements receive
    the event. See [the DOM spec](https://dom.spec.whatwg.org/#introduction-to-dom-events) and [JavaScript Event order](https://www.quirksmode.org/js/events_order.html#link4) for a detailed explanation.
    If not specified, `useCapture` defaults to `false`.

    > [!NOTE]
    > For event listeners attached to the event target, the event is in the target phase, rather than the capturing and bubbling phases.
    > Event listeners in the _capturing_ phase are called before event listeners in the target and bubbling phases.

- `wantsUntrusted` {{optional_inline}} {{non-standard_inline}}
  - : A Firefox (Gecko)-specific parameter. If `true`, the listener receives
    synthetic events dispatched by web content (the default is `false` for
    browser {{glossary("chrome")}} and `true` for regular web pages). This
    parameter is useful for code found in add-ons, as well as the browser itself.

### Return value

None ({{jsxref("undefined")}}).

## Usage notes

### The event listener callback

The event listener can be specified as either a callback function or
an object whose `handleEvent()` method serves as the callback function.

The callback function itself has the same parameters and return value as the
`handleEvent()` method; that is, the callback accepts a single parameter: an
object based on {{domxref("Event")}} describing the event that has occurred, and it
returns nothing.

For example, an event handler callback that can be used to handle both
{{domxref("Element/fullscreenchange_event", "fullscreenchange")}} and
{{domxref("Element/fullscreenerror_event", "fullscreenerror")}} might look like this:

```js
function handleEvent(event) {
  if (event.type === "fullscreenchange") {
    /* handle a full screen toggle */
  } else {
    /* handle a full screen toggle error */
  }
}
```

### The value of "this" within the handler

It is often desirable to reference the element on which the event handler was fired,
such as when using a generic handler for a set of similar elements.

When attaching a handler function to an element using `addEventListener()`,
the value of {{jsxref("Operators/this","this")}} inside the handler will be a reference to
the element. It will be the same as the value of the `currentTarget` property of
the event argument that is passed to the handler.

```js
my_element.addEventListener("click", function (e) {
  console.log(this.className); // logs the className of my_element
  console.log(e.currentTarget === this); // logs `true`
});
```

As a reminder, [arrow functions do not have their own `this` context](/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#cannot_be_used_as_methods).

```js
my_element.addEventListener("click", (e) => {
  console.log(this.className); // WARNING: `this` is not `my_element`
  console.log(e.currentTarget === this); // logs `false`
});
```

If an event handler (for example, {{domxref("Element.click_event", "onclick")}}) is specified on an element in the HTML source, the JavaScript code in the attribute value is effectively wrapped in a handler function that binds the value of `this` in a manner consistent with the `addEventListener()`; an occurrence of `this` within the code represents a reference to the element.

```html
<table id="my_table" onclick="console.log(this.id);">
  <!-- `this` refers to the table; logs 'my_table' -->
  …
</table>
```

Note that the value of `this` inside a function, _called by_ the code
in the attribute value, behaves as per [standard rules](/en-US/docs/Web/JavaScript/Reference/Operators/this). This is
shown in the following example:

```html
<script>
  function logID() {
    console.log(this.id);
  }
</script>
<table id="my_table" onclick="logID();">
  <!-- when called, `this` will refer to the global object -->
  …
</table>
```

The value of `this` within `logID()` is a reference to the global
object {{domxref("Window")}} (or `undefined` in the case of [strict mode](/en-US/docs/Web/JavaScript/Reference/Strict_mode).

#### Specifying "this" using bind()

The {{jsxref("Function.prototype.bind()")}} method lets you establish a fixed
`this` context for all subsequent calls — bypassing problems where it's unclear what `this` will be, depending on
the context from which your function was called. Note, however, that you'll need to keep
a reference to the listener around so you can remove it later.

This is an example with and without `bind()`:

```js
class Something {
  name = "Something Good";
  constructor(element) {
    // bind causes a fixed `this` context to be assigned to `onclick2`
    this.onclick2 = this.onclick2.bind(this);
    element.addEventListener("click", this.onclick1, false);
    element.addEventListener("click", this.onclick2, false); // Trick
  }
  onclick1(event) {
    console.log(this.name); // undefined, as `this` is the element
  }
  onclick2(event) {
    console.log(this.name); // 'Something Good', as `this` is bound to the Something instance
  }
}

const s = new Something(document.body);
```

Another solution is using a special function called `handleEvent()` to catch
any events:

```js
class Something {
  name = "Something Good";
  constructor(element) {
    // Note that the listeners in this case are `this`, not this.handleEvent
    element.addEventListener("click", this, false);
    element.addEventListener("dblclick", this, false);
  }
  handleEvent(event) {
    console.log(this.name); // 'Something Good', as this is bound to newly created object
    switch (event.type) {
      case "click":
        // some code here…
        break;
      case "dblclick":
        // some code here…
        break;
    }
  }
}

const s = new Something(document.body);
```

Another way of handling the reference to `this` is to use an arrow function, which doesn't create a separate `this` context.

```js
class SomeClass {
  name = "Something Good";

  register() {
    window.addEventListener("keydown", (e) => {
      this.someMethod(e);
    });
  }

  someMethod(e) {
    console.log(this.name);
    switch (e.code) {
      case "ArrowUp":
        // some code here…
        break;
      case "ArrowDown":
        // some code here…
        break;
    }
  }
}

const myObject = new SomeClass();
myObject.register();
```

### Getting data into and out of an event listener

Event listeners only take one argument,
an {{domxref("Event")}} or a subclass of `Event`,
which is automatically passed to the listener, and the return value is ignored.
Therefore, to get data into and out of an event listener, instead of passing the data through parameters and return values, you need to create [closures](/en-US/docs/Web/JavaScript/Guide/Closures) instead.

The functions passed as event listeners have access to all variables declared in the outer scopes that contain the function.

```js
const myButton = document.getElementById("my-button-id");
let someString = "Data";

myButton.addEventListener("click", () => {
  console.log(someString);
  // 'Data' on first click,
  // 'Data Again' on second click

  someString = "Data Again";
});

console.log(someString); // Expected Value: 'Data' (will never output 'Data Again')
```

Read [the function guide](/en-US/docs/Web/JavaScript/Guide/Functions#function_scopes_and_closures) for more information about function scopes.

### Memory issues

```js
const elems = document.getElementsByTagName("*");

// Case 1
for (const elem of elems) {
  elem.addEventListener(
    "click",
    (e) => {
      // Do something
    },
    false,
  );
}

// Case 2
function processEvent(e) {
  // Do something
}

for (const elem of elems) {
  elem.addEventListener("click", processEvent, false);
}
```

In the first case above, a new (anonymous) handler function is created with each
iteration of the loop. In the second case, the same previously declared function is used
as an event handler, which results in smaller memory consumption because there is only
one handler function created. Moreover, in the first case, it is not possible to call
{{domxref("EventTarget.removeEventListener", "removeEventListener()")}} because no
reference to the anonymous function is kept (or here, not kept to any of the multiple
anonymous functions the loop might create.) In the second case, it's possible to do
`myElement.removeEventListener("click", processEvent, false)`
because `processEvent` is the function reference.

Actually, regarding memory consumption, the lack of keeping a function reference is not
the real issue; rather it is the lack of keeping a _static_ function reference.

### Using passive listeners

If an event has a default action — for example, a {{domxref("Element/wheel_event", "wheel")}} event that scrolls the container by default — the browser is in general unable to start the default action until the event listener has finished, because it doesn't know in advance whether the event listener might cancel the default action by calling {{domxref("Event.preventDefault()")}}. If the event listener takes too long to execute, this can cause a noticeable delay, also known as {{glossary("jank")}}, before the default action can be executed.

By setting the `passive` option to `true`, an event listener declares that it will not cancel the default action, so the browser can start the default action immediately, without waiting for the listener to finish. If the listener does then call {{domxref("Event.preventDefault()")}}, this will have no effect.

The specification for `addEventListener()` defines the default value for the `passive` option as always being `false`. However, to realize the scroll performance benefits of passive listeners in legacy code, modern browsers have changed the default value of the `passive` option to `true` for the {{domxref("Element/wheel_event", "wheel")}}, {{domxref("Element/mousewheel_event", "mousewheel")}}, {{domxref("Element/touchstart_event", "touchstart")}} and {{domxref("Element/touchmove_event", "touchmove")}} events on the document-level nodes {{domxref("Window")}}, {{domxref("Document")}}, and {{domxref("Document.body")}}. That prevents the event listener from [canceling the event](/en-US/docs/Web/API/Event/preventDefault), so it can't block page rendering while the user is scrolling.

Because of that, when you want to override that behavior and ensure the `passive` option is `false`, you must explicitly set the option to `false` (rather than relying on the default).

You don't need to worry about the value of `passive` for the basic {{domxref("Element/scroll_event", "scroll")}} event.
Since it can't be canceled, event listeners can't block page rendering anyway.

See [Improving scroll performance using passive listeners](#improving_scroll_performance_using_passive_listeners) for an example showing the effect of passive listeners.

## Examples

### Add a simple listener

This example demonstrates how to use `addEventListener()` to watch for mouse
clicks on an element.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Function to change the content of t2
function modifyText() {
  const t2 = document.getElementById("t2");
  const isNodeThree = t2.firstChild.nodeValue === "three";
  t2.firstChild.nodeValue = isNodeThree ? "two" : "three";
}

// Add event listener to table
const el = document.getElementById("outside");
el.addEventListener("click", modifyText, false);
```

In this code, `modifyText()` is a listener for `click` events
registered using `addEventListener()`. A click anywhere in the table bubbles
up to the handler and runs `modifyText()`.

#### Result

{{EmbedLiveSample('Add_a_simple_listener')}}

### Add an abortable listener

This example demonstrates how to add an `addEventListener()` that can be aborted with an {{domxref("AbortSignal")}}.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Add an abortable event listener to table
const controller = new AbortController();
const el = document.getElementById("outside");
el.addEventListener("click", modifyText, { signal: controller.signal });

// Function to change the content of t2
function modifyText() {
  const t2 = document.getElementById("t2");
  if (t2.firstChild.nodeValue === "three") {
    t2.firstChild.nodeValue = "two";
  } else {
    t2.firstChild.nodeValue = "three";
    controller.abort(); // remove listener after value reaches "three"
  }
}
```

In the example above, we modify the code in the previous example such that after the second row's content changes to "three", we call `abort()` from the {{domxref("AbortController")}} we passed to the `addEventListener()` call. That results in the value remaining as "three" forever because we no longer have any code listening for a click event.

#### Result

{{EmbedLiveSample('Add_an_abortable_listener')}}

### Event listener with anonymous function

Here, we'll take a look at how to use an anonymous function to pass parameters into the
event listener.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Function to change the content of t2
function modifyText(newText) {
  const t2 = document.getElementById("t2");
  t2.firstChild.nodeValue = newText;
}

// Function to add event listener to table
const el = document.getElementById("outside");
el.addEventListener(
  "click",
  function () {
    modifyText("four");
  },
  false,
);
```

Notice that the listener is an anonymous function that encapsulates code that is then,
in turn, able to send parameters to the `modifyText()` function, which is
responsible for actually responding to the event.

#### Result

{{EmbedLiveSample('Event_listener_with_anonymous_function')}}

### Event listener with an arrow function

This example demonstrates an event listener implemented using arrow function
notation.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Function to change the content of t2
function modifyText(newText) {
  const t2 = document.getElementById("t2");
  t2.firstChild.nodeValue = newText;
}

// Add event listener to table with an arrow function
const el = document.getElementById("outside");
el.addEventListener(
  "click",
  () => {
    modifyText("four");
  },
  false,
);
```

#### Result

{{EmbedLiveSample('Event_listener_with_an_arrow_function')}}

Please note that while anonymous and arrow functions are similar, they have different
`this` bindings. While anonymous (and all traditional JavaScript functions)
create their own `this` bindings, arrow functions inherit the
`this` binding of the containing function.

That means that the variables and constants available to the containing function are
also available to the event handler when using an arrow function.

### Example of options usage

#### HTML

```html
<div class="outer">
  outer, once & none-once
  <div class="middle" target="_blank">
    middle, capture & none-capture
    <a class="inner1" href="https://www.mozilla.org" target="_blank">
      inner1, passive & preventDefault(which is not allowed)
    </a>
    <a class="inner2" href="https://developer.mozilla.org/" target="_blank">
      inner2, none-passive & preventDefault(not open new page)
    </a>
  </div>
</div>
<hr />
<button class="clear-button">Clear logs</button>
<section class="demo-logs"></section>
```

#### CSS

```css
.outer,
.middle,
.inner1,
.inner2 {
  display: block;
  width: 520px;
  padding: 15px;
  margin: 15px;
  text-decoration: none;
}
.outer {
  border: 1px solid red;
  color: red;
}
.middle {
  border: 1px solid green;
  color: green;
  width: 460px;
}
.inner1,
.inner2 {
  border: 1px solid purple;
  color: purple;
  width: 400px;
}
```

```css hidden
.demo-logs {
  width: 530px;
  height: 16rem;
  background-color: #ddd;
  overflow-x: auto;
  padding: 1rem;
}
```

#### JavaScript

```js hidden
const clearBtn = document.querySelector(".clear-button");
const demoLogs = document.querySelector(".demo-logs");

function log(msg) {
  demoLogs.innerText += `${msg}\n`;
}

clearBtn.addEventListener("click", () => {
  demoLogs.innerText = "";
});
```

```js
const outer = document.querySelector(".outer");
const middle = document.querySelector(".middle");
const inner1 = document.querySelector(".inner1");
const inner2 = document.querySelector(".inner2");

const capture = {
  capture: true,
};
const noneCapture = {
  capture: false,
};
const once = {
  once: true,
};
const noneOnce = {
  once: false,
};
const passive = {
  passive: true,
};
const nonePassive = {
  passive: false,
};

outer.addEventListener("click", onceHandler, once);
outer.addEventListener("click", noneOnceHandler, noneOnce);
middle.addEventListener("click", captureHandler, capture);
middle.addEventListener("click", noneCaptureHandler, noneCapture);
inner1.addEventListener("click", passiveHandler, passive);
inner2.addEventListener("click", nonePassiveHandler, nonePassive);

function onceHandler(event) {
  log("outer, once");
}
function noneOnceHandler(event) {
  log("outer, none-once, default\n");
}
function captureHandler(event) {
  // event.stopImmediatePropagation();
  log("middle, capture");
}
function noneCaptureHandler(event) {
  log("middle, none-capture, default");
}
function passiveHandler(event) {
  // Unable to preventDefault inside passive event listener invocation.
  event.preventDefault();
  log("inner1, passive, open new page");
}
function nonePassiveHandler(event) {
  event.preventDefault();
  // event.stopPropagation();
  log("inner2, none-passive, default, not open new page");
}
```

#### Result

Click the outer, middle, inner containers respectively to see how the options work.

{{ EmbedLiveSample('Example_of_options_usage', 600, 630) }}

### Event listener with multiple options

You can set more than one of the options in the `options` parameter. In the following example we are setting two options:

- `passive`, to assert that the handler will not call {{domxref("Event.preventDefault", "preventDefault()")}}
- `once`, to ensure that the event handler will only be called once.

#### HTML

```html
<button id="example-button">You have not clicked this button.</button>
<button id="reset-button">Click this button to reset the first button.</button>
```

#### JavaScript

```js
const buttonToBeClicked = document.getElementById("example-button");

const resetButton = document.getElementById("reset-button");

// the text that the button is initialized with
const initialText = buttonToBeClicked.textContent;

// the text that the button contains after being clicked
const clickedText = "You have clicked this button.";

// we hoist the event listener callback function
// to prevent having duplicate listeners attached
function eventListener() {
  buttonToBeClicked.textContent = clickedText;
}

function addListener() {
  buttonToBeClicked.addEventListener("click", eventListener, {
    passive: true,
    once: true,
  });
}

// when the reset button is clicked, the example button is reset,
// and allowed to have its state updated again
resetButton.addEventListener("click", () => {
  buttonToBeClicked.textContent = initialText;
  addListener();
});

addListener();
```

#### Result

{{EmbedLiveSample('Event_listener_with_multiple_options')}}

### Improving scroll performance using passive listeners

The following example shows the effect of setting `passive`. It includes a {{htmlelement("div")}} that contains some text, and a check box.

#### HTML

```html
<div id="container">
  <p>
    But down there it would be dark now, and not the lovely lighted aquarium she
    imagined it to be during the daylight hours, eddying with schools of tiny,
    delicate animals floating and dancing slowly to their own serene currents
    and creating the look of a living painting. That was wrong, in any case. The
    ocean was different from an aquarium, which was an artificial environment.
    The ocean was a world. And a world is not art. Dorothy thought about the
    living things that moved in that world: large, ruthless and hungry. Like us
    up here.
  </p>
</div>

<div>
  <input type="checkbox" id="passive" name="passive" checked />
  <label for="passive">passive</label>
</div>
```

```css hidden
#container {
  width: 150px;
  height: 200px;
  overflow: scroll;
  margin: 2rem 0;
  padding: 0.4rem;
  border: 1px solid black;
}
```

#### JavaScript

The code adds a listener to the container's {{domxref("Element/wheel_event", "wheel")}} event, which by default scrolls the container. The listener runs a long-running operation. Initially the listener is added with the `passive` option, and whenever the checkbox is toggled, the code toggles the `passive` option.

```js
const passive = document.querySelector("#passive");
passive.addEventListener("change", (event) => {
  container.removeEventListener("wheel", wheelHandler);
  container.addEventListener("wheel", wheelHandler, {
    passive: passive.checked,
    once: true,
  });
});

const container = document.querySelector("#container");
container.addEventListener("wheel", wheelHandler, {
  passive: true,
  once: true,
});

function wheelHandler() {
  function isPrime(n) {
    for (let c = 2; c <= Math.sqrt(n); ++c) {
      if (n % c === 0) {
        return false;
      }
    }
    return true;
  }

  const quota = 1000000;
  const primes = [];
  const maximum = 1000000;

  while (primes.length < quota) {
    const candidate = Math.floor(Math.random() * (maximum + 1));
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }

  console.log(primes);
}
```

#### Result

The effect is that:

- Initially, the listener is passive, so trying to scroll the container with the wheel is immediate.
- If you uncheck "passive" and try to scroll the container using the wheel, then there is a noticeable delay before the container scrolls, because the browser has to wait for the long-running listener to finish.

{{EmbedLiveSample("Improving scroll performance using passive listeners", 100, 300)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("EventTarget.removeEventListener()")}}
- [Creating and dispatching custom events](/en-US/docs/Web/API/Document_Object_Model/Events#creating_and_dispatching_events)
- [More details on the use of `this` in event handlers](https://www.quirksmode.org/js/this.html)
