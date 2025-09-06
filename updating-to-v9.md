# Updating to v9

{% hint style="danger" %}
Please note, that Notification v9 is not compatible with v8 add-ons and v9 add-ons are not compatible with Notification v8. If you're upgrading, please make sure to upgrade everything at once. &#x20;
{% endhint %}



## Most noticeable changes

The most noticeable changes to the new version of the Notification plugin are listed below.

### Custom database table

Notifications data were moved from the `wp_posts` table to the custom table in the database.

The code API within didn't change, so if you've been adjusting notifications via official methods, functions, or hooks, you're covered and don't have to change anything. &#x20;

### Coding standards

We dropped WP Coding Standards in favor of modern PSR-12. Multiple code APIs changed, mostly from snake\_case to camelCase, but for most of the functions and methods we offer a [casegnostic](https://github.com/micropackage/casegnostic) approach, they should be backward compatible.

### Webhooks carriers

Since version 9, **Webhook and Webook JSON carriers are available as a** [**paid add-on**](https://bracketspace.com/downloads/notification-webhooks/). This add-on now offers also an Incoming webhooks feature. We did this to better support this feature as a part of our business. Thank you for your understanding.

## **Compatibility Breaking Changes**

* Webook and Webhook JSON Carriers are now deprecated and won't work. [Read more about that change](https://docs.bracketspace.com/notification/extensions/webhooks)
* Notifications are now saved into the custom table instead of relying on wp\_posts.
* Class methods and properties has been changed from snake\_case to camelCase.
* In Post Triggers, dynamic property `$trigger->{$post_type}` has been replaced with static prop `$trigger->post`.
* The same as above applies to Post Trigger datetime tags, namely: postCreationDatetime, postPublicationDatetime, and postModificationDatetime.
* Post Merge Tags will now use `property_name` attribute rather than `post_type` to set trigger property used by resolvers.
* Hook `notification/data/save` and `notification/data/save/after` now pass Core\Notification instance in the first param instead of the WordPress adapter instance.
* Runtime components are now referenced by FQCN (Fully Qualified Class Name), instead of the name.

### Namespace changes

* `BracketSpace\Notification\Defaults\` changed to `BracketSpace\Notification\Repository\`
* `BracketSpace\Notification\Abstracts\Carrier` changed to `BracketSpace\Notification\Repository\Carrier\BaseCarrier`
* `BracketSpace\Notification\Abstracts\Field` changed to `BracketSpace\Notification\Repository\Field\BaseField`
* `BracketSpace\Notification\Abstracts\MergeTag` changed to `BracketSpace\Notification\Repository\MergeTag\BaseMergeTag`
* `BracketSpace\Notification\Abstracts\Recipient` changed to `BracketSpace\Notification\Repository\Recipient\BaseRecipient`
* `BracketSpace\Notification\Abstracts\Resolver` changed to `BracketSpace\Notification\Repository\Resolver\BaseResolver`
* `BracketSpace\Notification\Abstracts\Trigger` changed to `BracketSpace\Notification\Repository\Trigger\BaseTrigger`

### Hook depracations

* `notification/data/save/after`, use `notification/data/saved`

### Function and method deprecations

* `BracketSpace\Notification\Admin\PostType::getAllNotifications()`, use `BracketSpace\Notification\Database\NotificationDatabaseService::getAll()`
* `notification_convert_data()`, use `BracketSpace\Notification\Core\Notification::from('array', $array)`
* `notification_register_settings()`, use the `notification/settings/register` action directly
* `notification_get_settings()`, use `\Notification::component('settings')->getSettings()`
* `notification_update_setting()`, use `\Notification::component('settings')->updateSetting()`
* `notification_get_setting()`, use `\Notification::component('settings')->getSetting()`
* `notification_adapt()`, use `BracketSpace\Notification\Core\Notification::to()`
* `notification_adapt_from()`, use `BracketSpace\Notification\Core\Notification::from()`
* `notification_swap_adapter()`, use `::from()` and `::to()` methods on the `BracketSpace\Notification\Core\Notification` class
* `notification_add()`, use `BracketSpace\Notification\Register::notification()`
* `notification_log()`, use `BracketSpace\Notification\Core\Debugger::log()`
* `notification()`, use `BracketSpace\Notification\Register::notificationFromArray()`

### Removed deprecated hooks

* `notitication/admin/notifications/pre`, use `notification/admin/carriers/pre`
* `notitication/admin/notifications`, use `notification/admin/carriers`
* `notification/email/use_html_mime`, use `notification/carrier/email/use_html_mime`
* `notification/email/recipients`, use `notification/carrier/email/recipients`
* `notification/email/subject`, use `notification/carrier/email/subject`
* `notification/email/message/pre`, use `notification/carrier/email/message/pre`
* `notification/email/message/use_autop`, use `notification/carrier/email/message/use_autop`
* `notification/email/message`, use `notification/carrier/email/message`
* `notification/email/headers`, use `notification/carrier/email/headers`
* `notification/email/attachments`, use `notification/carrier/email/attachments`
* `notification/webhook/args`, use `notification/carrier/webhook/args`
* `notification/webhook/args/{$type}`, use `notification/carrier/webhook/args/{$type}`
* `notification/notification/form_fields/values`, use `notification/carrier/fields/values`

