---
title: "Información sobre la carga de archivos de Azure IoT Hub | Microsoft Docs"
description: "Guía del desarrollador: uso de la característica de carga de archivos de IoT Hub para administrar la carga de archivos desde un dispositivo a un contenedor de blobs de Azure Storage."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="3c1d1-103">Carga de archivos con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3c1d1-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="3c1d1-104">Tal como se detalla en el artículo [Puntos de conexión de IoT Hub][lnk-endpoints], un dispositivo puede iniciar cargas de archivos mediante el envío de una notificación a través de un punto de conexión accesible desde el dispositivo (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="3c1d1-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="3c1d1-105">Cuando un dispositivo notifica a IoT Hub que se ha completado una carga, este envía un mensaje de notificación de carga a través del punto de conexión accesible desde el servicio (**/messages/servicebound/filenotifications**).</span><span class="sxs-lookup"><span data-stu-id="3c1d1-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="3c1d1-106">En lugar de servir de intermediario de los mensajes, IoT Hub actúa como distribuidor a una cuenta de Azure Storage asociada.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="3c1d1-107">Un dispositivo solicita un token de almacenamiento de IoT Hub que es específico del archivo que el dispositivo quiere cargar.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="3c1d1-108">El dispositivo usa el URI de SAS para cargar el archivo en el almacenamiento y, cuando la carga ha finalizado, envía una notificación de finalización a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="3c1d1-109">IoT Hub comprueba que la carga del archivo está completa y agrega después un mensaje de notificación de carga de archivo al nuevo punto de conexión de notificaciones de archivos accesible desde el servicio.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="3c1d1-110">Antes de cargar un archivo en IoT Hub desde un dispositivo, tiene que configurar su centro mediante la [asociación de una cuenta de Azure Storage][lnk-associate-storage] al mismo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="3c1d1-111">El dispositivo puede entonces [inicializar una carga][lnk-initialize] y, a continuación, [notificar a IoT Hub][lnk-notify] cuando se complete la carga.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="3c1d1-112">Opcionalmente, cuando un dispositivo notifica a IoT Hub que la carga está completa, el servicio puede generar un [mensaje de notificación][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="3c1d1-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="3c1d1-113">Cuándo se deben usar</span><span class="sxs-lookup"><span data-stu-id="3c1d1-113">When to use</span></span>

<span data-ttu-id="3c1d1-114">Cargas de archivos, para archivos multimedia y grandes lotes de telemetría cargados por dispositivos conectados de manera intermitente o comprimidos para ahorrar ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="3c1d1-115">Si duda entre el uso de propiedades notificadas, mensajes de dispositivo a nube o carga de archivos, consulte [Device-to-cloud communication guidance][lnk-d2c-guidance] (Guía de comunicación de dispositivo a nube).</span><span class="sxs-lookup"><span data-stu-id="3c1d1-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="3c1d1-116">Asociar una cuenta de Azure Storage con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3c1d1-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="3c1d1-117">Para utilizar la funcionalidad de carga de archivos, primero debe vincular una cuenta de Azure Storage a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="3c1d1-118">Puede completar esta tarea a través de [Azure Portal][lnk-management-portal] o mediante programación, con las [API de REST del proveedor de recursos de IoT Hub][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="3c1d1-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="3c1d1-119">Una vez que ha asociado una cuenta de Azure Storage a IoT Hub, el servicio devuelve un URI de SAS a un dispositivo cuando este inicie una solicitud de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1d1-120">Los [SDK de IoT de Azure][lnk-sdks] administran automáticamente la recuperación del URI de SAS: cargan el archivo y notifican a IoT Hub que la carga se ha completado.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="3c1d1-121">Inicialización de una carga de archivos</span><span class="sxs-lookup"><span data-stu-id="3c1d1-121">Initialize a file upload</span></span>
<span data-ttu-id="3c1d1-122">IoT Hub tiene un punto de conexión concreto para dispositivos para solicitar un URI de SAS para el almacenamiento para cargar un archivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="3c1d1-123">Para iniciar el proceso de carga de archivos, el dispositivo envía una solicitud POST a `{iot hub}.azure-devices.net/devices/{deviceId}/files` con el cuerpo JSON siguiente:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="3c1d1-124">IoT Hub devuelve los datos siguientes, que usa el dispositivo para cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="3c1d1-125">En desuso: inicializar una carga de archivo con un comando GET</span><span class="sxs-lookup"><span data-stu-id="3c1d1-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="3c1d1-126">Esta sección describe la funcionalidad en desuso para la recepción de un URI de SAS de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="3c1d1-127">Use el método POST que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-127">Use the POST method described previously.</span></span>

<span data-ttu-id="3c1d1-128">IoT Hub tiene dos puntos de conexión de REST que permiten la carga de archivos: uno para obtener el URI de SAS para el almacenamiento y el otro para notificar al centro de IoT que la carga se ha completado.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="3c1d1-129">El dispositivo inicia el proceso de carga de archivos mediante el envío de una operación GET al centro de IoT en `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="3c1d1-130">IoT Hub devuelve:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-130">The IoT hub returns:</span></span>

* <span data-ttu-id="3c1d1-131">Un URI de SAS específico del archivo que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="3c1d1-132">Un identificador de correlación que se usará cuando se haya completado la carga.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="3c1d1-133">Notificación a IoT Hub de una carga de archivos completada</span><span class="sxs-lookup"><span data-stu-id="3c1d1-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="3c1d1-134">El dispositivo es responsable de cargar el archivo en el almacenamiento mediante los SDK de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="3c1d1-135">Cuando la carga se haya completado, el dispositivo envía una solicitud POST a `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` con el siguiente cuerpo JSON:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="3c1d1-136">El valor de `isSuccess` es un valor booleano que indica si se cargó correctamente el archivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="3c1d1-137">El código de estado para `statusCode` es el estado de la carga del archivo al almacenamiento y `statusDescription` corresponde a `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="3c1d1-138">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-138">Reference topics:</span></span>

<span data-ttu-id="3c1d1-139">Los siguientes temas de referencia proporcionan más información sobre la carga de archivos desde un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="3c1d1-140">Notificaciones de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="3c1d1-140">File upload notifications</span></span>

<span data-ttu-id="3c1d1-141">Opcionalmente, cuando el dispositivo notifica a IoT Hub que la carga ha finalizado, el servicio puede generar un mensaje de notificación que contiene el nombre y la ubicación de almacenamiento del archivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="3c1d1-142">Como se ha explicado en [Puntos de conexión][lnk-endpoints], IoT Hub entrega notificaciones de carga de archivos a través de un punto de conexión accesible desde el servicio (**/messages/servicebound/fileuploadnotifications**) en forma de mensajes.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="3c1d1-143">La semántica de recepción de las notificaciones de carga de archivos es la misma que para los mensajes de nube a dispositivo y tiene el mismo [ciclo de vida del mensaje][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="3c1d1-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="3c1d1-144">Cada mensaje recuperado del punto de conexión de notificación de carga de archivos es un registro JSON con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="3c1d1-145">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3c1d1-145">Property</span></span> | <span data-ttu-id="3c1d1-146">Description</span><span class="sxs-lookup"><span data-stu-id="3c1d1-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c1d1-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="3c1d1-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="3c1d1-148">Marca de tiempo que indica cuándo se creó la notificación.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="3c1d1-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="3c1d1-149">DeviceId</span></span> |<span data-ttu-id="3c1d1-150">**DeviceId** del dispositivo que ha cargado el archivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="3c1d1-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="3c1d1-151">BlobUri</span></span> |<span data-ttu-id="3c1d1-152">URI del archivo cargado.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="3c1d1-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="3c1d1-153">BlobName</span></span> |<span data-ttu-id="3c1d1-154">Nombre del archivo cargado.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="3c1d1-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="3c1d1-155">LastUpdatedTime</span></span> |<span data-ttu-id="3c1d1-156">Marca de tiempo que indica cuándo se actualizó por última vez el archivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="3c1d1-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="3c1d1-157">BlobSizeInBytes</span></span> |<span data-ttu-id="3c1d1-158">Tamaño del archivo cargado.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="3c1d1-159">**Ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-159">**Example**.</span></span> <span data-ttu-id="3c1d1-160">Este ejemplo muestra el cuerpo de ejemplo de un mensaje de notificación de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-160">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="3c1d1-161">Opciones de configuración de notificaciones de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="3c1d1-161">File upload notification configuration options</span></span>

<span data-ttu-id="3c1d1-162">Cada centro de IoT expone las siguientes opciones de configuración para las notificaciones de carga de archivos:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="3c1d1-163">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3c1d1-163">Property</span></span> | <span data-ttu-id="3c1d1-164">Description</span><span class="sxs-lookup"><span data-stu-id="3c1d1-164">Description</span></span> | <span data-ttu-id="3c1d1-165">Intervalo y valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3c1d1-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c1d1-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="3c1d1-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="3c1d1-167">Controla si las notificaciones de carga de archivos se escriben en el punto de conexión de notificaciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="3c1d1-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-168">Bool.</span></span> <span data-ttu-id="3c1d1-169">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-169">Default: True.</span></span> |
| <span data-ttu-id="3c1d1-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="3c1d1-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="3c1d1-171">TTL predeterminado para las notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="3c1d1-172">Intervalo ISO_8601 hasta 48H (1 minuto como mínimo).</span><span class="sxs-lookup"><span data-stu-id="3c1d1-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="3c1d1-173">Valor predeterminado: 1 hora.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="3c1d1-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="3c1d1-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="3c1d1-175">Duración del bloqueo de la cola de notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="3c1d1-176">De 5 a 300 segundos (5 segundos como mínimo).</span><span class="sxs-lookup"><span data-stu-id="3c1d1-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="3c1d1-177">Valor predeterminado: 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="3c1d1-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="3c1d1-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="3c1d1-179">Número máximo de entregas en la cola de notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="3c1d1-180">De 1 a 100.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-180">1 to 100.</span></span> <span data-ttu-id="3c1d1-181">Valor predeterminado: 100.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="3c1d1-182">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="3c1d1-182">Additional reference material</span></span>

<span data-ttu-id="3c1d1-183">Otros temas de referencia en la guía del desarrollador de IoT Hub son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="3c1d1-184">En [Puntos de conexión de IoT Hub][lnk-endpoints], se describen los diferentes puntos de conexión que expone cada centro de IoT Hub para las operaciones en tiempo de ejecución y de administración.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="3c1d1-185">En [Cuotas y limitación][lnk-quotas], se describen las cuotas y el comportamiento de limitación que se aplican al servicio IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="3c1d1-186">En [SDK de dispositivo y servicio IoT de Azure][lnk-sdks] se muestran los diversos SDK de lenguaje que puede usar para desarrollar aplicaciones para dispositivo y de servicio que interactúen con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="3c1d1-187">En [Lenguaje de consulta de IoT Hub][lnk-query], se describe el lenguaje de consulta que se puede usar para recuperar información de IoT Hub sobre los trabajos y dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="3c1d1-188">En [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt], se proporciona más información sobre la compatibilidad de IoT Hub con el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="3c1d1-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c1d1-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c1d1-189">Next steps</span></span>

<span data-ttu-id="3c1d1-190">Ahora que ha aprendido a cargar los archivos desde dispositivos con IoT Hub, puede interesarle el siguiente tema de la Guía del desarrollador de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="3c1d1-191">[Administrar identidades del dispositivo en IoT Hub][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="3c1d1-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="3c1d1-192">[Control del acceso a IoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="3c1d1-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="3c1d1-193">[Uso de dispositivos gemelos para sincronizar el estado y las configuraciones][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="3c1d1-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="3c1d1-194">[Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="3c1d1-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="3c1d1-195">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="3c1d1-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="3c1d1-196">Si desea probar algunos de los conceptos descritos en este artículo, puede interesarle el siguiente tutorial de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="3c1d1-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="3c1d1-197">[Cómo cargar archivos desde dispositivos a la nube con IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="3c1d1-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
