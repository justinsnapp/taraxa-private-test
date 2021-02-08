# Demonstrate setup of a private network of Taraxa nodes and deploy a simple smart contract application onto it


## Taraxa Command Line Interface

The Taraxa command line interface is a tool used to generate account keys, and node config files.    To install `taraxa-cli` use following command:

```
npm install -g taraxa-cli@1.5.55
```

Example for generating a set of keys for a Taraxa node:

```
jsnapp% taraxa account
address: 0xa072cb485c8a23378de9ea80348fb54da455ff0a
address w/ checksum: 0xA072CB485c8A23378DE9eA80348fb54da455fF0A
public key: 0x04cbd8f6cfd8dc52683b6f0e41bfa47609622389461889210b115986370a72cc5f11846f4fab314716bf55b2bef370c17a4d634d0637e6805fc676fdf26c980111
private key: 0x6551c1f8eeb2daea614e59d5fcd53c47333b5f09f3171fdd2d6192276c65c08c
mnemonic: fancy alone nominee dose custom spend other lunar garlic video south second
```

Taraxa config generation can be done using the cli by adding various options to it.   If a known name like "testnet" is supplied you will get a config for joining the public testnet.  In this case we want to generate one for a private testnet.   You will find it helpful though to reference the config generated for the public tesnet to see how the genesis block is defined.  The private testnet genesis block but allocate coins to node(s) that wish to pariticpate in consensus.  Re-allocation can be done via RPC calls to generate transactions to send coins from one node to another.

```
jsnapp% taraxa config --help                                
Usage: taraxa config [options]

generate a taraxa node config file

Options:
  -n, --network <string>           network (testnet, private), default: private
  -a, --as-boot-node               run this node as a boot node
  -b, --boot-node <string>         boot node string to join existing network. format: ip_address:port_number/node_id. this option can be repeated to add additional boot nodes (default:
                                   [])
  -c, --chain-id <number>          chain id
  -d, --dir <string>               taraxa config directory, default: ~/.taraxa-node
  -f, --force                      force overwrite of existing file
  -g, --genesis <string>           additional address to receive genesis coins. repeat this option to add more recipients. when -b is not provided, this boot node also receives genesis
                                   payouts. coins are split evenly. (default: [])
  -o, --stdout                     write output to std out instead of file
  -p, --private-key <string>       generate config using specific node secret (private key)
  -s, --stake-at-genesis <string>  genesis addresses that are also staking at genesis. repeat this option to add more. (default: [])
  -t, --tcp-port <number>          Specify TCP port to listen on (default 10002
  -u, --udp-port <number>          Specify UDP port to listen on (default 10002
  -v, --vrf-secret <string>        generate config using specific vrf secret
  -h, --help                       display help for command
```

## TASK 1: Generate Configs For Private Testnet

*We first want to generate config files a boot node, used by other nodes to join the network.   Then we generate config files for individual additional nodes to be able to join the network.*



**Generate a config for a new *private* network boot node:**

``` sh
$ taraxa config
Created node config for:
    network: private
    chain id: 4444
    address: 0x942FBF4f9D0CbE737e4f83C597D991ffA38fe42c
    id: 04a58a7add71a5c973e36fa754f5ddd00f3b15404677f3d20ac4fa02f808857c0d497e20ea95ffd5e3a516fac90693f4f3016291d353f7cf863457bcb834769c75

Wrote config to: /home/user1/.taraxa-node/conf/private.json

Note: This file contains private keys. Secure it properly.
```

**Generate a config to join an existing private network by specifying one or more boot nodes by repeating the `-b` option:**

```
taraxa config -n private -c 4444 -b 127.0.0.1:10002/04a58a7add71a5c973e36fa754f5ddd00f3b15404677f3d20ac4fa02f808857c0d497e20ea95ffd5e3a516fac90693f4f3016291d353f7cf863457bcb834769c75
```

###Task 1 Deliverable: Please upload your config files that you generated for your private network


## TASK 2: Deploy Network of Nodes

Docker images of the node already built along with the Taraxa cli installed are available on [docker hub](https://hub.docker.com/r/taraxa/taraxa).

```
docker pull taraxa/taraxa:1.5.55-89
```

To run a node you must provide the path to conf file:

```
./main --conf_taraxa /opt/taraxa_data/conf/testnet.json
```

###Docker Compose File (Provided in Repo)

**We have provided a starting point of a docker compose file for deploying a node.   Feel free to use this as a basis for your deployment...**

```
version: '3'
volumes:
    taraxa_data:
services:
    taraxa-node:
        container_name: taraxa-node
        image: taraxa/taraxa:1.5.55-89
        restart: always
        ports:
            - "10002:10002"
            - "10002:10002/udp"
            - "7777:7777"
            - "8777:8777"
        expose:
            - "10002"
            - "7777"
            - "8777"
        entrypoint:
            /usr/bin/sh
        command: >
            -c "taraxa config -d /var/taraxa --force &&
                ./main --conf_taraxa /var/taraxa/conf/private.json"
        volumes:
            - taraxa_data:/var/taraxa
```

###Task 2 Deliverable: Please upload your deployment scripts/commands for deploying a private Taraxa testnet with one (or more) boot node and two (or more) additional nodes



## Task 3: Deploy an ERC-20 token onto the private Taraxa network

###Task 3 Delivarble: Solidity ERC-20 token contract file for you ERC-20 token and python code for deploying it

*Some possibly helpful references...*

[Example guid on deploying an ERC-20 token](https://medium.com/better-programming/create-and-deploy-your-own-erc-20-token-on-the-ethereum-network-87931fe4db20)

[Deploying a smart contract via Python](https://support.blockdaemon.com/hc/en-us/articles/360022161812-How-To-Deploy-A-Smart-Contract-with-An-Ethereum-Node-Using-Web3py)

## TASK 4: Send ERC-20 tokens from Alice to Bob using python

###Task 4 Devlierable: Your private testnet should have (at least) two users, a rich "Alice" and a poor "Bob" who Alice gives some of her cool new ERC-20 tokens to...

*Some possibly helpful references...*

[Working with ERC-20 tokens in Python](https://web3py.readthedocs.io/en/stable/examples.html#working-with-an-erc20-token-contract)



