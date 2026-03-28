# Homelab Service Proxy

Acts as a reverse proxy to access homelab services. [Caddy](https://caddyserver.com/) is used as the web server for its simplicity.

## Setup
1. Create `.env` and populate with Spaceship (domain registrar) secrets:

```
LIBDNS_SPACESHIP_APIKEY=
LIBDNS_SPACESHIP_APISECRET=
```

2. Install [xcaddy](https://github.com/caddyserver/xcaddy). xcaddy is a custom caddy builder, used to incorporate the spaceship plugin to build caddy.

**Ubuntu**
```zsh
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/xcaddy/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-xcaddy-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/xcaddy/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-xcaddy.list
sudo apt update
sudo apt install xcaddy
```

**MacOS**
a. Install go

```zsh
brew install go
```

b. Build from source
```zsh
go install github.com/caddyserver/xcaddy/cmd/xcaddy@latest
```

3. Build caddy (uses spaceship plugin)

```zsh
xcaddy build --with github.com/dippysan/caddy_dns_spaceship
```

4. Run web server
```zsh
./caddy run --envfile ./.env
```

