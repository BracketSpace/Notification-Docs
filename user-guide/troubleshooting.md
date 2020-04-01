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

{% page-ref page="advanced/custom-post-type-support.md" %}





