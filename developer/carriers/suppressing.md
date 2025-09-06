---
description: How to disable the Carrier process on the fly
---

# Suppressing the Carrier

{% hint style="info" %}
To disable the whole Notification (all Carriers) it's better to use the `notification/should_send` filter.
{% endhint %}

If you want to suppress a specific Carrier you can do it like this:

```php
add_action( 'notification/carrier/pre-send', function( $carrier, $trigger, $notification ) {

	if ( $carrier->get_slug() == 'email' ) {
		$carrier->suppress();
	}

}, 10, 3 );
```

{% hint style="info" %}
You can target any Carrier or Trigger property in this action to test your conditions.
{% endhint %}

