# Known issues

## Multiple exactly the same Notifications

Problem occurs when Triggers gets executed multiple times during the same request, ie. when you are adding multiple posts via a loop.

This is related to the Notification plugin internal architecture and postponing feature. The plugin doesn't keep the action context and this is why so many same notifications is sent.

A quick fix to prevent that is to use below filter. Please note that if you are saving custom fields, they may not get recognized.

```php
add_filter( 'notification/integration/custom_fields/should_postpone_save_post', '__return_false' );
```

## Gutenberg and custom field

When using Gutenberg it's not possible to get every post information AND custom fields at the same time. Everything is saved separately in separate AJAX requests and there's no way we can access all the updated data at once.

