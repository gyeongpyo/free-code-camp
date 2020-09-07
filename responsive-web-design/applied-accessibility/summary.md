**General concepts**
1. have well-organized code that uses appropriate markup
2. ensure text alternatives exist for non-text and visual content
3. Create an easily-navigated page that's keyboard-friendly

## Add a Text Alternative to Images for Visually Impaired Accessibility
* `Alt`: describes the content of the image and provides an text-alternative for it. it's used by search engines to understand what an image contains.
* Screen readers can access the `alt` attribute and read its contents to deliver key information

## Know When Alt Text Should be Left Blank
* When an image is already explained with text content, or does not add meaning to page, the `img` still needs an `alt` attribute.

## Use Heading to Show Hierarchical Relationships of Content.
* Screen readers can be set to read only the headings on a page so the users gets a summary.
* It's important for the heading tags to have semantic meaning ,not be picked merely for their size values.
* *Semantic meaning* : the tags indicates the type of information it contains.
* each page should always have one (and only one) h1 element.

## Jump Straight to the Content Using the main Element
* `main`, `header`, `footer`, `nav`, `article`, and `section`
*  Using them where appropriate gives additional meaning in your markup.

##Wrap Content in the article Element
* `article` is a sectioning element, and is used to wrap independent, self-contained content.
* Determining whether content can stand alone
	* removing all surrounding context, would that content still make sense?
	* Would the content hold up if it were in an RSS feed?
* An `article` is for standalone content, and a `section` is for grouping thematically related content.
	* if a book is the article, then each chapter is a section. When there's no relationship between groups of content, then use a div.
```css
<div> - groups content
<section> - groups related content
<article> - groups independent, self-contained content
```
## Make Screen Reader Navigation Easier with the header Landmark
* `header`: used to wrap introductory information or navigation links for its parent tag.
* The `header` is meant for use in the `body` tag of your HTML document. This is different than the `head` element, which contains the page's title, meta information, etc.

## Make Screen Reader Navigation Easier with the nav Landmark
* `nav`: is meant to wrap around the main navigation links in your pages.

## Make Screen Reader Navigation Easier with the footer Landmark
* `footer`: It's primarily used to contain copyright information or links to related documents that usually sit at the bottom of a page.

## Improve Accessibility of Audio Content with the audio Element
* `audio`: gives semantic meaning when it wraps sound or audio stream content in you markup.
* The `audio` tag supports the `controls` attribute. This shows the browser default play, pause, and other controls, and supports keyboard functionality.
```css
<audio id="meowClip" controls>
  <source src="audio/meow.mp3" type="audio/mpeg" />
  <source src="audio/meow.ogg" type="audio/ogg" />
</audio>
```

## Improve Chart Accessibility with the figure Element
* `figure`, `figcaption` : wrap a visual representation with its caption.
* This gives a two-fold accessibility boost by both semantically grouping related content, and providing a text alternative that explains the `figure`.
```css
<figure>
  <img src="roundhouseDestruction.jpeg" alt="Photo of Camper Cat executing a roundhouse kick">
  <br>
  <figcaption>
    Master Camper Cat demonstrates proper form of a roundhouse kick.
  </figcaption>
</figure>
```

## Improve Form Field Accessibility with the label Element
* `label` wraps the text for a specific form control item.
* The `for` attribute on a `label` tag explicitly associates that `label` with the from and is used by screen readers.
* The value of the for attribute must be the same as the value of the id attribute of the form control.
```css
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name">
</form>
```

## Wrap Radio Buttons in a fieldset Element for Better Accessibility
* `fieldset` surrounds the entire grouping of radio buttons to achieve this.
* `legend` provide a description for the grouping.
* The `fieldset` wrapper and `legend` tag are not necessary when the choices are self-explanatory, like a gender selection.
```css
<form>
  <fieldset>
    <legend>Choose one of these three items:</legend>
    <input id="one" type="radio" name="items" value="one">
    <label for="one">Choice One</label><br>
    <input id="two" type="radio" name="items" value="two">
    <label for="two">Choice Two</label><br>
    <input id="three" type="radio" name="items" value="three">
    <label for="three">Choice Three</label>
  </fieldset>
</form>
```
## Add an Accessible Date Picker
* `type` attribute of the `input` field
	* `text`, `submit`, `date`
	* 
```css
<label for="input1">Enter a date:</label>
<input type="date" id="input1" name="input1">
```

## Standardize Times with the HTML 5 datetime Attribute
```css
<p>Master Camper Cat officiated the cage match between Goro and Scorpion <time datetime="2013-02-13">last Wednesday</time>, which ended in a draw.</p>
```

## Make Elements Only Visible to a Screen Reader by Using Custom CSS
* CSS is used to position the screen reader-only elements off the visual area of the browser window.
> display: none; or visibility: hidden; hides content for everyone, including screen reader users
> Zero values for pixel sizes, such as width: 0px; height: 0px; removes that element from the flow of your document, meaning screen readers will ignore it
```css
.sr-only {
  position: absolute;
  left: -10000px;
  width: 1px;
  height: 1px;
  top: auto;
  overflow: hidden;
}
```

## Improve Readability with High Contrast Text
* The Web Content Accessibility Guidelines (WCAG) recommend at least a 4.5 to 1 contrast ratio for normal text. The ratio is calculated by comparing the relative luminance values of two colors.

##Avoid Colorblindness Issues by Using Sufficient Contrast
* Two accesibility issues
	* screen reader users won't see it
	* foreground and background colors need sufficient contrast

## Avoid Colorblindness Issues by Carefully Choosing Colors that Convey Information
*  Close colors can be thought of as neighbors on the color wheel, and those combinations should be avoided when conveying important information.

## Give Links Meaning by Using Descriptive Link Text
```css
<a href="">information about batteries</a>
```

## Make Links Navigable with HTML Access Keys
* `accesskey`: to specify a shortcut key to activate or bring focus to an element. (for keyboard-only users)
```css
<button accesskey="b">Important Button</button>
```

## Use tabindex to Add Keyboard Focus to an Element
* `tabindex`:
	* 0: automatically receive keyboard focus when a user tabs through a page
	* -1: indicates that an element is focusable, but is not reachable by the keyboard.
```css
<div tabindex="0">I need keyboard focus!</div>
```

## Use tabindex to Specify the Order of Keyboard Focus for Several Elements
* `tabindex` attribute also specifies the exact tab order of elements. (greater than or equal to 1)
	* Then it cycles through the sequence of specified `tabindex` values (2, 3, etc.), before moving to default and` tabindex="0"` items.