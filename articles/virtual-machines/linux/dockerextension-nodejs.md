---
title: "Hola aaaUse extensión de máquina virtual de Azure Docker con hello 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Conozca cómo toouse Hola tooquickly de extensión de máquina virtual Docker e implementar de forma segura un entorno de Docker en Azure con plantillas de administrador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Crear un entorno de Docker en Azure con extensión de máquina virtual Docker Hola Hola 1.0 de CLI de Azure
Docker es una plataforma de creación de imágenes que le permite trabajar de tooquickly con contenedores en Linux (y también de Windows) y la administración de contenedor populares. En Azure, existen varias maneras puede implementar según las necesidades de tooyour de Docker. En este artículo se centra sobre el uso de la extensión de máquina virtual Docker de Hola y plantillas del Administrador de recursos de Azure. 

Para obtener más información acerca de los métodos de implementación diferentes de hello, incluido el uso de la máquina de Docker y servicios de contenedor de Azure, vea Hola siguientes artículos:

* prototipo de tooquickly una aplicación, puede crear un único host de Docker con [Docker máquina](docker-machine.md).
* En entornos grandes y más estables, puede usar la extensión de máquina virtual de Azure Docker hello, que también es compatible con [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate implementaciones de contenedor coherente. Este artículo se detallan mediante la extensión de máquina virtual de Azure Docker Hola.
* toobuild para entornos de producción entornos escalables que proporcionan herramientas de programación y administración adicionales, puede implementar un [Docker Swarm clúster en los servicios de contenedor de Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#azure-docker-vm-extension-overview) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](dockerextension.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola 

## <a name="azure-docker-vm-extension-overview"></a>Introducción a la extensión de máquina virtual de Docker para Azure
Hola extensión de máquina virtual de Azure Docker instala y configura el demonio de Docker Hola, cliente de Docker y Docker Compose en la máquina virtual (VM) de Linux. Mediante el uso de extensión de máquina virtual de Azure Docker hello, tiene más control y características que simplemente se usa máquina Docker o creación de host de Docker Hola usted mismo. Estos más características, como [Docker Compose](https://docs.docker.com/compose/overview/), asegúrese de extensión de máquina virtual de Azure Docker Hola adecuado para entornos de producción o desarrollador más sólidos.

Las plantillas de administrador de recursos Azure definen estructura completa de Hola de su entorno. Las plantillas permiten toocreate y configurar recursos tales como host de Docker de hello las máquinas virtuales, almacenamiento, controles de acceso basado en roles (RBAC) y diagnósticos. Puede volver a usar estas implementaciones adicionales de toocreate de plantillas de una manera coherente. Para más información sobre Azure Resource Manager, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Implementar una plantilla con hello extensión de máquina virtual de Azure Docker
Vamos a usar una existente toocreate de plantilla de inicio rápido un Ubuntu VM que use tooinstall de extensión de máquina virtual de Azure Docker hello y configurar host de Docker Hola. Puede ver la plantilla de hello aquí: [implementación Simple de una VM de Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Necesita hello [CLI de Azure más reciente](../../cli-install-nodejs.md) instalado e inició sesión mediante el modo de administrador de recursos de hello como sigue:

```azurecli
azure config mode arm
```

Implementar la plantilla de hello mediante Hola CLI de Azure, especifique Hola plantilla URI. Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación. Use el nombre y la ubicación de su grupo de recursos como sigue:

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Responder Hola indicaciones tooname su cuenta de almacenamiento, proporcione un nombre de usuario y una contraseña y proporcione un nombre DNS. Hola de salida es similar toohello siguiente ejemplo:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hola CLI de Azure devuelve toohello símbolo del sistema después de unos pocos segundos, pero el host Docker todavía se está creando y configurado por hello extensión de máquina virtual de Azure Docker. Se tarda unos minutos para hello toofinish de implementación. Puede ver detalles sobre el estado de host de Docker Hola con hello `azure vm show` comando.

Hello en el ejemplo siguiente se comprueba estado Hola de máquina virtual denominada hello *myDockerVM* (Hola nombre predeterminado de la plantilla de hello: no cambie este nombre) en grupo de recursos de hello llamado *myResourceGroup*. Escriba el nombre de Hola Hola del grupo de recursos que creó en hello anterior paso:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

Hola salida de hello `azure vm show` comando es similar toohello siguiente ejemplo:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Cerca de la parte superior de Hola de salida de hello, vea hello **ProvisioningState** de hello máquina virtual. Cuando se muestra *correcto*, ha terminado la implementación de Hola y puede SSH toohello máquina virtual.

Final de hello de la salida de hello, *FQDN* muestra el nombre de dominio completo de hello del host Docker. Este FQDN es lo que usa host de Docker de tooSSH tooyour Hola restantes pasos.

## <a name="deploy-your-first-nginx-container"></a>Implementación del primer contenedor nginx
Una vez haya terminado implementación hello, SSH tooyour nuevo host de Docker desde el equipo local. Escriba su nombre de usuario y el FQDN como sigue:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
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

toosee el contenedor en acción, abra una copia de seguridad un explorador web y escriba el nombre FQDN de hello del host Docker:

![Ejecución del contenedor ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Referencia sobre la plantilla de la extensión de máquina virtual de Docker para Azure
ejemplo de Hola anterior usa una plantilla existente de inicio rápido. También puede implementar la extensión de máquina virtual de Azure Docker Hola con sus propias plantillas de administrador de recursos. toodo por lo tanto, agregar Hola después tooyour plantillas de administrador de recursos, la definición de hello *vmName* de la máquina virtual correctamente:

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
    "typeHandlerVersion": "1.1",
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

