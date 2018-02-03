## lightning-in-a-box

`tl;dr: ./start.sh`

This project aims to be a single-command launch for lnd/btcd on testnet (for now). It requires some understanding of Docker to use and is tailored for a Unix for now.

If you want to run lightning on command-line; try it out!

_Note_: The Lightning testnet is alpha software and always in flux. Be aware that updating your node can require clearing all local data (sometimes including wallets).

### Setup (docker)

You need docker & docker-compose. If you have OSX then just run `brew bundle` as this repo has a Brewfile.

### Usage

#### lnd

Once docker is installed just execute `./start.sh` and you are off. This script is a very small wrapper around docker-compose. You should see docker-compose build lnd and then start the lnd container.

A few things have to happen for you to start making channels:

* Docker must build the container(s) including a build of lnd from source. This is done on purpose so that everyone can see the code that will be running.
* LND must sync its filter chain. By default lnd must retrieve the filter chain from a compatible btcd node. This repo uses the community full node @ [faucet.lightning.community](faucet.lightning.community)
* LND must connect with peers on the network to create channels and route payments. This will only happen after the filter chain sync.

_Depending on your internet speed this can take awhile_

#### lncli

The primary way to work with lnd is through the accompanying `lncli`. This is built along side the daemon but its in the container. To eliminate the need for jumping in the container to work there are wrapper scripts in the `bin` directory.

`./bin/lncli` executes commands against your lnd as if it was native.

You will know your lnd is ready to go when it reports back `synced_to_chain`.

```
> ./bin/lncli getinfo
{
    "identity_pubkey": "0318d4c7aff98202fa7ab4bb3a45198fe78a691834b391cf542eaea875e745641d",
    "alias": "0318d4c7aff98202fa7a",
    "num_pending_channels": 0,
    "num_active_channels": 4,
    "num_peers": 5,
    "block_height": 1261956,
    "block_hash": "000000000005c17f47d70b692ec5a72c8b511016e2bedc42c3ea1014ebb4ff6f",
    "synced_to_chain": true,
    "testnet": true,
    "chains": [
        "bitcoin"
    ],
    "uris": [
    ]
}
```

### Next steps

If you are looking for more resources on lnd - like how to open a channel - check out the official docs on the [lnd repo](https://github.com/lightningnetwork/lnd).

Also, if you are familiar with docker-compose you will see this repo contains btcd and bitcoind. There is more to come....
