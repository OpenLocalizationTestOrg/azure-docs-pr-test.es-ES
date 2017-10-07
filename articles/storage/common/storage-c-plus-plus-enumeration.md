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
# <a name="list-azure-storage-resources-in-c"></a>Enumeración de los recursos de Almacenamiento de Azure en C++
Las operaciones de lista son los escenarios de desarrollo de toomany clave con el almacenamiento de Azure. Este artículo describe cómo toomost eficazmente enumerar objetos de almacenamiento de Azure con hello enumerar las API proporcionadas en hello biblioteca de cliente de almacenamiento de Azure de Microsoft para C++.

> [!NOTE]
> Esta guía tiene como destino hello biblioteca de cliente de almacenamiento de Azure para C++ versión 2.x, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Hola biblioteca cliente de almacenamiento proporciona una variedad de toolist métodos u objetos de consulta en el almacenamiento de Azure. Este artículo trata Hola los escenarios siguientes:

* Enumerar contenedores de una cuenta
* Enumerar blobs de un contenedor o un directorio virtual de blobs
* Enumerar colas de una cuenta
* Enumerar tablas en una cuenta
* Query Entities de una tabla

Cada uno de estos métodos se muestra con diferentes sobrecargas para diferentes escenarios.

## <a name="asynchronous-versus-synchronous"></a>Asincrónica frente sincrónica
Porque Hola biblioteca de cliente de almacenamiento para C++ se basa en hello [biblioteca de C++ REST](https://github.com/Microsoft/cpprestsdk), inherentemente admitimos operaciones asincrónicas mediante el uso de [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Por ejemplo:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Operaciones sincrónicas ajustan operaciones asincrónicas de hello correspondiente:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Si está trabajando con varias aplicaciones o servicios de subprocesos, se recomienda que realice Hola async API directamente en lugar de crear una sincronización de Hola de toocall API, que tiene consecuencias importantes sobre el rendimiento de subproceso.

## <a name="segmented-listing"></a>Enumeración segmentada
escala de Hola de almacenamiento en nube requiere lista segmentado. Por ejemplo, puede tener más de un millón de blobs en un contenedor de blobs de Azure o más de mil millones de entidades en una tabla de Azure. Estos no son números teóricos, sino casos de uso reales de clientes.

Por lo tanto, resulta poco práctico si toolist todos los objetos en una única respuesta. En su lugar, puede enumerar objetos mediante la paginación. Cada uno de enumerar las API de hello tiene un *segmentada* sobrecarga.

respuesta de Hola para una operación de lista segmentados incluye:

* <i>_segment</i>, que contiene Hola conjunto de resultados devueltos para un toohello sola llamada API de lista.
* *continuation_token*, toohello siguiente llamada que se pasa en la página siguiente Hola de orden tooget de resultados. Cuando no hay ningún tooreturn resultados más, el token de continuación hello es null.

Por ejemplo, una llamada típica toolist todos los blobs en un contenedor pueden parecer Hola siguiente fragmento de código. código de Hello está disponible en nuestro [ejemplos](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

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

Tenga en cuenta que el número de Hola de resultados devueltos en una página puede controlarse mediante parámetro hello *max_results* en sobrecarga Hola de cada API, por ejemplo:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Si no se especifica hello *max_results* parámetro, valor predeterminado de Hola se devuelve el valor máximo de resultados de too5000 en una sola página.

Tenga en cuenta también que una consulta en el almacenamiento de tabla de Azure puede devolver ningún registro, o menos registros que el valor de Hola de hello *max_results* parámetro que ha especificado, incluso si el token de continuación hello no está vacía. Un motivo podría ser que esa consulta hello no se pudo completar en cinco segundos. Mientras el token de continuación hello no está vacía, Hola consulta debe seguir y el código no debe suponer el tamaño de Hola de resultados del segmento.

Hola recomienda patrón para la mayoría de los escenarios de codificación está segmentada enumerar, que proporciona información de progreso explícita de enumeración o consultar y la manera en que el servicio de Hola responde tooeach solicitud. Especialmente para servicios o aplicaciones de C++, puede ayudar a control de nivel inferior de hello Mostrar progreso de la memoria de control y el rendimiento.

## <a name="greedy-listing"></a>Enumeración expansiva
Las versiones anteriores del programa Hola a biblioteca de cliente de almacenamiento de C++ (versiones 0.5.0 obtener una vista previa y versiones anteriores) incluye las API de lista no segmentado para tablas y colas, como en el siguiente ejemplo de Hola:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Estos métodos se implementaron como contenedores de API segmentadas. Para cada respuesta de lista segmentado, código de hello anexa el vector de hello resultados tooa y devuelve todos los resultados después de que se analizaron contenedores completa Hola.

Este enfoque puede funcionar cuando la cuenta de almacenamiento de Hola o la tabla contiene un pequeño número de objetos. Sin embargo, con un aumento del número de Hola de objetos, memoria de hello necesaria podría aumentar sin límite, porque todos los resultados permanecen en memoria. Una operación de lista puede tardar mucho tiempo, durante qué Hola llamador no tenía ninguna información sobre su progreso.

Estos expansivo enumerar las API en hello SDK no existe en C#, Java, u Hola entorno JavaScript Node.js. tooavoid Hola posibles problemas del uso de estas API expansivas, eliminamos ellos en la versión 0.6.0 vista previa.

Si el código llama a estas API expansivas:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Debe modificar el código de hello toouse segmentada enumerar API:

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

Mediante la especificación de hello *max_results* parámetro del segmento de hello, puede equilibrar entre un número de solicitudes hello y consideraciones de rendimiento de toomeet de uso de memoria de la aplicación.

Además, si está utilizando lista segmentado API, pero almacenar datos de hello en una colección local en un estilo "expansiva", también recomendamos encarecidamente que refactorizar el toohandle código almacenar datos en una colección local cuidadosamente a escala.

## <a name="lazy-listing"></a>Enumeración diferida
Aunque lista expansivo genera posibles problemas, es conveniente si no hay demasiados objetos en el contenedor de Hola.

Si también usa C# o el SDK de Java de Oracle, debe estar familiarizado con hello Enumerable modelo de programación, lo que ofrece una diferida de estilo de lista, donde hello datos en un determinado desplazamiento es solo capturan si es necesario. En C++, una plantilla basada en el iterador hello también proporciona un enfoque similar.

Una API de enumeración diferida normal, con **list_blobs** como ejemplo, tiene el siguiente aspecto:

```cpp
list_blob_item_iterator list_blobs() const;
```

Un fragmento de código típico que utiliza el modelo de lista diferida Hola podría tener este aspecto:

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

Tenga en cuenta que la enumeración diferida solo está disponible en modo sincrónico.

En comparación con la enumeración expansiva, la diferida captura los datos solo cuando es necesario. Tras bastidores de hello, recupera los datos del almacenamiento de Azure solo cuando se mueve el iterador siguiente de hello en el siguiente segmento. Por lo tanto, el uso de memoria se controla con un tamaño límite y operación hello es rápido.

Lista diferida API se incluyen en hello biblioteca cliente de almacenamiento de C++ en la versión 2.2.0.

## <a name="conclusion"></a>Conclusión
En este artículo, analizamos diferentes sobrecargas para enumerar las API para varios objetos en la biblioteca cliente de almacenamiento de Hola para C++. toosummarize:

* Se recomiendan encarecidamente las API asincrónicas en escenarios de varios subprocesos.
* La enumeración segmentada es recomendable para la mayoría de los escenarios.
* Lista diferida se proporciona en la biblioteca de Hola como un contenedor adecuado en escenarios sincrónicos.
* Lista expansiva no se recomienda y se ha quitado de la biblioteca de Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el almacenamiento de Azure y la biblioteca de cliente para C++, vea Hola recursos siguientes.

* [¿Cómo toouse almacenamiento de blobs de C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [¿Cómo toouse almacenamiento de tablas de C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [¿Cómo toouse almacenamiento de cola desde C++](../storage-c-plus-plus-how-to-use-queues.md)
* [Documentación de la Biblioteca de cliente de almacenamiento de Azure para la API de C++.](http://azure.github.io/azure-storage-cpp/)
* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Documentación de Almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/)

