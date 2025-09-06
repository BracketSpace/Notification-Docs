---
description: Debug quickly why the plugin isn't working
---

# Troubleshooting

{% hint style="danger" %}
Make sure the Notification plugin and all the extensions are up-to-date!
{% endhint %}

## The Recipients field is empty

Notification plugin, since v7 uses WordPress' REST API to render the recipients field. You must ensure the `/notification` endpoint is accessible and the API is accessible. &#x20;

## Nothing is sent

To debug the missing message (Carrier execution) please enable the Notification log in **Notification > Settings > Debugging**. All the executions will be caught there.

{% hint style="warning" %}
Please make sure the notification suppressing checkbox is turned off if you wish to send the message to the public.&#x20;
{% endhint %}

If the notification gets caught, you can inspect the details (ie. if the recipient is set correctly) and if they seem to be ok, check if your WordPress is sending the emails (SMTP is set correctly?) or it can connect to the API (depends on the selected Carrier).

If the notification is not there, you probably found a bug. Please [report it on Github](https://github.com/BracketSpace/Notification/issues/new?assignees=\&labels=bug\&template=bug-report.md\&title=).

## Multiple Notifications are sent

Most of the time this is caused by the post editor saving the content multiple times. Ie. Gutenberg saves the main content in one request, taxonomy terms in another request, ACF saves the fields in another request, and so on.

Please activate the [Background Processing](advanced/background-processing.md) feature to prevent this from happening.

## Weird characters are being sent in the email

This might be related to the content encoding. You can try to define the email header (activate that in Notification -> Settings -> Carriers -> Email) as follows:

| Key          |                          |
| ------------ | ------------------------ |
| Content-Type | text/html; charset=UTF-8 |

## It shows an error with an invalid license, that expires today

If you experience this issue and you have a valid license, most likely you can see an empty license field on the Notification -> Extensions screen. In this case, simply deactivate the license and activate it again.

{% hint style="info" %}
If you have an expired Notification license you'd like to renew, contact us at support@bracketspace.com for a 20% discount.
{% endhint %}

## Cannot see the Custom Post Type on the Triggers list while creating a Notification

See:

{% content-ref url="advanced/custom-post-type-support.md" %}
[custom-post-type-support.md](advanced/custom-post-type-support.md)
{% endcontent-ref %}

## Storage templates base path: .../wp-content/plugins/notification/src/templates must exist and be a directory

This error will most likely occur in tandem with: `Warning: ftp_nlist() expects parameter 1 to be resource, null given`

To make sure the plugin works, please add the following to your `wp-config.php`:

```php
if (!defined('FS_METHOD')) define('FS_METHOD', 'direct');
```
