# Background processing

The background processing feature allows you to process the carriers in the background, using WP Cron feature. This means while doing an action with should trigger the notification, instead waiting for the process to finish \(and ie. send 100k emails\) the action is loaded in the cron, and executed in the next cron call.

It's particularly helpful to distribute the server load but it also resolves the Gutenberg issue, where wrong custom fields or taxonomies were included in the notification.

To enable this feature navigate to Notification -&gt; Settings and in Advanced section, check the **Background processing** checkbox. From now on, the actions will be executed via cron.

{% hint style="warning" %}
Enabling this feature can cause a slight delay with the notification sending, up to a few minutes. This is because WP Cron is dependent on the website traffic, so the more visitors you have, the ealier it will be executed. You can hook it into the server task scheduler as well.
{% endhint %}

