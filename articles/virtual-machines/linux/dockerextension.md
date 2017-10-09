---
title: "Hola aaaUse extensión de máquina virtual de Azure Docker | Documentos de Microsoft"
description: "Obtenga información acerca cómo toouse Hola tooquickly de extensión de máquina virtual Docker y segura implementar un entorno de Docker en Azure con plantillas de administrador de recursos y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Crear un entorno de Docker en Azure con la extensión de máquina virtual Docker Hola
Docker es una plataforma de creación de imágenes que le permite trabajar de tooquickly con contenedores en Linux y administración de contenedor populares. En Azure, existen varias maneras puede implementar según las necesidades de tooyour de Docker. En este artículo se centra en utilizar la extensión de máquina virtual Docker de Hola y plantillas del Administrador de recursos de Azure con hello Azure CLI 2.0. También puede realizar estos pasos con hello [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Introducción a la extensión de máquina virtual de Docker para Azure
Hola extensión de máquina virtual de Azure Docker instala y configura el demonio de Docker Hola, cliente de Docker y Docker Compose en la máquina virtual (VM) de Linux. Mediante el uso de extensión de máquina virtual de Azure Docker hello, tiene más control y características que simplemente se usa máquina Docker o creación de host de Docker Hola usted mismo. Estos más características, como [Docker Compose](https://docs.docker.com/compose/overview/), asegúrese de extensión de máquina virtual de Azure Docker Hola adecuado para entornos de producción o desarrollador más sólidos.

Para obtener más información acerca de los métodos de implementación diferentes de hello, incluido el uso de la máquina de Docker y servicios de contenedor de Azure, vea Hola siguientes artículos:

* prototipo de tooquickly una aplicación, puede crear un único host de Docker con [Docker máquina](docker-machine.md).
* toobuild para entornos de producción entornos escalables que proporcionan herramientas de programación y administración adicionales, puede implementar un [Docker Swarm clúster en los servicios de contenedor de Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Implementar una plantilla con hello extensión de máquina virtual de Azure Docker
Vamos a usar una existente toocreate de plantilla de inicio rápido un Ubuntu VM que use tooinstall de extensión de máquina virtual de Azure Docker hello y configurar host de Docker Hola. Puede ver la plantilla de hello aquí: [implementación Simple de una VM de Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación:

```azurecli
az group create --name myResourceGroup --location westus
```

A continuación, implementar una máquina virtual con [Crear implementación de grupo az](/cli/azure/group/deployment#create) que incluye la extensión de máquina virtual de Azure Docker Hola de [esta plantilla de administrador de recursos de Azure en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Proporcione sus propios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* y *dnsNameForPublicIP* de la manera siguiente:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Se tarda unos minutos para hello toofinish de implementación. Una vez finalizada la implementación de hello, [mover paso toonext](#deploy-your-first-nginx-container) tooSSH tooyour máquina virtual. 

Opcionalmente, el símbolo del sistema de tooinstead control devuelto toohello e implementación de hello permiten continúan en segundo plano de hello, agregue hello `--no-wait` marca toohello anterior comando. Este proceso le permite tooperform otro trabajo en hello CLI mientras continúa la implementación de Hola durante unos minutos. 

A continuación, puede ver detalles sobre el estado de host de hello Docker con [mostrar de la máquina virtual de az](/cli/azure/vm#show). Hello en el ejemplo siguiente se comprueba estado Hola de máquina virtual denominada hello *myDockerVM* (Hola nombre predeterminado de la plantilla de hello: no cambie este nombre) en grupo de recursos de hello llamado *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Cuando vuelve este comando *correcto*, ha terminado la implementación de Hola y puede SSH toohello VM Hola siguiendo el paso.

## <a name="deploy-your-first-nginx-container"></a>Implementación del primer contenedor nginx
usar tooview detalles de la máquina virtual, incluyendo nombre DNS de hello, `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour nuevas Docker de host desde el equipo local como sigue:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Una vez iniciada la sesión toohello host Docker, vamos a ejecutar un contenedor de nginx:

```bash
sudo docker run -d -p 80:80 nginx
```

salida de Hello es similar toohello siguiente ejemplo como hello nginx imagen se descarga y un contenedor inicia:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Comprobar el estado de Hola de contenedores de Hola que se ejecutan en el host Docker como se indica a continuación:

```bash
sudo docker ps
```

salida de Hello es similar toohello ejemplo siguiente, que muestra que el contenedor de hello nginx se está ejecutando y los puertos TCP 80 y 443 y reenvían:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

toosee el contenedor en acción, abra una copia de seguridad un explorador web y escriba el nombre DNS de hello del host Docker:

![Ejecución del contenedor ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Referencia sobre la plantilla de la extensión de máquina virtual de Docker para Azure
ejemplo de Hola anterior usa una plantilla existente de inicio rápido. También puede implementar la extensión de máquina virtual de Azure Docker Hola con sus propias plantillas de administrador de recursos. toodo por lo tanto, agregar Hola después tooyour plantillas de administrador de recursos, la definición de hello `vmName` de la máquina virtual correctamente:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Puede encontrar un tutorial más detallado sobre el uso de plantillas de Resource Manager en [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Pasos siguientes
Puede ser conveniente demasiado[configurar el puerto TCP de hello Docker daemon](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprender [seguridad Docker](https://docs.docker.com/engine/security/security/), o implementar contenedores con [Docker Compose](https://docs.docker.com/compose/overview/). Para obtener más información sobre Hola extensión de máquina virtual de Azure Docker propio, vea hello [GitHub proyecto](https://github.com/Azure/azure-docker-extension/).

Leer más información acerca de las opciones de implementación de Docker adicionales de hello en Azure:

* [Usar el equipo de Docker con hello Azure controlador](docker-machine.md)  
* [Introducción a Docker y redactar toodefine y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure](docker-compose-quickstart.md).
* [Implementación de un clúster del servicio Contenedor de Azure](../../container-service/dcos-swarm/container-service-deployment.md)

