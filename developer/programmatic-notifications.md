# Programmatic Notifications

The notifications doesn't necessarly have to be saved in WordPress database nor loaded from JSON files. A good example is [dynamic trigger testing](snippets/general/automatic-trigger-testing.md) where all the notifications are created on the fly.

### Basic example

You can define the notification with a simple array. Below is a minimal example with all the required parameters.

```php
if ( function_exists( 'notification' ) ) :
notification( [
	'title'    => 'My programmatic notification', // For internal reference.
	'trigger'  => 'trigger_slug', // Trigger slug (can be a Triggerable object).
	'carriers' => [ // An array with format: carrier_slug => data array
		'email' => [
			'activated'  => true, // Must be true.
			'enabled'    => true, // Must be true.
			'subject'    => 'Email from ghost notification!', 
			'body'       => 'This is nice, {user_first_name}, huh?',
			'recipients' => [
				[
					'type'      => 'administrator',
					'recipient' => '',
				],
				[
					'type'      => 'email',
					'recipient' => '{user_email}',
				],
			],
		],
	],
	'enabled'  => true, // Must be true.
] );
endif;
```

{% hint style="info" %}
You can reference the Carrier fields by [checking the source code](https://github.com/BracketSpace/Notification/tree/master/class/Defaults/Carrier). You should check the `add_form_field` method calls which will contain the field slug and other useful info about the type.
{% endhint %}

### All arguments

All arguments available:

```php
if ( function_exists( 'notification' ) ) :
notification( [
	'hash'     => 'my_programmatic_notification', // Unique notification hash, automatically generated.
	'title'    => 'My programmatic notification',
	'trigger'  => 'trigger_slug',
	'carriers' => [
		'email' => [
			'activated'  => true,
			'enabled'    => true,
			'subject'    => 'Email from ghost notification!', 
			'body'       => 'This is nice, {user_first_name}, huh?',
			'recipients' => [
				[
					'type'      => 'administrator',
					'recipient' => '',
				],
				[
					'type'      => 'email',
					'recipient' => '{user_email}',
				],
			],
		],
	],
	'enabled'  => true,
	'extras'   => [], // Extra data array, ie. config for add-ons.
	'version'  => time(), // Version of the notification, should be a timestamp. Default: current time.
] );
endif;
```

