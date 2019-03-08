# Enable support for non-public Custom Post Type

By default, you can select only public post types in the Notification settings. To add a support for non-public post type you need to add it via a filter:

```php
add_filter( 'notification/settings/triggers/valid_post_types', function( $post_types ) {

	$post_types[] = get_post_type_object( 'non_public_post_type_slug' );

	return $post_types;

}, 10, 2 );
```

{% hint style="warning" %}
Not all Merge Tags will be working properly for the private post type, ie. the permalink tag.
{% endhint %}

