# Adding Merge Tags to existing Triggers

Sometimes it's needed to add your own Merge Tag to an already defined Trigger. In example you can add a custom meta Merge Tag to default `Post Published` Trigger.

To do this simply hook into the action and add your Merge Tag:

```php
use BracketSpace\Notification\Repository\MergeTag;
use BracketSpace\Notification\Repository\Trigger\Post\PostPublished;

// Hook into an action when Merge Tags are attached to Trigger.
add_action(
    'notification/trigger/merge_tags',
    function($trigger)
    {
        // Check if registered Trigger is the one you need.
        if (! $trigger instanceof PostPublished::class) {
            return;
        }

        // Pay attention to the Tag type you are defining.
        // If you want to output an HTML, use HtmlTag instead.
        $trigger->addMergeTag(
            new MergeTag\StringTag(
                [
                    'slug' => 'new_merge_tag',
                    'name' => __('New Merge Tag', 'textdomain'),
                    'resolver' => function($trigger) {
                        return get_post_meta($trigger->post->ID, '_my_meta_key', true);
                    },
                ]
            )
        );
    }
);
```

{% hint style="warning" %}
Since v9, dynamic property `$trigger->{$post_type}` has been replaced with a static prop `$trigger->post`.
{% endhint %}



## Targeting all Post Type Triggers

You can target all the Post Type Triggers like this:

```php
add_action(
    'notification/trigger/merge_tags',
    function($trigger)
    {
        if (! preg_match(
                '/post\/(.*)\/(updated|trashed|published|drafted|added|pending|scheduled)/',
                $trigger->getSlug()
        ) {
            return;
        }

        // Add your Tag.
    }
);
```

## Global Merge Tags

The Notification plugin also supports global Merge Tags which are added to all Triggers. You can use this nifty function to create one:

```php
use BracketSpace\Notification\Defaults\MergeTag\StringTag;
use BracketSpace\Notification\Register;

Register::globalMergeTag(new StringTag([
	'slug' => 'option_value',
	'name'=> __('Site option', 'textdomain'),
	'resolver' => function($trigger) {
		return get_option('your_option_name', 'Default');
	},
]));
```

{% hint style="warning" %}
Before using any property of the Trigger make sure it's available. Global Merge Tags are intended to be loosely connected with any Trigger.
{% endhint %}
