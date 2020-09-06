```css
{
  text-align: justify;
  text-align: right;
  text-align: left;
  text-align: center;
  text-transform: lowercase; /*uppercase capitalize initial inherit none */
  
  width: 220px;
  height: 20px;

  background-color: rgba(45, 45, 45, 0.1);
  
  font-size: 27px;
  font-weight: 200;
  
  box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23); /* offset-x offset-y blur-radius spread-radius color */
  opacity: 0.7
    
  line-height: 25px
}
<strong>bold</strong>
<u>underline</u>
<em>italic</em>
<s>strikethrough</s>
<hr>

a:hover { /* pseudo-classes */
  cover: red
}
```

## Relative Position

* CSS Box Model: treats each HTML element as its own box.

  * Block level elements: 100% of the width of its parent element, and as tall as its contents.
  * Inline elements: as tall as their content, and as wide as their content.

* Normal flow: the default layout of elements

* Relative position: how many pixels, percentages, or ems to move the item away from where it is normally positioned.

  * Changing an element's position to relative does not remove it from the normal flow - other elements around

  ```css
  { position: relative}
  ```

## Absolute Position

* This removes the element from the normal flow of the document, so surrounding items ignore it.
* If you forget to add a position rule to the parent item, (this is typically done using `position: relative;`), the browser will keep looking up the chain and ultimately default to the body tag.

```css
{position: absolute}
```

## Fixed Position

* Fixed position is a type of absolute positioning that locks an element relative to the browser window.
* One key difference between the `fixed` and `absolute` positions is that an element with a fixed position won't move when the user scrolls.

```css
{position: fixed};
```

## Push Elements Left or Right with the float property

* Floating elements are removed from the normal flow of a document and pushed to either the `left` or `right` of their containing parent element.

```css
#left {
  float: left;
  width: 50%;
}
#right {
  float: right;
  width: 40%;
}
```

## z-index

higher values for the `z-index` property of an element move it higher in the stack than those with lower values.

```css
.first {
    background-color: red;
    position: absolute;
    z-index: 2;
  }
  .second {
    background-color: blue;
    position: absolute;
    left: 40px;
    top: 50px;
    z-index: 1;
  }
```

## Center an Element Horizontally Using the margin Property

* One way to center a block element horizontally is to set its `margin` to a value of auto.

## Complementary Colors

* complementary colors: two colors are opposite each other on the wheel.

## Tertiary Colors

* Tertiary colors are the result of combining a primary color with one of its secondary color neighbors
* One example that can use tertiary colors is called the split-complementary color scheme

## Hue, Saturation and Lightness

* Hue: color angle (0~360) of the color wheel
* Saturation: the amount of gray in a color (0~100%)
* Lightness is the amount of white or black in a color (0~100%)
* `hsl()` can adjust above characteristics.

## A Gradual CSS Linear Gradient

```css
background: linear-gradient(gradient_direction, color 1, color 2, color 3, ...);

background: linear-gradient(35deg, #CCFFFF, #FFCCCC);
```

* First argument: It can be stated as a degree

## A Striped Element

* `repeating-linear-gradient()`

```css
background: repeating-linear-gradient(
      45deg,
      yellow 0px,
      yellow 40px,
      black 40px,
      black 80px
    );
```

## Background url()

```css
<style>
  body {
    background: url("https://cdn-media-1.freecodecamp.org/imgr/MJAkxbh.png");
  }
</style>

```

## Transform scale Property

```css
#ball2 {
  left: 65%;
  transform: scale(1.5);
}

/* add interactivity to elements */
div:hover {
  transform: scale(1.1);
}

/* The following code skews the paragraph element by -32 degrees along the X-axis. */
p {
  transform: skewX(-32deg);
}
#top {
  background-color: red;
  transform: skewY(-10deg);
}
```

## `::after`, `::before`

* the `content` property is required.
* These pseudo-elements are used to add something before or after a selected element.

```css
.heart::before {
  content: "";
  background-color: yellow;
  border-radius: 25%;
  position: absolute;
  height: 50px;
  width: 70px;
  top: -50px;
  left: 5px;
}
```

## How the CSS @keyframes and animation Properties Work

* Animation properties: how the animation should behave
*  `@keyframes`: what happens during that animation.
```css
<style>
  div {
    height: 40px;
    width: 70%;
    background: black;
    margin: 50px auto;
    border-radius: 5px;
  }

  #rect {
    animation-name: rainbow;
    animation-duration: 4s;
    animation-fill-mode: forwards; /* to stay highlighted */
  }

  @keyframes rainbow {
    0% {
      background-color: blue;
    }
    50% {
      background-color: green;
    }
    100% {
      background-color: yellow;
    }
  }
</style>
<div id="rect"></div>
```
* `animation-fill-mode`  specifies the style applied to an element when the animation has finished.

## Create Movement Using CSS Animation
* Use offset properties `right`, `left`, `top`, and `bottom`

```css
@(Free code camp)keyframes rainbow {
    0% {
      background-color: blue;
      top: 0px;
      left: 0px;
    }
    50% {
      background-color: green;
      top: 50px;
      left: 25px;
    }
    100% {
      background-color: yellow;
      top: 0px;
      left: -25px;
    }
  }
```

## Animate Elements Continually
* `animation-iteration-count`: how many times you would like to loop through the animation.

```css
animation-iteration-count: infinite;
```

## Change Animation Timing with keywords
* `animation-timing-function`: controls how quickly an animated element changes over the duration of the animation.
	* `ease` value: starts slow, speeds up in the middle, and then slows down again in the end.
	* `ease-out`: quick in the beginning then slows down.
	* `ease-in`: slow in the beginning, then speeds up at the end
	* `linear`: a constant animation speed throughout.

## Bezier Curves
* `cubic-bezier(x1, y1, x2, y2)`
	* consist of four main points that sit on this 1 by 1 grid (p0, p1, p2, p3)
	* p0: (0,0)
	* p1: (x1, y1)
	* p2: (x2, y2)
	* p3: (1,1)
* X-axis: the duration of the animation (as a time scale)
* Y-axis: the change in the animation
```css
/* linear */
cubic-bezier(0.25, 0.25, 0.75, 0.75);
```

## Use a Bezier Curve to Move a Graphic
```css
/* speeds up first and then slows down */
animation-timing-function: cubic-bezier(0, 0, 0.58, 1);
```
