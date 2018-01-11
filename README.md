# Validate.js [![Build Status](https://travis-ci.org/cferdinandi/validate.svg)](https://travis-ci.org/cferdinandi/validate)

Forked from [cferdinandi/validate](https://github.com/cferdinandi/validate)

A lightweight form validation script that augments native HTML5 form validation elements and attributes, providing a better user experience and giving you more control.

When a visitor leaves a field, Validate.js immediately validates the field and displays an error if applicable. It also validates the entire form on submit, and provides support for custom `onSubmit()` functions (for example, Ajax form submission).


<hr>

__*Included in this repo is a demo.html which contains a extensive form with all markup options, including translating default error messages and adding custom error messages per input.*__

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

To translate the default messages, you can overwrite them by adding this to your form:

```html
<form>
	<script>
		var messages = {
		    messageValueMissing: 'Dit veld is verplicht.',
		    messageValueMissingSelect: 'Kies een optie',
		    messageValueMissingSelectMulti: 'Kies een of meerdere opties',
		    messageTypeMismatchEmail: 'Vul een geldig e-mailadres in.',
		    messageTypeMismatchURL: 'Vul een geldige url in.',
		    messageTooShort: 'Deze tekst moet minstens {minLength} tekens bevatten. Je gebruikt nu maar {length} tekens.',
		    messageTooLong: 'Deze tekst mag maar {maxLength} tekens bevatten. Je gebruikt nu {length} tekens.',
		    messagePatternMismatch: 'Vul dit veld in volgens het aangegeven patroon.',
		    messageBadInput: 'Vul een geldig getal in.',
		    messageStepMismatch: 'Vul een geldig getal in zoals aangegeven.',
		    messageRangeOverflow: 'Deze waarde mag niet hoger zijn dan {max}.',
		    messageRangeUnderflow: 'Deze waarde mag niet lager zijn dan {min}.',
		    messageGeneric: 'Vul een geldige waarde in.',
		}
	</script>
	...
```

To add a custom message to an input, you add `data-error-[type of error]` to your input, followed by the error message. Like so:

```html
<input type="text" name="Name" class="form__group__input" data-error-valueMissing="Vul je naam in" required>
```

## License

The code is available under the [MIT License](LICENSE.md).
