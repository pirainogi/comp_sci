# Scrolling
- Browser needs to draw your site/application to the screen upon scroll event
  - opportunity to minimize the work the browser has to do ini order to get everything drawn and maximize page performance

## How the Browser Draws
- DOM tree: all of the elements within the page  
- Browser looks at your styled DOM and finds things it think will look the same when you scroll
- groups elements together and takes a picture of them
  - **layer**
- Each of those layers needs to be painted and rasterized to a texture and then composited together to the image that you see on the screen
- scrolling likely requires the browser to paint some of the pixels in those layers (compositor layers)
  - by grouping into layers, we only need to update that specific layer's texture when something inside that specific layer has changed
  - only need to update where we want to only paint and rasterize the part of the render layer's texture that has been damaged rather than the whole thing
- _less painting is better_

## Expensive Styles
- not all styles are created equal
  - associated draw code for some styling takes a long time to run comparatively
  - styles that require repainting often cause hits in performance  
- everything is changing so something that's slow today could be fast tomorrow
- browser to browser differences
- leverage dev tools to identify the bottleneck and then see how to reduce the browser's workload

## Reflows and Repaints
- reflowing
  - requesting `offsetTop` in JS requires a lot of work
    - browser needs to layout the  page in order to determine the answer
- changing another property based on `offsetTop` value, element (and compositor layer) needs to be repainted > expensive  
  - knock-on effect that we invalidated that `offsetTop` calculation by repainting
    - browser understands something to have changed
- when you scale reflowing to a collection of elements
  - force the browser into an expensive and unnecessary reflow-repaint cycle
  - avoid by collecting the `offsetTop` values first and then do visual updates
    - doesn't need to repeatedly recalculate the positions of the images on the page (if we use `requestAnimationFrame`, schedule visual updates at optimal time for the browser)

## Debouncing Scroll Events
- Store the last scroll value in a variable whenever you receive a scroll event, perform your visual updates in a `requestAnimationFrame`, making use of the last known value
- Browser can schedule the visual updates at the correct time
  - no more actual work than necessary inside each frame 
