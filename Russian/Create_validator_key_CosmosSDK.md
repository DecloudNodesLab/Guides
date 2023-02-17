# Создание priv_validator_key.json

Так как, ноды экосистемы **Cosmos SDK** стандартизированны - то и файл `priv_validator_key.json` будет подходить к проектам Cosmos.

Если у вас еще нет этого файла - разверните через **Cloudmos** ([инструкция и пример использования здесь](/Russian/Cloudmos(Akashlytics).md)) этот [deploy.yaml](https://github.com/DecloudNodesLab/Projects/blob/main/CosmosSDK/get_validator_key.yaml) .

- После окончания развертывания, в вкладке `LOG-LOG` скопируйте вывод между полями `===CUT HERE===` в текстовый файл на ваше локальное устройство:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/187510333-291e1df8-85dc-492f-8a0a-36000354d857.png" width=60% </p>

Возможно, у вас скопируется `app:` что является лишним в файле. Приведите содержимое файла к виду:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/187510935-d52ba819-e3f7-4711-846f-fdd2d16faf84.png" width=60% </p>

Сохраните файл под именем `priv_validator_key.json` , теперь вы его можете использовать для любых нод экосистемы **Cosmos SDK** .

Закройте деплоймент, `5 АКТ` вернутся на счет:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/187511436-c7628eb1-68d2-4018-891b-cf8ca11ebbed.png" width=60% </p>

