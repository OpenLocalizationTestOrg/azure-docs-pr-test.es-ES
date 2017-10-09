---
title: "aaa \"crear un índice (API de .NET - búsqueda de Azure) | Documentos de Microsoft\""
description: "Crear un índice en el código mediante Hola SDK de .NET de búsqueda de Azure."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Crear un índice de búsqueda de Azure usando Hola SDK para .NET
> [!div class="op_single_selector"]
> * [Información general](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

En este artículo le guiará a través del proceso de Hola de creación de una búsqueda de Azure [índice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) con hello [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk).

Antes de seguir con esta guía y crear un índice, debe haber [creado ya un servicio de Búsqueda de Azure](search-create-service-portal.md).

> [!NOTE]
> Todo el código de ejemplo de este artículo está escrito en C#. Puede encontrar el código fuente completo hello [en GitHub](http://aka.ms/search-dotnet-howto). También puede leer sobre hello [SDK de .NET de búsqueda de Azure](search-howto-dotnet-sdk.md) para un tutorial más detallado del código de ejemplo de Hola.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificación de la clave de API de administración del servicio de Búsqueda de Azure
Ahora que ha aprovisionado un servicio de búsqueda de Azure, trata de solicitudes de tooissue casi listo en su extremo de servicio con hello .NET SDK. En primer lugar, necesitará tooobtain uno Hola administración claves de api que se generó para aprovisionar el servicio de búsqueda de Hola. Hola .NET SDK enviará esta clave de api en cada servicio de tooyour de solicitud. Tener una clave válida establece la confianza, por cada solicitud, entre Hola aplicación enviando Hola solicitud y el servicio de Hola que los controle.

1. toofind claves de api de su servicio, inicie sesión en toohello [portal de Azure](https://portal.azure.com/)
2. Vaya hoja del servicio de búsqueda de Azure tooyour
3. Haga clic en hello icono "Claves"

El servicio tendrá *claves de administración* y *claves de consulta*.

* El principal y secundaria *claves de administración* conceder derechos completos tooall operaciones, incluido el servicio de hello capacidad toomanage hello, crear y eliminar índices, los indizadores y orígenes de datos. Existen dos claves para que pueda continuar la clave secundaria de hello toouse si decide tooregenerate Hola primary key y viceversa.
* Su *claves de consulta* conceder acceso de solo lectura tooindexes y documentos, y son aplicaciones tooclient normalmente distribuida que emiten solicitudes de búsqueda.

Para fines de Hola de creación de un índice, puede usar su clave de administración principal o secundaria.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Cree una instancia de hello SearchServiceClient (clase)
usar toostart Hola SDK de .NET de búsqueda de Azure, necesitará toocreate una instancia del programa Hola a `SearchServiceClient` clase. Esta clase tiene varios constructores. Hola uno desea que toma el nombre del servicio de búsqueda y un `SearchCredentials` objeto como parámetros. `SearchCredentials` incluye su clave de API.

código de Hello siguiente crea un nuevo `SearchServiceClient` con valores para el nombre de servicio de búsqueda de Hola y clave de api que se almacenan en el archivo de configuración de la aplicación hello (`appsettings.json` en caso de hello de hello [aplicación de ejemplo](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` tiene una propiedad `Indexes`. Esta propiedad proporciona todos los métodos de hello necesita toocreate, lista, actualizar o eliminar los índices de búsqueda de Azure.

> [!NOTE]
> Hola `SearchServiceClient` clase administra el servicio de búsqueda de tooyour de conexiones. En orden tooavoid abrir demasiadas conexiones, debe intentar tooshare una única instancia de `SearchServiceClient` en la aplicación si es posible. Sus métodos es seguras para subprocesos tooenable este tipo de uso compartido.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Definición del índice de Azure Search
Una sola llamada toohello `Indexes.Create` método creará el índice. Este método toma como parámetro un objeto `Index` que define el índice de Búsqueda de Azure. Necesita toocreate un `Index` objeto e inicialícela como sigue:

1. Conjunto hello `Name` propiedad de hello `Index` toohello nombre del objeto de su índice.
2. Conjunto hello `Fields` propiedad de hello `Index` matriz de objetos tooan de `Field` objetos. Hola de toocreate de manera más fácil de Hello `Field` objetos es que realiza la llamada hello `FieldBuilder.BuildForType` método, pasando una clase de modelo para el parámetro de tipo hello. Una clase de modelo tiene propiedades que se asignan campos de toohello de su índice. Esto le permite toobind documentos de su tooinstances de índice de búsqueda de la clase de modelo.

> [!NOTE]
> Si no tiene pensado toouse una clase de modelo, todavía puede definir el índice mediante la creación de `Field` objetos directamente. Puede proporcionar nombre de hello del constructor de toohello campo hello, junto con el tipo de datos de hello (o el analizador para los campos de cadena). También puede establecer otras propiedades, como `IsSearchable`, `IsFilterable`, etc.
>
>

Es importante mantener sus necesidades de negocio y experiencia de usuario de búsqueda en cuenta al diseñar el índice como cada campo debe estar asignado hello [adecuados propiedades](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Estas controlan propiedades que buscar características (filtrado, facetas, ordenación, búsqueda de texto completo, etc.) se aplican toowhich campos. Para cualquier propiedad que no se establece explícitamente, Hola `Field` característica de búsqueda de toodisabling Hola correspondiente a menos que lo habilite específicamente valores predeterminados de clase.

En nuestro ejemplo, hemos llamado a nuestro índice "hoteles" y definido los campos mediante una clase de modelo: Cada propiedad de clase de modelo de hello tiene atributos que determinan el comportamiento de hello relacionados con la búsqueda del campo de índice correspondientes de Hola. clase de modelo de Hello se define como sigue:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

Cuidadosamente que hemos elegido atributos de Hola para cada propiedad en función de cómo creemos que se usarán en una aplicación. Por ejemplo, es probable que puede interesarle coincidencias de palabras clave en hello personas buscando hoteles `description` campo, para habilitar la búsqueda de texto completo para ese campo mediante la adición de hello `IsSearchable` atributo toohello `Description` propiedad.

Tenga en cuenta que exactamente un campo en el índice de tipo `string` debe designarse como Hola Hola *clave* campo agregando hello `Key` atributo (consulte `HotelId` Hola ejemplo anterior).

definición del índice Hola anterior utiliza un analizador de lenguaje para hello `description_fr` campo porque está previsto toostore texto en francés. Vea [tema de compatibilidad de lenguaje de hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) , así como la correspondiente hello [entrada de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) para obtener más información acerca de analizadores de lenguaje.

> [!NOTE]
> De forma predeterminada, el nombre hello de cada propiedad de la clase de modelo se utiliza como nombre de Hola del campo correspondiente de hello en el índice de Hola. Si desea toomap todos los nombres de campo de toocamel con mayúsculas y minúsculas de los nombres de propiedad, marcar la clase hello con hello `SerializePropertyNamesAsCamelCase` atributo. Si desea toomap tooa otro nombre, puede usar hello `JsonProperty` atributo como hello `DescriptionFr` propiedad anterior. Hola `JsonProperty` atributo tiene prioridad sobre hello `SerializePropertyNamesAsCamelCase` atributo.
> 
> 

Ahora que hemos definido una clase de modelo, podemos crear fácilmente una definición de índice:

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Crear índice Hola
Ahora que tiene un inicializado `Index` objeto, puede crear el índice de hello simplemente mediante una llamada a `Indexes.Create` en su `SearchServiceClient` objeto:

```csharp
serviceClient.Indexes.Create(definition);
```

Para una solicitud correcta, método hello devolverá normalmente. Si hay un problema con la solicitud de Hola como un parámetro no válido, se producirá el método hello `CloudException`.

Cuando haya terminado con un índice y quiere toodelete lo, llame a hello `Indexes.Delete` método en su `SearchServiceClient`. Por ejemplo, se trata cómo se eliminaría el índice de "hoteles" hello:

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> código de ejemplo de Hola en este artículo utiliza métodos sincrónicos de Hola de hello SDK de .NET de búsqueda de Azure para simplificar el trabajo. Le recomendamos que use métodos asincrónicos de hello en su propio tookeep aplicaciones escalables y con capacidad de respuesta. Por ejemplo, pudieron utilizar ejemplos anteriores se Hola `CreateAsync` y `DeleteAsync` en lugar de `Create` y `Delete`.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Después de crear un índice de búsqueda de Azure, estará listo demasiado[cargar su contenido en el índice de hello](search-what-is-data-import.md) para que pueda empezar a buscar los datos.

