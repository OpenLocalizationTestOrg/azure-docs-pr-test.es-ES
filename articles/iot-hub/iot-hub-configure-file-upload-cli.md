---
title: "Configuración de carga de archivos a IoT Hub con CLI de Azure (az.py) | Documentos de Microsoft"
description: "Configuración de cargas de archivos a Azure IoT Hub mediante la CLI de Azure 2.0 (az.py) multiplataforma."
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
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="d2a7a-103">Configuración de cargas de archivos de IoT Hub mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d2a7a-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="d2a7a-104">Para usar la [funcionalidad de carga de archivos en IoT Hub][lnk-upload], primero debe asociar una cuenta de Azure Storage con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="d2a7a-105">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="d2a7a-106">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d2a7a-107">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-107">An active Azure account.</span></span> <span data-ttu-id="d2a7a-108">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d2a7a-109">[CLI de Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="d2a7a-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="d2a7a-110">Un centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-110">An Azure IoT hub.</span></span> <span data-ttu-id="d2a7a-111">Si no tiene ningún IoT Hub, puede usar el [comando][lnk-cli-create-iothub] `az iot hub create` para crear uno o usar el portal para [Crear un IoT Hub][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="d2a7a-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="d2a7a-112">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-112">An Azure Storage account.</span></span> <span data-ttu-id="d2a7a-113">Si no tiene ninguna cuenta de almacenamiento de Azure, puede usar la [CLI de Azure 2.0: Administrar cuentas de almacenamiento][lnk-manage-storage] para crear una o usar el portal para [Crear una cuenta de almacenamiento][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="d2a7a-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="d2a7a-114">Inicio de sesión y configuración de la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="d2a7a-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="d2a7a-115">Inicie sesión en la cuenta de Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="d2a7a-116">En el símbolo del sistema, ejecute el [comando de inicio de sesión][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="d2a7a-117">Siga las instrucciones para realizar la autenticación mediante el código e inicie sesión en la cuenta de Azure a través de un explorador web.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="d2a7a-118">Si tiene varias suscripciones de Azure, iniciar sesión en Azure le concede acceso a todas las cuentas de Azure asociadas con las credenciales.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="d2a7a-119">Use el siguiente [comando para mostrar las cuentas de Azure][lnk-az-account-command] que tiene disponibles para su uso:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="d2a7a-120">Use el siguiente comando para seleccionar la suscripción que desea usar para ejecutar los comandos que crearán la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="d2a7a-121">Puede usar el nombre de la suscripción o el identificador de la salida del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="d2a7a-122">Recuperación de los detalles de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="d2a7a-122">Retrieve your storage account details</span></span>

<span data-ttu-id="d2a7a-123">En los siguientes pasos se supone que ha creado la cuenta de almacenamiento mediante el modelo de implementación de **Resource Manager**, y no el modelo **clásico**.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="d2a7a-124">Para configurar cargas de archivos desde sus dispositivos, necesitará la cadena de conexión de una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="d2a7a-125">Esta cuenta debe encontrarse en la misma suscripción que IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="d2a7a-126">También necesitará el nombre de un contenedor de blobs de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="d2a7a-127">Use el siguiente comando para recuperar las claves de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="d2a7a-128">Anote el valor de **connectionString**.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="d2a7a-129">La necesitará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-129">You need it in the following steps.</span></span>

<span data-ttu-id="d2a7a-130">Puede usar un contenedor de blobs existente para sus cargas de archivos o crear uno nuevo:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="d2a7a-131">Para mostrar los contenedores de blobs existentes en su cuenta de almacenamiento, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="d2a7a-132">Para crear un contenedor de blobs en su cuenta de almacenamiento, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="d2a7a-133">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="d2a7a-133">File upload</span></span>

<span data-ttu-id="d2a7a-134">Ahora puede configurar el centro de IoT para habilitar la [funcionalidad de carga de archivos] [lnk-upload] con los datos de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="d2a7a-135">La configuración requiere los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-135">The configuration requires the following values:</span></span>

<span data-ttu-id="d2a7a-136">**Contenedor de almacenamiento:**: un contenedor de blobs en una cuenta de almacenamiento de Azure en la suscripción actual para asociar con su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="d2a7a-137">En la sección anterior, recuperó la información necesaria de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="d2a7a-138">IoT Hub genera automáticamente identificadores URI de SAS con permisos de escritura en este contenedor de blobs para los dispositivos que se utilizarán cuando se carguen archivos.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="d2a7a-139">**Receive notifications for uploaded files** (Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="d2a7a-140">**SAS TTL**(TTL SAS): este valor es el periodo de vida de los URI de SAS que IoT Hub devuelve al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="d2a7a-141">De forma predeterminada, está establecido en una hora.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-141">Set to one hour by default.</span></span>

<span data-ttu-id="d2a7a-142">**File notification settings default TTL**(TTL predeterminado de configuración de notificación de archivos): el periodo de vida de una notificación de carga de archivos antes de que caduque.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="d2a7a-143">De forma predeterminada, está establecido en un día.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-143">Set to one day by default.</span></span>

<span data-ttu-id="d2a7a-144">**File notification maximum delivery count**(Número máximo de entregas de notificaciones de archivo): el número de veces que IoT Hub tratará de entregar una notificación de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="d2a7a-145">De forma predeterminada, está establecido en 10.</span><span class="sxs-lookup"><span data-stu-id="d2a7a-145">Set to 10 by default.</span></span>

<span data-ttu-id="d2a7a-146">Use los siguientes comandos del CLI de Azure para configurar la carga de archivos en IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="d2a7a-147">En un uso de shell de Bash:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="d2a7a-148">En un uso de símbolo del sistema de Windows:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="d2a7a-149">Puede revisar la configuración de carga de archivos en IoT Hub con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="d2a7a-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2a7a-150">Next steps</span></span>

<span data-ttu-id="d2a7a-151">Para más información sobre las funcionalidades de carga de archivos de IoT Hub, consulte [Carga de archivos desde un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="d2a7a-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="d2a7a-152">Siga estos vínculos para más información sobre la administración de Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="d2a7a-153">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="d2a7a-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="d2a7a-154">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="d2a7a-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="d2a7a-155">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="d2a7a-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="d2a7a-156">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="d2a7a-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d2a7a-157">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d2a7a-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d2a7a-158">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d2a7a-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="d2a7a-159">[Protección total de la solución de IoT][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="d2a7a-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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