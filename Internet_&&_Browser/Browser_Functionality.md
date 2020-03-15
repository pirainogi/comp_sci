- present the web resource you choose, by requesting it from the server and displaying it in the browser window
  - resource usually: HTML document, PDF, image, other content
- location of the resource is specified by the user using a URI (Uniform Resource Identifier)
- how the browser interprets and displays HTML files is specified in the HTML and CSS specifications
  - maintained by W3C (World Wide Web Consortium)
  - standards organization for the web
- common browser user interface elements:
  - address bar for inserting a URI
  - back and fwd buttons
  - bookmarking operation
  - refresh and stop btns
  - home btn
- HTML5 specification doesn't define UI elements a browser must have, but lists common elements

# Structure
- browsers like Chrome run multiple instances of the rendering engine: one for each tab
  - each tab is a separate process
1. user interface
  - address bar
  - back/fwd btns
  - bookmarking menu
  - every part of the browser display except the window where the user sees the requested page 
2. browser engine
  - marshals actions between the UI and the rendering engine
3. rendering engine
  - responsible for displaying the requested content
  - parses HTML and CSS and displays the content on the screen
4. Networking
  - for network calls (HTTP requests) using different implementations for different platform behind a platform-independent interface
5. UI backend
  - drawing basic widgets (combo boxes and windows)
  - exposes a generic interface that is not platform specific
  - uses operating system user interface methods
6. JS Interpreter
  - parse and execute JS
7. Data Storage
  - persistence layer
  - may need to save data locally (cookies)
  - support storage mechanisms such as localStorage, IndexedDB, WebSQL, and FileSystem
