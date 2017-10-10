# Your first HTML form

The first article in our series provides your very first experience of creating an HTML form, including designing a simple form, implementing it using the right HTML elements, adding some very simple styling via CSS, and how data is sent to a server.

## What are HTML forms?

HTML Forms are one of the main points of interaction between a user and a web site or application. They allow users to send data to the web site. Most of the time that data is sent to the web server, but the web page can also intercept it to use it on its own.

An HTML Form is made of one or more widgets. Those widgets can be text fields (single line or multiline), select boxes, buttons, checkboxes, or radio buttons. Most of the time those widgets are paired with a label that describes their purpose — properly implemented labels are able to clearly instruct both sighted and blind users on what to enter into a form input.

The main difference between a HTML form and a regular HTML document is that most of the time, the data collected by the form is sent to a web server. In that case, you need to set up a web server to receive and process the data. How to set up such a server is beyond the scope of this article, but if you want to know more, see Sending form data later in the module.

## Designing your forms

Before starting to code, it's always better to step back and take the time to think about your form. Designing a quick mockup will help you to define the right set of data you want to ask your user. From a user experience (UX) point of view, it's important to remember that the bigger your form, the more you risk losing users. Keep it simple and stay focused: ask only for that data you absolutely need. Designing forms is an important step when you are building a site or application. It's beyond the scope of this article to cover the user experience of forms, but if you want to dig into that topic you should read the following articles:


* Smashing Magazine has very <a href="http://uxdesign.smashingmagazine.com/tag/forms/">good articles</a> about forms UX, but perhaps the most important is their Extensive Guide To Web Form Usability.
* UXMatters is also a very thoughtful resource with good advice from basic <a href="http://www.uxmatters.com/mt/archives/2012/05/7-basic-best-practices-for-buttons.php">best practices</a> to complex concerns such as multi-page forms.

In this article, we'll build a simple contact form. Let's make a rough sketch.

<p align="center">
	<img src="images/form-sketch-low.jpg" alt="">
</p>

Our form will contain three text fields and one button. We are asking the user for their name, their e-mail and the message they want to send. Hitting the button will send their data to a web server.

## Active learning

Ok, now we're ready to go to HTML and code our form. To build our contact form, we will use the following HTML elements: `<form>`, `<label>`, `<input>`, `<textarea>`, and `<button>`.

Before you go any further, make a local copy of our <a href="active_learning/form_starter.html">simple HTML template</a> — you'll enter your form HTML into here.

<strong>The `<form>` element</strong>

All HTML forms start with a `<form>` element like this:
```html
<form action="/my-handling-form-page" method="post">

</form>
```

This element formally defines a form. It's a container element like a `<div>` or `<p>` element, but it also supports some specific attributes to configure the way the form behaves. All of its attributes are optional but it's considered best practice to always set at least the action attribute and the method attribute.

* The `action` attribute defines the location (URL) where the form's collected data should be sent when it is submitted.
* The `method` attribute defines which HTTP method to send the data with (it can be "get" or "post").

For now, add the above `<form>` element into your HTML body.

<strong>The `<label>`, `<input>`, and `<textarea>` elements</strong>

Our contact form is really simple and contains three text fields, each with a label. The input field for the name will be a basic single-line text field, the input field for the e-mail will be a single-line text field that accepts only an e-mail address, and the input field for the message will be a basic multiline text field.

In terms of HTML code we need something like the following to implement these form widgets:

```html
form action="/my-handling-form-page" method="post">
    <div>
        <label for="name">Name:</label>
        <input type="text" id="name" name="user_name">
    </div>
    <div>
        <label for="mail">E-mail:</label>
        <input type="email" id="mail" name="user_mail">
    </div>
    <div>
        <label for="msg">Message:</label>
        <textarea id="msg" name="user_message"></textarea>
    </div>
</form>
```

Update your form code to look like the above.

The `<div>` elements are there to conveniently structure our code and make styling easier (see later in the article). Note the use of the for attribute on all `<label>` elements; it's a formal way to link a label to a form widget. This attribute references the id of the corresponding widget. There is some benefit to doing this. The most obvious one is to allow the user to click on the label to activate the corresponding widget.

On the `<input>` element, the most important attribute is the type attribute. This attribute is extremely important because it defines the way the `<input>` element behaves. It can radically change the element so pay attention to it.

* In our simple example we use the value `text` for the first input — the default value for this attribute. It represents a basic single-line text field that accepts any kind of text input.
* For the second input, we use the value `email` that defines a single-line text field that only accepts a well-formed e-mail address. This last value turns a basic text field into a kind of "intelligent" field that will perform some checks on the data typed by the user.

>	Last but not least, note the syntax of `<input>` vs. `<textarea></textarea>`. This is one of the oddities of HTML. The `<input>` tag is an empty element, meaning that it doesn't need a closing tag. On the contrary, `<textarea>` is not an empty element, so you have to close it with the proper ending tag. This has an impact on a specific feature of HTML forms: the way you define the default value. To define the default value of an `<input>` element you have to use the value attribute like this:

```html
<input type="text" value="by default this element is filled with this text" />
```

On the contrary, if you want to define the default value of a `<textarea>`, you just have to put that default value between the starting and ending tag of the `<textarea>` element, like this:
```html
<textarea>by default this element is filled with this text</textarea>
```

<strong>The `<button>` element</strong>

Our form is almost ready; we just have to add a button to allow the user to send their data once they have filled out the form. This is simply done by using the `<button>`element; add the following just above the closing `</form>` tag:

```html
<div class="button">
  <button type="submit">Send your message</button>
</div>
```

You'll see that the `<button>` element also accepts a type attribute — this accepts one of three values: submit, reset, or button.

* A click on a `submit` button (the default value) sends the form's data to the web page defined by the `action` attribute of the `<form>` element.
* A click on a `reset` button resets all the form widgets to their default value immediately. From a UX point of view, this is considered bad practice.
* A click on a `button` does... nothing! That sounds silly, but it's amazingly useful for building custom buttons with JavaScript.

>	<strong>Note</strong>: You can also use the `<input>` element with the corresponding type to produce a button, for example `<input type="submit">`. The main advantage of the `<button>` element is that the `<input>` element only allows plain text as its label whereas the `<button>` element allows full HTML content, allowing more complex, creative button text.
