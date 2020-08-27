+++
title = "Using the Example Wallet"
weight = 2
template = "docs-page.html"
+++

# Working with the bdk CLI Example Wallet

The bitcoindevkit comes with an example cli wallet used for testing during development. This article explains what it offers and how to use it.

<br />

## Building the Wallet
Cargo (Rust's package manager) offers the ability to build and run examples scripts that can be added to libraries under a directory usually called `examples`. You build the examples using the following command:

```sh
cargo build --examples
```

In our case, this will produce a binary called `wallet` which you can find under `/target/debug/examples`.


You can then run the binary using the following structure:

```sh
cargo run --example wallet -- <flags and arguments to be passed to the binary>
```

<br />

## Using the Wallet (Basics)

Start by running the wallet with the `--help` flag to see what it can do:

```txt
cargo run --example wallet --help

wallet 0.1.0
BDK Team
Example bdk based wallet for testing

USAGE:
    wallet [OPTIONS] --connections <NUMBER> --password <PASSWORD>

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -c, --connections <NUMBER>     number of peer connections [default: 5]
    -d, --data <DIRECTORY>         data directory [default: .]
    -i, --discovery <discovery>    turn peer discovery on or off [default: on]  [possible values: on, off]
    -l, --log <LEVEL>              logging level [default: info]  [possible values: debug, info, warn, error]
    -n, --net <NETWORK>            bitcoin network [default: testnet]  [possible values: regtest, testnet]
    -p, --password <PASSWORD>      wallet password
    -a, --peers <IP_ADDRESS>...    ip addresses of peer nodes, eg. 127.0.0.1:9333
```

You can start the wallet by using something like:
```sh
cargo run --example wallet -- --password testpass
```
This will get you in the wallet application, which will await further commands:

```txt
cargo run --example wallet -- --password testpass

logging level: INFO
working directory: "."
discovery: true
network: testnet
peers: []
created new wallet, seed words: use cattle tag cage good razor plunge pipe dial cabbage goat approve
first deposit address: 2MxRb5jtzezZLMrx7qLQuJXagStjGjtxKC7
peer connections: 5
No previous history.
starting p2p thread
>>
```

Once wallet is started, use the `help` command from the >> prompt to get a list of sub-commands the wallet can execute.

<br />

## Using the Wallet (Advanced)

A more involved wallet startup might look something like the following, and would require the use of a local regtest network:

```sh
cargo run --example wallet -- --net regtest --password testpass --peers 127.0.0.1:18432
```
A great way to get a regtest going is by using Nigiri. Check out [our article](@/docs/testing-bdk/nigiri-regtest.md) on how to do just that if you need. From there, use the Nigiri Chopsticks API to create a new block and send the reward to `<DEPOSIT ADDRESS>`

```sh
curl -X POST --data '{"address": "<DEPOSIT ADDRESS>"}' http://localhost:3000/faucet
```
   
Or connect to the Nigiri created bitcoind and use the containers bitcoin-cli to generate multiple bocks and send the reward to `<DEPOSIT ADDRESS>`
   
```sh
docker exec -it resources_bitcoin_1 bitcoin-cli -regtest -rpcport=19001 -rpcuser=admin1 -rpcpassword=123 generatetoaddress 100 <DEPOSIT ADDRESS>
```
   
Or if you have bitcoin-cli installed on your local OS outside the Nigiri container you can use it to tell the Nigiri 
   created bitcoind to generate multiple blocks and send the rewards to `<DEPOSIT ADDRESS>`
   
```sh
bitcoin-cli -regtest -rpcport=18433 -rpcuser=admin1 -rpcpassword=123 generatetoaddress 100 <DEPOSIT ADDRESS>
```

Using the wallet generates `/testnet/` or `/regtest/` directories (by default in the directory where the wallet is called), which you can delete once you are done with:

```sh
rm -rf ./testnet
rm -rf ./regtest
```

<br />

## Checking the Logs

The wallet will keep its logs in a file called `wallet.log` located in the newly created `/regtest/` or `/testnet/` directory. You can print the lastest logs using the following command:

```sh
tail -f regtest/wallet.log
```

The wallet also keeps a history of all commands passed to it, which are in the `/regtest/history.txt` file. Print out its content using

```sh
cat ./regtest/history.txt
```

