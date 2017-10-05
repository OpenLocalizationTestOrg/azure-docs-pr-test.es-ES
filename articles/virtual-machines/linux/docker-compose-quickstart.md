---
title: Uso de Docker Compose en una VM Linux en Azure | Microsoft Docs
description: "Uso de Docker y Compose en máquinas virtuales con Linux mediante la CLI de Azure"
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
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a>Introducción a Docker y Compose para definir y ejecutar una aplicación de contenedores múltiples en Azure
Con [Compose](http://github.com/docker/compose), usará un archivo de texto simple para definir una aplicación compuesta de varios contenedores de Docker. Después, puede poner en marcha la aplicación con un solo comando que realiza todos los pasos para implementarla en el entorno definido. Como ejemplo, en este artículo se muestra cómo configurar rápidamente un blog de WordPress con una base de datos SQL MariaDB de back-end en una máquina virtual Ubuntu. También puede utilizar Compose para configurar aplicaciones más complejas.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Configuración de una máquina virtual Linux como host de Docker
Puede emplear diversos procedimientos de Azure, así como las imágenes y plantillas de Azure Resource Manager disponibles en Azure Marketplace, para crear una máquina virtual Linux y configurarla como host de Docker. Por ejemplo, consulte [Uso de la extensión de VM de Docker para implementar el entorno](dockerextension.md) para crear rápidamente una máquina virtual Ubuntu con la extensión de máquina virtual de Azure Docker mediante el uso de una [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Cuando utilice la extensión de máquina virtual de Docker, la máquina virtual se configurará automáticamente como un host de Docker.


### <a name="create-docker-host-with-azure-cli-20"></a>Creación de un host de Docker con la CLI de Azure 2.0
Instale la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).

En primer lugar, cree un grupo de recursos para su entorno de Docker con [az group create](/cli/azure/group#create). En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westus*:

```azurecli
az group create --name myResourceGroup --location westus
```

A continuación, implemente una VM con [az group deployment create](/cli/azure/group/deployment#create), que incluye la extensión de VM de Docker para Azure de [esta plantilla de Azure Resource Manager en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Proporcione sus propios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* y *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

La implementación tarda unos minutos en finalizar. Una vez finalizada la implementación, [vaya al paso siguiente](#verify-that-compose-is-installed) para SSH en la VM. 

Opcionalmente, en lugar de devolver el control al símbolo del sistema y permitir que la implementación continúe en segundo plano, agregue la marca `--no-wait` al comando anterior. Este proceso permite realizar otro trabajo en la CLI mientras continúa la implementación durante unos minutos. Puede ver detalles sobre el estado del host de Docker con [az vm show](/cli/azure/vm#show). En el ejemplo siguiente, se comprueba el estado de la máquina virtual denominada *myDockerVM* (se trata del nombre predeterminado de la plantilla; no lo cambie) del grupo de recursos denominado *myResourceGroup*.

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Cuando este comando devuelve un estado *correcto*, ha terminado la implementación y puede implementar SSH en la máquina virtual en el paso siguiente.


## <a name="verify-that-compose-is-installed"></a>Comprobación de que se ha instalado Compose
Una vez que haya terminado la implementación, aplique SSH a su nuevo host de Docker mediante el nombre DNS que proporcionó durante la implementación. Puede usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` para ver los detalles de la máquina virtual, incluido el nombre DNS.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Para comprobar que Compose esté instalado en la máquina virtual, ejecute el siguiente comando:

```bash
docker-compose --version
```

Verá una salida similar a *docker-compose 1.6.2, build 4d72027*.

> [!TIP]
> Si utiliza otro método para crear un host de Docker y necesita instalar Compose de forma manual, consulte la [documentación de esta herramienta](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Creación de un archivo de configuración docker-compose.yml
A continuación, debe crear un archivo `docker-compose.yml` , que es simplemente un archivo de configuración para definir los contenedores de Docker para ejecutar la máquina virtual. El archivo especifica la imagen que se ejecutará en cada contenedor (o podría ser una compilación de un Dockerfile), variables de entorno y dependencias necesarias, puertos y vínculos entre contenedores. Para más información sobre la sintaxis del archivo YML, consulte la [referencia del archivo de Compose](https://docs.docker.com/compose/compose-file/).

Cree el archivo *docker-compose.yml* de la manera siguiente:

```bash
touch docker-compose.yml
```

Use el editor de texto que prefiera para agregar algunos datos al archivo. En el ejemplo siguiente se usa el editor *vi*:

```bash
vi docker-compose.yml
```

Pegue el siguiente ejemplo en el archivo de texto. Esta configuración usa imágenes del [Registro de DockerHub](https://registry.hub.docker.com/_/wordpress/) para instalar WordPress (el sistema de administración de contenido y blogs de código abierto) y una base de datos SQL MariaDB de back-end vinculada. Escriba su propio *MYSQL_ROOT_PASSWORD* como se indica a continuación:

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

## <a name="start-the-containers-with-compose"></a>inicio de los contenedores con Compose
En el mismo directorio que el archivo *docker-compose.yml*, ejecute el comando siguiente (dependiendo de su entorno, quizás tenga que ejecutar `docker-compose` mediante `sudo`):

```bash
docker-compose up -d
```

Este comando inicia los contenedores de Docker especificados en *docker-compose.yml*. Este paso tarda uno o dos minutos en completarse. Verá un resultado similar al del siguiente ejemplo:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Asegúrese de utilizar la opción **-d** al iniciar para que los contenedores se ejecuten continuamente en segundo plano.


Para comprobar que los contenedores están activos, escriba `docker-compose ps`. Debería ver algo parecido a lo siguiente:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Ahora puede conectarse a WordPress directamente en la máquina virtual a través del puerto 80. Abra un explorador web y escriba el nombre DNS de la máquina virtual (por ejemplo, `http://mypublicdns.westus.cloudapp.azure.com`). Ahora debería ver la pantalla de inicio de WordPress, donde se puede completar la instalación e iniciar la aplicación.

![Pantalla de inicio de WordPress][wordpress_start]

## <a name="next-steps"></a>Pasos siguientes
* Consulte el [manual del usuario de extensión de máquina virtual de Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obtener más opciones de configuración de Docker y Compose en su máquina virtual de Docker. Por ejemplo, una de ellas consiste en colocar el archivo YML de Compose (convertido a JSON) directamente en la configuración de la extensión de máquina virtual de Docker.
* Consulte la [referencia de línea de comandos de Compose](http://docs.docker.com/compose/reference/) y el [manual del usuario](http://docs.docker.com/compose/) para obtener más ejemplos de compilación e implementación de aplicaciones con varios contenedores.
* Use una plantilla del Administrador de recursos de Azure, o bien una propia o una proporcionada por la [comunidad](https://azure.microsoft.com/documentation/templates/), para implementar una VM de Azure con Docker y una aplicación configurada con Compose. Por ejemplo, la plantilla [Implementación de un blog de WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) usa Docker y Compose para implementar rápidamente WordPress con un back-end de MySQL en una máquina virtual de Ubuntu.
* Pruebe a integrar Docker Compose con un clúster de Docker Swarm. Consulte [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso de Compose con Swarm) para conocer distintos escenarios.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
