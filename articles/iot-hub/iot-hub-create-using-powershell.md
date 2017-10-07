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
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Crear un centro de IoT mediante el cmdlet New-AzureRmIotHub Hola

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introducción

Puede usar toocreate de cmdlets de PowerShell de Azure y administre centros de IoT de Azure. Este tutorial muestra cómo toocreate un centro de IoT con PowerShell.

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello Azure Resource Manager.

toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. <br/>Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [Cmdlets de Azure PowerShell][lnk-powershell-install].

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

## <a name="create-resource-group"></a>Creación de un grupo de recursos

Es necesario un toodeploy de grupo de recursos un centro de IoT. Puede usar un grupo de recursos existente o crear uno nuevo.

Puede usar hello en el que puede implementar un centro de IoT de comando toodiscover Hola ubicaciones siguientes:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate un grupo de recursos para el centro de IoT de hello admite ubicaciones de centro de IoT, Hola de uso siguiente comando. Este ejemplo crea un grupo de recursos denominado **MyIoTRG1** en hello **UU** región:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Crear un centro de IoT

toocreate un centro de IoT en grupo de recursos de Hola que creó en el paso anterior hello, Hola de uso siguiente comando. Este ejemplo se crea un **S1** concentrador llama **MyTestIoTHub** en hello **UU** región:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

nombre de Hola de centro de IoT Hola debe ser único.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


Puede enumerar todos los centros de IoT de hello en su suscripción mediante Hola siguiente comando:

```powershell
Get-AzureRmIotHub
```

ejemplo de Hola anterior agrega un centro de IoT S1 estándar para la que se facturan. Puede eliminar el centro de IoT de hello mediante Hola siguiente comando:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

Como alternativa, puede quitar un grupo de recursos y todos los recursos que contiene utilizando el siguiente comando de Hola de Hola:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha implementado un centro de IoT mediante un cmdlet de PowerShell, puede que desee tooexplore adicional:

* Descubra otros [cmdlets de PowerShell para trabajar con la instancia de IoT Hub][lnk-iothub-cmdlets].
* Obtenga información sobre las capacidades de Hola de hello [API de REST de proveedor de recursos de centro de IoT][lnk-rest-api].

toolearn más sobre el desarrollo de centro de IoT, vea Hola siguientes artículos:

* [Introducción tooC SDK][lnk-c-sdk]
* [SDK de IoT de Azure][lnk-sdks]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Simular un dispositivo con IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
