<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>
 
# Шаблоны команд для CLI проектов на базе Cosmos SDK.

> $BINARY - здесь бинарный файл проекта, у каждого он свой, как и denom и chain-id

 1. [Команды аккаунта (кошелька)](/Russian/Command_Cosmos_SDK.md#команды-аккаунта-кошелька)
 2. [Команды валидатора](/Russian/Command_Cosmos_SDK.md#команды-валидатора)
 3. [Команды голосования](/Russian/Command_Cosmos_SDK.md#команды-голосованияs)
 4. [Команды настроек сети](/Russian/Command_Cosmos_SDK.md#команды-настроек-сети)
 
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

[Наверх](/Russian/Command_Cosmos_SDK.md#шаблоны-команд-для-cli-проектов-на-базе-cosmos-sdk) .

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

[Наверх](/Russian/Command_Cosmos_SDK.md#шаблоны-команд-для-cli-проектов-на-базе-cosmos-sdk) .
  
___

## Команды голосования
  
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
  
[Наверх](/Russian/Command_Cosmos_SDK.md#шаблоны-команд-для-cli-проектов-на-базе-cosmos-sdk) .
  
  
___

## Команды настроек сети
  
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

[Наверх](/Russian/Command_Cosmos_SDK.md#шаблоны-команд-для-cli-проектов-на-базе-cosmos-sdk) .

___
