---
description: Version 1.0.0 or later
---

# Email Attachments

{% hint style="success" %}
[Download this extension](https://bracketspace.com/downloads/notification-email-attachments/)
{% endhint %}

### Attaching files to the email

Plugin accepts:

* absolute paths
* relative paths
* URL (but only pointing to inside or wp-content)

It doesn't matter if the values will be rendered with a Merge Tag or if they are inserted manually. Ie. if you'd like to include a `includes/xample.zip` file from WordPress root directory, you just need to write that in the file field in the attachments section.

### File filter

For security reasons, you cannot attach hidden files (starting with the `.`) nor WordPress files (starting with `wp`). These will be skipped without any warning.
