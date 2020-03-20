---
description: >-
  Useful with AJAX requests or when you have to wait for the data to be saved in
  database
---

# Delaying Trigger execution with Cron

First, you have to hook into your desired action. This is not the action added to Trigger.

```php
// Delay the execution with cron.
add_action( 'your_desired_triggering_action', function() {

	$event_name   = 'ntfn_your_desired_triggering_action_proxy';
	$proxy_params = [ '1', 'param2_value' ];

	if ( ! wp_next_scheduled( $event_name, $proxy_params ) ) {
		wp_schedule_single_event( time() + 5, $event_name, $proxy_params );
	}

}, 10, 1 );
```

This action registers a single cron even, executed after 5 seconds. Be sure to pass along all the params you need to identify the action.

Then, create the proxy action, called from cron, in which you call the real trigger action. Make sure here to compose all the parameters the Trigger's`action` method need.

```php
// Cron proxy action.
add_action( 'ntfn_your_desired_triggering_action_proxy', function( $param1, $param2 ) {
	$post = get_post( $param1 );
	do_action( 'action_registered_in_trigger', $post, $param2 );
}, 10, 2 );
```

