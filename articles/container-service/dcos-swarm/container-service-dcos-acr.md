---
title: "aaaUsing ACR con un clúster de Azure DC/OS | Documentos de Microsoft"
description: "Use un Azure Container Registry con un clúster DC/OS en Azure Container Service"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, contenedores, microservicios, Mesos, Azure, recurso compartido de archivos, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>Usar ACR con un toodeploy de clúster de DC/OS la aplicación

En este artículo, exploraremos cómo toouse del registro de contenedor de Azure con un clúster de DC/OS. Uso de ACR permite tooprivately almacén y administrar imágenes del contenedor. Este tutorial trata Hola siguientes tareas:

> [!div class="checklist"]
> * Implementación de Azure Container Registry (en caso de ser necesaria)
> * Configuración de la autenticación de ACR en un clúster de DC/OS
> * Cargar un toohello de imagen del registro de contenedor de Azure
> * Ejecutar una imagen de contenedor de hello del registro de contenedor de Azure

Necesita un controlador de dominio ACS/OS hello toocomplete de clúster de los pasos de este tutorial. Si es necesario, este [script de ejemplo](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) puede crear uno.

Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Implementación de Azure Container Registry

Si es necesario, cree un registro de contenedor de Azure con hello [crear acr az](/cli/azure/acr#create) comando. 

Hello en el ejemplo siguiente se crea un registro con un generar nombre de forma aleatoria. registro de Hello también se configura con una cuenta de administrador con hello `--admin-enabled` argumento.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Una vez que se ha creado el registro de hello, Hola CLI de Azure da como resultado siguiente toohello similares de datos. Tome nota de hello `name` y `loginServer`, se usan en pasos posteriores.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Obtener credenciales de registro de contenedor hello mediante hello [show de credencial de acr az](/cli/azure/acr/credential) comando. Hola sustituto `--name` con hello uno anotó en el último paso de Hola. Tome nota de una contraseña, ya que es necesaria más adelante.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Para obtener más información acerca del registro de contenedor de Azure, consulte [registros de contenedor de Docker de introducción tooprivate](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>Administración de la autenticación de ACR

imagen toopush y extracción de un registro privado es toofirst de forma convencional de Hello autenticar con registro de hello. toodo por lo tanto, se usaría hello `docker login` comando en cualquier cliente que necesita del registro de tooaccess Hola privada. Dado que un clúster de DC/OS puede contener muchos nodos, todos ellos necesitan toobe autenticado con hello ACR, resulta útil tooautomate este proceso a través de cada nodo. 

### <a name="create-shared-storage"></a>Creación de almacenamiento compartido

Este proceso utiliza un recurso compartido de archivos de Azure que se ha montado en cada nodo de clúster de Hola. Si aún no se ha configurado el almacenamiento compartido, consulte [Configuración de un recurso compartido de archivos dentro de un clúster de DC/OS](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>Configuración de la autenticación de ACR

En primer lugar, obtenga Hola FQDN de Hola DC/OS maestro y almacenarlo en una variable.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Crear una conexión SSH con hello (Hola primera maestra o) del clúster basadas en DC/OS. Actualizar nombre de usuario de hello si se utilizó un valor no predeterminado al crear el clúster de Hola.

```azurecli-interactive
ssh azureuser@$FQDN
```

Siguiente ejecución Hola comando toologin toohello del registro de contenedor de Azure. Reemplace hello `--username` por nombre de Hola de registro de contenedor de Hola y Hola `--password` con una de las contraseñas de hello proporcionado. Reemplace el último argumento de hello *mycontainerregistry.azurecr.io* en ejemplo de Hola con nombre de hello loginServer de registro de contenedor de Hola. 

Este comando almacena los valores de autenticación de hello localmente en hello `~/.docker` ruta de acceso.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Crear un archivo comprimido que contiene los valores de autenticación de hello contenedor del registro.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Copie este almacenamiento de clúster compartido de archivo toohello. Este paso realiza archivo hello disponible en todos los nodos del clúster de Hola DC/OS.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Cargar imagen tooACR

Ahora desde un equipo de desarrollo, o cualquier otro sistema con Docker instalado, cree una imagen y cargarla toohello del registro de contenedor de Azure.

Crear un contenedor de imagen de Ubuntu Hola.

```azurecli-interactive
docker run ubunut --name base-image
```

Ahora captura Hola contenedor en una nueva imagen. nombre de la imagen de Hello necesita hello tooinclude `loginServer` nombre de hello contenedor registrywith un formato de `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Inicio de sesión en hello del registro de contenedor de Azure. Sustituir el nombre de Hola por hello loginServer, Hola: nombre de usuario con el nombre de Hola de registro de contenedor de Hola y Hola--contraseña con una de las contraseñas de hello proporcionado.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Por último, cargue el registro de hello imágenes toohello ACR. En este ejemplo, se carga una imagen llamada dcos-demo.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Ejecución de una imagen desde ACR

toouse una imagen desde el registro ACR hello, cree un archivo de nombres *acrDemo.json* y Hola copia siguiendo el texto en él. Reemplazar el nombre de la imagen de Hola con nombre de loginServer de hello contenedor del registro y el nombre de la imagen, por ejemplo `loginServer/imageName`. Tome nota de hello `uris` propiedad. Esta propiedad contiene la ubicación de Hola Hola contenedor autenticación del archivo registro, que en este caso es el recurso compartido de archivos de Azure de Hola que está montado en cada nodo de clúster de Hola DC/OS.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Implementar aplicación hello con hello DC/OC CLI.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial ha configurar toouse DC/OS tareas de registro de contenedor de Azure incluidos Hola siguientes:

> [!div class="checklist"]
> * Implementación de Azure Container Registry (en caso de ser necesaria)
> * Configuración de la autenticación de ACR en un clúster de DC/OS
> * Cargar un toohello de imagen del registro de contenedor de Azure
> * Ejecutar una imagen de contenedor de hello del registro de contenedor de Azure
