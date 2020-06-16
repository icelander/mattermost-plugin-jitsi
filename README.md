# Mattermost Jitsi Plugin (Beta)

[![Build Status](https://img.shields.io/circleci/project/github/mattermost/mattermost-plugin-jitsi/master)](https://circleci.com/gh/mattermost/mattermost-plugin-jitsi)
[![Code Coverage](https://img.shields.io/codecov/c/github/mattermost/mattermost-plugin-jitsi/master)](https://codecov.io/gh/mattermost/mattermost-plugin-jitsi)
[![Release](https://img.shields.io/github/v/release/mattermost/mattermost-plugin-jitsi)](https://github.com/mattermost/mattermost-plugin-jitsi/releases/latest)
[![HW](https://img.shields.io/github/issues/mattermost/mattermost-plugin-jitsi/Up%20For%20Grabs?color=dark%20green&label=Help%20WanOted)](https://github.com/mattermost/mattermost-plugin-jitsi/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc+label%3A%22Up+For+Grabs%22+label%3A%22Help+Wanted%22)

**Maintainer:** [Jesús Espino](https://github.com/jespino)
**Originally developed by:** [Sean Sackowitz](https://github.com/seansackowitz).

Start and join voice calls, video calls and use screen sharing with your team members with a Jitsi plugin for Mattermost.

Clicking a video icon in a Mattermost channel posts a message that invites team members to join a Jitsi meetings call.

![image](https://user-images.githubusercontent.com/13119842/82381170-ba500680-99f7-11ea-8254-d4503999783e.png)

## Features

- Use a `/jitsi` command to start a new meeting. Optionally append a desired meeting topic after the command.
- Embed Jitsi meetings as a floating window inside Mattermost for a seamless experience.
- Click a video icon in channel header to start a new Jitsi meeting in the channel. Not yet supported on mobile.
- Use a `/jitsi settings` command to configure user preferences, including
    - whether Jitsi meetings appear as a floating window inside Mattermost or in a separate window
    - how meeting names are generated

The plugin has been tested on Chrome, Firefox and the Mattermost Desktop Apps.

## Installation

1. Go to https://github.com/mattermost/mattermost-plugin-jitsi/releases to download the latest release file in tar.gz format.
2. Upload the file through **System Console > Plugins > Management**, or manually upload it to the Mattermost server under plugin directory. See [documentation](https://docs.mattermost.com/administration/plugins.html#set-up-guide) for more details.

## Configuration

Go to **System Console > Plugins > Jitsi** and set the following values:

1. **Enable Plugin**: ``true``
2. **Jitsi Server URL**: The URL for your Jitsi server. If you set the Jitsi Server URL to https://meet.jit.si it uses the public server provided by Jitsi.
3. **Embed Jitsi video inside Mattermost**: When true, Jitsi video is embedded as a floating window inside Mattermost. This feature is experimental.
4. (Optional) If your Jitsi server uses JSON Web Tokens (JWT) for authentication, set:

  - **Use JWT Authentication for Jitsi**: ``true``
  - **App ID** and **App Secret** used for JWT authentication
  - **Meeting Link Expiry Time** in minutes. Defaults to 30 minutes.
  
5. **Jitsi Meeting Names**: Select how Jitsi meeting names are generated by default. The user can optionally override this setting for themselves via `/jitsi settings`.

  - Defaults to using random English words in title case, but you can also use a UUID as the meeting link, or the team and channel name where the Jitsi meeting is created. You can also allow the user to choose the meeting name each time by default.

You're all set! To test it, go to any Mattermost channel and click the video icon in the channel header to start a new Jitsi meeting.

### Manual Builds

You can use Docker to compile the binaries yourself. Run `./docker-make` shell script which builds a Docker image with necessary build dependencies and runs `make all` afterwards.

You can also use make targets like `dist` (`./docker-make dist`) from the [Makefile](./Makefile).

## Developing

This plugin contains both a server and web app portion.

Use `make` to check the quality of your code, as well as build distributions of the plugin that you can upload to a Mattermost server for testing.

### Server

Inside the `/server` directory, you will find the Go files that make up the server-side of the plugin. Within there, build the plugin like you would any other Go application.

### Web App

Inside the `/webapp` directory, you will find the JS and React files that make up the client-side of the plugin. Within there, modify files and components as necessary. Test your syntax by running `npm run build`.
