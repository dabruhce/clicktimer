# clicktimer


### output
```
Time since last key press: 1143 milliseconds
Time since last key press: 249 milliseconds
Time since last key press: 7 milliseconds
Time since last key press: 24 milliseconds
Time since last key press: 705 milliseconds
Time since last key press: 191 milliseconds
Time since last key press: 25 milliseconds
Time since last key press: 32 milliseconds

```

### install
```
npm i
node keypress.js
```

### keypress.js
```node
const keypress = require('keypress');

// Make `process.stdin` begin emitting "keypress" events
keypress(process.stdin);

let lastKeyPressTime = null;
let previousKeyPressTime = null;
let lastKeyPressed = null;

process.stdin.on('keypress', (ch, key) => {
  const currentTime = Date.now();

  if (key) {
    // Display the key pressed
    // console.log(`Key pressed: ${key.name}`);

    if (lastKeyPressTime !== null) {
      // Update the previous keypress time
      previousKeyPressTime = lastKeyPressTime;
      // Display the previous key pressed
      // console.log(`Previous key pressed: ${lastKeyPressed}`);
    }

    // Update the last keypress time and the last key pressed
    lastKeyPressTime = currentTime;
    lastKeyPressed = key.name;

    if (previousKeyPressTime !== null) {
      const interval = lastKeyPressTime - previousKeyPressTime;
      console.log(`Time since last key press: ${interval} milliseconds`);
    }
  }

  if (key && key.ctrl && key.name === 'c') {
    process.stdin.pause(); // Exit on Ctrl+C
  }
});

// Allow the "keypress" events to be captured
process.stdin.setRawMode(true);
process.stdin.resume();
```

