# Plugin loading chain

The plugin initialize itself in a few steps:

1. Plugin loaded by WordPress - all the classes and functions are loaded
2. `do_action( 'notification/boot/initial' )`
3. On `plugins_loaded` with priority `10` Carriers, Recipients and Global Merge Tags are loaded
4. On `init` with priority `1000` Triggers are loaded
5. `do_action( 'notification/boot' )` - Plugin is fully initialized and all the defaults are loaded



