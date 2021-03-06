# Framelet - lighweight messaging library for iframes

```
  ______                        _      _   
 |  ____|                      | |    | |  
 | |__ _ __ __ _ _ __ ___   ___| | ___| |_ 
 |  __| '__/ _` | '_ ` _ \ / _ \ |/ _ \ __|
 | |  | | | (_| | | | | | |  __/ |  __/ |_ 
 |_|  |_|  \__,_|_| |_| |_|\___|_|\___|\__|
 ```

## API


There is only one function named `Framelet`, you can get the instance by:

```js
const framelet = Framelet('<CONTEXT>', targetContentWindow);
```

Add a message listener on channel for once
```js
framelet.once('<TOPIC>', (message) => { console.log(message); });
```

Add a message listener on topic
```js
framelet.on('<TOPIC>', (message) => { console.log(message); });
```

Send a message to the topic
```js
framelet.send('<TOPIC>', '<MESSAGE>');
```

If both topic and listener are undefined, remove all
```js
framelet.off(['<TOPIC>', () => {}]);
```

## EXAMPLE #1

### PARENT

```js
import Framelet from 'framelet';

var iframe = document.createElement('iframe');
iframe.id = 'framelet_iframe';
iframe.src = '//<URL>/child.html';

const framelet = Framelet('<CONTEXT>', iframe.contentWindow);

framelet.on('<TOPIC>.*', (message) => {
   console.log(message);
});

framelet.send('<TOPIC>.*', 'Hi, from parent!');
```

### CHILD

```js
import Framelet from 'framelet';

const framelet = Framelet('<CONTEXT>', window.parent);

framelet.on('<TOPIC>.*', (message) => {
   console.log(message);
});

framelet.send('<TOPIC>.*', 'Hi, from child!');
```

### POST MESSAGE

> The window.postMessage() method safely enables cross-origin communication between Window objects; e.g., between a page and a pop-up that it spawned, or between a page and an iframe embedded within it.


## REFERENCES
- [hustcc/post-messager](https://github.com/hustcc/post-messenger)
- [Mozilla/postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
