---
description: Version 2.0.0
---

# Scheduled Triggers

{% hint style="success" %}
[Download this extension](https://bracketspace.com/downloads/notification-scheduled-triggers/)
{% endhint %}

## How the plugin works

Let's assume that you want to send a notification **7 days after post publication date**. The time window is set to 1 day. This setting means that it will match any post which publication date was between 8 and 7 days ago.

![The timeline. Each gray dot stands for the scheduled check \(default: 5 minutes\)](../.gitbook/assets/scheduled-triggers-after-static.png)



The notification **7 days before post publication date** \(scheduled post\) works the similar way. The time window is as well 1 day. This setting means that it will match any post which has future publication date between 6 and 7 days in the future.

![The timelime](../.gitbook/assets/scheduled-triggers-before-static.png)

### Behind the scenes

The plugin is running on the WordPress Cron. The default schedule is 5 minutes, but you can make it run every day or week, it's configurable.

On each of the executions, the proper objects \(Posts or Users\) are picked from the database. If you are using the Merge Tag time value, **all not locked object are queried**.

![Schedule running and matching an object](../.gitbook/assets/scheduled-triggers.gif)

If there's a match and Notification gets sent, the object is locked for a specific time. 

### Window setting

Defines the time window in which the trigger can be executed. The time setting you set above is a point in time. Having the time window set to 5 minutes means what only 5 minutes after this point in time, the trigger can be executed. This prevents targeting irrelevant posts or users.

Example: having a point in time set to 1 hour after post publication date and 1 day time window, means that if post is published now, only within 1 day this trigger can be executed and match your post.

It's the best to keep the window at least two times longer than the trigger schedule. If the trigger runs daily, set the window to two days. If it will be too short, no object will ever match.

### Lock setting

Used to lock the matched item for a specific time. Ie. when a certain post gets matched and the notification is sent, it can be locked for the next 1 day. It won't be matched again during this time.

You must lock the object either for a specific time or forever to prevent the notification flood.

## Optimization

It's the best to use the predefined options whenever possible:

* Publication date \(post\)
* Modification date \(post\)
* Registration date \(user\)

This way the plugin will query only relevant objects from database.

If you use the Merge Tag, ie. with post meta, the plugin has to pull all not locked objects from database and test each one of them separately. It may cause a high resource usage if you have many posts/users in database and you run a very frequent schedule.

