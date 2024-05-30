# How to create discord bot in JS

During this project we will create base discord bot in javascript.

## Step 1: Requierements

### Install nodejs and npm

For this project we need to use npm and nodejs to run the program

#### Fedora
```bash
sudo dnf install -y gcc-c++ make
sudo curl -sL https://rpm.nodesource.com/setup_20.x | sudo bash - 
sudo dnf install nodejs
node -v
npm -v
```

#### Arch

```bash
sudo pacman -S nodejs
node -v
npm -v
```

#### Ubuntu

```bash
cd ~
curl -sL https://deb.nodesource.com/setup_20.x -o /tmp/nodesource_setup.sh
sudo bash /tmp/nodesource_setup.sh
sudo apt install nodejs
node -v
npm -v
```

#### Windows or MacOS

Download the LTS version on this [link](https://nodejs.org/en)


### Install the discord.js librairie

download all this repository to get all necessary files

use this command : ``npm i``

### Create file

Create a file named ``index.js`` and add the following code to it

```js
const { Client, Events, GatewayIntentBits } = require("discord.js");
const { token } = require("./config.json");

const client = new Client({ intents: [GatewayIntentBits.Guilds] });

client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}!`);
});

client.login(token);
```

To obtain TOKEN, click on this link and create an application by following the steps below.

[Discord developper](https://discord.com/developers/applications)

replace the line in the config.json with your own token

use ``npm run start`` to start the bot

#### Invite your discord bot on your server

replace in the following url ID by your client_id

https://discord.com/oauth2/authorize?client_id=ID

## Step 2 : Basic command

The bot has been created and can now be connected. Now we'll create a basic command.

For example, when you type ``/ping`` in the discord chat, the bot will respond with ``pong``.

run this command : ``npm i fs``

add this before ``client.on('ready'...``

```js
const fs = require("node:fs");
const path = require("node:path");
const { Client, Collection, Events, GatewayIntentBits } = require("discord.js");
const { token } = require("./config.json");

const client = new Client({ intents: [GatewayIntentBits.Guilds] });

client.commands = new Collection();

const foldersPath = path.join(__dirname, "commands");
const commandFiles = fs
    .readdirSync(foldersPath)
    .filter((file) => file.endsWith(".js"));
for (const file of commandFiles) {
    const filePath = path.join(foldersPath, file);
    const command = require(filePath);
    if ("data" in command && "execute" in command) {
        client.commands.set(command.data.name, command);
    } else {
        console.log(
            `[WARNING] The command at ${filePath} is missing a required "data" or "execute" property.`,
        );
    }
}
```

Use this event to do that in the index.js : 

```js
client.on('interactionCreate', async interaction => {
  if (!interaction.isChatInputCommand()) return;
    const command = interaction.client.commands.get(interaction.commandName);

    if (!command) {
        console.error(
            `No command matching ${interaction.commandName} was found.`,
        );
        return;
    }

    try {
        await command.execute(interaction);
    } catch (error) {
        console.error(error);
        if (interaction.replied || interaction.deferred) {
            await interaction.followUp({
                content: "There was an error while executing this command!",
                ephemeral: true,
            });
        } else {
            await interaction.reply({
                content: "There was an error while executing this command!",
                ephemeral: true,
            });
        }
    }
});
```

Create file in folder ``commands/ping.js``for example.

paste the following code

```js
const { SlashCommandBuilder } = require("discord.js");

module.exports = {
    data: new SlashCommandBuilder()
        .setName("ping")
        .setDescription("reply with pong"),
    async execute(interaction) {
        await interaction.reply(`pong`);
    },
};
```

run ``npm run commands`` to deploy your command on your server

If you have no idea how to do it, consult the lib discord.js doc directly [here](https://discord.js.org/docs/packages/discord.js/14.15.2) to understand it more easily.

## Step 3 : Bot activity

Now that we have our first command, ``/ping``, we'll move on to another concept: **Activity**.

It consists in modifying the bot's activity, for example ``Play Need4Stek``.

To do this we will use the documentation in the bot activity section, which can be found [here](https://discord.js.org/docs/packages/discord.js/14.15.2/ClientUser:Class#setPresence)

## Step 4 : Catch reaction and roles

We are now going to assign a role according to the reactions put on a specific message.

To do that we are using this topics on stackoverflow [page](https://stackoverflow.com/questions/59069737/discord-js-trying-to-add-role-by-reacting-to-the-message)

## Step 5 : Imagine

Now you have the base to create discord bot.

Add new features on your bot !
