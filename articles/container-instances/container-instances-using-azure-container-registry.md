---
title: aaaDeploy tooAzure instancias de contenedor de hello del registro de contenedor de Azure | Documentos de Azure
description: Implementar instancias de contenedor tooAzure de hello del registro de contenedor de Azure
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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="91cc6-103">Implementar instancias de contenedor tooAzure de hello del registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="91cc6-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="91cc6-104">Hola del registro de contenedor de Azure es un registro basado en Azure, privado, para las imágenes de contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="91cc6-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="91cc6-105">Este artículo trata cómo imágenes del contenedor toodeploy almacenan Hola del registro de contenedor de Azure tooAzure instancias de contenedor.</span><span class="sxs-lookup"><span data-stu-id="91cc6-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="91cc6-106">Uso de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="91cc6-106">Using hello Azure CLI</span></span>

<span data-ttu-id="91cc6-107">Hola CLI de Azure incluye comandos para crear y administrar contenedores en instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="91cc6-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="91cc6-108">Si especifica una imagen privada en hello `create` comando, también puede especificar Hola imagen del registro requiere una contraseña tooauthenticate con registro de contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="91cc6-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="91cc6-109">Hola `create` el comando también admite la especificación de hello `registry-login-server` y `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="91cc6-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="91cc6-110">Sin embargo, servidor de inicio de sesión de Hola para saludo del registro de contenedor de Azure es siempre *registryname*. nombre de usuario predeterminado hello y azurecr.io es *registryname*, por lo que estos valores se deducen del nombre de la imagen de hello si no se proporcionan explícitamente.</span><span class="sxs-lookup"><span data-stu-id="91cc6-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="91cc6-111">Uso de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91cc6-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="91cc6-112">Puede especificar propiedades de Hola de seguridad del registro de contenedor de Azure en una plantilla de Azure Resource Manager mediante la inclusión de hello `imageRegistryCredentials` propiedad de definición de grupo del contenedor de hello:</span><span class="sxs-lookup"><span data-stu-id="91cc6-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="91cc6-113">tooavoid almacenar la contraseña del registro de contenedor directamente en la plantilla de hello, se recomienda que se almacenan como un secreto en [el almacén de claves de Azure](../key-vault/key-vault-manage-with-cli2.md) y hacer referencia a él en plantilla de hello mediante hello [integración nativa entre Hola, Administrador de recursos de Azure y el almacén de claves](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="91cc6-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="91cc6-114">Uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="91cc6-114">Using hello Azure portal</span></span>

<span data-ttu-id="91cc6-115">Si mantener imágenes de contenedor en hello del registro de contenedor de Azure, puede crear fácilmente un contenedor en instancias de contenedor de Azure mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="91cc6-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="91cc6-116">Hola portal de Azure, navegue tooyour registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="91cc6-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="91cc6-117">Elija Repositorios.</span><span class="sxs-lookup"><span data-stu-id="91cc6-117">Choose Repositories.</span></span>

    ![menú de registro de contenedor de Azure Hola Hola portal de Azure][acr-menu]

3. <span data-ttu-id="91cc6-119">Elija el repositorio de Hola que desee toodeploy desde.</span><span class="sxs-lookup"><span data-stu-id="91cc6-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="91cc6-120">Haga clic en la etiqueta de hello para la imagen de contenedor de hello desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="91cc6-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Menú contextual para iniciar el contenedor con Azure Container Instances][acr-runinstance-contextmenu]

5. <span data-ttu-id="91cc6-122">Escriba un nombre para el contenedor de Hola y un nombre para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="91cc6-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="91cc6-123">También puede cambiar los valores predeterminados de hello si lo desea.</span><span class="sxs-lookup"><span data-stu-id="91cc6-123">You can also change hello default values if you wish.</span></span>

    ![Menú Crear para Azure Container Instances][acr-create-deeplink]

6. <span data-ttu-id="91cc6-125">Una vez que se haya completado la implementación de hello, puede navegar por grupo de contenedor toohello de hello notificaciones panel toofind su dirección IP y otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="91cc6-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Vista de detalles del grupo de contenedores de Azure Container Instances][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="91cc6-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91cc6-127">Next steps</span></span>

<span data-ttu-id="91cc6-128">Saber cómo insertarlas del registro de contenedor privado tooa toobuild contenedores e implementarlos en instancias de contenedor de tooAzure por [completar el tutorial de hello](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="91cc6-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
