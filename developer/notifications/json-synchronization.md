---
description: >-
  Synchronize all the Notifications by saving them within the theme or plugin
  files.
---

# JSON synchronization

This is very similar how Advanced Custom Fields JSON synchronization works. Whenever you save the  notification in wp-admin the JSON file with all the config is saved within the directory you specified. It works the other way around as well - if you don't have the notification in your WordPress database, you can pull it from the file.

The notification is sent even if it's just in the file and not in the database, so you can import it just for editing purposes.

### Default usage

```php
use BracketSpace\Notification\Core\Sync;

add_action( 'notification/init', function () {
	Sync::enable();
}, 5 );
```

You can put this code in your custom plugin or in your child theme's functions.php file.

Bu default, all the notification will be saved within the `wp-content/themes/$theme/notifications/` directory.

### Custom notifications directory

You can put the notifications in a custom directory if you like, just pass the **full path** in the parameter.

To put the notifications within the `wp-content/uploads` directory do it like this:

```php
use BracketSpace\Notification\Core\Sync;

add_action( 'notification/init', function () {
    $uploads_dir = wp_upload_dir();
    Sync::enable( $uploads_dir['basedir'] );
}, 5 );
```

{% hint style="info" %}
The Notification plugin supports only one synchronization directory
{% endhint %}
