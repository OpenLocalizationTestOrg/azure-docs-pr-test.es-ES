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
# <a name="deploy-a-container-group"></a><span data-ttu-id="81d64-103">Implementación de un grupo de contenedores</span><span class="sxs-lookup"><span data-stu-id="81d64-103">Deploy a container group</span></span>

<span data-ttu-id="81d64-104">Instancias de contenedor de Azure compatible con la implementación de Hola de varios contenedores en un solo host mediante un *grupo contenedor*.</span><span class="sxs-lookup"><span data-stu-id="81d64-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="81d64-105">Esto es útil cuando se crea un sidecar de aplicación para el registro, la supervisión o cualquier otra configuración donde un servicio necesita un segundo proceso asociado.</span><span class="sxs-lookup"><span data-stu-id="81d64-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="81d64-106">Este documento describe la ejecución de una configuración de sidecar de varios contenedores sencilla mediante una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="81d64-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="81d64-107">Configurar plantilla Hola</span><span class="sxs-lookup"><span data-stu-id="81d64-107">Configure hello template</span></span>

<span data-ttu-id="81d64-108">Cree un archivo denominado `azuredeploy.json` y Hola copia siguiendo json en él.</span><span class="sxs-lookup"><span data-stu-id="81d64-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="81d64-109">En este ejemplo, se definen un grupo de contenedores con dos contenedores y una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="81d64-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="81d64-110">primer contenedor de grupo de Hola de Hola ejecuta una aplicación con conexión a internet.</span><span class="sxs-lookup"><span data-stu-id="81d64-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="81d64-111">segundo contenedor Hello, asociado hello, hace que una aplicación de web principal de toohello de solicitud HTTP a través de la red local del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d64-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="81d64-112">En este ejemplo asociado puede ser tootrigger expandido una alerta si recibió un código de respuesta HTTP distintos de 200 OK.</span><span class="sxs-lookup"><span data-stu-id="81d64-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="81d64-113">toouse un registro de imagen de contenedor privado, agregar un documento de json de objeto toohello con hello siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="81d64-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="81d64-114">Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="81d64-114">Deploy hello template</span></span>

<span data-ttu-id="81d64-115">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="81d64-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="81d64-116">Implementar la plantilla de hello con hello [Crear implementación de grupo az](/cli/azure/group/deployment#create) comando.</span><span class="sxs-lookup"><span data-stu-id="81d64-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="81d64-117">Al cabo de unos segundos, recibirá una respuesta inicial de Azure.</span><span class="sxs-lookup"><span data-stu-id="81d64-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="81d64-118">Visualización del estado de la implementación</span><span class="sxs-lookup"><span data-stu-id="81d64-118">View deployment state</span></span>

<span data-ttu-id="81d64-119">estado de hello tooview de implementación de hello, use hello `az container show` comando.</span><span class="sxs-lookup"><span data-stu-id="81d64-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="81d64-120">Esto devuelve la dirección IP pública Hola aprovisionado sobre qué Hola pueden tener acceso a aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="81d64-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="81d64-121">Salida:</span><span class="sxs-lookup"><span data-stu-id="81d64-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="81d64-122">Ver registros</span><span class="sxs-lookup"><span data-stu-id="81d64-122">View logs</span></span>   

<span data-ttu-id="81d64-123">Ver la salida de registro de hello de un contenedor con hello `az container logs` comando.</span><span class="sxs-lookup"><span data-stu-id="81d64-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="81d64-124">Hola `--container-name` argumento especifica el contenedor de Hola de qué registros se toopull.</span><span class="sxs-lookup"><span data-stu-id="81d64-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="81d64-125">En este ejemplo, se especifica el primer contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d64-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="81d64-126">Salida:</span><span class="sxs-lookup"><span data-stu-id="81d64-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="81d64-127">Hola toosee los registros para contenedor de lado automóvil hello, ejecute hello mismo nombre del comando especificando Hola segundo contenedor.</span><span class="sxs-lookup"><span data-stu-id="81d64-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="81d64-128">Salida:</span><span class="sxs-lookup"><span data-stu-id="81d64-128">Output:</span></span>

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

<span data-ttu-id="81d64-129">Como puede ver, asociado Hola realiza periódicamente una aplicación de web principal de toohello de solicitud HTTP a través de tooensure de red local del grupo de Hola que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="81d64-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81d64-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81d64-130">Next steps</span></span>

<span data-ttu-id="81d64-131">Este documento trata los pasos de hello necesarios para implementar un contenedor de la instancia del contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="81d64-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="81d64-132">Para un tooend final que experiencia de instancias de contenedor de Azure, vea el tutorial de instancias de contenedor de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d64-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="81d64-133">[Tutorial de Azure Container Instances]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="81d64-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
