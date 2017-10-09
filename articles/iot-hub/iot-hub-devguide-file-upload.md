---
title: cargar el archivo aaaUnderstand centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - característica de carga de archivo uso Hola de toomanage centro de IoT cargar archivos desde un contenedor de blobs de dispositivo tooan almacenamiento de Azure."
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
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="97f9d-103">Carga de archivos con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="97f9d-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="97f9d-104">Tal como se detalla en hello [los extremos del centro de IoT] [ lnk-endpoints] artículo, un dispositivo puede iniciar una carga de archivo mediante el envío de una notificación a través de un punto de conexión de dispositivo (**/devices/ {deviceId} / archivos**).</span><span class="sxs-lookup"><span data-stu-id="97f9d-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="97f9d-105">Cuando un dispositivo notifica al centro de IoT que una carga completa, centro de IoT envía un mensaje de notificación de la carga de archivos a través de hello **/messages/servicebound/filenotifications** a nivel de servicio de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="97f9d-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="97f9d-106">En lugar de mensajes a través del centro de IoT propio de intermediación, centro de IoT en su lugar, actúa como un tooan distribuidor había asociado de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="97f9d-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="97f9d-107">Un dispositivo solicita un token de almacenamiento del centro de IoT es específico toohello archivo hello dispositivo desea tooupload.</span><span class="sxs-lookup"><span data-stu-id="97f9d-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="97f9d-108">dispositivo de Hello usa Hola URI de SAS tooupload Hola archivo toostorage y, cuando se completa la carga de hello dispositivo Hola envía una notificación de finalización tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="97f9d-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="97f9d-109">Centro de IoT comprueba la carga de archivos de hello es completa y, a continuación, agrega un extremo de notificación archivo carga notificación mensaje toohello a nivel de servicio archivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="97f9d-110">Antes de cargar un archivo tooIoT concentrador desde un dispositivo, debe configurar el centro por [asociar un almacenamiento de Azure] [ lnk-associate-storage] tooit de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="97f9d-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="97f9d-111">El dispositivo puede, a continuación, [inicializar una carga] [ lnk-initialize] y, a continuación, [notificar al centro de IoT] [ lnk-notify] cuando finalice la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="97f9d-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="97f9d-112">Si lo desea, cuando un dispositivo notifica al centro de IoT esa carga de hello finalización, el servicio Hola puede generar un [mensaje de notificación][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="97f9d-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="97f9d-113">Cuando toouse</span><span class="sxs-lookup"><span data-stu-id="97f9d-113">When toouse</span></span>

<span data-ttu-id="97f9d-114">Usar archivos de medios de toosend de carga de archivos y los lotes de telemetría grandes cargados por dispositivos conectados de forma intermitente o ancho de banda de toosave comprimido.</span><span class="sxs-lookup"><span data-stu-id="97f9d-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="97f9d-115">Consulte demasiado[Guía de comunicación de dispositivos a la nube] [ lnk-d2c-guidance] si está en duda entre usar propiedades notificados, mensajes del dispositivo a la nube o cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="97f9d-116">Asociar una cuenta de Azure Storage con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="97f9d-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="97f9d-117">funcionalidad de carga de archivos de hello toouse, primero debe vincular un toohello de cuenta de almacenamiento de Azure centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="97f9d-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="97f9d-118">Puede completar esta tarea a través de hello [portal de Azure][lnk-management-portal], o mediante programación a través de hello [API de REST de proveedor de recursos de centro de IoT] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="97f9d-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="97f9d-119">Una vez que haya asociado una cuenta de almacenamiento de Azure con el centro de IoT, Hola servicio devuelve un URI de SAS tooa dispositivo al dispositivo de hello inicia una solicitud de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="97f9d-120">Hola [SDK de Azure IoT] [ lnk-sdks] automáticamente Hola a recuperar el identificador URI de SAS, cargar archivo hello y notificar el centro de IoT de una carga completada.</span><span class="sxs-lookup"><span data-stu-id="97f9d-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="97f9d-121">Inicialización de una carga de archivos</span><span class="sxs-lookup"><span data-stu-id="97f9d-121">Initialize a file upload</span></span>
<span data-ttu-id="97f9d-122">Centro de IoT tiene un extremo concreto para dispositivos toorequest un URI de SAS para tooupload un archivo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97f9d-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="97f9d-123">proceso de carga de archivos de hello tooinitiate, Hola dispositivo envía una solicitud POST demasiado`{iot hub}.azure-devices.net/devices/{deviceId}/files` con hello siguiendo el cuerpo JSON:</span><span class="sxs-lookup"><span data-stu-id="97f9d-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="97f9d-124">Centro de IoT devuelve Hola datos, qué dispositivo hello usa el archivo de hello tooupload siguientes:</span><span class="sxs-lookup"><span data-stu-id="97f9d-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="97f9d-125">En desuso: inicializar una carga de archivo con un comando GET</span><span class="sxs-lookup"><span data-stu-id="97f9d-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="97f9d-126">Esta sección describe la funcionalidad en desuso para saber cómo tooreceive un URI de SAS del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="97f9d-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="97f9d-127">Utilice el método POST de Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="97f9d-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="97f9d-128">Centro de IoT tiene dos archivos de toosupport de extremos REST cargar uno tooget Hola URI de SAS para el almacenamiento y Hola otro centro de IoT de hello toonotify de una carga completada.</span><span class="sxs-lookup"><span data-stu-id="97f9d-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="97f9d-129">Hello dispositivo inicia el proceso de carga de archivos de hello mediante el envío de un centro de IoT GET toohello en `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="97f9d-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="97f9d-130">Centro de IoT Hola devuelve:</span><span class="sxs-lookup"><span data-stu-id="97f9d-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="97f9d-131">Un URI de SAS toohello específico archivo toobe cargado.</span><span class="sxs-lookup"><span data-stu-id="97f9d-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="97f9d-132">Un identificador de correlación toobe usa una vez completada la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="97f9d-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="97f9d-133">Notificación a IoT Hub de una carga de archivos completada</span><span class="sxs-lookup"><span data-stu-id="97f9d-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="97f9d-134">dispositivo de Hello es responsable de cargar Hola archivo toostorage mediante SDK de almacenamiento de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="97f9d-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="97f9d-135">Una vez completada la carga de hello, dispositivo Hola envía una solicitud POST demasiado`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` con hello siguiendo el cuerpo JSON:</span><span class="sxs-lookup"><span data-stu-id="97f9d-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="97f9d-136">Hola valo `isSuccess` es un valor Boolean que indica si el archivo hello se cargó correctamente.</span><span class="sxs-lookup"><span data-stu-id="97f9d-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="97f9d-137">Hola código de estado de `statusCode` es Hola estado para la carga de Hola de toostorage de archivo de Hola y Hola `statusDescription` corresponde toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="97f9d-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="97f9d-138">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="97f9d-138">Reference topics:</span></span>

<span data-ttu-id="97f9d-139">Hello temas de referencia siguientes proporcionan más información sobre cómo descargar archivos desde un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="97f9d-140">Notificaciones de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="97f9d-140">File upload notifications</span></span>

<span data-ttu-id="97f9d-141">Si lo desea, cuando un dispositivo notifica al centro de IoT que una carga completa, centro de IoT puede generar un mensaje de notificación que contiene Hola nombre y ubicación de almacenamiento de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="97f9d-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="97f9d-142">Como se ha explicado en [Puntos de conexión][lnk-endpoints], IoT Hub entrega notificaciones de carga de archivos a través de un punto de conexión accesible desde el servicio (**/messages/servicebound/fileuploadnotifications**) en forma de mensajes.</span><span class="sxs-lookup"><span data-stu-id="97f9d-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="97f9d-143">Hola semántica de recepción de notificaciones de carga de archivos son Hola igual que para los mensajes en la nube al dispositivo y ha Hola mismo [message Lifecycle-español][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="97f9d-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="97f9d-144">Cada mensaje recuperado de extremo de notificación de carga de archivo hello es un registro JSON con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="97f9d-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="97f9d-145">Propiedad</span><span class="sxs-lookup"><span data-stu-id="97f9d-145">Property</span></span> | <span data-ttu-id="97f9d-146">Description</span><span class="sxs-lookup"><span data-stu-id="97f9d-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97f9d-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="97f9d-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="97f9d-148">Marca de tiempo que indica cuando se creó la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="97f9d-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="97f9d-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="97f9d-149">DeviceId</span></span> |<span data-ttu-id="97f9d-150">**Id. de dispositivo** de dispositivo de Hola que cargan el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="97f9d-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="97f9d-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="97f9d-151">BlobUri</span></span> |<span data-ttu-id="97f9d-152">URI del archivo hello cargado.</span><span class="sxs-lookup"><span data-stu-id="97f9d-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="97f9d-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="97f9d-153">BlobName</span></span> |<span data-ttu-id="97f9d-154">Nombre del programa Hola a carga el archivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="97f9d-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="97f9d-155">LastUpdatedTime</span></span> |<span data-ttu-id="97f9d-156">Marca de tiempo que indica cuándo se actualizó por última vez archivo hello.</span><span class="sxs-lookup"><span data-stu-id="97f9d-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="97f9d-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="97f9d-157">BlobSizeInBytes</span></span> |<span data-ttu-id="97f9d-158">Tamaño del programa Hola a carga el archivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="97f9d-159">**Ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="97f9d-159">**Example**.</span></span> <span data-ttu-id="97f9d-160">Este ejemplo se muestra el cuerpo Hola de un archivo de carga de mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="97f9d-160">This example shows hello body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="97f9d-161">Opciones de configuración de notificaciones de carga de archivos</span><span class="sxs-lookup"><span data-stu-id="97f9d-161">File upload notification configuration options</span></span>

<span data-ttu-id="97f9d-162">Cada centro de IoT expone Hola siguientes opciones de configuración para las notificaciones de carga de archivo:</span><span class="sxs-lookup"><span data-stu-id="97f9d-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="97f9d-163">Propiedad</span><span class="sxs-lookup"><span data-stu-id="97f9d-163">Property</span></span> | <span data-ttu-id="97f9d-164">Description</span><span class="sxs-lookup"><span data-stu-id="97f9d-164">Description</span></span> | <span data-ttu-id="97f9d-165">Intervalo y valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="97f9d-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97f9d-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="97f9d-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="97f9d-167">Controla si las notificaciones de carga de archivo se escriben toohello extremo de notificaciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="97f9d-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="97f9d-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="97f9d-168">Bool.</span></span> <span data-ttu-id="97f9d-169">Valor predeterminado: True.</span><span class="sxs-lookup"><span data-stu-id="97f9d-169">Default: True.</span></span> |
| <span data-ttu-id="97f9d-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="97f9d-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="97f9d-171">TTL predeterminado para las notificaciones de carga de archivos.</span><span class="sxs-lookup"><span data-stu-id="97f9d-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="97f9d-172">Intervalo de ISO_8601 una too48H (1 minuto como mínimo).</span><span class="sxs-lookup"><span data-stu-id="97f9d-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="97f9d-173">Valor predeterminado: 1 hora.</span><span class="sxs-lookup"><span data-stu-id="97f9d-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="97f9d-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="97f9d-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="97f9d-175">Duración del bloqueo de la cola de notificaciones de carga de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="97f9d-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="97f9d-176">5 too300 segundos (5 segundos como mínimos).</span><span class="sxs-lookup"><span data-stu-id="97f9d-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="97f9d-177">Valor predeterminado: 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="97f9d-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="97f9d-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="97f9d-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="97f9d-179">Número máximo de entregas de archivo hello cargar cola de notificación.</span><span class="sxs-lookup"><span data-stu-id="97f9d-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="97f9d-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="97f9d-180">1 too100.</span></span> <span data-ttu-id="97f9d-181">Valor predeterminado: 100.</span><span class="sxs-lookup"><span data-stu-id="97f9d-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="97f9d-182">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="97f9d-182">Additional reference material</span></span>

<span data-ttu-id="97f9d-183">Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:</span><span class="sxs-lookup"><span data-stu-id="97f9d-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="97f9d-184">[Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.</span><span class="sxs-lookup"><span data-stu-id="97f9d-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="97f9d-185">[Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola y comportamientos que se aplican toohello servicio del centro de IoT de limitación.</span><span class="sxs-lookup"><span data-stu-id="97f9d-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="97f9d-186">[SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK que se puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="97f9d-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="97f9d-187">[Lenguaje de consulta de centro de IoT] [ lnk-query] describe el lenguaje de consulta de Hola que puede utilizar información tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.</span><span class="sxs-lookup"><span data-stu-id="97f9d-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="97f9d-188">[Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="97f9d-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97f9d-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97f9d-189">Next steps</span></span>

<span data-ttu-id="97f9d-190">Ahora que ha aprendido cómo tooupload los archivos de dispositivos mediante el centro de IoT, es posible que interesa Hola temas de guía para desarrolladores de centro de IoT siguientes:</span><span class="sxs-lookup"><span data-stu-id="97f9d-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="97f9d-191">[Administrar identidades del dispositivo en IoT Hub][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="97f9d-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="97f9d-192">[Controlar el acceso tooIoT concentrador][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="97f9d-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="97f9d-193">[Usar el estado del dispositivo: los gemelos toosynchronize y configuraciones][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="97f9d-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="97f9d-194">[Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="97f9d-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="97f9d-195">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="97f9d-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="97f9d-196">Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="97f9d-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="97f9d-197">[Funcionamiento de cloud archivos tooupload de toohello de dispositivos con el centro de IoT][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="97f9d-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
