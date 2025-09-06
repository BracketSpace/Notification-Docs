# Custom Recipient

The [Recipient](../general/extension-possibilities.md#recipient) API is meant to provide a unified interface for Carriers. You don't have to use them but it's the best to keep the logic separated.

As an example, default Email Carrier registers a couple of Recipients - User selected from a list, Role, Administrator, Plain text email, etc. They all resolves to a flat array of emails. The Webhook provider registers URL recipients: GET, POST, PUT etc.

Your Custom Recipient may allow to select User from a dropdown and parse list of all selected Users to some kind of UUID, the one which is understood by your [Custom Carrier](../carriers/custom-carrier.md).

## Recipient class

```php
use BracketSpace\Notification\Abstracts;
use BracketSpace\Notification\Defaults\Field;

/**
 * ExampleRecipient Recipient
 */
class ExampleRecipient extends Abstracts\Recipient {

	/**
	 * Constructor
	 */
	public function __construct() {
		parent::__construct( [
			'slug'          => 'recipient_slug',
			'name'          => __( 'Recipient', 'textdomain' ),
			'default_value' => 'default',
		] );
	}

	/**
	 * Parses raw recipient value to something consumable by the Carrier.
	 *
	 * @param  string $value Raw value saved by the user.
	 * @return array         Array of resolved values
	 */
	public function parse_value( $value = '' ) {

		if ( empty( $value ) ) {
			$value = [ $this->get_default_value() ];
		}

		$value = do_something_with_the_value( $value );

		// Keep in mind you should return an array here.
		// This is because you may select a recipient which parses to multiple values.
		// Example: User Role recipient may parse to multiple emails.
		return [ $value ];

	}

	/**
	 * Prints the Recipient field.
	 *
	 * @return Field
	 */
	public function input() {

		// You should build an array of options here if you are using SelectField field.
		$opts = [
			'recipient1' => __( 'Recipient 1', 'textdomain' ),
			'recipient2' => __( 'Recipient 2', 'textdomain' ),
		];

		// You can use other fields as well.
		return new Field\SelectField( [
			'label'     => __( 'My Recipient', 'textdomain' ),
			'name'      => 'recipient',       // Don't change this.
			'css_class' => 'recipient-value', // Don't change this.
			'value'     => $this->get_default_value(),
			'pretty'    => true,
			'options'   => $opts,
		] );

	}

}
```

## Registering the Recipient

{% hint style="info" %}
Since version 8.0.0, recipients can be registered anytime on `notification/init` action and it doesn't matter if it's before or after the Carrier is registered.
{% endhint %}

```php
use BracketSpace\Notification\Register;

add_action( 'notification/init', function() {
    // You need to provide the Carrier slug.
    Register::recipient( 'carrier-slug', new ExampleRecipient() );
} );
```
