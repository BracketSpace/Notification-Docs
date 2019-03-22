# White label mode

One of the coolest Notification features is the white labeling. To put it in this mode you’ll need to call just one function:

```php
if ( function_exists( 'notification_whitelabel' ) ) {
	notification_whitelabel();
}
```

What it does is just removes all the default triggers. The fun part starts with the parameters you can use. See below:

```php
notification_whitelabel( [
	// admin page hook under which you want the Notifications to be displayed.
	'page_hook'       => 'edit.php?post_type=page',
	// if display extensions.
	'extensions'      => false,
	// if display settings.
	'settings'        => false,
	// control settings access, provided user IDs will have an access.
	// this works only if settings are enabled.
	'settings_access' => array( 123, 456 ),
] );
```

{% hint style="info" %}
If Notifications page is moved to a submenu of another page, the settings and extensions are added as a separate submenu.
{% endhint %}

## Adjusting Notification post type labels and capabilities

As easy as using two filters.

### Labels

```php
add_filter( 'notification/whitelabel/cpt/labels', function( $labels ) {

	// These are the defaults.
	return [
		'name'                => __( 'Notifications', 'notification' ),
		'singular_name'       => __( 'Notification', 'notification' ),
		'add_new'             => _x( 'Add New Notification', 'notification', 'notification' ),
		'add_new_item'        => __( 'Add New Notification', 'notification' ),
		'edit_item'           => __( 'Edit Notification', 'notification' ),
		'new_item'            => __( 'New Notification', 'notification' ),
		'view_item'           => __( 'View Notification', 'notification' ),
		'search_items'        => __( 'Search Notifications', 'notification' ),
		'not_found'           => __( 'No Notifications found', 'notification' ),
		'not_found_in_trash'  => __( 'No Notifications found in Trash', 'notification' ),
		'parent_item_colon'   => __( 'Parent Notification:', 'notification' ),
		'menu_name'           => __( 'Notifications', 'notification' ),
	];

} );
```

### Capabilities

```php
add_filter( 'notification/post_type/capabilities', function( $capabilities ) {

	// These are the defaults.
	return [
		'edit_post'          => 'manage_options',
		'read_post'          => 'manage_options',
		'delete_post'        => 'manage_options',
		'edit_posts'         => 'manage_options',
		'edit_others_posts'  => 'manage_options',
		'delete_posts'       => 'manage_options',
		'publish_posts'      => 'manage_options',
		'read_private_posts' => 'manage_options'
	];

} );
```

