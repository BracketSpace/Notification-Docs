---
description: Disable all the Carriers at once
---

# Suppressing the Notification

This is the best approach if you have to test the specific Notification, instead of a single Carrier.

To do this, you should use the filter:

```php
add_filter( 'notification/should_send', function( $should_send, $notification, $trigger ) {
	
	if ( $something ) {
		$should_send = false;
	}
	
	return $should_send;
	
}, 10, 3 );
```

{% hint style="danger" %}
At this point, the Trigger doesn't executed the action\(\) method so you cannot use the Merge Tags.
{% endhint %}

