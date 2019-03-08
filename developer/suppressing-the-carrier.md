# Suppressing the Carrier

If you want to suppress the Carrier from an external script, you can do it with an action:

```php
add_action( 'notification/carrier/pre-send', function( $carrier, $trigger ) {

	if ( $carrier->get_slug() == 'email' ) {
		$carrier->suppress();
	}

}, 10, 2 );
```

{% hint style="info" %}
You can target any Carrier or Trigger property in this action.
{% endhint %}

