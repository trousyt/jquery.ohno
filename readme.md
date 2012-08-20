jQuery.OhNo
===========

_Summary_: jQuery.OhNo is a simple client-side validation framework designed to make hooking into your DOM elements and validating them simple.

_Usage_:

1. Create a new instance of the OhNoValidation object.
2. Add validation checks by calling the addValidation method.
3. Call validate to start the validation.

A simple example:

	$(document).ready(function() {
		var v = new OhNoValidation();
		v.addValidation('#username', 'presence', { alias: 'Username', message: '{alias} must not be blank!' });
		v.addValidation('#password', 'presence', { alias: 'Password', message: 'You must fill in a password!' });

		v.bindForm('#form');
	});

Now you have set up validation on two fields and bound to the submit event of the page's form tag. Simple.

You also can have more control over how and when validation is fired. Simply calling validate() whenever you would like to validate is possible from whatever event you choose. 

To immediately receive the validation result when validation is complete, use the option 'afterValidated' by either setting it independently or including it upon object instantiation.

	var v = new OhNoValidation({ afterValidated: function(result) {
		alert('Validation returned '+result);
	}});

	v.setOption('afterValidated', function(result) {
		alert('Validation returned '+result);	// Returns boolean value of true or false
	});

_Custom Validators_:
Implementing custom validators is extremely simple. By calling the addValidatorFunction method, you can register your own. Only a few guidelines are necessary.

Your function must accept selector, name, and options (hash) and return a boolean value indicating the end-result.

The 'presence' validator is implemented like so:

	v.addValidatorFunction('presence', function(selector, name, options) {
		var trim = function(str) {
			return this.replace(/^[\t]+|[ \t]+$/g, '');
		};
		
		var el = $(selector);
		if (el) {
			var val = el.val();
			if(trim(el.val())) {
				return true;
			}
		}

		return false;
	});

Now we can use that custom function by specifying its name when adding a validation:

	v.addValidation('#username', 'presence');


