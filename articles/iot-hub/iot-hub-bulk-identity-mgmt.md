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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Administración de las identidades de dispositivo de IoT Hub de forma masiva

Cada centro de IoT tiene un registro de la identidad puede usar recursos de toocreate por dispositivo de servicio de Hola. registro de la identidad de Hello también permite los puntos de conexión de dispositivo de toocontrol acceso toohello. Este artículo describe cómo tooimport y exportar identidades de dispositivos de forma masiva tooand desde un registro de la identidad.

Las operaciones de importación y exportación tienen lugar en el contexto de Hola de *trabajos* que le permiten operaciones de servicio de forma masiva tooexecute en un centro de IoT.

Hola **RegistryManager** clase incluye hello **ExportDevicesAsync** y **ImportDevicesAsync** métodos que usan hello **trabajo** marco de trabajo. Estos métodos permiten tooexport, importación y sincronización la totalidad de Hola de un registro de identidad IoT hub.

## <a name="what-are-jobs"></a>¿Qué son los trabajos?

Las operaciones del registro de identidad usan hello **trabajo** sistema Hola cuando la operación:

* Se potencialmente mucho tiempo de ejecución comparado toostandard operaciones en tiempo de ejecución.
* Devuelve una gran cantidad de usuario de toohello de datos.

En lugar de una sola llamada de API en espera o bloqueos en el resultado de hello de operación de hello, operación Hola crea de forma asincrónica un **trabajo** para ese centro de IoT. operación de Hello, a continuación, inmediatamente devuelve un **JobProperties** objeto.

Hola después de C# código fragmento de código se muestra cómo toocreate un trabajo de exportación:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> Hola toouse **RegistryManager** clase en el código de C#, agregue hello **Microsoft.Azure.Devices** proyecto de tooyour de paquete de NuGet. Hola **RegistryManager** clase está en hello **Microsoft.Azure.Devices** espacio de nombres.

Puede usar hello **RegistryManager** clase tooquery estado de Hola de hello **trabajo** con hello devuelve **JobProperties** metadatos.

Hello siguiente fragmento de código de C# muestra cómo toopoll cada cinco segundos toosee si hello trabajo ha terminado de ejecutar:

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

## <a name="export-devices"></a>Exportación de dispositivos

Hola de uso **ExportDevicesAsync** totalidad de hello tooexport de método de un tooan de registro de identidad de IoT hub [el almacenamiento de Azure](../storage/index.md) contenedor de blob mediante un [firma de acceso compartido](../storage/common/storage-security-guide.md#data-plane-security).

Este método permite toocreate copias de seguridad confiable de la información del dispositivo en un contenedor de blob que usted controla.

Hola **ExportDevicesAsync** método requiere dos parámetros:

* Una *cadena* que contiene un identificador URI de un contenedor de blobs. Este identificador URI debe contener un token SAS que concede acceso de escritura toohello contenedor. trabajo de Hello crea un blob en bloques en estos datos de dispositivo de exportación de contenedor toostore Hola serializado. token de SAS de Hello debe incluir estos permisos:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* A *booleano* que indica si desea que las claves de autenticación de tooexclude de los datos de exportación. Si es **false**, las claves de autenticación se incluyen en la exportación. De lo contrario, las claves se exportan como **null**.

Hello siguiente fragmento de código de C# muestra cómo tooinitiate un trabajo de exportación que incluye las claves de autenticación de dispositivo en hello exportar los datos y, a continuación, el sondeo de finalización:

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

Hello trabajo almacena su salida en el contenedor de blobs de hello proporcionado como un blob en bloques con nombre hello **devices.txt**. datos de salida de Hello constan de JSON que serializa datos del dispositivo, con un dispositivo por línea.

Hello en el ejemplo siguiente se muestra datos de salida de hello:

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Si un dispositivo tiene datos gemelas, datos de hello gemelas también se exportan junto con los datos del dispositivo Hola. Hello en el ejemplo siguiente se muestra este formato. Todos los datos de línea de "twinETag" hello hasta el final de hello son datos gemelas.

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

Si necesita obtener acceso a datos de toothis en el código, puede deserializar fácilmente estos datos con hello **ExportImportDevice** clase. Hello siguiente fragmento de código de C# muestra cómo la información de dispositivo de tooread que exportó anteriormente tooa blob en bloques:

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
> También puede usar hello **GetDevicesAsync** método de hello **RegistryManager** clase toofetch una lista de los dispositivos. Sin embargo, este enfoque tiene un límite máximo de 1000 en número de Hola de objetos de dispositivo que se devuelven. Hola espera caso de uso de hello **GetDevicesAsync** método es para la depuración de tooaid de escenarios de desarrollo y no se recomienda para las cargas de trabajo de producción.

## <a name="import-devices"></a>Importación de dispositivos

Hola **ImportDevicesAsync** método Hola **RegistryManager** clase permite operaciones de importación y sincronización de masiva de tooperform en un registro de identidad IoT hub. Al igual que hello **ExportDevicesAsync** /método siguiente, hello **ImportDevicesAsync** método usa Hola **trabajo** framework.

Tenga cuidado utilizando hello **ImportDevicesAsync** método porque en suma tooprovisioning nuevos dispositivos en el registro de identidad, también puede actualizar y eliminar los dispositivos existentes.

> [!WARNING]
> Una operación de importación no se puede deshacer. Realizar la copia de seguridad de los datos existentes con hello siempre **ExportDevicesAsync** contenedor de blobs de método tooanother antes de realizar cargas masivas cambios del registro de identidad tooyour.

Hola **ImportDevicesAsync** método toma dos parámetros:

* A *cadena* que contiene un identificador URI de un [el almacenamiento de Azure](../storage/index.md) blob toouse contenedor como *entrada* toohello trabajo. Este identificador URI debe contener un token SAS que concede acceso de lectura toohello contenedor. Este contenedor debe contener un blob con nombre hello **devices.txt** tooimport de datos del dispositivo de hello serializado que contiene en su registro de identidad. Hello datos de importación deben contener información del dispositivo en hello JSON mismo formato que hello **ExportImportDevice** trabajo que se usa cuando crea un **devices.txt** blob. token de SAS de Hello debe incluir estos permisos:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* A *cadena* que contiene un identificador URI de un [el almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/) blob toouse contenedor como *salida* de trabajo de Hola. Hello trabajo crea un blob en bloques en este contenedor toostore cualquier información de error de importación de hello completado **trabajo**. token de SAS de Hello debe incluir estos permisos:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> parámetros de Hello dos pueden apuntar toohello mismo contenedor de blob. parámetros separados Hola simplemente permiten un mayor control sobre los datos tal y como contenedor de salida de hello requiere permisos adicionales.

Hola después de C# código fragmento de código se muestra cómo tooinitiate un trabajo de importación:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Este método también puede ser datos de Hola de tooimport usado para gemelas de dispositivo de Hola. formato de Hello para la entrada de datos de Hola Hola igual como formato de Hola se muestra en hello **ExportDevicesAsync** sección. De esta manera, puede volver a importar Hola exportan datos. Hola **$metadata** es opcional.

## <a name="import-behavior"></a>Comportamiento de la importación

Puede usar hello **ImportDevicesAsync** método tooperform Hola a continuación de forma masiva las operaciones en el registro de identidad:

* Registro masivo de nuevos dispositivos
* Eliminación masiva de dispositivos existentes
* Cambios masivos de estado (habilitar o deshabilitar dispositivos)
* Asignación masiva de nuevas claves de autenticación de dispositivos
* Regeneración automática masiva de claves de autenticación de dispositivos
* Actualización masiva de datos gemelos

Puede realizar cualquier combinación de hello anteriores operaciones dentro de una única **ImportDevicesAsync** llamar. Por ejemplo, puede registrar nuevos dispositivos y eliminar o actualizar los dispositivos existentes en hello mismo tiempo. Cuando se usa junto con hello **ExportDevicesAsync** método, puede migrar completamente todos los dispositivos desde una tooanother de centro de IoT.

Si el archivo de importación de hello incluye metadatos gemelas, estos metadatos sobrescriben Hola existente gemelas metadatos. Si el archivo de importación de hello no incluye metadatos gemelas, a continuación, solo Hola `lastUpdateTime` se actualizan los metadatos utilizando Hola hora actual.

Hola de uso opcional **importMode** propiedad en los datos de serialización de importación de Hola para cada dispositivo toocontrol Hola importación proceso por dispositivo. Hola **importMode** propiedad tiene Hola siguientes opciones:

| importMode | Descripción |
| --- | --- |
| **createOrUpdate** |Si no existe un dispositivo con hello especificado **identificador**, está registrado recientemente. <br/>Si el dispositivo de hello ya existe, se sobrescribe la información existente con hello proporcionada datos de entrada sin tener en cuenta toohello **ETag** valor. <br> usuario de Hello, opcionalmente, puede especificar datos gemelas junto con los datos del dispositivo Hola. valor etag del gemelas Hello, si se especifica, se procesa por separado de etag del dispositivo de Hola. Si hay una falta de coincidencia con el etag del gemelas existente de hello, se escribe un error en el archivo de registro de toohello. |
| **crear** |Si no existe un dispositivo con hello especificado **identificador**, está registrado recientemente. <br/>Si ya existe un dispositivo de hello, se escribe un error en el archivo de registro de toohello. <br> usuario de Hello, opcionalmente, puede especificar datos gemelas junto con los datos del dispositivo Hola. valor etag del gemelas Hello, si se especifica, se procesa por separado de etag del dispositivo de Hola. Si hay una falta de coincidencia con el etag del gemelas existente de hello, se escribe un error en el archivo de registro de toohello. |
| **update** |Si ya existe un dispositivo con hello especificado **identificador**, se sobrescribe la información existente con hello proporcionada datos de entrada sin tener en cuenta toohello **ETag** valor. <br/>Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro. |
| **updateIfMatchETag** |Si ya existe un dispositivo con hello especificado **identificador**, se sobrescribe la información existente con hello proporcionada datos de entrada sólo si hay un **ETag** coincide con. <br/>Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro. <br/>Si no hay un **ETag** falta de coincidencia, se escribe el archivo de registro de toohello un error. |
| **createOrUpdateIfMatchETag** |Si no existe un dispositivo con hello especificado **identificador**, está registrado recientemente. <br/>Si ya existe un dispositivo de hello, se sobrescribe la información existente con hello proporcionada datos de entrada sólo si hay un **ETag** coincide con. <br/>Si no hay un **ETag** falta de coincidencia, se escribe el archivo de registro de toohello un error. <br> usuario de Hello, opcionalmente, puede especificar datos gemelas junto con los datos del dispositivo Hola. valor etag del gemelas Hello, si se especifica, se procesa por separado de etag del dispositivo de Hola. Si hay una falta de coincidencia con el etag del gemelas existente de hello, se escribe un error en el archivo de registro de toohello. |
| **delete** |Si ya existe un dispositivo con hello especificado **identificador**, se elimina sin tener en cuenta toohello **ETag** valor. <br/>Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro. |
| **deleteIfMatchETag** |Si ya existe un dispositivo con hello especificado **identificador**, se elimina solo si hay un **ETag** coincide con. Si el dispositivo de hello no existe, se escribe un error toohello archivo de registro. <br/>Si se produce un error de coincidencia de ETag, se escribe un error en el archivo de registro de toohello. |

> [!NOTE]
> Si no definen explícitamente los datos de serialización de hello un **importMode** marca para un dispositivo, el valor predeterminado es demasiado**createOrUpdate** Hola durante la operación de importación.

## <a name="import-devices-example--bulk-device-provisioning"></a>Ejemplo de importación de dispositivos: aprovisionamiento masivo de dispositivos

Hello siguiente ejemplo de código de C# se muestra cómo toogenerate varias identidades de dispositivos que:

* Incluyen claves de autenticación.
* Escribir ese blob en bloques dispositivo información tooa.
* Importar dispositivos Hola del registro de identidad de Hola.

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

## <a name="import-devices-example--bulk-deletion"></a>Ejemplo de importación de dispositivos: eliminación masiva

Hello ejemplo de código siguiente muestra cómo los dispositivos de hello toodelete mediante que agregó Hola ejemplo de código anterior:

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

## <a name="get-hello-container-sas-uri"></a>Obtener el contenedor de hello URI de SAS

Hello ejemplo de código siguiente muestra cómo toogenerate una [URI de SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) con lectura, escritura y eliminación de permisos para un contenedor de blobs:

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

## <a name="next-steps"></a>Pasos siguientes

En este artículo, ha aprendido cómo tooperform de forma masiva las operaciones en el registro de la identidad de hello en un centro de IoT. Siga estos toolearn de vínculos más acerca de cómo administrar el centro de IoT de Azure:

* [Métricas de IoT Hub][lnk-metrics]
* [Supervisión de operaciones][lnk-monitor]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]
* [Simular un dispositivo con IoT Edge][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
