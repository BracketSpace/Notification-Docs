# Adding Merge Tags to existing Triggers

Sometimes it's needed to add your own Merge Tag to already defined Trigger. In example you can add a custom meta Merge Tag to default `Post Published` Trigger.

To do this simply hook into the action and add your Merge Tag:

```php
// Hook into an action when Merge Tags are attached to Trigger.
add_action( 'notification/trigger/merge_tags', function( $trigger ) {

	// Check if registered Trigger is the one you need.
	if ( 'post/post/updated' !== $trigger->get_slug() ) {
		return;
	}

	// Pay attention to the Tag type you are defining.
	// If you want to output an HTML, use HtmlTag instead.
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\StringTag( [
		'slug'     => 'new_merge_tag',
		'name'     => __( 'New Merge Tag', 'textdomain' ),
		'resolver' => function( $trigger ) {
			return get_post_meta( $trigger->post->ID, '_my_meta_key', true );
		},
	] ) );

} );
```

## Targeting all Post Type Triggers

You can target all the Post Type Triggers like this:

```php
add_action( 'notification/trigger/merge_tags', function( $trigger ) {

	if ( ! preg_match( '/post\/(.*)\/(updated|trashed|published|drafted|added|pending|scheduled)/', $trigger->get_slug() )
		return;
	}

	// Add your Tag.

} );
```

## Global Merge Tags

The Notification plugin also supports global Merge Tags which are added to all Triggers. You can use this nifty function to create one:

```php
notification_add_global_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\StringTag( [
	'slug'     => 'option_value',
	'name'     => __( 'Site title', 'textdomain' ),
	'resolver' => function( $trigger ) {
		return get_option( 'your_option_name', 'Default' );
	},
] ) );
```

{% hint style="warning" %}
Before using any property of the Trigger make sure it's avaible. Global Merge Tags are intended to be loosly connected with any Trigger.
{% endhint %}

