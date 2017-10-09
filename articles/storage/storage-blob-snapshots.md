---
title: "aaaCreate una instantánea de solo lectura de un blob en el almacenamiento de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una instantánea de un tooback blob los datos de blob en un momento dado en el tiempo. Comprender cómo se facturan instantáneas y cómo toouse les toominimize cargos de capacidad."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Creación de una instantánea de un blob

Una instantánea es una versión de solo lectura de un blob que se ha realizado en un momento dado. Las instantáneas son útiles para realizar copias de seguridad de blobs. Después de crear una instantánea, puede leerla, copiarla o eliminarla, pero no puede modificarla.

Una instantánea de un blob es blob base tooits idénticas, excepto blob Hola URI tiene un **DateTime** valor anexa hora toohello blob URI tooindicate hello en qué Hola se tomó la instantánea. Por ejemplo, si el URI de blob en una página es `http://storagesample.core.blob.windows.net/mydrives/myvhd`, instantánea Hola URI es similar demasiado`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Todas las instantáneas comparten el URI del blob base Hola. Hola sólo hay distinción entre blob base Hola y Hola Hola anexado **DateTime** valor.
>

Un blob puede tener cualquier número de instantáneas. Las instantáneas se conservan hasta que se eliminen explícitamente. Una instantánea no puede durar más que su blob base. Puede enumerar instantáneas de hello asociadas Hola blob base tootrack las instantáneas actuales.

Cuando se crea una instantánea de un blob, Hola propiedades del sistema del blob son instantáneas toohello copiada con hello mismos valores. metadatos del blob base Hello también son copiada toohello instantánea, a menos que especifique metadatos independientes para hello de instantáneas al crearlo.

Las concesiones asociadas blob base hello no afectan a la instantánea de Hola. No puede adquirir una concesión en una instantánea.

Un archivo de disco duro virtual es información actual de hello toostore usado y el estado de un disco de máquina virtual. Puede separar un disco desde Hola VM o apagar Hola VM y, a continuación, tomar una instantánea de su archivo de disco duro virtual. Puede usar ese archivo de instantánea posterior tooretrieve Hola VHD en ese momento en el tiempo de archivo y vuelva a crear Hola máquina virtual.

Si está habilitado el cifrado de servicio de almacenamiento (SSE) para la cuenta de almacenamiento de hello en qué Hola reside blob y luego todas las instantáneas realizadas del blob se cifrarán en reposo.

## <a name="create-a-snapshot"></a>Crear una instantánea
Hello ejemplo de código siguiente muestra cómo toocreate una instantánea mediante el uso de Hola [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Este ejemplo especifica los metadatos adicionales para instantáneas de Hola cuando se crea.

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a>Copiar instantáneas
Las operaciones de copia con blobs e instantáneas siguen estas reglas:

* Puede copiar una instantánea sobre su blob base. Mediante la promoción de una posición de toohello instantánea del blob base hello, puede restaurar una versión anterior de un blob. Hola instantánea se conserva, pero el blob base Hola se sobrescribe con una copia modificable de la instantánea de Hola.
* Puede copiar un blob de destino tooa de instantánea con un nombre diferente. blob de destino de Hello resultante es un blob de escritura y no es una instantánea.
* Cuando se copia un blob de origen, las instantáneas de blob de origen de hello no son destino toohello copiada. Cuando un blob de destino se sobrescribe con una copia, las instantáneas asociadas al blob de destino original Hola permanecen intactas.
* Cuando se crea una instantánea de un blob en bloques, la lista de bloques confirmados del blob de hello también es instantánea toohello copiada. No se copiarán los bloques sin confirmar.

## <a name="specify-an-access-condition"></a>Especificar una condición de acceso
Cuando se llama a [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], puede especificar una condición de acceso para que hello instantánea se crea únicamente si se cumple una condición. toospecify una condición de acceso, use hello [AccessCondition] [ dotnet_AccessCondition] parámetro. Si no se cumple la condición, no se crea la instantánea de Hola y Hola servicio Blob devuelve el código de estado no especifica hello [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Eliminar instantáneas
No se puede eliminar un blob con instantáneas a menos que también se eliminan las instantáneas de Hola. Puede eliminar las instantáneas individualmente, o especificar que todas las instantáneas se elimina cuando se elimina el blob de origen Hola. Si intentas toodelete un blob que todavía tiene instantáneas, se producirá un error.

Hola siguiendo el ejemplo de código muestra cómo toodelete un blob y sus instantáneas en. NET, donde `blockBlob` es un objeto de tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Instantáneas con Almacenamiento Premium de Azure
Cuando utilice instantáneas con almacenamiento Premium, se aplica Hola siguientes reglas:

* Hola número máximo de instantáneas por blob en páginas en una cuenta de almacenamiento premium es 100. Si se supera dicho límite, Hola operación de instantánea Blob devuelve el código de error 409 (`SnapshotCountExceeded`).
* Puede tomar una instantánea de un blob en páginas en una cuenta de almacenamiento premium cada 10 minutos. Si se supera la tasa, Hola operación de instantánea Blob devuelve el código de error 409 (`SnapshotOperationRateExceeded`).
* tooread una instantánea, puede usar Hola Copy Blob operación toocopy un blob en páginas tooanother instantánea en la cuenta de hello. blob de destino de Hello para la operación de copia de hello no debe tener las instantáneas existentes. Si Hola blob de destino tiene instantáneas, Hola operación Copy Blob devuelve el código de error 409 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Instantánea de tooa URI absoluto Hola devuelto
Este ejemplo de código de C# crea una instantánea y escribe Hola URI absoluto para la ubicación principal Hola.

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>Descripción de cómo las instantáneas pueden incrementar los costes
Crear una instantánea, que es una copia de solo lectura de un blob, puede dar lugar a cuenta de tooyour de gastos de almacenamiento de datos adicionales. Al diseñar la aplicación, es importante toobe consciente de cómo podrían acumular estos cargos por lo que puede reducir los costos.

### <a name="important-billing-considerations"></a>Consideraciones importantes sobre facturación
Hola lista siguiente incluye puntos clave tooconsider al crear una instantánea.

* La cuenta de almacenamiento incurre en cargos por si hay bloques únicos o páginas, independientemente de si están en blob de Hola o de instantánea de Hola. Su cuenta no incurre en gastos adicionales para instantáneas asociadas a un blob hasta que actualice el blob de hello en el que se basan. Después de actualizar el blob base hello, divergirá respecto a sus instantáneas. Cuando esto sucede, se le cobra por hello bloques o páginas únicos en cada blob o una instantánea.
* Al reemplazar un bloque en un blob en bloques, ese bloque será considerado como un bloque único a la hora de aplicar cargos. Esto es cierto incluso si el bloque de hello tiene Hola mismo identificador de bloque y Hola mismo datos tal como se ha de instantánea de Hola. Cuando se confirma el bloque de hello, divergirá respecto a su equivalente en la instantánea y le cobrará por sus datos. Hola que mismo es aplicable para una página en un blob en páginas que se actualiza con datos idénticos.
* Reemplazar un blob en bloques por llamada hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] método reemplaza todos los bloques en el blob de Hola. Si tiene una instantánea asociada a ese blob, todos los bloques en el blob base hello y la instantánea ahora distinguir y le cobrará por todos los bloques de hello en ambos blobs. Esto es cierto incluso si los datos de hello en blob de base de Hola y de instantánea de hello siguen siendo idénticos.
* Hola servicio Blob de Azure no tiene un toodetermine significa que si dos bloques contienen datos idénticos. Cada bloque al que se carga y confirma se trata como único, incluso si ha Hola mismo hello y datos bloquear el mismo Id. Dado que cargas se incrementan con los bloques únicos, es importante tooconsider actualiza un blob con una instantánea resultante en bloques únicos adicionales y cargos adicionales.

### <a name="minimize-cost-with-snapshot-management"></a>Minimización del costo con la administración de instantáneas

Se recomienda administrar cuidadosamente las instantáneas tooavoid cargos adicionales. Puede seguir estas prácticas recomendadas toohelp minimizar los costes de hello producidos por el almacenamiento de Hola de las instantáneas:

* Eliminar y volver a crear las instantáneas asociadas a un blob cada vez que actualice el blob de hello, incluso si va a actualizar con datos idénticos, a menos que el diseño de aplicaciones requiere que se conserven las instantáneas. Si elimina y vuelve a crear instantáneas del blob de hello, puede asegurarse de que las instantáneas y blobs de hello no van a divergir.
* Si está realizando el mantenimiento de instantáneas para un blob, evite llamar a [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate blob de Hola. Estos métodos reemplazan todos los bloques de hello en blob de hello, haciendo que el blob base y su toodiverge instantáneas significativamente. En su lugar, la actualización Hola menor número posible de bloques mediante el uso de Hola [PutBlock] [ dotnet_PutBlock] y [PutBlockList] [ dotnet_PutBlockList] métodos.

### <a name="snapshot-billing-scenarios"></a>Escenarios de facturación de instantáneas
Hola los escenarios siguientes demuestran cómo cargas se incrementan para un blob en bloques y sus instantáneas.

**Escenario 1**

En el escenario 1, blob base hello no se actualizó después de que se tomó la instantánea de hello, por lo que los cargos se generan solo para bloques únicos 1, 2 y 3.

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Escenario 2**

En el escenario 2, se ha actualizado el blob base hello, pero instantánea hello no. Bloque 3 se actualizó y, aunque contenga Hola los mismos datos y Hola el mismo Id., es no Hola igual que el bloque 3 en instantánea Hola. Como resultado, la cuenta de hello se cobra por cuatro bloques.

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Escenario 3**

En el escenario 3, se ha actualizado el blob base hello, pero instantánea hello no. Bloque 3 se ha reemplazado por el bloque 4 en blob de base de hello, pero instantánea Hola sigue reflejando el bloque 3. Como resultado, la cuenta de hello se cobra por cuatro bloques.

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Escenario 4**

En el escenario 4, blob base Hola se ha actualizado por completo y no contiene ninguno de los bloques originales. Como resultado, la cuenta de hello se cobra por todos los ocho bloques únicos. Esta situación puede producirse si usa un método de actualización como [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray][dotnet_UploadFromByteArray], ya que estos métodos reemplazan la totalidad de contenido de Hola de un blob.

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Pasos siguientes

* Puede encontrar más información acerca de cómo trabajar con instantáneas de discos de máquina virtuales (VM) en [Copias de seguridad de discos de máquinas virtuales de Azure no administrados con instantáneas incrementales](storage-incremental-snapshots.md)

* Para obtener más ejemplos de código que usa Blob Storage, consulte [Ejemplos de código de Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Puede descargar una aplicación de ejemplo y ejecutarlo o examinar el código de hello en GitHub.

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx