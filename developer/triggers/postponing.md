# Postponing the Trigger action

Action postpone is very useful in some scenarios. It allows you to test some conditions in an earlier action and execute the Trigger in a later one.

## Postponed Trigger

Let’s take a look at an example:

```php
class CustomTrigger extends BracketSpace\Notification\Abstracts\Trigger {

	/**
	 * Constructor
	 */
	public function __construct() {

		parent::__construct(
			'myplugin/custom_trigger',
			__( 'Custom Trigger title', 'textdomain' )
		);

		// We are registering our ealier action with 2 arguments.
		$this->add_action( 'earlier_action', 10, 2 );

	}

	/**
	 * Assigns action callback args to object
	 * Return `false` if you want to abort the trigger execution
	 *
	 * @return mixed void or false if no notifications should be sent
	 */
	public function action( $param, $another_param ) {

		$this->this = $param;
		$this->that = $another_param;

		// Postpone this action to a later hook.
		$this->postpone_action( 'later_action', 10, 1 );

	}

}
```

As you can see we can set any properties in ealier action and execute the trigger later.

## Postponed action callback

What if you need another callback argument, passed to the later action? You can use the second method:

```php
/**
 * Postponed action callback
 *
 * Return `false` if you want to abort the trigger execution
 *
 * @return mixed void or false if no notifications should be sent
 */
public function postponed_action( $later_action_param ) {

	// we have access to the new callback args here.
	$this->from_later_action = $later_action_param;

	// you can also abort in the later action by returning false.
	if ( $this->from_later_action === false ) {
		return false;
	}

}
```

## Troubleshooting

### **Postponed trigger is executed twice**

Sometimes an action is done recursively. In this case you have to bail in the _postponed\_action_ callback if the action has been already done:

```php
public function postponed_action() {

	// Fix for the action being called recursively.
	if ( did_action( 'postponed_action_hook_name' ) ) {
		return false;
	}

}
```

