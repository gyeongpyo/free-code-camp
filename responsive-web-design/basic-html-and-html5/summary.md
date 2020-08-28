* tags give a descriptive structure to your HTML, make your HTML easier to read, and help with Search Engine Optimization (SEO) and accessibility.

## Anchor Elements

* Link to Internal Section

  * you assign a link's `href` attribute to a `#` plus the value of the `id`

    ```html
    <a href="#contacts-header">Contacts</a>
    ...
    <h2 id="contacts-header">Contacts</h2>
    ```

## Radio Button

```html
<label for="indoor"> 
  <input id="indoor" type="radio" name="indoor-outdoor">Indoor 
</label>
```

* It is considered best practice to set a `for` attribute on the `label` element, with a value that matches the value of the `id` attribute of the `input` element. This allows assistive technologies to create a linked relationship between the label and the child `input` element. For example:

* Why is input tag nested within label tag: https://stackoverflow.com/a/12894185