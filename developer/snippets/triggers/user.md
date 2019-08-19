# User

## Adding default Merge Tags to "User registered" Trigger

```php
add_action( 'notification/trigger/registered', function( $trigger ) {

	if ( $trigger->get_slug() !== 'wordpress/user_registered' ) {
		return;
	}

	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserNicename() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserDisplayName() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserFirstName() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserLastName() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserBio() );

} );
```
