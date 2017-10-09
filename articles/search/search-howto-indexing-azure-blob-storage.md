---
title: "aaaIndexing almacenamiento de blobs de Azure con búsqueda de Azure"
description: "Obtenga información acerca de cómo tooindex Azure Blob Storage y extraer el texto de documentos con búsqueda de Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Indexación de documentos en Almacenamiento de blobs de Azure con Búsqueda de Azure
Este artículo se muestra cómo tooindex documentos de toouse búsqueda de Azure (como PDF, documentos de Microsoft Office y otros formatos comunes) almacenados en el almacenamiento de blobs de Azure. En primer lugar, explican conceptos básicos de Hola de instalar y configurar un indizador de blob. A continuación, ofrece una exploración más profunda de comportamientos y escenarios son tooencounter probable.

## <a name="supported-document-formats"></a>Formatos de documento admitidos
indizador de blob de Hello puede extraer el texto de hello después de formatos de documento:

* PDF
* Formatos de Microsoft Office: DOC/DOCX XLSX, XLS y PPTX/PPT, MSG (correos electrónicos de Outlook)  
* HTML
* XML
* ZIP
* EML
* RTF
* Archivos de texto sin formato (vea también [Indexing plain text (Indexación de texto sin formato)](#IndexingPlainText))
* JSON (vea [Indexación de blobs JSON](search-howto-index-json-blobs.md))
* CSV (consulte la característica [Indexación de blobs CSV](search-howto-index-csv-blobs.md) en versión preliminar)

> [!IMPORTANT]
> La compatibilidad con matrices CSV y JSON está actualmente en fase de versión preliminar. Estos formatos son disponibles solo con la versión **2016-09-01-versión preliminar** de hello API de REST o versión 2.x-versión preliminar de hello .NET SDK. Por favor, recuerde que las versiones preliminares de las API están pensadas para realizar pruebas y evaluar, y no deben usarse en entornos de producción.
>
>

## <a name="setting-up-blob-indexing"></a>Configuración de la indexación de blob
Puede configurar un indexador de Azure Blob Storage utilizando:

* [Portal de Azure](https://ms.portal.azure.com)
* [API de REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) de Azure Search
* [SDK de .NET de Azure Search](https://aka.ms/search-sdk)

> [!NOTE]
> Algunas características (por ejemplo, las asignaciones de campos) todavía no están disponibles en el portal de Hola y tienen toobe utilizado mediante programación.
>
>

En este caso, mostramos cómo flujo hello mediante Hola API de REST.

### <a name="step-1-create-a-data-source"></a>Paso 1: Creación de un origen de datos
Un origen de datos especifica qué datos tooindex, los datos de hello tooaccess de credenciales necesarias y directivas tooefficiently identifican cambios en datos de hello (filas nuevas, modificadas o eliminadas). Se puede utilizar un origen de datos por varios indizadores en hello mismo servicio de búsqueda.

Para la indización de blobs, origen de datos de hello debe tener Hola propiedades necesarias siguientes:

* **nombre** es nombre único de Hola Hola del origen de datos dentro del servicio de búsqueda.
* **type** debe ser `azureblob`.
* **credenciales** proporciona la cadena de conexión de cuenta de almacenamiento de hello como hello `credentials.connectionString` parámetro. Vea [cómo toospecify credenciales](#Credentials) a continuación para obtener más información.
* **container** especifica un contenedor en la cuenta de almacenamiento. De forma predeterminada, todos los blobs en el contenedor de hello son recuperables. Si solo desea tooindex blobs en un directorio virtual determinado, puede especificar ese directorio mediante Hola opcional **consulta** parámetro.

toocreate un origen de datos:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Para obtener más información sobre Hola crear origen de datos API, vea [crear origen de datos](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>¿Cómo toospecify credenciales ####

Puede proporcionar credenciales de Hola Hola contenedor de blobs de una de estas maneras:

- **Cadena de conexión de la cuenta de almacenamiento de acceso completo**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Puede obtener cadena de conexión de Hola de hello portal de Azure desplazándose hoja de cuenta de almacenamiento de toohello > Configuración > claves (para cuentas de almacenamiento estándar) o configuración > claves (para cuentas de almacenamiento de Azure Resource Manager) de acceso.
- **Firma de acceso compartido de cuenta de almacenamiento** cadena de conexión (SAS): `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` Hola SAS debe tener Hola lista y permisos de lectura en contenedores y objetos (blobs en este caso).
-  **Firma de acceso compartido del contenedor**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` Hola SAS debe tener Hola lista y permisos de lectura en el contenedor de Hola.

Para más información sobre las firmas de acceso compartido, consulte [Uso de firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Si usa credenciales SAS, necesitará credenciales de origen de datos de tooupdate Hola periódicamente con firmas renovado tooprevent su caducidad. Si las credenciales de SA expiran, indizador Hola se producirá un error con un mensaje de error similar demasiado`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Paso 2: Creación de un índice
índice de Hola especifica campos hello en un documento, los atributos, y otras construcciones de esa experiencia de búsqueda de Hola de forma.

Le mostramos cómo toocreate un índice con una búsqueda `content` campo texto de hello toostore extraído de blobs:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Para obtener más información sobre la creación de índices, vea el artículo de [creación de índices](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Paso 3: Creación de un indexador
Un indizador que conecta a un origen de datos con un índice de búsqueda de destino y proporciona una actualización de datos de programación tooautomate Hola.

Una vez que se han creado el origen de datos e índices de hello, está listo toocreate indizador de hello:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Este indizador se ejecutará cada dos horas (intervalo de programación se establece demasiado "PT2H"). toorun un indizador cada 30 minutos, establezca el intervalo de saludo demasiado "PT30M". intervalo admitido de Hello más corta es 5 minutos. Hola programación es opcional: si se omite, un indizador que se ejecuta solo una vez cuando se crea. Sin embargo, puede ejecutarlo a petición en cualquier momento.   

Para obtener más detalles sobre Hola crear API de indizador, visite [crear indizador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Proceso mediante el cual Azure Search indiza los blobs

Función hello [configuración indexer](#PartsOfBlobToIndex), indizador de blob de hello puede indizar solo los metadatos de almacenamiento (resulta útil cuando la atención única sobre Hola metadatos y no es necesario tooindex Hola contenido de blobs), almacenamiento y contenido de los metadatos, o ambos metadatos y el contenido textual. De forma predeterminada, el indizador de Hola extrae metadatos y el contenido.

> [!NOTE]
> De forma predeterminada, se indexan blobs con contenido estructurado como JSON o CSV como un único fragmento de texto. Si desea tooindex JSON y CSV blobs de una manera estructurada, consulte [JSON de indización de blobs](search-howto-index-json-blobs.md) y [indización CSV blobs](search-howto-index-csv-blobs.md) características de vista previa.
>
> Un documento compuesto o insertado (por ejemplo, un archivo ZIP o un documento de Word con correo electrónico de Outlook insertado que contiene datos adjuntos) también se indexa como un solo documento.

* el contenido textual del documento de Hola Hola se extrae en un campo de cadena denominado `content`.

> [!NOTE]
> Búsqueda de Azure limita la cantidad de texto extrae según el nivel de precios de hello: 32.000 caracteres gratuitamente capa, 64.000 en Basic y 4 millones para los niveles estándar, estándar S2 y S3 estándar. Se incluye una advertencia en respuesta de estado de indizador de Hola para documentos truncados.  

* Propiedades de metadatos especificado por el usuario está presentes en el blob de hello, si los hay, se extraen literalmente.
* Propiedades de metadatos de blob estándar se extraen en hello siguientes campos:

  * **metadatos\_almacenamiento\_nombre** (Edm.String) - nombre de archivo de Hola de blob de Hola. Por ejemplo, si tiene un blob /my-container/my-folder/subfolder/resume.pdf, Hola valor de este campo es `resume.pdf`.
  * **metadatos\_almacenamiento\_ruta de acceso** (Edm.String) - Hola URI completo del blob de hello, incluida la cuenta de almacenamiento de Hola. Por ejemplo: `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **metadatos\_almacenamiento\_contenido\_tipo** (Edm.String) - tipo de contenido especificado por el código de hello usa el blob de hello tooupload. Por ejemplo: `application/octet-stream`.
  * **metadatos\_almacenamiento\_última\_modificar** (Edm.DateTimeOffset) - última modificación de marca de tiempo de blob de Hola. Búsqueda de Azure utiliza este blobs de tooidentify cambia de marca de tiempo, tooavoid indizar todo el contenido después de indizar inicial de Hola.
  * **metadata\_storage\_size** (Edm.Int64): Tamaño del blob en bytes.
  * **metadatos\_almacenamiento\_contenido\_md5** (Edm.String) - hash MD5 del contenido de blob de hello, si está disponible.
* Formato de documento de tooeach específico de propiedades de metadatos se extraen en campos de hello enumerados [aquí](#ContentSpecificMetadata).

No es necesario toodefine campos de hello anteriormente propiedades todos en el índice de búsqueda: simplemente capturar propiedades de Hola que necesita para la aplicación.

> [!NOTE]
> A menudo, los nombres de campo de hello en el índice existente será diferentes de los nombres de campo de hello generados durante la extracción del documento. Puede usar **campo asignaciones** nombres de propiedad de hello toomap proporcionados por los nombres de campo de búsqueda de Azure toohello en el índice de búsqueda. A continuación, verá un ejemplo del uso de las asignaciones de campos.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Definición de claves de documento y asignaciones de campos
Búsqueda de Azure, clave de documento de hello identifica de forma exclusiva un documento. Cada índice de búsqueda tiene que tener exactamente un campo de clave del tipo Edm.String. campo de clave de Hello es obligatorio para cada documento que se va a agregar el índice toohello (es realmente Hola único campo obligatorio).  

Debe considerar detenidamente qué campo extraído debe asignar el campo de clave de toohello para el índice. los candidatos de Hello son:

* **metadatos\_almacenamiento\_nombre** : Esto puede ser un candidato adecuado, pero tenga en cuenta que los nombres de 1) Hola no podrían ser únicos, como puede tener blobs con hello igual nombre en carpetas diferentes, y (2) Hola nombre puede contener caracteres que no son válidos en las claves de documento, como guiones. Para tratar con caracteres no válidos mediante el uso de hello `base64Encode` [función de asignación de campo](search-indexer-field-mappings.md#base64EncodeFunction) : si lo hace, recuerde las claves de documento tooencode al pasarlos en API llama como la búsqueda. (Por ejemplo, en .NET puede usar hello [método UrlTokenEncode](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) para ese fin).
* **metadatos\_almacenamiento\_ruta de acceso** : uso de ruta de acceso completa de hello garantiza la unicidad, pero definitivamente contiene la ruta de acceso de hello `/` caracteres que son [no válido en una clave de documento](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Como anteriormente, tiene la opción de Hola de codificación claves de hello mediante hello `base64Encode` [función](search-indexer-field-mappings.md#base64EncodeFunction).
* Si ninguna de las opciones de hello anteriores funciona, puede agregar un BLOB de toohello de propiedad de metadatos personalizados. Esta opción, sin embargo, requieren su tooadd de proceso de carga de blob que blobs tooall de propiedad de metadatos. Puesto que la clave de hello es una propiedad obligatoria, todos los blobs que no tienen dicha propiedad se producirá un error toobe indizado.

> [!IMPORTANT]
> Si no hay ninguna asignación explícita para el campo de clave de hello en el índice de hello, búsqueda de Azure utiliza automáticamente `metadata_storage_path` como Hola clave y Base64 codifica los valores de clave (Hola segunda opción anterior).
>
>

En este ejemplo, vamos a seleccionar hello `metadata_storage_name` campo como clave de documento de Hola. Supongamos también que el índice tiene un campo de clave denominado `key` y un campo `fileSize` para almacenar el tamaño del documento Hola. toowire las cosas como se esperaba, especifique Hola siguiendo las asignaciones de campos al crear o actualizar el indizador:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring de todos junto, aquí cómo puede agregar las asignaciones de campos y habilitar codificación de base 64 de claves para un indizador existente:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn más información acerca de las asignaciones de campos, vea [este artículo](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Control de qué blobs se indizan
Puede controlar qué blobs se indizan y cuáles se pasan por alto.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Solo los blobs Hola con determinadas extensiones de archivo de índice
Puede indizar solo blobs Hola con extensiones de nombre de archivo Hola se especifica mediante hello `indexedFileNameExtensions` parámetro de configuración del indizador. valor de Hello es una cadena que contiene una lista separada por comas de extensiones de archivo (con un punto inicial). Tooindex por ejemplo, hello única. PDF y. Los blobs DOCX, para ello:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>Exclusión de blobs con extensiones de archivo específicas
Puede excluir blobs con extensiones de nombre de archivo específico de indización mediante hello `excludedFileNameExtensions` parámetro de configuración. valor de Hello es una cadena que contiene una lista separada por comas de extensiones de archivo (con un punto inicial). Por ejemplo, tooindex todos los blobs excepto aquellos que tengan Hola. PNG y. Extensiones JPEG, para ello:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Si los dos parámetros `indexedFileNameExtensions` y `excludedFileNameExtensions` están presentes, Búsqueda de Azure mira primero en `indexedFileNameExtensions` y, luego, en `excludedFileNameExtensions`. Esto significa que si hello misma extensión de archivo está presente en las dos listas, se excluirán de la indización.

### <a name="dealing-with-unsupported-content-types"></a>Operaciones con tipos de contenido no admitidos

De forma predeterminada, indizador de blob de hello detiene tan pronto como encuentra un blob con un tipo de contenido no admitido (por ejemplo, una imagen). Por supuesto puede usar hello `excludedFileNameExtensions` parámetro tooskip ciertos tipos de contenido. Sin embargo, deberá tooindex blobs sin conocer de antemano todos Hola posibles tipos de contenido. toocontinue indización cuando se encuentra un tipo de contenido no admitido, establezca hello `failOnUnsupportedContentType` parámetro de configuración demasiado`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Omisión de errores de análisis

Azure lógica de extracción de búsqueda de documento no es perfecta y a veces producirá un error tooparse documentos de un tipo de contenido admitido, como. DOCX o. PDF. Si no desea hello toointerrupt indización en tales casos, establezca hello `maxFailedItems` y `maxFailedItemsPerBatch` valores razonables de toosome de parámetros de configuración. Por ejemplo:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Controlar qué partes del blob de Hola se indizan

Puede controlar qué partes de blobs de Hola se indizan mediante hello `dataToExtract` parámetro de configuración. Puede tomar Hola siguientes valores:

* `storageMetadata`-Especifica que solo hello [propiedades de blob estándar y los metadatos especificados por el usuario](../storage/blobs/storage-properties-metadata.md) se indizan.
* `allMetadata`-Especifica que los metadatos almacenamiento hello y [metadatos específicos del tipo de contenido](#ContentSpecificMetadata) extraído de blob de Hola se indizan contenido.
* `contentAndMetadata`: Especifica que se indizan todos los metadatos y el contenido textual extraídos de blob de Hola. Se trata de un valor predeterminado de Hola.

Por ejemplo, tooindex solo Hola metadatos de almacenamiento, use:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>Uso de toocontrol de metadatos de blob cómo se indizan blobs

tooall blobs aplican los parámetros de configuración de Hola que se ha descrito anteriormente. En ocasiones, puede que desee toocontrol cómo *blobs individuales* se indizan. Puede hacerlo agregando Hola siguientes propiedades de metadatos y los valores de blobs:

| Nombre de propiedad | Valor de la propiedad | Explicación |
| --- | --- | --- |
| AzureSearch_Skip |"true" |Indica el blob de hello blob indizador toocompletely skip Hola. No se trata de realizar la extracción de metadatos ni del contenido. Esto es útil cuando un blob determinado se produce un error repetidamente e interrumpe el proceso de indización de Hola. |
| AzureSearch_SkipContent |"true" |Esto es equivalente de `"dataToExtract" : "allMetadata"` configuración describe [anteriormente](#PartsOfBlobToIndex) tooa ámbito determinado blob. |

## <a name="incremental-indexing-and-deletion-detection"></a>Indexación incremental y detección de eliminación
Cuando configura un toorun de indizador de blob según una programación, vuelve a indizar sólo Hola cambiado blobs, según lo determinado por la del blob de hello `LastModified` marca de tiempo.

> [!NOTE]
> No tiene una directiva de detección de cambios toospecify: indización incremental se habilita automáticamente.

toosupport eliminar los documentos, usar un enfoque de "eliminación temporal". Si elimina blobs Hola directamente, documentos correspondientes no se quitará del índice de búsqueda de Hola. En su lugar, use Hola pasos:  

1. Agregar un blob tooindicate tooAzure búsqueda que lógicamente se elimina de metadatos personalizados propiedad toohello
2. Configurar una directiva de detección de eliminación de software en el origen de datos de Hola
3. Una vez que el indizador de hello ha procesado el blob de hello (tal y como se muestra en el estado del indizador Hola API), puede eliminar físicamente blob Hola

Por ejemplo, hello después directiva considera que un toobe blob eliminado si tiene una propiedad de metadatos `IsDeleted` con el valor de Hola `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Indización de grandes conjuntos de datos

La indización de blobs puede ser un proceso lento. En casos donde haya millones de tooindex de blobs, puede acelerar la indización de los datos de creación de particiones y usar varios indizadores tooprocess Hola de datos en paralelo. Le mostramos cómo puede configurar esta opción:

- Divida los datos en varios contenedores de blobs o carpetas virtuales.
- Configure varios orígenes de datos de Azure Search, uno por cada contenedor o carpeta. carpeta de blobs de toopoint tooa, use hello `query` parámetro:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Cree un indizador correspondiente a cada origen de datos. Todos Hola indizadores pueden punto toohello mismo índice de búsqueda de destino.  

- Una unidad de búsqueda del servicio puede ejecutar un indexador en cualquier momento dado. La creación de varios indexadores como se ha descrito arriba solo es útil si se ejecutan realmente en paralelo. toorun varios indizadores en paralelo, escalar el servicio de búsqueda mediante la creación de un número adecuado de particiones y réplicas. Por ejemplo, si su servicio de búsqueda tiene 6 unidades de búsqueda (por ejemplo, las réplicas de 2 particiones x 3), a continuación, 6 indizadores pueden ejecutar al mismo tiempo, lo que produce un aumento de seis veces en el rendimiento de la indexación Hola. toolearn más información acerca de ajuste de escala y planear la capacidad, consulte [escalar los niveles de recursos de consulta e indización cargas de trabajo en búsqueda de Azure](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Indización de los documentos con datos relacionados

Puede que desee "ensamblar" demasiado documentos de varios orígenes en el índice. Por ejemplo, puede que desee toomerge texto de blobs con otros metadatos almacenados en la base de datos de Cosmos. Incluso puede utilizar Hola inserción API indización junto con varios indizadores acumular demasiado buscar documentos de varias partes. 

Para este toowork, todos los indizadores y otros componentes deben tooagree en clave de documento de Hola. Para obtener un tutorial detallado, vea este artículo externo: [Combine documents with other data in Azure Search (Combinación de documentos con otros datos en Azure Search)](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Indexación de texto sin formato 

Si todos los blobs contienen texto sin formato en hello misma codificación, puede mejorar significativamente el rendimiento indización mediante el uso de **análisis de modo de texto**. texto toouse análisis modo, conjunto hello `parsingMode` propiedad de configuración demasiado`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

De forma predeterminada, Hola `UTF-8` se supone la codificación. toospecify una codificación diferente, utilice hello `encoding` propiedad de configuración: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Propiedades de metadatos específicas del tipo de contenido
Hello tabla siguiente resume el procesamiento realizado para cada formato de documento y describe las propiedades de metadatos de hello extraídas por búsqueda de Azure.

| Formato de documento/Tipo de contenido | Propiedades de metadatos específicas del tipo de contenido | Detalles de procesamiento |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Seccionar el marcado HTML y extraer texto |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Extraer texto, incluyendo los documentos insertados (excepto las imágenes) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Extraer texto, incluyendo los documentos insertados |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Extraer texto, incluyendo los documentos insertados |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Extraer texto, incluyendo los documentos insertados |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Extraer texto, incluyendo los documentos insertados |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Extraer texto, incluyendo los documentos insertados |
| PPT (application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Extraer texto, incluyendo los documentos insertados |
| MSG (application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Extraer texto, incluidos los datos adjuntos |
| ZIP (application/zip) |`metadata_content_type` |Extraer el texto de todos los documentos en el archivo de Hola |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Seccionar el marcado XML y extraer texto |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Extraer texto<br/>Nota: Si necesita tooextract documento varios campos de un blob JSON, consulte [indización JSON blobs](search-howto-index-json-blobs.md) para obtener más información |
| EML (message/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Extraer texto, incluidos los datos adjuntos |
| RTF (aplicación/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Extraer texto|
| Plain text (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Extraer texto|


## <a name="help-us-make-azure-search-better"></a>Ayúdenos a mejorar Búsqueda de Azure
Si tiene solicitudes o ideas para mejorar las características, remítalas en [UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
