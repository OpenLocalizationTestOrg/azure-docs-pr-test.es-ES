---
title: "Creación de un centro de IoT de Azure mediante una plantilla (PowerShell) | Microsoft Docs"
description: "Describe cómo usar una plantilla de Azure Resource Manager para crear un centro de IoT con PowerShell."
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
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="45b5c-103">Creación de un centro de IoT con una plantilla de Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="45b5c-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="45b5c-104">Puede usar Azure Resource Manager para crear y administrar los centros de IoT de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="45b5c-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="45b5c-105">En este tutorial se muestra cómo usar una plantilla de Azure Resource Manager para crear un IoT Hub con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45b5c-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="45b5c-106">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="45b5c-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="45b5c-107">Este artículo trata sobre el uso del modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45b5c-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="45b5c-108">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="45b5c-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="45b5c-109">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="45b5c-109">An active Azure account.</span></span> <br/><span data-ttu-id="45b5c-110">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="45b5c-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="45b5c-111">[Azure PowerShell 1.0][lnk-powershell-install] o posterior.</span><span class="sxs-lookup"><span data-stu-id="45b5c-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="45b5c-112">El artículo [Uso de Azure PowerShell con Azure Resource Manager][lnk-powershell-arm] contiene más información sobre cómo utilizar PowerShell y plantillas de Azure Resource Manager para crear recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="45b5c-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="45b5c-113">Conexión a su suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="45b5c-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="45b5c-114">En un símbolo del sistema de PowerShell, escriba el siguiente comando para iniciar sesión en su suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="45b5c-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="45b5c-115">Si tiene varias suscripciones de Azure, el inicio de sesión en Azure le concede acceso a todas las suscripciones de Azure asociadas a sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="45b5c-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="45b5c-116">Use el siguiente comando para mostrar las suscripciones de Azure que están disponibles para su uso:</span><span class="sxs-lookup"><span data-stu-id="45b5c-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="45b5c-117">Use el siguiente comando para seleccionar la suscripción que desea usar para ejecutar los comandos que crearán la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="45b5c-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="45b5c-118">Puede usar el nombre de la suscripción o el identificador de la salida del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="45b5c-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="45b5c-119">Puede usar los comandos siguientes para conocer donde puede implementar un centro de IoT y las versiones de API admitidas actualmente:</span><span class="sxs-lookup"><span data-stu-id="45b5c-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="45b5c-120">Cree un grupo de recursos para que contenga su centro de IoT mediante el siguiente comando en una de las ubicaciones compatibles para IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="45b5c-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="45b5c-121">En este ejemplo se crea un grupo de recursos denominado **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="45b5c-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="45b5c-122">Enviar una plantilla para crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="45b5c-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="45b5c-123">Use una plantilla de JSON para crear un nuevo centro de IoT en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="45b5c-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="45b5c-124">También puede usar una plantilla de Azure Resource Manager para realizar cambios en un IoT Hub existente.</span><span class="sxs-lookup"><span data-stu-id="45b5c-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="45b5c-125">Use un editor de texto para crear una plantilla de Azure Resource Manager llamada **template.json** , con la siguiente definición de recursos, para crear un nuevo IoT Hub estándar.</span><span class="sxs-lookup"><span data-stu-id="45b5c-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="45b5c-126">Este ejemplo agrega el centro de IoT en la región **este de EE. UU.**, crea dos grupos de consumidores (**cg1** and **cg2**) en el punto de conexión compatible con centros de eventos y usa la versión de API **2016-02-03**.</span><span class="sxs-lookup"><span data-stu-id="45b5c-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="45b5c-127">En esta plantilla se espera también que pase el nombre del centro de IoT como un parámetro denominado **hubName**.</span><span class="sxs-lookup"><span data-stu-id="45b5c-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="45b5c-128">Para ver una lista actualizada de las ubicaciones admitidas en IoT Hub, consulte [Estado de Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="45b5c-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="45b5c-129">Guarde el archivo de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45b5c-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="45b5c-130">En este ejemplo, se da por supuesto que lo guarda en una carpeta llamada **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="45b5c-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="45b5c-131">Ejecute el comando siguiente para implementar el nuevo centro de IoT, pasando el nombre de su centro de IoT como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="45b5c-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="45b5c-132">En este ejemplo, el nombre de la instancia de IoT Hub es `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="45b5c-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="45b5c-133">El nombre de su instancia de IoT Hub debe único globalmente:</span><span class="sxs-lookup"><span data-stu-id="45b5c-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="45b5c-134">El resultado muestra las claves para el centro de IoT que ha creado.</span><span class="sxs-lookup"><span data-stu-id="45b5c-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="45b5c-135">Para comprobar que la aplicación ha agregado la nueva instancia de IoT Hub, visite [Azure Portal][lnk-azure-portal] y vea la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="45b5c-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="45b5c-136">Como alternativa, use el cmdlet de PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="45b5c-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="45b5c-137">Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará.</span><span class="sxs-lookup"><span data-stu-id="45b5c-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="45b5c-138">Cuando haya terminado, podrá eliminar el centro de IoT Hub a través de [Azure Portal][lnk-azure-portal] o mediante el cmdlet **Remove-AzureRmResource** de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45b5c-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45b5c-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45b5c-139">Next steps</span></span>

<span data-ttu-id="45b5c-140">Ahora que ha implementado un IoT Hub mediante una plantilla de Azure Resource Manager con PowerShell, quizá desee seguir explorando:</span><span class="sxs-lookup"><span data-stu-id="45b5c-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="45b5c-141">Consulte las funcionalidades de la [API de REST del proveedor de recursos de IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="45b5c-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="45b5c-142">Para más información sobre las funcionalidades de Azure Resource Manager, consulte [Información general de Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="45b5c-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="45b5c-143">Para obtener más información sobre cómo desarrollar para IoT Hub, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="45b5c-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="45b5c-144">[Introducción al SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="45b5c-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="45b5c-145">[SDK de IoT de Azure][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="45b5c-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="45b5c-146">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="45b5c-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="45b5c-147">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="45b5c-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
