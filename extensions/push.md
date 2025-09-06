---
description: Version 1.0.0 or later
---

# Push

{% hint style="success" %}
[Download this extension](https://bracketspace.com/downloads/notification-push/)
{% endhint %}

### First-time configuration

After installing and activating the plugin you have to generate VAPID Keys. They are used to authorize Subscribers, and without them, the integration will not work.

Click the link in admin notification or head over to Settings -> Carriers -> Push.

![](../.gitbook/assets/image\(1\).png)

Next, press Generate button and Save changes.

![](../.gitbook/assets/image\(2\).png)

### Plugin configuration

#### Permission Pop-Up mode

By default pop-up asking for permission to receive Push Notifications will be shown after clicking the "Subscribe" button (Manual mode). You can change it to show a pop-up to Users immediately after the first click on the page (Automatic mode).

#### Subscribing by logged-in Users

To gain more control over subscriptions you can check the option, that only logged-in users can subscribe to receive Push Notifications. This mode is recommended if you want to send more personal Notifications, e.g. about changing order status.

### The "Subscribe" button

You can display the "Subscribe" button on any of your pages using `[notification-push-subscribe-button]` Shortcode. You can customize it with several attributes:

* `id` - set the id attribute to the button
* `class` - set the additional classes to the button
* `label` - set the text of the button
* `granted_label` - set the text of the button if permission is already granted
* `denied_label` - set the text of button if permission was revoked

You can also use the following code to display the button from PHP:

```php
use BracketSpace\Notification\Push\Frontend\SubscibeButton;

SubscibeButton::render();
```

The "Subscribe" button is available to be used in both Manual and Automatic mode.

### Managing subscriptions

There is no way to determine who is the subscriber if a subscription is not connected with the user. This situation can happen if the `Subscribing by logged-in Users` option is not checked. In this case, the site administrator cannot remove every user subscription on their demand. Fortunately, users can revoke permission by themselves:

* Mozilla Firefox instruction: [https://support.mozilla.org/en-US/kb/push-notifications-firefox#w\_how-do-i-revoke-web-push-permissions-for-a-specific-site](https://support.mozilla.org/en-US/kb/push-notifications-firefox#w_how-do-i-revoke-web-push-permissions-for-a-specific-site)
* Google Chrome instruction: [https://support.google.com/chrome/answer/3220216](https://support.google.com/chrome/answer/3220216)

You can see user subscriptions on the user list in the admin dashboard.

![](../.gitbook/assets/image\(3\).png)

In the user edit view, you can see details about its subscriptions, or remove any of them separately.

![](../.gitbook/assets/image\(4\).png)

### Notification Recipients

There are two plugin-specific recipients

#### Every subscriber

This Recipient will try to send Notification to every subscriber, no matter if they are connected with a specific user or not.

#### User

This Recipient will try to send Notification to every browser in which the given user subscribed for receiving notifications. The list shows users which are subscribed at least once.
