---
title: aaaCreate un centro de IoT mediante Azure CLI (az.py) | Documentos de Microsoft
description: "¿Cómo toocreate un centro de IoT de Azure utilizando Hola multiplataforma Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="ff561-103">Crear un centro de IoT con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ff561-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="ff561-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="ff561-104">Introduction</span></span>

<span data-ttu-id="ff561-105">Puede usar toocreate de CLI de Azure 2.0 (az.py) y administrar los centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="ff561-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="ff561-106">Este artículo muestra cómo toouse Hola toocreate de CLI de Azure 2.0 (az.py) a un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ff561-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="ff561-107">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="ff561-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="ff561-108">[CLI de Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) : Hola CLI para modelos de implementación de administración de recursos y clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="ff561-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="ff561-109">Azure CLI 2.0 (az.py) - Hola CLI de próxima generación para el modelo de implementación de administración de hello recursos tal como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ff561-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="ff561-110">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff561-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ff561-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ff561-111">An active Azure account.</span></span> <span data-ttu-id="ff561-112">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ff561-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ff561-113">[CLI de Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="ff561-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="ff561-114">Inicio de sesión y configuración de la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="ff561-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="ff561-115">Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="ff561-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="ff561-116">En el símbolo de hello, ejecute hello [comando de inicio de sesión][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="ff561-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="ff561-117">Siga Hola instrucciones tooauthenticate utilizando el código de hello e inicie sesión en tooyour cuenta de Azure a través de un explorador web.</span><span class="sxs-lookup"><span data-stu-id="ff561-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="ff561-118">Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall Hola asociadas con sus credenciales de cuentas de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff561-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="ff561-119">Utilice Hola siguiente [toolist comando Hola cuentas de Azure] [ lnk-az-account-command] disponibles para toouse:</span><span class="sxs-lookup"><span data-stu-id="ff561-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="ff561-120">Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ff561-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="ff561-121">Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="ff561-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="ff561-122">Creación de un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ff561-122">Create an IoT Hub</span></span>

<span data-ttu-id="ff561-123">Use hello Azure CLI toocreate un grupo de recursos y, a continuación, agregue un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ff561-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="ff561-124">Cuando crea una instancia de IoT Hub, debe crearla en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ff561-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="ff561-125">Utilice un grupo de recursos existente, o bien ejecute hello siguiente [comando toocreate un grupo de recursos][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="ff561-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="ff561-126">ejemplo de Hola anterior crea grupo de recursos de hello en hello ubicación oeste de EE..</span><span class="sxs-lookup"><span data-stu-id="ff561-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="ff561-127">Puede ver una lista de ubicaciones disponibles mediante la ejecución de comando hello `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="ff561-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="ff561-128">Ejecute hello siguiente [comando toocreate un centro de IoT] [ lnk-az-iot-command] en el grupo de recursos, con un nombre único global para el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="ff561-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="ff561-129">comando anterior Hola crea un centro de IoT en hello S1 para el que se le cobra según el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="ff561-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="ff561-130">Para más información, consulte el artículo sobre los [precios de Azure IoT Hub][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="ff561-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="ff561-131">Eliminación de una instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ff561-131">Remove an IoT Hub</span></span>

<span data-ttu-id="ff561-132">Puede usar hello Azure CLI demasiado[eliminar un recurso individual][lnk-az-resource-command], como un centro de IoT o eliminar un grupo de recursos y todos sus recursos, incluidos los centros de IoT.</span><span class="sxs-lookup"><span data-stu-id="ff561-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="ff561-133">toodelete un centro de IoT, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="ff561-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="ff561-134">toodelete de comandos de un grupo de recursos y todos sus recursos, ejecución Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff561-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="ff561-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff561-135">Next steps</span></span>
<span data-ttu-id="ff561-136">toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ff561-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="ff561-137">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ff561-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="ff561-138">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="ff561-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ff561-139">[Uso de hello toomanage portal Azure centro de IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="ff561-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
