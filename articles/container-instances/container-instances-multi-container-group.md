---
title: "aaaAzure instancias de contenedor - grupo contenedor múltiples | Documentos de Azure"
description: 'Azure Container Instances: grupo con varios contenedores'
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a>Implementación de un grupo de contenedores

Instancias de contenedor de Azure compatible con la implementación de Hola de varios contenedores en un solo host mediante un *grupo contenedor*. Esto es útil cuando se crea un sidecar de aplicación para el registro, la supervisión o cualquier otra configuración donde un servicio necesita un segundo proceso asociado. 

Este documento describe la ejecución de una configuración de sidecar de varios contenedores sencilla mediante una plantilla de Azure Resource Manager.

## <a name="configure-hello-template"></a>Configurar plantilla Hola

Cree un archivo denominado `azuredeploy.json` y Hola copia siguiendo json en él. 

En este ejemplo, se definen un grupo de contenedores con dos contenedores y una dirección IP pública. primer contenedor de grupo de Hola de Hola ejecuta una aplicación con conexión a internet. segundo contenedor Hello, asociado hello, hace que una aplicación de web principal de toohello de solicitud HTTP a través de la red local del grupo de Hola. 

En este ejemplo asociado puede ser tootrigger expandido una alerta si recibió un código de respuesta HTTP distintos de 200 OK. 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

toouse un registro de imagen de contenedor privado, agregar un documento de json de objeto toohello con hello siguiendo el formato.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Implementar la plantilla de Hola

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Implementar la plantilla de hello con hello [Crear implementación de grupo az](/cli/azure/group/deployment#create) comando.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

Al cabo de unos segundos, recibirá una respuesta inicial de Azure. 

## <a name="view-deployment-state"></a>Visualización del estado de la implementación

estado de hello tooview de implementación de hello, use hello `az container show` comando. Esto devuelve la dirección IP pública Hola aprovisionado sobre qué Hola pueden tener acceso a aplicaciones.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Salida:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Ver registros   

Ver la salida de registro de hello de un contenedor con hello `az container logs` comando. Hola `--container-name` argumento especifica el contenedor de Hola de qué registros se toopull. En este ejemplo, se especifica el primer contenedor de Hola. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Salida:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

Hola toosee los registros para contenedor de lado automóvil hello, ejecute hello mismo nombre del comando especificando Hola segundo contenedor.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Salida:

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

Como puede ver, asociado Hola realiza periódicamente una aplicación de web principal de toohello de solicitud HTTP a través de tooensure de red local del grupo de Hola que se está ejecutando.

## <a name="next-steps"></a>Pasos siguientes

Este documento trata los pasos de hello necesarios para implementar un contenedor de la instancia del contenedor de Azure. Para un tooend final que experiencia de instancias de contenedor de Azure, vea el tutorial de instancias de contenedor de Azure de Hola.

> [!div class="nextstepaction"]
> [Tutorial de Azure Container Instances]: ./container-instances-tutorial-prepare-app.md
