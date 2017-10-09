---
title: 'Operaciones de indexador (API de REST del servicio Azure Search: 2015-02-28-Preview) | Microsoft Docs'
description: "Operaciones de indexador (API de REST del servicio de Búsqueda de Azure: 2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Operaciones de indexador (API de REST del servicio de Búsqueda de Azure: 2015-02-28-Preview)
> [!NOTE]
> Este artículo describen los indizadores en hello [API de REST de vista previa 2015-02-28](search-api-2015-02-28-preview.md). Esta versión de la API agrega versiones preliminares del indexador de Almacenamiento de blobs de Azure con la extracción de documentos y del indexador de Almacenamiento de tablas de Azure, además de otras mejoras. Hola API también admite disponible con carácter general indizadores (GA), incluidos los indizadores para base de datos de SQL Azure, SQL Server en máquinas virtuales de Azure y base de datos de Azure Cosmos.
> 
> 

## <a name="overview"></a>Información general
Búsqueda de Azure puede integrarse directamente con algunos orígenes de datos común, quitar Hola necesidad toowrite código tooindex los datos. tooset de este servicio, se puede llamar toocreate de API de búsqueda de Azure de Hola y administrar **indizadores** y **orígenes de datos**. 

Un **indizador** es un recurso que conecta los orígenes de datos con los índices de búsqueda de destino. Un indizador que se usa en hello siguientes maneras: 

* Realizar una copia única de hello datos toopopulate un índice.
* Sincronizar un índice con cambios en el origen de datos de hello según una programación. programación de Hello es parte de la definición de indizador de Hola.
* Invocar a petición tooupdate un índice según sea necesario. 

Un **indizador** es útil cuando desea actualizaciones periódicas tooan índice. Puede configurar una programación en línea como parte de una definición de indexador o ejecutarla a petición mediante [Ejecutar indexador](#RunIndexer). 

A **origen de datos** especifica qué datos hay toobe indizados, credenciales tooaccess Hola datos y directivas tooenable búsqueda de Azure tooefficiently identificar cambios en los datos de hello (como modificar o eliminar filas de una tabla de base de datos). Se define como un recurso independiente para que puedan usarlo múltiples indizadores.

Hola siguientes orígenes de datos es compatibles actualmente:

* **Azure SQL Database** y **SQL Server en máquinas virtuales de Azure**. Para obtener un tutorial de destino, consulte [este artículo](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Para obtener un tutorial de destino, consulte [este artículo](search-howto-index-documentdb.md). 
* **Almacenamiento de blobs de Azure**, incluidos formatos de documento siguiente hello: PDF, Microsoft Office (DOCX/DOC, XLS/XSLX, PPTX/PPT, MSG), HTML, XML, ZIP y texto sin formato de archivos (incluido JSON). Para obtener un tutorial dirigido, consulte [este artículo](search-howto-indexing-azure-blob-storage.md).
* **Azure Table Storage**. Para obtener un tutorial de destino, consulte [este artículo](search-howto-indexing-azure-tables.md).

Estamos pensando en Agregar compatibilidad con orígenes de datos adicionales en hello futuras. toohelp nos priorizar estas decisiones, proporcione sus comentarios en hello [foro de comentarios de búsqueda de Azure](http://feedback.azure.com/forums/263029-azure-search).

Vea [límites de servicio](search-limits-quotas-capacity.md) para máximo limita los recursos de origen de tooindexer y los datos relacionados.

## <a name="typical-usage-flow"></a>Flujo típico de uso
Puede crear y administrar indexadores y orígenes de datos mediante solicitudes HTTP sencillas (POST, GET, PUT, DELETE) en un recurso `data source` o `indexer` determinado.

La configuración de la indexación automática suele ser un proceso de cuatro pasos:

1. Identificar el origen de datos de Hola que contiene los datos de Hola que necesita toobe indizado. Tenga en cuenta que búsqueda de Azure pueden no admitir todos los tipos de datos de hello presentes en el origen de datos. Vea [tipos de datos admitidos](https://msdn.microsoft.com/library/azure/dn798938.aspx) para lista de Hola.
2. Cree un índice de Búsqueda de Azure cuyo esquema sea compatible con su origen de datos.
3. Cree un origen de datos de Búsqueda de Azure, tal como se describe en [Crear origen de datos](#CreateDataSource).
4. Cree un indexador de Búsqueda de Azure tal y como se describe en [Crear indexador](#CreateIndexer).

Debe planear la creación de un indizador para cada combinación de origen de datos e índice de destino. Puede tener varios indexadores que escriban en hello mismo índice y se puede volver a usar Hola mismo origen de datos para varios indizadores. Sin embargo, un indizador que solo puede utilizar un origen de datos a la vez y solo puede escribir el índice único tooa. 

Después de crear un indizador, puede recuperar su estado de ejecución con hello [obtener estado del indizador](#GetIndexerStatus) operación. También puede ejecutar un indexador en cualquier momento (en lugar de o en suma toorunning periódicamente en una programación) con hello [ejecutar indizador](#RunIndexer) operación.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Crear origen de datos
En búsqueda de Azure, se utiliza un origen de datos con los indizadores, proporcionando información de conexión de hello para la actualización de datos ad hoc o programado de un índice de destino. Puede crear un origen de datos nuevo dentro de un servicio de Búsqueda de Azure mediante una solicitud HTTP POST.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Como alternativa, puede usar PUT y especificar el nombre de origen de datos de hello en hello URI. Si el origen de datos de hello no existe, se creará.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> número máximo de Hola de orígenes de datos permitido varía según el nivel de precios. servicio gratuito de Hello permite too3 orígenes de datos. El servicio estándar permite 50 orígenes de datos. Consulte [Límites de servicio](search-limits-quotas-capacity.md) para obtener más información.
> 
> 

**Solicitud**

HTTPS es necesario para todas las solicitudes de servicio. Hola **crear origen de datos** solicitud puede crearse mediante un método POST o PUT. Al usar POST, debe proporcionar un nombre de origen de datos en el cuerpo de la solicitud junto con la definición de origen de datos de Hola Hola. Con PUT, nombre de hello forma parte de la dirección URL de Hola. Si no existe el origen de datos de hello, se crea. Si ya existe, está actualizada toohello nueva definición. 

nombre de origen de datos de Hello debe estar en minúsculas, empezar por una letra o un número, no tener barras o puntos y tener menos de 128 caracteres. Después de iniciar el nombre de origen de datos de Hola con una letra o un número, rest Hola de nombre de hello puede incluir cualquier letra, número y guiones, como Hola guiones no sean consecutivos. Consulte [Reglas de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx) para obtener más información.

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`.

**Encabezados de solicitud**

Hola lista siguiente describe Hola necesarios y los encabezados de solicitud opcionales. 

* `Content-Type`: obligatorio. Establezca esta propiedad demasiado`application/json`
* `api-key`: obligatorio. Hola `api-key` es tooauthenticate usado Hola solicitud tooyour servicio de búsqueda. Es un valor de cadena, el servicio de tooyour único. Hola **crear origen de datos** solicitud debe incluir un `api-key` encabezado establece clave de administrador de tooyour (como clave de consulta tooa lugar). 

También necesitará Hola nombre tooconstruct Hola solicitud dirección URL del servicio. Se puede obtener el nombre de servicio hello y `api-key` desde el panel de servicio en hello [Portal de Azure](https://portal.azure.com/). Vea [crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) para obtener ayuda de navegación de página.

<a name="CreateDataSourceRequestSyntax"></a>
**Sintaxis del cuerpo de la solicitud**

Hola el cuerpo de solicitud de hello contiene una definición de origen de datos, que incluye el tipo de origen de datos de hello, datos de credenciales tooread hello, así como una detección de cambios de datos opcionales y detección de eliminación de datos identifican las directivas que son utilizado tooefficiently cambiado o datos eliminados en el origen de datos de hello cuando se usa con un indizador programado periódicamente. 

sintaxis de Hola para estructurar la carga de la solicitud de hello es como sigue. En este tema se proporciona una solicitud de ejemplo.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

La solicitud contiene Hola propiedades siguientes: 

* `name`: obligatorio. nombre de Hola Hola del origen de datos. Un nombre de origen de datos debe solo contener letras minúsculas, números o guiones, no puede empezar ni terminar con guiones y caracteres too128 limitado.
* `description`: descripción opcional. 
* `type`: obligatorio. Debe ser uno de los tipos de orígenes de datos de hello admitida:
  * `azuresql` : base de datos SQL de Azure y SQL Server en máquinas virtuales de Azure
  * `documentdb` : Azure Cosmos DB
  * `azureblob` : Blob Storage de Azure
  * `azuretable` : Table Storage de Azure
* `credentials`:
  * Hola necesario `connectionString` propiedad especifica la cadena de conexión de Hola Hola origen de datos. formato de Hola de cadena de conexión de hello depende de tipo de origen de datos de hello: 
    * Para SQL Azure, se trata de cadena de conexión de SQL Server habitual de Hola. Si usa la cadena de conexión de hello tooretrieve portal Azure hello, usar hello `ADO.NET connection string` opción.
    * Para base de datos de Azure Cosmos, cadena de conexión de Hola debe Hola siguiendo el formato: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Todos los valores de hello son necesarios. Puede encontrarlos en hello [portal de Azure](https://portal.azure.com/).  
    * Para blobs de Azure y el almacenamiento de tabla, se trata de cadena de conexión de cuenta de almacenamiento de Hola. se describe el formato de Hello [aquí](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). Se requiere un protocolo para el punto de conexión HTTPS.  
* `container`, necesaria: especifica Hola datos tooindex con hello `name` y `query` propiedades: 
  * `name`, obligatorio:
    * SQL Azure: especifica Hola tabla o vista. Puede usar nombres calificados con el esquema, como `[dbo].[mytable]`.
    * Documentos: especifica la colección de Hola. 
    * Almacenamiento de blobs de Azure: especifica el contenedor de almacenamiento de Hola.
    * El almacenamiento de tabla: especifica nombre Hola de tabla Hola. 
  * `query`, opcional:
    * Documentos: permite toospecify una consulta que aplana un diseño del documento JSON arbitrario en un esquema sin formato que se puede indizar la búsqueda de Azure.  
    * Almacenamiento de blobs de Azure: permite toospecify una carpeta virtual dentro de contenedor de blobs de Hola. Por ejemplo, para la ruta de acceso de blob `mycontainer/documents/blob.pdf`, `documents` puede utilizarse como carpetas virtuales Hola.
    * El almacenamiento de tabla: permite toospecify una consulta que filtros Hola conjunto de toobe filas importado.
    * SQL Azure: no se admite la consulta. Si necesita esta funcionalidad, vote por [esta sugerencia](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Hola opcional `dataChangeDetectionPolicy` y `dataDeletionDetectionPolicy` a continuación se describen las propiedades.

<a name="DataChangeDetectionPolicies"></a>
**Directivas de detección de cambios de datos**

propósito de Hola de los datos cambia la directiva de detección es tooefficiently identificar elementos de datos que han cambiado. Las directivas compatibles varían en función de tipo de origen de datos de Hola. En las siguientes secciones se describe cada directiva. 

***Directiva de detección de cambios de límite superior*** 

Use esta directiva cuando el origen de datos contiene una columna o propiedad que cumple Hola siguiendo criterios:

* Todas las inserciones especifican un valor para la columna de Hola. 
* Elemento de tooan de todas las actualizaciones también cambie el valor de Hola de columna Hola. 
* valor de Hola de esta columna aumenta con cada cambio.
* Las consultas que usan una continuación de toohello similar de cláusula de filtro `WHERE [High Water Mark Column] > [Current High Water Mark Value]` se pueden ejecutar eficientemente.

Por ejemplo, al utilizar orígenes de datos de SQL Azure, un indizada `rowversion` columna es candidato ideal de Hola para su uso con directivas de marca de agua de Hola. 

Esta directiva se puede especificar del modo siguiente:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Al utilizar orígenes de datos de la base de datos de Azure Cosmos, debe utilizar hello `_ts` propiedad proporcionada por base de datos de Azure Cosmos. 

Cuando se usa automáticamente los orígenes de datos de Blob de Azure, búsqueda de Azure utiliza una marca de agua alta cambiar directiva de detección en función de timestamp de última modificación del blob; no es necesario toospecify esta directiva usted mismo.   

***Directiva de detección de cambios integrados de SQL***

Si la base de datos SQL admite el [seguimiento de cambios](https://msdn.microsoft.com/library/bb933875.aspx), se recomienda usar la directiva de seguimiento de cambios integrada de SQL. Esta directiva habilita el seguimiento de cambios más eficaz hello y permite filas tooidentify eliminado de búsqueda de Azure sin necesidad de toohave una columna de "eliminación temporal" explícita en el esquema.

Seguimiento de cambios integrado se admiten a partir de hello después de versiones de la base de datos de SQL Server: 

* SQL Server 2008 R2, si usa SQL Server en máquinas virtuales de Azure.
* Base de datos SQL de Azure V12, si está usando la Base de datos SQL de Azure.  

Al usar la directiva de seguimiento de cambios integrada de SQL, no especifique una directiva de detección de eliminación de datos independiente, ya que esta directiva tiene compatibilidad integrada para identificar las filas eliminadas. 

Esta directiva solo se puede usar con tablas; no se puede usar con vistas. Necesita tooenable seguimiento de cambios para tabla de Hola que está utilizando para poder usar esta directiva. Consulte [Habilitar y deshabilitar el seguimiento de cambios](https://msdn.microsoft.com/library/bb964713.aspx) para obtener instrucciones.    

Al estructurar hello **crear origen de datos** solicitar SQL política de seguimiento de cambios integrado pueden especificarse como se indica a continuación:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Directivas de detección de eliminación de datos**

Hola de una directiva de detección de eliminación de datos sirve tooefficiently identificar elementos de datos eliminados. Actualmente, directiva de hello solo admitido es hello `Soft Delete` directiva, que permite identificar eliminado los elementos en función de valor de Hola de un `soft delete` columna o propiedad de origen de datos de Hola. Esta directiva se puede especificar del modo siguiente:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Solo se admiten las columnas con cadenas, números enteros o valores booleanos. Hola valor utilizado como `softDeleteMarkerValue` debe ser una cadena, incluso si la columna correspondiente de hello contiene enteros o booleanos. Por ejemplo, si el valor de Hola que aparece en el origen de datos es 1, use `"1"` como hello `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Ejemplos de cuerpo de solicitud**

Si piensa que el origen de datos de hello toouse con un indizador que se ejecuta en una programación, este ejemplo muestra cómo cambiar toospecify y eliminación de las directivas de detección: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Si solo piensa toouse origen de datos de Hola para una copia única de los datos de hello, se pueden omitir las directivas de hello:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Respuesta**

Para obtener una solicitud correcta: "201 Creado". 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Actualizar el origen de datos
Puede actualizar un origen de datos existente mediante una solicitud HTTP PUT. Especificar nombre de Hola de tooupdate de origen de datos de hello en URI de solicitud de hello:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`. En [Control de versiones de API de Azure Search](https://msdn.microsoft.com/library/azure/dn864560.aspx) se incluyen detalles e información adicional sobre versiones alternativas.

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Solicitud**

Hello sintaxis de cuerpo de solicitud es Hola igual que para [solicita crear origen de datos](#CreateDataSourceRequestSyntax).

Algunas propiedades no se pueden actualizar en un origen de datos existente. Por ejemplo, no se puede cambiar el tipo de saludo de un origen de datos existente.  

Si no desea la cadena de conexión de hello toochange para un origen de datos existente, puede especificar literal hello `<unchanged>` de cadena de conexión de Hola. Esto es útil en situaciones donde necesita tooupdate un origen de datos, pero no tiene la cadena de conexión de acceso cómodo toohello puesto que se trata de datos de seguridad.

**Respuesta**

Para efectuar una solicitud correcta: 201 Creado si se ha creado un origen de datos nuevo, y 204 Sin contenido si se ha actualizado un origen de datos existente.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Enumerar orígenes de datos
Hola **orígenes de datos de lista** operación devuelve una lista de orígenes de datos de hello en el servicio de búsqueda de Azure. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Para obtener una solicitud correcta: "200 Correcto".

A continuación se proporciona un cuerpo de respuesta de ejemplo:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Tenga en cuenta que puede filtrar Hola respuesta hacia abajo de propiedades de hello toojust que le interesa. Por ejemplo, si desea que solo una lista de nombres de origen de datos, utilice Hola OData `$select` opción de consulta:

    GET /datasources?api-version=205-02-28&$select=name

En este caso, respuesta Hola Hola ejemplo anterior podría aparecer como sigue: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Se trata de un ancho de banda de toosave técnica útil si tiene una gran cantidad de orígenes de datos en el servicio de búsqueda.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Obtener origen de datos
Hola **obtener el origen de datos** operación obtiene la definición de origen de datos de Hola de búsqueda de Azure.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

respuesta de Hello es tooexamples similar en [solicitudes de ejemplo de crear origen de datos](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> No establezca hello `Accept` encabezado de solicitud demasiado`application/json;odata.metadata=none` al llamar a esta API como si lo hace, provocará `@odata.type` toobe de atributo se omite de la respuesta de Hola y no será capaz de toodifferentiate entre el cambio de datos y detección de eliminación de datos directivas de tipos diferentes. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Eliminar origen de datos
Hola **eliminar el origen de datos** operación quita un origen de datos de su servicio de búsqueda de Azure.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Si algún indizador hace una referencia de origen de datos de Hola que se dispone a eliminar, operación de eliminación de hello seguirá adelante. Sin embargo, los indexadores pasarán a un estado de error en su siguiente ejecución.  
> 
> 

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 204 Sin contenido.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Crear indexador
Puede crear un indexador nuevo dentro de un servicio de Búsqueda de Azure mediante una solicitud HTTP POST:

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Como alternativa, puede usar PUT y especificar el nombre de origen de datos de hello en hello URI. Si el origen de datos de hello no existe, se creará.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> número máximo de Hola de indizadores permitido varía según el nivel de precios. servicio gratuito de Hello permite que un too3 indizadores. El servicio estándar permite 50 indexadores. Consulte [Límites de servicio](search-limits-quotas-capacity.md) para obtener más información.
> 
> 

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

<a name="CreateIndexerRequestSyntax"></a>
**Sintaxis del cuerpo de la solicitud**

cuerpo de saludo de solicitud de hello contiene una definición de indizador, que especifica el origen de datos de Hola y el índice de destino de hello para la indización, así como la programación de indización opcional y parámetros. 

sintaxis de Hola para estructurar la carga de la solicitud de hello es como sigue. En este tema se proporciona una solicitud de ejemplo.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Programación de indexador**

Un indizador puede especificar opcionalmente una programación. Si una programación está presente, el indizador de Hola se ejecutará periódicamente según la programación. Programación tiene Hola siguientes atributos:

* `interval`: obligatorio. Valor de duración que especifica un intervalo o período durante el que se ejecuta el indizador. Hola más pequeño permitido intervalo es 5 minutos. Hola más larga es un día. Debe tener el formato de un valor "dayTimeDuration" XSD (subconjunto restringido de un valor de [duración ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). patrón de Hola para esto es: `"P[nD][T[nH][nM]]"`. Ejemplos: `PT15M` para cada 15 minutos, `PT2H` para cada 2 horas. 
* `startTime`: obligatorio. Una fecha y hora UTC indizador Hola debe iniciar su ejecución. 

**Parámetros de un indexador**

Un indexador puede especificar varios parámetros que afectan a su comportamiento. Todos los parámetros de hello son opcionales.  

* `maxFailedItems`: número de Hola de elementos que pueden dar error toobe indizadas antes de una ejecución del indexador se considera un error. El valor predeterminado es 0. Se devuelve información sobre los elementos con error por hello [obtener estado del indizador](#GetIndexerStatus) operación. 
* `maxFailedItemsPerBatch`: número de Hola de elementos que pueden dar error toobe indizados en cada lote antes de que una ejecución del indexador se considera un error. El valor predeterminado es 0.
* `base64EncodeKeys`: especifica si las claves de documento estarán codificadas en base 64. Búsqueda de Azure impone restricciones en los caracteres que pueden estar presentes en una clave del documento. Sin embargo, los valores de hello en los datos de origen pueden contener caracteres que no son válidos. Si es necesario tooindex como valores como las claves de documento, este indicador puede establecerse tootrue. El valor predeterminado es `false`.
* `batchSize`: Especifica el número de Hola de elementos que se leen desde el origen de datos de Hola e indizadas como un único lote en el rendimiento de tooimprove de orden. valor predeterminado de Hello depende de tipo de origen de datos de hello: es 1000 para SQL Azure y base de datos de Azure Cosmos y 10 para el almacenamiento de blobs de Azure.

**Asignaciones de campos**

Puede usar asignaciones de campo toomap un nombre de campo de nombre de campo diferente de tooa en origen de datos de hello en el índice de destino de Hola. Por ejemplo, considere una tabla de origen con un campo `_id`. Búsqueda de Azure no permite que un nombre de campo a partir de un carácter de subrayado, por lo que debe cambiarse de campo Hola. Esto puede hacerse mediante hello `fieldMappings` propiedad de indizador de hello como sigue: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Puede especificar varias asignaciones de campo. 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Los nombres de campo de origen y destino no distinguen entre mayúsculas y minúsculas.

<a name="FieldMappingFunctions"></a>
***Funciones de asignación de campos***

Asignaciones de campos también pueden ser los valores del campo de origen utilizados tootransform mediante *asignar funciones*.

Actualmente solo se admite una función de este tipo: `jsonArrayToStringCollection`. Analiza un campo que contenga una cadena con formato como una matriz JSON en un campo Collection (EDM.String) en el índice de destino de Hola. Está pensado para su usarse con el indexador de SQL Azure en particular, puesto que SQL no tiene un tipo de datos de colección nativo. Se puede usar del modo indicado a continuación: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Por ejemplo, si hello campo de origen contiene cadena de hello `["red", "white", "blue"]`, Hola de campo de destino de tipo `Collection(Edm.String)` se rellenará con valores de hello tres `"red"`, `"white"` y `"blue"`.

Tenga en cuenta que hello `targetFieldName` propiedad es opcional; si se omitiera, Hola `sourceFieldName` se utiliza el valor. 

<a name="CreateIndexerRequestExamples"></a>
**Ejemplos de cuerpo de solicitud**

Hello en el ejemplo siguiente se crea un indizador que copia datos de tabla de hello al que hace referencia hello `ordersds` toohello del origen de datos `orders` índice según una programación que empieza el 1 de enero de 2015 UTC y se ejecuta cada hora. Cada invocación de indizador será correcto si no tiene más de 5 artículos fallar toobe indizada en cada lote, y no más de 10 elementos toobe en total. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Respuesta**

Para obtener una solicitud correcta: "201 Creado".

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Actualizar indexador
Puede actualizar un indexador existente mediante una solicitud HTTP PUT. Especificar nombre de Hola de hello indizador tooupdate en URI de solicitud de hello:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hola `api-version` es necesario. versión actual de Hello es `2015-02-28`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Solicitud**

Hello sintaxis de cuerpo de solicitud es Hola igual que para [solicita crear indizador](#CreateIndexerRequestSyntax).

**Respuesta**

Para efectuar una solicitud correcta: 201 Creado si se ha creado un indexador nuevo, y 204 Sin contenido si se ha actualizado un indexador existente.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Enumerar indexadores
Hola **enumeración de indizadores** operación devuelve la lista de Hola de indizadores en el servicio de búsqueda de Azure. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Hola `api-version` es necesario. versión de vista previa de Hello es `2015-02-28-Preview`. [Versiones de Búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx) contiene detalles y más información sobre versiones alternativas.

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Para obtener una solicitud correcta: "200 Correcto".

A continuación se proporciona un cuerpo de respuesta de ejemplo:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Tenga en cuenta que puede filtrar Hola respuesta hacia abajo de propiedades de hello toojust que le interesa. Por ejemplo, si desea que solo una lista de nombres de los indizadores, use Hola OData `$select` opción de consulta:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

En este caso, respuesta Hola Hola ejemplo anterior podría aparecer como sigue: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Se trata de un ancho de banda de toosave técnica útil si tiene una gran cantidad de indizadores en el servicio de búsqueda.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Obtener indexador
Hola **Get Indexer** operación obtiene la definición de indizador de Hola de búsqueda de Azure.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Hola `api-version` es necesario. versión de vista previa de Hello es `2015-02-28-Preview`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 200 Correcto.

respuesta de Hello es tooexamples similar en [indizador crear solicitudes de ejemplo](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Eliminar indexador
Hola **eliminar indizador** operación quita un indizador de su servicio de búsqueda de Azure.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Cuando se elimina un indizador, ejecuciones de indizador de hello en curso en ese momento ejecutarán toocompletion, pero no se programará ningún más ejecuciones. Toouse intentos dará como resultado un indizador inexistente en el código de estado HTTP 404 no encontrado. 

Hola `api-version` es necesario. versión de vista previa de Hello es `2015-02-28-Preview`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: al obtener una respuesta correcta, se visualiza 204 Sin contenido.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Ejecutar indexador
En suma toorunning periódicamente según una programación, un indizador también se puede invocar a petición a través de hello **ejecutar indizador** operación: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Hola `api-version` es necesario. versión de vista previa de Hello es `2015-02-28-Preview`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: 202 Aceptado se obtiene tras una respuesta correcta.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Obtener el estado del indexador
Hola **obtener estado del indizador** operación recupera Hola actual estado de historial de ejecución y un indizador: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Hola `api-version` es necesario. versión de vista previa de Hello es `2015-02-28-Preview`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: 200 Correcto al obtener una respuesta correcta.

cuerpo de respuesta de Hello contiene información sobre el estado general del estado de indizador, última invocación de indizador hello, así como el historial reciente invocaciones de indizador hello (si existe). 

Un cuerpo de respuesta de muestra tiene el siguiente aspecto: 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Estado del indexador**

Estado del indizador puede ser uno de hello siguientes valores:

* `running`indica que indizador Hola se ejecuta con normalidad. Tenga en cuenta que algunas de las ejecuciones de indizador de hello todavía puedan tener errores, por lo que es un Hola de buena idea toocheck `lastResult` propiedad así. 
* `error`indica que ese indizador Hola ha experimentado un error que no se puede corregir sin intervención humana. Por ejemplo, pueden haber caducado las credenciales del origen de datos de hello, o esquema de Hola Hola origen de datos o de índice de destino de hello ha cambiado provocando una ruptura forma. 

**Resultado de la ejecución del indexador**

Un resultado de la ejecución de indexador contiene información sobre la ejecución de un indexador único. resultado de Hello más reciente aparece como hello `lastResult` propiedad del estado de indizador de Hola. Otros resultados recientes, si está presente, se devuelven como hello `executionHistory` propiedad del estado de indizador de Hola. 

Resultado de la ejecución de indizador contiene Hola propiedades siguientes: 

* `status`: Hola estado de una ejecución. Consulte [Estado de la ejecución del indexador](#IndexerExecutionStatus) a continuación para obtener más información. 
* `errorMessage`: mensaje de error de una ejecución errónea. 
* `startTime`: hora de hello en UTC cuando inició esta ejecución.
* `endTime`: hora de hello en UTC cuando termina la ejecución. No se establece este valor si la ejecución de hello está aún en curso.
* `errors`: una matriz de errores de nivel de elemento, si los hay. Cada entrada contiene una clave de documento (propiedad `key`) y un mensaje de error (propiedad `errorMessage`). 
* `itemsProcessed`: Hola número de elementos de origen de datos (por ejemplo, las filas de tabla) que Hola indizador intentada tooindex durante esta ejecución. 
* `itemsFailed`: Hola número de elementos que dieron error durante la ejecución de este.  
* `initialTrackingState`: siempre `null` para la primera ejecución del indizador hello, o si el directiva de seguimiento de cambios de datos de hello no está habilitado en el origen de datos de hello utilizado. Si está habilitada esta directiva, en las ejecuciones posteriores, este valor indica valor procesado por esta ejecución de seguimiento de cambios de (el más bajo) primera Hola. 
* `finalTrackingState`: siempre `null` si la directiva de seguimiento de cambios de datos de hello no está habilitado en el origen de datos de hello utilizado. En caso contrario, indica valor procesado correctamente por esta ejecución de seguimiento de cambios de (el más alto) más reciente Hola. 

<a name="IndexerExecutionStatus"></a>
**Estado de la ejecución del indexador**

Estado de ejecución de indizador captura el estado de saludo de una única ejecución de indizador. Puede tener Hola siguientes valores:

* `success`indica que se ha completado correctamente la ejecución del indizador Hola.
* `inProgress`indica que la ejecución de indizador de hello está en curso. 
* `transientFailure` indica que la ejecución de indexador ha fallado. Consulte la propiedad `errorMessage` para obtener detalles. Error de Hello puede o no requerir intervención humana toofix: por ejemplo, corregir una incompatibilidad de esquema entre el origen de datos de Hola y el índice de destino de hello requiere acción del usuario, mientras que un tiempo de inactividad del origen de datos temporal no. Las invocaciones del indexador continuarán según la programación, si hay alguna establecida. 
* `persistentFailure`indica que indizador Hola generó un error de forma que se requiera intervención humana. Detención de ejecuciones programadas del indexador. Tras solucionar el problema de hello, utilice las ejecuciones de restablecimiento de la API de indizador toorestart Hola programado. 
* `reset`indica que indizador Hola se ha restablecido mediante un tooReset llamada API de indizador (ver abajo). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Restablecer el indexador
Hola **restablecer indizador** operación restablece el estado asociado con el indizador de Hola de seguimiento de cambios de Hola. Esto le permite volver a indizar (por ejemplo, si ha cambiado el esquema de origen de datos) del principio de tootrigger o directiva de detección de cambios de datos de toochange Hola para un origen de datos asociado con el indizador de Hola.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Hola `api-version` es necesario. versión de vista previa de Hello es `2015-02-28-Preview`. 

Hola `api-key` debe ser una clave de administración (como clave de consulta tooa lugar). Consulte la sección de autenticación de toohello en [API de REST de servicio de búsqueda](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn más información acerca de las claves. [Crear un servicio de búsqueda en el portal de hello](search-create-service-portal.md) explica cómo utilizan la dirección URL del servicio de tooget Hola y propiedades de clave en la solicitud de Hola.

**Respuesta**

Código de estado: 204 Sin contenido para obtener una respuesta correcta.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Asignación entre tipos de datos de SQL y tipos de datos de Búsqueda de Azure
<table style="font-size:12">
<tr>
<td>Tipo de datos de SQL</td>    
<td>Tipos de campos de índice de destino permitidos</td>
<td>Notas</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>real, float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, money<br>decimal<br>numeric
</td>
<td>Edm.String</td>
<td>Búsqueda de Azure no admite la conversión de tipos decimales en Edm.Double porque esto podría provocar la pérdida de precisión
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>Vea [funciones de asignación de campos](#FieldMappingFunctions) en este documento para obtener más información acerca de cómo tootransform una columna de cadenas en una Collection (EDM.String)</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>geography</td>
<td>Edm.GeographyPoint</td>
<td>Se admiten solo las instancias de geography de tipo POINT con SRID 4326 (que es el valor predeterminado de hello)</td>
</tr>
<tr>
<td>rowversion</td>
<td>N/D</td>
<td>Columnas de versión de fila no se puede almacenar en el índice de búsqueda de hello, pero pueden usarse para el seguimiento de cambios</td>
</tr>
<tr>
<td>time, timespan<br>binary, varbinary, image,<br>xml, geometry, CLR types</td>
<td>N/D</td>
<td>No compatible</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>asignación entre tipos de datos de JSON y de Búsqueda de Azure
<table style="font-size:12">
<tr>
<td>Tipo de datos de JSON</td>    
<td>Tipos de campos de índice de destino permitidos</td>
<td>Notas</td>
</tr>
<tr>
<td>booleano</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Números enteros</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Números de punto flotante</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Matrices de tipos primitivos, por ejemplo "a", "b", "c"</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Cadenas que parecen fechas</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Objetos de punto de GeoJSON</td>
<td>Edm.GeographyPoint</td>
<td>Los puntos GeoJSON son objetos JSON en hello siguiendo el formato: {"tipo": "Point", "coordinates": [lat largo]} </td>
</tr>
<tr>
<td>Otros objetos JSON</td>
<td>N/D</td>
<td>No se admite; actualmente Búsqueda de Azure solo admite tipos primitivos y colecciones de cadenas</td>
</tr>
</table>
