# Runtime

The plugin initializes itself on action `init` with priority `5` (see the [loading chain](plugin-loading-chain.md)) so after this hook, you can access the whole Runtime object with a simple wrapper class. Within the Runtime, we invoke certain singletons, accessible by their class names.

To get the Runtime object:

```php
$runtime = \Notification::runtime();
```

To get the Settings component:

<pre class="language-php"><code class="lang-php"><strong>// via the component
</strong><strong>use BracketSpace\Notification\Core\Settings;
</strong><strong>
</strong><strong>$settings = \Notification::component(Settings::class);
</strong><strong>
</strong><strong>// or via the alias
</strong><strong>$settings = \Notification::settings()
</strong></code></pre>

To get the plugin version:

```php
$version = \Notification::version();
```

To get the plugin filesystem:

```php
$fs= \Notification::fs();
```

{% hint style="info" %}
Please note the `Notification` class lives in the global namespace.
{% endhint %}

