<div align="center">
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>
  
# Обзор и руководство по использованию кастомного пользовательского web интерфейса Cloudmos.


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

| [English guide](/English/Cloudmos.md) | 
|:--:|  
</div>

___

#### В этой статье:
1. [Подключение аккаунта и подготовка к работе](/Russian/Cloudmos.md#подключение-аккаунта-и-подготовка-к-работе).
2. [Создать развертывание](/Russian/Cloudmos.md#%D1%82%D0%B5%D1%81%D1%82%D0%BE%D0%B2%D0%BE%D0%B5-%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5).
3. [Содержимое окна разветывания](/Russian/Cloudmos.md#%D1%81%D0%BE%D0%B4%D0%B5%D1%80%D0%B6%D0%B8%D0%BC%D0%BE%D0%B5-%D0%BE%D0%BA%D0%BD%D0%B0-%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F)
4. [Закрыть развертывание](/Russian/Cloudmos.md#%D0%B7%D0%B0%D0%BA%D1%80%D1%8B%D1%82%D1%8C-%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)
5. [Обзор Cloudmos](/Russian/Cloudmos.md#обзор-функционала-cloudmos)

___

## Подключение аккаунта и подготовка к работе.

Авторизуйтесь на [web UI Cloudmos](https://deploy.cloudmos.io/) с помощью приложения Keplr:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221588325-7ef4f756-4706-4106-8a3a-839034782469.gif" width=70% </p>


  
 > Пополните счет AKT. Следует учитывать, что при каждом развертывании на счете блокируются ***5 AKT*** + требуется небольшое количество AKT для оплаты газа. Таким образом, для теста достаточно пополнить счет на ***6 АКТ***. Токен АКТ можно пробрести на биржах ```Gate```, ```AsendeX```, ```Osmosis``` . 
  

### Создание сертификата
  
После того как счет АКТ пополнен - необходимо запросить и установить сертификат из блокчейна, для этого:
  
1. Справа вверху нажмите ***CREATE CERTIFICATE***  
2. Выберите комисиию за транзакцию и поддтвердите транзакцию.

Сертификат создан, Вы можете его увидеть в правом верхнем углу окна.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221591238-e1858e2f-eb8f-4ff1-a01b-269dbb91e1af.gif" width=70% </p>

Подготовка завершена, теперь сделаем тестовое разветывание.

[Вернуться к содержанию.](/Russian/Cloudmos.md#%D0%B2-%D1%8D%D1%82%D0%BE%D0%B9-%D1%81%D1%82%D0%B0%D1%82%D1%8C%D0%B5)
  
___

## Тестовое развертывание

В ***Cloudmos*** есть готовые файлы ***манифеста (deploy.yml)***, они находятся во вкладке ```Templates```, ознакомьтесь с предложением готовых решений: 

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221591869-b37798b8-76d6-476f-8c3d-ec8be35683db.png" width=60% </p>

Развернем всем известную игру ***Super Mario***, для этого выберем соответствующий раздел ***Games*** в ```Templeates``` и нажмем на ```Super Mario```:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221592345-5eb3f69a-c391-40e1-8d3b-203d7a87069d.png" width=60% </p>

Нажимаем ***Deploy***: 

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221592527-cc96d385-e682-4ad8-bd47-e2308f9116df.png" width=60% </p>

***Cloudmos*** быстро проверяет наличие сертификата и ***5 АКТ*** на балансе, и открывает заполненное окно ***манифеста (deploy.yml)***, остановимся на содержимом манифеста:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221593433-2e94845d-3db2-4adf-acf8-672570b6340c.png" width=60% </p>

Здесь обратите внимание на:

Раздел ```services``` (строки 4-11). В строке 6 указан образ в ***Docker hub*** из которого будет развернут контейнер, в нашем случае это ```pengbai/docker-supermario```. Подраздел ***expose*** отвечает за открытия и переадресацию портов. В нашем случае порт 8080 представляем, как 80 внешний.

Раздел ```profiles``` (строки 13-22) здесь в подразделе ```resources``` мы указываем арендуемые характеристики оборудования под наш контейнер с игрой ***Super Mario***. В нашем случае это ```1 cpu, 512 мб ОЗУ и 512мб жесткого диска```. Задайте ввеху имя развертывания и нажимите ***CREATE DEPLOYMENT***.
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221593892-f1385fd5-5d68-45e3-b74a-c0bec7a9e6bc.png" width=30% </p>

Депонируем ***5 АКТ*** из нашего счета, нажимаем ```DEPOSIT```:

Устанавливаем размер комиссии за транpакцию и подтверждаем ее. На данном этапе мы отправили в сеть запрос на мощности для нашего конетйнера с игрой. Нам остается дождаться ответа от провайдеров с их предложениями и ценами. ***Обратите внимание, у Вас со счет были депонированы 5 АКТ***.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221594641-9f02b27b-04b6-4459-9108-ebb852b40434.png" width=90% </p>

Выбираем провайдера и нажимаем ```ACCEPT BID```, еще раз устанавливаем комиссию для транзакиции и подтверждаем ее. Дожидаемся развертки контейнера. После того, как контейнер развернут, перейдите на вкладку ```LEASES```.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221595596-3e2ecd06-2b3a-462b-97db-c8e3466f3c41.png" width=80% </p>

Здесь доступна информация о Вашем провайдере, стоимости аренды, а также индивидуальная ссылка на Ваше развертывание. Нажмите на нее.
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/179998220-473b42ec-144f-4bff-b640-801fc727983b.png" width=60% </p>

Отлично! Похоже, Вы развернули игру в Akash Network! Но Вам же нужно нечто большее, чем игра? Тогда перейдите к разделу описания функционала ***Cloudmos(Akashlytics)*** =)
  
[Вернуться к содержанию.](/Russian/Cloudmos.md#%D0%B2-%D1%8D%D1%82%D0%BE%D0%B9-%D1%81%D1%82%D0%B0%D1%82%D1%8C%D0%B5)
  
___  
  
## Содержимое окна развертывания

Во вкладке ```Dashboard``` отображаются Ваши активные разветывания, зайдите в него.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596081-3ec6f4eb-2987-4aff-b0dd-33fe2ba045f6.png" width=100% </p>

Как узнали раннее, во вкладке ```LEASES``` содержится общая информация о развертывании - провайдер, ресурсы, переадресованный порты и ссылки.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596340-5d4a87b7-3d53-47d3-a00e-d50fadfbaf5a.png" width=100% </p>

Во вкладке ```LOGS``` есть еще 2 подраздела, это подраздел ```LOGS``` - здесь отображаются логи ***ВНУТРИ*** контейнера (нажав кнопку ```DOWNLOADS LOGS```, можно их скачать в файл):

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596683-75800c6a-1a59-4753-84ab-45c7ac0463fa.png" width=100% </p>

и подраздел ```EVENTS``` - здесь отображаются логи ***k8s***, процесс скачивания и старта вашего образа:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596900-39597059-c8f2-4d5a-a1af-b3955c04f7ce.png" width=100% </p>

На вкладке ```SHELL``` можете использовать некоторые ***НЕ интерактивные*** команды внутри контейнера
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221597223-d678a85b-7091-4cc2-bfa1-2d3e4d24a7e5.png" width=100% </p>

Вкладка ```UPDATE``` содержит текущий ***манифест (deploy.yml)***, здесь Вы можете добавить переменные или изменить версию образа, в этом случае контейнер будет перезапущен. ***(ВАЖНО! Нельзя изменить ресурсы! Для этого надо закрыть равертывание и развернуть заново!).***
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221597762-983bbe87-d4a9-41fe-828c-a059a7346736.png" width=100% </p>

Вкладка ```RAW DATA``` содержит ```JSON``` информацию из блокчейна ```AKASH```
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221598012-a444a5c6-0a98-4d35-9ce8-0cf63579eb28.png" width=100% </p>

[Вернуться к содержанию.](/Russian/Cloudmos.md#%D0%B2-%D1%8D%D1%82%D0%BE%D0%B9-%D1%81%D1%82%D0%B0%D1%82%D1%8C%D0%B5)

___
  
 
## Закрыть развертывание

Чтобы закрыть развертывание, необходимо в контекстном меню нажать ```CLOSE``` и подтвердить транзакцию


<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221598510-9450f1ae-5b2c-4037-bb79-cc24d0d03a36.png" width=100% </p>

После закрытия развертывание остаток ***АКТ*** вернется на Ваш основной счет.
  
[Вернуться к содержанию.](/Russian/Cloudmos.md#%D0%B2-%D1%8D%D1%82%D0%BE%D0%B9-%D1%81%D1%82%D0%B0%D1%82%D1%8C%D0%B5)

___

  
### Обзор функционала Cloudmos.
  
***Dashboard*** - здесь указаны актуальные параметры Вашего счета(1), текущее состояние аренды в сети(2) и Ваши активные развертывания(3).

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599302-10794063-abb5-4303-9f59-f501a8561740.png" width=60% </p>

***Deployments*** - все, когда-либо созданные, разветывания на Вашем адресе, включая не активные.

  <p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599517-615a7796-bae8-4cba-8c96-acae9de506a8.png" width=60% </p>

***Templates*** - готовые решения для развертываний, игры, БД, конструкторы сайтов, майнер и т.д..

  <p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599709-f8969486-a26d-408c-9aac-671dfcff9b32.png" width=60% </p>
  
***Provider*** - список существующих провайдеров в маркетплейсе Akash Network с параметрами их оборудования.

 <p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599849-e1cf4f85-d25a-418e-a4b5-077634d2ebf0.png" width=60% </p> 

***Settings*** - настройка RPC ноды приложения (1). Так же доступно быстрое переключение в поле вверху окна (2).

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221600341-ecb778bd-857e-420e-b13d-b7ff4f22e8ec.png" width=60% </p>
  
[Вернуться к содержанию.](/Russian/Cloudmos.md#%D0%B2-%D1%8D%D1%82%D0%BE%D0%B9-%D1%81%D1%82%D0%B0%D1%82%D1%8C%D0%B5)

___
