# User

## Adding default Merge Tags to "User registered" Trigger

```php
use BracketSpace\Notification\Defaults\MergeTag;

add_action( 'notification/trigger/merge_tags', function( $trigger ) {
	if ( $trigger->get_slug() !== 'user/registered' ) {
		return;
	}

	$trigger->add_merge_tag( new MergeTag\User\UserNicename() );
	$trigger->add_merge_tag( new MergeTag\User\UserDisplayName() );
	$trigger->add_merge_tag( new MergeTag\User\UserFirstName() );
	$trigger->add_merge_tag( new MergeTag\User\UserLastName() );
	$trigger->add_merge_tag( new MergeTag\User\UserBio() );
} );
```
