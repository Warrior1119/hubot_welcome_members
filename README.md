# hubot-rocketchat-boilerplate
Create and run a Rocket.Chat bot in under two minutes. 

### NB: THIS IS A WORK IN PROGRESS

> Please do not attempt to implement until this message is removed
>
> The `-develop` tag will also be removed from the package file.

## Quick Start

```
git clone https://github.com/Warrior1119/hubot_welcome_members.git
cd hubot_welcome_members
npm install
```
Create a _.env_ file with content:

```
export ROCKETCHAT_URL=myserver.com
export ROCKETCHAT_USER=mybotuser
export ROCKETCHAT_PASSWORD=mypassword
export ROCKETCHAT_ROOM=general
export ROCKETCHAT_USESSL=true
...
```

Adjust the content to fit your server and user credentials. Make sure `myuser` has **BOT role** on the server, if you don't know what that means, ask your server administrator to set it up for you.

Then run the bot:

```
source .env
bin/hubot
```

On the server, login as a regular user (not the BOT user), go to GENERAL, and try:

```
mybotuser what time is it
```

OR

```
mybotuser rc version
```
`< TBD:  insert sample run screenshot >`

You can examine the source code of these two bots under the `/scripts` directory, where you can add your own bot scripts written in Javascript.

## More Details

This is a boilerplate for making your own bots with Hubot and Rocket.Chat.

### Running Locally

You can run with the shell adapter just to test

1. Run `yarn` or `npm install` to install dependencies
2. Use the `yarn shell` script to start the bot with shell adaptor
3. Say `hubot help` to see what it can do

When you're ready to connect the bot to an instance of Rocket.Chat

1. Create a user for the bot, with the role _bot_
2. Create an `./.env` file with the user and connection settings
3. Run `yarn local` script to connect to your local Rocket.Chat

The `local` npm script will read in the env file, so you can populate and modify
those settings easily (see [configuration](#configuration)). In production, they
should be pre-populated in the server environment.

### Running in Production

There are executables for different environments that all run the Hubot binary.

Before running make sure your production environment has the required 
environment variables for the adapter, url, user, name and pass. Or you can add
them after the launch command as switches, like `-a rocketchat`.

- `bin/hubot` unix binary
- `bin/hubot.cmd` in windows
- `Procfile` for Heroku

Env variables should be populated on the server before launching
(see [configuration](#configuration)). The launcher will also install npm
dependencies on every run, in case it's booting in a fresh container (this isn't
required when working locally).

More information on [deployment configs][deployment] here.

### Adding Scripts

Scripts can be added to the `./scripts` folder, or by installing node packages
and listing their names in the `external-scripts.json` array. There's an example
of each in this repo, but neither is required.

### Example Scripts

Two scripts are packaged with the boilerplate, as a demo for manual tests.
Each of the following will respond in a public channel if the bot username is
prefixed, or without the bot's name if in a DM.

- `what time is it` or `what's the time` - Tells you the time
- `rc version` - Gives you version info for Rocket.Chat and Hubot (two messages)

## Configuration

When running locally, we've used [`dotenv`][dotenv] to load configs from the
`./.env` file. That makes it easy for setting environment variables.

Please see [adapter docs for source of truth on environment variables][env].
