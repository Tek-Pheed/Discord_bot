# How to create discord bot in JS

## Requierements

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
