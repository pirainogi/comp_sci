# Critical Render Path
- sequence of steps that your browser goes through to convert HTML, CSS, and JS into pixels on the screen
- optimizing the CRP improves render performance
  - optimizing CRP also improves time to first render
  - important to ensure reflows and repaints can happen at 60 frames per second
    - ensures performant user interactions and avoid jank
- CRP includes the DOM, CSSOM, render tree, and layout
1. DOM (document object model) is created as the HTML is parsed
2. HTML may request JS
  - JS may alter the DOM
3. HTML includes or makes request for styles
  - builds the CSSOM
4. Browser engine combines the two to create the Render Tree
5. Layout determines size and location of everything on page
6. Pixels painted to the screen

## Understanding CRP
- web performance includes server requests and responses, loading, scripting, rendering, layout, and painting pixels
1. request for webpage/app starts with HTML request
2. server returns HTML (with response headers and data)
3. browser begins parsing the HTML, converting bytes to the DOM tree
4. browser initializes requests every time it finds links to external resources
  - stylesheets, scripts, embedded image references
5. if a request is blocking, parsing the rest of the HTML is blocked until import asset is handled
6. browser continues to parse the HTML (making requests and building DOM) until the end of the tree
7. browser builds the CSSOM
8. browser builds the render tree
  - computes styles for all visible content
9. layout: defines the location and the size of all render tree elements
10. page is rendered (painted) onto the screen

## DOM
- construction is incremental
- HTMLL response turns into tokes which turn into nodes which turn into the DOM tree.
- single DOM node starts with a startTag token and ends with an endTag token
- nodes contain all relevant info about the HTML element
- info is described using tokens
- nodes are connected into a DOM tree based on token hierarchy
- if another set of startTag/endTag tokens come _between_ a set of startTag/endTags, it makes a node inside of a node
- greater number of nodes, the longer the following events in the critical rendering path will take
- extra nodes won't make a difference but divitis can lead to jank

## CSSOM (CSS Object Model)
- contains all of the styles of the page: info on how to style the DOM
- CSS is render blocking
  - browser blocks page rendering until it receives and processes all of the CSS
  - rules can be overwritten so the content can't be rendered until the entire CSSOM is complete
- as the parser converts tokens into nodes, with descendants of nodes inheriting styles
- incremental processing features don't apply to CSS like they do to HTML because subsequent rules may override previous ones
- CSSOM is built as the CSS is parsed, but it can't be used to built the render tree until it is completely parsed
- less specific selectors are faster than more specific ones
  - `.foo {}` is faster than `.foo .bar {}` because when the browser finds `.foo` in the second scenario, it has to walk up the DOM to check if `.foo` has an ancestor `.bar`
    - penalty isn't likely worth optimizing
- optimizing CSS: minification, and separating deferred CSS into non-blocking requests by using media queries

## Render Tree
- captures both content and styles
  - DOM and CSSOM are combined into the render tree
- browser checks every node starting from the root of the DOM tree, determines which CSS rules are attached
- only captures visible content
  - head is not included in the render tree
- if `display: none` is set on an element, neither it or its descendants are in the render tree

## Layout
- Layout is dependent on the size of the screen
- determines where and how elements are positioned on the page, determining height and width of each elements and where they are in relation to each other
- layout happens every time a device is rotated or a browser is resized
- layout performance is impacted by the DOM
  - greater number of nodes, the longer layout takes
- layout can be a bottleneck, leading to jank if required during scrolling or other animations
  - 20ms delay on load or orientation may be fine, but leads to jank on animation or scroll
- any time the render tree is modified (added nodes, altered content, or updated box model styles on a node) layout occurs
- to reduce frequency and duration of layout events, batch updates and avoid animating box model properties
- block level elements, by definition, have a default width of 100% of the width of their parent
- element with a width of 50% will be half the width of its parent
- unless otherwise defined, the body has a width of 100%
  - 100% of the viewport
- width of device impacts layout
  - viewport meta tag defines the width of the layout viewport
  - by-default full screen browsers, like a phone's browser, by setting `<meta name="viewport" content="width=device-width">` the width will be the width of the device instead of the viewport width
  - device-width changes when a user rotates their phone btw landscape and portrait mode

## Paint
- once the render tree is created and layout occurs, pixels can be painted on the screen
- onload, the entire screen is painted
- after that, only impacted areas of the screen will be repainted
  - browsers are optimized to repaint the minimal areas required
- paint time depends on what kind of updates are being applied to the render tree
- painting is fast, but important to remember to allow both layout and repaint times when measuring how long an animation frame may take

## Optimizing for CRP
- prioritize which resources get loaded
- control the order in which they are loaded
- reduce the file sizes of resources
- minimize the number of critical resources by deferring their download, marking as async, or eliminate all together
- optimize the number of requests required along with the file size of each request
- optimize the order in which critical resources are loaded by prioritizing the downloading of critical assets, shorten the critical path length 
