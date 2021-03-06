---
shortTitle: Webhooks
title: Webhooks
---

Instead of requesting our API to see the who has and has not voted for your bot, you can now use webhooks! 
Webhooks will send a `POST` request to a URL or a Discord Webhook of your choice when your bot has been voted for.

--- 

## Custom Webhooks
For Users with a Custom Webhook Server you can start by setting up your webhook URL in the edit form of your bot on our site, it can be found at `https://infinitybotlist.com/bots/:botID/edit` under the `Custom Webhook Url` section of the edit form. Once you've entered the URL you want the webhook to be sent to and provide a secret, you're all set! If you need help setting up custom webhooks inside of your bot or web server don't be afraid to ask in our [discord server](https://infinitybotlist.com/join) in the `》api-support` channel.

---

## Discord Webhooks
Start by setting up your webhook URL in the edit form of your bot on our site, it can be found at https://infinitybotlist.com/bots/:botID/edit under the `Webhook Url` section of the edit form. Once you've entered the URL you want the webhook to be sent to, you're all set! If you need help setting up webhooks inside of your bot don't be afraid to ask in our [discord server](https://infinitybotlist.com/join) in the `》api-support` channel.

---

## Security
1. On the edit page you can see another input for `Secret` or `Secret Auth`. Here you can provide a shared secret that you can check for on the server side.
2. To verify requests are coming from us, look for the value in the `Authorization` header and make sure it is the same as the value you provided in the form.

---

## Acknowledgement
- Webhooks sent by `infinitybotlist.com` **must** be acknowledged with a `2XX` status response (like 200) in order to be considered successful. 
- Unsuccessful webhooks will trigger a [retry](#retrial).

Official `infinitybotlist.com` libraries will be setup to acknowledge webhooks automatically in the near future.

---

## Timeouts
Responses to webhooks must be returned within 5 seconds, otherwise they are considered a timeout and will be queued for a retry (if available).

---

## Retrial
- Webhook requests that time out or return a `5XX` status response (like 500) will be retried up to 10 times. 
- Errors resulting with status `4XX` (like 404, 403 or 400) will not be retried as these are considered user errors.

---

## Data Format
The format of the data your webhook URL will receive in a `POST` request.

#### Bot Webhooks
| Field     | Type        | Description                                                                                         |
| --------- | ----------- | --------------------------------------------------------------------------------------------------- |
| bot       | `snowflake` | Discord ID of the bot that received a vote.                                                         |
| name      | `string`    | Discord Username of the bot that received a vote.                                                   |
| user      | `snowflake` | Discord ID of the user who voted.                                                                   |
| amount    | `string`    | Amount of votes the bot has in total.                                                               |

---

## More Events
Looking for webhook events other than votes? They will be available in a Future Update.
