# User

## Adding default Merge Tags to "User registered" Trigger

```php
add_action( 'notification/trigger/merge_tags', function( $trigger ) {

	if ( $trigger->get_slug() !== 'user/registered' ) {
		return;
	}

	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserNicename() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserDisplayName() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserFirstName() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserLastName() );
	$trigger->add_merge_tag( new BracketSpace\Notification\Defaults\MergeTag\User\UserBio() );

} );
```

