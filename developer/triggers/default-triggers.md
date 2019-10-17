---
description: A list of all Trigger names and slugs
---

# List of all default Triggers

{% tabs %}
{% tab title="Comment" %}
This covers all the comment types. Use `comment`, `pingback`, `trackback`, `another_comment_type` instead of the `{comment_type_slug}`.

| Trigger name | Trigger slug |
| :--- | :--- |
| Comment added | `wordpress/comment_{comment_type_slug}_added` |
| Comment approved | `wordpress/comment_{comment_type_slug}_approved` |
| Comment replied | `wordpress/comment_{comment_type_slug}_replied` |
| Comment spammed | `wordpress/comment_{comment_type_slug}_spammed` |
| Comment trashed | `wordpress/comment_{comment_type_slug}_trashed` |
| Comment unapproved | `wordpress/comment_{comment_type_slug}_unapproved` |
| Comment published | `wordpress/comment_{comment_type_slug}_published` |
{% endtab %}

{% tab title="Media" %}
| Trigger name | Trigger slug |
| :--- | :--- |
| Media added | `wordpress/media_added` |
| Media trashed | `wordpress/media_trashed` |
| Media updated | `wordpress/media_updated` |
{% endtab %}

{% tab title="Plugin" %}
| Trigger name | Trigger slug |
| :--- | :--- |
| Plugin activated | `wordpress/plugin/activated` |
| Plugin deactivated | `wordpress/plugin/deactivated` |
| Plugin installed | `wordpress/plugin/installed` |
| Plugin removed | `wordpress/plugin/removed` |
| Plugin updated | `wordpress/plugin/updated` |
{% endtab %}

{% tab title="Post" %}
This covers all the custom post types, as well. Use `post`, `page`, `product`, `another_post_type` instead of the `{post_type_slug}`.

| Trigger name | Trigger slug |
| :--- | :--- |
| Post added | `wordpress/{post_type_slug}/added` |
| Post saved as a draft | `wordpress/{post_type_slug}/drafted` |
| Post sent for review | `wordpress/{post_type_slug}/pending` |
| Post published | `wordpress/{post_type_slug}/published` |
| Post trashed | `wordpress/{post_type_slug}/trashed` |
| Post updated | `wordpress/{post_type_slug}/updated` |
{% endtab %}

{% tab title="Taxonomy" %}
This covers all the taxonomies. Use `category`, `post_tag`, `another_taxonomy` instead of the `{taxonomy_slug}`.

| Trigger name | Trigger slug |
| :--- | :--- |
| Taxonomy term created | `wordpress/{taxonomy_slug}/created` |
| Taxonomy term deleted | `wordpress/{taxonomy_slug}/deleted` |
| Taxonomy term updated | `wordpress/{taxonomy_slug}/updated` |
{% endtab %}

{% tab title="Theme" %}
| Trigger name | Trigger slug |
| :--- | :--- |
| Theme installed | `wordpress/theme/installed` |
| Theme switched | `wordpress/theme/switched` |
| Theme updated | `wordpress/theme/updated` |
{% endtab %}

{% tab title="User" %}
| Trigger name | Trigger slug |
| :--- | :--- |
| User deleted | `wordpress/user_deleted` |
| User login | `wordpress/user_login` |
| User login failed | `wordpress/user_login_failed` |
| User logout | `wordpress/user_logout` |
| User password changed | `wordpress/user_password_changed` |
| User password reset request | `wordpress/user_password_reset_request` |
| User profile updated | `wordpress/user_profile_updated` |
| User registration | `wordpress/user_registered` |
{% endtab %}

{% tab title="WordPress" %}
| Trigger name | Trigger slug |
| :--- | :--- |
| Available updates | `wordpress/updates_available` |
{% endtab %}
{% endtabs %}

