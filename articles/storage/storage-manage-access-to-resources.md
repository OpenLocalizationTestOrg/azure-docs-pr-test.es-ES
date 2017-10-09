---
title: "acceso aaaEnable público de lectura para los contenedores y blobs en almacenamiento de blobs de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomake contenedores y blobs disponibles para el acceso anónimo y cómo tooaccess ellos mediante programación."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="23b6f-103">Administrar blobs y acceso de lectura anónimo toocontainers</span><span class="sxs-lookup"><span data-stu-id="23b6f-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="23b6f-104">Puede habilitar el acceso de lectura anónimo y público tooa contenedor y sus blobs en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="23b6f-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="23b6f-105">Al hacerlo, puede conceder acceso de solo lectura a los recursos de toothese sin compartir la clave de cuenta y sin necesidad de una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="23b6f-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="23b6f-106">Acceso de lectura público es mejor para escenarios donde desea que ciertas blobs tooalways esté disponible para el acceso de lectura anónimo.</span><span class="sxs-lookup"><span data-stu-id="23b6f-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="23b6f-107">Para un control más minucioso, puede crear una firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="23b6f-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="23b6f-108">Firmas de acceso compartido le permiten acceso tooprovide restringido mediante permisos diferentes, durante un período de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="23b6f-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="23b6f-109">Para obtener más información sobre la creación de firmas de acceso compartido, vea [Uso de firmas de acceso compartido (SAS) en Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="23b6f-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="23b6f-110">Conceder a los usuarios anónimos permisos toocontainers y blobs</span><span class="sxs-lookup"><span data-stu-id="23b6f-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="23b6f-111">De forma predeterminada, un contenedor y cualquiera de sus blobs puede tener acceso a solo el propietario Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="23b6f-112">contenedor de tooa de permisos de lectura de los usuarios anónimos toogive y sus blobs, puede establecer Hola permisos tooallow público el acceso al contenedor.</span><span class="sxs-lookup"><span data-stu-id="23b6f-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="23b6f-113">Los usuarios anónimos pueden leer los blobs dentro de un contenedor es accesible públicamente sin autenticar la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="23b6f-114">Puede configurar un contenedor con hello los siguientes permisos:</span><span class="sxs-lookup"><span data-stu-id="23b6f-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="23b6f-115">**Acceso no público de lectura:** Hola contenedor y sus blobs son accesibles solo por propietario hello de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="23b6f-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="23b6f-116">Éste es Hola predeterminado para todos los contenedores nuevo.</span><span class="sxs-lookup"><span data-stu-id="23b6f-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="23b6f-117">**Acceso solo para blobs público de lectura:** Blobs de hello contenedor pueden leerse mediante una solicitud anónima, pero los datos del contenedor no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="23b6f-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="23b6f-118">Los clientes anónimos no pueden enumerar blobs de hello en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="23b6f-119">**Acceso de lectura público completo**: todos los datos del contenedor y de los blobs se pueden leer mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="23b6f-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="23b6f-120">Los clientes pueden enumerar blobs en el contenedor de Hola por una solicitud anónima, pero no pueden enumerar contenedores dentro de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="23b6f-121">Puede usar los siguientes permisos del contenedor de tooset de Hola:</span><span class="sxs-lookup"><span data-stu-id="23b6f-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="23b6f-122">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23b6f-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="23b6f-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="23b6f-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="23b6f-124">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="23b6f-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="23b6f-125">Mediante programación, mediante una de las bibliotecas de cliente de almacenamiento de Hola o hello API de REST</span><span class="sxs-lookup"><span data-stu-id="23b6f-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="23b6f-126">Establecer permisos del contenedor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23b6f-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="23b6f-127">permisos del contenedor tooset Hola [portal de Azure](https://portal.azure.com), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="23b6f-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="23b6f-128">Abra su **cuenta de almacenamiento** hoja en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="23b6f-129">Puede encontrar la cuenta de almacenamiento seleccionando **cuentas de almacenamiento** en la hoja de menús del portal principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="23b6f-130">En **servicio BLOB** en la hoja de menú de hello, seleccione **contenedores**.</span><span class="sxs-lookup"><span data-stu-id="23b6f-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="23b6f-131">Haga doble clic en la fila de contenedor de Hola o del contenedor de Hola de hello seleccione puntos suspensivos tooopen **menú contextual**.</span><span class="sxs-lookup"><span data-stu-id="23b6f-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="23b6f-132">Seleccione **directiva de acceso** en el menú contextual de Hola.</span><span class="sxs-lookup"><span data-stu-id="23b6f-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="23b6f-133">Seleccione un **tipo de acceso** de hello menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="23b6f-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Cuadro de diálogo Editar metadatos del contenedor](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="23b6f-135">Establecimiento de los permisos del contenedor con .NET</span><span class="sxs-lookup"><span data-stu-id="23b6f-135">Set container permissions with .NET</span></span>
<span data-ttu-id="23b6f-136">tooset permisos para un contenedor con C# y Hola biblioteca cliente de almacenamiento para. NET, en primer lugar recuperar los permisos existentes del contenedor de Hola Hola llamada **GetPermissions** método.</span><span class="sxs-lookup"><span data-stu-id="23b6f-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="23b6f-137">Hola de conjunto, a continuación, **PublicAccess** propiedad hello **BlobContainerPermissions** objeto devuelto por hello **GetPermissions** método.</span><span class="sxs-lookup"><span data-stu-id="23b6f-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="23b6f-138">Por último, llame hello **SetPermissions** método con hello actualiza permisos.</span><span class="sxs-lookup"><span data-stu-id="23b6f-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="23b6f-139">Hola siguiente ejemplo establece permisos del contenedor de hello toofull acceso de lectura público.</span><span class="sxs-lookup"><span data-stu-id="23b6f-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="23b6f-140">acceso de lectura de tooset permisos toopublic para blobs únicamente, establecer hello **PublicAccess** propiedad demasiado**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="23b6f-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="23b6f-141">conjunto de todos los permisos para usuarios anónimos, tooremove Hola propiedad demasiado**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="23b6f-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="23b6f-142">Acceso anónimo a contenedores y blobs</span><span class="sxs-lookup"><span data-stu-id="23b6f-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="23b6f-143">Un cliente que tiene acceso a contenedores y blobs de forma anónima puede utilizar constructores que no requieren credenciales.</span><span class="sxs-lookup"><span data-stu-id="23b6f-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="23b6f-144">Hello en los ejemplos siguientes muestra algunas formas distintas de recursos del servicio Blob tooreference forma anónima.</span><span class="sxs-lookup"><span data-stu-id="23b6f-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="23b6f-145">Creación de un objeto de cliente anónimo</span><span class="sxs-lookup"><span data-stu-id="23b6f-145">Create an anonymous client object</span></span>
<span data-ttu-id="23b6f-146">Puede crear un nuevo objeto de cliente de servicio para el acceso anónimo al proporcionar extremo del servicio de Blob de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="23b6f-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="23b6f-147">Sin embargo, también debe conocer el nombre de Hola de un contenedor en esa cuenta a la que está disponible para el acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="23b6f-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="23b6f-148">Referencia a un contenedor de forma anónima</span><span class="sxs-lookup"><span data-stu-id="23b6f-148">Reference a container anonymously</span></span>
<span data-ttu-id="23b6f-149">Si tiene un contenedor de tooa de dirección URL de Hola que está disponible de forma anónima, utilizarla contenedor de hello tooreference directamente.</span><span class="sxs-lookup"><span data-stu-id="23b6f-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="23b6f-150">Referencia a un blob de forma anónima</span><span class="sxs-lookup"><span data-stu-id="23b6f-150">Reference a blob anonymously</span></span>
<span data-ttu-id="23b6f-151">Si dispone de blob de tooa de dirección URL de Hola que está disponible para el acceso anónimo, puede hacer referencia directamente con esa dirección URL de blob de hello:</span><span class="sxs-lookup"><span data-stu-id="23b6f-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="23b6f-152">Funciones que los usuarios tooanonymous disponibles</span><span class="sxs-lookup"><span data-stu-id="23b6f-152">Features available tooanonymous users</span></span>
<span data-ttu-id="23b6f-153">Hello en la tabla siguiente muestra qué operaciones pueden ser llamadas por los usuarios anónimos cuando ACL del contenedor se establece el acceso público de tooallow.</span><span class="sxs-lookup"><span data-stu-id="23b6f-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="23b6f-154">Operación REST</span><span class="sxs-lookup"><span data-stu-id="23b6f-154">REST Operation</span></span> | <span data-ttu-id="23b6f-155">Permiso con acceso de lectura público completo</span><span class="sxs-lookup"><span data-stu-id="23b6f-155">Permission with full public read access</span></span> | <span data-ttu-id="23b6f-156">Permiso con acceso de lectura público para solo para los blobs</span><span class="sxs-lookup"><span data-stu-id="23b6f-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23b6f-157">List Containers</span><span class="sxs-lookup"><span data-stu-id="23b6f-157">List Containers</span></span> |<span data-ttu-id="23b6f-158">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-158">Owner only</span></span> |<span data-ttu-id="23b6f-159">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-159">Owner only</span></span> |
| <span data-ttu-id="23b6f-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="23b6f-160">Create Container</span></span> |<span data-ttu-id="23b6f-161">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-161">Owner only</span></span> |<span data-ttu-id="23b6f-162">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-162">Owner only</span></span> |
| <span data-ttu-id="23b6f-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="23b6f-163">Get Container Properties</span></span> |<span data-ttu-id="23b6f-164">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-164">All</span></span> |<span data-ttu-id="23b6f-165">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-165">Owner only</span></span> |
| <span data-ttu-id="23b6f-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="23b6f-166">Get Container Metadata</span></span> |<span data-ttu-id="23b6f-167">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-167">All</span></span> |<span data-ttu-id="23b6f-168">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-168">Owner only</span></span> |
| <span data-ttu-id="23b6f-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="23b6f-169">Set Container Metadata</span></span> |<span data-ttu-id="23b6f-170">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-170">Owner only</span></span> |<span data-ttu-id="23b6f-171">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-171">Owner only</span></span> |
| <span data-ttu-id="23b6f-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="23b6f-172">Get Container ACL</span></span> |<span data-ttu-id="23b6f-173">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-173">Owner only</span></span> |<span data-ttu-id="23b6f-174">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-174">Owner only</span></span> |
| <span data-ttu-id="23b6f-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="23b6f-175">Set Container ACL</span></span> |<span data-ttu-id="23b6f-176">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-176">Owner only</span></span> |<span data-ttu-id="23b6f-177">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-177">Owner only</span></span> |
| <span data-ttu-id="23b6f-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="23b6f-178">Delete Container</span></span> |<span data-ttu-id="23b6f-179">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-179">Owner only</span></span> |<span data-ttu-id="23b6f-180">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-180">Owner only</span></span> |
| <span data-ttu-id="23b6f-181">List Blobs</span><span class="sxs-lookup"><span data-stu-id="23b6f-181">List Blobs</span></span> |<span data-ttu-id="23b6f-182">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-182">All</span></span> |<span data-ttu-id="23b6f-183">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-183">Owner only</span></span> |
| <span data-ttu-id="23b6f-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="23b6f-184">Put Blob</span></span> |<span data-ttu-id="23b6f-185">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-185">Owner only</span></span> |<span data-ttu-id="23b6f-186">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-186">Owner only</span></span> |
| <span data-ttu-id="23b6f-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="23b6f-187">Get Blob</span></span> |<span data-ttu-id="23b6f-188">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-188">All</span></span> |<span data-ttu-id="23b6f-189">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-189">All</span></span> |
| <span data-ttu-id="23b6f-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="23b6f-190">Get Blob Properties</span></span> |<span data-ttu-id="23b6f-191">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-191">All</span></span> |<span data-ttu-id="23b6f-192">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-192">All</span></span> |
| <span data-ttu-id="23b6f-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="23b6f-193">Set Blob Properties</span></span> |<span data-ttu-id="23b6f-194">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-194">Owner only</span></span> |<span data-ttu-id="23b6f-195">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-195">Owner only</span></span> |
| <span data-ttu-id="23b6f-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="23b6f-196">Get Blob Metadata</span></span> |<span data-ttu-id="23b6f-197">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-197">All</span></span> |<span data-ttu-id="23b6f-198">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-198">All</span></span> |
| <span data-ttu-id="23b6f-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="23b6f-199">Set Blob Metadata</span></span> |<span data-ttu-id="23b6f-200">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-200">Owner only</span></span> |<span data-ttu-id="23b6f-201">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-201">Owner only</span></span> |
| <span data-ttu-id="23b6f-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="23b6f-202">Put Block</span></span> |<span data-ttu-id="23b6f-203">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-203">Owner only</span></span> |<span data-ttu-id="23b6f-204">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-204">Owner only</span></span> |
| <span data-ttu-id="23b6f-205">Get Block List (solo bloques confirmados)</span><span class="sxs-lookup"><span data-stu-id="23b6f-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="23b6f-206">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-206">All</span></span> |<span data-ttu-id="23b6f-207">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-207">All</span></span> |
| <span data-ttu-id="23b6f-208">Get Block List (solo bloques sin confirmar o todos los bloques)</span><span class="sxs-lookup"><span data-stu-id="23b6f-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="23b6f-209">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-209">Owner only</span></span> |<span data-ttu-id="23b6f-210">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-210">Owner only</span></span> |
| <span data-ttu-id="23b6f-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="23b6f-211">Put Block List</span></span> |<span data-ttu-id="23b6f-212">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-212">Owner only</span></span> |<span data-ttu-id="23b6f-213">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-213">Owner only</span></span> |
| <span data-ttu-id="23b6f-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="23b6f-214">Delete Blob</span></span> |<span data-ttu-id="23b6f-215">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-215">Owner only</span></span> |<span data-ttu-id="23b6f-216">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-216">Owner only</span></span> |
| <span data-ttu-id="23b6f-217">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="23b6f-217">Copy Blob</span></span> |<span data-ttu-id="23b6f-218">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-218">Owner only</span></span> |<span data-ttu-id="23b6f-219">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-219">Owner only</span></span> |
| <span data-ttu-id="23b6f-220">Instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="23b6f-220">Snapshot Blob</span></span> |<span data-ttu-id="23b6f-221">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-221">Owner only</span></span> |<span data-ttu-id="23b6f-222">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-222">Owner only</span></span> |
| <span data-ttu-id="23b6f-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="23b6f-223">Lease Blob</span></span> |<span data-ttu-id="23b6f-224">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-224">Owner only</span></span> |<span data-ttu-id="23b6f-225">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-225">Owner only</span></span> |
| <span data-ttu-id="23b6f-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="23b6f-226">Put Page</span></span> |<span data-ttu-id="23b6f-227">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-227">Owner only</span></span> |<span data-ttu-id="23b6f-228">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-228">Owner only</span></span> |
| <span data-ttu-id="23b6f-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="23b6f-229">Get Page Ranges</span></span> |<span data-ttu-id="23b6f-230">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-230">All</span></span> |<span data-ttu-id="23b6f-231">Todo</span><span class="sxs-lookup"><span data-stu-id="23b6f-231">All</span></span> |
| <span data-ttu-id="23b6f-232">Append Blob</span><span class="sxs-lookup"><span data-stu-id="23b6f-232">Append Blob</span></span> |<span data-ttu-id="23b6f-233">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-233">Owner only</span></span> |<span data-ttu-id="23b6f-234">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="23b6f-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23b6f-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23b6f-235">Next steps</span></span>

* [<span data-ttu-id="23b6f-236">Autenticación de hello servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="23b6f-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="23b6f-237">Uso de Firmas de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="23b6f-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="23b6f-238">Delegación de acceso con una firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="23b6f-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
