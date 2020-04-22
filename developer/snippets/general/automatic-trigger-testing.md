# Automatic Trigger testing

If you even wondered how you can automatically test your Triggers without setup them up via wp-admin, this guide is for you.

Use below snippet to create an email notification in background, with one Administrator recipient and all the merge tags in the content. The subject is Trigger name.

```php
add_action( 'notification/trigger/registered', function( $trigger ) {

	if ( 'post/updated' !== $trigger->get_slug() ) {
		return;
	}

	$content = '';
	foreach ( $trigger->get_merge_tags( 'visible' ) as $merge_tag ) {
		$content .= $merge_tag->get_name() . ': {' . $merge_tag->get_slug() . '}' . "\r\n\r\n";
	}

	notification( [
		'hash'     => uniqid(),
		'title'    => $trigger->get_name(),
		'trigger'  => $trigger,
		'carriers' => [
			'email' => [
				'activated'  => true,
				'enabled'    => true,
				'subject'    => $trigger->get_name(),
				'body'       => $content,
				'recipients' => [
					[
						'type'      => 'administrator',
						'recipient' => '',
					],
				],
			],
		],
		'enabled'  => true,
		'extras'   => [],
		'version'  => time(),
	] );

} );
```

