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
