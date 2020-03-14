# Grid  
- CSS layout method designed for the two-dimensional layout of items on a webpage or application

## Basic Concepts
- method of creating grid structures that are described in CSS (not HTML).
- creates layouts that can be redefined using Media Queries to adapt to different contexts
- separate the order of elements in the source from their visual presentation  
  - change the location of page elements as is best for your layout at different breakpoints
  - do not need to compromise a sensible structured document for your responsive design

### Flexbox
- one-dimensional layouts

## Terminology
- **grid lines**: lines that made up the grid
  - can be horizontal or vertical
  - refer by number or name
- **grid tracks**: space between two grid lines
  - either horizontal or vertical
- **grid cell**: space  between four grid lines
  - smallest unit in our grid that is available to place an item into
- **grid area**: any area in the grid bound by four grid lines
  - may contain any number of grid cells

## Defining a Grid
- `display:  grid`or `display: inline-grid` on the _parent_ element
- create the gride using `grid-template-columns` and `grid-template-rows`
- `grid-gap` creates a gap between columns and rows
  - shorthand for `grid-column-gap` and `grid-row-gap` to set individually
- `grid-column-start` and `grid-row-start`
- `grid-column-end` and `grid-row-end`
  - if an item will only span one grid track, you can omit the `-end` value

## Examples

### 4x4 Grid Template
![codepen](https://codepen.io/pirainogi/pen/BaNrErP)
```HTML
<div class="wrapper">
  <div class="box a"></div>
  <div class="box b"></div>
  <div class="box c"></div>
  <div class="box d"></div>
</div>
```
```CSS
.wrapper {
  display: grid;
  grid-template-columns: 100px, 100px;
  grid-gap: 10px;
}

.box {
  background-color: green;
}
```

### 4x4 Grid (Line-Based)
![codepen](https://codepen.io/pirainogi/pen/GRJxLwd)
```CSS
.wrapper {
  display: grid;
  grid-template-columns: 50px 50px;
  grid-gap: 5px;
}

.box {
  background-color: green;
  height: 50px
}

.a {
  grid-column-start: 2;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 2;
}

.b {
  grid-column-start: 2;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 3;
}

.c {
  grid-column-start: 1;
  grid-column-end: 2;
  grid-row-start: 2;
  grid-row-end: 3;
}

.d {
  grid-column-start: 1;
  grid-column-end: 2;
  grid-row-start: 1;
  grid-row-end: 2;
}
```
