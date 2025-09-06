# Known issues

## Webhook carrier not available

Please upgrade to the [Webhooks add-on](https://bracketspace.com/downloads/notification-webhooks/). Read more about this change in [upgrading to v9 section](updating-to-v9.md#webhooks-carriers).

## Gutenberg and custom field

When using Gutenberg it's not possible to get every post information AND custom fields at the same time. Everything is saved separately in separate AJAX requests and there's no way we can access all the updated data at once.

You should enable the [Background processing](user-guide/advanced/background-processing.md) to get rid of this issue.

## Pods custom fields

Custom fields saved via Pods framework doesn't get recognized by the Notification plugin thus cannot be used with the Custom Fields extension.

You can try to enable the [Background processing](user-guide/advanced/background-processing.md) to get rid of this issue.
