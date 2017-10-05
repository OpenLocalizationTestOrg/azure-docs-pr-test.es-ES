---
title: "Creación de un centro de IoT Hub mediante la CLI de Azure (azure.js) | Microsoft Docs"
description: "Describe cómo crear un centro de IoT Hub de Azure mediante la CLI de Azure entre plataformas (azure.js)."
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
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="0a57f-103">Creación de una instancia de IoT Hub mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0a57f-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="0a57f-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="0a57f-104">Introduction</span></span>

<span data-ttu-id="0a57f-105">Puede usar la CLI de Azure (azure.js) para crear y administrar los centros de IoT Hub de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="0a57f-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="0a57f-106">En este artículo se muestra cómo utilizar la CLI de Azure (azure.js) para crear un centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0a57f-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="0a57f-107">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="0a57f-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="0a57f-108">CLI de Azure (azure.js): la CLI de los modelos de implementación de administración de recursos y clásico, tal y como se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="0a57f-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="0a57f-109">[CLI de Azure 2.0 (az.py)](iot-hub-create-using-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a57f-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="0a57f-110">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a57f-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0a57f-111">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0a57f-111">An active Azure account.</span></span> <span data-ttu-id="0a57f-112">En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0a57f-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0a57f-113">[CLI de Azure 0.10.4][lnk-CLI-install] o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="0a57f-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="0a57f-114">Si ya tiene la CLI de Azure instalada, puede validar la versión actual en el símbolo del sistema con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0a57f-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="0a57f-115">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0a57f-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0a57f-116">La CLI de Azure debe estar en el modo Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="0a57f-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="0a57f-117">Definición de su cuenta y suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="0a57f-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="0a57f-118">En el símbolo del sistema, escriba el siguiente comando para iniciar sesión:</span><span class="sxs-lookup"><span data-stu-id="0a57f-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="0a57f-119">Utilice el explorador web sugerido y el código de autenticación.</span><span class="sxs-lookup"><span data-stu-id="0a57f-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="0a57f-120">Si tiene varias suscripciones de Azure, la conexión a Azure le concede acceso a todas las suscripciones asociadas a sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0a57f-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0a57f-121">Puede ver las suscripciones de Azure, y determinar cuál es la predeterminada, mediante el comando:</span><span class="sxs-lookup"><span data-stu-id="0a57f-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="0a57f-122">Para establecer el contexto de la suscripción en el que desea ejecutar el resto de los comandos, use:</span><span class="sxs-lookup"><span data-stu-id="0a57f-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="0a57f-123">Si no tiene un grupo de recursos, puede crear uno denominado **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="0a57f-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="0a57f-124">El artículo [Uso de la CLI de Azure para administrar los recursos y grupos de recursos de Azure][lnk-CLI-arm] ofrece más información sobre cómo usar la CLI de Azure para administrar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a57f-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="0a57f-125">Creación de un IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0a57f-125">Create an IoT Hub</span></span>

<span data-ttu-id="0a57f-126">Parámetros obligatorios:</span><span class="sxs-lookup"><span data-stu-id="0a57f-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="0a57f-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="0a57f-127">**resource-group**.</span></span> <span data-ttu-id="0a57f-128">El nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a57f-128">The resource group name.</span></span> <span data-ttu-id="0a57f-129">El formato no distingue mayúsculas de minúsculas, admite caracteres alfanuméricos, guiones bajos y guiones, y debe tener una longitud de entre 1 y 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0a57f-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="0a57f-130">**nombre**.</span><span class="sxs-lookup"><span data-stu-id="0a57f-130">**name**.</span></span> <span data-ttu-id="0a57f-131">El nombre del centro de IoT Hub que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="0a57f-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="0a57f-132">El formato no distingue mayúsculas de minúsculas, admite caracteres alfanuméricos, guiones bajos y guiones, y debe tener una longitud de entre 3 y 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0a57f-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="0a57f-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="0a57f-133">**location**.</span></span> <span data-ttu-id="0a57f-134">La ubicación (centro de datos/región de Azure) para aprovisionar el centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0a57f-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="0a57f-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="0a57f-135">**sku-name**.</span></span> <span data-ttu-id="0a57f-136">El nombre de la SKU; uno de los siguientes: [F1, S1, S2 o S3].</span><span class="sxs-lookup"><span data-stu-id="0a57f-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="0a57f-137">Para consultar la lista completa más reciente, diríjase a la página de precios de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0a57f-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="0a57f-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="0a57f-138">**units**.</span></span> <span data-ttu-id="0a57f-139">El número de unidades aprovisionadas.</span><span class="sxs-lookup"><span data-stu-id="0a57f-139">The number of provisioned units.</span></span> <span data-ttu-id="0a57f-140">Intervalo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="0a57f-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="0a57f-141">Las unidades de IoT Hub se basan en el recuento total de mensajes y en el número de dispositivos que desea conectar.</span><span class="sxs-lookup"><span data-stu-id="0a57f-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="0a57f-142">Para ver todos los parámetros de creación disponibles, puede usar el comando de ayuda en el símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="0a57f-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="0a57f-143">Ejemplo rápido: para crear un centro de IoT Hub denominado **exampleIoTHubName** en el grupo de recursos **exampleResourceGroup**, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0a57f-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="0a57f-144">Este comando de la CLI de Azure crea un IoT Hub Estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="0a57f-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="0a57f-145">Puede eliminar el IoT Hub denominado **exampleIoTHubName** con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0a57f-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="0a57f-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a57f-146">Next steps</span></span>

<span data-ttu-id="0a57f-147">Para obtener más información sobre cómo desarrollar para IoT Hub, consulte el siguiente artículo:</span><span class="sxs-lookup"><span data-stu-id="0a57f-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="0a57f-148">[SDK de IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="0a57f-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0a57f-149">Para explorar aún más las funcionalidades de Centro de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="0a57f-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0a57f-150">[Uso de Azure Portal para administrar IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="0a57f-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
