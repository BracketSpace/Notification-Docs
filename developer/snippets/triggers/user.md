# User

## Adding default Merge Tags to "User registered" Trigger

```php
use BracketSpace\Notification\Defaults\MergeTag;

add_action(
    'notification/trigger/merge_tags',
    function($trigger) {
        if ($trigger->getSlug() !== 'user/registered') {
            return;
        }

        $trigger->addMergeTag(new MergeTag\User\UserNicename());
        $trigger->addMergeTag(new MergeTag\User\UserDisplayName());
        $trigger->addMergeTag(new MergeTag\User\UserFirstName());
        $trigger->addMergeTag(new MergeTag\User\UserLastName());
        $trigger->addMergeTag(new MergeTag\User\UserBio());
    }
);
```
