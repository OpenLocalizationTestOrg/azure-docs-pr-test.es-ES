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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="a33d5-103">Configuración de cargas de archivos de IoT Hub mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a33d5-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="a33d5-104">Hola toouse [funcionalidad de carga de archivos en el centro de IoT][lnk-upload], primero debe asociar una cuenta de almacenamiento de Azure con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a33d5-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="a33d5-105">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="a33d5-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="a33d5-106">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a33d5-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a33d5-107">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="a33d5-107">An active Azure account.</span></span> <span data-ttu-id="a33d5-108">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a33d5-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="a33d5-109">[CLI de Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="a33d5-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="a33d5-110">Un centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="a33d5-110">An Azure IoT hub.</span></span> <span data-ttu-id="a33d5-111">Si no dispone de un centro de IoT, puede usar hello `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate uno o utilice Hola portal demasiado [crear un centro de IoT] [centro de portal lnk].</span><span class="sxs-lookup"><span data-stu-id="a33d5-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="a33d5-112">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a33d5-112">An Azure Storage account.</span></span> <span data-ttu-id="a33d5-113">Si no tienes una cuenta de almacenamiento de Azure, puede usar hello [2.0 de CLI de Azure: administrar cuentas de almacenamiento] [ lnk-manage-storage] toocreate uno o utilice Hola portal demasiado[crear una cuenta de almacenamiento] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="a33d5-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="a33d5-114">Inicio de sesión y configuración de la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="a33d5-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="a33d5-115">Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="a33d5-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="a33d5-116">En el símbolo de hello, ejecute hello [comando de inicio de sesión][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="a33d5-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="a33d5-117">Siga Hola instrucciones tooauthenticate utilizando el código de hello e inicie sesión en tooyour cuenta de Azure a través de un explorador web.</span><span class="sxs-lookup"><span data-stu-id="a33d5-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="a33d5-118">Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall Hola asociadas con sus credenciales de cuentas de Azure.</span><span class="sxs-lookup"><span data-stu-id="a33d5-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="a33d5-119">Utilice Hola siguiente [toolist comando Hola cuentas de Azure] [ lnk-az-account-command] disponibles para toouse:</span><span class="sxs-lookup"><span data-stu-id="a33d5-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="a33d5-120">Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toocreate su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a33d5-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="a33d5-121">Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="a33d5-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="a33d5-122">Recuperación de los detalles de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a33d5-122">Retrieve your storage account details</span></span>

<span data-ttu-id="a33d5-123">Hello siguientes pasos se supone que creó su cuenta de almacenamiento con hello **el Administrador de recursos** modelo de implementación y no Hola **clásico** modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="a33d5-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="a33d5-124">archivo tooconfigure cargas de los dispositivos, deberá cadena de conexión de Hola para una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a33d5-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="a33d5-125">cuenta de almacenamiento de Hello debe estar en hello misma suscripción que el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a33d5-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="a33d5-126">También necesita Hola nombre de un contenedor de blob en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a33d5-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="a33d5-127">Usar hello después comando tooretrieve las claves de cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a33d5-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="a33d5-128">Tome nota de hello **connectionString** valor.</span><span class="sxs-lookup"><span data-stu-id="a33d5-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="a33d5-129">Necesita Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="a33d5-129">You need it in hello following steps.</span></span>

<span data-ttu-id="a33d5-130">Puede usar un contenedor de blobs existente para sus cargas de archivos o crear uno nuevo:</span><span class="sxs-lookup"><span data-stu-id="a33d5-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="a33d5-131">contenedores blob toolist Hola existentes en la cuenta de almacenamiento, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a33d5-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="a33d5-132">toocreate un contenedor de blobs en la cuenta de almacenamiento, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a33d5-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="a33d5-133">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="a33d5-133">File upload</span></span>

<span data-ttu-id="a33d5-134">Ahora puede configurar su tooenable de centro de IoT [funcionalidad de carga de archivos] [ lnk-upload] con los detalles de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a33d5-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="a33d5-135">configuración de Hello requiere Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="a33d5-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="a33d5-136">**Contenedor de almacenamiento**: un contenedor de blobs en una cuenta de almacenamiento de Azure con su tooassociate de suscripción de Azure actual con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a33d5-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="a33d5-137">Recuperar información de cuenta de almacenamiento necesario Hola Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="a33d5-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="a33d5-138">Centro de IoT genera automáticamente el URI de SAS con el contenedor de blobs de toothis de permisos de escritura para dispositivos toouse cuando cargan archivos.</span><span class="sxs-lookup"><span data-stu-id="a33d5-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="a33d5-139">**Receive notifications for uploaded files** (Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="a33d5-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="a33d5-140">**SAS TTL**: esta opción es hello time-to-live de hello SAS URI devuelto toohello dispositivo por centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="a33d5-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="a33d5-141">Establece la hora de tooone predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a33d5-141">Set tooone hour by default.</span></span>

<span data-ttu-id="a33d5-142">**Notificación de configuración de TTL predeterminado de archivos**: Hola tiempo de vida de una notificación de carga de archivo antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="a33d5-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="a33d5-143">Establezca tooone día de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a33d5-143">Set tooone day by default.</span></span>

<span data-ttu-id="a33d5-144">**Número máximo de entregas de notificación de archivos**: número de Hola de tiempo de espera hello toodeliver de intentos de centro de IoT una notificación de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="a33d5-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="a33d5-145">Establecer too10 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a33d5-145">Set too10 by default.</span></span>

<span data-ttu-id="a33d5-146">Usar hello después la configuración de carga de archivo de hello tooconfigure de comandos de CLI de Azure en su centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="a33d5-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="a33d5-147">En un uso de shell de Bash:</span><span class="sxs-lookup"><span data-stu-id="a33d5-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="a33d5-148">En un uso de símbolo del sistema de Windows:</span><span class="sxs-lookup"><span data-stu-id="a33d5-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="a33d5-149">Puede revisar la configuración de carga de archivos de hello en el centro de IoT mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a33d5-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="a33d5-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a33d5-150">Next steps</span></span>

<span data-ttu-id="a33d5-151">Para obtener más información acerca de las capacidades de carga de archivo Hola de centro de IoT, consulte [cargar archivos desde un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="a33d5-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="a33d5-152">Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="a33d5-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="a33d5-153">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="a33d5-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="a33d5-154">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="a33d5-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="a33d5-155">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="a33d5-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="a33d5-156">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="a33d5-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a33d5-157">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a33d5-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a33d5-158">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a33d5-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="a33d5-159">[Proteger la solución de IoT de hello masa][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="a33d5-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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