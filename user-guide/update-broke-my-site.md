---
description: Version 9.0.0 is not compatible with any of the free and premium add-ons!
---

# Update broke my site

It's very important to update the Notification plugin in a safe environment and with all the extensions **at the same time.**&#x20;

## My website is down

Sorry that it happened! Please make sure to always check the update notes before upgrading the plugin and backup your site before making any major changes like updates.

Your website is down because the new Notification version is not compatible with most of the extensions. We needed to upgrade our internal API for better performance and to reduce the tech-debt.

{% hint style="success" %}
To quickly restore your website please enable recovery mode (link was sent to the website admin email) and disable Notification plugin(s) or restore the website backup.
{% endhint %}

From here, you have two options to proceed.

### Upgrade all the extensions (recommended)

The new Notification version has also security patches, so we advise to upgrade everything as soon as possible.

If your website is up already, just upgrade all the extensions and reactivate the plugins. You can also find the latest plugin packages [on your store account](https://bracketspace.com/dashboard/).

### Downgrade to the previous Notification version

If you cannot update all the extensions or you don't want to do that, you can download the [Notification v8.0.15 package](https://downloads.wordpress.org/plugin/notification.8.0.15.zip) and downgrade it by going to Plugins -> Add New -> Upload Plugin.

## My customizations are not compatible anymore

If you extended the plugin with custom Triggers, Carriers, Recipients, or anything else, you need to update your code to the latest version.

Please refer to the changelog in readme.txt and the developer documentation here on how to use the new internal API.
