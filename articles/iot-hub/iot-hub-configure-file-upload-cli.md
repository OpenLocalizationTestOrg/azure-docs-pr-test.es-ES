---
title: aaaConfigure archivo carga tooIoT concentrador mediante Azure CLI (az.py) | Documentos de Microsoft
description: "Cómo tooconfigure fileuploads tooAzure centro de IoT utilizando Hola multiplataforma Azure CLI 2.0 (az.py)."
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Configuración de cargas de archivos de IoT Hub mediante la CLI de Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Hola toouse [funcionalidad de carga de archivos en el centro de IoT][lnk-upload], primero debe asociar una cuenta de almacenamiento de Azure con el centro de IoT. Puede usar una cuenta de almacenamiento existente o crear una nueva.

toocomplete este tutorial, necesita Hola siguientes:

* Una cuenta de Azure activa. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* [CLI de Azure 2.0][lnk-CLI-install].
* Un centro de Azure IoT. Si no dispone de un centro de IoT, puede usar hello `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate uno o utilice Hola portal demasiado [crear un centro de IoT] [centro de portal lnk].
* Una cuenta de almacenamiento de Azure. Si no tienes una cuenta de almacenamiento de Azure, puede usar hello [2.0 de CLI de Azure: administrar cuentas de almacenamiento] [ lnk-manage-storage] toocreate uno o utilice Hola portal demasiado[crear una cuenta de almacenamiento] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Inicio de sesión y configuración de la cuenta de Azure

Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción.

1. En el símbolo de hello, ejecute hello [comando de inicio de sesión][lnk-login-command]:

    ```azurecli
    az login
    ```

    Siga Hola instrucciones tooauthenticate utilizando el código de hello e inicie sesión en tooyour cuenta de Azure a través de un explorador web.

1. Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall Hola asociadas con sus credenciales de cuentas de Azure. Utilice Hola siguiente [toolist comando Hola cuentas de Azure] [ lnk-az-account-command] disponibles para toouse:

    ```azurecli
    az account list
    ```

    Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT. Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Recuperación de los detalles de la cuenta de almacenamiento

Hello siguientes pasos se supone que creó su cuenta de almacenamiento con hello **el Administrador de recursos** modelo de implementación y no Hola **clásico** modelo de implementación.

archivo tooconfigure cargas de los dispositivos, deberá cadena de conexión de Hola para una cuenta de almacenamiento de Azure. cuenta de almacenamiento de Hello debe estar en hello misma suscripción que el centro de IoT. También necesita Hola nombre de un contenedor de blob en la cuenta de almacenamiento de Hola. Usar hello después comando tooretrieve las claves de cuenta de almacenamiento:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Tome nota de hello **connectionString** valor. Necesita Hola pasos.

Puede usar un contenedor de blobs existente para sus cargas de archivos o crear uno nuevo:

* contenedores blob toolist Hola existentes en la cuenta de almacenamiento, utilice Hola siguiente comando:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate un contenedor de blobs en la cuenta de almacenamiento, Hola de uso siguiente comando:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Carga de archivos

Ahora puede configurar su tooenable de centro de IoT [funcionalidad de carga de archivos] [ lnk-upload] con los detalles de la cuenta de almacenamiento.

configuración de Hello requiere Hola siguientes valores:

**Contenedor de almacenamiento**: un contenedor de blobs en una cuenta de almacenamiento de Azure con su tooassociate de suscripción de Azure actual con el centro de IoT. Recuperar información de cuenta de almacenamiento necesario Hola Hola sección anterior. Centro de IoT genera automáticamente el URI de SAS con el contenedor de blobs de toothis de permisos de escritura para dispositivos toouse cuando cargan archivos.

**Receive notifications for uploaded files** (Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos.

**SAS TTL**: esta opción es hello time-to-live de hello SAS URI devuelto toohello dispositivo por centro de IoT. Establece la hora de tooone predeterminada.

**Notificación de configuración de TTL predeterminado de archivos**: Hola tiempo de vida de una notificación de carga de archivo antes de que expire. Establezca tooone día de forma predeterminada.

**Número máximo de entregas de notificación de archivos**: número de Hola de tiempo de espera hello toodeliver de intentos de centro de IoT una notificación de carga de archivo. Establecer too10 de forma predeterminada.

Usar hello después la configuración de carga de archivo de hello tooconfigure de comandos de CLI de Azure en su centro de IoT:

En un uso de shell de Bash:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

En un uso de símbolo del sistema de Windows:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Puede revisar la configuración de carga de archivos de hello en el centro de IoT mediante el siguiente comando de hello:

```azurecli
az iot hub show --name {your iot hub name}
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

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create