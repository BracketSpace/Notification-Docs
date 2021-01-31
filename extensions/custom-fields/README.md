---
description: Documentation for version 1.4 or later
---

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

Any ACF field value can be retrieved with the regular meta merge tags, but sometimes you'd want to let ACF format the data for you.

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
    [user_email] => admin@example.com
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

Getting the meta often means you need to work with arrays. Deeper levels can be easily accessed with `:` character.

Let's consider an example, where you have this array in your meta:

```php
Array
(
    [date] => 2019-03-14 10:46:17
    [accepted] => 1
    [email] => 'user@example.com'
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
    [user_email] => admin@example.com
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

#### Multidimensional arrays

But what in case you have a multidimensional array like this?

```text
Array
(
    [user] => Array
    (
        [user_firstname] => Panda
        [user_lastname] => Bear
        [user_email] => admin@example.com
    )
)
```

Easy! Just pass the nested keys after another colon:

```text
{... user_field:user:user_email}
```

Same story with numeric arrays:

```text
Array
(
    [0] => Array
    (
        [user_firstname] => Panda
        [user_lastname] => Bear
        [user_email] => admin@example.com
    )
)
```

```text
{... user_field:0:user_email}
```

### Pipelines

Sometimes the value in meta is not exactly in a form you'd like. The most common scenario is having a post or user ID saved in the meta while you want to display a `post_title` or `display_name`.

Each pipe is processing the value and manipulate its representation. You can think about it like this:

```text
Initial value -> replace -> reshape -> replace -> format
```

So the initial value of User ID can be replaced with a whole User object and this object can be formatted as JSON.

{% hint style="info" %}
Pipes can be mixed together and each pipe can be used with the array accessors. They work with ACF and regular meta Merge Tags.  
[See the example](./#examples).
{% endhint %}

All supported pipelines:

| Objects | Manipulators | Formatters |
| :--- | :--- | :--- |
| [post](./#post) | [first](./#first) | [bool](./#bool) |
| [postmeta](./#postmeta) | [last](./#last) | [join](./#join) |
| [term](./#term) | pluck | [json](./#json) |
| [termmeta](./#termmeta) |  |  |
| [user](./#user) |  |  |
| [usermeta](./#usermeta) |  |  |

#### post

Gets the [post object](https://developer.wordpress.org/reference/classes/wp_post/) as an array.

```text
|post
```

#### postmeta

Gets the post meta.

```text
|postmeta,$key,$single
```

`$key` and `$single` arguments are optional. If you omit the `$key` argument all the post meta is retrieved. This is an equivalent of [`get_post_meta` function](https://developer.wordpress.org/reference/functions/get_post_meta/).

`$single` will evaluate to boolean, so you can write any of: `on`, `true`, `1`, `yes`, etc.

#### term

Gets the [term object](https://developer.wordpress.org/reference/classes/wp_term/) as an array.

```text
|term
```

#### termmeta

Gets the term meta.

```text
|termmeta,$key,$single
```

`$key` and `$single` arguments are optional. If you omit the `$key` argument all the term meta is retrieved. This is an equivalent of [`get_term_meta` function](https://developer.wordpress.org/reference/functions/get_term_meta/).

`$single` will evaluate to boolean, so you can write any of: `on`, `true`, `1`, `yes`, etc.

#### user

Get the [user object](https://developer.wordpress.org/reference/classes/wp_user/) as an array.

```text
|user
```

#### usermeta

Gets the user meta.

```text
|usermeta,$key,$single
```

`$key` and `$single` arguments are optional. If you omit the `$key` argument all the user meta is retrieved. This is an equivalent of [`get_term_meta` function](https://developer.wordpress.org/reference/functions/get_term_meta/).

`$single` will evaluate to boolean, so you can write any of: `on`, `true`, `1`, `yes`, etc.

#### pluck

Plucks the values from the collection

```text
|pluck,$key
```

`$key` argument is required. This is an equivalent of [`wp_list_pluck` function](https://developer.wordpress.org/reference/functions/wp_list_pluck/).

Plucking the `name` key from this array:

```text
Array
(
    [0] => Array
    (
        [name] => John Doe
    )
    [1] => Array
    (
        [name] => Jane Doe
    )
)
```

Will result with:

```text
Array
(
    [0] => John Doe
    [1] => Jane Doe
)
```

#### join

Joins the array values into a comma-separated string.

```text
|join
```

Joining an array:

```text
Array
(
    [0] => John Doe
    [1] => Jane Doe
)
```

Will result with:

```text
John Doe, Jane Doe
```

#### first

Gets the first element of an array.

```text
|first
```

Getting the first element of an array:

```text
Array
(
    [0] => John Doe
    [1] => Jane Doe
)
```

Will result with:

```text
John Doe
```

#### last

Gets the last element of an array.

```text
|last
```

Getting the last element of an array:

```text
Array
(
    [0] => John Doe
    [1] => Jane Doe
)
```

Will result with:

```text
Jane Doe
```

#### bool

Formats the boolean value in the desired way.

```text
|bool,$true,$false
```

* `$true` String to return when the value is evaluated to `true`
* `$false` String to return when the value is evaluated to `false`

Example:

```text
|bool,Active and ready to go,Disabled
```

#### json

Formats the value as json.

```text
|json
```

### Value formatting

String values are always displayed as literal strings. No HTML is escaped.

If the returned value is an array with a single item, it's automatically unwrapped and the first item is returned.

Array values are represented with `print_r()` function and wrapped with `<pre>` tags. Example:

```text
Array
(
    [0] => Array
    (
        [name] => John Doe
    )
    [1] => Array
    (
        [name] => Jane Doe
    )
)
```

Boolean values are represented as `Yes` or `No` by default.

You can change the format by using the formatting pipes, like bool, join, or json.

### Examples

Post has a `related_post` field \(stored post ID\) where another related post can be selected. The related post has a field where `owner` can be selected and this returns the user ID. To get this user email:

```text
{postmeta {post_ID} related_post|postmeta,owner,true|user:user_email}
```

Explanation:

* `{postmeta {post_ID} related_post` - gets the initial value of the related post, post ID is retrieved
* `|postmeta,owner,true` - related post ID is used to get the meta key `owner` and `true` means the single value should be returned. We get the User ID.
* `|user:user_email` - user ID is used to get the whole user representation. We access the `user_email` array key to get the email

### Limitations

The plugin cannot handle iterators. Ie. if you want to map an array of users. In other words, it's not possible to work on the collections. The subsequent pipes are meant to reduce the data to a single value.
