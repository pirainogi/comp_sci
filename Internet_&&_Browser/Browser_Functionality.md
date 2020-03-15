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
