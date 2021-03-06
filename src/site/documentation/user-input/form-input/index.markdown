---
layout: article
title: "Create Amazing Forms"
description: "Forms are hard to fill out on mobile. The best forms are the ones with the
fewest inputs."
introduction: "Forms are hard to fill out on mobile. The best forms are the ones with the
fewest inputs. Good forms provide semantic input types. Keys should change to
match the user's input type; users pick a date in a calendar. Keep your user
informed. Validation tools should tell the user what they need to do before
submitting the form."
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
collection: user-input
key-takeaways:
  label-and-name:
    - Always use <code>label</code>s on form inputs, and ensure they're visible when
      the field is in focus.
    - Use <code>placeholder</code>s to provide guidance about what you expect.
    - To help the browser auto-complete the form, use established <code>name</code>'s
      for elements and include the <code>autocomplete</code> attribute.
  choose-best-input-type:
    - Choose the most appropriate input type for your data to simplify input.
    - Offer suggestions as the user types with the <code>datalist</code> element.
  provide-real-time-validation:
    - Leverage the browser's built-in validation attributes like
      <code>pattern</code>, <code>required</code>, <code>min</code>,
      <code>max</code>, etc.
    - Use JavaScript and the Constraints Validation API for more complex
      validation requirements.
    - Show validation errors in real time, and if the user tries to submit an
      invalid form, show all fields they need to fix.
  use-request-auto-complete:
    - <code>requestAutocomplete</code> can greatly simplify the checkout process and
      improve the user experience.
    - If <code>requestAutocomplete</code> is available, hide the checkout form and move people
      directly to the confirmation page.
    - Ensure input fields include the appropriate autocomplete attribute.
remember:
  use-placeholders:
    - Placeholders disappear as soon as focus is placed in an element, thus
      they are not a replacement for labels.  They should be used as an aid
      to help guide users on the required format and content.
  recommend-input:
    - Auto-complete only works when the form method is post.
  use-datalist:
    - The <code>datalist</code> values are provided as suggestions, and users
      are not restricted to the suggestions provided.
  provide-real-time-validation:
    - Even with client-side input validation, it is always important to
      validate data on the server to ensure consistency and security in your data.
  show-all-errors:
    - You should show the user all of the issues on the form at once, rather than showing them one at a time.
  request-auto-complete-flow:
    - If you're asking for any kind of personal information or credit card
      data, ensure the page is served via SSL.  Otherwise the dialog will
      warn the user their information may not be secure.
---
{% wrap content %}

<style>
  img, video, object {
    max-width: 100%;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  table.inputtypes th:nth-of-type(2) {
    min-width: 270px;
  }

  table.tc-heavyright th:first-of-type {
    width: 30%;
  }
</style>

{% include modules/toc.liquid %}

## Label and name inputs properly

{% include modules/takeaway.liquid list=page.key-takeaways.label-and-name %}

### The importance of labels

The `label` element provides direction to the user, telling them what
information is needed in a form element.  Each `label` is associated with an
input element by placing it inside the `label` element, or by using the "`for`"
attribute.  Applying labels to form elements also helps to improve the touch
target size: the user can touch either the label or the input in order to place
focus on the input element.

{% include_code _code/order.html labels %}

### Label sizing and placement

Labels and inputs should be large enough to be easy to press.  In portrait
viewports, field labels should be above input elements, and beside them in
landscape.  Ensure field labels and the corresponding input boxes are visible at
the same time.  Be careful with custom scroll handlers that may scroll input
elements to the top of the page hiding the label, or labels placed below input
elements may be covered by the virtual keyboard.

### Use placeholders

The placeholder attribute provides a hint to the user about what's expected in
the input by displaying its value as light text until the element gets focus.

<input type="text" placeholder="MM-YYYY">

{% highlight html%}
<input type="text" placeholder="MM-YYYY" ...>
{% endhighlight %}


{% include modules/remember.liquid title="Remember" list=page.remember.use-placeholders %}


### Use metadata to enable auto-complete

Users appreciate when websites save them time by automatically filling common
fields like names, email addresses and other frequently used fields, plus it
helps to reduce potential input errors -- especially on virtual keyboards and
small devices.

Browsers use many heuristics to determine which fields they can
[auto-populate](https://support.google.com/chrome/answer/142893) [based on
previously specified data by the
user](https://support.google.com/chrome/answer/142893), and you can give hints
to the browser by providing both the name attribute and the autocomplete
attribute on each input element.

For example, to hint to the browser that it should auto-complete the form with
the users name, email address and phone number, you should use:

{% include_code _code/order.html autocomplete %}


### Recommended input `name` and `autocomplete` attribute values

<table class="table-3 autocompletes">
  <thead>
    <tr>
      <th data-th="Content type">Content type</th>
      <th data-th="name attribute"><code>name</code> attribute</th>
      <th data-th="autocomplete attribute"><code>autocomplete</code> attribute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Content type">Name</td>
      <td data-th="name attribute">
        <code>name</code>
        <code>fname</code>
        <code>mname</code>
        <code>lname</code>
      </td>
      <td data-th="autocomplete attribute"><code>name</code></td>
    </tr>
    <tr>
      <td data-th="Content type">Email</td>
      <td data-th="name attribute"><code>email</code></td>
      <td data-th="autocomplete attribute"><code>email</code></td>
    </tr>
    <tr>
      <td data-th="Content type">Address</td>
      <td data-th="name attribute">
        <code>address</code>
        <code>city</code>
        <code>region</code>
        <code>province</code>
        <code>state</code>
        <code>zip</code>
        <code>zip2</code>
        <code>postal</code>
        <code>country</code>
      </td>
      <td data-th="autocomplete attribute">
        <code>street-address</code>
        <code>locality</code>
        <code>region</code>
        <code>postal-code</code>
        <code>country</code>
      </td>
    </tr>
    <tr>
      <td data-th="Content type">Phone</td>
      <td data-th="name attribute">
        <code>phone</code>
        <code>mobile</code>
        <code>country-code</code>
        <code>area-code</code>
        <code>exchange</code>
        <code>suffix</code>
        <code>ext</code>
      </td>
      <td data-th="autocomplete attribute"><code>tel</code></td>
    </tr>
    <tr>
      <td data-th="Content type">Credit Card</td>
      <td data-th="name attribute">
        <code>ccname</code>
        <code>cardnumber</code>
        <code>cvc</code>
        <code>ccmonth</code>
        <code>ccyear</code>
        <code>exp-date</code>
        <code>card-type</code>
      </td>
      <td data-th="autocomplete attribute">
        <code>cc-name</code>
        <code>cc-number</code>
        <code>cc-csc</code>
        <code>cc-exp-month</code>
        <code>cc-exp-year</code>
        <code>cc-exp</code>
        <code>cc-type</code>
      </td>
    </tr>
  </tbody>
</table>

The `autocomplete` attributes should be prefixed with either `shipping` or `billing`, depending on the context.


{% include modules/remember.liquid title="Remember" list=page.remember.recommend-input %}

### The `autofocus` attribute

On some forms, for example the Google home page where the only thing you want
the user to do is fill out a particular field, you can add the `autofocus`
attribute.  When set, desktop browsers immediately move the focus to the input
field, making it easy for users to quickly begin using the form.  Mobile
browsers ignore the `autofocus` attribute, to prevent the keyboard from randomly
appearing.

Be careful using the autofocus attribute because it will steal keyboard focus
and potentially preventing the backspace character from being used for
navigation.

{% highlight html %}
<input type="text" autofocus ...>
{% endhighlight %}

## Choose the best input type

Every tap counts. Users appreciate websites that automatically present number
pads for entering phone numbers, or automatically advance fields as they entered
them. Look for opportunities to eliminate wasted taps in your forms.

{% include modules/takeaway.liquid list=page.key-takeaways.choose-best-input-type %}

### HTML5 input types

HTML5 introduced a number of new input types. These new input types give hints
to the browser about what type of keyboard layout to display for on-screen
keyboards.  Users are more easily able to enter the required information without
having to change their keyboard and only see the appropriate keys for that input
type.

<table class="table-2 inputtypes">
  <thead>
    <tr>
      <th data-th="Input type">Input <code>type</code></th>
      <th data-th="Typical keyboard">Typical Keyboard</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Input type">
        <code>url</code><br> For entering a URL. It must start with a valid URI scheme,
        for example <code>http://</code>, <code>ftp://</code> or <code>mailto:</code>.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/url-ios.png" srcset="imgs/url-ios.png 1x, imgs/url-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>tel</code><br>For entering phone numbers. It does <b>not</b>
        enforce a particular syntax for validation, so if you want to ensure
        a particular format, you can use pattern.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/tel-android.png" srcset="imgs/tel-android.png 1x, imgs/tel-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>email</code><br>For entering email addresses, and hints that
        the @ should be shown on the keyboard by default. You can add the
        multiple attribute if more than one email address will be provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/email-android.png" srcset="imgs/email-android.png 1x, imgs/email-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>search</code><br>A text input field styled in a way that is
        consistent with the platform's search field.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/plain-ios.png" srcset="imgs/plain-ios.png 1x, imgs/plain-ios-2x.png 2x" class="keybimg">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>number</code><br>For numeric input, can be any rational
        integer or float value.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/number-android.png" srcset="imgs/number-android.png 1x, imgs/number-android-2x.png 2x" class="keybimg">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>range</code><br>For number input, but unlike the number input
        type, the value is less important. It is displayed to the user as a
        slider control.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/range-ios.png">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>datetime-local</code><br>For entering a date and time value
        where the time zone provided is the local time zone.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/datetime-local-ios.png" srcset="imgs/datetime-local-ios.png 1x, imgs/datetime-local-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>date</code><br>For entering a date (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/date-android.png" srcset="imgs/date-android.png 1x, imgs/date-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>time</code><br>For entering a time (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/time-ios.png" srcset="imgs/time-ios.png 1x, imgs/time-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>week</code><br>For entering a week (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/week-android.png" srcset="imgs/week-android.png 1x, imgs/week-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>month</code><br>For entering a month (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/month-ios.png" srcset="imgs/month-ios.png 1x, imgs/month-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>color</code><br>For picking a color.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/color-android.png" srcset="imgs/color-android.png 1x, imgs/color-android-2x.png 2x">
      </td>
    </tr>
  </tbody>
</table>

### Offer suggestions during input with datalist

The `datalist` element isn't an input type, but a list of suggested input values
to associated with a form field. It lets the browser suggest autocomplete
options as the user types. Unlike select elements where users must scan long
lists to find the value they're looking for, and limiting them only to those
lists, `datalist`s provide hints as the user types.

{% include_code _code/order.html datalist %}

{% include modules/remember.liquid title="Remember" list=page.remember.use-datalist %}

## Provide real-time validation

Real-time data validation doesn't just help to keep your data clean, but it also
helps improve the user experience.  Modern browsers have several built-in tools
to help provide real-time data validation and may prevent the user from
submitting an invalid form.  Visual cues should be used to indicate whether a
form has been completed properly.

{% include modules/takeaway.liquid list=page.key-takeaways.provide-real-time-validation %}

### Use these attributes to validate input

#### The `pattern` attribute

The `pattern` attribute specifies a [regular
expression](http://en.wikipedia.org/wiki/Regular_expression) used to validate an
input field. For example, to validate a US Zip code (5 digits, sometimes
followed by a dash and an additional 4 digits), we would set the `pattern` like
this:

{% highlight html %}
<input type="text" pattern="^\d{5,6}(?:[-\s]\d{4})?$" ...>
{% endhighlight %}

##### Common regular expression patterns

<table class="table-2 tc-heavyright">
  <thead>
    <tr>
      <th data-th="Description">Description</th>
      <th data-th="Regular expression">Regular expression</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Description">Postal address</td>
      <td data-th="Regular expression"><code>[a-zA-Z\d\s\-\,\#\.\+]+</code></td>
    </tr>
    <tr>
      <td data-th="Description">Zip Code (US)</td>
      <td data-th="Regular expression"><code>^\d{5,6}(?:[-\s]\d{4})?$</code></td>
    </tr>
    <tr>
      <td data-th="Description">IP Address</td>
      <td data-th="Regular expression"><code>^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$</code></td>
    </tr>
    <tr>
      <td data-th="Description">Credit Card Number</td>
      <td data-th="Regular expression"><code>^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|6(?:011|5[0-9]{2})[0-9]{12}|(?:2131|1800|35\d{3})\d{11})$</code></td>
    </tr>
    <tr>
      <td data-th="Description">Social Security Number</td>
      <td data-th="Regular expression"><code>^\d{3}-\d{2}-\d{4}$</code></td>
    </tr>
    <tr>
      <td data-th="Description">North American Phone Number</td>
      <td data-th="Regular expression"><code>^(?:(?:\+?1\s*(?:[.-]\s*)?)?(?:\(\s*([2-9]1[02-9]|[2-9][02-8]1|[2-9][02-8][02-9])\s*\)|([2-9]1[02-9]|[2-9][02-8]1|[2-9][02-8][02-9]))\s*(?:[.-]\s*)?)?([2-9]1[02-9]|[2-9][02-9]1|[2-9][02-9]{2})\s*(?:[.-]\s*)?([0-9]{4})(?:\s*(?:#|x\.?|ext\.?|extension)\s*(\d+))?$</code></td>
    </tr>
  </tbody>
</table>

#### The `required` attribute

If the `required` attribute is present, then the field must contain a value before
the form can be submitted. For example, to make the zip code required, we'd
simply add the required attribute:

{% highlight html %}
<input type="text" required pattern="^\d{5,6}(?:[-\s]\d{4})?$" ...>
{% endhighlight %}

#### The `min`, `max` and `step` attributes

For numeric input types like number or range as well as date/time inputs, you
can specify the minimum and maximum values, as well as how much they should each
increment/decrement when adjusted by the slider or spinners.  For example, a
shoe size input would set a minumum size of 1 and a maximum size 13, with a step
of 0.5

{% highlight html %}
<input type="number" min="1" max="13" step="0.5" ...>
{% endhighlight %}

#### The `maxlength` attribute

The `maxlength` attribute can be used to specify the maximum length of an input or
textbox and is useful when you want to limit the length of information that the
user can provide. For example, if you want to limit a filename to 12 characters,
you can use the following.

{% highlight html %}
<input type="text" id="83filename" maxlength="12" ...>
{% endhighlight %}

#### The `novalidate` attribute

In some cases, you may want to allow the user to submit the form even if it
contains invalid input. To do this, add the `novalidate` attribute to the form
element, or individual input fields. In this case, all pseudo classes and
JavaScript APIs will still allow you to check if the form validates.

{% highlight html %}
<form role="form" novalidate>
  <label for="inpEmail">Email address</label>
  <input type="email" ...>
</form>
{% endhighlight %}

{% include modules/remember.liquid title="Remember" list=page.remember.provide-real-time-validation %}

### Use JavaScript for more complex real-time validation

When the built-in validation plus regular expressions aren't enough, you can use
the [Constrains Validation API](http://dev.w3.org/html5/spec-preview/constraints.html#constraint-validation),
a powerful tool for handling custom validation.  The API allows you to do things
like set a custom error, check whether an element is valid, and determine the
reason that an element is invalid:

<table class="table-2 tc-heavyright">
  <thead>
    <tr>
      <th data-th="API">API</th>
      <th data-th="Description">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="API"><code>setCustomValidity()</code></td>
      <td data-th="Description">Sets a custom validation message and the <code>customError</code> property of the <code>ValidityState</code> object to <code>true</code>.</td>
    </tr>
    <tr>
      <td data-th="API"><code>validationMessage</code></td>
      <td data-th="Description">Returns a string with the reason the input failed the validation test.</td>
    </tr>
    <tr>
      <td data-th="API"><code>checkValidity()</code></td>
      <td data-th="Description">Returns <code>true</code> if the element satisfies all of it's constraints, and <code>false</code> otherwise.</td>
    </tr>
    <tr>
      <td data-th="API"><code>validity</code></td>
      <td data-th="Description">Returns a <code>ValidityState</code> object representing the validity states of the element.</td>
    </tr>
  </tbody>
</table>

#### Set custom validation messages

If a field fails validation, use `setCustomValidity()` to mark the field invalid
and explain why the field didn't validate.  For example, a sign up form might
ask the user to confirm their email address by entering it twice.  Use the blur
event on the second input to validate the two inputs and set the appropriate
response.  For example:

{% include_code _code/order.html customvalidation javascript %}

#### Prevent form submission on invalid forms

Because not all browsers will prevent the user from submitting the form if there
is invalid data, you should catch the submit event, and use the `checkValidity()`
on the form element to determine if the form is valid.  For example:

{% include_code _code/order.html preventsubmission javascript %}

### Show feedback in real-time

It's helpful to provide a visual indication on each field that indicates whether
the user has completed the form properly before they've submitted the form.
HTML5 also introduces a number of new pseudo-classes that can be used to style
inputs based on their value or attributes.

<table class="table-2 tc-heavyright">
  <thead>
    <tr>
      <th data-th="Pseudo-class">Pseudo-class</th>
      <th data-th="Use">Use</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Pseudo-class"><code>:valid</code></td>
      <td data-th="Use">Explicitly sets the style for an input to be used when the value meets all of the validation requirements.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:invalid</code></td>
      <td data-th="Use">Explicitly sets the style for an input to be used when the value does not meet all of the validation requirements.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:required</code></td>
      <td data-th="Use">Explicitly sets the style for an input element that has the required attribute set.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:optional</code></td>
      <td data-th="Use">Explicitly sets the style for an input element that does not have the required attribute set.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:in-range</code></td>
      <td data-th="Use">Explicitly sets the style for a number input element where the value is in range.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:out-of-range</code></td>
      <td data-th="Use">Explicitly sets the style for a number input element where the value is out of range.</td>
    </tr>
  </tbody>
</table>

Validation happens immediately which means that when the page is loaded, fields
may be marked as invalid, even though the user hasn't had a chance to fill them
in yet.  It also means that as the user types, and it's possible they'll see the
invalid style while typing. To prevent this, you can combine the CSS with
JavaScript to only show invalid styling when the user has visited the field.

{% include_code _code/order.html invalidstyle css %}
{% include_code _code/order.html initinputs javascript %}

{% include modules/remember.liquid title="Important" list=page.remember.show-all-errors %}

## Simplify checkout with `requestAutocomplete`

While `requestAutocomplete` was designed to help users fill out any form, today
it's most common use is in eCommerce where shopping cart abandonment on the
mobile web [can be as high as
97%](http://seewhy.com/blog/2012/10/10/97-shopping-cart-abandonment-rate-mobile-devices-concern-you/).
Imagine 97% of people in a supermarket, with a cart brimming full of things that
they want, flipping their cart over and walking out.

{% include modules/takeaway.liquid list=page.key-takeaways.use-request-auto-complete %}

Rather than the site relying on a particular payment provider,
`requestAutocomplete` requests payment details (such as name, address and credit
card information) from the browser, which are optionally stored by the browser
much like other auto-complete fields.

### `requestAutocomplete` flow

The ideal experience will show the `requestAutocomplete` dialog instead of loading the
page that displays the checkout form. If all goes well, the user shouldn't see
the form at all.  You can easily add `requestAutoComplete` to existing forms
without having to change any field names.  Simply add the `autocomplete`
attribute to each form element with the appropriate value and add the
`requestAutocomplete()` function on the form element. The browser will handle
the rest.

<img src="imgs/rac_flow.png" class="center" alt="Request autocomplete flow">

{% include_code _code/rac.html rac javascript %}

The `requestAutocomplete` function on the `form` element indicates to the
browser that it should populate the form.  As a security feature, the function
must be called via a user gesture like a touch or mouse click. A dialog is then
displayed asking the user permission to populate the fields and which details
they want to populate it with.

{% include_code _code/rac.html handlerac javascript %}

Upon completion of `requestAutocomplete`, the function will either fire the
`autocomplete` event if it finished successfully, or `autocompleteerror` if
it was unable to complete the form.  If it completed successfully and the form
validates to your needs, simply submit the form and proceed to the final
confirmation.

{% include modules/remember.liquid title="Remember" list=page.remember.request-auto-complete-flow %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
