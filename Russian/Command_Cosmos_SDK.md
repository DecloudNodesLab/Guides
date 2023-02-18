<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>
 
# Шаблоны команд для CLI проектов на базе Cosmos SDK.

> $BINARY - здесь бинарный файл проекта, у каждого он свой, как и denom и chain-id

 1. [Команды аккаунта (кошелька)](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#account-wallet-commands)
 2. [Команды валидатора](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#validator-commands)
 3. [Команды голосования](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#voting-commands)
 4. [Команды настроек сети](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#network-settings-commands)
 
___
## Команды аккаунта (кошелька)

Cоздать кошелек:

```
$BINARY keys add <WALLET_NAME> --keyring-backend os
```

Восстановить кошелек (после команды вставить seed):

```
$BINARY keys add <WALLET_NAME> --recover --keyring-backend os
```

Проверить баланс:

```
$BINARY q bank balances <ADDRESS>
```

Отправить 1 токен на другой адрес:

```
$BINARY tx bank send <АДРЕС_ОТПРАВИТЕЛЯ> <АДРЕС_ПОЛУЧАТЕЛЯ> 1000000$DENOM --fees 500$DENOM -y
```

[Наверх](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#commands-for-the-command-line-of-cosmos-sdk-ecosystem-projects) .

___

## Команды валидатора

Создать валидатора

```
$BINARY tx staking create-validator --amount="1000000$DENOM" --pubkey=$($BINARY tendermint show-validator) --moniker="$MONIKER"	--chain-id="$CHAIN"	--commission-rate="0.10" --commission-max-rate="0.20" --commission-max-change-rate="0.01" --min-self-delegation="1000000" --gas="auto"	--from="$address" --fees="555$DENOM" -y
```

Проверить pubkey валидатора

```
$BINARY tendermint show-validator
```

Проверить валидатора

```
$BINARY query staking validator <valoper_address>
```

```
$BINARY query staking validators --limit 1000000 -o json | jq '.validators[] | select(.description.moniker=="$MONIKER")' | jq
```
  
Собрать комиссионные + реварды

```
$BINARY tx distribution withdraw-rewards <valoper_address> --from <ADDRESS> --fees 500$DENOM --commission -y
```

Заделегировать себе  1 000 000 'u'токен

```
$BINARY tx staking delegate <valoper_address> 1000000$DENOM --from <ADDRESS> --fees 500$DENOM -y
```

[Наверх](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#commands-for-the-command-line-of-cosmos-sdk-ecosystem-projects) .
  
___

#### Команды голосования
  
Список предложений

```
$BINARY q gov proposals
```
  
Посмотреть результат голосования

```
$BINARY q gov proposals --voter <ADDRESS>
```
  
Проголосовать за предложение 

```
$BINARY tx gov vote 1 yes --from <ADDRESS> --fees 555$DENOM
```
  
Внести депозит в предложение

```
$BINARY tx gov deposit 1 1000000$DENOM --from <ADDRESS> --fees 555$DENOM
```

Создать предложение

```
$BINARY tx gov submit-proposal --title="Randomly reward" --description="Reward 10 testnet participants who completed more than 3 tasks" --type="Text" --deposit="11000000$DENOM" --from <ADDRESS> --fees 500$DENOM
```
  
[Наверх](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#commands-for-the-command-line-of-cosmos-sdk-ecosystem-projects) .
  
  
___

#### Команды настроек сети
  
Параметры сети

```
$BINARY q staking params
```

```
$BINARY q slashing params
```

Выбраться из тюрьмы

```
$BINARY tx slashing unjail --from <ADDRESS> --fees 500$DENOM -y
```

```
$BINARY q slashing signing-info $($BINARY tendermint show-validator)
```

Проверить статус

```
curl localhost:26657/status
```

[Наверх](https://github.com/Dimokus88/guides/blob/main/Cosmos%20SDK/COMMAND.MD#commands-for-the-command-line-of-cosmos-sdk-ecosystem-projects) .

___
