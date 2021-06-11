# Zabbix Matrix webhook

[![CI](https://github.com/jooola/zabbix-matrix-webhook/actions/workflows/ci.yml/badge.svg)](https://github.com/jooola/zabbix-matrix-webhook/actions/workflows/ci.yml)

This guide describes how to integrate your Zabbix 4.4 installation with Matrix using the Zabbix webhook feature. This guide will provide instructions on setting up a media type.

## Matrix configuration

The configuration of the webhook use [Element](https://element.io/) to interact with the Matrix server, but receiving notification from Zabbix work with any [Matrix client](https://matrix.org/clients/).

### Create a Matrix account

Visit [app.element.io](https://app.element.io/) and create a new account for your bot.

### Retrieve the bot's access token

Open a **private/incognito** window in you browser, and sign in [app.element.io](https://app.element.io) with the bot account:

![](docs/matrix_access_token1.png)

Open the bot account settings pages:

![](docs/matrix_access_token2.png)

In the settings page, open the `Help & About` tab, scroll to the bottom `Advanced` section and click on `<click to reveal>` to retrieve the access token:

![](docs/matrix_access_token3.png)

Finally, **do not log out** (logging out invalidate the access token), instead, just close the **private/incognito** window.

### Set up a Matrix room

Invite the bot in the room you want the alerts to be sent.

In the room settings page, open the `Advanced` tab and retrieve the `Internal room ID`:

![](docs/matrix_room_id1.png)

## Zabbix webhook configuration

Import the [`media_matrix.yml`](media_matrix.yml) or [`media_matrix.json`](media_matrix.json) file into your zabbix installation. Depending on the Zabbix server version, you might need to tweak the file before importing it.

- Prior to Zabbix versions 5.2: Import the [`media_matrix.json`](media_matrix.json) JSON file, YAML import is not supported.
- Prior to Zabbix versions 5.0: Remove the `message_templates` section from the import file.

In the media type configuration, fill the `<server>` value with the Matrix server [URL](https://en.wikipedia.org/wiki/URL) and `<token>` with the previously retrieved access token.

Create or configure the `Matrix` media type for your user, and paste the `Internal room ID` in the `Send to` field.
