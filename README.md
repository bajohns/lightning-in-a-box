## lightning-in-a-box

This project aims to be a single-command launch for lnd/btcd on testnet (for now). It requires some 
understanding of Docker to use and is tailored for a Unix for now.

If you want to run lightning on command-line; try it out!

### Setup

You need docker & docker-compose. If you have OSX then just run `brew bundle` as this repo has a Brewfile.

### Usage

Once docker is installed just execute `./start.sh` and you are off. This script is a very small wrapper around 
docker-compose. You should see docker-compose build lnd and then start the lnd container.

