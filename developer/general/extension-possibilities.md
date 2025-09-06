# Extension possibilities

The Notification plugin has a great, powerful developer API which allows you to extend it nearly limitless.

Take a look at [plugin’s repository at Github](https://github.com/BracketSpace/Notification/tree/master) to search for actions and filters you can use, but also to see how the default things are registered.

## Modular components

### Carrier

By default, plugin supports the Email and Webhook carriers, but it can be anything. You can even send real paper letters with it as long as you have service provider and API access for it.

The best part is that you can create any form fields, including repeatable fields. All using very simple internal API.

{% content-ref url="../carriers/custom-carrier.md" %}
[custom-carrier.md](../carriers/custom-carrier.md)
{% endcontent-ref %}

### Trigger

The trigger is a class which handles the action you want to hook in. Because it utilizes the WordPress actions system, you can hook up to anything you want! Even a page refresh, but this would probably kill your server.

{% content-ref url="../triggers/custom-trigger.md" %}
[custom-trigger.md](../triggers/custom-trigger.md)
{% endcontent-ref %}

### Merge Tag

This is a tiny bit of code which replaces things like `{this}` to `This`. With them, you can create dynamic parts of the Notification. An example is `{post_permalink}` Merge Tag used in _Post published_ Trigger.

There are few very basic Merge Tag types, like String, Integer, URL etc. but we have also more specific ones, like User Email. You can use them too!

The configuration couldn’t be simpler. You just have to define a property with needed information in the Trigger class and that’s it.

If you wish to add some more Merge tags to existing Triggers – that’s not a problem.

If you wish to add completely new Merge tags – that’s not a problem too.

{% content-ref url="../triggers/adding-merge-tags-to-existing-triggers.md" %}
[adding-merge-tags-to-existing-triggers.md](../triggers/adding-merge-tags-to-existing-triggers.md)
{% endcontent-ref %}

### Recipient

The recipient is also represented by a class. It’s not obligatory to use them with any custom Notification, but it’s highly recommended to keep unified interface of the plugin.

Also, it provides a value parser which automatically changes saved values to values which are understood by your Notification. For example, the Email Notification has Recipients. In the database, we are storing user IDs and with Recipient class they are automatically changed to an email address.

{% content-ref url="../recipients/custom-recipient.md" %}
[custom-recipient.md](../recipients/custom-recipient.md)
{% endcontent-ref %}

## Summary

I hope this will give you a nice idea how you can extend Notification plugin by yourself.

In the WordPress admin, we have also an Extensions screen. We’ll be happy to put your extensions there!
