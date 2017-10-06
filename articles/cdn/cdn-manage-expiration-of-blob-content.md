---
title: "expiración de aaaManage de blobs de almacenamiento de Azure en red CDN de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las opciones de Hola para controlar el período de vida para los blobs en almacenamiento en caché de CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="64f7a-103">Administración de la expiración de Azure Storage Blob en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="64f7a-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64f7a-104">Azure Web Apps/Cloud Services, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="64f7a-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="64f7a-105">Azure Storage Blob service</span><span class="sxs-lookup"><span data-stu-id="64f7a-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="64f7a-106">Hola [servicio blob](../storage/common/storage-introduction.md#blob-storage) en [el almacenamiento de Azure](../storage/common/storage-introduction.md) uno de varios orígenes basado en Azure se integra con la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="64f7a-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="64f7a-107">Cualquier contenido de blob accesible públicamente se puede almacenar en caché en la red CDN de Azure hasta que transcurra su tiempo de vida (TTL).</span><span class="sxs-lookup"><span data-stu-id="64f7a-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="64f7a-108">Hello TTL determina hello [ *Cache-Control* encabezado](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en respuesta Hola HTTP desde el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="64f7a-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="64f7a-109">No puede elegir tooset ningún período de vida de un blob.</span><span class="sxs-lookup"><span data-stu-id="64f7a-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="64f7a-110">En este caso, la red CDN de Azure aplica automáticamente un valor predeterminado de TTL de siete días.</span><span class="sxs-lookup"><span data-stu-id="64f7a-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="64f7a-111">Para obtener más información acerca del funcionamiento de CDN de Azure toospeed tooblobs de acceso y otros archivos, vea hello [información general sobre la red CDN de Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64f7a-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="64f7a-112">Para obtener más detalles sobre Hola servicio de blob de almacenamiento de Azure, consulte [conceptos del servicio Blob](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="64f7a-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="64f7a-113">Este tutorial muestra varias maneras que puede establecer Hola TTL en un blob en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="64f7a-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="64f7a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="64f7a-114">Azure PowerShell</span></span>
<span data-ttu-id="64f7a-115">[Azure PowerShell](/powershell/azure/overview) es uno de hello formas más rápida y más eficaces tooadminister los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="64f7a-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="64f7a-116">Hola de uso `Get-AzureStorageBlob` tooget cmdlet un blob de toohello referencia, a continuación, establezca hello `.ICloudBlob.Properties.CacheControl` propiedad.</span><span class="sxs-lookup"><span data-stu-id="64f7a-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="64f7a-117">También puede usar PowerShell[administrar los perfiles de red CDN y puntos de conexión](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="64f7a-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="64f7a-118">Biblioteca de cliente de Almacenamiento de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="64f7a-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="64f7a-119">tooset un blob del TTL con. NET, use hello [biblioteca de cliente de almacenamiento de Azure para .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) propiedad.</span><span class="sxs-lookup"><span data-stu-id="64f7a-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="64f7a-120">Hay muchos más ejemplos de código de .NET en hello [ejemplos de almacenamiento de blobs de Azure para .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="64f7a-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="64f7a-121">Otros métodos</span><span class="sxs-lookup"><span data-stu-id="64f7a-121">Other methods</span></span>
* [<span data-ttu-id="64f7a-122">Interfaz de la línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="64f7a-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="64f7a-123">Al cargar el blob de hello, establecer hello *cacheControl* propiedad mediante hello `-p` cambiar.</span><span class="sxs-lookup"><span data-stu-id="64f7a-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="64f7a-124">Este ejemplo establece tooone hora (3600 segundos) de hello TTL.</span><span class="sxs-lookup"><span data-stu-id="64f7a-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="64f7a-125">API de REST de servicios de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="64f7a-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="64f7a-126">Explícitamente conjunto hello *x-ms---control de caché blob* propiedad en un [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [colocar la lista de bloques](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), o [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) solicitud.</span><span class="sxs-lookup"><span data-stu-id="64f7a-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="64f7a-127">Herramientas de administración de almacenamiento de terceros</span><span class="sxs-lookup"><span data-stu-id="64f7a-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="64f7a-128">Algunas herramientas de administración del almacenamiento de Azure de terceros permiten hello tooset *CacheControl* propiedad blobs.</span><span class="sxs-lookup"><span data-stu-id="64f7a-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="64f7a-129">Hola prueba *Cache-Control* encabezado</span><span class="sxs-lookup"><span data-stu-id="64f7a-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="64f7a-130">Puede comprobar fácilmente Hola TTL de los blobs.</span><span class="sxs-lookup"><span data-stu-id="64f7a-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="64f7a-131">Mediante el explorador [herramientas de desarrollo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), probar que el blob es incluidos hello *Cache-Control* encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="64f7a-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="64f7a-132">También puede utilizar una herramienta como **wget**, [Postman](https://www.getpostman.com/), o [Fiddler](http://www.telerik.com/fiddler) encabezados de respuesta de tooexamine Hola.</span><span class="sxs-lookup"><span data-stu-id="64f7a-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64f7a-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64f7a-133">Next Steps</span></span>
* [<span data-ttu-id="64f7a-134">Obtenga información sobre hello *Cache-Control* encabezado</span><span class="sxs-lookup"><span data-stu-id="64f7a-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="64f7a-135">Obtenga información acerca de cómo toomanage caducidad del contenido del servicio de nube en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="64f7a-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

