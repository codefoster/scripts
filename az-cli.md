## Web App
``` bash
# Create a Webapp from a Container Image
az group create -n foo -l westus
az appservice plan create -n foo-asp -g foo --sku B1 --is-linux
az webapp create -g foo -p foo-asp -n foo-site -i drupal
```

## Virtual Machines
``` bash
# show the public ip
az vm show -n ubuntu -g unwesteurope -d --query publicIps


# create and attach a new managed disk to a vm
az vm disk attach -g <resource group> --vm-name <vm name> --name <disk name> --new --size-gb <size>

# detach a disk
az vm disk detach -g <resource group> --vm-name <vm name> -n <disk name>

# delete the disk
az disk delete -g <resource group> -n <disk name>

```

## Azure Database for MySQL

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