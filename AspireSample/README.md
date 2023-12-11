# .NET Aspire sample application

## Summary

App is created with command `dotnet new aspire-starter --use-redis-cache --output AspireSample`.

To create `manifest.json` file, cd into *.AppHost folder and run command `dotnet run --publisher manifest --output-path manifest.json`

## Infrastructure

To init `azd` environment, used command `azd init`, select `Use code in directory`, selected confirm and selected `webfrontend` as service that is exposed to internet. Name of environment set as `aspire-sample-sandbox` as this name will be used for resource group name, so that it is not generic environment name, but includes app name as well.

