---
title: cargar el archivo aaaUse hello Azure PowerShell tooconfigure | Documentos de Microsoft
description: "Cómo toouse hello Azure PowerShell cmdlets tooconfigure el IoT hub tooenable cargas de archivos desde dispositivos conectados. Incluye información acerca de cómo configurar la cuenta de almacenamiento de Azure de destino de Hola."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Configuración de cargas de archivos de IoT Hub mediante PowerShell

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Hola toouse [funcionalidad de carga de archivos en el centro de IoT][lnk-upload], primero debe asociar una cuenta de almacenamiento de Azure con el centro de IoT. Puede usar una cuenta de almacenamiento existente o crear una nueva.

toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [Cmdlets de Azure PowerShell][lnk-powershell-install].
* Un centro de Azure IoT. Si no dispone de un centro de IoT, puede usar hello [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate uno o utilice Hola portal demasiado[crear un centro de IoT] [ lnk-portal-hub].
* Una cuenta de almacenamiento de Azure. Si no tiene una cuenta de almacenamiento de Azure, puede usar hello [cmdlets de PowerShell de almacenamiento de Azure] [ lnk-powershell-storage] toocreate uno o utilice Hola portal demasiado[crear una cuenta de almacenamiento] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Inicio de sesión y configuración de la cuenta de Azure

Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción.

1. En el símbolo del sistema de PowerShell hello, ejecute hello **AzureRmAccount de inicio de sesión** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales. Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:

    ```powershell
    Get-AzureRMSubscription
    ```

    Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toomanage su centro de IoT. Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Recuperación de los detalles de la cuenta de almacenamiento

Hello siguientes pasos se supone que creó su cuenta de almacenamiento con hello **el Administrador de recursos** modelo de implementación y no Hola **clásico** modelo de implementación.

archivo tooconfigure cargas de los dispositivos, deberá cadena de conexión de Hola para una cuenta de almacenamiento de Azure. cuenta de almacenamiento de Hello debe estar en hello misma suscripción que el centro de IoT. También necesita Hola nombre de un contenedor de blob en la cuenta de almacenamiento de Hola. Usar hello después comando tooretrieve las claves de cuenta de almacenamiento:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Tome nota de hello **key1** valor de clave de cuenta de almacenamiento. Necesita Hola pasos.

Puede usar un contenedor de blobs existente para sus cargas de archivos o crear uno nuevo:

* contenedores blob toolist Hola existentes en la cuenta de almacenamiento, utilice Hola siguientes comandos:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate un contenedor de blobs en la cuenta de almacenamiento, Hola de uso siguientes comandos:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Configuración del centro de IoT

Ahora puede configurar su tooenable de centro de IoT [funcionalidad de carga de archivos] [ lnk-upload] con los detalles de la cuenta de almacenamiento.

configuración de Hello requiere Hola siguientes valores:

**Contenedor de almacenamiento**: un contenedor de blobs en una cuenta de almacenamiento de Azure con su tooassociate de suscripción de Azure actual con el centro de IoT. Recuperar información de cuenta de almacenamiento necesario Hola Hola sección anterior. Centro de IoT genera automáticamente el URI de SAS con el contenedor de blobs de toothis de permisos de escritura para dispositivos toouse cuando cargan archivos.

**Receive notifications for uploaded files** (Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos.

**SAS TTL**: esta opción es hello time-to-live de hello SAS URI devuelto toohello dispositivo por centro de IoT. Establece la hora de tooone predeterminada.

**Notificación de configuración de TTL predeterminado de archivos**: Hola tiempo de vida de una notificación de carga de archivo antes de que expire. Establezca tooone día de forma predeterminada.

**Número máximo de entregas de notificación de archivos**: número de Hola de tiempo de espera hello toodeliver de intentos de centro de IoT una notificación de carga de archivo. Establecer too10 de forma predeterminada.

Usar hello después la configuración de carga de archivo de hello tooconfigure de cmdlet de PowerShell en el centro de IoT:

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las capacidades de carga de archivo Hola de centro de IoT, consulte [cargar archivos desde un dispositivo][lnk-upload].

Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:

* [Administración masiva de dispositivos de IoT][lnk-bulk]
* [Métricas de IoT Hub][lnk-metrics]
* [Supervisión de operaciones][lnk-monitor]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con IoT Edge][lnk-iotedge]
* [Proteger la solución de IoT de hello masa][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md