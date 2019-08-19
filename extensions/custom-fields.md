# Custom Fields

{% hint style="success" %}
[Download this extension](https://bracketspace.com/downloads/notification-custom-fields/)
{% endhint %}

### Regular meta

The Custom Fields extension supports meta of three object types:

* Posts
* Users
* Comments

Here are the examples with equivalents in `get_****_meta()`

```text
{postmeta {post_ID} metakey}
// equivalent of:
// get_post_meta( $post_id, $metakey, true );
```

```text
{usermeta {user_ID} metakey}
// equivalent of:
// get_user_meta( $user_id, $metakey, true );
```

```text
{commentmeta {comment_ID} metakey}
// equivalent of:
// get_comment_meta( $comment_id, $metakey, true );
```

Note that `{post_ID}` or `{user_ID}` or `{comment_ID}` part is the object ID which can be static \(like just `365783`\) or can be a merge tag. If you are using merge tags for this part, like in the examples, please make sure you can see this merge tag in the sidebar. So if you choose the **Book updated** trigger, the `{post_ID}` will become `{book_ID}`.

### Advanced Custom Fields meta

Any ACF field value can be get with the regular meta merge tags, but sometimes you'd want to let ACF format the data for you.

Very similar to regular meta you can use it like this:

```text
{acf {post_ID} my_field_slug}
{acf comment_{comment_ID} fieldname}
{acf user_{user_ID} fieldname}
{acf term_{term_ID} fieldname}
```

Which is an equivalent of:

```php
get_field( $fieldname, $item_id );
```

{% hint style="info" %}
You can access the first-level array key as well
{% endhint %}

Giving an example, you can have a field of type _User_ and return format of _User array_. Your meta will look like this:

```text
Array
(
    [ID] => 1
    [user_firstname] => Panda
    [user_lastname] => Bear
    [nickname] => admin
    [user_nicename] => admin
    [display_name] => Panda Bear
    [user_email] => admin@localhost.localhost
    [user_url] => 
    [user_registered] => 2019-03-14 10:46:17
    [user_description] => 
    [user_avatar] => <img alt='' src='http://2.gravatar.com/avatar/21c9a0124feee215cb7c5759f7e6670b?s=96&#038;d=mm&#038;r=g' srcset='http://2.gravatar.com/avatar/21c9a0124feee215cb7c5759f7e6670b?s=192&#038;d=mm&#038;r=g 2x' class='avatar avatar-96 photo' height='96' width='96' />
)
```

To access the `user_email` key, you just need to do it like this:

```text
{acf {post_ID} user_field:user_email}
```

### Access array keys

{% hint style="info" %}
You can also get array values from meta and access their first-level keys.
{% endhint %}

Let's consider an example, where you have this array in your meta:

```php
Array
(
    [date] => 2019-03-14 10:46:17
    [accepted] => 1
    [email] => 'user@email.com'
)
```

To access the `email` key you just need to pass the array key after the colon:

```text
{postmeta {post_ID} metakey:email}
```

This will work with any type of meta.

Giving the ACF example, you can have a field of type _User_ and return format of _User array_. Your meta will look like this:

```text
Array
(
    [ID] => 1
    [user_firstname] => Panda
    [user_lastname] => Bear
    [nickname] => admin
    [user_nicename] => admin
    [display_name] => Panda Bear
    [user_email] => admin@localhost.localhost
    [user_url] => 
    [user_registered] => 2019-03-14 10:46:17
    [user_description] => 
    [user_avatar] => <img alt='' src='http://2.gravatar.com/avatar/21c9a0124feee215cb7c5759f7e6670b?s=96&#038;d=mm&#038;r=g' srcset='http://2.gravatar.com/avatar/21c9a0124feee215cb7c5759f7e6670b?s=192&#038;d=mm&#038;r=g 2x' class='avatar avatar-96 photo' height='96' width='96' />
)
```

To access the `user_email` key, you just need to do it like this:

```text
{acf {post_ID} user_field:user_email}
```

#### Multidimensional array

But what in case you have a multidimensional array like this?

```text
Array
(
    [user] => Array
    (
        [user_firstname] => Panda
        [user_lastname] => Bear
        [user_email] => admin@localhost.localhost
    )
)
```

Easy! Just pass the nested keys after another colon:

```text
{... user_field:user:user_email}
```

### Pipelines

Sometimes the value in meta is not exactly in a form you'd like. The most common scenario is having a post or user ID saved in the meta while you want to display a `post_title` or `display_name`.

This is where pipelines come to the rescue. Let's assume you have a Taxonomy ACF field added to your post, where you can select multiple terms. The raw meta would look like this:

```text
Array
(
    [0] => 14
    [1] => 1
    [2] => 46
)
```

Which are just the term IDs.

To get term names out of these, you can use pipeline like so:

```text
{acf {post_ID} taxonomy_field|term:name}
```

The pipeline comes after a `|` character and we support three pipes:

* post
* user
* term

And do you notice the `|term:name` array key notation here? That's right, the `|term` part will get the whole term data and the `:name` will access the term array key _name_.

{% hint style="info" %}
Pipelines are supported by both ACF and regular meta Merge Tags. You can use multidimensional array access as well `:with:this:notation` 
{% endhint %}

