# Plugin loading chain

The plugin initialize itself in a few steps:

1. Plugin loaded by WordPress (or theme/plugin if it's bundled)
2. On `init 5` Notification plugin is initialized - all the classes and functions are loaded
3. `do_action( 'notification/init' )` - Plugin is initialized. Safe for extending

