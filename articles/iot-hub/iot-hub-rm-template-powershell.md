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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Creación de un centro de IoT con una plantilla de Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Puede usar el Administrador de recursos de Azure toocreate y administrar centros de IoT de Azure mediante programación. Este tutorial muestra cómo toouse una toocreate de plantilla un centro de IoT con PowerShell de Azure Resource Manager.

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello Azure Resource Manager.

toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. <br/>Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [Azure PowerShell 1.0][lnk-powershell-install] o posterior.

> [!TIP]
> artículo de Hello [con Azure PowerShell con el Administrador de recursos de Azure] [ lnk-powershell-arm] proporciona más información acerca de cómo toouse PowerShell y el Administrador de recursos de Azure plantillas toocreate Azure recursos.

## <a name="connect-tooyour-azure-subscription"></a>Conectar tooyour suscripción de Azure

En un símbolo del sistema de PowerShell, escriba Hola después comando toosign en tooyour suscripción de Azure:

```powershell
Login-AzureRmAccount
```

Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales. Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:

```powershell
Get-AzureRMSubscription
```

Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT. Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

Puede usar Hola después toodiscover de comandos que puede implementar un centro de IoT y Hola admite versiones de API:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Crear un toocontain de grupo de recursos de su centro de IoT mediante el siguiente comando en una de las ubicaciones de hello compatible para el centro de IoT de Hola. En este ejemplo se crea un grupo de recursos denominado **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Enviar una toocreate de plantilla un centro de IoT

Utilice un toocreate de plantilla JSON un centro de IoT en el grupo de recursos. También puede utilizar un centro de IoT Azure Resource Manager plantilla toomake cambios tooan existente.

1. Usar un toocreate de editor de texto llama a una plantilla de Azure Resource Manager **template.json** con Hola siguientes toocreate de definición de recursos de un nuevo centro de IoT estándar. Este ejemplo agrega Hola centro de IoT en hello **este de EE.** región, crea dos grupos de consumidores (**cg1** y **cg2**) en el punto de conexión de hello compatible con el centro de eventos y usa hello **2016-02-03** versión de API. Esta plantilla también espera toopass en nombre del centro de IoT Hola como un parámetro denominado **hubName**. Consulte lista actual de Hola de ubicaciones que admiten el centro de IoT [estado de Azure][lnk-status].

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

2. Guardar archivo de plantilla de Azure Resource Manager hello en el equipo local. En este ejemplo, se da por supuesto que lo guarda en una carpeta llamada **c:\templates**.

3. Ejecute hello después comando toodeploy el nuevo centro de IoT, pasando el nombre de Hola de su centro de IoT como un parámetro. En este ejemplo, nombre de Hola de centro de IoT hello es `abcmyiothub`. nombre de Hola de su centro de IoT debe ser único globalmente:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. salida de Hello muestra las claves de hello para el centro de IoT de Hola que creó.

5. tooverify agregado la aplicación Hola nuevo centro de IoT, visite hello [portal de Azure] [ lnk-azure-portal] y ver la lista de recursos. O bien, usar hello **Get-AzureRmResource** cmdlet de PowerShell.

> [!NOTE]
> Esta aplicación de ejemplo agrega un centro de IoT estándar S1 por el que se le cobrará. Puede eliminar el centro de IoT de Hola a través de hello [portal de Azure] [ lnk-azure-portal] o mediante el uso de hello **Remove-AzureRmResource** cmdlet de PowerShell cuando haya terminado.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha implementado un centro de IoT usando una plantilla de administrador de recursos de Azure con PowerShell, puede que desee tooexplore adicional:

* Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].
* Lectura [Introducción al administrador de recursos de Azure] [ lnk-azure-rm-overview] toolearn más información acerca de las capacidades de hello del Administrador de recursos de Azure.

toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:

* [Introducción tooC SDK][lnk-c-sdk]
* [SDK de IoT de Azure][lnk-sdks]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con Azure IoT Edge][lnk-iotedge]

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
