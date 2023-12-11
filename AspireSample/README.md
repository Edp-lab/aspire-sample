# .NET Aspire sample application

## Summary

App is created with command `dotnet new aspire-starter --use-redis-cache --output AspireSample`.

To create `manifest.json` file, cd into *.AppHost folder and run command `dotnet run --publisher manifest --output-path manifest.json`

## Environment

To init `azd` environment, used command `azd init`, select `Use code in directory`, selected confirm and selected `webfrontend` as service that is exposed to internet. Name of environment set as `aspire-sample-sandbox` as this name will be used for resource group name, so that it is not generic environment name, but includes app name as well.

For some reason, it will not enabled the selected service `webfrontend` as exposed to internet. To do it manually, go to generated `.azure` folder and open file `/aspire-sample-sandbox/config.json` and change so that `"exposedServices": ["webfrontend"]`.

For now, there is some bug that deploying with external ingress does not work. So in file `AspireSample.Web/manifests/containerApp.tmpl.yaml` you have to change the property `properties.configuration.ingress.external` to `false` and then log in to Azure Portal, go to theContainer app, In Overview tab, on right hand side under Networking, click in Ingress Enabled. Then select mark check-box Ingress Enabled to expose the service to the internet.

## Infrastructure

To generate yaml deployment files, execute command `azd infra synth`, this creates:
    - containerApp deployment files for each service in each projects directory under `/manifests/containerApp.tmpl.yaml`;
    - `main.bicep`, `main.parameters.json` and `resources.bicep` files for infrastructure code.

By default, resource names will be a prefix of resource type followed by a random string of characters. To give meaningful names to resources, modify `infra/resources.bicep` file where resources are declared.

To provision the infrastructure, run command `azd provision`

To deploy your apps to the new infra, run command `azd deploy`

To deploy a single service from your stack, run command `azd deploy {{SERVICE_NAME}}`, replace `{{SERVICE_NAME}}` with your service name, e.g., `azd deploy webfrontend` 
