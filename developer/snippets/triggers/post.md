# Post

## Post published - include private posts

```php
add_action(
    'notification/trigger/registered',
    function($trigger) {
        if ($trigger->getSlug() !== 'post/post/published') {
            return;
        }

        $trigger->addAction('new_to_private', 10);
        $trigger->addAction('auto-draft_to_private', 10);
        $trigger->addAction('draft_to_private', 10);
        $trigger->addAction('pending_to_private', 10);
        $trigger->addAction('future_to_private', 10);
    }
);
```

## Post updated - add other post statuses

```php
add_filter(
    'notification/trigger/wordpress/post/updated/statuses',
    function($statuses, $postType) {
        if ($postType === 'my-post-type') {
            $statuses[] = 'on-hold';
        } 
        
        return $statuses;
    },
    10,
    2 
);
```
