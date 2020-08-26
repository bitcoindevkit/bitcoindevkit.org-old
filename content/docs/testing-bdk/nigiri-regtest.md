+++
title = "Set up a Regtest Network"
weight = 1
template = "docs-page.html"
+++

# Setting up a Regtest Network using Nigiri

Nigiri is a regtest-in-a-box tool we recommend for testing and developing with the bitcoin development kit. You can find their [GitHub repository here](https://github.com/vulpemventures/nigiri) and their [official website here](https://nigiri.vulpem.com/).

<br />

## Overview

Nigiri is a series of docker containers that together form an ecosystem around a bitcoin regtest network. It provides a bitcoin daemon, an electrum Rust server, an Esplora block explorer web interface, and a Liquid daemon.

See their [readme](https://github.com/vulpemventures/nigiri) for how to set it up. You can either download the binary at [nigiri.vulpem.com](https://nigiri.vulpem.com/) or you can build it from source. Both are well explained.

The easiest way to get Nigiri up and running is to use the following bash command:

```sh
curl https://getnigiri.vulpem.com | bash
```

The first thing you need to do once you have Nigiri installed is to start it up:

```sh
nigiri start

# nigiri stop
```

From there, a simple way to get started and play with the regtest in Nigiri is to get inside the bitcoin node container and use bitcoin-cli directly:

```sh
# get inside the container
docker exec -it resources_bitcoin_1 bash

# generate a new address
bitcoin-cli -datadir=config getnewaddress
```
<br />

## Logs

You can access the logs for all containers and services using the following commands:

```sh
# bitcoind
nigiri logs node

# electrs
nigiri logs electrs

# chopsticks
nigiri logs chopsticks
```
<br />

## Configuration

Nigiri stores the `bitcoin.conf`  by default in the `~/.nigiri` data directory folder.
To tweak your Bitcoin node configuration:

1. Edit the `~/.nigiri/resources/volumes/regtest/config/bitcoin.conf` file
2. If already started, stop and delete `nigiri stop --delete`
3. Start and mount inside the container the edited configuration file `nigiri start`
