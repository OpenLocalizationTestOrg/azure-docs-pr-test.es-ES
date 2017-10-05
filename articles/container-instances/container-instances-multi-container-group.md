---
title: 'Azure Container Instances: grupo con varios contenedores | Azure Docs'
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
ms.openlocfilehash: 140f58582645ea32f77e901eb13364ed145bbecf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="f898e-103">Implementación de un grupo de contenedores</span><span class="sxs-lookup"><span data-stu-id="f898e-103">Deploy a container group</span></span>

<span data-ttu-id="f898e-104">Azure Container Instances admite compatible la implementación de varios contenedores en un solo host mediante un *grupo de contenedores*.</span><span class="sxs-lookup"><span data-stu-id="f898e-104">Azure Container Instances support the deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="f898e-105">Esto es útil cuando se crea un sidecar de aplicación para el registro, la supervisión o cualquier otra configuración donde un servicio necesita un segundo proceso asociado.</span><span class="sxs-lookup"><span data-stu-id="f898e-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="f898e-106">Este documento describe la ejecución de una configuración de sidecar de varios contenedores sencilla mediante una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f898e-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-the-template"></a><span data-ttu-id="f898e-107">Configuración de la plantilla</span><span class="sxs-lookup"><span data-stu-id="f898e-107">Configure the template</span></span>

<span data-ttu-id="f898e-108">Cree un archivo denominado `azuredeploy.json` y copie el siguiente código json en él.</span><span class="sxs-lookup"><span data-stu-id="f898e-108">Create a file named `azuredeploy.json` and copy the following json into it.</span></span> 

<span data-ttu-id="f898e-109">En este ejemplo, se definen un grupo de contenedores con dos contenedores y una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="f898e-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="f898e-110">El primer contenedor del grupo ejecuta una aplicación accesible desde Internet.</span><span class="sxs-lookup"><span data-stu-id="f898e-110">The first container of the group runs an internet facing application.</span></span> <span data-ttu-id="f898e-111">El segundo contenedor, el sidecar, realiza una solicitud HTTP a la aplicación web principal a través de la red local del grupo.</span><span class="sxs-lookup"><span data-stu-id="f898e-111">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span></span> 

<span data-ttu-id="f898e-112">Este ejemplo de sidecar podría ampliarse para desencadenar una alerta si recibe un código de respuesta HTTP distinto de 200 OK.</span><span class="sxs-lookup"><span data-stu-id="f898e-112">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="f898e-113">Para usar un registro de imagen de contenedor privado, agregue un objeto al documento json con el formato siguiente.</span><span class="sxs-lookup"><span data-stu-id="f898e-113">To use a private container image registry, add an object to the json document with the following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-the-template"></a><span data-ttu-id="f898e-114">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="f898e-114">Deploy the template</span></span>

<span data-ttu-id="f898e-115">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f898e-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="f898e-116">Implemente la plantilla con el comando [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="f898e-116">Deploy the template with the [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="f898e-117">Al cabo de unos segundos, recibirá una respuesta inicial de Azure.</span><span class="sxs-lookup"><span data-stu-id="f898e-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="f898e-118">Visualización del estado de la implementación</span><span class="sxs-lookup"><span data-stu-id="f898e-118">View deployment state</span></span>

<span data-ttu-id="f898e-119">Para ver el estado de la implementación, use el comando `az container show`.</span><span class="sxs-lookup"><span data-stu-id="f898e-119">To view the state of the deployment, use the `az container show` command.</span></span> <span data-ttu-id="f898e-120">Esto devuelve la dirección IP pública aprovisionada a través de la cual se puede acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f898e-120">This returns the provisioned public IP address over which the application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="f898e-121">Salida:</span><span class="sxs-lookup"><span data-stu-id="f898e-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="f898e-122">Ver registros</span><span class="sxs-lookup"><span data-stu-id="f898e-122">View logs</span></span>   

<span data-ttu-id="f898e-123">Vea la salida del registro de un contenedor mediante el comando `az container logs`.</span><span class="sxs-lookup"><span data-stu-id="f898e-123">View the log output of a container using the `az container logs` command.</span></span> <span data-ttu-id="f898e-124">El argumento `--container-name` especifica el contenedor del que se van a extraer registros.</span><span class="sxs-lookup"><span data-stu-id="f898e-124">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="f898e-125">En este ejemplo, se especifica el primer contenedor.</span><span class="sxs-lookup"><span data-stu-id="f898e-125">In this example, the first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="f898e-126">Salida:</span><span class="sxs-lookup"><span data-stu-id="f898e-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="f898e-127">Para ver los registros para el contenedor sidecar, ejecute el mismo comando especificando el segundo nombre del contenedor.</span><span class="sxs-lookup"><span data-stu-id="f898e-127">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="f898e-128">Salida:</span><span class="sxs-lookup"><span data-stu-id="f898e-128">Output:</span></span>

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

<span data-ttu-id="f898e-129">Como puede ver, el sidecar realiza periódicamente una solicitud HTTP a la aplicación web principal a través de la red local del grupo para asegurarse de que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="f898e-129">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f898e-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f898e-130">Next steps</span></span>

<span data-ttu-id="f898e-131">En este documento se explican los pasos necesarios para implementar una instancia de contenedor de Azure de varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="f898e-131">This document covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="f898e-132">Para obtener una experiencia integral de Azure Container Instances, consulte el tutorial de Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="f898e-132">For an end to end Azure Container Instances experience, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="f898e-133">[Tutorial de Azure Container Instances]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="f898e-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
