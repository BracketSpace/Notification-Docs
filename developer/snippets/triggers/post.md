# Post

## Post published - include private posts

```php
add_action( 'notification/trigger/registered', function( $trigger ) {

	if ( $trigger->get_slug() !== 'post/post/published' ) {
		return;
	}

	$trigger->add_action( 'new_to_private', 10 );
	$trigger->add_action( 'auto-draft_to_private', 10 );
	$trigger->add_action( 'draft_to_private', 10 );
	$trigger->add_action( 'pending_to_private', 10 );
	$trigger->add_action( 'future_to_private', 10 );

} );
```

## Post updated - add other post statuses

```php
add_filter( 'notification/trigger/wordpress/post/updated/statuses', function( $statuses, $post_type ) {
    if ( 'my-post-type' === $post_type ) {
        $statuses[] = 'on-hold';
    } 
    
    return $statuses;
}, 10, 2 );
```

