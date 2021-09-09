# Relayer

### Install Cro
```
$ wget https://github.com/cosmos/relayer/releases/download/v0.9.3/Cosmos.Relayer_0.9.3_linux_amd64.tar.gz
$ tar -zxvf Cosmos.Relayer_0.9.3_linux_amd64.tar.gz
$ cp "Cosmos Relayer" /usr/local/bin/rly
```

### Init config
```
$ rly config init
$ cd .relayer/config
```

### Create a settings file for Ki
```
$ nano ki_config.json
```
copy the content and place it in a file

> {
  "chain-id": "kichain-t-4",
  "rpc-addr": "http://localhost:26657",
  "account-prefix": "tki",
  "gas-adjustment": 1.5,
  "gas-prices": "0.025utki",
  "trusting-period": "10m"
}

### Create a settings file for Cro
```
$ nano cro_config.json
```
copy the content and place it in a file

> {
  "chain-id": "testnet-croeseid-4",
  "rpc-addr": "http://localhost:26652",
  "account-prefix": "tcro",
  "gas-adjustment": 1.5,
  "gas-prices": "0.025basetcro",
  "trusting-period": "10m"
}

### Add settings to config
```
$ rly chains add -f $HOME/.relayer/config/ki_config.json
$ rly chains add -f $HOME/.relayer/config/cro_config.json
$ cd
```

### Add or restore wallets
add:
```
$ rly keys add testnet-croeseid-4 key_cro
$ rly keys add kichain-t-4 key_ki
```
or restore:
```
$ rly keys restore testnet-croeseid-4 key_cro "your mnemonic Cro wallet"
$ rly keys restore kichain-t-4 key_ki "your mnemonic Ki wallet"
```

### Check wallets balances
```
$ rly q bal testnet-croeseid-4
$ rly q bal kichain-t-4
```

#### Faucets:
> Ki: [Discord group "Ki Foundation"](https://discord.gg/sgYfsqcV)

> Cro: [Discord group "Crypto.org Chain"](https://discord.com/invite/pahqHz26q4)

### Init the light client
```
$ rly light init testnet-croeseid-4 -f
$ rly light init kichain-t-4 -f
```

### Create channels
```
$ rly paths generate kichain-t-4 testnet-croeseid-4 ki-cro --port=transfer
$ rly paths generate testnet-croeseid-4 kichain-t-4 cro-ki --port=transfer
```

### Check list 
```
$ rly chains list
```
there should be flags: 
```
0: kichain-t-4          -> key(✔) bal(✔) light(✔) path(✔)
1: testnet-croeseid-4   -> key(✔) bal(✔) light(✔) path(✔)
```
