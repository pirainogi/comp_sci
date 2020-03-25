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

# Rendering Engine
- responsible for rendering
  - display of requested content in the browser screen
- can display HTML and XML documents and images
- display other types of data via plugins or extensions  

## Types
- Internet Explorer uses Trident
- Firefox uses Gecko
- Safari uses WebKit
- Chrome and Opera use Blink, a form of WebKit
- Webkit is an OSS rendering engine which started as an engine for the Linux platform and was modified by Apple to support Mac and Windows

## Flow
- start getting contents of the requested doc from the networking layer
  - 8kB chunks
- basic flow:
  - parsing HTML to construct DOM tree
  - render tree construction
  - layout of render tree
  - painting the render tree
- rendering engine will start parsing the HTML doc and convert the elements to DOM nodes in a tree called the _content tree_
- engine will parse the style data (external CSS files and internal style elements)
- render tree is created by combining DOM tree and CSSOM tree (also known as _frame tree_)
  - process is called attachment
- render tree contains rectangles with visual attributes like color and dimensions
  - rectangles are in the right order to be displayed on the screen
- layout process: giving each node the exact coordinates where it should appear on the screen (also known as _reflow_)
- painting: render tree is traversed and each node is painted using the UI backend layer
- rendering engine will try to display content on the screen as soon as possible
  - will not wait until all HTML is parsed before starting to build and layout the render tree
  - parts of the content will be parsed and displayed while the process continues with the rest of the contents that keep coming from the network

### Parsing
- translating a document into a structure that the code can use
- result is usually a tree of nodes that represent the structure of the document
  - _parse tree_ or _syntax tree_

#### Grammars
- parsing is based on the syntax rules that the document obeys
  - language/format it was written in
- every format must have deterministic grammar consisting of vocabulary and syntax rules (_content free grammar_)

#### Parser-Lexer Combination
- parsing can be separated into sub-processes:
  - lexical analysis
    - process of  breaking the input into tokens
    - tokens are the language vocabulary: collection of valid building blocks
  - syntax analysis
    - apply language syntax rules
- divide the work between two components:
  - lexer (or tokenizer)  
    - break the input into valid tokens
    - knows to strip irrelevant characters like white spaces and line breaks
  - parser
    - construct the parse tree by analyzing the document structure according to the language syntax rules
- process is iterative
  - parser will ask the lexer for a new token and try to match the token with one of the syntax rules
  - if matched, node with the corresponding token will be added to the parse tree
  - if no match, parser will store the token internally and keep asking for tokens until a rule matching all internally stored tokens is found
    - if no rule found, parser raises an exception
    - document not valid and contains syntax errors  
- parse tree is not the final product in most cases
  - translation to transform the input document into another format
    - ex: compilation
      - compiler that compiles source code into machine code first parses into a parse tree and then translates the tree into a machine code document

### Types of Parsers
- top down parsers
  - examine the high level structure of the syntax and try to find a rule match
- bottom up parsers
  - start with the input and gradually transform it into syntax rules
  - start with the low level rules until the high level rules are met
- generate a parser with a tool
  - feed them the grammar of your language (vocab and syntax rules) and they generate a working parser
- WebKit uses two:
  - Flex for creating a lexer (Lex)
    - input is a file containing regular expression definitions of the tokens
  - Bison for creating a parser (Yacc)
    - language syntax rules in BNF format

### HTML Parser
- parse the HTML markup into a parse tree
  - more difficult grammar because HTML has a "soft" syntax
- custom parser for HTML
  - tokenization
    - lexical analysis
    - parsing the input into tokens
      - start tags, end tags, attribute names, and attribute values
    - recognizes the token, gives it to the tree constructor, and consumes the next character for recognizing the next token, etc
  - tree construction
    - Document object is created
    - stage the DOM tree with the Document in its root
    - elements added to the Document

### DOM
- Document Object Model
  - object presentation of the HTML document and the interface of HTML elements to the outside world (ie JS)
  - root of the tree is the "Document" object
- output tree (parse tree) is a tree of DOM element and attribute nodes
- after parsing is finished, document is considered interactive and will start parsing scripts in deferred mode
- then set to complete and a load event is fired

### CSS Parsing
- CSS specification defines CSS lexical and syntax grammar
- order of processing scripts/style sheets:
  - scripts
    - model of the web is synchronous
    - authors expect scripts to be parsed and executed immediately
      - parsing of document halts until script has been executed
      - if external, needs to be fetched (synchronously) and parsing halts until returned
    - defer a script
      - will execute after the document is parsed
    - HTML5 allows scripts to be parsed asychronously
  - speculative parsing
    - while executing scripts, WebKit and Firefox allows another thread to parse the rest of the document and find out what other resources need to be loaded from the network
    - resources can be loaded on parallel connections
    - ONLY references to external resources (not DOM tree)
  - style sheets
    - Firefox blocks all scripts when there is a style sheet being loaded/parsed
    - WebKit blocks scripts only when they try to access certain style properties that may be affected by unloaded style sheets
    - style has to be loaded and parsed before a script can access it

## Render Tree Construction
- while DOM tree is being constructed, browser creates the render tree
  - tree of visual elements in the order in which they will be displayed
  - visual representation of the document
  - enable painting contents in the correct order
- Firefox calls the elements in the tree _frames_
- WebKit calls them renderer or render object
- each renderer represents a rectangular area usually corresponding to a node's CSS box
  - height, width, position
  - box type is affected by the `display` attribute

### Render tree relation to the DOM tree
- renderers correspond to DOM elements but not one to one relationship
- non-visual DOM elements will not be inserted into the render tree
  - `<head>`
  - any element who has `display: none`
- also, there are DOM elements that correspond to several visual objects
  - usually elements with complex structure that cannot be described by a single rectangle
    - example: `<select>` has 3 renderers
      - one for display area
      - one for drop down list box
      - one for button
    - when text is broken up into multiple lines, the additional lines are additional renderers
  - some render objects correspond to a DOM node but not in the same place
    - floats and absolutely positioned elements are out of flow, placed on a different part of the tree and mapped to the real frame
    - placeholder frame is where they should have been

#### Flow of Constructing the Tree
- Firefox:  
  - presentation is registered to the listener for DOM updates
  - presentation delegates the frame creation to the `FrameConstructor` and the constructor resolves style and creates a frame
- WebKit:
  - process of resolving style and creating a renderer is called _attachment_
  - every DOM node as an attach method
  - attachment is synchronous
  - node insertion to the DOM tree calls the new node attach method
- processing the html and body tags results in the construction of  the render tree root
- root render object corresponds to what the CSS spec calls the containing block: topmost block that contains all other blocks
  - dimensions are the viewport
- rest of tree is constructed as DOM nodes insert

### Style Computation
- building the render tree requires calculating the visual properties of each render object
  - calculate the style properties of each element
  - includes stylesheets of various origins, inline style elements, visual properties of HTML
- origins are browsers default stylesheets, style sheets provided by the author, and user style sheets (provided by the browser user)
- difficulties
  - style data is a very large construct, can cause memory problems
  - finding the matching rules for each element can cause performance issues if not optimized
  - applying the rules requires complex cascade rules that define the hierarchy of the rules

#### Sharing Style Data
- WebKit nodes reference style objects (RenderStyle)
- objects can be shared by nodes in some conditions
- nodes are siblings or cousins and
  - must be in the same mouse state
  - neither has an `id`
  - tag names match
  - class attributes match
  - mapped attributes are identical
  - link states match
  - focus states match
  - neither element is affected by attribute selectors
  - no inline styling
  - no sibling selectors in use at all
    - WebCore throws a global switch when any sibling selector is encountered and disables style sharing for the entire document when present
      - includes `+`, `:first-child`, `:last-child`
- Firefox has two extra trees for easier computation  
  - rule tree
    - enables sharing these values between nodes to avoid computing them again
    - saves space
  - style context tree
    - contain end values
    - computed by applying all matching rules in the correct order and performing manipulations that transform them from logical to concrete values
- also has style objects but not stored in a tree like style context tree, only the DOM node points to its relevant style
- matched rules are stored in a tree
  - bottom nodes in a path have higher priority
  - tree contains all the paths for rule matches that were found
  - storing rules is done lazily
  - whenever a node style needs to be computed, the computed paths are added to the tree

#### Division into structs
- style contexts are divided into structs
  - contain style information for a certain category (like border or color)
  - all properties in a struct are either inherited or non inherited
    - inherited properties are properties that unless defined by the element, are inherited from the parent
    - non inherited (_reset_ properties) use default values if not defined
- tree helps 
