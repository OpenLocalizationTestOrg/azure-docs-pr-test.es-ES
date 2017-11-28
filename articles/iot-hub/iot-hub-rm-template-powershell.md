---
title: aaaCreate un centro de IoT de Azure mediante una plantilla (PowerShell) | Documentos de Microsoft
description: "¿Cómo toouse un toocreate de plantilla un centro de IoT con PowerShell de Azure Resource Manager."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="0cf19-103">Creación de un centro de IoT con una plantilla de Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0cf19-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="0cf19-104">Puede usar el Administrador de recursos de Azure toocreate y administrar centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="0cf19-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="0cf19-105">Este tutorial muestra cómo toouse una toocreate de plantilla un centro de IoT con PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0cf19-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="0cf19-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0cf19-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0cf19-107">Este artículo tratan con modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0cf19-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="0cf19-108">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0cf19-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0cf19-109">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0cf19-109">An active Azure account.</span></span> <br/><span data-ttu-id="0cf19-110">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0cf19-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0cf19-111">[Azure PowerShell 1.0][lnk-powershell-install] o posterior.</span><span class="sxs-lookup"><span data-stu-id="0cf19-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="0cf19-112">artículo de Hello [con Azure PowerShell con el Administrador de recursos de Azure] [ lnk-powershell-arm] proporciona más información acerca de cómo toouse PowerShell y el Administrador de recursos de Azure plantillas toocreate Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="0cf19-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="0cf19-113">Conectar tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="0cf19-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="0cf19-114">En un símbolo del sistema de PowerShell, escriba Hola después comando toosign en tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="0cf19-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0cf19-115">Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="0cf19-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0cf19-116">Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:</span><span class="sxs-lookup"><span data-stu-id="0cf19-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="0cf19-117">Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0cf19-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="0cf19-118">Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="0cf19-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="0cf19-119">Puede usar Hola después toodiscover de comandos que puede implementar un centro de IoT y Hola admite versiones de API:</span><span class="sxs-lookup"><span data-stu-id="0cf19-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="0cf19-120">Crear un toocontain de grupo de recursos de su centro de IoT mediante el siguiente comando en una de las ubicaciones de hello compatible para el centro de IoT de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cf19-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="0cf19-121">En este ejemplo se crea un grupo de recursos denominado **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="0cf19-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="0cf19-122">Enviar una toocreate de plantilla un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="0cf19-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="0cf19-123">Utilice un toocreate de plantilla JSON un centro de IoT en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0cf19-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="0cf19-124">También puede utilizar un centro de IoT Azure Resource Manager plantilla toomake cambios tooan existente.</span><span class="sxs-lookup"><span data-stu-id="0cf19-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="0cf19-125">Usar un toocreate de editor de texto llama a una plantilla de Azure Resource Manager **template.json** con Hola siguientes toocreate de definición de recursos de un nuevo centro de IoT estándar.</span><span class="sxs-lookup"><span data-stu-id="0cf19-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="0cf19-126">Este ejemplo agrega Hola centro de IoT en hello **este de EE.** región, crea dos grupos de consumidores (**cg1** y **cg2**) en el punto de conexión de hello compatible con el centro de eventos y usa hello **2016-02-03** versión de API.</span><span class="sxs-lookup"><span data-stu-id="0cf19-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="0cf19-127">Esta plantilla también espera toopass en nombre del centro de IoT Hola como un parámetro denominado **hubName**.</span><span class="sxs-lookup"><span data-stu-id="0cf19-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="0cf19-128">Consulte lista actual de Hola de ubicaciones que admiten el centro de IoT [estado de Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="0cf19-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="0cf19-129">Guardar archivo de plantilla de Azure Resource Manager hello en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="0cf19-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="0cf19-130">En este ejemplo, se da por supuesto que lo guarda en una carpeta llamada **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="0cf19-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="0cf19-131">Ejecute hello después comando toodeploy el nuevo centro de IoT, pasando el nombre de Hola de su centro de IoT como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="0cf19-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="0cf19-132">En este ejemplo, nombre de Hola de centro de IoT hello es `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="0cf19-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="0cf19-133">nombre de Hola de su centro de IoT debe ser único globalmente:</span><span class="sxs-lookup"><span data-stu-id="0cf19-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="0cf19-134">salida de Hello muestra las claves de hello para el centro de IoT de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="0cf19-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="0cf19-135">tooverify agregado la aplicación Hola nuevo centro de IoT, visite hello [portal de Azure] [ lnk-azure-portal] y ver la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="0cf19-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="0cf19-136">O bien, usar hello **Get-AzureRmResource** cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0cf19-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="0cf19-137">Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="0cf19-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="0cf19-138">Puede eliminar el centro de IoT de Hola a través de hello [portal de Azure] [ lnk-azure-portal] o mediante el uso de hello **Remove-AzureRmResource** cmdlet de PowerShell cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="0cf19-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cf19-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0cf19-139">Next steps</span></span>

<span data-ttu-id="0cf19-140">Ahora que ha implementado un centro de IoT usando una plantilla de administrador de recursos de Azure con PowerShell, puede que desee tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="0cf19-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="0cf19-141">Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="0cf19-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="0cf19-142">Lectura [Introducción al administrador de recursos de Azure] [ lnk-azure-rm-overview] toolearn más información acerca de las capacidades de hello del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cf19-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="0cf19-143">toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="0cf19-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="0cf19-144">[Introducción tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="0cf19-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="0cf19-145">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="0cf19-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0cf19-146">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="0cf19-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0cf19-147">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0cf19-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
