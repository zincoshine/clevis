# 🗜️clevis

Ethereum blockchain orchestration, testing, CLI, and Dapp scaffolding.

## install

easiest: use docker (it handles the environment and RPC node for you):
```
docker pull austingriffith/clevis:latest
docker run -ti --rm --name clevis -p 3000:3000 -p 8545:8545 \
  -v ~/your-dapp-directory:/dapp austingriffith/clevis
```

OR install/link for the source:
```
git clone https://github.com/austintgriffith/clevis.git
cd clevis
npm install
sudo npm link
```

OR try an npm install:
```
sudo npm install --unsafe-perm -g clevis@latest
```

If you aren't using docker make sure you install ganache-cli and mocha:
```
npm install -g ganache-cli
npm install --g mocha
```

[Read full article and watch screencast here!](https://medium.com/@austin_48503/%EF%B8%8Fclevis-blockchain-orchestration-682d2396aeef)


## demo

[![Clevis Demo Video](https://user-images.githubusercontent.com/2653167/44128017-a7caa1d2-9ffd-11e8-999c-ceabc3287647.png)](https://www.youtube.com/watch?v=lekFaRzma8U)


## docker options

### attach to already running clevis container
```
docker exec -ti clevis bash
```


### external RPC
```
docker run -ti --rm --name clevis --env network="http://10.0.0.107:8545" \
  -p 3000:3000 -p 8545:8545 -v ~/your-dapp-directory:/dapp austingriffith/clevis
```

### Automatic Rinkeby Geth Node
```
docker run -ti --rm --name clevis --env network="rinkeby" \
  -p 3000:3000 -p 8545:8545 -v ~/your-dapp-directory:/dapp austingriffith/clevis
```

### Automatic Ropsten Geth Node
```
docker run -ti --rm --name clevis --env network="ropsten" \
  -p 3000:3000 -p 8545:8545 -v ~/your-dapp-directory:/dapp austingriffith/clevis
```

### Automatic Mainnet Geth Node
```
docker run -ti --rm --name clevis --env network="mainnet." \
  -p 3000:3000 -p 8545:8545 -v ~/your-dapp-directory:/dapp austingriffith/clevis
```

### Docker build from Clevis Repo
```
git clone https://github.com/austintgriffith/clevis.git
cd clevis
docker build . -t clevis
docker run -ti --rm --name clevis -p 3000:3000 -p 8545:8545 -v ~/your-dapp-directory:/dapp clevis
```

## troubleshooting

Right now the web3 dependencies are not very well supported and installs can fail on certain machines.

I would recommend using Docker and the container model because it handles the environment and geth node for you.

*WARNING* if you get this error: gyp ERR! stack Error: EACCES: permission denied, mkdir '/usr/local/lib/node_modules/clevis/node_modules/scrypt/build'
```
rm -rf .node-gyp
sudo npm install --unsafe-perm -g clevis@latest
```

If you have other errors or problems, let's get this list populated. Shoot me an email and let's debug: austin@concurrence.io


## commands/examples

### help
```
clevis help
```
lists available commands and usage

### init
```
clevis init
```
installs/updates latest version, creates the react app, and initializes configuration

### version
```
clevis version
```
lists current version

### update
```
clevis update
```
loads latest prices and standard gas and updates config

### accounts
```
clevis accounts
```
lists accounts from Geth or other RPC endpoint

### new [password]
```
clevis new ""
```
creates a new address

### unlock [accountindex] ["password"]
```
clevis unlock 0 ""
```
unlocks account

### send [amount] [fromindex] [toindex]
```
clevis send 0.1 0 1
```
send ether from one local account to another by index

### sendTo [amount] [fromindex] [toaddress]
```
clevis sendTo 0.1 0 0x6FC8152A3C0E0aC8e61faf233915e1334b58fC77
```
send ether from local account to any address

### balance [address]
```
clevis balance 0x6FC8152A3C0E0aC8e61faf233915e1334b58fC77
```
get balance of any Ethereum address or local index

### sign [string] [accountindex] [password]
```
clevis sign "Hello World" 0 ""
```
sign a string with a local account

### recover [string] [signature]
```
clevis recover "Hello World" "0x87dc7..."
```
recover address used to sign a string

### sha3 [string]
```
clevis sha3 "Hello World"
```
generates the keccak256 hash of a string

### sendData [amount] [fromindex] [toaddress] [data]
```
clevis sendData 0.001 0 0x6FC8152A3C0E0aC8e61faf233915e1334b58fC77 "0x01"
```
send ether and/or data to an account

### create [contractname]
```
clevis create SomeContract
```
create a contract

### compile [contractname]
```
clevis compile SomeContract
```
compile a contract

### deploy [contractname] [accountindex]
```
clevis deploy SomeContract 0
```
deploy a contract

### explain [contractname]
```
clevis explain SomeContract
```
list all contract commands/events etc

### contract [scriptname] [contractname] [[accountIndex]] [[contractArguments...]]
```
clevis contract someFunction SomeContract 1 someArgument
```
interact with a contract
these scripts are generated automatically using the ABI
(list .clevis folder inside any contract folder to see all scripts)

you can also read from contracts:
```
clevis contract balanceOf Copper 0x2a906694d15df38f59e76ed3a5735f8aabcce9cb
```

### test [testname]
```
clevis test compile
```
run mocha test from tests folder

### wei [amount] [symbol]
```
clevis wei 0.1 ether
```
convert to wei from ether or others like gwei or szabo

### hex [asciistring]
```
clevis hex "Hello World"
```
convert a string to hex

### ascii [hexstring]
```
clevis ascii "0x48656c6c6f20576f726c64"
```
convert hex to a string

### blockNumber
```
clevis blockNumber
```
get current block number

### block [blocknumber]
```
clevis block 2618069
```
get block information

### transaction [hash]
```
clevis transaction 0x474acab2ba2702a90c4b774d7cee7fe1364ca1df01735ecef188522f8ce40bc4
```
get transaction information

### build
```
clevis build
```
builds static react site

### upload [target]
```
clevis upload metatx.io
```
uploads static react site to s3 bucket named after url

### invalidate [target]
```
clevis invalidate E3837d00567
```
invalidate cloudfront caching to show fresh content

## demo

[![cleviscast](http://s3.amazonaws.com/atgpub/clevispreview2.png)](http://s3.amazonaws.com/atgpub/clevis.mp4)
