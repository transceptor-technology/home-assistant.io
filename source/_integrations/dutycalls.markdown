---
title: DutyCalls
description: Instructions on how to add DutyCalls notifications to Home Assistant.
ha_category:
  - Notifications
ha_release: 1.0.0
ha_domain: dutycalls
ha_iot_class: Cloud Push
ha_codeowners:
  - '@robbm1'
ha_platforms:
  - notify
---

The `dutycalls` platform allows you to deliver notifications from Home Assistant to [DutyCalls](https://dutycalls.me/).

## Setup

1. Create a [workspace](https://docs.dutycalls.me/getting-started/#step-1-create-a-workspace) under your dutycalls account.
2. Add a [source](https://docs.dutycalls.me/getting-started/#step-2-add-a-source) to your newly created workspace. Make sure that the source is created with the default config! If this is not done, it may be that the integration does not work or only partially functions.
3. Click the `Setup` button of the added source and request its credentials..
4. Copy the `username` and `password` of the source, and put those credentials into your `configuration.yaml` file -- see below.
5. Add a [channel](https://docs.dutycalls.me/getting-started/#step-3-add-a-channel) and link it to the source you just created.
6. Copy the `name` of the channel and put those credentials into your `configuration.yaml` file -- see below.

<div class='note'>

**Important**: You should store your credentials in a secure location. It is important to keep your credentials confidential to protect your account.

</div>

## Configuration

To enable the DutyCalls notification in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
notify:
  - platform: dutycalls
    default_channel: YOUR_DUTYCALLS_CHANNEL_NAME
    username: YOUR_DUTYCALLS_API_USERNAME
    password: YOUR_DUTYCALLS_API_PASSWORD
```

{% configuration %}
default_channel:
  description: The default channel to post to if no channel is explicitly specified when posting the ticket. A channel can be specified adding a `target` attribute to the JSON at the same level as `message`.
  required: true
  type: string
username:
  description: Home Assistant will post to DutyCalls using the username specified.
  required: true
  type: string
password:
  description: Home Assistant will post to DutyCalls using the password specified.
  required: true
  type: string
{% endconfiguration %}

### DutyCalls Service Data

The following attributes can be placed inside the `data` key of the service call for extended functionality:

| Attribute              | Optional | Description |
| ---------------------- | -------- | ----------- |
| `date_time`            |      yes | The `dateTime` of the ticket. *NOTE*: This must be a Unix timestamp (the number of seconds since the Unix Epoch).
| `severity`             |      yes | The `severity` of the ticket. *NOTE*: This must be a number between `0` and `1`.
| `sender`               |      yes | The `sender` of the ticket.
| `link`                 |      yes | The `link` of the ticket. *NOTE*: This must be a valid URL.
| `identifier`           |      yes | The `identifier` of the ticket.

<div class='note'>

**Important**: Make sure that the source is created with the default config! If this is not done, it may be that the integration does not work or only partially functions.

</div>

### Examples

To post a simple ticket to DutyCalls:

```yaml
message: Message that will be used as the body of the ticket.
title: Title of the ticket.
```

To post a ticket with optional properties to DutyCalls:

```yaml
message: Message that will be used as the body of the ticket.
title: Title of the ticket.
data:
  date_time: 1318874398
  severity: 0.5
  sender: Me
  link: http://site.com
  identifier: 8d7b0d0d-8111-4c56-8e80-0b528d207954
```

To post a ticket to DutyCalls, targeted at multiple channels:

```yaml
message: Message that will be used as the body of the ticket.
title: Title of the ticket.
target:
  - my_first_channel
  - my_second_channel
```
