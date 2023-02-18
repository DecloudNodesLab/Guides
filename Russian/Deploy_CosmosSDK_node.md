<div align="center">

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>

# Нода валидатора (стандарта Cosmos SDK), развертка в Akash Network.
</div>
<div align="center">
  
| [Twitter Decloud Nodes Lab](https://twitter.com/NodesLab) | 
|:--:|

| [Akash Network](https://akash.network/) | [Forum Akash Network](https://forum.akash.network/) | 
|:--:|:--:|
___

Наши новостные каналы и русскоязычная техническая поддержка:

| [Discord Akash](https://discord.akash.network/) | [Telegram Akash EN](https://t.me/AkashNW) | [Telegram Akash RU](https://t.me/akash_ru) | [TwitterAkash](https://twitter.com/akashnet_) | [TwitterAkashRU](https://twitter.com/akash_ru) |
|:--:|:--:|:--:|:--:|:--:|

Перед началом ознакомления ***[скачайте и установите](https://cloudmos.io/cloud-deploy) ПО Cloudmos(Akashlytics)*** на свой рабочий компьютер.
  
</div>
 
<div align="center">
  
[English version](/English/Deploy_CosmosSDK_node.md)
  
</div>

___

## Развертка ноды:

Выберите проект и разверните файл [deploy.yml](https://github.com/DecloudNodesLab/Projects/tree/main/CosmosSDK) ноды с помощью **Cloudmos (Akashlytics)**  ([инструкция по использованию здесь](/Russian/Cloudmos(Akashlytics).md)).
Если вы используете проекты которые мы подготовили, то Вам достаточно внести свои значения в переменные указанные ниже в `deploy.yml`, остальные оставьте неизменными: <br/>
```
- "SSH_PASS="  - Пароль для подключения по SSH (пользователь `root`). Если его не указать - служба SSH не будет установлена.
- "MONIKER=" - Имя ноды.
- "VALIDATOR_KEY_JSON_BASE64=" - Вставьте содержимое файла `priv_validator_key.json` зашифрованное с помощью **BASE64** *.
```
Если вы самостоятельно разворачиваете ноду проекта, то вот список доступных переменных для изменения в  `deploy.yml`: <br/>
```
- "GITHUB_REPOSITORY=" - Ссылка на репозиторий проекта, который будет клонирован в контейнер и внутри которого 
                         произойдет компиляция бинарного файла.
- "BINARY_LINK=" ссылка на скомпилированный бинарный файл или архив с ним.* 
- "BINARY_VERSION=" Версия или коммит бинарного файла, который вы хотите скомпилировать(может использываться только 
                    с заполненным GITHUB_REPOSITORY).
- "RPC=" - Внешняя RPC нода, используется для синхронизации STATE SYNC, поиска актуальных пиров, считывания GENESIS файла.
- "GENESIS=" - Ссылка на файл genesis.json. При наличии этой переменной автоматическоесчитывание из RPC будет отключено.
- "PEERS=" - Внесите список пиров через запятую,в этом случае автоматический поиск будет отключен.
- "SEEDS=" - Внесите список сидов через запятую.
- "DENOM=" - Ручная установка denom токена.
- "CHAIN=" - Ручная установка chain-id.
- "STATE_SYNC=off" - отключение синхронизации state sync.
- "SNAPSHOT=" - Ссылка на архив снепшот сети формата lz4. Использовать в паре с STATE_SYNC=off.
- "PRUNING=off" - отключение пруннинга. Если оставить переменную пустой - пруннинг будет включен, можно добавить 
                  значения  KEEP_RECENT и INTERVAL при необходимости. Значения по-умолчанию KEEP_RECENT=1000 и INTERVAL=10
- "SNAPSHOT_INTERVAL" - в ручную задать интервал снепшотов, по-умолчанию значение равно 2000.
- "DISABLE_RPC=off" - отключить RPC на ноде, порт 26657 станет недоступным.

* При использовании BINARY_LINK необзодимо дополнительно добавить переменную BINARY - содержащую имя 
бинарного файла. Если ее не установить - имя бинарного файла будет задано как "serviced".

```
Если у вас нет `priv_validator_key.json` - обратитесь [к этой инструкции](/Russian/Create_validator_key_CosmosSDK.md). 

> *Если вы хотите развернуть **RPC** ноду без ключа валидатора - оставьте `VALIDATOR_KEY_JSON_BASE64` пустым или вовсе удалите эту строку. Нода запустится на сгенерированном `priv_validator_key.json`. 

На данном этапе нода развернута . Перейдя на переадресованный порт **26657** во вкладке `LEASES` откроется `websocket` ноды, где будет доступна ее актуальная информация. 

<div align="center">

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032797-70a74454-75dd-4910-8a30-9a88a1715531.png" width=45% align="left"</p>
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032818-069eef95-8242-459f-b503-ad8322261482.png" width=45% </p>

</div>

Если вам нужно **создать** валидатора на вашем `priv_validator_key.json` перейдите к следующему пункту.

## Создание валидатора:

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
$BINARY tx staking delegate $valoper <amount>$DENOM --from $address --chain-id $CHAIN --fees 555$DENOM  -y
```

* Собрать награды:

```
$BINARY tx distribution withdraw-rewards $valoper --from $address --fees 500$DENOM --commission --chain-id $CHAIN -y
```
Другие команды по управлению нодой [можете найти здесь](https://github.com/Dimokus88/Akash-Nodes-Lab/blob/main/Guide/Command_Cosmos_SDK.md).

[К началу](https://github.com/Dimokus88/Crowd_Control/blob/main/README.md#Crowd_Control-validator-node-on-akash-network)

**Спасибо что воспользовались Akash Network!**
___


