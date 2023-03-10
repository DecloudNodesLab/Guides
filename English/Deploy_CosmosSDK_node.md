<div align="center">

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>

# Validator node (based on Cosmos SDK), deployment to Akash Network.
</div>
<div align="center">
  
| [Twitter Decloud Nodes Lab](https://twitter.com/NodesLab) |
|:--:|

| [Akash Network](https://akash.network/) | [Akash Network Forum](https://forum.akash.network/) |
|:--:|:--:|
___

Our newsfeeds technical support:

| [Discord Akash](https://discord.akash.network/) | [Telegram Akash EN](https://t.me/AkashNW) | [Telegram Akash RU](https://t.me/akash_ru) | [TwitterAkash](https://twitter.com/akashnet_) | [TwitterAkashRU](https://twitter.com/akash_ru) |
|:--:|:--:|:--:|:--:|:--:|

</div>
 
<div align="center">
  
[Русская версия](/Russian/Deploy_CosmosSDK_node.md)
  
</div>

___

## Node deployment:

Select a project and deploy the [deploy.yml](https://github.com/DecloudNodesLab/Projects/tree/main/CosmosSDK) file using **Cloudmos (Akashlytics)** ([instructions for use here](/English/Cloudmos.md)).
If you use the projects that we have prepared, then you just need to enter your values in the variables listed below in `deploy.yml`, leave the rest unchanged: <br/>
```
- "SSH_PASS=" - Password for connecting via SSH (user `root`). If it is not specified, the SSH service will not be installed.
- "MONIKER=" - Node name.
- "VALIDATOR_KEY_JSON_BASE64=" - Paste the contents of the `priv_validator_key.json` file encrypted with BASE64 *.
```
> *If you want to deploy an **RPC** node without a validator key - missing delete this environment `VALIDATOR_KEY_JSON_BASE64`. The node runs on the generated `priv_validator_key.json`.

If you deployed the project node yourself, then here is a list of available environment in `deploy.yml`: <br/>
```
- "GITHUB_REPOSITORY=" - Link to the project repository that will be cloned into the container and inside which
                           getting a compilation of a binary file.
- "BINARY_LINK=" link to compiled binary file or archive with it.*
- "BINARY_VERSION=" The version or commit of the binary you want to compile (can only use
                      with GITHUB_REPOSITORY populated).
- "RPC=" - External RPC node used to check STATE SYNC, find effective peers, read GENESIS file.
- "GENESIS=" - Link to genesis.json file. With this capability, reading from RPC will be disabled.
- "PEERS=" - Enter a list of peers separated by commas, in this case, automatic search will be disabled.
- "SEEDS=" - Enter a list of seeds separated by commas.
- "DENOM=" - Manual setting of the nominal value of the token.
- "CHAIN=" - Manual setting of chain-id.
- "STATE_SYNC=off" - disable state sync.
- "SNAPSHOT=" - Link to lz4 network snapshot archive. Use in conjunction with STATE_SYNC=off.
- "PRUNING=off" - disable pruning. If you leave the variable empty - pruning will be enabled, you can add
                    KEEP_RECENT and INTERVAL values, if needed. The default values are KEEP_RECENT=1000 and INTERVAL=10
- "SNAPSHOT_INTERVAL" - in a large interval of snapshots, the default value is 2000.
- "DISABLE_RPC=off" - public RPC on host, port 26657 will become available.

* When building BINARY_LINK, you must add a BINARY variable - containing the name
binary file.

```
If you don't have `priv_validator_key.json`, refer to [this manual](/English/Create_validator_key_CosmosSDK.md).

By going to the forwarded port **26657**, in the `LEASES` tab, you can view `websocket` of the node, where its up-to-date information was available.

<div align="center">

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032797-70a74454-75dd-4910-8a30-9a88a1715531.png" width=45% align="left"</p>
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032818-069eef95-8242-459f-b503-ad8322261482.png" width=45% </p>

</div>

If you need to **create** a validator `priv_validator_key.json` then - next point.

[Up](/English/Deploy_CosmosSDK_node.md#validator-node-based-on-cosmos-sdk-deployment-to-akash-network)

## Create a validator:

Connect to the worker node via **SSH** protocol using forwarded port **22**, user **root** and password set in **deploy.yml**:
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032966-3fa2ffae-5348-4a2c-a4e8-5d33c57ba320.png" width=60% </p>
  
Of the check status if `false` means the node is **synchronized**:
  
```
curl -s localhost: 26657/status | jq .result.sync_info.catch_up
```

If the node is **synchronized** - run:

```
source ~/.bashrc && wget -q -O create_validator.sh https://raw.githubusercontent.com/Dimokus88/universe/main/script/create_validator.sh && chmod +x c
reate_validator.sh && sudo /bin/bash create_validator.sh
```

Follow the script execution prompts.

When the validator is created, request the remaining balance:

```
$BINARY q bank balances $address
```

You can delegate the remaining tokens to yourself, but leave a small part to pay for transaction gas:

```
$BINARY tx staking delegate $valoper <amount>$DENOM --from $address --chain-id $CHAIN --fees 555$DENOM -y
```

* Collect rewards:

```
$BINARY tx distribution withdraw-rewards $valoper --from $address --fees 500$DENOM --commission --chain-id $CHAIN -y
```
Other commands for managing a node [can be found here](/English/Command_Cosmos_SDK.md).

[Up](/English/Deploy_CosmosSDK_node.md#validator-node-based-on-cosmos-sdk-deployment-to-akash-network)

**Thank you for using Akash Network!**
___
