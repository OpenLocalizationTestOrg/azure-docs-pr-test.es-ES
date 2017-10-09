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
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="5d7c3-104">Creación de una instantánea de un blob</span><span class="sxs-lookup"><span data-stu-id="5d7c3-104">Create a blob snapshot</span></span>

<span data-ttu-id="5d7c3-105">Una instantánea es una versión de solo lectura de un blob que se ha realizado en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="5d7c3-106">Las instantáneas son útiles para realizar copias de seguridad de blobs.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="5d7c3-107">Después de crear una instantánea, puede leerla, copiarla o eliminarla, pero no puede modificarla.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="5d7c3-108">Una instantánea de un blob es blob base tooits idénticas, excepto blob Hola URI tiene un **DateTime** valor anexa hora toohello blob URI tooindicate hello en qué Hola se tomó la instantánea.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="5d7c3-109">Por ejemplo, si el URI de blob en una página es `http://storagesample.core.blob.windows.net/mydrives/myvhd`, instantánea Hola URI es similar demasiado`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="5d7c3-110">Todas las instantáneas comparten el URI del blob base Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="5d7c3-111">Hola sólo hay distinción entre blob base Hola y Hola Hola anexado **DateTime** valor.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="5d7c3-112">Un blob puede tener cualquier número de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="5d7c3-113">Las instantáneas se conservan hasta que se eliminen explícitamente.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="5d7c3-114">Una instantánea no puede durar más que su blob base.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="5d7c3-115">Puede enumerar instantáneas de hello asociadas Hola blob base tootrack las instantáneas actuales.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="5d7c3-116">Cuando se crea una instantánea de un blob, Hola propiedades del sistema del blob son instantáneas toohello copiada con hello mismos valores.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="5d7c3-117">metadatos del blob base Hello también son copiada toohello instantánea, a menos que especifique metadatos independientes para hello de instantáneas al crearlo.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="5d7c3-118">Las concesiones asociadas blob base hello no afectan a la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="5d7c3-119">No puede adquirir una concesión en una instantánea.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="5d7c3-120">Un archivo de disco duro virtual es información actual de hello toostore usado y el estado de un disco de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="5d7c3-121">Puede separar un disco desde Hola VM o apagar Hola VM y, a continuación, tomar una instantánea de su archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="5d7c3-122">Puede usar ese archivo de instantánea posterior tooretrieve Hola VHD en ese momento en el tiempo de archivo y vuelva a crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="5d7c3-123">Si está habilitado el cifrado de servicio de almacenamiento (SSE) para la cuenta de almacenamiento de hello en qué Hola reside blob y luego todas las instantáneas realizadas del blob se cifrarán en reposo.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="5d7c3-124">Crear una instantánea</span><span class="sxs-lookup"><span data-stu-id="5d7c3-124">Create a snapshot</span></span>
<span data-ttu-id="5d7c3-125">Hello ejemplo de código siguiente muestra cómo toocreate una instantánea mediante el uso de Hola [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="5d7c3-126">Este ejemplo especifica los metadatos adicionales para instantáneas de Hola cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

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

## <a name="copy-snapshots"></a><span data-ttu-id="5d7c3-127">Copiar instantáneas</span><span class="sxs-lookup"><span data-stu-id="5d7c3-127">Copy snapshots</span></span>
<span data-ttu-id="5d7c3-128">Las operaciones de copia con blobs e instantáneas siguen estas reglas:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="5d7c3-129">Puede copiar una instantánea sobre su blob base.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="5d7c3-130">Mediante la promoción de una posición de toohello instantánea del blob base hello, puede restaurar una versión anterior de un blob.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="5d7c3-131">Hola instantánea se conserva, pero el blob base Hola se sobrescribe con una copia modificable de la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="5d7c3-132">Puede copiar un blob de destino tooa de instantánea con un nombre diferente.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="5d7c3-133">blob de destino de Hello resultante es un blob de escritura y no es una instantánea.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="5d7c3-134">Cuando se copia un blob de origen, las instantáneas de blob de origen de hello no son destino toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="5d7c3-135">Cuando un blob de destino se sobrescribe con una copia, las instantáneas asociadas al blob de destino original Hola permanecen intactas.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="5d7c3-136">Cuando se crea una instantánea de un blob en bloques, la lista de bloques confirmados del blob de hello también es instantánea toohello copiada.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="5d7c3-137">No se copiarán los bloques sin confirmar.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="5d7c3-138">Especificar una condición de acceso</span><span class="sxs-lookup"><span data-stu-id="5d7c3-138">Specify an access condition</span></span>
<span data-ttu-id="5d7c3-139">Cuando se llama a [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], puede especificar una condición de acceso para que hello instantánea se crea únicamente si se cumple una condición.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="5d7c3-140">toospecify una condición de acceso, use hello [AccessCondition] [ dotnet_AccessCondition] parámetro.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="5d7c3-141">Si no se cumple la condición, no se crea la instantánea de Hola y Hola servicio Blob devuelve el código de estado no especifica hello [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="5d7c3-142">Eliminar instantáneas</span><span class="sxs-lookup"><span data-stu-id="5d7c3-142">Delete snapshots</span></span>
<span data-ttu-id="5d7c3-143">No se puede eliminar un blob con instantáneas a menos que también se eliminan las instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="5d7c3-144">Puede eliminar las instantáneas individualmente, o especificar que todas las instantáneas se elimina cuando se elimina el blob de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="5d7c3-145">Si intentas toodelete un blob que todavía tiene instantáneas, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="5d7c3-146">Hola siguiendo el ejemplo de código muestra cómo toodelete un blob y sus instantáneas en. NET, donde `blockBlob` es un objeto de tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="5d7c3-147">Instantáneas con Almacenamiento Premium de Azure</span><span class="sxs-lookup"><span data-stu-id="5d7c3-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="5d7c3-148">Cuando utilice instantáneas con almacenamiento Premium, se aplica Hola siguientes reglas:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="5d7c3-149">Hola número máximo de instantáneas por blob en páginas en una cuenta de almacenamiento premium es 100.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="5d7c3-150">Si se supera dicho límite, Hola operación de instantánea Blob devuelve el código de error 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="5d7c3-151">Puede tomar una instantánea de un blob en páginas en una cuenta de almacenamiento premium cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="5d7c3-152">Si se supera la tasa, Hola operación de instantánea Blob devuelve el código de error 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="5d7c3-153">tooread una instantánea, puede usar Hola Copy Blob operación toocopy un blob en páginas tooanother instantánea en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="5d7c3-154">blob de destino de Hello para la operación de copia de hello no debe tener las instantáneas existentes.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="5d7c3-155">Si Hola blob de destino tiene instantáneas, Hola operación Copy Blob devuelve el código de error 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="5d7c3-156">Instantánea de tooa URI absoluto Hola devuelto</span><span class="sxs-lookup"><span data-stu-id="5d7c3-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="5d7c3-157">Este ejemplo de código de C# crea una instantánea y escribe Hola URI absoluto para la ubicación principal Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

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

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="5d7c3-158">Descripción de cómo las instantáneas pueden incrementar los costes</span><span class="sxs-lookup"><span data-stu-id="5d7c3-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="5d7c3-159">Crear una instantánea, que es una copia de solo lectura de un blob, puede dar lugar a cuenta de tooyour de gastos de almacenamiento de datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="5d7c3-160">Al diseñar la aplicación, es importante toobe consciente de cómo podrían acumular estos cargos por lo que puede reducir los costos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="5d7c3-161">Consideraciones importantes sobre facturación</span><span class="sxs-lookup"><span data-stu-id="5d7c3-161">Important billing considerations</span></span>
<span data-ttu-id="5d7c3-162">Hola lista siguiente incluye puntos clave tooconsider al crear una instantánea.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="5d7c3-163">La cuenta de almacenamiento incurre en cargos por si hay bloques únicos o páginas, independientemente de si están en blob de Hola o de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="5d7c3-164">Su cuenta no incurre en gastos adicionales para instantáneas asociadas a un blob hasta que actualice el blob de hello en el que se basan.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="5d7c3-165">Después de actualizar el blob base hello, divergirá respecto a sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="5d7c3-166">Cuando esto sucede, se le cobra por hello bloques o páginas únicos en cada blob o una instantánea.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="5d7c3-167">Al reemplazar un bloque en un blob en bloques, ese bloque será considerado como un bloque único a la hora de aplicar cargos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="5d7c3-168">Esto es cierto incluso si el bloque de hello tiene Hola mismo identificador de bloque y Hola mismo datos tal como se ha de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="5d7c3-169">Cuando se confirma el bloque de hello, divergirá respecto a su equivalente en la instantánea y le cobrará por sus datos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="5d7c3-170">Hola que mismo es aplicable para una página en un blob en páginas que se actualiza con datos idénticos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="5d7c3-171">Reemplazar un blob en bloques por llamada hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] método reemplaza todos los bloques en el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="5d7c3-172">Si tiene una instantánea asociada a ese blob, todos los bloques en el blob base hello y la instantánea ahora distinguir y le cobrará por todos los bloques de hello en ambos blobs.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="5d7c3-173">Esto es cierto incluso si los datos de hello en blob de base de Hola y de instantánea de hello siguen siendo idénticos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="5d7c3-174">Hola servicio Blob de Azure no tiene un toodetermine significa que si dos bloques contienen datos idénticos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="5d7c3-175">Cada bloque al que se carga y confirma se trata como único, incluso si ha Hola mismo hello y datos bloquear el mismo Id.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="5d7c3-176">Dado que cargas se incrementan con los bloques únicos, es importante tooconsider actualiza un blob con una instantánea resultante en bloques únicos adicionales y cargos adicionales.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="5d7c3-177">Minimización del costo con la administración de instantáneas</span><span class="sxs-lookup"><span data-stu-id="5d7c3-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="5d7c3-178">Se recomienda administrar cuidadosamente las instantáneas tooavoid cargos adicionales.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="5d7c3-179">Puede seguir estas prácticas recomendadas toohelp minimizar los costes de hello producidos por el almacenamiento de Hola de las instantáneas:</span><span class="sxs-lookup"><span data-stu-id="5d7c3-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="5d7c3-180">Eliminar y volver a crear las instantáneas asociadas a un blob cada vez que actualice el blob de hello, incluso si va a actualizar con datos idénticos, a menos que el diseño de aplicaciones requiere que se conserven las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="5d7c3-181">Si elimina y vuelve a crear instantáneas del blob de hello, puede asegurarse de que las instantáneas y blobs de hello no van a divergir.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="5d7c3-182">Si está realizando el mantenimiento de instantáneas para un blob, evite llamar a [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="5d7c3-183">Estos métodos reemplazan todos los bloques de hello en blob de hello, haciendo que el blob base y su toodiverge instantáneas significativamente.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="5d7c3-184">En su lugar, la actualización Hola menor número posible de bloques mediante el uso de Hola [PutBlock] [ dotnet_PutBlock] y [PutBlockList] [ dotnet_PutBlockList] métodos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="5d7c3-185">Escenarios de facturación de instantáneas</span><span class="sxs-lookup"><span data-stu-id="5d7c3-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="5d7c3-186">Hola los escenarios siguientes demuestran cómo cargas se incrementan para un blob en bloques y sus instantáneas.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="5d7c3-187">**Escenario 1**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-187">**Scenario 1**</span></span>

<span data-ttu-id="5d7c3-188">En el escenario 1, blob base hello no se actualizó después de que se tomó la instantánea de hello, por lo que los cargos se generan solo para bloques únicos 1, 2 y 3.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="5d7c3-190">**Escenario 2**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-190">**Scenario 2**</span></span>

<span data-ttu-id="5d7c3-191">En el escenario 2, se ha actualizado el blob base hello, pero instantánea hello no.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="5d7c3-192">Bloque 3 se actualizó y, aunque contenga Hola los mismos datos y Hola el mismo Id., es no Hola igual que el bloque 3 en instantánea Hola.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="5d7c3-193">Como resultado, la cuenta de hello se cobra por cuatro bloques.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-193">As a result, hello account is charged for four blocks.</span></span>

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="5d7c3-195">**Escenario 3**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-195">**Scenario 3**</span></span>

<span data-ttu-id="5d7c3-196">En el escenario 3, se ha actualizado el blob base hello, pero instantánea hello no.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="5d7c3-197">Bloque 3 se ha reemplazado por el bloque 4 en blob de base de hello, pero instantánea Hola sigue reflejando el bloque 3.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="5d7c3-198">Como resultado, la cuenta de hello se cobra por cuatro bloques.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-198">As a result, hello account is charged for four blocks.</span></span>

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="5d7c3-200">**Escenario 4**</span><span class="sxs-lookup"><span data-stu-id="5d7c3-200">**Scenario 4**</span></span>

<span data-ttu-id="5d7c3-201">En el escenario 4, blob base Hola se ha actualizado por completo y no contiene ninguno de los bloques originales.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="5d7c3-202">Como resultado, la cuenta de hello se cobra por todos los ocho bloques únicos.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="5d7c3-203">Esta situación puede producirse si usa un método de actualización como [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], o [UploadFromByteArray][dotnet_UploadFromByteArray], ya que estos métodos reemplazan la totalidad de contenido de Hola de un blob.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Recursos de almacenamiento de Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="5d7c3-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d7c3-205">Next steps</span></span>

* <span data-ttu-id="5d7c3-206">Puede encontrar más información acerca de cómo trabajar con instantáneas de discos de máquina virtuales (VM) en [Copias de seguridad de discos de máquinas virtuales de Azure no administrados con instantáneas incrementales](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="5d7c3-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="5d7c3-207">Para obtener más ejemplos de código que usa Blob Storage, consulte [Ejemplos de código de Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="5d7c3-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="5d7c3-208">Puede descargar una aplicación de ejemplo y ejecutarlo o examinar el código de hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d7c3-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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