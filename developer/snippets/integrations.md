# Integrations

## Disable Gutenberg integration for specific Post Types

Useful when specific Post Type is enabled for REST but no Gutenberg is used to create the content.

```php
add_filter( 'notification/integration/gutenberg', function( $integration_enabled, $post_type, $trigger ) {
    if ( 'my-cpt' === $post_type ) {
        return false;
    }
    return $integration_enabled;
}, 10, 3 );
```

