---
title: Uso de Azure PowerShell para configurar la carga de archivos | Microsoft Docs
description: "Cómo usar los cmdlets de Azure PowerShell para configurar su centro de IoT para habilitar cargas de archivos desde dispositivos conectados. Incluye información sobre cómo configurar la cuenta de Azure Storage."
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="eeb97-104">Configuración de cargas de archivos de IoT Hub mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="eeb97-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="eeb97-105">Para usar la [funcionalidad de carga de archivos en IoT Hub][lnk-upload], primero debe asociar una cuenta de Azure Storage con su centro.</span><span class="sxs-lookup"><span data-stu-id="eeb97-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="eeb97-106">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="eeb97-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="eeb97-107">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eeb97-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="eeb97-108">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="eeb97-108">An active Azure account.</span></span> <span data-ttu-id="eeb97-109">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="eeb97-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="eeb97-110">[Cmdlets de Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="eeb97-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="eeb97-111">Un centro de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="eeb97-111">An Azure IoT hub.</span></span> <span data-ttu-id="eeb97-112">Si no dispone de un centro de IoT, puede usar el [cmdlet New-AzureRmIoTHub][lnk-powershell-iothub] para crear uno o usar el portal para [crear un centro de IoT][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="eeb97-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="eeb97-113">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb97-113">An Azure storage account.</span></span> <span data-ttu-id="eeb97-114">Si no tiene una cuenta de almacenamiento de Azure, puede usar los [cmdlets de PowerShell de Azure Storage] [lnk-powershell-storage] para crear una o usar el portal para [crear una cuenta de almacenamiento][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="eeb97-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="eeb97-115">Inicio de sesión y configuración de la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="eeb97-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="eeb97-116">Inicie sesión en su cuenta de Azure y seleccione la suscripción.</span><span class="sxs-lookup"><span data-stu-id="eeb97-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="eeb97-117">En el símbolo del sistema de PowerShell, ejecute el cmdlet **Login-AzureRmAccount**:</span><span class="sxs-lookup"><span data-stu-id="eeb97-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="eeb97-118">Si tiene varias suscripciones de Azure, el inicio de sesión en Azure le concede acceso a todas las suscripciones de Azure asociadas a sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="eeb97-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="eeb97-119">Use el siguiente comando para mostrar las suscripciones de Azure que están disponibles para su uso:</span><span class="sxs-lookup"><span data-stu-id="eeb97-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="eeb97-120">Use el siguiente comando para seleccionar la suscripción que desea usar para ejecutar los comandos para administrar su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="eeb97-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="eeb97-121">Puede usar el nombre de la suscripción o el identificador de la salida del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="eeb97-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="eeb97-122">Recuperación de los detalles de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="eeb97-122">Retrieve your storage account details</span></span>

<span data-ttu-id="eeb97-123">En los siguientes pasos se supone que ha creado la cuenta de almacenamiento mediante el modelo de implementación de **Resource Manager**, y no el modelo **clásico**.</span><span class="sxs-lookup"><span data-stu-id="eeb97-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="eeb97-124">Para configurar cargas de archivos desde sus dispositivos, necesitará la cadena de conexión de una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb97-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="eeb97-125">Esta cuenta debe encontrarse en la misma suscripción que IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="eeb97-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="eeb97-126">También necesitará el nombre de un contenedor de blobs de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eeb97-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="eeb97-127">Use el siguiente comando para recuperar las claves de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="eeb97-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="eeb97-128">Anote el valor de la clave de almacenamiento **key1**.</span><span class="sxs-lookup"><span data-stu-id="eeb97-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="eeb97-129">La necesitará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="eeb97-129">You need it in the following steps.</span></span>

<span data-ttu-id="eeb97-130">Puede usar un contenedor de blobs existente para sus cargas de archivos o crear uno nuevo:</span><span class="sxs-lookup"><span data-stu-id="eeb97-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="eeb97-131">Para mostrar los contenedores de blobs existentes en su cuenta de almacenamiento, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="eeb97-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="eeb97-132">Para crear un contenedor de blobs en su cuenta de almacenamiento, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="eeb97-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="eeb97-133">Configuración del centro de IoT</span><span class="sxs-lookup"><span data-stu-id="eeb97-133">Configure your IoT hub</span></span>

<span data-ttu-id="eeb97-134">Ahora puede configurar el centro de IoT para habilitar la [funcionalidad de carga de archivos] [lnk-upload] con los datos de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eeb97-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="eeb97-135">La configuración requiere los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="eeb97-135">The configuration requires the following values:</span></span>

<span data-ttu-id="eeb97-136">**Contenedor de almacenamiento:**: un contenedor de blobs en una cuenta de almacenamiento de Azure en la suscripción actual para asociar con su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="eeb97-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="eeb97-137">En la sección anterior, recuperó la información necesaria de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eeb97-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="eeb97-138">IoT Hub genera automáticamente identificadores URI de SAS con permisos de escritura en este contenedor de blobs para los dispositivos que se utilizarán cuando se carguen archivos.</span><span class="sxs-lookup"><span data-stu-id="eeb97-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="eeb97-139">**Receive notifications for uploaded files** (Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="eeb97-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="eeb97-140">**SAS TTL**(TTL SAS): este valor es el periodo de vida de los URI de SAS que IoT Hub devuelve al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eeb97-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="eeb97-141">De forma predeterminada, está establecido en una hora.</span><span class="sxs-lookup"><span data-stu-id="eeb97-141">Set to one hour by default.</span></span>

<span data-ttu-id="eeb97-142">**File notification settings default TTL**(TTL predeterminado de configuración de notificación de archivos): el periodo de vida de una notificación de carga de archivos antes de que caduque.</span><span class="sxs-lookup"><span data-stu-id="eeb97-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="eeb97-143">De forma predeterminada, está establecido en un día.</span><span class="sxs-lookup"><span data-stu-id="eeb97-143">Set to one day by default.</span></span>

<span data-ttu-id="eeb97-144">**File notification maximum delivery count**(Número máximo de entregas de notificaciones de archivo): el número de veces que IoT Hub tratará de entregar una notificación de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="eeb97-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="eeb97-145">De forma predeterminada, está establecido en 10.</span><span class="sxs-lookup"><span data-stu-id="eeb97-145">Set to 10 by default.</span></span>

<span data-ttu-id="eeb97-146">Use el siguiente cmdlet de PowerShell para configurar la carga de archivos en su centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="eeb97-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="eeb97-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eeb97-147">Next steps</span></span>

<span data-ttu-id="eeb97-148">Para más información sobre las funcionalidades de carga de archivos de IoT Hub, consulte [Carga de archivos desde un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="eeb97-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="eeb97-149">Siga estos vínculos para más información sobre la administración de Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="eeb97-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="eeb97-150">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="eeb97-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="eeb97-151">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="eeb97-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="eeb97-152">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="eeb97-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="eeb97-153">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="eeb97-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="eeb97-154">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="eeb97-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="eeb97-155">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="eeb97-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="eeb97-156">[Protección total de la solución de IoT][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="eeb97-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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