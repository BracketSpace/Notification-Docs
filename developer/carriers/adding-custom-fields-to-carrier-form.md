# Adding custom fields to Carrier form

To add new fields to the Carrier form you need to hook into the `notification/carrier/registered` action.

```php
use BracketSpace\Notification\Repository\Carrier\Email;
use BracketSpace\Notification\Repository\Field\InputField;

add_action(
    'notification/carrier/registered',
    function($carrier)
    {
        if (! $carrier instanceof Email::class) {
            return;
        }

        $carrier->addFormField(
            new InputField(
                [
                    'label' => __('Example Field', 'textdomain'),
                    'name' => 'example',
                    'resolvable' => true,
                ]
            )
        );
    }
);
```

{% hint style="info" %}
All the field data will be automatically stored and available in `$carrier->data` property in `send()` method.
{% endhint %}
