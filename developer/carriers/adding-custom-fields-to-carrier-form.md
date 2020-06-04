# Adding custom fields to Carrier form

To add new fields to Carrier form you need to hook into the `notification/carrier/registered` action.

```php
add_action( 'notification/carrier/registered', function( $carrier ) {

	if ( 'email' === $carrier->get_slug() ) {
		return;
	}

	$carrier->add_form_field( new BracketSpace\Notification\Defaults\Field\InputField( array(
		'label'      => __( 'Example Field' ),
		'name'       => 'example',
		'resolvable' => true,
	) ) );

} );
```

{% hint style="info" %}
All the field data will be automatically stored and available in `$carrier->data` property in `send()` method.
{% endhint %}

