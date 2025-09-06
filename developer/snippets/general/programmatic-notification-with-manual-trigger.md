---
description: >-
  Send the notification from the code, nothing needs to be configured in the
  Dashboard.
---

# Programmatic Notification with manual Trigger

To make it work you'll need:

* Custom Manual Trigger
* Notification definition
* Action to trigger the Notification

## Trigger

Let's define a simple Trigger without any Merge Tags.

```php
use BracketSpace\Notification\Abstracts;

add_action( 'notification/init', function() {

/**
 * Manual trigger class
 */
class ManualTrigger extends Abstracts\Trigger {

	/**
	 * Constructor
	 */
	public function __construct() {

		parent::__construct(
			'support/manual_trigger',
			'Manual Trigger'
		);


		$this->add_action( 'notification_manual_trigger_348m7t5', 10 );

		$this->set_group( 'Support' );

		$this->set_description( 'Triggered with notification_manual_trigger_348m7t5 action.' );

	}

	/**
	 * Action callback
	 *
	 * @return void
	 */
	public function action() {
		// This trigger should always process.
	}

	/**
	 * Merge Tags
	 *
	 * @return void
	 */
	public function merge_tags() {
		// This trigger doesn't include any Merge Tags.
	}

}

} );
```

You need to wrap the class definition with `notification/init` action, because [this is the earliest the abstract classes are accessible](../../general/plugin-loading-chain.md).

{% hint style="info" %}
Read more about [Custom Triggers](../../triggers/custom-trigger.md)
{% endhint %}

## Notification

The notification is just a function call with a configuration array. We'll register the Notification along with the Trigger.

```php
use BracketSpace\Notification\Register;

add_action( 'notification/init', function() {
	$manual_trigger = new ManualTrigger;

	Register::trigger( $manual_trigger );

	notification( [
		'hash'     => 'notification_manual_trigger_348m7t5',
		'title'    => 'Notification manual trigger',
		'trigger'  => $manual_trigger,
		'carriers' => [
			'email' => [
				'activated'  => true,
				'enabled'    => true,
				'subject'    => 'Manual trigger test',
				'body'       => 'Hello from the other side!',
				'recipients' => [
					[
						'type'      => 'administrator',
						'recipient' => '',
					],
				],
			],
		],
		'enabled'  => true,
		'extras'   => [],
		'version'  => time(),
	] );
} );
```

In this example, we using a simple email Carrier, but you are free to use any other Carrier registered within the Notification plugin. The easiest way to get the Carrier configuration is to set it up in WordPress Dashboard and just export the Notification to JSON. The JSON file will have all the keys you need to configure here.&#x20;

{% hint style="info" %}
Read more about [Programmatic Notifications](../../notifications/programmatic-notifications.md)
{% endhint %}

## Action

Our Trigger uses `notification_manual_trigger_348m7t5` action hook, so the only one thing left is to call it somewhere. The simplest would be:

```php
do_action( 'notification_manual_trigger_348m7t5' );
```

It can be convenient to wrap this with a simple `$_GET` param check.

```php
add_action( 'init', function() {
	if ( isset( $_GET['i3m84ty'] ) ) {
		do_action( 'notification_manual_trigger_348m7t5' );
	}
} );
```

And call it like this: `example.com?i3m84ty`&#x20;
