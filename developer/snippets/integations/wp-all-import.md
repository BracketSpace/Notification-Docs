# WP All Import

## Importing posts

By default, WP All Import plugin will trigger the actions twice for each post imported.

{% hint style="warning" %}
This guide assumes that you have the option "**Increase speed by disabling do\_action calls in wp\_insert\_post during import.**" checked, in the Import settings in Advanced Options tab.
{% endhint %}

{% hint style="warning" %}
You must use `Post added` trigger for this integration (or other `Custom Post Type added` trigger) or `Post updated` trigger.
{% endhint %}

```php
// Add our proxy action to the trigger.
add_action( 'notification/trigger/registered', function( $trigger ) {

	if ( preg_match( '/post\/(.*)\/added/', $trigger->get_slug() ) ) {
		$trigger->add_action( 'notification_pmxi_added_post', 10, 3 );
	}

	if ( preg_match( '/post\/(.*)\/updated/', $trigger->get_slug() ) ) {
		$trigger->add_action( 'notification_pmxi_updated_post', 10, 3 );
	}

} );

// Proxy action.
add_action( 'pmxi_saved_post', function( $post_id, $node, $is_update ) {
	if ( ! $is_update ) {
		do_action( 'notification_pmxi_added_post', $post_id, get_post( $post_id ), false );
	} else {
		do_action( 'notification_pmxi_updated_post', $post_id, get_post( $post_id ), get_post( $post_id ) );
	}
}, 10, 3 );

// Disable postponing.
add_filter( 'notification/integration/gutenberg', function( $initial ) {
	if ( defined( 'WP_IMPORTING' ) && WP_IMPORTING ) {
		return false;
	}
	return $initial;
} );

add_filter( 'notification/integration/custom_fields/should_postpone_save_post', function( $initial ) {
	if ( defined( 'WP_IMPORTING' ) && WP_IMPORTING ) {
		return false;
	}
	return $initial;
} );
```
