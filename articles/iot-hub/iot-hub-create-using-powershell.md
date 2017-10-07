---
title: aaaCreate un centro de IoT de Azure con un cmdlet de PowerShell | Documentos de Microsoft
description: "¿Cómo toouse un toocreate de cmdlet de PowerShell un centro de IoT."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="fa5f4-103">Crear un centro de IoT mediante el cmdlet New-AzureRmIotHub Hola</span><span class="sxs-lookup"><span data-stu-id="fa5f4-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="fa5f4-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="fa5f4-104">Introduction</span></span>

<span data-ttu-id="fa5f4-105">Puede usar toocreate de cmdlets de PowerShell de Azure y administre centros de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="fa5f4-106">Este tutorial muestra cómo toocreate un centro de IoT con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="fa5f4-107">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa5f4-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fa5f4-108">Este artículo tratan con modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="fa5f4-109">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="fa5f4-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-110">An active Azure account.</span></span> <br/><span data-ttu-id="fa5f4-111">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="fa5f4-112">[Cmdlets de Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="fa5f4-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="fa5f4-113">Conectar tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="fa5f4-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="fa5f4-114">En un símbolo del sistema de PowerShell, escriba Hola después comando toosign en tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="fa5f4-115">Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="fa5f4-116">Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="fa5f4-117">Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="fa5f4-118">Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="fa5f4-119">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fa5f4-119">Create resource group</span></span>

<span data-ttu-id="fa5f4-120">Es necesario un toodeploy de grupo de recursos un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="fa5f4-121">Puede usar un grupo de recursos existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="fa5f4-122">Puede usar hello en el que puede implementar un centro de IoT de comando toodiscover Hola ubicaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="fa5f4-123">toocreate un grupo de recursos para el centro de IoT de hello admite ubicaciones de centro de IoT, Hola de uso siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="fa5f4-124">Este ejemplo crea un grupo de recursos denominado **MyIoTRG1** en hello **UU** región:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="fa5f4-125">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="fa5f4-125">Create an IoT hub</span></span>

<span data-ttu-id="fa5f4-126">toocreate un centro de IoT en grupo de recursos de Hola que creó en el paso anterior hello, Hola de uso siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="fa5f4-127">Este ejemplo se crea un **S1** concentrador llama **MyTestIoTHub** en hello **UU** región:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="fa5f4-128">nombre de Hola de centro de IoT Hola debe ser único.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="fa5f4-129">Puede enumerar todos los centros de IoT de hello en su suscripción mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="fa5f4-130">ejemplo de Hola anterior agrega un centro de IoT S1 estándar para la que se facturan.</span><span class="sxs-lookup"><span data-stu-id="fa5f4-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="fa5f4-131">Puede eliminar el centro de IoT de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="fa5f4-132">Como alternativa, puede quitar un grupo de recursos y todos los recursos que contiene utilizando el siguiente comando de Hola de Hola:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="fa5f4-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fa5f4-133">Next steps</span></span>

<span data-ttu-id="fa5f4-134">Ahora que ha implementado un centro de IoT mediante un cmdlet de PowerShell, puede que desee tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="fa5f4-135">Descubra otros [cmdlets de PowerShell para trabajar con la instancia de IoT Hub][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="fa5f4-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="fa5f4-136">Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="fa5f4-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="fa5f4-137">toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="fa5f4-138">[Introducción tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="fa5f4-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="fa5f4-139">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="fa5f4-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="fa5f4-140">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="fa5f4-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="fa5f4-141">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="fa5f4-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md