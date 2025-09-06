# Custom Trigger

New, custom triggers can be easily registered in your plugin or theme. All you need is a simple class declaration and a function call.

The Trigger is really only a wrapper for WordPress' action(s).&#x20;

## Trigger class

Have a look at the example Trigger class.

```php
use BracketSpace\Notification\Repository\MergeTag;
use BracketSpace\Notification\Repository\Trigger\BaseTrigger;

/**
 * Custom trigger class
 */
class CustomTrigger extends BaseTrigger
{
    /**
     * Param value
     */
    public $paramValue;

    /**
     * Constructor
     */
    public function __construct()
    {
        // 1. Slug, can be prefixed with your plugin name.
        // 2. Title, should be translatable.
        parent::__construct(
            'myplugin/custom_trigger',
            __('Custom Trigger title', 'textdomain')
        );

        // 1. Action hook.
        // 2. (optional) Action priority, default: 10.
        // 3. (optional) Action args, default: 1.
        // It's the same as add_action( 'any_action_hook', 'callback', 10, 2 ) with
        // only difference - the callback is always context() method (see below).
        $this->addAction('any_action_hook', 10, 2);

        // 1. Trigger group, should be translatable.
        // This is optional, Group is displayed in the Trigger select.
        $this->setGroup(__('My Triggers', 'textdomain'));

        // 1. Trigger description, should be translatable.
        // This is optional, Description is displayed in the Trigger select.
        $this->setDescription(
            __('Fires when a page with "myparam" parameter is visited', 'textdomain')
        );
    }

    /**
     * Assigns action callback args to object
     * Return `false` if you want to abort the trigger execution
     *
     * You can use the action method arguments as usually.
     *
     * @return mixed void or false if no notifications should be sent
     */
    public function context($paramOne, $paraTwo)
    {
        /**
         * This is a method callback hooked to the action you've added in the Constructor.
         *
         * Two important things which are happening here:
         * - $this->callback_args is a numeric array containing all the callback parameters
         *   if you want to treat them as an array
         * - if you want to abort Trigger execution, you must return false here
         */

        // If the second parameter ($process in our action) is false then abort, no carriers will be processed.
        if (false === $paramTwo) {
            return false;
        }

        // We can assign any property here, whole object will be accessible in Merge Tag resolver.
        $this->paramValue = $paramOne;
    }

    /**
     * Registers attached merge tags
     *
     * @return void
     */
    public function mergeTags()
    {
        /**
         * In this method you can assign any Merge Tags to the trigger.
         *
         * To see what Merge Tags are available go to Notification plugin's core
         * and look in class/Repository/MergeTag directory.
         */

        $this->addMergeTag(
            new MergeTag\StringTag(
                [
                    // Slug (required), this will be used as {parametrized_url} value.
                    // Don't translate this.
                    'slug' => 'parametrized_url',
                    // Name (required), should be translatable.
                    'name' => __('Parametrized URL', 'textdomain'),
                    // Resolver (required), this can be a closure like below or function name
                    // like: 'parametrized_url_resolver' or [$this, 'parametrized_url_resolver'].
                    'resolver' => function($trigger) {
                        // Trigger object is available here,
                        // with all the properties you set in action() method.
                        return add_query_arg('source', $trigger->paramValue, site_url());
                    },
                    // Description (optional), should be translatable, default: ''.
                    'description' => __('Homepage URL with ?source=param', 'textdomain'),
                    // Example indicator (optional)
                    // if true, then description will have "Example" label, default: false.
                    'example' => true,
                ]
            )
        );
    }
}
```

### Lazy loading Trigger params

When the Trigger is registered or defined, it's too early to pull data from WordPress components like Post Types or Taxonomies. In such case, you can lazy load the name, description, and group - these get evaluated only for editing purposes.

Instead of defining all the params in the constructor, create getter methods. An example of Post Trigger:

```php
/**
 * Post trigger class
 */
abstract class PostTrigger extends BaseTrigger
{
    /**
     * Constructor
     *
     * @param array<mixed> $params trigger configuration params.
     */
    public function __construct($params = [])
    {
        $this->postType = $params['post_type'];

        parent::__construct($params['slug']);
    }

    /**
     * Lazy loads group name
     *
     * @return string|null Group name
     */
    public function getGroup()
    {
        return WpObjectHelper::getPostTypeName($this->postType);
    }

    /**
     * Gets Post Type slug
     *
     * @return string Post Type slug
     */
    public function getPostType(): string
    {
        return $this->postType;
    }

    /*********************************
     * Below code comes from specific post trigger
     *********************************/

    /**
     * Lazy loads the name
     *
     * @return string name
     */
    public function getName(): string
    {
        return sprintf(
        // translators: singular post name.
            __('%s scheduled', 'notification'),
            WpObjectHelper::getPostTypeName($this->postType)
        );
    }

    /**
     * Lazy loads the description
     *
     * @return string description
     */
    public function getDescription(): string
    {
        return sprintf(
        // translators: 1. singular post name, 2. post type slug.
            __('Fires when %1$s (%2$s) is scheduled', 'notification'),
            WpObjectHelper::getPostTypeName($this->postType),
            $this->postType
        );
    }
}
```

## Registering the Trigger

Having this class is only a first step. To get the trigger registered you must create an instance of this class and pass it to the Notification plugin. The best action to do that is `notification/init`

```php
use BracketSpace\Notification\Register;

add_action('notification/init', function() {
    Register::trigger(new CustomTrigger());
});
```
