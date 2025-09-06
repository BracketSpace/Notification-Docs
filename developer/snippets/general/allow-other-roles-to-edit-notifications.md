# Allow other roles to edit Notifications

&#x20;You can overwrite the Notification post type capabilities. [See the capabilities for specific roles](https://wordpress.org/support/article/roles-and-capabilities/).

In the example below, you are allowing everyone with an editor role or greater to manage the notifications.

```php
add_filter(
    'notification/post_type/capabilities',
    function($capabilities) {
        return [
            'edit_post' => 'publish_posts',
            'read_post' => 'publish_posts',
            'delete_post' => 'publish_posts',
            'edit_posts' => 'publish_posts',
            'edit_others_posts' => 'publish_posts',
            'delete_posts' => 'publish_posts',
            'publish_posts' => 'publish_posts',
            'read_private_posts' => 'publish_posts',
        ];
    }
);
```

{% hint style="danger" %}
Please note that the capability the user has to have is `unfiltered_html`. Otherwise, the notification configuration won't be saved properly.
{% endhint %}

