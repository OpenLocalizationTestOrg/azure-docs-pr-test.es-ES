---
title: "Inicio rápido: API Recomendaciones de Azure Machine Learning (ver. 1)| Microsoft Docs"
description: "Recomendaciones de aprendizaje automática de Azure - Guía de inicio rápido"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a>Guía de inicio rápido de hello (versión 1) de la API de recomendaciones de aprendizaje de máquina

> [!NOTE]
> Debería empezar a utilizar hello [recomendaciones API cognitivos servicio](https://www.microsoft.com/cognitive-services/recommendations-api) en lugar de esta versión. Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe. Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.
>
> Obtenga más información sobre [toohello de migración nuevo servicio cognitivos](http://aka.ms/recomigrate).
> 
> 

Este documento se describe cómo tooonboard su servicio o aplicación toouse recomendaciones de aprendizaje de máquina de Microsoft Azure. Puede encontrar más detalles en hello API recomendaciones en hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>Información general
toouse recomendaciones de aprendizaje de máquina de Azure, necesita hello tootake pasos:

* Crear un modelo: un modelo es un contenedor de datos de uso, datos del catálogo y del modelo de recomendación de Hola.
* Importar datos de catálogo: un catálogo contienen información de metadatos en los elementos de Hola. 
* Importar datos de uso: los datos de uso se pueden cargar en una de las dos formas siguientes (o ambas):
  * Si carga un archivo que contiene datos de uso de saludo.
  * Mediante el envío de eventos de adquisición de datos.
    Normalmente carga un archivo de uso en orden toobe puede toocreate un modelo de recomendación inicial (arranque) y usarlo hasta que el sistema de hello recopila suficientes datos con formato de adquisición de datos de Hola.
* Crear un modelo de recomendación: se trata de una operación asincrónica en qué Hola sistema recomendación toma todos los datos de uso de Hola y crea un modelo de recomendación. Esta operación puede tardar varios minutos o varias horas, según Hola parámetros de configuración de compilación de tamaño de datos de Hola y Hola. Cuando se desencadenan compilación hello, obtendrá un identificador de compilación. Usar toocheck al proceso de compilación de hello ha finalizado antes de iniciar tooconsume recomendaciones.
* Recomendaciones de uso: obtenga recomendaciones para un elemento específico o una lista de elementos.

Todos los pasos de hello anteriores se realizan a través de hello API de recomendaciones de aprendizaje de máquina de Azure.  Puede descargar una aplicación de ejemplo que implementa cada uno de estos pasos de hello [así la galería.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>Limitaciones
* número máximo de Hola de modelos por suscripción es 10.
* número máximo de Hola de elementos que puede contener un catálogo es 100.000.
* número máximo de Hola de puntos de uso que se mantienen es ~ 5 000 000. Hola más antigua se eliminará si nuevos se cargan o se notificarán.
* tamaño máximo de Hola de datos que se pueden enviar en POST (por ejemplo, importar datos del catálogo, importar datos de uso) es 200MB.
* Hello número de transacciones por segundo para una compilación de modelo de recomendación que no está activa es ~ 2TPS. Una compilación de modelo de recomendación que está activa puede contener una too20TPS.

## <a name="integration"></a>Integración
### <a name="authentication"></a>Autenticación
Microsoft Azure Marketplace es compatible con cualquier método de autenticación básica o OAuth Hola. Puedes buscar fácilmente Hola claves de cuenta desplazándose toohello claves en marketplace de hello en [la configuración de la cuenta](https://datamarket.azure.com/account/keys). 

#### <a name="basic-authentication"></a>Autenticación básica
Agregar encabezado de autorización de hello:

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

Convertir tooBase64 (C#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

Convertir tooBase64 (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>URI de servicio
Hola URI raíz del servicio para las API de Azure Machine Learning recomendaciones hello es [aquí.](https://api.datamarket.azure.com/amla/recommendations/v2/)

URI del servicio completo Hola se expresa mediante elementos de especificación de OData de Hola.

### <a name="api-version"></a>Versión de API
Cada llamada a la API tendrá, al final de hello, un parámetro de consulta denominado valor apiVersion que se debe establecer demasiado "1.0".

### <a name="ids-are-case-sensitive"></a>Los identificadores distinguen mayúsculas de minúsculas
Identificadores, devueltos por cualquiera de hello API, distinguen mayúsculas de minúsculas y deben usarse como tales cuando se pasan como parámetros en llamadas posteriores a la API. Por ejemplo, los identificadores de modelo y de catálogo distinguen mayúsculas de minúsculas.

### <a name="create-a-model"></a>Crear un modelo
Creación de una solicitud de "creación de modelo":

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelName |Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).<br>Longitud máxima: 20 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

* `feed/entry/content/properties/id`-Contiene el identificador del modelo Hola.
  Tenga en cuenta que el Id. de modelo de hello distingue mayúsculas de minúsculas.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a>Importar datos de catálogo
Si va a cargar varias catálogo archivos toohello mismo modelo con varias llamadas, insertamos solo Hola nuevos elementos de catálogo. Los elementos existentes permanecerán con valores originales de Hola.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de hello (distingue mayúsculas de minúsculas) |
| filename |Identificador textual del catálogo de Hola.<br>Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).<br>Longitud máxima: 50 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |Datos del catálogo. Formato:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Nombre</th><th>Obligatorio</th><th>Tipo</th><th>Description</th></tr><tr><td>Id. de elemento</td><td>yes</td><td>Alfanumérico, longitud máxima 50</td><td>Identificador único de un elemento</td></tr><tr><td>Nombre del elemento</td><td>Sí</td><td>Alfanumérico, longitud máxima 255</td><td>Nombre del elemento</td></tr><tr><td>Categoría del elemento</td><td>Sí</td><td>Alfanumérico, longitud máxima 255</td><td>Toowhich categoría que este elemento pertenece (por ejemplo, libros de cocina, series...)</td></tr><tr><td>Descripción</td><td>No</td><td>Alfanumérico, longitud máxima 4000</td><td>Descripción de este elemento</td></tr></table><br>El tamaño máximo de archivo es de 200 MB.<br><br>Ejemplo:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**Respuesta**:

código de estado HTTP: 200

* `Feed\entry\content\properties\LineCount` : número de líneas aceptadas.
* `Feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a>Importar datos de uso
#### <a name="uploading-a-file"></a>Carga de un archivo
Esta sección se muestra cómo los datos de uso de tooupload mediante un archivo. Puede llamar a esta API varias veces con datos de uso. Todos los datos de uso se guardarán para todas las llamadas.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de hello (distingue mayúsculas de minúsculas) |
| filename |Identificador textual del catálogo de Hola.<br>Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).<br>Longitud máxima: 50 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |Datos de uso. Formato:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nombre</th><th>Obligatorio</th><th>Tipo</th><th>Description</th></tr><tr><td>Id. de usuario</td><td>Sí</td><td>Alfanuméricas</td><td>Identificador único de un usuario</td></tr><tr><td>Id. de elemento</td><td>yes</td><td>Alfanumérico, longitud máxima 50</td><td>Identificador único de un elemento</td></tr><tr><td>Hora</td><td>No</td><td>La fecha en este formato: AAAA/MM/DDTHH:MM:SS (por ejemplo, 2013/06/20T10:00:00)</td><td>Hora de los datos</td></tr><tr><td>Evento</td><td>No, si se suministra también se debe colocar la fecha</td><td>Uno de hello siguientes:<br>• Click<br>• RecommendationClick<br>•    AddShopCart<br>• RemoveShopCart<br>• compra</td><td></td></tr></table><br>El tamaño máximo de archivo es de 200 MB.<br><br>Ejemplo:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Respuesta**:

código de estado HTTP: 200

* `Feed\entry\content\properties\LineCount` : número de líneas aceptadas.
* `Feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.
* `Feed\entry\content\properties\FileId` : identificador de archivo.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a>Utilizar la adquisición de datos
Esta sección muestra cómo toosend eventos real hora de recomendaciones de aprendizaje de máquina tooAzure, normalmente desde su sitio Web.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Request body |Entrada de datos de evento para cada evento que desee toosend. Debe enviar para la misma sesión de usuario o el Examinador de Hola Hola mismo identificador en el campo de SessionId Hola. (Vea el ejemplo del cuerpo de evento aparece a continuación). |

* Ejemplo para evento 'Click':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Ejemplo para evento 'RecommendationClick':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Ejemplo para evento 'AddShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Ejemplo para evento 'RemoveShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Ejemplo para el evento “Purchase”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* Ejemplo con envío de 2 eventos, 'Click' y 'AddShopCart':
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Respuesta**: código de estado HTTP: 200

### <a name="build-a-recommendation-model"></a>Compilar un modelo de recomendación
| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de hello (distingue mayúsculas de minúsculas) |
| userDescription |Identificador textual del catálogo de Hola. Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %. Vea el ejemplo anterior.<br>Longitud máxima: 50 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

Se trata de una API asincrónica. Obtendrá un Id. de compilación como respuesta. tooknow cuando ha finalizado la generación de hello, debe llamar a la API de "Obtener compilaciones estado de un modelo de" hello y busque este Id. de compilación en la respuesta de Hola. Tenga en cuenta que una compilación puede tardar desde toohours minutos según el tamaño de Hola de datos de Hola.

No se puede consumir recomendaciones hasta Hola crear extremos.

Estado de compilación válido:

* Crear: se creó el modelo.
* Queued: se desencadenó la compilación del modelo y está en la cola.
* Building: el modelo se está compilando.
* Success: la compilación finalizó correctamente.
* Error: la compilación finalizó con un error.
* Cancelled: la compilación se canceló.
* Cancelling: la compilación se está cancelando.

Tenga en cuenta esa compilación Hola que identificador puede encontrarse en hello siguiendo la ruta de acceso:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a>Obtención del estado de compilación de un modelo
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de hello (distingue mayúsculas de minúsculas) |
| onlyLastBuild |Indica si tooreturn Hola a todos crear historial de modelo de Hola o solo de estado de Hola de compilación más reciente de Hola. |
| apiVersion |1.0 |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada compilación. Cada entrada tiene Hola datos siguientes:

* `feed/entry/content/properties/UserName`: Nombre de usuario de Hola.
* `feed/entry/content/properties/ModelName`: Nombre del modelo de Hola.
* `feed/entry/content/properties/ModelId` : identificador único de modelo.
* `feed/entry/content/properties/IsDeployed`: Si se implementa compilación hello (conocido como) compilación activa).
* `feed/entry/content/properties/BuildId` : identificador único de compilación.
* `feed/entry/content/properties/BuildType`-Tipo de compilación de Hola.
* `feed/entry/content/properties/Status` : estado de la compilación. Puede ser uno de los siguientes de hello: Error, creación, en cola, Cancelar, cancelado, correcto
* `feed/entry/content/properties/StatusMessage`: Mensaje de estado detallado (se aplica solo toospecific estados).
* `feed/entry/content/properties/Progress` : progreso de la compilación (%).
* `feed/entry/content/properties/StartTime` : hora de inicio de la compilación.
* `feed/entry/content/properties/EndTime` : hora de finalización de la compilación.
* `feed/entry/content/properties/ExecutionTime` : duración de la compilación.
* `feed/entry/content/properties/ProgressStep`– Detalles acerca de la fase actual de Hola que una compilación en curso se encuentra en.

Estado de compilación válido:

* Creado: se creó la entrada de solicitud de compilación.
* En cola: la solicitud de compilación se ha desencadenado y puesto en cola.
* Compilando: la compilación está en curso.
* Success: la compilación finalizó correctamente.
* Error: la compilación finalizó con un error.
* Cancelled: la compilación se canceló.
* Cancelling: la compilación se está cancelando.

Valores válidos para el tipo de compilación:

* Rango: compilación de rango. (Para rango detalles de la compilación, consulte toohello documento de "Documentación de recomendación de aprendizaje de máquina API").
* Recomendación: compilación de recomendación.
* Fbt: compilación que con frecuencia se compra junta.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a>Obtención de recomendaciones
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de hello (distingue mayúsculas de minúsculas) |
| itemIds |Lista separada por comas de hello elementos toorecommend para.<br>Longitud máxima: 1024 |
| numberOfResults |Número de resultados requeridos |
| includeMetatadata |Uso futuro, siempre es false |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning`: razonamiento de la recomendación (por ejemplo, explicaciones de la recomendación).

OData XML

respuesta de ejemplo de Hola siguiente incluye 10 elementos recomendados:

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a>Actualización del modelo
Puede actualizar la descripción del modelo de Hola u Hola Id. de compilación activa.
*Id. de compilación activa*: cada compilación para cada modelo tiene un identificador de compilación. Id. de compilación activa de Hello es primera compilación correcta Hola de cada nuevo modelo. Una vez que tiene un identificador de compilación activa y hace que las compilaciones adicionales de Hola mismo modelo, deberá tooexplicitly establézcala como hello predeterminado Id. de compilación si desea. Cuando utilizas recomendaciones, si no especifica el Id. de generación de Hola que desee toouse, predeterminado Hola uno se usará automáticamente.

Este mecanismo le permite - una vez que tiene un modelo de recomendación en producción - toobuild nuevos modelos y probarlas antes de promover ellos tooproduction.

| Método HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| id |Identificador único del modelo de hello (distingue mayúsculas de minúsculas) |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>Tenga en cuenta que Hola XML etiquetas descripción y ActiveBuildId son opcionales. Si no desea tooset descripción o ActiveBuildId, quite la etiqueta completa Hola. |

**Respuesta**:

código de estado HTTP: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>Información legal
Este documento se ofrece "tal cual". La información y las opiniones expresadas en este documento, como las direcciones URL y otras referencias a sitios web de Internet, pueden cambiar sin previo aviso. Algunos ejemplos mencionados se proporcionan únicamente con fines ilustrativos y son ficticios. No se pretende ninguna asociación o conexión real ni debe deducirse. Este documento no proporcionan ningún derecho legal tooany la propiedad intelectual de ningún producto de Microsoft. Puede copiar y usar este documento con fines internos y de referencia. © 2014 Microsoft. Todos los derechos reservados. 

