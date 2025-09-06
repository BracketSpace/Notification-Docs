# Slack

## Posting to private channel

In order to be able to post to private channel (group), you need to invite the `notification` bot to this channel first.

You can do this by typing the following in the Slack private channel:

```
/invite @notification
```

## Why I need to select a channel while authenticating the Notification Slack App?

This is because backward compatibility and need for webhook creation. The Notification bot will have access to all public channels by default. You can add it to the private channel(s) as well.
