# Azure Service Princial y politica de KV

## Generar un credenciales de Azurepara terraform y KV

```bash
SubscriptionID=
RG_NAME=ContosoResourceGroup
LOCATION="EAST US"
KV_NAME=ContosoKeyVault

## Generar el SP que puedo actuar a nive del subscripcion
#az ad sp create-for-rbac --name "my-sp-name" --role contributor --scopes /subscriptions/${SubscriptionID}

## Generar un group de recursos
az group create -n $RG_NAME -l $LOCATION

## Generar un KV en el grupo de recursos
az keyvault create --name $KV_NAME --resource-group $RG_NAME --location $LOCATION

## Crear un secreto en el KV
az keyvault secret set --vault-name $KV_NAME --name "SQLPassword" --value "hVFkk965BuUv "

## Autorizar al SP a obtener los secretos de KV
az keyvault set-policy --name $KV_NAME --spn $SPN --secret-permissions get
```

## Documentos de referencia

- https://docs.microsoft.com/en-us/azure/key-vault/general/manage-with-cli2
