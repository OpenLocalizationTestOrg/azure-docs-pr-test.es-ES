---
title: aaaCreate un centro de IoT mediante Azure CLI (azure.js) | Documentos de Microsoft
description: "¿Cómo toocreate un centro de IoT de Azure utilizando Hola multiplataforma Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="c97c8-103">Crear un centro de IoT con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c97c8-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="c97c8-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="c97c8-104">Introduction</span></span>

<span data-ttu-id="c97c8-105">Puede usar toocreate de CLI de Azure (azure.js) y administrar los centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c97c8-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="c97c8-106">Este artículo muestra cómo toouse Hola toocreate de CLI de Azure (azure.js) a un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c97c8-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="c97c8-107">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="c97c8-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="c97c8-108">CLI de Azure (azure.js): Hola CLI hello clásico y modelos de implementación de administración de recursos como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="c97c8-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="c97c8-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -Hola CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c97c8-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="c97c8-110">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c97c8-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c97c8-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c97c8-111">An active Azure account.</span></span> <span data-ttu-id="c97c8-112">En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c97c8-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="c97c8-113">[CLI de Azure 0.10.4][lnk-CLI-install] o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="c97c8-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="c97c8-114">Si ya tienes Hola CLI de Azure instalado, puede validar versión actual de hello en el símbolo del sistema Hola con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c97c8-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="c97c8-115">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c97c8-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c97c8-116">Hola CLI de Azure debe estar en modo Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c97c8-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="c97c8-117">Definición de su cuenta y suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="c97c8-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="c97c8-118">En el símbolo de hello, inicio de sesión, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c97c8-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="c97c8-119">Hola uso sugerido explorador web y tooauthenticate de código.</span><span class="sxs-lookup"><span data-stu-id="c97c8-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="c97c8-120">Si tiene varias suscripciones de Azure, conectar tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="c97c8-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="c97c8-121">Puede ver Hola suscripciones de Azure e identifique cuál es la predeterminada de hello, mediante el comando hello:</span><span class="sxs-lookup"><span data-stu-id="c97c8-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="c97c8-122">uso de comandos de contexto de suscripción de hello tooset bajo el cual desea rest de hello toorun de hello:</span><span class="sxs-lookup"><span data-stu-id="c97c8-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="c97c8-123">Si no tiene un grupo de recursos, puede crear uno denominado **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="c97c8-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="c97c8-124">artículo de Hello [usar hello Azure CLI toomanage Azure y grupos de recursos] [ lnk-CLI-arm] proporciona más información acerca de cómo toouse hello Azure CLI toomanage Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="c97c8-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c97c8-125">Creación de un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c97c8-125">Create an IoT Hub</span></span>

<span data-ttu-id="c97c8-126">Parámetros obligatorios:</span><span class="sxs-lookup"><span data-stu-id="c97c8-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="c97c8-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="c97c8-127">**resource-group**.</span></span> <span data-ttu-id="c97c8-128">nombre del grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c97c8-128">hello resource group name.</span></span> <span data-ttu-id="c97c8-129">formato de Hello es entre mayúsculas y minúsculas alfanuméricos, caracteres de subrayado y guiones, longitud de 1-64.</span><span class="sxs-lookup"><span data-stu-id="c97c8-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="c97c8-130">**nombre**.</span><span class="sxs-lookup"><span data-stu-id="c97c8-130">**name**.</span></span> <span data-ttu-id="c97c8-131">nombre de Hola de hello IoT hub toobe creado.</span><span class="sxs-lookup"><span data-stu-id="c97c8-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="c97c8-132">formato de Hello es entre mayúsculas y minúsculas alfanuméricos, caracteres de subrayado y guiones, longitud de 3-50.</span><span class="sxs-lookup"><span data-stu-id="c97c8-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="c97c8-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="c97c8-133">**location**.</span></span> <span data-ttu-id="c97c8-134">Centro de IoT Hola de Hello ubicación (región/centro de datos azure) tooprovision.</span><span class="sxs-lookup"><span data-stu-id="c97c8-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="c97c8-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="c97c8-135">**sku-name**.</span></span> <span data-ttu-id="c97c8-136">nombre de Hola de sku de hello, uno de: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="c97c8-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="c97c8-137">Para la lista completa de hello más reciente, consulte toohello página de precios para el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c97c8-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="c97c8-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="c97c8-138">**units**.</span></span> <span data-ttu-id="c97c8-139">número de Hola de unidades de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="c97c8-139">hello number of provisioned units.</span></span> <span data-ttu-id="c97c8-140">Intervalo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="c97c8-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="c97c8-141">Unidades de centro de IoT se basan en el número total de mensajes, hello y recuento de dispositivos que desee tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c97c8-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="c97c8-142">toosee Hola a todos los parámetros disponibles para la creación, puede usar comandos de la Ayuda de hello en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="c97c8-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="c97c8-143">Ejemplo rápido: toocreate llama a un centro de IoT **exampleIoTHubName** en grupo de recursos de hello **exampleResourceGroup**, ejecute hello comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c97c8-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="c97c8-144">Este comando de la CLI de Azure crea un IoT Hub Estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="c97c8-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="c97c8-145">Puede eliminar el centro de IoT de hello **exampleIoTHubName** con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c97c8-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="c97c8-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c97c8-146">Next steps</span></span>

<span data-ttu-id="c97c8-147">toolearn más sobre el desarrollo de centro de IoT, vea Hola artículo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c97c8-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="c97c8-148">[SDK de IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="c97c8-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="c97c8-149">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="c97c8-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c97c8-150">[Uso de hello toomanage portal Azure centro de IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="c97c8-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
