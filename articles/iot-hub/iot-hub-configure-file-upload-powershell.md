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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="02ff0-104">Configuración de cargas de archivos de IoT Hub mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="02ff0-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="02ff0-105">Hola toouse [funcionalidad de carga de archivos en el centro de IoT][lnk-upload], primero debe asociar una cuenta de almacenamiento de Azure con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="02ff0-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="02ff0-106">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="02ff0-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="02ff0-107">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="02ff0-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="02ff0-108">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="02ff0-108">An active Azure account.</span></span> <span data-ttu-id="02ff0-109">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="02ff0-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="02ff0-110">[Cmdlets de Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="02ff0-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="02ff0-111">Un centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="02ff0-111">An Azure IoT hub.</span></span> <span data-ttu-id="02ff0-112">Si no dispone de un centro de IoT, puede usar hello [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate uno o utilice Hola portal demasiado[crear un centro de IoT] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="02ff0-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="02ff0-113">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="02ff0-113">An Azure storage account.</span></span> <span data-ttu-id="02ff0-114">Si no tiene una cuenta de almacenamiento de Azure, puede usar hello [cmdlets de PowerShell de almacenamiento de Azure] [ lnk-powershell-storage] toocreate uno o utilice Hola portal demasiado[crear una cuenta de almacenamiento] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="02ff0-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="02ff0-115">Inicio de sesión y configuración de la cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="02ff0-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="02ff0-116">Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="02ff0-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="02ff0-117">En el símbolo del sistema de PowerShell hello, ejecute hello **AzureRmAccount de inicio de sesión** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="02ff0-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="02ff0-118">Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="02ff0-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="02ff0-119">Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:</span><span class="sxs-lookup"><span data-stu-id="02ff0-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="02ff0-120">Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toomanage su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="02ff0-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="02ff0-121">Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="02ff0-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="02ff0-122">Recuperación de los detalles de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="02ff0-122">Retrieve your storage account details</span></span>

<span data-ttu-id="02ff0-123">Hello siguientes pasos se supone que creó su cuenta de almacenamiento con hello **el Administrador de recursos** modelo de implementación y no Hola **clásico** modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="02ff0-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="02ff0-124">archivo tooconfigure cargas de los dispositivos, deberá cadena de conexión de Hola para una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="02ff0-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="02ff0-125">cuenta de almacenamiento de Hello debe estar en hello misma suscripción que el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="02ff0-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="02ff0-126">También necesita Hola nombre de un contenedor de blob en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="02ff0-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="02ff0-127">Usar hello después comando tooretrieve las claves de cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="02ff0-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="02ff0-128">Tome nota de hello **key1** valor de clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="02ff0-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="02ff0-129">Necesita Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="02ff0-129">You need it in hello following steps.</span></span>

<span data-ttu-id="02ff0-130">Puede usar un contenedor de blobs existente para sus cargas de archivos o crear uno nuevo:</span><span class="sxs-lookup"><span data-stu-id="02ff0-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="02ff0-131">contenedores blob toolist Hola existentes en la cuenta de almacenamiento, utilice Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="02ff0-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="02ff0-132">toocreate un contenedor de blobs en la cuenta de almacenamiento, Hola de uso siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="02ff0-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="02ff0-133">Configuración del centro de IoT</span><span class="sxs-lookup"><span data-stu-id="02ff0-133">Configure your IoT hub</span></span>

<span data-ttu-id="02ff0-134">Ahora puede configurar su tooenable de centro de IoT [funcionalidad de carga de archivos] [ lnk-upload] con los detalles de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="02ff0-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="02ff0-135">configuración de Hello requiere Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="02ff0-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="02ff0-136">**Contenedor de almacenamiento**: un contenedor de blobs en una cuenta de almacenamiento de Azure con su tooassociate de suscripción de Azure actual con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="02ff0-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="02ff0-137">Recuperar información de cuenta de almacenamiento necesario Hola Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="02ff0-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="02ff0-138">Centro de IoT genera automáticamente el URI de SAS con el contenedor de blobs de toothis de permisos de escritura para dispositivos toouse cuando cargan archivos.</span><span class="sxs-lookup"><span data-stu-id="02ff0-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="02ff0-139">**Receive notifications for uploaded files** (Recibir notificaciones para archivos cargados): habilite o deshabilite las notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="02ff0-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="02ff0-140">**SAS TTL**: esta opción es hello time-to-live de hello SAS URI devuelto toohello dispositivo por centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="02ff0-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="02ff0-141">Establece la hora de tooone predeterminada.</span><span class="sxs-lookup"><span data-stu-id="02ff0-141">Set tooone hour by default.</span></span>

<span data-ttu-id="02ff0-142">**Notificación de configuración de TTL predeterminado de archivos**: Hola tiempo de vida de una notificación de carga de archivo antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="02ff0-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="02ff0-143">Establezca tooone día de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="02ff0-143">Set tooone day by default.</span></span>

<span data-ttu-id="02ff0-144">**Número máximo de entregas de notificación de archivos**: número de Hola de tiempo de espera hello toodeliver de intentos de centro de IoT una notificación de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="02ff0-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="02ff0-145">Establecer too10 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="02ff0-145">Set too10 by default.</span></span>

<span data-ttu-id="02ff0-146">Usar hello después la configuración de carga de archivo de hello tooconfigure de cmdlet de PowerShell en el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="02ff0-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="02ff0-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="02ff0-147">Next steps</span></span>

<span data-ttu-id="02ff0-148">Para obtener más información acerca de las capacidades de carga de archivo Hola de centro de IoT, consulte [cargar archivos desde un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="02ff0-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="02ff0-149">Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="02ff0-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="02ff0-150">[Administración masiva de dispositivos de IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="02ff0-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="02ff0-151">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="02ff0-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="02ff0-152">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="02ff0-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="02ff0-153">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="02ff0-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="02ff0-154">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="02ff0-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="02ff0-155">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="02ff0-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="02ff0-156">[Proteger la solución de IoT de hello masa][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="02ff0-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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