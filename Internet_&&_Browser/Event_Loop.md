- Browser event handlers behave like other asynchronous notifications.
  - Scheduled when the event occurs
  - Must wait for other scripts that are running to finish before they get a chance to run
- Events can be processed only when nothing else
  - If the event loop is tied up with other work, any interaction with the page (which happens through events) will be delayed until there’s time to process it.

## EventsTable
- Sole purpose is to keep track of events and send them to the Event Queue
- Data structure which knows that a certain function should be triggered after a certain event
  - Once that event occurs, it sends a notice
- every time you call a setTimeout or do an async operation, it is added to the Events Table

## Event Queue
- Data structure that is similar to the Stack
- Receives functions from the events table
- Event loop sends these events to the call stack

## Event Loop
- Constantly running process that checks if the call stack is empty.
  - If there is something in the event queue that is waiting it is moved to the call stack, when the stack is empty.
  - If the stack is not empty, then nothing happens
- For pages where you want to do something really complex in the background, browsers provide web workers.
  - A worker is a JavaScript process that runs alongside the main script on its own timeline.
  - Workers do not share their global scope or any other data with the main script’s environment.
  - Have to communicate with them by sending messages back and forth
- Event loop is what allows JS to use callbacks and promises

### SUMMARY
- Event loop is continuously running in JS
- If the call stack is empty and there’s an event that’s been triggered, it’ll be added to the call stack
