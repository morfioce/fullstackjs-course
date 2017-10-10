# How to structure an HTML form

With the basics out of the way, we now look in more detail at the elements used to provide structure and meaning to the different parts of a form.

## The `form` element

The `<form>` element formally defines a form and attributes that determine the behavior of this form. Each time you want to create an HTML form, you must start it by using this element, putting all the contents inside. Many assistive technologies or browser plugins can discover `<form>` elements and implement special hooks to make them easier to use.

We already met this in the prevous article.

>	It's strictly forbidden to nest a form inside another form. Nesting can cause forms to behave in an unpredictable manner based on the browser that is being used.

## The `<fieldset>` and `<legend>` elements

The `<fieldset>` element is a convenient way to create groups of widgets that share the same purpose, for styling and semantic purposes. You can label a `<fieldset>` by including a `<legend>` element just below the opening `<fieldset>` tag. The text content of the `<legend>` formally describes the purpose of the `<fieldset>`. It is included inside.

Many assistive technologies will use the `<legend>` element as if it is a part of the label of each widget inside the corresponding `<fieldset>` element. For example, some screen readers such as Jaws or NVDA will speak the legend's content before speaking the label of each widget.

Here is a little example:

```html
<form>
  <fieldset>
    <legend>Fruit juice size</legend>
    <p>
      <input type="radio" name="size" id="size_1" value="small">
      <label for="size_1">Small</label>
    </p>
    <p>
      <input type="radio" name="size" id="size_2" value="medium">
      <label for="size_2">Medium</label>
    </p>
    <p>
      <input type="radio" name="size" id="size_3" value="large">
      <label for="size_3">Large</label>
    </p>
  </fieldset>
</form>
```

When reading the above form, a screen reader will speak "Fruit juice size small" for the first widget, "Fruit juice size medium" for the second, and "Fruit juice size large" for the third.

The use case in this example is one of the most important. Each time you have a set of radio buttons, you ought to nest them inside a `<fieldset>` element. There are other use cases, and in general the `<fieldset>` element can also be used to section a form. Ideally long forms should be split across multiple pages, but if a form is getting long but has to be on a single page, putting the different related sections inside different fieldsets can improve usability.

Because of its influence over assistive technology, the `<fieldset>` element is one of the key elements for building accessible forms; however it is your responsibility not to abuse it. If possible, each time you build a form, try to listen to how a screen reader interprets it. If it sounds odd, try to improve the form structure.

## The <label> element

As we saw in the previous article, The `<label>` element is the formal way to define a label for an HTML form widget. This is the most important element if you want to build accessible forms — when implemented properly, screenreaders will speak a form element's label along with any related instructions. Take this example, which we saw in the previous article:

```html
<label for="name">Name:</label> <input type="text" id="name" name="user_name">
```

With the `<label>` associated correctly with the `<input>` via their `for` and `id` attributes respectively (the label `for` attribute references the `id` attribute of the corresponding widget), a screenreader will read out something like "Name, edit text".

If the label isn't set up correctly, a screenreader will only read out something like "Edit text blank", which isn't very helpful at all.

Note that a widget can be nested inside its `<label>` element, like so:

```html
<label for="name">
  Name: <input type="text" id="name" name="user_name">
</label>
```

Even in such cases however, it is considered best practice to set the `for` attribute because some assistive technologies do not understand implicit relationships between labels and widgets.

## Common HTML structures used with forms

Beyond the structures specific to HTML forms, it's good to remember that forms are just HTML. This means that you can use all the power of HTML to structure an HTML form.

As you can see in the examples, it's common practice to wrap a label and its widget with a `<div>` element. `<p>` elements are also commonly used, as are HTML lists (the latter is most common for structuring multiple checkboxes or radio buttons).

In addition to the `<fieldset>` element, it's also common practice to use HTML titles (e.g.`<h1>, <h2>`) and sectioning (e.g. `<section>`) to structure a complex form.

Above all, it is up to you to find a style that you find comfortable to code with, and which also results in accessible, usable forms.

This has each separate section of functionality contained in `<section>` elements, and a `<fieldset>` to contain the radio buttons.

## Active learning: building a form structure

Let's put these ideas into practice and build a slightly more involved form structure — a payment form. This form will contain a number of widget types that you may not yet understand — don't worry about this for now. For now, read the descriptions carefully as you follow the below instructions, and start to form an appreciation of which wrapper elements we are using to structure the form, and why.7

1. To start with, make a local copy of our blank template file and the <a href="active_learning/payment_style.css">CSS</a> for our payment form in a new directory on your computer.

2. First of all, apply the CSS to the HTML by adding the following line inside the HTML `<head>`:
```html
<link href="payment_style.css" rel="stylesheet">
```

3. Next, start your form off by adding the outer `<form>` element:
```html
<form>

</form>
```

4. Inside the `<form>` tags, start by adding a heading and paragraph to inform users how required fields are marked:
```html
h1>Payment form</h1>
<p>Required fields are followed by <strong><abbr title="required">*</abbr></strong>.</p>
```

5. Next we'll add a larger section of code into the form, below our previous entry. Here you'll see that we are wrapping the contact information fields inside a distinct `<section>` element. Moreover, we have a set of two radio buttons, each of which we are putting inside its own list (`<li>`) element. Last, we have two standard text `<input>`s and their associated `<label>` elements, each contained inside a `<p>`, plus a password input for entering a password. Add this code to your form now:  
