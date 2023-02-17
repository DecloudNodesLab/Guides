<div align="center">
  
# Нода валидатора (стандарта Cosmos SDK), развертка в Akash Network.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/163564929-166f6a01-a6e2-4412-a4e9-40e54c821f05.png" width=70% </p>

| [Akash Network](https://akash.network/) | [Forum Akash Network](https://forum.akash.network/) | 
|:--:|:--:|
___

Прежде чем начать - подпишитесь на наши новостные каналы:

| [Discord Akash](https://discord.gg/ybKMsYYZkx) | [Telegram Akash EN](https://t.me/AkashNW) | [Telegram Akash RU](https://t.me/akash_ru) | [TwitterAkash](https://twitter.com/akashnet_) | [TwitterAkashRU](https://twitter.com/akash_ru) |
|:--:|:--:|:--:|:--:|:--:|

</div>
 
<div align="center">
  
[English version](/English/Deploy_CosmosSDK_node.md)
  
</div>

___

### Развертка ноды:

Выберите проект и разверните файл [deploy.yml](https://github.com/DecloudNodesLab/Projects/tree/main/CosmosSDK) ноды с помощью **Cloudmos (Akashlytics)**  ([инструкция по использованию здесь](/Russian/Cloudmos(Akashlytics).md)) установив значения в соответствующих переменных  `deploy.yml`: 
- **SSH_PASS** - Пароль для подключения по SSH (пользователь `root`) 
- **MONIKER**-имя ноды  
- **VALIDATOR_KEY_JSON_BASE64**-Вставьте содержимое файла `priv_validator_key.json` зашифрованное с помощью **BASE64** *.

Если у вас нет `priv_validator_key.json` - обратитесь [к этой инструкции](/Russian/Create_validator_key_CosmosSDK.md). 

> *Если вы хотите развернуть **RPC** ноду без ключа валидатора - оставьте `LINK_KEY` пустым или вовсе удалите эту строку. Нода запустится на сгенерированном `priv_validator_key.json`. 

На данном этапе нода развернута . Перейдя на переадресованный порт **26657** во вкладке `LEASES` откроется `websocket` ноды, где будет доступна ее актуальная информация. 
  


<div align="center">

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032797-70a74454-75dd-4910-8a30-9a88a1715531.png" width=45% align="left"</p>
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032818-069eef95-8242-459f-b503-ad8322261482.png" width=45% </p>

</div>

Если вам нужно **создать** валидатора на вашем `priv_validator_key.json` перейдите к следующему пункту.

### Создание валидатора:

Подключитесь к работающей ноде по протоколу **SSH**, используя переадресованный **22** порт, пользователь **root** и пароль заданный вами в **deploy.yml**:
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032966-3fa2ffae-5348-4a2c-a4e8-5d33c57ba320.png" width=60% </p>
  
Проверьте статус синхронизации, если `false` значит нода **синхронизированна**:
  
```
curl -s localhost:26657/status | jq .result.sync_info.catching_up
```

Если нода **синхронизированна** - выполните:

```
source ~/.bashrc && wget -q -O create_validator.sh https://raw.githubusercontent.com/Dimokus88/universe/main/script/create_validator.sh && chmod +x create_validator.sh && sudo /bin/bash create_validator.sh
```

Следуйте подсказкам выполнения скрипта.

Когда валидатор будет создан запросите оставшийся баланс:

```
$BINARY q bank balances $address
```

Можете делегировать на себя оставшиеся токены, но оставьте небольшую часть для оплаты газа транзакций:

```
$BINARY tx staking delegate $valoper <amount>$DENOM --from $address --chain-id $CHAIN --fees 555$DENOM --home /root/$BINARY/ -y
```

* Собрать награды:

```
$BINARY tx distribution withdraw-rewards $valoper --from $address --fees 500$DENOM --commission --chain-id $CHAIN --home /root/$BINARY/ -y
```
Другие команды по управлению нодой [можете найти здесь](https://github.com/Dimokus88/Akash-Nodes-Lab/blob/main/Guide/Command_Cosmos_SDK.md).

[К началу](https://github.com/Dimokus88/Crowd_Control/blob/main/README.md#Crowd_Control-validator-node-on-akash-network)

**Спасибо что воспользовались Akash Network!**
___


