---
title: "aaaIndexing almacenamiento de tabla de Azure con búsqueda de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se almacenan los datos de tooindex en almacenamiento de tabla de Azure con búsqueda de Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Indexación de Azure Table Storage con Azure Search
Este artículo muestra cómo se almacena los toouse datos tooindex de búsqueda de Azure en almacenamiento de tabla de Azure.

## <a name="set-up-azure-table-storage-indexing"></a>Configuración de la indexación de Azure Table Storage

Puede configurar un indexador de Azure Table Storage mediante estos recursos:

* [Portal de Azure](https://ms.portal.azure.com)
* [API de REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) de Azure Search
* [SDK de .NET de Azure Search](https://aka.ms/search-sdk)

Aquí mostramos cómo Hola flujo mediante el uso de hello API de REST. 

### <a name="step-1-create-a-datasource"></a>Paso 1: Creación de un origen de datos

Un origen de datos especifica qué datos tooindex, hello requieren credenciales tooaccess datos de Hola y directivas de Hola que habilitar la búsqueda de Azure tooefficiently identifican cambios en los datos de Hola.

Para la indización de la tabla, el origen de datos de hello debe tener Hola propiedades siguientes:

- **nombre** es Hola nombre único del origen de datos de hello dentro del servicio de búsqueda.
- **type** debe ser `azuretable`.
- **credenciales** parámetro contiene la cadena de conexión de cuenta de almacenamiento de Hola. Vea hello [especificar credenciales](#Credentials) sección para obtener más información.
- **contenedor** Hola de conjuntos de nombre de la tabla y una consulta opcional.
    - Especificar el nombre de la tabla de hello mediante hello `name` parámetro.
    - Si lo desea, especifique una consulta mediante el uso de hello `query` parámetro. 

> [!IMPORTANT] 
> Siempre que sea posible, utilice un filtro en PartitionKey para mejorar el rendimiento. Cualquier otra consulta realiza un examen de toda la tabla, lo que produce un rendimiento deficiente de las tablas grandes. Vea hello [consideraciones de rendimiento](#Performance) sección.


toocreate un origen de datos:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Para obtener más información sobre Hola crear origen de datos API, consulte [crear origen de datos](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Credenciales de toospecify de formas ####

Puede proporcionar credenciales de hello para la tabla de hello en una de estas maneras: 

- **Cadena de conexión de cuenta de almacenamiento de acceso completo**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` puede obtener cadena de conexión de Hola de hello portal de Azure va toohello **hoja de la cuenta de almacenamiento** > **configuración**   >  **Claves** (para cuentas de almacenamiento clásicas) o **configuración** > **las claves de acceso** (para recursos de Azure Cuentas de almacenamiento de administrador).
- **Cuenta de almacenamiento compartido de cadena de conexión de firma de acceso**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` firma de acceso compartido de hello debe tener Hola lista y permisos de lectura en contenedores (tablas en este caso) y objetos (filas de tabla).
-  **Firma de acceso compartido de tabla**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` firma de acceso compartido de hello debe tener permisos de consulta (lectura) en la tabla de Hola.

Para más información sobre las firmas de acceso compartido de almacenamiento, consulte [Uso de firmas de acceso compartido (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Si usa credenciales de firma de acceso compartido, necesitará credenciales de origen de datos de hello tooupdate periódicamente con firmas renovado tooprevent su caducidad. Si las credenciales de firma de acceso compartido expiran, indizador Hola se produce un error con un mensaje de error similar demasiado "credenciales proporcionadas en la cadena de conexión de hello no son válidas o que han expirado."  

### <a name="step-2-create-an-index"></a>Paso 2: Creación de un índice
índice de Hola especifica campos hello en un documento, los atributos de hello, y otras construcciones de esa experiencia de búsqueda de Hola de forma.

toocreate un índice:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Para más información sobre la creación de índices, consulte [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index) (Creación de un índice).

### <a name="step-3-create-an-indexer"></a>Paso 3: Creación de un indexador
Un indizador que conecta a un origen de datos con un índice de búsqueda de destino y proporciona una actualización de datos de programación tooautomate Hola. 

Después de crean origen de datos y el índice de hello, está listo toocreate indizador de hello:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Este indexador se ejecuta cada dos horas. (intervalo de programación de saludo se establece demasiado "PT2H".) toorun un indizador cada 30 minutos, establezca el intervalo de saludo demasiado "PT30M". intervalo admitido de Hello más corta es cinco minutos. programación de Hello es opcional; Si se omite, un indizador que se ejecuta solo una vez cuando se crea. Sin embargo, puede ejecutarlo a petición en cualquier momento.   

Para obtener más información sobre Hola indizador crear API, consulte [crear indizador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Trabajo con distintos nombres de campos
En ocasiones, los nombres de campo de hello en el índice existente son diferentes de los nombres de propiedad de hello en la tabla. Puede usar nombres de propiedad de campo asignaciones toomap Hola Hola tabla toohello nombres de campo en el índice de búsqueda. toolearn más información acerca de las asignaciones de campos, vea [asignaciones de campos de indizador de búsqueda de Azure salvar las diferencias de hello entre orígenes de datos y búsqueda de índices](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Trabajo con claves de documento
Búsqueda de Azure, clave de documento de hello identifica de forma exclusiva un documento. Cada índice de búsqueda debe tener exactamente un campo clave de tipo `Edm.String`. campo de clave de Hello es obligatorio para cada documento que se va a agregar toohello índice. (De hecho, su Hola solo campo obligatorio.)

Como las filas de tablas tienen una clave compuesta, Azure Search genera un campo sintético llamado `Key`, que es una concatenación de valores de clave de partición y clave de fila. Por ejemplo, si una fila de la PartitionKey es `PK1` y RowKey es `RK1`, a continuación, Hola `Key` es el valor del campo `PK1RK1`.

> [!NOTE]
> Hola `Key` valor puede contener caracteres que no son válidos en las claves de documento, como guiones. Para tratar con caracteres no válidos mediante el uso de hello `base64Encode` [función de asignación de campo](search-indexer-field-mappings.md#base64EncodeFunction). Si lo hace, recuerde tooalso use Base64 de seguridad de la dirección URL una codificación al pasar las claves de documento en la API llama como la búsqueda.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Indexación incremental y detección de eliminación
Cuando configura un toorun de indizador de tabla según una programación, indexar filas sólo nuevos o actualizados, determinado por una fila `Timestamp` valor. No tienes toospecify una directiva de detección de cambios. La indexación incremental se habilita automáticamente.

tooindicate que algunos documentos se deben quitar del índice de hello, puede usar una estrategia de eliminación temporal. En lugar de eliminar una fila, agregue un tooindicate de propiedad que ha eliminado y configurar una directiva de detección de eliminación de software en el origen de datos de Hola. Por ejemplo, hello después directiva considera que se elimina una fila si la fila de hello tiene una propiedad `IsDeleted` con el valor de Hola `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Consideraciones sobre rendimiento

De forma predeterminada, la búsqueda de Azure usa Hola después de filtro de consulta: `Timestamp >= HighWaterMarkValue`. Dado que las tablas de Azure no tienen un índice secundario en hello `Timestamp` campo, este tipo de consulta requiere un recorrido de tabla completa y, por tanto, es lento para tablas de gran tamaño.


Aquí hay dos posibles enfoques para mejorar el rendimiento de la indexación de tablas. Ambos se basan en el uso de particiones de tabla: 

- Si los datos se pueden dividir de forma natural en varios intervalos de partición, cree un origen de datos y un indexador correspondiente para cada intervalo de partición. Ahora, cada indizador tiene tooprocess sólo un intervalo de partición específica, lo que produce un mejor rendimiento de las consultas. Si los datos de Hola que necesita toobe indizada tienen un pequeño número de particiones fijos, incluso mejores: cada indizador solo realiza un recorrido de la partición. Por ejemplo, toocreate un origen de datos para el procesamiento de un intervalo de partición con las claves de `000` demasiado`100`, utilice una consulta como esta: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Si los datos se partición por tiempo (por ejemplo, crear una nueva partición cada día o semana), considere la posibilidad de hello enfoque: 
    - Usar una consulta de forma de hello: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Supervisar el progreso de indizador mediante [obtener API de estado de indizador](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)y actualizar periódicamente hello `<TimeStamp>` condición de consulta de hello basada en hello más reciente correcta marca de agua de alto valor. 
    - Con este enfoque, si necesita tootrigger un indizar completa, debe consulta de origen de datos de hello tooreset de indizador de suma tooresetting Hola. 


## <a name="help-us-make-azure-search-better"></a>Ayúdenos a mejorar Búsqueda de Azure
Si tiene solicitudes o ideas para mejorar las características, envíelas en el [sitio de UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
