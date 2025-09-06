# Custom Carrier

Carrier is an element which connects the WordPress action with a service. Default Carriers are Email and Webhook.

If you want to connect with API or other delivery service, you should create a custom Carrier.

Carriers very often needs the [Recipients](../recipients/custom-recipient.md), so you may want to add a custom one as well.

## Carrier class

```php
use BracketSpace\Notification\Interfaces\Triggerable;
use BracketSpace\Notification\Abstracts;
use BracketSpace\Notification\Defaults\Field;

/**
 * ExampleCarrier Carrier
 */
class ExampleCarrier extends Abstracts\Carrier {

	/**
	 * Carrier icon, optional
	 *
	 * @var string SVG
	 */
	public $icon = '<svg>...</svg>';

	/**
	 * Carrier constructor
	 */
	public function __construct() {
		// Provide the slug and translatable name.
		parent::__construct( 'example-carrier', __( 'Example Carrier', 'textdomain' ) );
	}

	/**
	 * Used to register Carrier form fields
	 * Uses $this->add_form_field();
	 *
	 * @return void
	 */
	public function form_fields() {

		$this->add_form_field( new Field\InputField( [
			'label' => __( 'Example field', 'notification' ),
			'name'  => 'fieldslug',
		] ) );

		// Special field which renders all Carrier's recipients.
		// You may override name, slug and description here.
		$this->add_recipients_field( [
			'name' => 'Items',
			'slug' => 'items',
		] );

	}

	/**
	 * Sends the notification
	 *
	 * @param  Triggerable $trigger trigger object.
	 * @return void
	 */
	public function send( Triggerable $trigger ) {
		// Data contains the user data with rendered Merge Tags.
		$data = $this->data;

		// Parsed recipients are also available.
		$data['parsed_recipients'];

		// This is where you should connect with your service to send out the Notifiation.
	}

}
```

## Registering the Carrier

To get the Carrier registered you must create an instance of your class and pass it to the Notification plugin. The best action to do that is `notification/init`.

```php
use BracketSpace\Notification\Register;

add_action( 'notification/init', function() {
    Register::carrier( new ExampleCarrier() );
} );
```
