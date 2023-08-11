# Setup

*Using Snap*

* OBS Studio
* VSCode
* Cameractrls
* Tilix

*Other methods*

* [Git](https://git-scm.com/download/linux)
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

* [nvm](https://github.com/nvm-sh/nvm#installing-and-updating)
* [Docker](https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository)

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