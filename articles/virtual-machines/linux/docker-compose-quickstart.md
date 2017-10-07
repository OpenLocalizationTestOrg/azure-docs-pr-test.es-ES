---
title: aaaUse Docker Compose en una VM de Linux en Azure | Documentos de Microsoft
description: "Cómo toouse Docker y Redactar en máquinas virtuales de Linux con Hola CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Obtener partió toodefine Docker y crear y ejecutar una aplicación de contenedor de varios en Azure
Con [redactar](http://github.com/docker/compose), use un toodefine del archivo de texto simple de una aplicación que consta de varios contenedores de Docker. , A continuación, haga clic en la aplicación en un único comando que hace todo lo que toodeploy el entorno definido. Por ejemplo, este artículo muestra cómo tooquickly configurado un blog de WordPress con un back-end de base de datos MariaDB SQL en una VM Ubuntu. También puede utilizar tooset de redacción de seguridad de aplicaciones más complejas.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Configuración de una máquina virtual Linux como host de Docker
Puede usar diversos procedimientos de Azure y las imágenes disponibles o plantillas de administrador de recursos en Azure Marketplace de hello toocreate una VM de Linux y se configura como un host Docker. Por ejemplo, vea [con hello extensión de máquina virtual Docker toodeploy su entorno](dockerextension.md) tooquickly crear una VM Ubuntu con hello extensión de máquina virtual de Azure Docker mediante un [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Cuando se utiliza la extensión de máquina virtual Docker de hello, la máquina virtual se configura automáticamente como un host Docker y redactar ya está instalado.


### <a name="create-docker-host-with-azure-cli-20"></a>Creación de un host de Docker con la CLI de Azure 2.0
Hola de instalación más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).

En primer lugar, cree un grupo de recursos para su entorno de Docker con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación:

```azurecli
az group create --name myResourceGroup --location westus
```

A continuación, implementar una máquina virtual con [Crear implementación de grupo az](/cli/azure/group/deployment#create) que incluye la extensión de máquina virtual de Azure Docker Hola de [esta plantilla de administrador de recursos de Azure en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Proporcione sus propios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* y *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Se tarda unos minutos para hello toofinish de implementación. Una vez finalizada la implementación de hello, [mover paso toonext](#verify-that-compose-is-installed) tooSSH tooyour máquina virtual. 

Opcionalmente, el símbolo del sistema de tooinstead control devuelto toohello e implementación de hello permiten continúan en segundo plano de hello, agregue hello `--no-wait` marca toohello anterior comando. Este proceso le permite tooperform otro trabajo en hello CLI mientras continúa la implementación de Hola durante unos minutos. A continuación, puede ver detalles sobre el estado de host de hello Docker con [mostrar de la máquina virtual de az](/cli/azure/vm#show). Hello en el ejemplo siguiente se comprueba estado Hola de máquina virtual denominada hello *myDockerVM* (Hola nombre predeterminado de la plantilla de hello: no cambie este nombre) en grupo de recursos de hello llamado *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Cuando vuelve este comando *correcto*, ha terminado la implementación de Hola y puede SSH toohello VM Hola siguiendo el paso.


## <a name="verify-that-compose-is-installed"></a>Comprobación de que se ha instalado Compose
Una vez finalizada la implementación de hello, SSH tooyour nuevo host Docker utilizando el nombre DNS de Hola que proporcionó durante la implementación. Puede usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview detalles de la máquina virtual, incluido el nombre DNS de Hola.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck que componen se instala en Hola de máquina virtual, ejecute el siguiente comando de hello:

```bash
docker-compose --version
```

Obtiene un resultado similar demasiado*docker-redactar 1.6.2, compilación 4D 72027*.

> [!TIP]
> Si usa otro método toocreate un host Docker y necesita tooinstall crear usted mismo, consulte hello [redactar documentación](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Creación de un archivo de configuración docker-compose.yml
A continuación creará un `docker-compose.yml` archivo, que es simplemente un archivo de configuración de texto, toorun de contenedores de Docker toodefine hello en hello máquina virtual. archivo Hello especifica Hola imagen toorun en cada contenedor (o bien, podría deberse a una compilación de un archivo Dockerfile), variables de entorno necesarias y las dependencias, puertos y vínculos de hello entre contenedores. Para más información sobre la sintaxis del archivo YML, consulte la [referencia del archivo de Compose](https://docs.docker.com/compose/compose-file/).

Crear hello *docker compose.yml* como sigue:

```bash
touch docker-compose.yml
```

Utilice la tooadd del editor de texto que prefiera algunos archivos de toohello de datos. Hello en el ejemplo siguiente se usa hello *vi* editor:

```bash
vi docker-compose.yml
```

Pegue Hola siguiente ejemplo en el archivo de texto. Esta configuración usa las imágenes de hello [DockerHub registro](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (sistema de administración contenido y creación de blogs de código abierto Hola) y un servidor vinculado MariaDB SQL de base de datos. Escriba su propio *MYSQL_ROOT_PASSWORD* como se indica a continuación:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Contenedores de Hola de inicio con redactar
En Hola mismo directorio como su *docker compose.yml* archivo, ejecute el siguiente comando de hello (dependiendo de su entorno, deberá toorun `docker-compose` con `sudo`):

```bash
docker-compose up -d
```

Este comando inicia contenedores de Docker Hola especificados en *docker compose.yml*. Tarda un minuto o dos para este paso toocomplete. Vea toohello similar de salida siguiente ejemplo:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Estar seguro de hello toouse **-d** opción Inicio para que los contenedores de Hola se ejecutan en segundo plano de hello continuamente.


tooverify que son contenedores de hello, tipo `docker-compose ps`. Debería ver algo parecido a lo siguiente:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Ahora puede conectarse tooWordPress directamente en hello VM en el puerto 80. Abra un explorador web y escriba el nombre DNS de saludo de la máquina virtual (como `http://mypublicdns.westus.cloudapp.azure.com`). Ahora debería ver Hola que WordPress iniciar pantalla, donde puede completar la instalación de Hola y empezar a trabajar con la aplicación hello.

![Pantalla de inicio de WordPress][wordpress_start]

## <a name="next-steps"></a>Pasos siguientes
* Vaya toohello [Guía de usuario de extensión de máquina virtual Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obtener más opciones tooconfigure Docker y Redactar en la máquina virtual Docker. Por ejemplo, una opción es tooput redactar yml archivo hello (tooJSON convertido) directamente en la configuración de Hola de hello extensión de máquina virtual de Docker.
* Extraer del repositorio hello [crear la referencia de línea de comandos](http://docs.docker.com/compose/reference/) y [Guía de usuario](http://docs.docker.com/compose/) para obtener más ejemplos de crear e implementar aplicaciones de contenedor de varios.
* Usar una plantilla de Azure Resource Manager, ya sea su propio o uno proceden de Hola [Comunidad](https://azure.microsoft.com/documentation/templates/), toodeploy una VM de Azure con Docker y una aplicación prepararle redactar. Por ejemplo, hello [implementar un blog de WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) plantilla utiliza Docker y redactar tooquickly implementar WordPress con un back-end de MySQL en una VM Ubuntu.
* Pruebe a integrar Docker Compose con un clúster de Docker Swarm. Consulte [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso de Compose con Swarm) para conocer distintos escenarios.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
