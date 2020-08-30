## The ways to apply CSS to elements

* inline

  ```html
  <h2 style="color: blue;">CatPhotoApp</h2>
  ```

* selector

  ```html
  <style>
    h2 {
      color: red;
    }
  </style>
  ```

  * class

    * `.className`
    * apply CSS to multiple HTML elements

      ```html
      <style>
        .red-text {
          color: red;
        }
      </style>
      ```

  * id

    * `#.idName`
    * unique
    * has a higher specificity(importance) than a class (if both are applied to same element, `id` style will be applied)

  * attribute selector

    * `[attr=value]`

    ```css
    [type='radio'] {
      margin: 20px 0px 20px 0px;
    }
    ```

## Absolute Units vs. Relative Units

* Absolute units: `in`, `mm`
* Relative units: `em` or `rem`

## Inherit and override

* Every elements inherit from `body` tag
* It is possible to override `body` element's CSS.
* If there are more than one class applied to elements, the order of the `class` declarations in the `<style>` section is what is important (later declaration has precedence)
* id attribute takes precedence over class
* Inline style takes precedence over id.

* `!important` takes precedence over inline style.

```html
<style>
  body {
    background-color: black;
    font-family: monospace;
    color: green;
  }
  #orange-text {
    color: orange;
  }
  .pink-text {
    color: pink !important;
  }
  .blue-text {
    color: blue;
  }
</style>
<h1 id="orange-text" class="pink-text blue-text" style="color: white">Hello World!</h1>

```

## CSS Variables

* Create variables

```css
--variableName: value;
--penguin-skin: gray;
```

* Assign its value to other CSS properties

```css
background: var(--penguin-skin);
```

* Fallback

```css
var(--penguin-skin, black)
```

* For Compatibility, it's as easy as providing another more widely supported value immediately before your declaration.

```css
<style>
  :root {
    --red-color: red;
  }
  .red-box {
    background: red;
    background: var(--red-color);
    height: 200px;
    width:200px;
  }
</style>
```

## Inherit CSS Variables

* `:root` is a pseudo-class selector that matches the root element of the document, usually the `html` element. By creating your variables in `:root`, they will be available globally and can be accessed from any other selector in the style sheet.

```css
<style>
  :root {
    /* Only change code below this line */
    --penguin-belly: pink;
    /* Only change code above this line */
  }

  body {
    background: var(--penguin-belly, #c6faf1);
  }
</style>
```

* You can then over-write these variables by setting them again within a specific element

## Property

```html
<style>
  .property-collection {
    color : blue;
	  font-size: 30px;
    font-family: Helvetica, sans-serif; /* FAMILY_NAME, GENERIC_NAME(to degrade)  */
    width: 500px;
    
    border-color: red;
    border-width: 5px;
    border-style: solid;
    border-radius: 10px;
    
    background-color: green;
    
    padding: 10px;
    padding-top: 40px;
    padding-right: 20px;
    padding-bottom: 20px;
    padding-left: 40px;
		/* padding: top right bottom left */
    /* padding: 10px 20px 10px 20px; */
    margin: 10px
    margin-top: 40px;
    margin-right: 20px;
    margin-bottom: 20px;
    margin-left: 40px;
	}	
</style>
```

