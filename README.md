# taraxa-private-test




```
npm install -g taraxa-cli
```

```
jsnapp% taraxa account
address: 0xa072cb485c8a23378de9ea80348fb54da455ff0a
address w/ checksum: 0xA072CB485c8A23378DE9eA80348fb54da455fF0A
public key: 0x04cbd8f6cfd8dc52683b6f0e41bfa47609622389461889210b115986370a72cc5f11846f4fab314716bf55b2bef370c17a4d634d0637e6805fc676fdf26c980111
private key: 0x6551c1f8eeb2daea614e59d5fcd53c47333b5f09f3171fdd2d6192276c65c08c
mnemonic: fancy alone nominee dose custom spend other lunar garlic video south second
```

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
