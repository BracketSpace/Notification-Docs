---
description: A list of all Trigger names and slugs
---

# List of all default Triggers

{% tabs %}
{% tab title="Comment" %}
This covers all the comment types. Use `comment`, `pingback`, `trackback`, `another_comment_type` instead of the `{comment_type_slug}`.

| Trigger name       | Trigger slug                             |
| ------------------ | ---------------------------------------- |
| Comment added      | `comment/{comment_type_slug}/added`      |
| Comment approved   | `comment/{comment_type_slug}/approved`   |
| Comment replied    | `comment/{comment_type_slug}/replied`    |
| Comment spammed    | `comment/{comment_type_slug}/spammed`    |
| Comment trashed    | `comment/{comment_type_slug}/trashed`    |
| Comment unapproved | `comment/{comment_type_slug}/unapproved` |
| Comment published  | `comment/{comment_type_slug}/published`  |
{% endtab %}

{% tab title="Media" %}
| Trigger name  | Trigger slug    |
| ------------- | --------------- |
| Media added   | `media/added`   |
| Media trashed | `media/trashed` |
| Media updated | `media/updated` |
{% endtab %}

{% tab title="Plugin" %}
| Trigger name       | Trigger slug         |
| ------------------ | -------------------- |
| Plugin activated   | `plugin/activated`   |
| Plugin deactivated | `plugin/deactivated` |
| Plugin installed   | `plugin/installed`   |
| Plugin removed     | `plugin/removed`     |
| Plugin updated     | `plugin/updated`     |
{% endtab %}

{% tab title="Post" %}
This covers all the custom post types, as well. Use `post`, `page`, `product`, `another_post_type` instead of the `{post_type_slug}`.

| Trigger name             | Trigger slug                                |
| ------------------------ | ------------------------------------------- |
| Post added               | `post/{post_type_slug}/added`               |
| Post saved as a draft    | `post/{post_type_slug}/drafted`             |
| Post sent for review     | `post/{post_type_slug}/pending`             |
| Post approved            | `post/{post_type_slug}/approved`            |
| Post published           | `post/{post_type_slug}/published`           |
| Post published privately | `post/{post_type_slug}/published-privately` |
| Post trashed             | `post/{post_type_slug}/trashed`             |
| Post updated             | `post/{post_type_slug}/updated`             |
| Post scheduled           | `post/{post_type_slug}/scheduled`           |
{% endtab %}

{% tab title="Taxonomy" %}
This covers all the taxonomies. Use `category`, `post_tag`, `another_taxonomy` instead of the `{taxonomy_slug}`.

| Trigger name          | Trigger slug                       |
| --------------------- | ---------------------------------- |
| Taxonomy term created | `taxonomy/{taxonomy_slug}/created` |
| Taxonomy term deleted | `taxonomy/{taxonomy_slug}/deleted` |
| Taxonomy term updated | `taxonomy/{taxonomy_slug}/updated` |
{% endtab %}

{% tab title="Theme" %}
| Trigger name    | Trigger slug      |
| --------------- | ----------------- |
| Theme installed | `theme/installed` |
| Theme switched  | `theme/switched`  |
| Theme updated   | `theme/updated`   |
{% endtab %}

{% tab title="User" %}
| Trigger name                | Trigger slug                  |
| --------------------------- | ----------------------------- |
| User deleted                | `user/deleted`                |
| User login                  | `user/login`                  |
| User login failed           | `user/login_failed`           |
| User logout                 | `user/logout`                 |
| User password changed       | `user/password_changed`       |
| User password reset request | `user/password_reset_request` |
| User profile updated        | `user/profile_updated`        |
| User registered             | `user/registered`             |
| User role changed           | `user/role_changed`           |
| User email change request   | `user/email_change_request`   |
| User email changed          | `user/email_changed`          |
{% endtab %}

{% tab title="WordPress" %}
| Trigger name              | Trigger slug                     |
| ------------------------- | -------------------------------- |
| Available updates         | `wordpress/updates_available`    |
| Site email change request | `wordpress/email_change_request` |
| Site email changed        | `wordpress/email_changed`        |
| WordPress updated         | `wordpress/updated`              |
{% endtab %}

{% tab title="Privacy" %}
| Trigger name                 | Trigger slug                  |
| ---------------------------- | ----------------------------- |
| Personal Data erased         | `privacy/data-erased`         |
| Personal Data erase request  | `privacy/data-erase-request`  |
| Personal Data exported       | `privacy/data-exported`       |
| Personal Data export request | `privacy/data-export-request` |
{% endtab %}
{% endtabs %}
