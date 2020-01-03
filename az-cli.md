# Web App
``` bash
# Create a Webapp from a Container Image
az group create -n <group> -l <location>
az appservice plan create -n <asp> -g <group> --sku <sku> --is-linux
az webapp create -g <group> -p <asp> -n <site> -i <image>
```

# Virtual Machines
``` bash
# show the public ip
az vm show -n <name> -g <group> -d --query publicIps


# create and attach a new managed disk to a vm
az vm disk attach -g <group> --vm-name <vm> --name <disk> --new --size-gb <size>

# detach a disk
az vm disk detach -g <group> --vm-name <vm> -n <disk>

# delete the disk
az disk delete -g <group> -n <disk>

```

# Azure Database for MySQL

``` bash
# Create Server and Database
az mysql server create -g foo -n foo-mysql -l westus2 -u myadmin -p abcd1234! --sku-name GP_Gen5_2 --version 5.7
az mysql db create -n drupal -g foo -s foo-data

# Turn Off SSL Enforcement
az mysql server update -g foo -n foo-data --ssl-enforcement Disabled

# Delete Database
az mysql db delete -n drupal -s foo-data -g foo

# Get Properties
az mysql server show -n foo-data -g foo -o json
```

# Azure Service Bus


## Create a subscription (with sessions)
az servicebus topic subscription create -g x --namespace-name x --topic-name x -n car1 --enable-session

## Delete a subscription
az servicebus topic subscription delete -g x --namespace-name x --topic-name x -n car1

## Create a subscription rule
az servicebus topic subscription rule create -g ehrx --namespace-name exrxsb --topic-name messages --subscription-name car1 --name carId --filter-sql-expression carId=1

# IoT Hub

# Storage

## Batch download blobs
``` bash
az storage blob download-batch -d . -s <container> --account-name $ACCOUNT_NAME --account-key $ACCOUNT_KEY
```

##