---
title: "Habilitación del acceso de lectura público para los contenedores y blobs en Azure Blob Storage | Microsoft Docs"
description: "Obtenga información acerca de cómo permitir el acceso anónimo a contenedores y blobs y cómo tener acceso a ellos mediante programación."
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
ms.openlocfilehash: c7b83667b58649c156a62fa68cebd854c13e2cba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="37241-103">Administración del acceso de lectura anónimo a contenedores y blobs</span><span class="sxs-lookup"><span data-stu-id="37241-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="37241-104">Puede habilitar el acceso de lectura anónimo y público a un contenedor y sus blobs en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="37241-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="37241-105">Al hacerlo, puede conceder acceso de solo lectura a estos recursos sin compartir la clave de cuenta y sin necesidad de una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="37241-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="37241-106">El acceso de lectura público es mejor para escenarios donde desea que ciertos blobs estén siempre disponibles para el acceso de lectura anónimo.</span><span class="sxs-lookup"><span data-stu-id="37241-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="37241-107">Para un control más minucioso, puede crear una firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="37241-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="37241-108">Las firmas de acceso compartido le permiten proporcionar acceso restringido con distintos permisos para un período específico.</span><span class="sxs-lookup"><span data-stu-id="37241-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="37241-109">Para obtener más información sobre la creación de firmas de acceso compartido, vea [Uso de firmas de acceso compartido (SAS) en Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="37241-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="37241-110">Concesión de permisos a usuarios anónimos a contenedores y blobs</span><span class="sxs-lookup"><span data-stu-id="37241-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="37241-111">De forma predeterminada, solamente el dueño de la cuenta de almacenamiento puede obtener acceso a un contenedor y a todos los blobs en su interior.</span><span class="sxs-lookup"><span data-stu-id="37241-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="37241-112">Para dar a los usuarios anónimos permisos de lectura para un contenedor y sus blobs, puede establecer los permisos del contenedor de forma que se permita el acceso público.</span><span class="sxs-lookup"><span data-stu-id="37241-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="37241-113">Los usuarios anónimos pueden leer los blobs que estén en un contenedor con acceso público sin necesidad de tener que autenticar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="37241-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="37241-114">Puede configurar un contenedor con los permisos siguientes:</span><span class="sxs-lookup"><span data-stu-id="37241-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="37241-115">**Sin acceso de lectura público:** solo puede obtener acceso al contenedor y a sus blobs el propietario de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="37241-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="37241-116">Este es el valor predeterminado para todos los contenedores nuevos.</span><span class="sxs-lookup"><span data-stu-id="37241-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="37241-117">**Acceso de lectura público solo para blobs:** los blobs dentro del contenedor pueden leerse mediante una solicitud anónima, pero los datos del contenedor no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="37241-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="37241-118">Los clientes anónimos no pueden enumerar los blobs dentro del contenedor.</span><span class="sxs-lookup"><span data-stu-id="37241-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="37241-119">**Acceso de lectura público completo**: todos los datos del contenedor y de los blobs se pueden leer mediante una solicitud anónima.</span><span class="sxs-lookup"><span data-stu-id="37241-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="37241-120">Los clientes pueden enumerar los blobs del contenedor a través de una solicitud anónima, pero no pueden enumerar los contenedores que están en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="37241-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="37241-121">Puede usar lo siguiente para establecer permisos de contenedor:</span><span class="sxs-lookup"><span data-stu-id="37241-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="37241-122">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="37241-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="37241-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="37241-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="37241-124">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="37241-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="37241-125">Mediante programación, con una de las bibliotecas de cliente de almacenamiento o la API de REST.</span><span class="sxs-lookup"><span data-stu-id="37241-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="37241-126">Establecimiento de permisos de contenedor en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="37241-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="37241-127">Para configurar los permisos del contenedor en [Azure Portal](https://portal.azure.com), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="37241-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="37241-128">Abra la hoja **Cuenta de almacenamiento** en el portal.</span><span class="sxs-lookup"><span data-stu-id="37241-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="37241-129">Puede encontrar la cuenta de almacenamiento seleccionando **Cuentas de almacenamiento** en la hoja del menú del portal principal.</span><span class="sxs-lookup"><span data-stu-id="37241-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="37241-130">En **SERVICIO BLOB** en la hoja de menú, seleccione **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="37241-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="37241-131">Haga doble clic en la fila del contenedor o seleccione los tres puntos para abrir el **menú contextual** del contenedor.</span><span class="sxs-lookup"><span data-stu-id="37241-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="37241-132">Seleccione **Directiva de acceso** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="37241-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="37241-133">Seleccione un **tipo de acceso** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="37241-133">Select an **Access type** from the drop down menu.</span></span>

    ![Cuadro de diálogo Editar metadatos del contenedor](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="37241-135">Establecimiento de los permisos del contenedor con .NET</span><span class="sxs-lookup"><span data-stu-id="37241-135">Set container permissions with .NET</span></span>
<span data-ttu-id="37241-136">Para configurar permisos para un contenedor con C# y la Biblioteca del cliente de almacenamiento para .NET, primero recupere los permisos existentes del contenedor llamando al método **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="37241-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="37241-137">A continuación, establezca la propiedad **PublicAccess** para el objeto **BlobContainerPermissions** devuelto por el método **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="37241-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="37241-138">Por último, llame al método **SetPermissions** con los permisos actualizados.</span><span class="sxs-lookup"><span data-stu-id="37241-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="37241-139">El ejemplo siguiente establece los permisos del contenedor para el acceso de lectura público completo.</span><span class="sxs-lookup"><span data-stu-id="37241-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="37241-140">Para establecer permisos de acceso de lectura público solo para blobs, establezca la propiedad **PublicAccess** en **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="37241-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="37241-141">Para quitar todos los permisos para los usuarios anónimos, establezca la propiedad en **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="37241-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="37241-142">Acceso anónimo a contenedores y blobs</span><span class="sxs-lookup"><span data-stu-id="37241-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="37241-143">Un cliente que tiene acceso a contenedores y blobs de forma anónima puede utilizar constructores que no requieren credenciales.</span><span class="sxs-lookup"><span data-stu-id="37241-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="37241-144">En los ejemplos siguientes se muestran varias maneras diferentes de hacer referencia a recursos del servicio BLOB de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="37241-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="37241-145">Creación de un objeto de cliente anónimo</span><span class="sxs-lookup"><span data-stu-id="37241-145">Create an anonymous client object</span></span>
<span data-ttu-id="37241-146">Puede crear un nuevo objeto de cliente de servicio para el acceso anónimo proporcionando el punto de conexión del servicio BLOB para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="37241-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="37241-147">Sin embargo, también debe conocer el nombre de un contenedor en esa cuenta que esté disponible para el acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="37241-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="37241-148">Referencia a un contenedor de forma anónima</span><span class="sxs-lookup"><span data-stu-id="37241-148">Reference a container anonymously</span></span>
<span data-ttu-id="37241-149">Si tiene la dirección URL de un contenedor que está disponible de forma anónima, puede utilizarla para hacer referencia al contenedor directamente.</span><span class="sxs-lookup"><span data-stu-id="37241-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="37241-150">Referencia a un blob de forma anónima</span><span class="sxs-lookup"><span data-stu-id="37241-150">Reference a blob anonymously</span></span>
<span data-ttu-id="37241-151">Si tiene la dirección URL a un blob que está disponible para el acceso anónimo, puede hacer referencia al blob directamente con esa dirección URL:</span><span class="sxs-lookup"><span data-stu-id="37241-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="37241-152">Características disponibles para los usuarios anónimos</span><span class="sxs-lookup"><span data-stu-id="37241-152">Features available to anonymous users</span></span>
<span data-ttu-id="37241-153">En la siguiente tabla, se indican las operaciones a las que pueden llamar los usuarios anónimos cuando la ACL de un contenedor se establece para permitir un acceso público.</span><span class="sxs-lookup"><span data-stu-id="37241-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="37241-154">Operación REST</span><span class="sxs-lookup"><span data-stu-id="37241-154">REST Operation</span></span> | <span data-ttu-id="37241-155">Permiso con acceso de lectura público completo</span><span class="sxs-lookup"><span data-stu-id="37241-155">Permission with full public read access</span></span> | <span data-ttu-id="37241-156">Permiso con acceso de lectura público para solo para los blobs</span><span class="sxs-lookup"><span data-stu-id="37241-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="37241-157">List Containers</span><span class="sxs-lookup"><span data-stu-id="37241-157">List Containers</span></span> |<span data-ttu-id="37241-158">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-158">Owner only</span></span> |<span data-ttu-id="37241-159">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-159">Owner only</span></span> |
| <span data-ttu-id="37241-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="37241-160">Create Container</span></span> |<span data-ttu-id="37241-161">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-161">Owner only</span></span> |<span data-ttu-id="37241-162">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-162">Owner only</span></span> |
| <span data-ttu-id="37241-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="37241-163">Get Container Properties</span></span> |<span data-ttu-id="37241-164">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-164">All</span></span> |<span data-ttu-id="37241-165">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-165">Owner only</span></span> |
| <span data-ttu-id="37241-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="37241-166">Get Container Metadata</span></span> |<span data-ttu-id="37241-167">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-167">All</span></span> |<span data-ttu-id="37241-168">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-168">Owner only</span></span> |
| <span data-ttu-id="37241-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="37241-169">Set Container Metadata</span></span> |<span data-ttu-id="37241-170">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-170">Owner only</span></span> |<span data-ttu-id="37241-171">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-171">Owner only</span></span> |
| <span data-ttu-id="37241-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="37241-172">Get Container ACL</span></span> |<span data-ttu-id="37241-173">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-173">Owner only</span></span> |<span data-ttu-id="37241-174">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-174">Owner only</span></span> |
| <span data-ttu-id="37241-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="37241-175">Set Container ACL</span></span> |<span data-ttu-id="37241-176">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-176">Owner only</span></span> |<span data-ttu-id="37241-177">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-177">Owner only</span></span> |
| <span data-ttu-id="37241-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="37241-178">Delete Container</span></span> |<span data-ttu-id="37241-179">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-179">Owner only</span></span> |<span data-ttu-id="37241-180">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-180">Owner only</span></span> |
| <span data-ttu-id="37241-181">List Blobs</span><span class="sxs-lookup"><span data-stu-id="37241-181">List Blobs</span></span> |<span data-ttu-id="37241-182">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-182">All</span></span> |<span data-ttu-id="37241-183">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-183">Owner only</span></span> |
| <span data-ttu-id="37241-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="37241-184">Put Blob</span></span> |<span data-ttu-id="37241-185">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-185">Owner only</span></span> |<span data-ttu-id="37241-186">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-186">Owner only</span></span> |
| <span data-ttu-id="37241-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="37241-187">Get Blob</span></span> |<span data-ttu-id="37241-188">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-188">All</span></span> |<span data-ttu-id="37241-189">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-189">All</span></span> |
| <span data-ttu-id="37241-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="37241-190">Get Blob Properties</span></span> |<span data-ttu-id="37241-191">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-191">All</span></span> |<span data-ttu-id="37241-192">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-192">All</span></span> |
| <span data-ttu-id="37241-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="37241-193">Set Blob Properties</span></span> |<span data-ttu-id="37241-194">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-194">Owner only</span></span> |<span data-ttu-id="37241-195">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-195">Owner only</span></span> |
| <span data-ttu-id="37241-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="37241-196">Get Blob Metadata</span></span> |<span data-ttu-id="37241-197">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-197">All</span></span> |<span data-ttu-id="37241-198">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-198">All</span></span> |
| <span data-ttu-id="37241-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="37241-199">Set Blob Metadata</span></span> |<span data-ttu-id="37241-200">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-200">Owner only</span></span> |<span data-ttu-id="37241-201">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-201">Owner only</span></span> |
| <span data-ttu-id="37241-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="37241-202">Put Block</span></span> |<span data-ttu-id="37241-203">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-203">Owner only</span></span> |<span data-ttu-id="37241-204">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-204">Owner only</span></span> |
| <span data-ttu-id="37241-205">Get Block List (solo bloques confirmados)</span><span class="sxs-lookup"><span data-stu-id="37241-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="37241-206">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-206">All</span></span> |<span data-ttu-id="37241-207">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-207">All</span></span> |
| <span data-ttu-id="37241-208">Get Block List (solo bloques sin confirmar o todos los bloques)</span><span class="sxs-lookup"><span data-stu-id="37241-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="37241-209">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-209">Owner only</span></span> |<span data-ttu-id="37241-210">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-210">Owner only</span></span> |
| <span data-ttu-id="37241-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="37241-211">Put Block List</span></span> |<span data-ttu-id="37241-212">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-212">Owner only</span></span> |<span data-ttu-id="37241-213">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-213">Owner only</span></span> |
| <span data-ttu-id="37241-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="37241-214">Delete Blob</span></span> |<span data-ttu-id="37241-215">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-215">Owner only</span></span> |<span data-ttu-id="37241-216">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-216">Owner only</span></span> |
| <span data-ttu-id="37241-217">Copia de blobs</span><span class="sxs-lookup"><span data-stu-id="37241-217">Copy Blob</span></span> |<span data-ttu-id="37241-218">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-218">Owner only</span></span> |<span data-ttu-id="37241-219">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-219">Owner only</span></span> |
| <span data-ttu-id="37241-220">Instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="37241-220">Snapshot Blob</span></span> |<span data-ttu-id="37241-221">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-221">Owner only</span></span> |<span data-ttu-id="37241-222">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-222">Owner only</span></span> |
| <span data-ttu-id="37241-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="37241-223">Lease Blob</span></span> |<span data-ttu-id="37241-224">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-224">Owner only</span></span> |<span data-ttu-id="37241-225">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-225">Owner only</span></span> |
| <span data-ttu-id="37241-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="37241-226">Put Page</span></span> |<span data-ttu-id="37241-227">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-227">Owner only</span></span> |<span data-ttu-id="37241-228">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-228">Owner only</span></span> |
| <span data-ttu-id="37241-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="37241-229">Get Page Ranges</span></span> |<span data-ttu-id="37241-230">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-230">All</span></span> |<span data-ttu-id="37241-231">Todo</span><span class="sxs-lookup"><span data-stu-id="37241-231">All</span></span> |
| <span data-ttu-id="37241-232">Append Blob</span><span class="sxs-lookup"><span data-stu-id="37241-232">Append Blob</span></span> |<span data-ttu-id="37241-233">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-233">Owner only</span></span> |<span data-ttu-id="37241-234">Solo el propietario</span><span class="sxs-lookup"><span data-stu-id="37241-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="37241-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37241-235">Next steps</span></span>

* [<span data-ttu-id="37241-236">Autenticación para los servicios de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="37241-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="37241-237">Uso de Firmas de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="37241-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="37241-238">Delegación de acceso con una firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="37241-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)