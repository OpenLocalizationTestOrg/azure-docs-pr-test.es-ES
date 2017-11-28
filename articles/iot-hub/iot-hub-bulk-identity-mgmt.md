---
title: "exportación de aaaImport de identidades de dispositivos del centro de IoT de Azure | Documentos de Microsoft"
description: "¿Cómo toouse hello Azure IoT servicio SDK tooperform operaciones contra Hola identidad del registro tooimport masiva y exportar identidades de dispositivos. Las operaciones de importación permiten toocreate, update y delete de identidades de dispositivos de forma masiva."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="6bdce-104">Administración de las identidades de dispositivo de IoT Hub de forma masiva</span><span class="sxs-lookup"><span data-stu-id="6bdce-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="6bdce-105">Cada centro de IoT tiene un registro de la identidad puede usar recursos de toocreate por dispositivo de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="6bdce-106">registro de la identidad de Hello también permite los puntos de conexión de dispositivo de toocontrol acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="6bdce-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="6bdce-107">Este artículo describe cómo tooimport y exportar identidades de dispositivos de forma masiva tooand desde un registro de la identidad.</span><span class="sxs-lookup"><span data-stu-id="6bdce-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="6bdce-108">Las operaciones de importación y exportación tienen lugar en el contexto de Hola de *trabajos* que le permiten operaciones de servicio de forma masiva tooexecute en un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6bdce-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="6bdce-109">Hola **RegistryManager** clase incluye hello **ExportDevicesAsync** y **ImportDevicesAsync** métodos que usan hello **trabajo** marco de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6bdce-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="6bdce-110">Estos métodos permiten tooexport, importación y sincronización la totalidad de Hola de un registro de identidad IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6bdce-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="6bdce-111">¿Qué son los trabajos?</span><span class="sxs-lookup"><span data-stu-id="6bdce-111">What are jobs?</span></span>

<span data-ttu-id="6bdce-112">Las operaciones del registro de identidad usan hello **trabajo** sistema Hola cuando la operación:</span><span class="sxs-lookup"><span data-stu-id="6bdce-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="6bdce-113">Se potencialmente mucho tiempo de ejecución comparado toostandard operaciones en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6bdce-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="6bdce-114">Devuelve una gran cantidad de usuario de toohello de datos.</span><span class="sxs-lookup"><span data-stu-id="6bdce-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="6bdce-115">En lugar de una sola llamada de API en espera o bloqueos en el resultado de hello de operación de hello, operación Hola crea de forma asincrónica un **trabajo** para ese centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6bdce-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="6bdce-116">operación de Hello, a continuación, inmediatamente devuelve un **JobProperties** objeto.</span><span class="sxs-lookup"><span data-stu-id="6bdce-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="6bdce-117">Hola después de C# código fragmento de código se muestra cómo toocreate un trabajo de exportación:</span><span class="sxs-lookup"><span data-stu-id="6bdce-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="6bdce-118">Hola toouse **RegistryManager** clase en el código de C#, agregue hello **Microsoft.Azure.Devices** proyecto de tooyour de paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="6bdce-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="6bdce-119">Hola **RegistryManager** clase está en hello **Microsoft.Azure.Devices** espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="6bdce-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="6bdce-120">Puede usar hello **RegistryManager** clase tooquery estado de Hola de hello **trabajo** con hello devuelve **JobProperties** metadatos.</span><span class="sxs-lookup"><span data-stu-id="6bdce-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="6bdce-121">Hello siguiente fragmento de código de C# muestra cómo toopoll cada cinco segundos toosee si hello trabajo ha terminado de ejecutar:</span><span class="sxs-lookup"><span data-stu-id="6bdce-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="6bdce-122">Exportación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="6bdce-122">Export devices</span></span>

<span data-ttu-id="6bdce-123">Hola de uso **ExportDevicesAsync** totalidad de hello tooexport de método de un tooan de registro de identidad de IoT hub [el almacenamiento de Azure](../storage/index.md) contenedor de blob mediante un [firma de acceso compartido](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="6bdce-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="6bdce-124">Este método permite toocreate copias de seguridad confiable de la información del dispositivo en un contenedor de blob que usted controla.</span><span class="sxs-lookup"><span data-stu-id="6bdce-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="6bdce-125">Hola **ExportDevicesAsync** método requiere dos parámetros:</span><span class="sxs-lookup"><span data-stu-id="6bdce-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="6bdce-126">Una *cadena* que contiene un identificador URI de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="6bdce-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="6bdce-127">Este identificador URI debe contener un token SAS que concede acceso de escritura toohello contenedor.</span><span class="sxs-lookup"><span data-stu-id="6bdce-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="6bdce-128">trabajo de Hello crea un blob en bloques en estos datos de dispositivo de exportación de contenedor toostore Hola serializado.</span><span class="sxs-lookup"><span data-stu-id="6bdce-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="6bdce-129">token de SAS de Hello debe incluir estos permisos:</span><span class="sxs-lookup"><span data-stu-id="6bdce-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="6bdce-130">A *booleano* que indica si desea que las claves de autenticación de tooexclude de los datos de exportación.</span><span class="sxs-lookup"><span data-stu-id="6bdce-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="6bdce-131">Si es **false**, las claves de autenticación se incluyen en la exportación.</span><span class="sxs-lookup"><span data-stu-id="6bdce-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="6bdce-132">De lo contrario, las claves se exportan como **null**.</span><span class="sxs-lookup"><span data-stu-id="6bdce-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="6bdce-133">Hello siguiente fragmento de código de C# muestra cómo tooinitiate un trabajo de exportación que incluye las claves de autenticación de dispositivo en hello exportar los datos y, a continuación, el sondeo de finalización:</span><span class="sxs-lookup"><span data-stu-id="6bdce-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="6bdce-134">Hello trabajo almacena su salida en el contenedor de blobs de hello proporcionado como un blob en bloques con nombre hello **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="6bdce-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="6bdce-135">datos de salida de Hello constan de JSON que serializa datos del dispositivo, con un dispositivo por línea.</span><span class="sxs-lookup"><span data-stu-id="6bdce-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="6bdce-136">Hello en el ejemplo siguiente se muestra datos de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="6bdce-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Si un dispositivo tiene datos gemelas, datos de hello gemelas también se exportan junto con los datos del dispositivo Hola. Hello en el ejemplo siguiente se muestra este formato. <span data-ttu-id="6bdce-139">Todos los datos de línea de "twinETag" hello hasta el final de hello son datos gemelas.</span><span class="sxs-lookup"><span data-stu-id="6bdce-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="6bdce-140">Si necesita obtener acceso a datos de toothis en el código, puede deserializar fácilmente estos datos con hello **ExportImportDevice** clase.</span><span class="sxs-lookup"><span data-stu-id="6bdce-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="6bdce-141">Hello siguiente fragmento de código de C# muestra cómo la información de dispositivo de tooread que exportó anteriormente tooa blob en bloques:</span><span class="sxs-lookup"><span data-stu-id="6bdce-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="6bdce-142">También puede usar hello **GetDevicesAsync** método de hello **RegistryManager** clase toofetch una lista de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6bdce-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="6bdce-143">Sin embargo, este enfoque tiene un límite máximo de 1000 en número de Hola de objetos de dispositivo que se devuelven.</span><span class="sxs-lookup"><span data-stu-id="6bdce-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="6bdce-144">Hola espera caso de uso de hello **GetDevicesAsync** método es para la depuración de tooaid de escenarios de desarrollo y no se recomienda para las cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="6bdce-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="6bdce-145">Importación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="6bdce-145">Import devices</span></span>

<span data-ttu-id="6bdce-146">Hola **ImportDevicesAsync** método Hola **RegistryManager** clase permite operaciones de importación y sincronización de masiva de tooperform en un registro de identidad IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6bdce-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="6bdce-147">Al igual que hello **ExportDevicesAsync** /método siguiente, hello **ImportDevicesAsync** método usa Hola **trabajo** framework.</span><span class="sxs-lookup"><span data-stu-id="6bdce-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="6bdce-148">Tenga cuidado utilizando hello **ImportDevicesAsync** método porque en suma tooprovisioning nuevos dispositivos en el registro de identidad, también puede actualizar y eliminar los dispositivos existentes.</span><span class="sxs-lookup"><span data-stu-id="6bdce-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="6bdce-149">Una operación de importación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="6bdce-149">An import operation cannot be undone.</span></span> <span data-ttu-id="6bdce-150">Realizar la copia de seguridad de los datos existentes con hello siempre **ExportDevicesAsync** contenedor de blobs de método tooanother antes de realizar cargas masivas cambios del registro de identidad tooyour.</span><span class="sxs-lookup"><span data-stu-id="6bdce-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="6bdce-151">Hola **ImportDevicesAsync** método toma dos parámetros:</span><span class="sxs-lookup"><span data-stu-id="6bdce-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="6bdce-152">A *cadena* que contiene un identificador URI de un [el almacenamiento de Azure](../storage/index.md) blob toouse contenedor como *entrada* toohello trabajo.</span><span class="sxs-lookup"><span data-stu-id="6bdce-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="6bdce-153">Este identificador URI debe contener un token SAS que concede acceso de lectura toohello contenedor.</span><span class="sxs-lookup"><span data-stu-id="6bdce-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="6bdce-154">Este contenedor debe contener un blob con nombre hello **devices.txt** tooimport de datos del dispositivo de hello serializado que contiene en su registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="6bdce-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="6bdce-155">Hello datos de importación deben contener información del dispositivo en hello JSON mismo formato que hello **ExportImportDevice** trabajo que se usa cuando crea un **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="6bdce-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="6bdce-156">token de SAS de Hello debe incluir estos permisos:</span><span class="sxs-lookup"><span data-stu-id="6bdce-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="6bdce-157">A *cadena* que contiene un identificador URI de un [el almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/) blob toouse contenedor como *salida* de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="6bdce-158">Hello trabajo crea un blob en bloques en este contenedor toostore cualquier información de error de importación de hello completado **trabajo**.</span><span class="sxs-lookup"><span data-stu-id="6bdce-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="6bdce-159">token de SAS de Hello debe incluir estos permisos:</span><span class="sxs-lookup"><span data-stu-id="6bdce-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="6bdce-160">parámetros de Hello dos pueden apuntar toohello mismo contenedor de blob.</span><span class="sxs-lookup"><span data-stu-id="6bdce-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="6bdce-161">parámetros separados Hola simplemente permiten un mayor control sobre los datos tal y como contenedor de salida de hello requiere permisos adicionales.</span><span class="sxs-lookup"><span data-stu-id="6bdce-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="6bdce-162">Hola después de C# código fragmento de código se muestra cómo tooinitiate un trabajo de importación:</span><span class="sxs-lookup"><span data-stu-id="6bdce-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="6bdce-163">Este método también puede ser datos de Hola de tooimport usado para gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="6bdce-164">formato de Hello para la entrada de datos de Hola Hola igual como formato de Hola se muestra en hello **ExportDevicesAsync** sección.</span><span class="sxs-lookup"><span data-stu-id="6bdce-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="6bdce-165">De esta manera, puede volver a importar Hola exportan datos.</span><span class="sxs-lookup"><span data-stu-id="6bdce-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="6bdce-166">Hola **$metadata** es opcional.</span><span class="sxs-lookup"><span data-stu-id="6bdce-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="6bdce-167">Comportamiento de la importación</span><span class="sxs-lookup"><span data-stu-id="6bdce-167">Import behavior</span></span>

<span data-ttu-id="6bdce-168">Puede usar hello **ImportDevicesAsync** método tooperform Hola a continuación de forma masiva las operaciones en el registro de identidad:</span><span class="sxs-lookup"><span data-stu-id="6bdce-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="6bdce-169">Registro masivo de nuevos dispositivos</span><span class="sxs-lookup"><span data-stu-id="6bdce-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="6bdce-170">Eliminación masiva de dispositivos existentes</span><span class="sxs-lookup"><span data-stu-id="6bdce-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="6bdce-171">Cambios masivos de estado (habilitar o deshabilitar dispositivos)</span><span class="sxs-lookup"><span data-stu-id="6bdce-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="6bdce-172">Asignación masiva de nuevas claves de autenticación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="6bdce-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="6bdce-173">Regeneración automática masiva de claves de autenticación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="6bdce-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="6bdce-174">Actualización masiva de datos gemelos</span><span class="sxs-lookup"><span data-stu-id="6bdce-174">Bulk update of twin data</span></span>

<span data-ttu-id="6bdce-175">Puede realizar cualquier combinación de hello anteriores operaciones dentro de una única **ImportDevicesAsync** llamar.</span><span class="sxs-lookup"><span data-stu-id="6bdce-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="6bdce-176">Por ejemplo, puede registrar nuevos dispositivos y eliminar o actualizar los dispositivos existentes en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="6bdce-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="6bdce-177">Cuando se usa junto con hello **ExportDevicesAsync** método, puede migrar completamente todos los dispositivos desde una tooanother de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6bdce-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="6bdce-178">Si el archivo de importación de hello incluye metadatos gemelas, estos metadatos sobrescriben Hola existente gemelas metadatos.</span><span class="sxs-lookup"><span data-stu-id="6bdce-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="6bdce-179">Si el archivo de importación de hello no incluye metadatos gemelas, a continuación, solo Hola `lastUpdateTime` se actualizan los metadatos utilizando Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="6bdce-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="6bdce-180">Hola de uso opcional **importMode** propiedad en los datos de serialización de importación de Hola para cada dispositivo toocontrol Hola importación proceso por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6bdce-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="6bdce-181">Hola **importMode** propiedad tiene Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="6bdce-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="6bdce-182">importMode</span><span class="sxs-lookup"><span data-stu-id="6bdce-182">importMode</span></span> | <span data-ttu-id="6bdce-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="6bdce-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6bdce-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="6bdce-184">**createOrUpdate**</span></span> |<span data-ttu-id="6bdce-185">Si no existe un dispositivo con hello especificado **identificador**, está registrado recientemente.</span><span class="sxs-lookup"><span data-stu-id="6bdce-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="6bdce-186">Si el dispositivo de hello ya existe, se sobrescribe la información existente con hello proporcionada datos de entrada sin tener en cuenta toohello **ETag** valor.</span><span class="sxs-lookup"><span data-stu-id="6bdce-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="6bdce-187">usuario de Hello, opcionalmente, puede especificar datos gemelas junto con los datos del dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="6bdce-188">valor etag del gemelas Hello, si se especifica, se procesa por separado de etag del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="6bdce-189">Si hay una falta de coincidencia con el etag del gemelas existente de hello, se escribe un error en el archivo de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="6bdce-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="6bdce-190">**crear**</span><span class="sxs-lookup"><span data-stu-id="6bdce-190">**create**</span></span> |<span data-ttu-id="6bdce-191">Si no existe un dispositivo con hello especificado **identificador**, está registrado recientemente.</span><span class="sxs-lookup"><span data-stu-id="6bdce-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="6bdce-192">Si ya existe un dispositivo de hello, se escribe un error en el archivo de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="6bdce-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="6bdce-193">usuario de Hello, opcionalmente, puede especificar datos gemelas junto con los datos del dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="6bdce-194">valor etag del gemelas Hello, si se especifica, se procesa por separado de etag del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="6bdce-195">Si hay una falta de coincidencia con el etag del gemelas existente de hello, se escribe un error en el archivo de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="6bdce-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="6bdce-196">**update**</span><span class="sxs-lookup"><span data-stu-id="6bdce-196">**update**</span></span> |<span data-ttu-id="6bdce-197">Si ya existe un dispositivo con hello especificado **identificador**, se sobrescribe la información existente con hello proporcionada datos de entrada sin tener en cuenta toohello **ETag** valor.</span><span class="sxs-lookup"><span data-stu-id="6bdce-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="6bdce-198">Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="6bdce-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="6bdce-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="6bdce-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="6bdce-200">Si ya existe un dispositivo con hello especificado **identificador**, se sobrescribe la información existente con hello proporcionada datos de entrada sólo si hay un **ETag** coincide con.</span><span class="sxs-lookup"><span data-stu-id="6bdce-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="6bdce-201">Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="6bdce-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="6bdce-202">Si no hay un **ETag** falta de coincidencia, se escribe el archivo de registro de toohello un error.</span><span class="sxs-lookup"><span data-stu-id="6bdce-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="6bdce-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="6bdce-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="6bdce-204">Si no existe un dispositivo con hello especificado **identificador**, está registrado recientemente.</span><span class="sxs-lookup"><span data-stu-id="6bdce-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="6bdce-205">Si ya existe un dispositivo de hello, se sobrescribe la información existente con hello proporcionada datos de entrada sólo si hay un **ETag** coincide con.</span><span class="sxs-lookup"><span data-stu-id="6bdce-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="6bdce-206">Si no hay un **ETag** falta de coincidencia, se escribe el archivo de registro de toohello un error.</span><span class="sxs-lookup"><span data-stu-id="6bdce-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="6bdce-207">usuario de Hello, opcionalmente, puede especificar datos gemelas junto con los datos del dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="6bdce-208">valor etag del gemelas Hello, si se especifica, se procesa por separado de etag del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="6bdce-209">Si hay una falta de coincidencia con el etag del gemelas existente de hello, se escribe un error en el archivo de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="6bdce-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="6bdce-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="6bdce-210">**delete**</span></span> |<span data-ttu-id="6bdce-211">Si ya existe un dispositivo con hello especificado **identificador**, se elimina sin tener en cuenta toohello **ETag** valor.</span><span class="sxs-lookup"><span data-stu-id="6bdce-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="6bdce-212">Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="6bdce-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="6bdce-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="6bdce-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="6bdce-214">Si ya existe un dispositivo con hello especificado **identificador**, se elimina solo si hay un **ETag** coincide con.</span><span class="sxs-lookup"><span data-stu-id="6bdce-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="6bdce-215">Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="6bdce-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="6bdce-216">Si se produce un error de coincidencia de ETag, se escribe un error en el archivo de registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="6bdce-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="6bdce-217">Si no definen explícitamente los datos de serialización de hello un **importMode** marca para un dispositivo, el valor predeterminado es demasiado**createOrUpdate** Hola durante la operación de importación.</span><span class="sxs-lookup"><span data-stu-id="6bdce-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="6bdce-218">Ejemplo de importación de dispositivos: aprovisionamiento masivo de dispositivos</span><span class="sxs-lookup"><span data-stu-id="6bdce-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="6bdce-219">Hello siguiente ejemplo de código de C# se muestra cómo toogenerate varias identidades de dispositivos que:</span><span class="sxs-lookup"><span data-stu-id="6bdce-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="6bdce-220">Incluyen claves de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6bdce-220">Include authentication keys.</span></span>
* <span data-ttu-id="6bdce-221">Escribir ese blob en bloques dispositivo información tooa.</span><span class="sxs-lookup"><span data-stu-id="6bdce-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="6bdce-222">Importar dispositivos Hola del registro de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="6bdce-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="6bdce-223">Ejemplo de importación de dispositivos: eliminación masiva</span><span class="sxs-lookup"><span data-stu-id="6bdce-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="6bdce-224">Hello ejemplo de código siguiente muestra cómo los dispositivos de hello toodelete mediante que agregó Hola ejemplo de código anterior:</span><span class="sxs-lookup"><span data-stu-id="6bdce-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="6bdce-225">Obtener el contenedor de hello URI de SAS</span><span class="sxs-lookup"><span data-stu-id="6bdce-225">Get hello container SAS URI</span></span>

<span data-ttu-id="6bdce-226">Hello ejemplo de código siguiente muestra cómo toogenerate una [URI de SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) con lectura, escritura y eliminación de permisos para un contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="6bdce-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="6bdce-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6bdce-227">Next steps</span></span>

<span data-ttu-id="6bdce-228">En este artículo, ha aprendido cómo tooperform de forma masiva las operaciones en el registro de la identidad de hello en un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6bdce-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="6bdce-229">Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="6bdce-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="6bdce-230">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="6bdce-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="6bdce-231">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="6bdce-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="6bdce-232">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="6bdce-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6bdce-233">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6bdce-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="6bdce-234">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6bdce-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
