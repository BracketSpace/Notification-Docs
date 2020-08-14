# MemberPress

## Avoid unwanted password reset mail from MemberPress

```php
add_filter( 'mepr-wp-mail-recipients', function( $recipients, $subject, $message, $headers ) {
  if ( strpos( $subject, 'Password Reset') !== false ) {
    $recipients = array(); // Remove all recipients.
  }
  return $recipients;
}, 11, 4 );
```



