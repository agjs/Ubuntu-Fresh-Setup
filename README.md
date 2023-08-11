# Setup

**General**

- Use proprietary (tested) GPU driver.
- sudo apt upgrade

**Install Jet Brains Font**

- [Download the Font](https://www.jetbrains.com/lp/mono/)
- Extract the zip to `~/Downloads`

```bash
# JetBrainsMono-2.304 the version might differ in the future

mkdir -p ~/.local/share/fonts
cd ~/Downloads/JetBrainsMono-2.304/fonts/ttf
cp *.ttf  ~/.local/share/fonts/
fc-cache -fv
```

## Install

**Using Snap**

- OBS Studio
- VSCode
- Cameractrls
- Tilix

**Other**

- [zsh and oh my zsh](https://ohmyz.sh/)

```bash
# Install zsh
sudo apt install zsh

# Install oh my zsh
https://ohmyz.sh/#install
```

- [Git](https://git-scm.com/download/linux)

```bash


git config --global user.name "Aleksandar"
git config --global user.email "hi@programmer.network"

# Generate SSH Key
ssh-keygen -t rsa -b 4096
chmod 600 ~/.ssh/id_rsa

# Install xclip
sudo apt-get install xclip

# Copy the public key
xclip -sel clip < ~/.ssh/id_rsa.pub

# Add the SSH Key to Github
# https://github.com/settings/keys
```

- [nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
- [Docker](https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository)

Setup Postgres and Redis

```bash
# Redis
sudo docker run --name redis-container -d -p 6379:6379 --restart=always redis:latest
```

```bash
# Postgres
sudo docker run --name postgres-container -e POSTGRES_PASSWORD=password -d -p 5432:5432 --restart=always postgres:latest

# Add the user to the docker group to run Docker commands without sudo:
sudo usermod -aG docker $USER

# Setup Postgres User & Development Database

docker exec -it postgres-container psql -U postgres

CREATE USER developer WITH PASSWORD 'postgrespw';
ALTER USER developer WITH SUPERUSER;
CREATE DATABASE development OWNER developer;
```

## Tilix (Terminal)

With Tilix, just like with other Terminal applications I'm using on Windows (Windows Terminal) and my Macbook Pro (iTerm 2), we want to configure two things, quake mode and a default directory that opens when a new session is created.

### Using Quake Mode via Shortcut in Tilix

To configure a shortcut for Quake Mode in Tilix, we need to set up a custom shortcut key combination in our system settings, since Tilix itself does not have an internal configuration for this. Here's a general guide:

- Open Tilix Preferences.
- Go to the "Quake" tab.
- Configure your Quake window preferences, such as height, width, position, etc.

Next, we'll need to set up a system-wide shortcut to invoke Tilix in Quake mode:
For GNOME (common in many Ubuntu installations):

- Open "Settings."
- Navigate to "Keyboard Shortcuts."
- Scroll down and click the "+" button to add a custom shortcut.
- Name it "Tilix Quake Mode" or something similar.
- In the "Command" field, enter tilix --quake.
- Click "Set Shortcut" and press the key combination you want to use.
- Click "Add."

Now, whenever we press the key combination you set, Tilix should appear in Quake mode.

### Fix paste shortcut

Tilix paste command by default is set to _CTRL + SHIFT + V_. Remember to update it to _CTRL + V_.

### Open "code" folder on each new session

We can configure Tilix to always start in a specific directory (such as our code folder) for each new session.

- Open Tilix.
- Right-click on the terminal window and go to "Profiles".
- Choose the profile you want to edit, or the default one if you haven't created any custom profiles.
- Click "Edit Profile".
- In the "Command" tab, find the "Run custom command instead of my shell" option.
- Check the box and enter the command you want to run. If you're using bash or Zsh, you might use something like:

```bash
bash --init-file <(echo "cd ~/path/to/your/code/folder")
```

or with Zsh:

```bash
zsh -c 'cd ~/path/to/your/code/folder; exec zsh'
```

Close the preferences window. Done.
