# Background Processing filter

Regardless of the [setting in Dashboard](../../../user-guide/advanced/background-processing.md) you can enable or disable background processing for a particular Trigger with a simple filter. You can reference [default Triggers](../../triggers/default-triggers.md) here.

{% tabs %}
{% tab title="Disable Triggers" %}
```php
add_filter(
    'notification/trigger/process_in_background',
    function($enabled, $trigger) {
        $disabledSlugs = [
            'user/registered',
            'user/login',
        ];

        if (in_array($trigger->getSlug(), $disabledSlugs, true)) {
            return false;
        }

        return $enabled;
    },
    10,
    2
);
```
{% endtab %}

{% tab title="Enable Triggers" %}
```php
add_filter(
    'notification/trigger/process_in_background',
    function($enabled, $trigger) {
        $enabledSlugs = [
            'user/registered',
            'user/login',
        ];

        if (in_array($trigger->getSlug(), $enabledSlugs, true)) {
            return true;
        }

        return $enabled;
    },
    10,
    2
);
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
This filter was added in version 7.2.3.
{% endhint %}
