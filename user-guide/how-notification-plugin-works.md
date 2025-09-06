# How Notification plugin works

The [Notification plugin](https://wordpress.org/plugins/notification/) was created to connect various WordPress actions with another services. Its initial version only allowed to send Emails, but in current state you can connect with any 3rd party software.

The plugin is built on top of WordPress' actions system which means it can listen to any action defined in WordPress. And it has a thousand of them. Also, every properly created plugin should use them as well.

{% hint style="info" %}
Examples:

* Send an email to WordPress administrator when user logs in
* Send a webhook to your accounting software when someone purchases a product
{% endhint %}

## Plugin components

The Notification plugin is created with a few components which works together. See below how they work and how they are bound together.

### Trigger

The Trigger is a WordPress action(s) which are observed by the plugin. Examples:

* User registration
* Post publication
* Plugin update

It allows the plugin to listen to what is happening in the background.

{% hint style="info" %}
The Notification is highly extensible. Developers can register own Triggers based on any WordPress actions.
{% endhint %}

### Carrier

The Carrier delivers the Notification. Example Carriers:

* Email
* Webhook
* Slack message
* File Logger

All the Carriers works with all the Triggers out of the box, even the custom ones.

### Merge Tag

This is a tiny bit of a dynamic information. You can think of it as a placeholder. Example Merge Tags:

* `{user_email}`
* `{plugin_name}`
* `{post_title}`

You can compose the Notification out of them when you don't really know what's going to be rendered. For example when you create the "User registered" Notification and use the `{user_email}` Merge Tag it's going to be rendered to `your@email.com` when you register and to `bracketspace@email.com` when I register.

## How does it work together

Trigger, Carriers and Merge Tags are all ingredients of a yummy Notification pie you can bake.

A Notification is a single "action and reaction" chain. When this happens, do this. If this Trigger is triggered, execute these Carriers. If User registers, send an Email and Webhook.

Each Trigger has a set of it's Merge Tags. Having the `{plugin_name}` Tag in context of a User registration would be rather silly 😉

You can use these Marge Tags in any Carrier. Ie. use the `{user_email}` as the Email recipient but also send it in a `user.email` field in the Webhook.

The rule of thumb is - if you cannot see the Merge Tag in the sidebar, you cannot use it.
