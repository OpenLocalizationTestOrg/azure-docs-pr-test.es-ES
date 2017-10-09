---
title: "asignaciones de aaaField en los indizadores de búsqueda de Azure"
description: "Configurar asignaciones de campo de búsqueda de Azure indizador tooaccount las diferencias en las representaciones de datos y nombres de campo"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Asignaciones de campos en los indexadores de Azure Search
Al utilizar indizadores de búsqueda de Azure, en ocasiones puede encontrar usted mismo en situaciones donde los datos de entrada no coincide bastante con esquema Hola de su índice de destino. En esos casos, puede usar **campo asignaciones** tootransform los datos en hello deseado forma.

Algunas situaciones donde las asignaciones de campos son útiles:

* Su origen de datos tiene un campo `_id`, pero Búsqueda de Azure no permite los nombres de campo que empiezan por un carácter de subrayado. Permite que una asignación de campo demasiado "cambia el nombre de" un campo.
* Desea toopopulate varios campos en hello indizarán con hello mismos datos del origen de datos, por ejemplo porque desea tooapply diferentes analizadores toothose campos. Las asignaciones de campos permiten "bifurcar" un campo de origen de datos.
* Necesita tooBase64 codificar o descodificar los datos. Las asignaciones de campos admiten varias **funciones de asignación**, incluidas las funciones de codificación y descodificación Base64.   

## <a name="setting-up-field-mappings"></a>Configuración de asignaciones de campos
Puede agregar las asignaciones de campos al crear un nuevo indizador mediante hello [crear indizador](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. Puede administrar las asignaciones de campos en un indizador de indización mediante hello [actualización indizador](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Una asignación de campos consta de 3 partes:

1. `sourceFieldName`, que representa un campo de su origen de datos. Esta propiedad es obligatoria.
2. `targetFieldName`opcional, que representa un campo de su índice de búsqueda. Si se omite, Hola el mismo nombre que en Hola se utiliza el origen de datos.
3. `mappingFunction`opcional, que puede transformar sus datos con una de las diversas funciones predefinidas. Hola lista completa de funciones es [a continuación](#mappingFunctions).

Asignaciones de campos se agregan toohello `fieldMappings` matriz en la definición de indizador de Hola.

Por ejemplo, así es como puede adaptarse a las diferencias existentes en los nombres de campo:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Un indexador puede tener varias asignaciones de campos. Por ejemplo, así es como puede "bifurcar" un campo:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Búsqueda de Azure usa nombres de campo y la función de la Hola del tooresolve comparación entre mayúsculas y minúsculas en las asignaciones de campos. Esto resulta útil (no es necesario tooget todas Hola mayúsculas y minúsculas derecha), pero significa que el origen de datos o un índice no puede tener campos que se diferencian sólo por mayúsculas o minúsculas.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Funciones de asignación de campos
Actualmente se admiten estas funciones:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Realiza *seguridad de direcciones URL* codificación Base64 del programa Hola a la cadena de entrada. Supone que Hola entrada con codificación UTF-8.

#### <a name="sample-use-case"></a>Caso de uso de ejemplo
Solo pueden aparecer caracteres de seguridad de direcciones URL en una clave de documento de búsqueda de Azure (dado que los clientes deben ser tooaddress capaz de documento de hello mediante Hola API de búsqueda, por ejemplo). Si los datos contienen caracteres no seguros la dirección URL y se desea toouse toopopulate un campo de clave en el índice de búsqueda, use esta función.   

#### <a name="example"></a>Ejemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Realiza descodificación en Base64 de la cadena de entrada de Hola. Hello entrada se supone tooa *seguridad de direcciones URL* cadena codificada en Base64.

#### <a name="sample-use-case"></a>Caso de uso de ejemplo
Los valores de metadatos personalizados del blob deben tener codificación ASCII. Puede usar Base64 codificación toorepresent arbitrario las cadenas Unicode en los metadatos personalizados de blob. Sin embargo, toomake búsqueda significativo, se puede usar esta función tooturn Hola codificado datos en las cadenas "normales" al rellenar el índice de búsqueda.  

#### <a name="example"></a>Ejemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Divide un campo de cadena con hello especifica delimitador y recoge Hola símbolo (token) en Hola posición especificada de la división de hello resultante.

Por ejemplo, si hello entrada es `Jane Doe`, hello `delimiter` es `" "`(espacio) hello y `position` es 0, el resultado de hello es `Jane`; si hello `position` es 1, el resultado de hello es `Doe`. Si la posición de hello hace referencia token tooa que no existe, se devolverá un error.

#### <a name="sample-use-case"></a>Caso de uso de ejemplo
El origen de datos contiene un `PersonName` campo y desea que tooindex como dos `FirstName` y `LastName` campos. Puede usar este hello toosplit de función mediante el carácter de espacio de hello como Hola delimitador de entrada.

#### <a name="parameters"></a>parameters
* `delimiter`: una toouse de cadena como separador de hello cuando dividir Hola la cadena de entrada.
* `position`: se divide una posición de base cero de entero de hello token toopick después de hello la cadena de entrada.    

#### <a name="example"></a>Ejemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Transformaciones de cadena con formato como una matriz JSON de cadenas en una matriz de cadenas que puede ser utilizado toopopulate un `Collection(Edm.String)` campo índice Hola.

Por ejemplo, si la cadena de entrada de hello es `["red", "white", "blue"]`, Hola de campo de destino de tipo `Collection(Edm.String)` se rellenará con valores de hello tres `red`, `white` y `blue`. En el caso de los valores de entrada que no pueden analizarse como matrices de cadenas JSON, se devolverá un error.

#### <a name="sample-use-case"></a>Caso de uso de ejemplo
La base de datos SQL Azure no tiene un tipo de datos integrado que naturalmente se asigna demasiado`Collection(Edm.String)` campos de búsqueda de Azure. toopopulate campos de la colección de cadenas, dar formato a los datos de origen como una matriz de cadena JSON y usar esta función.

#### <a name="example"></a>Ejemplo
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Ayúdenos a mejorar Búsqueda de Azure
Si dispone de las solicitudes de características o ideas para mejoras, póngase en contacto toous en nuestra [sitio UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
