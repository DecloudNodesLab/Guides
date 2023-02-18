<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>
 
# Command templates for CLI projects based on Cosmos SDK.

> $BINARY - here is the binary file of the project, each has its own, like denom and chain-id

  1. [Account (wallet) commands](/English/Command_Cosmos_SDK.md#account-wallet-commands)
  2. [Validator commands](/English/Command_Cosmos_SDK.md#validator-commands)
  3. [Voting commands](/English/Command_Cosmos_SDK.md#voting-commands)
  4. [Network settings commands](/English/Command_Cosmos_SDK.md#network-settings-commands)

 
> P.S. The [Nodejumper](https://nodejumper.io/) project team have created a great command generator, we recommend that you take a look at the example of the [Omniflix generator](https://nodejumper.io/omniflix/cheat-sheet).
___
## Account (wallet) commands

Create wallet:

```
$BINARY keys add <WALLET_NAME> --keyring-backend os
```

Restore wallet (after insert seed command):

```
$BINARY keys add <WALLET_NAME> --recover --keyring-backend os
```

Check balance:

```
$BINARY q bank balances <ADDRESS>
```

Send 1 token to another address:

```
$BINARY tx bank send <SENDER_ADDRESS> <RECEIVER_ADDRESS> 1000000$DENOM --fees 500$DENOM -y
```

[Up](/English/Command_Cosmos_SDK.md#command-templates-for-cli-projects-based-on-cosmos-sdk) .

___

## Validator commands

Create a validator

```
$BINARY tx staking create-validator --amount="1000000$DENOM" --pubkey=$($BINARY tendermint show-validator) --moniker="$MONIKER" --chain-id="$CHAIN" --commission -rate="0.10" --commission-max-rate="0.20" --commission-max-change-rate="0.01" --min-self-delegation="1000000" --gas="auto" -- from="$address" --fees="555$DENOM" -y
```

Check validator pubkey

```
$BINARY tendermint show-validator
```

Check validator

```
$BINARY query staking validator <valoper_address>
```

```
$BINARY query staking validators --limit 1000000 -o json | jq '.validators[] | select(.description.moniker=="$MONIKER")' | jq
```
  
Collect commissions + rewards

```
$BINARY tx distribution withdraw-rewards <valoper_address> --from <ADDRESS> --fees 500$DENOM --commission -y
```

Delegate 1,000,000 'u' token to yourself

```
$BINARY tx staking delegate <valoper_address> 1000000$DENOM --from <ADDRESS> --fees 500$DENOM -y
```

[Up](/English/Command_Cosmos_SDK.md#command-templates-for-cli-projects-based-on-cosmos-sdk) .
  
___

## Voting commands
  
Proposals list

```
$BINARY q gov proposals
```
  
View the result of the vote

```
$BINARY q gov proposals --voter <ADDRESS>
```
  
Vote 'yes' for the proposal №1

```
$BINARY tx gov vote 1 yes --from <ADDRESS> --fees 555$DENOM
```
  
Make a deposit to the offer

```
$BINARY tx gov deposit 1 1000000$DENOM --from <ADDRESS> --fees 555$DENOM
```

Create an offer

```
$BINARY tx gov submit-proposal --title="Randomly reward" --description="Reward 10 testnet participants who completed more than 3 tasks" --type="Text" --deposit="11000000$DENOM" --from <ADDRESS> --fees 500$DENOM
```
  
[Up](/English/Command_Cosmos_SDK.md#command-templates-for-cli-projects-based-on-cosmos-sdk) .
  
  
___

## Network settings commands
  
Network settings

```
$BINARY q staking params
```

```
$BINARY q slashing params
```

Get out of jail

```
$BINARY tx slashing unjail --from <ADDRESS> --fees 500$DENOM -y
```

```
$BINARY q slashing signing-info $($BINARY tendermint show-validator)
```

Check Status

```
curl localhost:26657/status
```

[Up](/English/Command_Cosmos_SDK.md#command-templates-for-cli-projects-based-on-cosmos-sdk) .

___
