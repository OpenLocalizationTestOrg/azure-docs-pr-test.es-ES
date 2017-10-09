---
title: "aaa \"crear un índice (portal - búsqueda de Azure) | Documentos de Microsoft\""
description: "Crear un índice mediante el Portal de Azure Hola."
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Crear un índice de búsqueda de Azure mediante el Portal de Azure Hola
> [!div class="op_single_selector"]
> * [Información general](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Usar el Diseñador de índice integrados de hello en tooprototype portal Azure o crear un [índice de búsqueda](search-what-is-an-index.md) toorun en su servicio de búsqueda de Azure. 

## <a name="prerequisites"></a>Requisitos previos

En este artículo se dan por hecho una [suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) y el [servicio Azure Search](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Búsqueda del servicio de búsqueda
1. Inicie sesión en toohello página del portal de Azure y revisar hello [buscan en servicios de su suscripción](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Seleccione el servicio Azure Search.

## <a name="name-hello-index"></a>Índice de Hola de nombre

1. Haga clic en hello **agregar índice** botón de barra de comandos de hello al principio de Hola de página de Hola.
2. Asigne un nombre a su índice de Búsqueda de Azure. 
   * Empiece con una letra.
   * Use únicamente letras minúsculas, números o guiones ("-").
   * Limitar los caracteres de too60 de nombre de Hola.

  nombre del índice Hola pasa a formar parte de la dirección URL del extremo Hola utilizado en el índice de toohello de conexiones y para enviar solicitudes HTTP en hello API de REST de búsqueda de Azure.

## <a name="define-hello-fields-of-your-index"></a>Definir campos de hello del índice

Composición de índice incluye un *colección Fields* que define los datos de búsqueda de hello en el índice. Más específicamente, especifica Hola estructura de los documentos que se cargan por separado. colección de campos de Hello incluye algunos campos obligatorios y opcionales, con el nombre y tipo, con índice atributos toodetermine cómo se puede utilizar el campo de Hola.

1. Hola **Add Index** hoja, haga clic en **campos >** tooslide abrir la hoja de definición de campo de Hola. 

2. Aceptar Hola genera *clave* campo de tipo Edm.String. De forma predeterminada, se denomina campo hello *identificador* , pero se puede cambiar como cadena Hola satisface [reglas de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Hay un campo de clave obligatorio para cada índice de Azure Search y debe ser una cadena.

3. Agregar campos toofully especifique documentos de Hola que se va a cargar. Si los documentos constan de un *Id. de*, *nombre del hotel*, *dirección*, *city*, y *región*, crear un campo correspondiente para cada uno de ellos en el índice de Hola. Hola de revisión [diseñar instrucciones de la siguiente sección de hello](#design) para ayudarle a configurar atributos.

4. También puede agregar cualquier campo que se use internamente en expresiones de filtro. En el campo de hello pueden definir otros atributos tooexclude campos de las operaciones de búsqueda.

5. Cuando termine, haga clic en **Aceptar** toosave y crear el índice de Hola.

## <a name="tips-for-adding-fields"></a>Sugerencias para agregar campos

Crear un índice en el portal de hello es teclado intensivo. Minimice los pasos con este flujo de trabajo:

1. En primer lugar, crear lista de campos de hello especificando nombres y tipos de datos de configuración.

2. A continuación, usar casillas de verificación de hello en parte superior de Hola de cada atributo toobulk habilita Hola para todos los campos y, a continuación, selectivamente desactive casillas para hello algunos campos que no lo requieran. Por ejemplo, los campos de cadena normalmente permiten realizar búsquedas. Por lo tanto, puede hacer clic en **Retrievable** y **Searchable** tooboth valores de retorno Hola de hello campo en los resultados de búsqueda, así como permitir la búsqueda de texto completo en el campo de Hola. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Guía de diseño para establecer atributos

Aunque puede agregar nuevos campos en cualquier momento, las definiciones de campo existentes se bloquean en duración de Hola de índice de Hola. Por este motivo, los desarrolladores suelen utilizar el portal de Hola para crear índices simples, pruebas ideas o usar toolook de páginas del portal de hello una configuración. Iteración frecuente sobre un diseño de índice es más eficaz si sigue un enfoque basado en código de modo que puede volver a generar índice Hola fácilmente.

Analizadores y proveedores de sugerencias están asociados con los campos antes de que se guarda el índice de Hola. Ser tooclick seguro a través de cada página con pestañas tooadd lenguaje analizadores o proveedores de sugerencias tooyour definición del índice.

Los campos de cadena se suelen marcar como **Buscable** y **Recuperable**.

Incluyen resultados de la búsqueda de campos utilizados toonarrow **Sortable**, **Filterable**, y **Facetable**.

Los atributos de campo determinan cómo se usa un campo, por ejemplo, si se usa en la búsqueda de texto completo, la navegación por facetas, las operaciones de ordenación, etc. Hello en la tabla siguiente describe cada atributo.

|Atributo|Descripción|  
|---------------|-----------------|  
|**buscable**|Búsqueda de texto completo permite realizar búsquedas, asunto toolexical análisis como separación de palabras durante la indización. Si establece un valor de campo de búsqueda tooa como "sunny day", internamente se dividirá en hello tokens individuales "sunny" y "day". Para obtener detalles, vea [Búsqueda de texto completo](search-lucene-query-architecture.md).|  
|**filtrable**|Se hace referencia en consultas **$filter**. Los campos filtrables de tipo `Edm.String` o `Collection(Edm.String)` no sufren separación de palabras, por lo que las comparaciones son solo de coincidencias exactas. Por ejemplo, si establece este campo f demasiado "sunny day", `$filter=f eq 'sunny'` encontrará ninguna coincidencia, pero `$filter=f eq 'sunny day'` le. |  
|**ordenable**|De forma predeterminada el sistema de hello ordena los resultados por puntuación, pero puede configurar a ordenación basándose en los campos de documentos de Hola. Los campos de tipo `Collection(Edm.String)` no pueden ser **ordenables**. |  
|**clasificable**|Normalmente se usa en una presentación de resultados de búsqueda que incluye un recuento de visitas por categoría (por ejemplo, hoteles de una ciudad concreta). Esta opción no puede utilizarse con campos de tipo `Edm.GeographyPoint`. Los campos de tipo `Edm.String` que son **filtrables**, **ordenables** o **clasificables** pueden tener como máximo 32 kilobytes de longitud. Para obtener detalles, vea [Creación de un índice de Búsqueda de Azure con la API de REST](https://docs.microsoft.com/rest/api/searchservice/create-index).|  
|**key**|Identificador único para los documentos en el índice de Hola. Se debe elegir exactamente un campo como campo de clave de Hola y debe ser del tipo `Edm.String`.|  
|**recuperable**|Determina si el campo de Hola se puede devolver resultados de la búsqueda. Esto es útil cuando desee que un campo de toouse (como *margen de beneficio*) como un filtro, ordenación o puntuación mecanismo, pero no no desee Hola campo toobe toohello visible usuario final. Este atributo debe ser `true` for `key` .|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>Crear índice de hoteles Hola utilizado en secciones de la API de ejemplo

La documentación de la API de Azure Search incluye ejemplos de código con un sencillo índice de *hoteles*. En la capturas de pantalla de Hola a continuación, puede ver definición de índice de hello, incluido el analizador de francés de hello especificado durante la definición del índice, lo que puede volver a crear como un ejercicio de práctica de portal de Hola.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Pasos siguientes

Después de crear un índice de búsqueda de Azure, puede mover el paso siguiente toohello: [cargar datos de búsqueda en el índice de hello](search-what-is-data-import.md).

También podría profundizar en los índices. Además toohello Fields (colección), un índice también especifica analizadores, proveedores de sugerencias, perfiles y la configuración de CORS de puntuación. Hello portal proporciona páginas con pestañas para definir los elementos más comunes de hello: campos, analizadores y proveedores de sugerencias. toocreate o modificar otros elementos, puede usar API de REST de Hola o .NET SDK.

## <a name="see-also"></a>Otras referencias

 [Cómo funciona la búsqueda de texto completo](search-lucene-query-architecture.md)  
 [API de REST del servicio Search](https://docs.microsoft.com/rest/api/searchservice/)[SDK de .NET](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

