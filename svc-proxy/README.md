# Homelab Service Proxy

Acts as a reverse proxy to access homelab services. [Caddy](https://caddyserver.com/) is used as the web server for its simplicity.

## Setup
1. Create `.env` and populate with Spaceship (domain registrar) secrets:

```
LIBDNS_SPACESHIP_APIKEY=
LIBDNS_SPACESHIP_APISECRET=
```

2. Install [xcaddy](https://github.com/caddyserver/xcaddy). xcaddy is a custom caddy builder, used to incorporate the spaceship plugin to build caddy.
a. Install go

**Ubuntu**
```zsh
sudo apt install golang-go
```

**MacOS**
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

