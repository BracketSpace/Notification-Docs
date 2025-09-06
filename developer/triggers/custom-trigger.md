# Custom Trigger

New, custom triggers can be easily registered in your plugin or theme. All you need is a simple class declaration and a function call.

The Trigger is really only a wrapper for WordPress' action(s).&#x20;

## Trigger class

Have a look at the example Trigger class.

```php
use BracketSpace\Notification\Abstracts\Trigger as AbstractTrigger;

/**
 * Custom trigger class
 */
class CustomTrigger extends AbstractTrigger {

	/**
	 * Constructor
	 */
	public function __construct() {

		// 1. Slug, can be prefixed with your plugin name.
		// 2. Title, should be translatable.
		parent::__construct(
			'myplugin/custom_trigger',
			__( 'Custom Trigger title', 'textdomain' )
		);

		// 1. Action hook.
		// 2. (optional) Action priority, default: 10.
		// 3. (optional) Action args, default: 1.
		// It's the same as add_action( 'any_action_hook', 'callback', 10, 2 ) with
		// only difference - the callback is always context() method (see below).
		$this->add_action( 'any_action_hook', 10, 2 );

		// 1. Trigger group, should be translatable.
		// This is optional, Group is displayed in the Trigger select.
		$this->set_group( __( 'My Triggers', 'textdomain' ) );

		// 1. Trigger description, should be translatable.
		// This is optional, Description is displayed in the Trigger select.
		$this->set_description(
			__( 'Fires when a page with "myparam" parameter is visited', 'textdomain' )
		);

	}

	/**
	 * Assigns action callback args to object
	 * Return `false` if you want to abort the trigger execution
	 *
	 * You can use the action method arguments as usually.
	 *
	 * @return mixed void or false if no notifications should be sent
	 */
	public function context( $param_one, $param_two ) {

		/**
		 * This is a method callback hooked to the action you've added in the Constructor.
		 *
		 * Two important things which are happening here:
		 * - $this->callback_args is a numeric array containing all the callback parameters
		 *   if you want to treat them as an array
		 * - if you want to abort Trigger execution, you must return false here
		 */

		// If the second parameter ($process in our action) is false then abort, no carriers will be processed.
		if ( false === $param_two ) {
			return false;
		}

		// We can assign any property here, whole object will be accessible in Merge Tag resolver.
		$this->param_value = $param_one;

	}

	/**
	 * Registers attached merge tags
	 *
	 * @return void
	 */
	public function merge_tags() {

		/**
		 * In this method you can assign any Merge Tags to the trigger.
		 *
		 * To see what Merge Tags are available go to Notification plugin's core
		 * and look in class/Defaults/MergeTag directory.
		 */

		$this->add_merge_tag( new \BracketSpace\Notification\Defaults\MergeTag\StringTag( [
			// Slug (required), this will be used as {parametrized_url} value.
			// Don't translate this.
			'slug'        => 'parametrized_url',
			// Name (required), should be translatable.
			'name'        => __( 'Parametrized URL', 'textdomain' ),
			// Resolver (required), this can be a closure like below or function name
			// like: 'parametrized_url_resolver' or array( $this, 'parametrized_url_resolver' ).
			'resolver'    => function( $trigger ) {
				// Trigger object is available here,
				// with all the properties you set in action() method.
				return add_query_arg( 'source', $trigger->param_value, site_url() );
			},
			// Description (optional), should be translatable, default: ''.
			'description' => __( 'Homepage URL with ?source= param', 'textdomain' ),
			// Example indicator (optional)
			// if true, then description will have "Example" label, default: false.
			'example'     => true,
		] ) );

	}

}
```

### Lazy loading Trigger params

When the Trigger is registered or defined, it's too early to pull data of WordPress components like Post Types or Taxonomies. In such case, you can lazy load the name, description and group - these get's evaluated only for the editing purposes.

Instead of defining all the params in constructor, create getter methods. An example for Post Trigger:

```php
use BracketSpace\Notification\Abstracts\Trigger as AbstractTrigger;

/**
 * Custom trigger class
 */
class CustomTrigger extends AbstractTrigger {

	/**
	 * Post Type slug
	 *
	 * @var string
	 */
	public $post_type;

	/**
	 * Constructor
	 *
	 * @param string $post_type optional, default: post.
	 */
	public function __construct( $post_type = 'post' ) {
		$this->post_type = $post_type;

		$this->add_action( 'any_action_hook', 10, 2 );
	}

	/**
	 * Lazy loads the name
	 *
	 * @return string name
	 */
	public function get_name() : string {
		// translators: singular post name.
		return sprintf( __( '%s trigger', 'notification' ), WpObjectHelper::get_post_type_name( $this->post_type ) );
	}

	/**
	 * Lazy loads the description
	 *
	 * @return string description
	 */
	public function get_description() : string {
		return sprintf(
			// translators: 1. singular post name, 2. post type slug.
			__( 'Fires when %1$s (%2$s) is processed', 'notification' ),
			WpObjectHelper::get_post_type_name( $this->post_type ),
			$this->post_type
		);
	}
	
	/**
	 * Lazy loads group name
	 *
	 * @return string|null Group name
	 */
	public function get_group() {
		return WpObjectHelper::get_post_type_name( $this->post_type );
	}

	/**
	 * @return false|void False if no notifications should be sent
	 */
	public function context() {
		// Context setup.
	}

	/**
	 * Registers attached merge tags
	 *
	 * @return void
	 */
	public function merge_tags() {
		// Merge Tags.
	}

}
```

## Registering the Trigger

Having this class is only a first step. To get the trigger registered you must create an instance of this class and pass it to the Notification plugin. The best action to do that is `notification/init`

```php
use BracketSpace\Notification\Register;

add_action( 'notification/init', function() {
    Register::trigger( new CustomTrigger() );
} );
```
