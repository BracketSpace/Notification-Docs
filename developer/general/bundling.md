# Bundling Notification plugin

Including Notification in your plugin or theme is really very simple. It can work as a library \(similar to Advanced Custom Fields or other plugins\).

One difference is that you don’t have to define anything. Just include the plugin’s _load.php_ file like this:

```php
require_once( 'path/to/plugin/notification/load.php' );
```

Notification will figure out its paths and URLs.

{% hint style="info" %}
When bundled, the Notification initializes on `init 4` to make sure it gets the priority. Notification loaded as a normal plugin is ignored.
{% endhint %}

