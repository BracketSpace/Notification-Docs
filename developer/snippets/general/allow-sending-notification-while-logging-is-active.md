# Allow sending Notification while logging is active

By default, if the Notification logging \(Settings -&gt; Debugging\) is active, all the Notifications are supressed. If you'd like to log them and still send theme, you can use this simple filter: 

```php
add_filter( 'notification/debug/suppress', '__return_false' );
```

