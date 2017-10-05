---
title: "Importación y exportación de identidades de dispositivo de IoT Hub de Azure | Microsoft Docs"
description: "Describe cómo usar el SDK de servicio IoT de Azure para realizar operaciones masivas en el registro de identidad con el fin de importar y exportar identidades de dispositivo. Las operaciones de importación permiten crear, actualizar y eliminar las identidades de dispositivo de forma masiva."
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
ms.openlocfilehash: ad2c6d585eef5450f7f0912ffa4753fe80d86b37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="2296f-104">Administración de las identidades de dispositivo de IoT Hub de forma masiva</span><span class="sxs-lookup"><span data-stu-id="2296f-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="2296f-105">Cada Centro de IoT tiene un registro de identidad que se puede usar para crear recursos por dispositivo en el servicio.</span><span class="sxs-lookup"><span data-stu-id="2296f-105">Each IoT hub has an identity registry you can use to create per-device resources in the service.</span></span> <span data-ttu-id="2296f-106">El registro de identidad también permite controlar el acceso a los puntos de conexión accesibles desde los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2296f-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="2296f-107">En este artículo se describe cómo importar y exportar identidades de dispositivo de forma masiva hacia y desde un Registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="2296f-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="2296f-108">Las operaciones de importación y exportación tienen lugar en el contexto de *Trabajos* que permiten ejecutar operaciones de servicio de forma masiva en un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2296f-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="2296f-109">La clase **RegistryManager** incluye los métodos **ExportDevicesAsync** y **ImportDevicesAsync**, que usan el marco **Trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2296f-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="2296f-110">Estos métodos le permiten exportar, importar y sincronizar la totalidad de un Registro de identidad de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2296f-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="2296f-111">¿Qué son los trabajos?</span><span class="sxs-lookup"><span data-stu-id="2296f-111">What are jobs?</span></span>

<span data-ttu-id="2296f-112">Las operaciones de Registro de identidad usan el sistema de **trabajo** cuando la operación:</span><span class="sxs-lookup"><span data-stu-id="2296f-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="2296f-113">Tiene un tiempo de ejecución potencialmente largo en comparación con las operaciones en tiempo de ejecución estándar.</span><span class="sxs-lookup"><span data-stu-id="2296f-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="2296f-114">Devuelve una gran cantidad de datos al usuario.</span><span class="sxs-lookup"><span data-stu-id="2296f-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="2296f-115">En estos casos, en lugar de una única API en espera o que bloquea el resultado de la operación, esta crea de forma asincrónica un **Trabajo** para ese Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2296f-115">Instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="2296f-116">La operación después devuelve inmediatamente un objeto **JobProperties**.</span><span class="sxs-lookup"><span data-stu-id="2296f-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="2296f-117">El siguiente fragmento de código de C# muestra cómo crear un trabajo de exportación:</span><span class="sxs-lookup"><span data-stu-id="2296f-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="2296f-118">Para usar la clase **RegistryManager** en el código de C#, agregue el paquete de NuGet **Microsoft.Azure.Devices** al proyecto.</span><span class="sxs-lookup"><span data-stu-id="2296f-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="2296f-119">La clase **RegistryManager** está en el espacio de nombres **Microsoft.Azure.Devices**.</span><span class="sxs-lookup"><span data-stu-id="2296f-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="2296f-120">Puede usar la clase **RegistryManager** para consultar el estado de **Trabajo** con los metadatos de **JobProperties** devueltos.</span><span class="sxs-lookup"><span data-stu-id="2296f-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="2296f-121">El siguiente fragmento de código de C# muestra cómo sondear cada cinco segundos para ver si el trabajo ha terminado de ejecutarse:</span><span class="sxs-lookup"><span data-stu-id="2296f-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="2296f-122">Exportación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="2296f-122">Export devices</span></span>

<span data-ttu-id="2296f-123">Use el método **ExportDevicesAsync** para exportar la totalidad de un Registro de identidad de IoT Hub a un contenedor de blobs de [Azure Storage](../storage/index.md) mediante una [firma de acceso compartido](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="2296f-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="2296f-124">Este método le permite crear copias de seguridad confiables de la información del dispositivo en un contenedor de blobs que usted controle.</span><span class="sxs-lookup"><span data-stu-id="2296f-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="2296f-125">El método **ExportDevicesAsync** requiere dos parámetros:</span><span class="sxs-lookup"><span data-stu-id="2296f-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="2296f-126">Una *cadena* que contiene un identificador URI de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2296f-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="2296f-127">Este identificador URI debe contener un token SAS que conceda acceso de escritura al contenedor.</span><span class="sxs-lookup"><span data-stu-id="2296f-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="2296f-128">El trabajo crea un blob en bloques en este contenedor para almacenar los datos serializados de exportación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="2296f-129">El token de SAS debe incluir estos permisos:</span><span class="sxs-lookup"><span data-stu-id="2296f-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="2296f-130">Un valor *booleano* que indica si desea excluir las claves de autenticación de los datos de exportación.</span><span class="sxs-lookup"><span data-stu-id="2296f-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="2296f-131">Si es **false**, las claves de autenticación se incluyen en la exportación.</span><span class="sxs-lookup"><span data-stu-id="2296f-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="2296f-132">De lo contrario, las claves se exportan como **null**.</span><span class="sxs-lookup"><span data-stu-id="2296f-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="2296f-133">El siguiente fragmento de código de C# muestra cómo iniciar un trabajo de exportación que incluye las claves de autenticación de dispositivo en los datos de exportación y luego sondea la finalización:</span><span class="sxs-lookup"><span data-stu-id="2296f-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
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

<span data-ttu-id="2296f-134">El trabajo almacena su salida en el contenedor de blobs proporcionado como un blob en bloques con el nombre **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="2296f-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="2296f-135">Los datos de salida se componen de datos de dispositivos serializados de JSON, con un dispositivo por línea.</span><span class="sxs-lookup"><span data-stu-id="2296f-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="2296f-136">En el siguiente ejemplo se muestran los datos de salida:</span><span class="sxs-lookup"><span data-stu-id="2296f-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Si un dispositivo tiene datos gemelos, estos también se exportan junto con los datos del dispositivo. En el siguiente ejemplo se muestra este formato. <span data-ttu-id="2296f-139">Todos los datos desde la línea "twinETag" hasta el final son datos gemelos.</span><span class="sxs-lookup"><span data-stu-id="2296f-139">All data from the "twinETag" line until the end are twin data.</span></span>

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

<span data-ttu-id="2296f-140">Si necesita acceso a los datos en el código, puede deserializar fácilmente estos datos mediante la clase **ExportImportDevice** .</span><span class="sxs-lookup"><span data-stu-id="2296f-140">If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class.</span></span> <span data-ttu-id="2296f-141">El siguiente fragmento de código de C# muestra cómo leer la información de dispositivo que se ha exportado previamente a un blob en bloques:</span><span class="sxs-lookup"><span data-stu-id="2296f-141">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

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
> <span data-ttu-id="2296f-142">También puede utilizar el método **GetDevicesAsync** de la clase **RegistryManager** para obtener una lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2296f-142">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="2296f-143">Sin embargo, este enfoque tiene un límite máximo de 1000 en cuanto al número de objetos de dispositivo que se devuelven.</span><span class="sxs-lookup"><span data-stu-id="2296f-143">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="2296f-144">El caso de uso esperado para el método **GetDevicesAsync** es para facilitar la depuración en escenarios de desarrollo, y no se recomienda para las cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="2296f-144">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="2296f-145">Importación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="2296f-145">Import devices</span></span>

<span data-ttu-id="2296f-146">El método **ImportDevicesAsync** de la clase **RegistryManager** le permite realizar operaciones de sincronización e importación masiva en un Registro de identidad de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2296f-146">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="2296f-147">Al igual que el método **ExportDevicesAsync**, el método **ImportDevicesAsync** usa el marco **Trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2296f-147">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="2296f-148">Tenga cuidado con el método **ImportDevicesAsync** porque además del aprovisionamiento de nuevos dispositivos en el Registro de identidad, también puede actualizar y eliminar dispositivos existentes.</span><span class="sxs-lookup"><span data-stu-id="2296f-148">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="2296f-149">Una operación de importación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="2296f-149">An import operation cannot be undone.</span></span> <span data-ttu-id="2296f-150">Realice siempre una copia de seguridad de los datos existentes mediante el método **ExportDevicesAsync** en otro contenedor de blobs antes de realizar cambios masivos en el Registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="2296f-150">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="2296f-151">El método **ImportDevicesAsync** requiere dos parámetros:</span><span class="sxs-lookup"><span data-stu-id="2296f-151">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="2296f-152">Una *cadena* que contiene un identificador URI de un contenedor de blobs de [Azure Storage](../storage/index.md) para usar como *entrada* para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2296f-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="2296f-153">Este identificador URI debe contener un token SAS que conceda acceso de lectura al contenedor.</span><span class="sxs-lookup"><span data-stu-id="2296f-153">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="2296f-154">Este contenedor debe incluir un blob con el nombre **devices.txt** que contenga los datos de dispositivo serializados para importar en el Registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="2296f-154">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="2296f-155">Los datos de importación deben contener la información del dispositivo en el mismo formato JSON que usa el trabajo **ExportImportDevice** cuando crea un blob **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="2296f-155">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="2296f-156">El token de SAS debe incluir estos permisos:</span><span class="sxs-lookup"><span data-stu-id="2296f-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="2296f-157">Una *cadena* que contenga un identificador URI de un contenedor de blobs de [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) para usar como *salida* del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2296f-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="2296f-158">El trabajo crea un blob en bloques en este contenedor para almacenar cualquier información de error del **Trabajo**de importación finalizado.</span><span class="sxs-lookup"><span data-stu-id="2296f-158">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="2296f-159">El token de SAS debe incluir estos permisos:</span><span class="sxs-lookup"><span data-stu-id="2296f-159">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="2296f-160">Los dos parámetros pueden apuntar al mismo contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2296f-160">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="2296f-161">Los parámetros independientes simplemente habilitan más control sobre sus datos, ya que el contenedor de salida requiere permisos adicionales.</span><span class="sxs-lookup"><span data-stu-id="2296f-161">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="2296f-162">El siguiente fragmento de código de C# muestra cómo iniciar un trabajo de importación:</span><span class="sxs-lookup"><span data-stu-id="2296f-162">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="2296f-163">Este método también se puede usar para importar los datos para el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="2296f-163">This method can also be used to import the data for the device twin.</span></span> <span data-ttu-id="2296f-164">El formato de la entrada de datos es el mismo que se muestra en la sección **ExportDevicesAsync**.</span><span class="sxs-lookup"><span data-stu-id="2296f-164">The format for the data input is the same as the format shown in the **ExportDevicesAsync** section.</span></span> <span data-ttu-id="2296f-165">De esta manera, se pueden volver a importar los datos exportados.</span><span class="sxs-lookup"><span data-stu-id="2296f-165">In this way, you can reimport the exported data.</span></span> <span data-ttu-id="2296f-166">El valor de **$metadata** es opcional.</span><span class="sxs-lookup"><span data-stu-id="2296f-166">The **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="2296f-167">Comportamiento de la importación</span><span class="sxs-lookup"><span data-stu-id="2296f-167">Import behavior</span></span>

<span data-ttu-id="2296f-168">Puede usar el método **ImportDevicesAsync** para realizar las siguientes operaciones de forma masiva en el Registro de identidad:</span><span class="sxs-lookup"><span data-stu-id="2296f-168">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="2296f-169">Registro masivo de nuevos dispositivos</span><span class="sxs-lookup"><span data-stu-id="2296f-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="2296f-170">Eliminación masiva de dispositivos existentes</span><span class="sxs-lookup"><span data-stu-id="2296f-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="2296f-171">Cambios masivos de estado (habilitar o deshabilitar dispositivos)</span><span class="sxs-lookup"><span data-stu-id="2296f-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="2296f-172">Asignación masiva de nuevas claves de autenticación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="2296f-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="2296f-173">Regeneración automática masiva de claves de autenticación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="2296f-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="2296f-174">Actualización masiva de datos gemelos</span><span class="sxs-lookup"><span data-stu-id="2296f-174">Bulk update of twin data</span></span>

<span data-ttu-id="2296f-175">Puede realizar cualquier combinación de las operaciones precedentes en una única llamada **ImportDevicesAsync**.</span><span class="sxs-lookup"><span data-stu-id="2296f-175">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="2296f-176">Por ejemplo, puede registrar nuevos dispositivos y eliminar o actualizar los dispositivos existentes al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="2296f-176">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="2296f-177">Cuando se utiliza junto con el método **ExportDevicesAsync** , puede migrar completamente todos los dispositivos de un Centro de IoT a otro.</span><span class="sxs-lookup"><span data-stu-id="2296f-177">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="2296f-178">Si el archivo de importación especifica metadatos gemelos, estos sobrescriben los existentes.</span><span class="sxs-lookup"><span data-stu-id="2296f-178">If the import file includes twin metadata, then this metadata overwrites the existing twin metadata.</span></span> <span data-ttu-id="2296f-179">Si el archivo de importación no incluye metadatos gemelos, solo se actualizan los metadatos de `lastUpdateTime` que usan la hora actual.</span><span class="sxs-lookup"><span data-stu-id="2296f-179">If the import file does not include twin metadata, then only the `lastUpdateTime` metadata is updated using the current time.</span></span>

<span data-ttu-id="2296f-180">Use la propiedad opcional **importMode** en los datos de serialización de importación para cada dispositivo para controlar el proceso de importación por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-180">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="2296f-181">La propiedad **importMode** tiene las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="2296f-181">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="2296f-182">importMode</span><span class="sxs-lookup"><span data-stu-id="2296f-182">importMode</span></span> | <span data-ttu-id="2296f-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="2296f-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2296f-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="2296f-184">**createOrUpdate**</span></span> |<span data-ttu-id="2296f-185">Si no existe un dispositivo con el **id.**especificado, este se registra por primera vez.</span><span class="sxs-lookup"><span data-stu-id="2296f-185">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="2296f-186">Si el dispositivo ya existe, la información existente se sobrescribe con los datos de entrada proporcionados con independencia del valor **ETag** .</span><span class="sxs-lookup"><span data-stu-id="2296f-186">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br> <span data-ttu-id="2296f-187">El usuario puede especificar opcionalmente datos gemelos junto con los datos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-187">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="2296f-188">El valor etag del gemelo, si se especifica, se procesa por separado del etag del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-188">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="2296f-189">Si no coincide con el etag del gemelo existente, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-189">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="2296f-190">**create**</span><span class="sxs-lookup"><span data-stu-id="2296f-190">**create**</span></span> |<span data-ttu-id="2296f-191">Si no existe un dispositivo con el **id.**especificado, este se registra por primera vez.</span><span class="sxs-lookup"><span data-stu-id="2296f-191">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="2296f-192">Si el dispositivo ya existe, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-192">If the device already exists, an error is written to the log file.</span></span> <br> <span data-ttu-id="2296f-193">El usuario puede especificar opcionalmente datos gemelos junto con los datos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-193">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="2296f-194">El valor etag del gemelo, si se especifica, se procesa por separado del etag del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-194">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="2296f-195">Si no coincide con el etag del gemelo existente, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-195">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="2296f-196">**update**</span><span class="sxs-lookup"><span data-stu-id="2296f-196">**update**</span></span> |<span data-ttu-id="2296f-197">Si ya existe un dispositivo con el **identificador** especificado, la información existente se sobrescribe con los datos de entrada proporcionados con independencia del valor **ETag**.</span><span class="sxs-lookup"><span data-stu-id="2296f-197">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="2296f-198">Si el dispositivo no existe, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-198">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="2296f-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="2296f-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="2296f-200">Si ya existe un dispositivo con el **identificador** especificado, la información existente se sobrescribe con los datos de entrada proporcionados solo si hay una coincidencia con **ETag**.</span><span class="sxs-lookup"><span data-stu-id="2296f-200">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="2296f-201">Si el dispositivo no existe, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-201">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="2296f-202">Si no existe la coincidencia con **ETag** , se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-202">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="2296f-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="2296f-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="2296f-204">Si no existe un dispositivo con el **id.**especificado, este se registra por primera vez.</span><span class="sxs-lookup"><span data-stu-id="2296f-204">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="2296f-205">Si el dispositivo ya existe, la información existente se sobrescribe con los datos de entrada proporcionados solo si hay una coincidencia con **ETag** .</span><span class="sxs-lookup"><span data-stu-id="2296f-205">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="2296f-206">Si no existe la coincidencia con **ETag** , se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-206">If there is an **ETag** mismatch, an error is written to the log file.</span></span> <br> <span data-ttu-id="2296f-207">El usuario puede especificar opcionalmente datos gemelos junto con los datos del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-207">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="2296f-208">El valor etag del gemelo, si se especifica, se procesa por separado del etag del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2296f-208">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="2296f-209">Si no coincide con el etag del gemelo existente, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-209">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="2296f-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="2296f-210">**delete**</span></span> |<span data-ttu-id="2296f-211">Si ya existe un dispositivo con el **identificador** especificado, este se elimina con independencia del valor **ETag**.</span><span class="sxs-lookup"><span data-stu-id="2296f-211">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="2296f-212">Si el dispositivo no existe, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-212">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="2296f-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="2296f-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="2296f-214">Si ya existe un dispositivo con el **identificador** especificado, este se elimina solo si hay una coincidencia con **ETag**.</span><span class="sxs-lookup"><span data-stu-id="2296f-214">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="2296f-215">Si el dispositivo no existe, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-215">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="2296f-216">Si no existe una coincidencia con ETag, se escribe un error en el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="2296f-216">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="2296f-217">Si los datos de serialización no definen explícitamente una marca **importMode** para un dispositivo, se establece de manera predeterminada en **createOrUpdate** durante la operación de importación.</span><span class="sxs-lookup"><span data-stu-id="2296f-217">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="2296f-218">Ejemplo de importación de dispositivos: aprovisionamiento masivo de dispositivos</span><span class="sxs-lookup"><span data-stu-id="2296f-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="2296f-219">El siguiente ejemplo de código de C# muestra cómo generar varias identidades de dispositivo que:</span><span class="sxs-lookup"><span data-stu-id="2296f-219">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="2296f-220">Incluyen claves de autenticación.</span><span class="sxs-lookup"><span data-stu-id="2296f-220">Include authentication keys.</span></span>
* <span data-ttu-id="2296f-221">Escriben la información del dispositivo en un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="2296f-221">Write that device information to a block blob.</span></span>
* <span data-ttu-id="2296f-222">Importan los dispositivos en el Registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="2296f-222">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
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

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
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

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="2296f-223">Ejemplo de importación de dispositivos: eliminación masiva</span><span class="sxs-lookup"><span data-stu-id="2296f-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="2296f-224">El ejemplo de código siguiente muestra cómo eliminar los dispositivos que ha agregado con el ejemplo de código anterior:</span><span class="sxs-lookup"><span data-stu-id="2296f-224">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
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

// Step 3: Call import using the same blob to delete all devices
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

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="2296f-225">Obtención del identificador URI de SAS del contenedor</span><span class="sxs-lookup"><span data-stu-id="2296f-225">Get the container SAS URI</span></span>

<span data-ttu-id="2296f-226">El ejemplo de código siguiente muestra cómo generar un [identificador URI de SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) con permisos de lectura, escritura y eliminación para un contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="2296f-226">The following code sample shows you how to generate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="2296f-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2296f-227">Next steps</span></span>

<span data-ttu-id="2296f-228">En este artículo, aprendió a realizar operaciones de forma masiva en el Registro de identidad en un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2296f-228">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="2296f-229">Siga estos vínculos para más información sobre la administración del Centro de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="2296f-229">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="2296f-230">[Métricas de IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="2296f-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="2296f-231">[Supervisión de operaciones][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="2296f-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="2296f-232">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="2296f-232">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2296f-233">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="2296f-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="2296f-234">[Simular un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2296f-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
