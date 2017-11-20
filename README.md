# jk-observer

The classic observer design pattern.

## Introduction

The Observer design pattern is a well known pattern to create reactive applications.
For example, your can attach listeners to a form text field, then when the text field value changes, all listeners are notified of that change and thus can do something in response. 

**This library is tested.**

## Attaching a listener and notify it

The following code shows how to attach a listener and how to notify it of events.

```js
import {Observer} from "jk-observer";

class Person {
    constructor(name) {
        this.name = name;
        // Create the observer with current context
        this. observer = new Observer(this);
    }
    
    on(event, listener) {
        // Attach listener
        this.observer.attach(event, listener);
    }
    
    say(words) {
        console.log(words);
        // Notify listeners
        this.observer.notify("say", words, new Date());
    }
}

const karl = new Person("karl");

// When this person says something,
// we will display it in the console with the time
karl.on("say", function(words, date) {
        console.log(`${this.name} said: "${words}" at ${date.toString()}`);
});
```

## Detaching a listener

In the case that you need to remove a previously attached listener, here is the code.

```js
import {Observer} from "jk-observer";

const doubleClickListener = function() {
    console.log("you double clicked");
};

const observer = new Observer();
observer.attach("click", doubleClickListener);
observer.detach("click", doubleClickListener);
```

## Changelog

### v1.0.0
- First public release

## License

This project is released under the [MIT License](http://www.opensource.org/licenses/MIT).
