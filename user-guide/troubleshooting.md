---
description: Debug quickly why the plugin isn't working
---

# Troubleshooting

{% hint style="danger" %}
Make sure the Notification plugin and all the extensions are up-to-date!
{% endhint %}

## Nothing is sent

To debug the missing message \(Carrier execution\) please enable the Notification log in **Notification &gt; Settings &gt; Debugging**. All the executions will be caught there.

If the notification gets caught, you can inspect the details \(ie. if the recipient is set correctly\) and if they seem to be ok, check if your WordPress is sending the emails \(SMTP is set correctly?\) or it can connect to the API \(depends on the selected Carrier\).

If the notification is not there, you probably found a bug. Please [report it on Github](https://github.com/BracketSpace/Notification/issues/new?assignees=&labels=bug&template=bug-report.md&title=).

## Cannot see the Custom Post Type on the Triggers list while creating a Notification

See:

{% page-ref page="custom-post-type-support.md" %}

## WordPress Updates trigger is not sending any notification

The mechanism of this trigger relies on the WordPress Cron system \(periodic tasks executions\). If you are not getting the notifications please go to **Tools &gt; Site Health** screen and confirm you cannot see any issues with WP Cron.

You can also install our [Advanced Cron Manager](https://wordpress.org/plugins/advanced-cron-manager/) plugin to confirm if the cron job is running and execute it manually to test without waiting for another automatic execution. The event name is: `notification_check_wordpress_updates`.

If after manual execution the notification is not sent, please apply the steps listed in [Nothing is sent](https://docs.bracketspace.com/notification/user-guide/troubleshooting#nothing-is-sent) chapter above.

