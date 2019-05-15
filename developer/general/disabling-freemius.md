# Disabling Freemius

If you don't want to load Freemius you can disable it in two ways:

### Constant

```php
define( 'NOTIFICATION_LOAD_FREEMIUS', false );
```

### Filter

```php
add_filter( 'notification/freemius', function( $load ) {
	return false;
}, 10, 1 );
```

{% hint style="warning" %}
The filter takes precedence
{% endhint %}

