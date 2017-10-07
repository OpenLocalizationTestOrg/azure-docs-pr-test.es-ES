---
title: aaaCreate el primer contenedor de instancias de contenedor de Azure | Documentos de Azure
description: Implemente y empiece a usar Azure Container Instances
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Creación del primer contenedor en Azure Container Instances

Instancias de contenedor Azure resulta fácil toocreate y administrar contenedores en Azure. En este tutorial, creará un contenedor de Azure y exponerlo toohello internet con una dirección IP pública. Esta operación se completa en un solo comando. En pocos segundos, verá lo siguiente en el explorador:

![Aplicación implementada mediante Azure Container Instances vista en el explorador][aci-app-browser]

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.12 o una versión posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Azure Container Instances son recursos de Azure y se deben colocar en un grupo de recursos de Azure, una colección lógica en la que se implementan y administran los recursos de Azure.

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Crear un contenedor

Para crear un contenedor debe especificar un nombre, una imagen de Docker y un grupo de recursos de Azure. Puede exponer opcionalmente Hola contenedor toohello internet con una dirección IP pública. En este caso, se va a usar un contenedor que hospeda una aplicación web muy simple escrita en [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

Dentro de unos segundos, debería obtener una solicitud de tooyour de respuesta. Inicialmente, el contenedor de hello estará en un **crear** estado, pero debe comenzar en cuestión de segundos. Puede comprobar el estado de hello mediante hello `show` comando:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

En parte inferior de Hola de salida de hello, verá el estado de aprovisionamiento del contenedor de Hola y su dirección IP:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Una vez que el contenedor de hello mueve toohello **correcto** estado, puede llegar a él en el Explorador de hello mediante la dirección IP Hola proporcionada. 

![Aplicación implementada mediante Azure Container Instances vista en el explorador][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Extraer registros de contenedor de Hola

Puede extraer registros Hola del contenedor de hello creada con hello `logs` comando:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Salida:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Eliminar el contenedor de Hola

Cuando haya terminado con el contenedor de hello, puede quitarlo mediante hello `delete` comando:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

Todo de hello el código de contenedor de hello utilizado en esta guía de inicio rápido está disponible [en GitHub][app-github-repo], junto con su Dockerfile. Si desea que tootry creación usted mismo y su implementación tooAzure instancias de contenedor con hello del registro de contenedor de Azure, continuar con tutorial de toohello instancias de contenedor de Azure.

> [!div class="nextstepaction"]
> [Tutoriales de Azure Container Instances](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png