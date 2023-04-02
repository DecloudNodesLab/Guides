<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" width=90% </p>

# Create priv_validator_key.json

Since the nodes of the **Cosmos SDK** ecosystem are standardized, the `priv_validator_key.json` file will also be suitable for Cosmos projects.

If you don't have this file yet - use **Cloudmos** to deploy this [deploy.yaml](https://github.com/DecloudNodesLab/Projects/blob/main/CosmosSDK/get_validator_key.yaml) .

- After deployment is complete, in the `LOG-LOG` tab, copy the output between the `===CUT HERE===` fields to a text file on your local device:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/187510333-291e1df8-85dc-492f-8a0a-36000354d857.png" width=60% </p>

You may have copied `app:` which is redundant in the file. Change the contents of the file to:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/187510935-d52ba819-e3f7-4711-846f-fdd2d16faf84.png" width=60% </p>

Save the file as `priv_validator_key.json` , now you can use it for any node in the **Cosmos SDK** ecosystem.

Close the deployment, `5 AKT` will be returned to the account:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/187511436-c7628eb1-68d2-4018-891b-cf8ca11ebbed.png" width=60% </p>
