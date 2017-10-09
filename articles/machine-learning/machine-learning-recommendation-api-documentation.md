---
title: "Documentación de la API de aprendizaje recomendaciones aaaMachine | Documentos de Microsoft"
description: "Documentación de API de recomendaciones de aprendizaje de máquina de Azure para un motor de recomendaciones disponible en Microsoft Azure Marketplace de Hola."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Documentación de la API de recomendación de Aprendizaje automático de Azure
> [!NOTE]
> Debería empezar a usar Hola recomendaciones API cognitivos servicio en lugar de esta versión. Hola recomendaciones cognitivos servicio va a sustituir este servicio y todas las características nuevas de Hola se van a desarrollar no existe. Tiene nuevas funcionalidades como compatibilidad con procesamientos por lotes, un explorador de API más eficaz, una interfaz de API más limpia, una experiencia de facturación y suscripción más coherente, etc.
> Obtenga más información sobre [migrar toohello nuevo servicio cognitivos](http://aka.ms/recomigrate)
> 
> 

Este documento describe las API de recomendaciones de Aprendizaje automático de Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Información general
Este documento es una referencia de API. Debe empezar con el documento de "Azure máquina recomendación – inicio rápido de aprendizaje" Hola.

Hola API de recomendaciones de aprendizaje de máquina de Azure puede dividirse en hello siguientes grupos lógicos:

* <ins>Limitaciones</ins>: Limitaciones de la API de recomendaciones.
* <ins>Información general</ins>: Información sobre la autenticación, el identificador URI de servicio y el control de versiones.
* <ins>Modelo Basic</ins> -API que permiten operaciones básicas de hello toodo en modelo (por ejemplo, crear, actualizar y eliminar un modelo).
* <ins>Opciones avanzadas del modelo</ins> -API que permiten la información sobre los datos en el modelo de hello tooget avanzada.
* <ins>Modelo de reglas de negocios</ins> -API que permiten toomanage las reglas de negocios en resultados de recomendación del modelo de Hola.
* <ins>Catálogo</ins> -API que permiten operaciones básicas de toodo en un catálogo de modelos. Un catálogo contiene información de metadatos en los elementos de Hola Hola de datos de uso.
* <ins>Característica</ins> -API que permiten la visión de tooget en el elemento en el catálogo de Hola y cómo toouse este recomendaciones mejor toobuild de información.
* <ins>Datos de uso</ins> -API que permiten toodo operaciones básicas en los datos de uso del modelo de Hola. Datos de uso de forma básica hello consisten de filas que incluyen pares de &#60; userId &#62; &#60; itemId &#62;.
* <ins>Compilación</ins> : las API que permiten tootrigger un modelo de compilación y realizar operaciones básicas que están relacionados toothis la compilación. Puede desencadenar una compilación de modelo una vez que tenga datos de uso valiosos.
* <ins>Recomendación</ins> -API que permiten recomendaciones tooconsume una vez que finaliza la compilación de Hola de un modelo.
* <ins>Datos de usuario</ins> -API que permiten toofetch información sobre los datos de uso de usuario de Hola.
* <ins>Las notificaciones</ins> -operaciones de tooyour API relacionadas con la API que permiten que las notificaciones de tooreceive en problemas. (Por ejemplo, está informando de datos de uso a través de la adquisición de datos y la mayoría de los eventos de Hola se producen errores en el procesamiento. Se generará una notificación de error).

## <a name="2-limitations"></a>2. Limitaciones
* número máximo de Hola de modelos por suscripción es 10.
* Hola número máximo de compilaciones por modelo es 20.
* número máximo de Hola de elementos que puede contener un catálogo es 100.000.
* número máximo de Hola de puntos de uso que se mantienen es ~ 5 000 000. Hola más antigua se eliminará si nuevos se cargan o se notificarán.
* tamaño máximo de Hola de datos que se pueden enviar en POST (por ejemplo, importar datos del catálogo, importar datos de uso) es 200MB.
* número máximo de Hola de elementos que se pueden hacer al obtener recomendaciones es 150.

## <a name="3-apis---general-information"></a>3. API: información general
### <a name="31-authentication"></a>3.1. Autenticación
Siga las instrucciones de Microsoft Azure Marketplace de hello relativos a la autenticación. marketplace de Hello es compatible con cualquier método de autenticación básica o OAuth de Hola.

### <a name="32-service-uri"></a>3.2. URI de servicio
Hola URI raíz del servicio para las API de Azure Machine Learning recomendaciones hello es [aquí.](https://api.datamarket.azure.com/amla/recommendations/v3/)

URI del servicio completo Hola se expresa mediante elementos de especificación de OData de Hola.  

### <a name="33-api-version"></a>3.3. Versión de API
Al final de hello, cada llamada a la API tendrá un parámetro de consulta denominado valor apiVersion que se debe establecer too1.0.

### <a name="34-ids-are-case-sensitive"></a>3.4. Los Id. distinguen mayúsculas de minúsculas
Identificadores, devueltos por cualquiera de hello API, distinguen mayúsculas de minúsculas y deben usarse como tales cuando se pasan como parámetros en llamadas posteriores a la API. Por ejemplo, los Id. de modelo y de catálogo distinguen mayúsculas de minúsculas.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Calidad de recomendaciones y elementos fríos
### <a name="41-recommendation-quality"></a>4.1. Calidad de recomendación
Crear un modelo de recomendación suele ser suficiente recomendaciones de tooprovide del sistema de tooallow Hola. No obstante, calidad de las recomendaciones varía según el uso de hello procesado y Hola cobertura del catálogo de Hola. Por ejemplo si tiene una gran cantidad de elementos fríos (elementos sin uso significativo), sistema de hello tendrá dificultades para proporcionar una recomendación para un elemento de este tipo o utilizando un elemento de este tipo como recomendada. Problema de elemento inactivos de orden tooovercome hello, sistema de Hola permite el uso de Hola de metadatos de las recomendaciones de hello elementos tooenhance Hola. Estos metadatos son características de tooas que se hace referencia. Características típicas son el autor de un libro o el actor de una película. Características son proporcionadas a través del catálogo de hello en forma de Hola de cadenas de clave/valor. Formato completo de Hola Hola del archivo de catálogo, consulte toohello [importar sección catálogo](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. Compilación de rango
Características pueden mejorar el modelo de recomendación de hello, pero toodo por lo que requiere el uso de Hola de características significativos. Con este fin se introdujo una nueva compilación, una compilación de rango. Esta compilación clasificará utilidad Hola de características. Una característica significativa es una característica con una puntuación de rango de 2 para arriba.
Una vez que conozca cuál de las características de hello son significativos, desencadenar una compilación de recomendación con lista de hello (o sublista) de características significativos. Es posible toouse que estas características de mejora de Hola de los elementos fríos y elementos de estado. En orden toouse para elementos semiactivos, Hola `UseFeatureInModel` se deben configurar los parámetros de compilación. En las características de toouse de orden para los elementos fríos, Hola `AllowColdItemPlacement` debe habilitarse el parámetro de compilación.
Nota: No es posible tooenable `AllowColdItemPlacement` sin habilitar `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Razonamiento de recomendación
El razonamiento de la recomendación es otro aspecto del uso de características. De hecho, motor de recomendaciones de aprendizaje de máquina de Azure Hola puede utilizar la explicaciones de recomendación de características tooprovide (conocido como) Razonamiento), iniciales toomore confianza Hola recomienda elemento de consumidor de la recomendación de Hola.
tooenable razonamiento, hello `AllowFeatureCorrelation` y `ReasoningFeatureList` parámetros deben ser el programa de instalación anterior toorequesting una compilación de recomendación.

## <a name="5-model-basic"></a>5. Modelo básico
### <a name="51-create-model"></a>5.1. Crear modelo
Crea una solicitud "crear modelo".

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
  **Nota**: el Id. de modelo distingue mayúsculas de minúsculas.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a>5.2. Obtener modelo
Crea una solicitud "obtener modelo".

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| id |Identificador único del modelo de hello (con distinción entre mayúsculas y minúsculas) |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

datos del modelo Hola pueden encontrarse en hello siguientes elementos:

* `feed/entry/content/properties/Id`: id. único de modelo.
* `feed/entry/content/properties/Name`: nombre del modelo.
* `feed/entry/content/properties/Date` : fecha de creación del modelo.
* `feed/entry/content/properties/Status` : estado del modelo. Uno de hello siguientes:
  * Created: el modelo se crea y no contiene Catálogo ni Uso.
  * ReadyForBuild: el modelo se crea y contiene Catálogo y Uso.
* `feed/entry/content/properties/HasActiveBuild`: Indica si el modelo de Hola se creó correctamente.
* `feed/entry/content/properties/BuildId` : id. de compilación activa del modelo.
* `feed/entry/content/properties/Mpr`: clasificación percentil de promedio del modelo (MPR, consulte ModelInsight para obtener más información).
* `feed/entry/content/properties/UserName` : nombre de usuario interno del modelo.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Obtener todos los modelos
Recupera todos los modelos del usuario actual de Hola.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

* `feed/entry/content/properties/Id`: id. único de modelo.
* `feed/entry/content/properties/Name`: nombre del modelo.
* `feed/entry/content/properties/Date` : fecha de creación del modelo.
* `feed/entry/content/properties/Status` : estado del modelo. Uno de hello siguientes:
  * Created: el modelo se crea y no contiene Catálogo ni Uso.
  * ReadyForBuild: el modelo se crea y contiene Catálogo y Uso.
* `feed/entry/content/properties/HasActiveBuild`: Indica si el modelo de Hola se creó correctamente.
* `feed/entry/content/properties/BuildId` : id. de compilación activa del modelo.
* `feed/entry/content/properties/Mpr`: MPR del modelo (consulte ModelInsight para obtener más información).
* `feed/entry/content/properties/UserName` : nombre de usuario interno del modelo.
* `feed/entry/content/properties/UsageFileNames`: lista de archivos de uso del modelo separados por coma.
* `feed/entry/content/properties/CatalogId`: id. de catálogo del modelo.
* `feed/entry/content/properties/Description`: descripción del modelo.
* `feed/entry/content/properties/CatalogFileName` : nombre de archivo del catálogo de modelos.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Actualizar modelo
Puede actualizar la descripción del modelo de Hola u Hola Id. de compilación activa.<br>
<ins>Id. de compilación activa</ins>: cada compilación para cada modelo tiene un identificador de compilación. Id. de compilación activa de Hello es primera compilación correcta Hola de cada nuevo modelo. Una vez que tiene un identificador de compilación activa y hace que las compilaciones adicionales de Hola mismo modelo, deberá tooexplicitly establézcala como hello predeterminado Id. de compilación si desea. Cuando utilizas recomendaciones, si no especifica el Id. de generación de Hola que desee toouse, predeterminado Hola uno se usará automáticamente.<br>
Este mecanismo le permite - una vez que tiene un modelo de recomendación en producción - toobuild nuevos modelos y probarlas antes de promover ellos tooproduction.

| Método HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| id |Identificador único del modelo de hello (con distinción entre mayúsculas y minúsculas) |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Tenga en cuenta que Hola XML etiquetas descripción y ActiveBuildId son opcionales. Si no desea tooset descripción o ActiveBuildId, quite la etiqueta completa Hola. |

**Respuesta**:

código de estado HTTP: 200

### <a name="55----delete-model"></a>5.5.    Eliminar modelo
Elimina un modelo existente por el Id.

| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| id |Identificador único del modelo de hello (con distinción entre mayúsculas y minúsculas) |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Modelo avanzado
### <a name="61----model-data-insight"></a>6.1.    Modelo de detalles de datos
Devuelve datos estadísticos sobre los datos de uso de Hola que este modelo se generó con.

Disponible solo para la compilación de recomendación.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

Hola datos se devuelven como una colección de propiedades.

* `feed/entry/id/content/properties/key`-Contiene el nombre de la propiedad de Hola.
* `feed/entry/id/content/properties/value`-Contiene el valor de la propiedad de Hola.

a continuación de la tabla de Hello muestra valor Hola que representa cada clave.

| Clave | Description |
|:--- |:--- |
| AvgItemLength |Número promedio de usuarios distintos por elemento. |
| AvgUserLength |Número promedio de usuarios distintos por usuario. |
| DensificationNumberOfItems |Número de elementos después de eliminar elementos que no se pueden modelar. |
| DensificationNumberOfUsers |Número de puntos de uso después de eliminar usuarios y elementos que no se pueden modelar. |
| DensificationNumberOfRecords |Número de puntos de uso después de eliminar usuarios y elementos que no se pueden modelar. |
| MaxItemLength |Número de usuarios distintivos para elemento de hello más popular. |
| MaxUserLength |Número máximo de elementos distintos para un usuario. |
| MinItemLength |Número máximo de usuarios distintos para un elemento. |
| MinUserLength |Número mínimo de elementos distintos para un usuario. |
| RawNumberOfItems |Número de elementos de archivos de uso de Hola. |
| RawNumberOfUsers |Número de puntos de uso antes de cualquier eliminación. |
| RawNumberOfRecords |Número de puntos de uso antes de cualquier eliminación. |
| SamplingNumberOfItems |N/D |
| SamplingNumberOfRecords |N/D |
| SamplingNumberOfUsers |N/D |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Perspectiva de modelo
Devuelve una visión general de modelo en la compilación active Hola o (si se proporciona) en una compilación concreta.

Disponible solo para la compilación de recomendación.

| Método HTTP | URI |
|:--- |:--- |
| GET |Con identificador de compilación activa:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Con identificador de compilación específica:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| buildId |Opcional: número que identifica una compilación correcta. |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

Hola datos se devuelven como una colección de propiedades.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

a continuación de la tabla de Hello muestra valor Hola que representa cada clave.

| Clave | Description |
|:--- |:--- |
| CatalogCoverage |¿Qué parte del catálogo de Hola puede modelarse con patrones de uso. resto de Hola de elementos de hello deberá características basadas en contenido. |
| Mpr |Clasificación de percentil medio del modelo de Hola. Un valor bajo es mejor. |
| NumberOfDimensions |Número de dimensiones utilizado por el algoritmo de descomposición en factores de matriz de Hola. |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Obtener el ejemplo de modelo
Obtiene una muestra de modelo de recomendación de Hola.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Con identificador de compilación específica:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

OData XML

Se devuelve una respuesta en formato de texto sin formato:

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Reglas de negocio de modelo
Éstos son tipos de Hola de reglas admitidas:

* <strong>Lista de bloqueadas</strong> -lista de bloqueadas permite tooprovide una lista de elementos que no desea tooreturn en los resultados de la recomendación de Hola. 
* <strong>FeatureBlockList</strong> -lista de bloqueadas de característica permite tooblock elementos basados en valores de hello de sus características.

*No envíe más de 1000 elementos en una sola regla de lista de bloqueo. Si lo hace, es posible que se agote el tiempo de espera de la llamada. Si necesita más de 1000 elementos tooblock, puede realizar varias llamadas de lista de bloqueo.*

* <strong>Upsale</strong> -Upsale permite tooenforce elementos tooreturn en los resultados de la recomendación de Hola.
* <strong>Lista blanca de direcciones</strong> -habilita la lista blanca se tooonly sugerir recomendaciones de una lista de elementos.
* <strong>FeatureWhiteList</strong> -lista blanca de característica le permite tooonly. se recomienda elementos que tienen valores de las características específicas.
* <strong>PerSeedBlockList</strong> : por habilita la lista de bloques de inicialización tooprovide por cada elemento de una lista de elementos que no se puede devolver como resultado de la recomendación.

### <a name="71----get-model-rules"></a>7.1.    Obtener reglas de modelo
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Ejemplo:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

* `feed/entry/content/properties/Id` : el identificador único de esta regla.
* `feed/entry/content/properties/Type`-Tipo de regla de Hola.
* `feed/entry/content/properties/Parameter` : el parámetro de regla.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Agregar regla
| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| ENCABEZADO |`"Content-Type", "text/xml"` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud | |

<ins>Cada vez que proporcionar los identificadores de elementos de reglas de negocios, que seguro Hola de toouse identificador externo del elemento de hello (Hola el mismo identificador que usó en el archivo de catálogo de hello)</ins><br>
<ins>tooadd una regla de lista de bloqueo:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>una regla de FeatureBlockList tooadd:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>una regla de Upsale tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd una regla de lista blanca de direcciones:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>una regla de FeatureWhiteList tooadd:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>una regla de PerSeedBlockList tooadd:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Respuesta**:

código de estado HTTP: 200

Hola API devuelve Hola recién creado reglas con sus detalles. propiedades de reglas de Hello pueden obtenerse de hello siguiendo las rutas de acceso:

* `feed/entry/content/properties/Id` : el identificador único de esta regla.
* `feed/entry/content/properties/Type`-Tipo de regla de hello: lista de bloqueadas o Upsale.
* `feed/entry/content/properties/Parameter` : el parámetro de regla.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Eliminar regla
| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| filterId |Identificador único del filtro de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

### <a name="74----delete-all-rules"></a>7.4.    Eliminar todas las reglas
| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

## <a name="8-catalog"></a>8. Catálogo
### <a name="81----import-catalog-data"></a>8.1.    Importar datos de catálogo
Si va a cargar varias catálogo archivos toohello mismo modelo con varias llamadas, insertamos solo Hola nuevos elementos de catálogo. Los elementos existentes permanecerán con valores originales de Hola. Los datos del catálogo no se pueden actualizar con este método.

datos del catálogo de Hello deben seguir Hola siguiendo el formato:

* Sin características: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* Con características: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Nota: el tamaño máximo del archivo de hello es 200MB.

** Detalles de formato **

| Nombre | Obligatorio | Tipo | Description |
|:--- |:--- |:--- |:--- |
| Id. de elemento |Sí |[A-z], [a-z], [0-9], [_] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;<br> Longitud máxima: 50 |Identificador único de un elemento. |
| Nombre del elemento |Sí |Cualquier carácter alfanumérico<br> Longitud máxima: 255 |Nombre del elemento. |
| Categoría del elemento |Sí |Cualquier carácter alfanumérico <br> Longitud máxima: 255 |Categoría toowhich este elemento pertenece (por ejemplo, cocina libros, series...); puede estar vacío. |
| Descripción |No, a menos que haya características (pero puede estar vacía) |Cualquier carácter alfanumérico <br> Longitud máxima: 4000 |Descripción de este elemento. |
| Lista de características |No |Cualquier carácter alfanumérico <br> Longitud máxima: 4000; número máximo de características: 20 |Lista separada por comas de nombre de la característica = valor de la característica que puede ser utilizados tooenhance recomendación del modelo; vea [temas avanzados](#2-advanced-topics) sección. |

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| ENCABEZADO |`"Content-Type", "text/xml"` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| filename |Identificador textual del catálogo de Hola.<br>Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).<br>Longitud máxima: 50 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |Ejemplo (con características):<br/>2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, libro, descripción del libro hello, crear = Richard Wright, publisher = Harper Flamingo Canadá, año = 2001<br>Hola 21bf8088-b6c0-4509-870c-e1c7ac78304a, Forgetting sala: A ficción (Byzantium Book), libro, crear = Nick Bantock, publisher = Harpercollins, año = 1997<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001<br>552a1940-21e4-4399-82bb-594b46d7ed54, retención de Animals, libro, descripción del libro hello, crear = Magnus Mills, publisher = publicación de juegos, año = 1998</pre> |

**Respuesta**:

código de estado HTTP: 200

Hola API devuelve un informe de importación de Hola.

* `feed\entry\content\properties\LineCount` : número de líneas aceptadas.
* `feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Obtener catálogo
Recupera todos los elementos del catálogo.
catálogo de Hello será recuperar una página a la vez. Si desea tooget elementos en un índice determinado, puede usar el parámetro de hello $skip odata. Por ejemplo si desea que los elementos de tooget a partir de posición 100, Agregar parámetro hello $skip = 100 solicitud toohello.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento de catálogo. Cada entrada tiene Hola datos siguientes:

* `feed/entry/content/properties/ExternalId`-Identificador externo del elemento del catálogo, Hola uno proporcionado por el cliente de Hola.
* `feed/entry/content/properties/InternalId`-Catálogo Id. interno del elemento, Hola uno generadas por las recomendaciones de aprendizaje de máquina de Azure.
* `feed/entry/content/properties/Name` : nombre de elemento de catálogo.
* `feed/entry/content/properties/Category` : categoría de elemento de catálogo.
* `feed/entry/content/properties/Description` : descripción de elemento de catálogo.
* `feed/entry/content/properties/Metadata` : metadatos de elemento de catálogo.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Obtener elementos de catálogo por token
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| token |Símbolo (token) de nombre del elemento del catálogo de Hola. Debe contener al menos 3 caracteres. |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento de catálogo. Cada entrada tiene Hola datos siguientes:

* `feed/entry/content/properties/InternalId`-Catálogo Id. interno del elemento, Hola uno generadas por las recomendaciones de aprendizaje de máquina de Azure.
* `feed/entry/content/properties/Name` : nombre de elemento de catálogo.
* `feed/entry/content/properties/Rating`: (para un uso futuro)
* `feed/entry/content/properties/Reasoning`: (para un uso futuro)
* `feed/entry/content/properties/Metadata`: (para un uso futuro)
* `feed/entry/content/properties/FormattedRating` : (para un uso futuro)

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Datos de uso
### <a name="91----import-usage-data"></a>9.1.    Importar datos de uso
#### <a name="911-uploading-file"></a>9.1.1. Carga de archivos
Esta sección se muestra cómo los datos de uso de tooupload mediante un archivo. Puede llamar a esta API varias veces con datos de uso. Todos los datos de uso se guardarán para todas las llamadas.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| filename |Identificador textual del catálogo de Hola.<br>Solo se permiten letras (A-Z, a-z), números (0-9), guiones (-) y caracteres de subrayado (_).<br>Longitud máxima: 50 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |Datos de uso. Formato:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nombre</th><th>Obligatorio</th><th>Tipo</th><th>Description</th></tr><tr><td>Id. de usuario</td><td>Sí</td><td>[A-z], [a-z], [0-9], [_] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;<br> Longitud máxima: 255 </td><td>Identificador único de un usuario.</td></tr><tr><td>Id. de elemento</td><td>Sí</td><td>[A-z], [a-z], [0-9], [&#95;] &#40;Carácter de subrayado&#41;, [-] &#40;Guion&#41;<br> Longitud máxima: 50</td><td>Identificador único de un elemento.</td></tr><tr><td>Hora</td><td>No</td><td>La fecha en este formato: AAAA/MM/DDTHH:MM:SS (por ejemplo, 2013/06/20T10:00:00)</td><td>Hora de los datos.</td></tr><tr><td>Evento</td><td>No, si se suministra también se debe colocar la fecha</td><td>Uno de hello siguientes:<br>• Click<br>• RecommendationClick<br>•    AddShopCart<br>• RemoveShopCart<br>• compra</td><td></td></tr></table><br>Tamaño de archivo máximo: 200 MB<br><br>Ejemplo:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Respuesta**:

código de estado HTTP: 200

* `Feed\entry\content\properties\LineCount` : número de líneas aceptadas.
* `Feed\entry\content\properties\ErrorCount`-Número de líneas que no se insertaron debido a error de tooan.
* `Feed\entry\content\properties\FileId` : identificador de archivo.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Uso de la adquisición de datos
Esta sección muestra cómo toosend eventos real hora de recomendaciones de aprendizaje de máquina tooAzure, normalmente desde su sitio Web.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| ENCABEZADO |`"Content-Type", "text/xml"` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| apiVersion |1.0 |
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
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
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

### <a name="92----list-model-usage-files"></a>9.2.    Mostrar archivos de uso de modelo
Recupera los metadatos de todos los archivos de uso de modelo.
Hello uso de archivos que recupera una página a la vez. Cada página contiene 100 elementos. Si desea tooget elementos en un índice determinado, puede usar el parámetro de hello $skip odata. Por ejemplo si desea que los elementos de tooget a partir de posición 100, Agregar parámetro hello $skip = 100 solicitud toohello.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| forModelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada archivo de uso. Cada entrada tiene Hola datos siguientes:

* `feed\entry\content\properties\Id`: id. de archivo de uso.
* `feed\entry\content\properties\Length` : longitud del archivo uso en MB.
* `feed\entry\content\properties\DateModified`-Fecha cuando se creó el archivo de uso de hello.
* `feed\entry\content\properties\UseInModel`-Si se usan archivos de uso de hello en el modelo de Hola.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Obtener estadísticas de uso
Obtiene estadísticas de uso.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| startDate |Fecha de inicio. Formato: aaaa/MM/ddTHH:mm:ss |
| endDate |Fecha de fin. Formato: aaaa/MM/ddTHH:mm:ss |
| eventTypes |Cadena separada por comas de evento tipos o null tooget todos los eventos |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

Una colección de elementos de clave y valor. Cada uno de ellos contiene la suma de Hola de eventos para un tipo de evento concreto agrupadas por hora.

* `feed\entry[i]\content\properties\Key`-Contiene la hora de hello (agrupado por hora) y el tipo de evento de Hola.
* `feed\entry[i]\content\properties\Value` : recuento total de eventos.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Obtener ejemplo de archivo de uso
Recupera Hola 2KB primer uso de contenido del archivo.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| fileId |Identificador único del archivo de uso del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

Se devuelve una respuesta en formato de texto sin formato:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Obtener el archivo de uso de modelo
Recupera todo el contenido del archivo de uso de Hola Hola.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| mId |Identificador único del modelo de Hola |
| fid |Identificador único del archivo de uso del modelo de Hola |
| descargar |1 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

Se devuelve una respuesta en formato de texto sin formato:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Eliminar archivo de uso
Elimina el archivo de uso de hello modelo especificado.

| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| fileId |Identificador único de hello archivo toobe eliminado |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

### <a name="97----delete-all-usage-files"></a>9.7.    Eliminar todos los archivos de uso
Elimina todos los archivos de uso del modelo.

| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

## <a name="10-features"></a>10. Características
Esta sección muestra cómo tooretrieve característica información, como características de hello importado y sus valores, su clasificación, y cuando se ha asignado este rango. Características se importan como parte de datos del catálogo de hello y, a continuación, su rango está asociado cuando se realiza una compilación de rango.
Rango en la característica puede cambiar correspondiente patrón toohello de datos de uso y el tipo de elementos. Pero para los elementos/uso coherente, rango de Hola que debería tener sólo pequeñas fluctuaciones.
rango de Hola de características es un número no negativo. Hello número 0 significa que no se clasifican esa característica hello (ocurre si se invoca esta finalización toohello anteriores de API de la primera compilación rank de hello). fecha de Hello en el que se atribuye rango Hola se denomina actualización de puntuación de Hola.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. Obtener información de características (para la última compilación de rango)
Recupera información de la función hello, incluida la clasificación de hello última rank compilación correcta.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| samplingSize |Número de valores tooinclude para cada característica según toohello datos presentes en el catálogo de Hola. <br/>Los valores posibles son:<br> -1 - Todas las muestras. <br>0: sin muestreo. <br>N: se devuelven N muestras para cada nombre de característica. |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello contiene una lista de entradas de información de característica. Cada entrada contiene:

* `feed/entry/content/m:properties/d:Name` : nombre de la característica.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Fecha de en qué Hola rango en la característica de toothis asignado, conocido como característica de actualización de puntuación. Una fecha histórica ('0001-01-01T00:00:00') significa que no se ha realizado ninguna compilación de rango.
* `feed/entry/content/m:properties/d:Rank`: rango de característica (flotante). Un rango de 2.0 para arriba se considera una buena característica.
* `feed/entry/content/m:properties/d:SampleValues`-Lista separados por comas de valores de tamaño de muestreo toohello solicitado.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. Obtener información de características (para una compilación de rango específica)
Recupera información de característica de hello, incluidos Hola de categoría para una compilación de rango específica.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| samplingSize |Número de valores tooinclude para cada característica según toohello datos presentes en el catálogo de Hola.<br/> Los valores posibles son:<br> -1 - Todas las muestras. <br>0: sin muestreo. <br>N: se devuelven N muestras para cada nombre de característica. |
| rankBuildId |Identificador único de compilación de rango de Hola o -1 para la última compilación de rango Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello contiene una lista de entradas de información de característica. Cada entrada contiene:

* `feed/entry/content/m:properties/d:Name` : nombre de la característica.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Fecha de en qué Hola rango en la característica de toothis asignado, conocido como característica de actualización de puntuación. Una fecha histórica ('0001-01-01T00:00:00') significa que no se ha realizado ninguna compilación de rango.
* `feed/entry/content/m:properties/d:Rank`: rango de característica (flotante). Un rango de 2.0 para arriba se considera una buena característica.
* `feed/entry/content/m:properties/d:SampleValues`-Lista separados por comas de valores de tamaño de muestreo toohello solicitado.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Compilación
  Esta sección explica Hola distintas API relacionadas con toobuilds. Hay tres tipos de compilación: una compilación de recomendación, una compilación de rango y una compilación FBT (artículos que con frecuencia se compran juntos).

propósito de la compilación de Hello recomendación es toogenerate usa un modelo de recomendación para realizar predicciones. Las predicciones (para este tipo de compilación) se presentan en dos modos:

* I2I - también conocida como Elemento recomendaciones tooItem: un elemento o una lista de elementos de esta opción predecirá una lista de elementos que son probable toobe de gran interés.
* U2I - también conocida como Recomendaciones de usuario tooItem - dadas un identificador de usuario (y, opcionalmente, una lista de elementos) esta opción predecirá una lista de elementos que son probable toobe interesa hello tiene el usuario (y sus opciones adicionales de elementos). recomendaciones de Hello U2I se basan en el historial de Hola de elementos que eran de interés para el usuario de hello tiempo toohello Hola modelo se generó.

Un rango es una técnica generación que le permite toolearn acerca de la utilidad de Hola de sus características. Por lo general, en orden tooget Hola mejores resultados para un modelo de recomendación que implican características, debe tener Hola pasos:

* Desencadenar una compilación rank (a menos que la puntuación de Hola de características es estable) y espere a que se obtendrá la puntuación de la característica de Hola.
* Recuperar rango Hola de las funciones de llamada hello [obtener información de características](#101-get-features-info-for-last-rank-build) API.
* Configurar una compilación de recomendación con hello parámetros siguientes:
  * `useFeatureInModel`-Establecer tooTrue.
  * `ModelingFeatureList`-Set tooa-lista separados por comas de características con una puntuación de 2.0 o más (según la rangos toohello recuperado en el paso anterior de hello).
  * `AllowColdItemPlacement`-Establecer tooTrue.
  * Opcionalmente, puede establecer `EnableFeatureCorrelation` tooTrue y `ReasoningFeatureList` toohello lista de características que desea toouse para obtener una explicación (normalmente Hola misma lista de características se usa en una sublista o modelización).
* Compilación de recomendación de Hola de desencadenador con hello configurado los parámetros.

Nota: Si no configura los parámetros (p. ej. de invocación de compilación de la recomendación de hello sin parámetros) o deshabilitar explícitamente de uso de Hola de características (p. ej. `UseFeatureInModel` establecer tooFalse), sistema Hola configurará parámetros relacionados con la característica de Hola toohello explica los valores anteriores en caso de que existe una compilación de rango.

No hay restricciones acerca de cómo ejecutar una compilación de rango y una recomendación generar de forma simultánea para hello mismo modelo. No obstante, no se puede ejecutar dos compilaciones de hello mismo tipo en hello mismo modelo en paralelo.

Una compilación FBT (con frecuencia se compra junto) es otro algoritmo de recomendación denominado a veces recomendador "conservador", que resulta conveniente para catálogos que no sean de naturaleza homogénea (homogéneo: libros, películas, algunos alimentos, moda; no homogéneo: equipos y dispositivos, entre dominios, gran diversidad).

Nota: si los archivos de uso que haya cargado hello contienen campo opcional Hola "tipo de evento", para FBT modelización sólo los eventos "Compra" se utilizará. Si no se proporciona ningún tipo de evento, todos los eventos se considerarán de compra.

#### <a name="111-build-parameters"></a>11.1 Parámetros de compilación
Cada tipo de compilación puede configurarse a través de un conjunto de parámetros (se muestra a continuación). Si no configura los parámetros de hello, sistema de hello automáticamente de atributo valores toohello parámetros según la información de toohello presente en el momento de hello desencadenar una compilación.

##### <a name="1111-usage-condenser"></a>11.1.1. Condensador de uso
Los usuarios o elementos con pocos puntos de uso podrían contener más ruido de información. sistema de Hello intente toopredict Hola un número mínimo de puntos de uso por toobe/elemento de usuario usadas en un modelo. Este número será dentro de intervalo de hello definido hello ItemCutoffLowerBound y los parámetros de ItemCutoffUpperBound elementos e intervalo de hello definida por hello UserCutOffLowerBound y parámetros de UserCutoffUpperBound para los usuarios de. efecto de condensador Hello en elementos o los usuarios puede reducirse mediante la configuración de al menos uno de hello correspondiente límites toozero.

##### <a name="1112-rank-build-parameters"></a>11.1.2. Parámetros de compilación de rango
a continuación de la tabla de Hello muestra los parámetros de compilación de Hola para una compilación de rango.

| Clave | Description | Tipo | Valor válido |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |número de Hola de iteraciones que realiza el modelo de Hola se refleja en hello hello y tiempo de precisión del modelo de proceso general. número mayor de Hola de Hello, obtendrá de conseguir una mayor precisión de hello, pero Hola proceso tardará más tiempo. |Entero |10-50 |
| NumberOfModelDimensions |número de Hola de dimensiones se relaciona toohello número de modelo de hello 'features' intentará toofind dentro de los datos. Aumentar el número de Hola de dimensiones le permitirá optimizar mejor de los resultados de hello en clústeres más pequeños. Sin embargo, hay demasiadas dimensiones impedirá modelo Hola buscar las correlaciones entre los elementos. |Entero |10-40 |
| ItemCutOffLowerBound |Define el límite de hello elemento inferior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| ItemCutOffUpperBound |Define el límite de hello elemento superior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| UserCutOffLowerBound |Define el límite de hello usuario inferior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| UserCutOffUpperBound |Define el límite de hello usuario superior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Parámetros de compilación de recomendación
tabla de Hello siguiente describe los parámetros de compilación de Hola para compilación de recomendación.

| Clave | Description | Tipo | Valor válido |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |número de Hola de iteraciones que realiza el modelo de Hola se refleja en hello hello y tiempo de precisión del modelo de proceso general. número mayor de Hola de Hello, obtendrá de conseguir una mayor precisión de hello, pero Hola proceso tardará más tiempo. |Entero |10-50 |
| NumberOfModelDimensions |número de Hola de dimensiones se relaciona toohello número de modelo de hello 'features' intentará toofind dentro de los datos. Aumentar el número de Hola de dimensiones le permitirá optimizar mejor de los resultados de hello en clústeres más pequeños. Sin embargo, hay demasiadas dimensiones impedirá modelo Hola buscar las correlaciones entre los elementos. |Entero |10-40 |
| ItemCutOffLowerBound |Define el límite de hello elemento inferior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| ItemCutOffUpperBound |Define el límite de hello elemento superior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| UserCutOffLowerBound |Define el límite de hello usuario inferior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| UserCutOffUpperBound |Define el límite de hello usuario superior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| Description |Descripción de la compilación. |String |Cualquier texto, máximo 512 caracteres |
| EnableModelingInsights |Le permite toocompute métricas en el modelo de recomendación de Hola. |Booleano |True/False |
| UseFeaturesInModel |Indica si se pueden utilizar características en el modelo de recomendación de orden tooenhance Hola. |Booleano |True/False |
| ModelingFeatureList |Lista separada por comas de toobe de nombres de característica utilizado en la compilación de recomendación de hello, en la recomendación de orden tooenhance Hola. |String |Nombres de las características, los caracteres de too512 |
| AllowColdItemPlacement |Indica si la recomendación de hello también debería insertar elementos fríos a través de la similitud de características. |Booleano |True/False |
| EnableFeatureCorrelation |Indica si se pueden utilizar características en el razonamiento. |Booleano |True/False |
| ReasoningFeatureList |Lista separada por comas de toobe de nombres de función permiten razonamiento frases (por ejemplo, explicaciones de recomendación). |String |Nombres de las características, los caracteres de too512 |
| EnableU2I |Permitir conocido como recomendación de hello personalizada U2I (recomendaciones de tooitem de usuario). |Booleano |True/False (true de forma predeterminada) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. Parámetros de compilación FBT
tabla de Hello siguiente describe los parámetros de compilación de Hola para compilación de recomendación.

| Clave | Description | Tipo | Valor válido (predeterminado) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Cómo es el modelo conservador Hola. Número de repeticiones coadministradores de toobe de elementos que se consideran para el modelado. |Entero |3-50 (6) |
| FbtMaxItemSetSize |Límites Hola número de elementos de un conjunto frecuente. |Entero |2-3 (2) |
| FbtMinimalScore |Puntuación mínima que frecuentes devuelve un conjunto debe haber en toobe orden incluido en hello da como resultado. Hola superior Hola mejor. |Double |0 y superior (0) |
| FbtSimilarityFunction |Define Hola similitud función toobe utilizado por compilación Hola. Elevación favorece serendipity, aparición coadministradores favorece previsibilidad y Jaccard es un compromiso entre dos Hola "nice". |String |cooccurrence, lift, jaccard (lift) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Desencadenar una compilación de recomendación
  De forma predeterminada, esta API desencadenará una compilación de modelo de recomendación. tootrigger un rango de compilación (en las características de tooscore de pedido), debe usarse la variante de API de generación de hello con el parámetro de tipo de compilación.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| ENCABEZADO |`"Content-Type", "text/xml"` (Si se envía el cuerpo de la solicitud) |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| userDescription |Identificador textual del catálogo de Hola. Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %. Vea el ejemplo anterior.<br>Longitud máxima: 50 |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |Si se deja vacío, a continuación, compilación Hola se ejecutarán con parámetros de compilación de hello predeterminados.<br><br>Si desea que los parámetros de compilación de hello tooset, enviar parámetros de hello como XML en el cuerpo de hello como en el siguiente ejemplo de Hola. (Consulte la sección de Hola "parámetros de compilación" para obtener una explicación de los parámetros de Hola.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Respuesta**:

código de estado HTTP: 200

Se trata de una API asincrónica. Obtendrá un Id. de compilación como respuesta. tooknow cuando ha finalizado la generación de hello, debe llamar a la API de "Obtener compilaciones estado de un modelo de" hello y busque este Id. de compilación en la respuesta de Hola. Tenga en cuenta que una compilación puede tardar desde toohours minutos según el tamaño de Hola de datos de Hola.

No se puede consumir recomendaciones hasta Hola crear extremos.

Estado de compilación válido:

* Crear: se ha creado la solicitud de compilación.
* En cola: la solicitud de compilación se ha enviado y puesto en cola.
* Compilando: la compilación está en curso.
* Correcto: la compilación finalizó correctamente.
* Error: la compilación finalizó con un error.
* Cancelada: se canceló la compilación.
* Cancelar: se ha enviado una solicitud de cancelación para compilación de Hola.

Tenga en cuenta esa compilación Hola que identificador puede encontrarse en hello siguiendo la ruta de acceso:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Desencadenar compilación (recomendación, rango o FBT)
| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| ENCABEZADO |`"Content-Type", "text/xml"` (Si se envía el cuerpo de la solicitud) |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| userDescription |Identificador textual del catálogo de Hola. Tenga en cuenta que si usa espacios debe codificarlo en su lugar con un 20 %. Vea el ejemplo anterior.<br>Longitud máxima: 50 |
| buildType |Tipo de hello compilación tooinvoke: <br/> "Recomendación" para compilación de recomendación <br> -"Categoría" para una compilación de rango <br/> - 'Fbt' para compilación FBT |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |Si se deja vacío, a continuación, compilación Hola se ejecutarán con parámetros de compilación de hello predeterminados.<br><br>Si desea que los parámetros de compilación tooset, enviarlos como XML en el cuerpo de hello como en el siguiente ejemplo de Hola. (Consulte la sección de "parámetros de compilación" hello para una explicación y una lista completa de parámetros de Hola.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Respuesta**:

código de estado HTTP: 200

Se trata de una API asincrónica. Obtendrá un Id. de compilación como respuesta. tooknow cuando ha finalizado la generación de hello, debe llamar a la API de "Obtener compilaciones estado de un modelo de" hello y busque este Id. de compilación en la respuesta de Hola. Tenga en cuenta que una compilación puede tardar desde toohours minutos según el tamaño de Hola de datos de Hola.

No se puede consumir recomendaciones hasta Hola crear extremos.

Estado de compilación válido:

* Crear: se creó el modelo.
* En cola: se desencadenó la compilación del modelo y está en la cola.
* Compilando: el modelo se está compilando.
* Correcto: la compilación finalizó correctamente.
* Error: la compilación finalizó con un error.
* Cancelada: se canceló la compilación.
* Cancelando: la compilación se está cancelando.

Tenga en cuenta esa compilación Hola que identificador puede encontrarse en hello siguiendo la ruta de acceso:`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a>11.4. Obtener el estado de compilación de un modelo
Recupera las compilaciones y su estado para un modelo especificado.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| onlyLastBuild |Indica si tooreturn Hola a todos crear historial de modelo de Hola o solo de estado de Hola de compilación más reciente de Hola |
| apiVersion |1.0 |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada compilación. Cada entrada tiene Hola datos siguientes:

* `feed/entry/content/properties/UserName`-Nombre de usuario de Hola.
* `feed/entry/content/properties/ModelName`-Nombre del modelo de Hola.
* `feed/entry/content/properties/ModelId` : identificador único de modelo.
* `feed/entry/content/properties/IsDeployed`-Si se implementa compilación hello (conocido como) compilación activa).
* `feed/entry/content/properties/BuildId` : identificador único de compilación.
* `feed/entry/content/properties/BuildType`-Tipo de compilación de Hola.
* `feed/entry/content/properties/Status` : estado de la compilación. Puede ser uno de los siguientes de hello: Error, creación, en cola, cancelando, cancelado, correcto.
* `feed/entry/content/properties/StatusMessage`-Mensaje de estado detallado (se aplica solo toospecific estados).
* `feed/entry/content/properties/Progress` : progreso de la compilación (%).
* `feed/entry/content/properties/StartTime` : hora de inicio de la compilación.
* `feed/entry/content/properties/EndTime` : hora de finalización de la compilación.
* `feed/entry/content/properties/ExecutionTime` : duración de la compilación.
* `feed/entry/content/properties/ProgressStep`-Los detalles acerca de la fase actual de Hola de una compilación en curso.

Estado de compilación válido:

* Creado: se creó la entrada de solicitud de compilación.
* En cola: la solicitud de compilación se ha desencadenado y puesto en cola.
* Compilando: la compilación está en curso.
* Correcto: la compilación finalizó correctamente.
* Error: la compilación finalizó con un error.
* Cancelada: se canceló la compilación.
* Cancelando: la compilación se está cancelando.

Valores válidos para el tipo de compilación:

* Rango: compilación de rango.
* Recomendación: compilación de recomendación.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a>11.5. Obtener estado de compilación
Recupera los estados de compilación de todos los modelos de un usuario

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| onlyLastBuild |Indica si tooreturn Hola a todos crear historial de modelo de Hola o solo de estado de Hola de compilación más reciente de Hola. |
| apiVersion |1.0 |

**Respuesta**:

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada compilación. Cada entrada tiene Hola datos siguientes:

* `feed/entry/content/properties/UserName`-Nombre de usuario de Hola.
* `feed/entry/content/properties/ModelName`-Nombre del modelo de Hola.
* `feed/entry/content/properties/ModelId` : identificador único de modelo.
* `feed/entry/content/properties/IsDeployed`-Si está implementada la compilación de Hola.
* `feed/entry/content/properties/BuildId` : identificador único de compilación.
* `feed/entry/content/properties/BuildType`-Tipo de compilación de Hola.
* `feed/entry/content/properties/Status` : estado de la compilación. Puede ser uno de los siguientes de hello: Error, creación, en cola, cancelado, cancelando, correcto.
* `feed/entry/content/properties/StatusMessage`-Mensaje de estado detallado (se aplica solo toospecific estados).
* `feed/entry/content/properties/Progress` : progreso de la compilación (%).
* `feed/entry/content/properties/StartTime` : hora de inicio de la compilación.
* `feed/entry/content/properties/EndTime` : hora de finalización de la compilación.
* `feed/entry/content/properties/ExecutionTime` : duración de la compilación.
* `feed/entry/content/properties/ProgressStep`-Los detalles acerca de la fase actual de Hola de una compilación en curso.

Estado de compilación válido:

* Creado: se creó la entrada de solicitud de compilación.
* En cola: la solicitud de compilación se ha desencadenado y puesto en cola.
* Compilando: la compilación está en curso.
* Correcto: la compilación finalizó correctamente.
* Error: la compilación finalizó con un error.
* Cancelada: se canceló la compilación.
* Cancelando: la compilación se está cancelando.

Valores válidos para el tipo de compilación:

* Rango: compilación de rango.
* Recomendación: compilación de recomendación.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a>11.6. Eliminar compilación
Elimina una compilación.

NOTA:  <br>no se puede eliminar una compilación activa. Hola modelo debe estar actualizado tooa diferentes active compilación antes de eliminarlo.<br>No puede eliminar una compilación en curso. Debe cancelar compilación hello en primer lugar mediante una llamada a <strong>Cancelar compilación</strong>.

| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| buildId |Identificador único de la compilación de Hola. |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

### <a name="117-cancel-build"></a>11.7. Cancelar compilación
Cancela una compilación que se encuentra en estado Building.

| Método HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| buildId |Identificador único de la compilación de Hola. |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

### <a name="118-get-build-parameters"></a>11.8. Obtener parámetros de compilación
Recupera parámetros de compilación.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| buildId |Identificador único de la compilación de Hola. |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

Esta API devuelve una colección de elementos de clave y valor. Cada elemento representa un parámetro y su valor:

* `feed/entry/content/properties/Key` : nombre del parámetro de compilación.
* `feed/entry/content/properties/Value` : valor del parámetro de compilación.

a continuación de la tabla de Hello muestra valor Hola que representa cada clave.

| Clave | Description | Tipo | Valor válido |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |número de Hola de iteraciones que realiza el modelo de Hola se refleja en hello hello y tiempo de precisión del modelo de proceso general. número mayor de Hola de Hello, obtendrá de conseguir una mayor precisión de hello, pero Hola proceso tardará más tiempo. |Entero |10-50 |
| NumberOfModelDimensions |número de Hola de dimensiones se relaciona toohello número de modelo de hello 'features' intentará toofind dentro de los datos. Aumentar el número de Hola de dimensiones le permitirá optimizar mejor de los resultados de hello en clústeres más pequeños. Sin embargo, hay demasiadas dimensiones impedirá modelo Hola buscar las correlaciones entre los elementos. |Entero |10-40 |
| ItemCutOffLowerBound |Define el límite de hello elemento inferior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| ItemCutOffUpperBound |Define el límite de hello elemento superior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| UserCutOffLowerBound |Define el límite de hello usuario inferior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| UserCutOffUpperBound |Define el límite de hello usuario superior para condensador Hola. Consulte el condensador de uso anteriormente. |Entero |2 o más (0 deshabilita el condensador) |
| Description |Descripción de la compilación. |String |Cualquier texto, máximo 512 caracteres |
| EnableModelingInsights |Le permite toocompute métricas en el modelo de recomendación de Hola. |Booleano |True/False |
| UseFeaturesInModel |Indica si se pueden utilizar características en el modelo de recomendación de orden tooenhance Hola. |Booleano |True/False |
| ModelingFeatureList |Lista separada por comas de toobe de nombres de característica utilizado en la compilación de recomendación de hello, en la recomendación de orden tooenhance Hola. |String |Nombres de las características, los caracteres de too512 |
| AllowColdItemPlacement |Indica si la recomendación de hello también debería insertar elementos fríos a través de la similitud de características. |Booleano |True/False |
| EnableFeatureCorrelation |Indica si se pueden utilizar características en el razonamiento. |Booleano |True/False |
| ReasoningFeatureList |Lista separada por comas de toobe de nombres de función permiten razonamiento frases (por ejemplo, explicaciones de recomendación). |String |Nombres de las características, los caracteres de too512 |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Recomendación
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. Obtención de recomendaciones de elemento (para la compilación activa)
Obtener recomendaciones de compilación activa de Hola de tipo "Recomendación" o "Fbt" basado en una lista de elementos de valores de inicialización (entrada).

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| itemIds |Lista separada por comas de hello elementos toorecommend para. <br>Si compilación activa hello es de tipo FBT, a continuación, puede enviar un único elemento. <br>Longitud máxima: 1024 |
| numberOfResults |Número de resultados obligatorios  <br> Máx.: 150 |
| includeMetatadata |Uso futuro, siempre es false |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

respuesta de ejemplo de Hola siguiente incluye 10 elementos recomendados.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. Obtención de recomendaciones de elemento (de una compilación concreta)
Obtiene recomendaciones de una compilación concreta de tipo "Recomendación" o "Fbt".

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| itemIds |Lista separada por comas de hello elementos toorecommend para. <br>Si compilación activa hello es de tipo FBT, a continuación, puede enviar un único elemento. <br>Longitud máxima: 1024 |
| numberOfResults |Número de resultados obligatorios  <br> Máx.: 150 |
| includeMetatadata |Uso futuro, siempre es false |
| buildId |Hola compilar toouse de identificador para esta solicitud de recomendación |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

Vea un ejemplo de respuesta en 12.1

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. Obtención de recomendaciones de FBT (para la compilación activa)
Obtenga recomendaciones de compilación activa de Hola de tipo "Fbt" basada en un elemento de valor de inicialización (entrada).

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| itemId |Elemento toorecommend para. <br>Longitud máxima: 1024 |
| numberOfResults |Número de resultados obligatorios  <br>Máx.: 150 |
| minimalScore |Resultados de puntuación mínima que frecuentes devuelve un conjunto debe haber en toobe orden incluido en hello |
| includeMetatadata |Uso futuro, siempre es false |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada conjunto de elementos recomendados (un conjunto de elementos que normalmente se compró junto con el producto de Hola/datos proporcionados por el valor de inicialización). Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id1`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name1`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Id2`: id. del 2º elemento recomendado (opcional).
* `Feed\entry\content\properties\Name2`-Nombre del elemento 2 de hello (opcional).
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

respuesta de ejemplo de Hola siguiente incluye 3 conjuntos de elementos recomendados.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. Obtención de recomendaciones FBT (de una compilación concreta)
Obtenga recomendaciones de una compilación concreta de tipo "Fbt".

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| itemId |Elemento toorecommend para. <br>Longitud máxima: 1024 |
| numberOfResults |Número de resultados obligatorios  <br>Máx.: 150 |
| minimalScore |Resultados de puntuación mínima que frecuentes devuelve un conjunto debe haber en toobe orden incluido en hello |
| includeMetatadata |Uso futuro, siempre es false |
| buildId |Hola compilar toouse de identificador para esta solicitud de recomendación |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada conjunto de elementos recomendados (un conjunto de elementos que normalmente se compró junto con el producto de Hola/datos proporcionados por el valor de inicialización). Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id1`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name1`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Id2`: id. del 2º elemento recomendado (opcional).
* `Feed\entry\content\properties\Name2`-Nombre del elemento 2 de hello (opcional).
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

Vea un ejemplo de respuesta en 12.3

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Obtención de recomendaciones de usuario (para la compilación activa)
Obtenga recomendaciones de la compilación activa de tipo "Recommendation" marcada como compilación activa.

Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de Hola.

Notas: 

1. No hay ninguna recomendación de usuario para la generación de FBT.
2. Si crear Hola active es FBT este método le devuelve un error.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| userId |Identificador único del usuario de Hola |
| numberOfResults |Número de resultados requeridos |
| includeMetatadata |Uso futuro, siempre es false |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

Vea un ejemplo de respuesta en 12.1

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Obtención de recomendaciones de usuario con lista de elementos (para la compilación activa)
Obtenga recomendaciones de la compilación activa de tipo "Recommendation" marcada como compilación activa con una lista de elementos adicional

Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de Hola y elementos de hello adicionales proporcionados.

Notas: 

1. No hay ninguna recomendación de usuario para la generación de FBT.
2. Si crear Hola active es FBT este método le devuelve un error.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| userId |Identificador único del usuario de Hola |
| itemsIds |Lista separada por comas de hello elementos toorecommend para. Longitud máxima: 1024 |
| numberOfResults |Número de resultados requeridos |
| includeMetatadata |Uso futuro, siempre es false |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

Vea un ejemplo de respuesta en 12.1

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. Obtención de recomendaciones del usuario (de una compilación concreta)
Obtenga recomendaciones de una compilación concreta de tipo "Recomendación" o "Fbt".

Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de hello (que se usa en la compilación concreta hello).

Nota: no hay ninguna recomendación de usuario para la generación de FBT.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| userId |Identificador único del usuario de Hola |
| numberOfResults |Número de resultados requeridos |
| includeMetatadata |Uso futuro, siempre es false |
| buildId |Hola compilar toouse de identificador para esta solicitud de recomendación |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

Vea un ejemplo de respuesta en 12.1

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Obtención de recomendaciones de usuario con lista de elementos (de una compilación concreta)
Obtener recomendaciones de usuario de una compilación concreta del tipo "Recomendación" y lista de Hola de elementos adicionales.

Hola API devolverá una lista de elemento de predicción según el historial de uso de toohello del usuario de Hola y lista adicional de Hola de elementos.

Nota: no hay ninguna recomendación de usuario para la generación de FBT.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| userId |Identificador único del usuario de Hola |
| itemIds |Lista separada por comas de hello elementos toorecommend para. Longitud máxima: 1024 |
| numberOfResults |Número de resultados requeridos |
| includeMetatadata |Uso futuro, siempre es false |
| buildId |Hola compilar toouse de identificador para esta solicitud de recomendación |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating`-Calificación de recomendación de hello; número mayor significa mayor confianza.
* `Feed\entry\content\properties\Reasoning` : razonamiento de la recomendación (por ejemplo, explicaciones de recomendación).

Vea un ejemplo de respuesta en 12.1

## <a name="13-user-usage-history"></a>13. Historial de uso del usuario
Una vez que se creó un modelo de recomendación sistema Hola permitirá tooretrieve historial de usuarios de hello (usuario específico de elementos asociados tooa) utilizado para la compilación de Hola.
Esta API permitir que el historial de usuario de hello tooretrieve

Nota: historial de usuarios de hello actualmente solo está disponible para compilaciones de recomendación.

### <a name="131-retrieve-user-history"></a>13.1 Recuperación del historial del usuario
Recupera la lista de Hola de elemento utilizado en hello active generar u Hola especifica compilar para hello tiene el Id. de usuario.

| Método HTTP | URI |
|:--- |:--- |
| GET |Obtener el historial de usuario de Hola de compilación activa Hola.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Obtener historial de usuarios de Hola Hola proporcionado compilación`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Ejemplo:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único de Hello del modelo de Hola. |
| userId |Hola identificador único del usuario de Hola. |
| buildId |parámetro opcional, permitir tooindicate desde la compilación de historial de usuarios de hello debe ser fetch |
| apiVersion |1.0 |

**Respuesta:**

código de estado HTTP: 200

respuesta de Hello incluye una entrada por cada elemento recomendado. Cada entrada tiene Hola datos siguientes:

* `Feed\entry\content\properties\Id`: id. de elemento recomendado.
* `Feed\entry\content\properties\Name`-Nombre del elemento de saludo.
* `Feed\entry\content\properties\Rating` : N/D.
* `Feed\entry\content\properties\Reasoning` : N/D.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Notificaciones
Recomendaciones de aprendizaje de máquina Azure crea notificaciones cuando se producen los errores persistentes en el sistema de Hola. Hay 3 tipos de notificaciones:

1. Error de compilación: esta notificación se desencadena con cada error de compilación.
2. Error - esta notificación de procesamiento de adquisición de datos se desencadena cuando se tienen más de 100 errores en hello últimos 5 minutos en el procesamiento de Hola de eventos de uso por el modelo.
3. Error de consumo de recomendación: esta notificación se desencadena cuando se tienen más de 100 errores en hello últimos 5 minutos en el procesamiento de Hola de solicitudes de recomendación por modelo.

### <a name="141-get-notifications"></a>14.1. Obtener notificaciones
Recupera todas las notificaciones de Hola para todos los modelos o para un único modelo.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Obtener todas las notificaciones de todos los modelos:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Ejemplo de obtener las notificaciones para un modelo específico:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Parámetro opcional. Cuando se omite, obtendrá todas las notificaciones para todos los modelos. <br>Valor válido: identificador único del modelo de Hola. |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta:**

código de estado HTTP: 200

OData XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Eliminar notificaciones de modelo
Elimina todas las notificaciones de lectura para un modelo.

| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Ejemplo:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| modelId |Identificador único del modelo de Hola |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

### <a name="143-delete-user-notifications"></a>14.3. Eliminar notificaciones de usuario
Elimina todas las notificaciones para todos los modelos.

| Método HTTP | URI |
|:--- |:--- |
| DELETE |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Nombre de parámetro | Valores válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Cuerpo de la solicitud |NINGUNA |

**Respuesta**:

código de estado HTTP: 200

## <a name="15-legal"></a>15. Información legal
Este documento se proporciona "como está". La información y las opiniones expresadas en este documento, como las direcciones URL y otras referencias a sitios web de Internet, pueden cambiar sin previo aviso.<br><br>
Algunos ejemplos mencionados se proporcionan únicamente con fines ilustrativos y son ficticios. No se pretende ninguna asociación o conexión real ni debe deducirse.<br><br>
Este documento no proporcionan ningún derecho legal tooany la propiedad intelectual de ningún producto de Microsoft. Puede copiar y usar este documento con fines internos y de referencia.<br><br>
© 2015 Microsoft. Todos los derechos reservados.

