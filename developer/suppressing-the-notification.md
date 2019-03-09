---
description: How to disable the Notification submission on the fly
---

# Suppressing the Notification

To disable the whole Notification \(all Carriers\) you really have to disable each Carrier separately. The action below will be called for each enabled Carrier for a specific Notification.

```php
add_action( 'notification/carrier/pre-send', function( $carrier, $trigger ) {
	$carrier->suppress();
}, 10, 2 );
```

If you want to suppress a specific Carrier you can do it like this:

```php
add_action( 'notification/carrier/pre-send', function( $carrier, $trigger ) {

	if ( $carrier->get_slug() == 'email' ) {
		$carrier->suppress();
	}

}, 10, 2 );
```

{% hint style="info" %}
You can target any Carrier or Trigger property in this action to test your conditions.
{% endhint %}

