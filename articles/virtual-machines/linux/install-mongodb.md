---
title: aaaInstall MongoDB en una VM de Linux con hello CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar MongoDB en un iusing de máquina virtual Linux Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>¿Cómo tooinstall y configurar MongoDB en una VM Linux
[MongoDB](http://www.mongodb.org) es una conocida base de datos NoSQL de código abierto y alto rendimiento. Este artículo muestra cómo tooinstall y configurar MongoDB en una VM de Linux con hello 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](install-mongodb-nodejs.md). Se muestran algunos ejemplos detallados de:

* [Instalación y configuración manuales de una instancia básica de MongoDB](#manually-install-and-configure-mongodb-on-a-vm)
* [Creación de una instancia básica de MongoDB mediante una plantilla de Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Creación de un clúster complejo con particiones de MongoDB con conjuntos de réplicas mediante una plantilla de Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Instalación y configuración manuales de MongoDB en una máquina virtual
MongoDB [proporciona instrucciones de instalación](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuciones de Linux, incluidos Red Hat/CentOS, SUSE, Ubuntu y Debian. Hello ejemplo siguiente se crea un *CentOS* máquina virtual. toocreate este entorno, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

Cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* con un usuario denominado *azureuser* mediante la autenticación de clave pública SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello VM con su propio nombre de usuario y hello `publicIpAddress` aparece en la salida de hello del paso anterior hello:

```bash
ssh azureuser@<publicIpAddress>
```

crear orígenes de la instalación tooadd Hola para MongoDB, un **yum** archivo repositorio como sigue:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Abrir archivo de repositorio de MongoDB Hola para editarlo. Agregue Hola siguientes líneas:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Instale MongoDB mediante **yum** como se indica a continuación:

```bash
sudo yum install -y mongodb-org
```

De forma predeterminada, SELinux está aplicado en las imágenes de CentOS, lo que impide el acceso de MongoDB. Instalar herramientas de administración de directivas y configure SELinux tooallow MongoDB toooperate en su 27017 el puerto TCP predeterminado de la siguiente manera:

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Iniciar servicio de MongoDB hello como sigue:

```bash
sudo service mongod start
```

Comprobar la instalación de MongoDB Hola al conectar con hello local `mongo` cliente:

```bash
mongo
```

Ahora puede probar instancia de MongoDB Hola agregando algunos datos y, a continuación, buscar:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

Si lo desea, configure MongoDB toostart automáticamente durante un reinicio del sistema:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Creación de una instancia básica de MongoDB en CentOS mediante una plantilla
Puede crear una instancia de MongoDB básica en una sola máquina virtual CentOS mediante Hola siguientes plantilla de inicio rápido de Azure de GitHub. Esta plantilla utiliza la extensión de Script personalizado de Hola para Linux tooadd una **yum** tooyour repositorio recién creado la máquina virtual CentOS y, a continuación, instalar MongoDB.

* [Instancia básica de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate este entorno, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login). En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

A continuación, implementar la plantilla de MongoDB Hola con [Crear implementación de grupo az](/cli/azure/group/deployment#create). Defina sus propios nombres y tamaños de recursos donde sea necesario; por ejemplo, para *newStorageAccountName*, *virtualNetworkName* y *vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

Inicie sesión en toohello VM utilizando Hola dirección pública de DNS de la máquina virtual. Puede ver la dirección DNS pública Hola con [mostrar de la máquina virtual de az](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour VM con su propio nombre de usuario y la dirección DNS pública:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Comprobar la instalación de MongoDB Hola al conectar con hello local `mongo` cliente como sigue:

```bash
mongo
```

Ahora puede probar instancia Hola agregando algunos datos y buscar los siguientes:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Creación de un clúster complejo con particiones de MongoDB en CentOS mediante una plantilla
Se puede crear un clúster particionado de MongoDB complejo con hello siguientes plantilla de inicio rápido de Azure de GitHub. Esta plantilla sigue hello [prácticas recomendadas de MongoDB clúster particionada](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancia y alta disponibilidad. plantilla de Hello crea dos particiones, con tres nodos en cada conjunto de réplicas. También se crean un conjunto con tres nodos de réplicas de servidor de configuración, más dos **mongos** enrutador servidores tooprovide coherencia tooapplications de entre las particiones de Hola.

* [Clúster con particiones de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Implementación de este clúster de MongoDB particionada complejo requiere más de 20 núcleos, que normalmente es el recuento de núcleos de hello predeterminado por región para una suscripción. Abra su recuento de núcleos de un tooincrease de solicitud de soporte técnico de Azure.

toocreate este entorno, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login). En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

A continuación, implementar la plantilla de MongoDB Hola con [Crear implementación de grupo az](/cli/azure/group/deployment#create). Defina sus propios nombres de recursos y tamaños donde sea necesario; por ejemplo, para *mongoAdminUsername*, *sizeOfDataDiskInGB* y *configNodeVmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

Esta implementación puede asumir un toodeploy de hora y configurar todas las instancias de máquina virtual de Hola. Hola `--no-wait` marca se utiliza al final de Hola de hello anterior símbolo de comando de tooreturn control toohello una vez que la implementación de la plantilla de hello haya sido aceptado por hello plataforma Windows Azure. A continuación, puede ver el estado de implementación de hello con [muestra de implementación de grupo az](/cli/azure/group/deployment#show). vistas de ejemplo siguientes Hola Hola estado de hello *myMongoDBCluster* implementación Hola *myResourceGroup* grupo de recursos:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Pasos siguientes
En estos ejemplos, puede conectar toohello MongoDB instancia localmente desde Hola máquina virtual. Si desea tooconnect toohello MongoDB instancia desde otra máquina virtual o una red, asegúrese de hello adecuado [se crean las reglas del grupo de seguridad de red](nsg-quickstart.md).

Estos ejemplos implementación el entorno de MongoDB de núcleo de Hola para fines de desarrollo. Aplicar opciones de configuración de seguridad de hello necesario para su entorno. Para obtener más información, vea hello [documentos de seguridad de MongoDB](https://docs.mongodb.com/manual/security/).

Para obtener más información acerca de cómo crear mediante plantillas, vea hello [Introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

plantillas de Azure Resource Manager Hola usar toodownload de extensión de Script personalizado de Hola y ejecutan scripts en las máquinas virtuales. Para obtener más información, consulte [hello mediante extensión de Script personalizado de Azure con las máquinas virtuales Linux](extensions-customscript.md).

