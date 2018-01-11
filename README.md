# Validate.js [![Build Status](https://travis-ci.org/cferdinandi/validate.svg)](https://travis-ci.org/cferdinandi/validate)

Forked from [cferdinandi/validate](https://github.com/cferdinandi/validate)

A lightweight form validation script that augments native HTML5 form validation elements and attributes, providing a better user experience and giving you more control.

When a visitor leaves a field, Validate.js immediately validates the field and displays an error if applicable. It also validates the entire form on submit, and provides support for custom `onSubmit()` functions (for example, Ajax form submission).


<hr>


## Getting Started

Everything you need is already in the Hybrid Framework. In total, it consists of 4 things:
1. _Frontend/js/vendor/validate.js_  
This is the main validation script.

2. _Frontend/js/vendor/validityState-polyfill.js_  
This is a polyfill which makes sure this method works in all modern browsers, and (mostly) IE10 and above.

3. _Frontend/js/form-validation.js_  
This contains an init method with a few options. 

4. _The form itself_  
This is probably the only thing you have to alter.  

### Building the form(markup)

Add the `required` attribute to required fields. Use `type="email"` and `type="url"` for email addresses and URLs, respectively. Include `pattern` attributes, `min` and `max`, and so on to set validation criteria for your form fields. View a [full list of types and attributes on MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5/Constraint_validation#Intrinsic_and_basic_constraints).

```html
<div>
	<label for="email">Email</label>
	<input type="email" id="email" required>
</div>

<div>
	<label for="url">URL</label>
	<input type="url" id="url" required>
</div>
```

If you're using validation patterns, you can also include a `title` with a custom validation message. This will display in the error message.

```html
<div>
	<label for="password">Password (At least 1 uppercase character, 1 lowercase character, and 1 number)</label>
	<input type="password" id="password" value="" title="Please choose a password that includes at least 1 uppercase character, 1 lowercase character, and 1 number." pattern="^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?!.*\s).*$" required>
</div>
```

#### hasError()
Check if a field has a validation error.

```javascript
validate.hasError(
	field, // The field to validate
	options // User settings, same as the ones passed in during validate.init() [optional]
);
```

**Example**

```javascript
var field = document.querySelector('[name="email"]');
var error = validate.hasError(field);

if (error) {
	// Do something...
}
```

#### showError()
Show an error message on a field.

```javascript
validate.showError(
	field, // The field to show an error message for
	error, // The error message to show
	options // User settings, same as the ones passed in during validate.init() [optional]
);
```

**Example 1: Write your own error**

```javascript
var field = document.querySelector('[name="email"]');
var error = 'This field is wrong, dude!';
validate.showError(field, error);
```

**Example 2: Using `hasError()`**

```javascript
var field = document.querySelector('[name="url"]');
var error = validate.hasError(field);
validate.showError(field, error);
```

#### removeError()
Remove the error message from a field.

```javascript
/**
 * Remove an error message from a field
 * @public
 * @param  {Node}   field   The field to remove the error from
 * @param  {Object} options User options
 */
validate.removeError(
	field, // The field to remove the error from
	options // User settings, same as the ones passed in during validate.init() [optional]
);
```

**Example**

```javascript
var field = document.querySelector('[name="email"]');
validate.removeError(field);
```

#### destroy()
Destroy the current `validate.init()`. Removes all errors and resets the DOM. This is called automatically during the `init` function to remove any existing initializations.

```javascript
validate.destroy();
```

## License

The code is available under the [MIT License](LICENSE.md).
