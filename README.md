wireguard-tools
===============

Full documentation about Wireguard installation and configuration process can be found [here](https://gitlab.com/snippets/1897102).

wgcg.sh
-------

### About

This script is created to ease manual process of Wireguard configuration and will help you to automatically generate all the required configuration files (client and server), PKI key pairs and preshared key.

### Usage

Before start using this script I would suggest updating default options in [wgcg.vars](./wgcg.vars) file, otherwise you will have to specify these options from the command line every time you run the script.

```bash
# Server name (wireguard interface name e.g. wg0 || wg1 || wg2)
export WGCG_SERVER_NAME="wg0"
# VPN (WG) IP private address
export WGCG_SERVER_WG_IP="10.0.0.1"
# Static server port
export WGCG_SERVER_PORT="52001"
# Server's public IP or FQDN
export WGCG_SERVER_PUBLIC_IP="wg.example.com"
```

Export variables defined in [wgcg.vars](./wgcg.vars) file

```bash
source wgcg.vars
```

Print help and current default options

```plain
# ./wgcg.sh -h
Usage:
  wgcg.sh options

Options:
  -s|--server-config [server_name] [server_wg_ip] [server_port]
  -c|--client-config client_name client_wg_ip [server_name] [server_port] [server_public_ip]
  -q|--gen-qr-code client_name
  -S|--sync [server_name] [server_public_ip]
  -h|--help

Current default options:
  WGCG_SERVER_NAME="wg0"
  WGCG_SERVER_WG_IP="10.0.0.1"
  WGCG_SERVER_PORT="52001"
  WGCG_SERVER_PUBLIC_IP="wg.example.com"
```

Generate server keys and config

```bash
./wgcg.sh -s
```

Generate client keys, client config and update server config (add a new Peer)

```bash
./wgcg.sh -c foo 10.0.0.2
```

Copy over updated server configuration to the server

```bash
./wgcg.sh --sync
```
