---
title: recursos de almacenamiento de Azure aaaList con hello biblioteca de cliente de almacenamiento para C++ | Documentos de Microsoft
description: "Obtenga información acerca de cómo hello toouse enumerar las API en la biblioteca de cliente de almacenamiento de Microsoft Azure para los contenedores de tooenumerate de C++, blobs, colas, tablas y entidades."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="1acaf-103">Enumeración de los recursos de Almacenamiento de Azure en C++</span><span class="sxs-lookup"><span data-stu-id="1acaf-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="1acaf-104">Las operaciones de lista son los escenarios de desarrollo de toomany clave con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1acaf-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="1acaf-105">Este artículo describe cómo toomost eficazmente enumerar objetos de almacenamiento de Azure con hello enumerar las API proporcionadas en hello biblioteca de cliente de almacenamiento de Azure de Microsoft para C++.</span><span class="sxs-lookup"><span data-stu-id="1acaf-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="1acaf-106">Esta guía tiene como destino hello biblioteca de cliente de almacenamiento de Azure para C++ versión 2.x, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="1acaf-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="1acaf-107">Hola biblioteca cliente de almacenamiento proporciona una variedad de toolist métodos u objetos de consulta en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1acaf-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="1acaf-108">Este artículo trata Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="1acaf-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="1acaf-109">Enumerar contenedores de una cuenta</span><span class="sxs-lookup"><span data-stu-id="1acaf-109">List containers in an account</span></span>
* <span data-ttu-id="1acaf-110">Enumerar blobs de un contenedor o un directorio virtual de blobs</span><span class="sxs-lookup"><span data-stu-id="1acaf-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="1acaf-111">Enumerar colas de una cuenta</span><span class="sxs-lookup"><span data-stu-id="1acaf-111">List queues in an account</span></span>
* <span data-ttu-id="1acaf-112">Enumerar tablas en una cuenta</span><span class="sxs-lookup"><span data-stu-id="1acaf-112">List tables in an account</span></span>
* <span data-ttu-id="1acaf-113">Query Entities de una tabla</span><span class="sxs-lookup"><span data-stu-id="1acaf-113">Query entities in a table</span></span>

<span data-ttu-id="1acaf-114">Cada uno de estos métodos se muestra con diferentes sobrecargas para diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="1acaf-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="1acaf-115">Asincrónica frente sincrónica</span><span class="sxs-lookup"><span data-stu-id="1acaf-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="1acaf-116">Porque Hola biblioteca de cliente de almacenamiento para C++ se basa en hello [biblioteca de C++ REST](https://github.com/Microsoft/cpprestsdk), inherentemente admitimos operaciones asincrónicas mediante el uso de [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="1acaf-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="1acaf-117">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1acaf-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="1acaf-118">Operaciones sincrónicas ajustan operaciones asincrónicas de hello correspondiente:</span><span class="sxs-lookup"><span data-stu-id="1acaf-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="1acaf-119">Si está trabajando con varias aplicaciones o servicios de subprocesos, se recomienda que realice Hola async API directamente en lugar de crear una sincronización de Hola de toocall API, que tiene consecuencias importantes sobre el rendimiento de subproceso.</span><span class="sxs-lookup"><span data-stu-id="1acaf-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="1acaf-120">Enumeración segmentada</span><span class="sxs-lookup"><span data-stu-id="1acaf-120">Segmented listing</span></span>
<span data-ttu-id="1acaf-121">escala de Hola de almacenamiento en nube requiere lista segmentado.</span><span class="sxs-lookup"><span data-stu-id="1acaf-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="1acaf-122">Por ejemplo, puede tener más de un millón de blobs en un contenedor de blobs de Azure o más de mil millones de entidades en una tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="1acaf-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="1acaf-123">Estos no son números teóricos, sino casos de uso reales de clientes.</span><span class="sxs-lookup"><span data-stu-id="1acaf-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="1acaf-124">Por lo tanto, resulta poco práctico si toolist todos los objetos en una única respuesta.</span><span class="sxs-lookup"><span data-stu-id="1acaf-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="1acaf-125">En su lugar, puede enumerar objetos mediante la paginación.</span><span class="sxs-lookup"><span data-stu-id="1acaf-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="1acaf-126">Cada uno de enumerar las API de hello tiene un *segmentada* sobrecarga.</span><span class="sxs-lookup"><span data-stu-id="1acaf-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="1acaf-127">respuesta de Hola para una operación de lista segmentados incluye:</span><span class="sxs-lookup"><span data-stu-id="1acaf-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="1acaf-128"><i>_segment</i>, que contiene Hola conjunto de resultados devueltos para un toohello sola llamada API de lista.</span><span class="sxs-lookup"><span data-stu-id="1acaf-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="1acaf-129">*continuation_token*, toohello siguiente llamada que se pasa en la página siguiente Hola de orden tooget de resultados.</span><span class="sxs-lookup"><span data-stu-id="1acaf-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="1acaf-130">Cuando no hay ningún tooreturn resultados más, el token de continuación hello es null.</span><span class="sxs-lookup"><span data-stu-id="1acaf-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="1acaf-131">Por ejemplo, una llamada típica toolist todos los blobs en un contenedor pueden parecer Hola siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="1acaf-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="1acaf-132">código de Hello está disponible en nuestro [ejemplos](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="1acaf-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="1acaf-133">Tenga en cuenta que el número de Hola de resultados devueltos en una página puede controlarse mediante parámetro hello *max_results* en sobrecarga Hola de cada API, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1acaf-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="1acaf-134">Si no se especifica hello *max_results* parámetro, valor predeterminado de Hola se devuelve el valor máximo de resultados de too5000 en una sola página.</span><span class="sxs-lookup"><span data-stu-id="1acaf-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="1acaf-135">Tenga en cuenta también que una consulta en el almacenamiento de tabla de Azure puede devolver ningún registro, o menos registros que el valor de Hola de hello *max_results* parámetro que ha especificado, incluso si el token de continuación hello no está vacía.</span><span class="sxs-lookup"><span data-stu-id="1acaf-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="1acaf-136">Un motivo podría ser que esa consulta hello no se pudo completar en cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="1acaf-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="1acaf-137">Mientras el token de continuación hello no está vacía, Hola consulta debe seguir y el código no debe suponer el tamaño de Hola de resultados del segmento.</span><span class="sxs-lookup"><span data-stu-id="1acaf-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="1acaf-138">Hola recomienda patrón para la mayoría de los escenarios de codificación está segmentada enumerar, que proporciona información de progreso explícita de enumeración o consultar y la manera en que el servicio de Hola responde tooeach solicitud.</span><span class="sxs-lookup"><span data-stu-id="1acaf-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="1acaf-139">Especialmente para servicios o aplicaciones de C++, puede ayudar a control de nivel inferior de hello Mostrar progreso de la memoria de control y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1acaf-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="1acaf-140">Enumeración expansiva</span><span class="sxs-lookup"><span data-stu-id="1acaf-140">Greedy listing</span></span>
<span data-ttu-id="1acaf-141">Las versiones anteriores del programa Hola a biblioteca de cliente de almacenamiento de C++ (versiones 0.5.0 obtener una vista previa y versiones anteriores) incluye las API de lista no segmentado para tablas y colas, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="1acaf-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="1acaf-142">Estos métodos se implementaron como contenedores de API segmentadas.</span><span class="sxs-lookup"><span data-stu-id="1acaf-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="1acaf-143">Para cada respuesta de lista segmentado, código de hello anexa el vector de hello resultados tooa y devuelve todos los resultados después de que se analizaron contenedores completa Hola.</span><span class="sxs-lookup"><span data-stu-id="1acaf-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="1acaf-144">Este enfoque puede funcionar cuando la cuenta de almacenamiento de Hola o la tabla contiene un pequeño número de objetos.</span><span class="sxs-lookup"><span data-stu-id="1acaf-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="1acaf-145">Sin embargo, con un aumento del número de Hola de objetos, memoria de hello necesaria podría aumentar sin límite, porque todos los resultados permanecen en memoria.</span><span class="sxs-lookup"><span data-stu-id="1acaf-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="1acaf-146">Una operación de lista puede tardar mucho tiempo, durante qué Hola llamador no tenía ninguna información sobre su progreso.</span><span class="sxs-lookup"><span data-stu-id="1acaf-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="1acaf-147">Estos expansivo enumerar las API en hello SDK no existe en C#, Java, u Hola entorno JavaScript Node.js.</span><span class="sxs-lookup"><span data-stu-id="1acaf-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="1acaf-148">tooavoid Hola posibles problemas del uso de estas API expansivas, eliminamos ellos en la versión 0.6.0 vista previa.</span><span class="sxs-lookup"><span data-stu-id="1acaf-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="1acaf-149">Si el código llama a estas API expansivas:</span><span class="sxs-lookup"><span data-stu-id="1acaf-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="1acaf-150">Debe modificar el código de hello toouse segmentada enumerar API:</span><span class="sxs-lookup"><span data-stu-id="1acaf-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="1acaf-151">Mediante la especificación de hello *max_results* parámetro del segmento de hello, puede equilibrar entre un número de solicitudes hello y consideraciones de rendimiento de toomeet de uso de memoria de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1acaf-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="1acaf-152">Además, si está utilizando lista segmentado API, pero almacenar datos de hello en una colección local en un estilo "expansiva", también recomendamos encarecidamente que refactorizar el toohandle código almacenar datos en una colección local cuidadosamente a escala.</span><span class="sxs-lookup"><span data-stu-id="1acaf-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="1acaf-153">Enumeración diferida</span><span class="sxs-lookup"><span data-stu-id="1acaf-153">Lazy listing</span></span>
<span data-ttu-id="1acaf-154">Aunque lista expansivo genera posibles problemas, es conveniente si no hay demasiados objetos en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1acaf-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="1acaf-155">Si también usa C# o el SDK de Java de Oracle, debe estar familiarizado con hello Enumerable modelo de programación, lo que ofrece una diferida de estilo de lista, donde hello datos en un determinado desplazamiento es solo capturan si es necesario.</span><span class="sxs-lookup"><span data-stu-id="1acaf-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="1acaf-156">En C++, una plantilla basada en el iterador hello también proporciona un enfoque similar.</span><span class="sxs-lookup"><span data-stu-id="1acaf-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="1acaf-157">Una API de enumeración diferida normal, con **list_blobs** como ejemplo, tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="1acaf-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="1acaf-158">Un fragmento de código típico que utiliza el modelo de lista diferida Hola podría tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="1acaf-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="1acaf-159">Tenga en cuenta que la enumeración diferida solo está disponible en modo sincrónico.</span><span class="sxs-lookup"><span data-stu-id="1acaf-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="1acaf-160">En comparación con la enumeración expansiva, la diferida captura los datos solo cuando es necesario.</span><span class="sxs-lookup"><span data-stu-id="1acaf-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="1acaf-161">Tras bastidores de hello, recupera los datos del almacenamiento de Azure solo cuando se mueve el iterador siguiente de hello en el siguiente segmento.</span><span class="sxs-lookup"><span data-stu-id="1acaf-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="1acaf-162">Por lo tanto, el uso de memoria se controla con un tamaño límite y operación hello es rápido.</span><span class="sxs-lookup"><span data-stu-id="1acaf-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="1acaf-163">Lista diferida API se incluyen en hello biblioteca cliente de almacenamiento de C++ en la versión 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="1acaf-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1acaf-164">Conclusión</span><span class="sxs-lookup"><span data-stu-id="1acaf-164">Conclusion</span></span>
<span data-ttu-id="1acaf-165">En este artículo, analizamos diferentes sobrecargas para enumerar las API para varios objetos en la biblioteca cliente de almacenamiento de Hola para C++.</span><span class="sxs-lookup"><span data-stu-id="1acaf-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="1acaf-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="1acaf-166">toosummarize:</span></span>

* <span data-ttu-id="1acaf-167">Se recomiendan encarecidamente las API asincrónicas en escenarios de varios subprocesos.</span><span class="sxs-lookup"><span data-stu-id="1acaf-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="1acaf-168">La enumeración segmentada es recomendable para la mayoría de los escenarios.</span><span class="sxs-lookup"><span data-stu-id="1acaf-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="1acaf-169">Lista diferida se proporciona en la biblioteca de Hola como un contenedor adecuado en escenarios sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="1acaf-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="1acaf-170">Lista expansiva no se recomienda y se ha quitado de la biblioteca de Hola.</span><span class="sxs-lookup"><span data-stu-id="1acaf-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1acaf-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1acaf-171">Next steps</span></span>
<span data-ttu-id="1acaf-172">Para obtener más información sobre el almacenamiento de Azure y la biblioteca de cliente para C++, vea Hola recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="1acaf-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="1acaf-173">¿Cómo toouse almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="1acaf-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="1acaf-174">¿Cómo toouse almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="1acaf-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="1acaf-175">¿Cómo toouse almacenamiento de cola desde C++</span><span class="sxs-lookup"><span data-stu-id="1acaf-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="1acaf-176">Documentación de la Biblioteca de cliente de almacenamiento de Azure para la API de C++.</span><span class="sxs-lookup"><span data-stu-id="1acaf-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="1acaf-177">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="1acaf-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="1acaf-178">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="1acaf-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

