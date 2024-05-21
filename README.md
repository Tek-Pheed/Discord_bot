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

Install this librairie in project root folder

```bash
npm i discord.js
```

### Create file

Create a file named ``index.js`` and add the following code to it

```js
import { Client, GatewayIntentBits } from 'discord.js';
const client = new Client({ intents: [GatewayIntentBits.Guilds] });

client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}!`);
});

client.login(TOKEN);
```

To obtain TOKEN, click on this link and create an application by following the steps below.

[Discord developper](https://discord.com/developers/applications)

## Step 2 : Basic command

The bot has been created and can now be connected. Now we'll create a basic command.

For example, when you type ``/ping`` in the discord chat, the bot will respond with ``pong``.

Use this event to do that : 

```js
client.on('interactionCreate', async interaction => {});
```

If you have no idea how to do it, consult the lib discord.js doc directly [here](https://discord.js.org/docs/packages/discord.js/14.15.2) to understand it more easily.

## Step 3 : Bot activity

Now that we have our first command, ``/ping``, we'll move on to another concept: **Activity**.

It consists in modifying the bot's activity, for example ``Play Need4Stek``.

To do this we will use the documentation in the bot activity section, which can be found [here](https://discord.js.org/docs/packages/discord.js/14.15.2/ClientUser:Class#setPresence)

## Step 4 : Catch reaction and roles

We are now going to assign a role according to the reactions put on a specific message.

To do that we are using this topics on stackoverflow [page](https://stackoverflow.com/questions/59069737/discord-js-trying-to-add-role-by-reacting-to-the-message)
