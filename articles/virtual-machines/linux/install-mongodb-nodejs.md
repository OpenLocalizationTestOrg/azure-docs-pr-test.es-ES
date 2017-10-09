---
title: aaaInstall MongoDB en una VM de Linux con Hola 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar MongoDB en una máquina virtual de Linux en Azure con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>¿Cómo tooinstall y configurar MongoDB en una VM de Linux con hello Azure CLI 1.0
[MongoDB](http://www.mongodb.org) es una conocida base de datos NoSQL de código abierto y alto rendimiento. Este artículo muestra cómo tooinstall y configurar MongoDB en una VM de Linux en Azure con el modelo de implementación del Administrador de recursos de Hola. Se muestran algunos ejemplos detallados de:

* [Instalación y configuración manuales de una instancia básica de MongoDB](#manually-install-and-configure-mongodb-on-a-vm)
* [Creación de una instancia básica de MongoDB mediante una plantilla de Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Creación de un clúster complejo con particiones de MongoDB con conjuntos de réplicas mediante una plantilla de Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- CLI de Azure 1.0 – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](create-cli-complete-nodejs.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Instalación y configuración manuales de MongoDB en una máquina virtual
MongoDB [proporciona instrucciones de instalación](https://docs.mongodb.com/manual/administration/install-on-linux/) para distribuciones de Linux, incluidos Red Hat/CentOS, SUSE, Ubuntu y Debian. Hello ejemplo siguiente se crea un *CentOS* máquina virtual con una clave SSH almacenada en *~/.ssh/id_rsa.pub*. Hola de respuesta solicita nombre de la cuenta de almacenamiento, nombre DNS y credenciales de administrador:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Inicie sesión en toohello VM mediante la dirección IP pública Hola que se muestra al final de Hola de hello anterior paso de creación de la máquina virtual:

```bash
ssh azureuser@40.78.23.145
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

De forma predeterminada, SELinux está aplicado en las imágenes de CentOS, lo que impide el acceso de MongoDB. Instalar herramientas de administración de directivas y configure SELinux tooallow MongoDB toooperate en su puerto TCP 27017 como se indica a continuación. 

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
Puede crear una instancia de MongoDB básica en una sola máquina virtual CentOS mediante Hola siguientes plantilla de inicio rápido de Azure de GitHub. Esta plantilla utiliza la extensión de Script personalizado de Hola para Linux tooadd una `yum` tooyour repositorio recién creado la máquina virtual CentOS y, a continuación, instalar MongoDB.

* [Instancia básica de MongoDB en CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Hello en el ejemplo siguiente se crea un grupo de recursos con nombre hello `myResourceGroup` en hello `eastus` región. Escriba sus propios valores, como se indica a continuación:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hola CLI de Azure devuelve tooa símbolo del sistema en cuestión de segundos de creación de la implementación de hello, pero cuya instalación hello y configuración toma toocomplete unos minutos. Comprobar el estado de Hola de implementación de hello con `azure group deployment show myResourceGroup`, escribir el nombre de Hola de su grupo de recursos según corresponda. Espere hasta que hello **ProvisioningState** muestra *correcto* antes de tratar de tooSSH toohello máquina virtual.

Una vez finalizada la implementación de hello completa, SSH toohello máquina virtual. Obtener dirección IP de saludo de la máquina virtual con hello `azure vm show` comando como en el siguiente ejemplo de Hola:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Casi final Hola de salida de hello, se muestra la dirección IP pública Hola. SSH tooyour máquina virtual con la dirección IP de saludo de la máquina virtual:

```bash
ssh azureuser@138.91.149.74
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

Hello en el ejemplo siguiente se crea un grupo de recursos con nombre hello *myResourceGroup* en hello *eastus* región. Escriba sus propios valores, como se indica a continuación:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hola CLI de Azure devuelve tooa símbolo del sistema en cuestión de segundos de creación de la implementación de hello, pero hello instalación y configuración pueden tardar más de una hora toocomplete. Comprobar el estado de Hola de implementación de hello con `azure group deployment show myResourceGroup`, ajustar el nombre de Hola de su grupo de recursos según corresponda. Espere hasta que hello **ProvisioningState** muestra *correcto* antes de conectar máquinas virtuales toohello.


## <a name="next-steps"></a>Pasos siguientes
En estos ejemplos, puede conectar toohello MongoDB instancia localmente desde Hola máquina virtual. Si desea tooconnect toohello MongoDB instancia desde otra máquina virtual o una red, asegúrese de hello adecuado [se crean las reglas del grupo de seguridad de red](nsg-quickstart.md).

Para obtener más información acerca de cómo crear mediante plantillas, vea hello [Introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

plantillas de Azure Resource Manager Hola usar toodownload de extensión de Script personalizado de Hola y ejecutan scripts en las máquinas virtuales. Para obtener más información, consulte [hello mediante extensión de Script personalizado de Azure con las máquinas virtuales Linux](extensions-customscript.md).

