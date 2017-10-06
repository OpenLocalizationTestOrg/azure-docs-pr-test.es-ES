---
title: aaaGuide toocreating un servicio de datos para hello Marketplace | Documentos de Microsoft
description: "Instrucciones detalladas de cómo toocreate, certificar e implementar un servicio de datos para la venta en hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Descripción del esquema de nodos de Hola para asignar un tooOData de servicio web existente a través de CSDL
> [!IMPORTANT]
> **En este momento, ya no se pueden incorporar nuevos editores del Servicio de datos. No se aprobarán nuevos servicios de datos para mostrarse en lista.** Si tiene una aplicación de negocio de SaaS desea toopublish en AppSource encontrará información más [aquí](https://appsource.microsoft.com/partners). Si tiene aplicaciones IaaS o desarrollador del servicio quiere como toopublish en Azure Marketplace también puede encontrar más información [aquí](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Este documento le ayudará a aclarar la estructura de nodo de Hola para asignar un tooCSDL de Protocolo OData. Es importante toonote que la estructura del nodo Hola está bien formado XML. Por tanto, el esquema de raíz, primarios y secundarios se puede aplicar al diseñar una asignación de OData.

## <a name="ignored-elements"></a>Elementos omitidos
Hola siguientes son Hola alto nivel CSDL elementos (nodos XML) que no van toobe usado back-end de hello Azure Marketplace durante la importación de Hola de metadatos del servicio de hello web. Pueden estar presentes, pero se omitirán.

| Elemento | Scope |
| --- | --- |
| Elemento Using |nodo de Hello, subnodos y todos los atributos |
| Elemento Documentation |nodo de Hello, subnodos y todos los atributos |
| ComplexType |nodo de Hello, subnodos y todos los atributos |
| Element Association |nodo de Hello, subnodos y todos los atributos |
| Propiedad extendida |nodo de Hello, subnodos y todos los atributos |
| EntityContainer |Solo hello siguientes se omiten los atributos: *extiende* y *AssociationSet* |
| Esquema |Solo hello siguientes se omiten los atributos: *Namespace* |
| FunctionImport |Solo hello siguientes se omiten los atributos: *modo* (valor predeterminado de ln se supone) |
| EntityType |Solo hello siguiente sub se omiten dichos nodos: *clave* y *PropertyRef* |

Hola a continuación describe Hola cambios (agregado y omite los elementos) toohello varios nodos de CSDL XML en detalle.

## <a name="functionimport-node"></a>Nodo FunctionImport
Un nodo de FunctionImport representa una dirección URL (punto de entrada) que expone un usuario final toohello de servicio. nodo de Hello permite que describen cómo se trata los URL hello, qué parámetros son toohello disponibles para el usuario final y cómo se proporcionan estos parámetros.

Encontrará más información sobre este nodo [aquí][MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx).

Hello siguientes son atributos adicionales de hello (o adiciones tooattributes) que se exponen por nodo de FunctionImport hello:

**d:baseUri** -plantilla URI de hello para el recurso REST de Hola que está expuesto tooMarketplace. Marketplace utilice consultas de tooconstruct de plantilla de hello en hello servicio web REST. plantilla URI de Hello contiene marcadores de posición para los parámetros de hello en formato Hola {parameterName}, donde parameterName es nombre de Hola de parámetro hello. Ejemplo: apiVersion={versiónDeAPI}.
Se permiten parámetros tooappear como parámetros URI o como parte de la ruta de acceso URI de Hola. En caso de hello de aspecto de hello en la ruta de acceso de hello siempre son obligatorios (no se pueden marcar como que acepta valores NULL). *Ejemplo:*`d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Nombre de** -nombre de Hola de hello función importada.  No puede ser Hola igual que otros nombres definidos en hello CSDL.  Ejemplo: Name = "GetModelUsageFile"

**EntitySet** *(opcional)* : si la función hello devuelve una colección de tipos de entidad, el valor de Hola de hello **EntitySet** debe ser la que pertenece la colección Hola Hola entidad conjunto toowhich. En caso contrario, Hola **EntitySet** atributo no debe usarse. *Ejemplo:*`EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(opcional)* -especifica tipo hello de elementos devueltos por hello URI.  No utilice este atributo si Hola función no devuelve un valor. Estos de Hello son tipos de hello admitida:

* **Collection (<Entity type name>)**: especifica una colección de tipos de entidad definidos. nombre de Hola está presente en el atributo de nombre de hello del nodo de EntityType de Hola. Un ejemplo es Collection(WXC.HourlyResult).
* **Sin formato (<mime type>)**: especifica un documento o blob sin formato que se devuelve toohello usuario. Un ejemplo es Raw(image/jpeg). Otros ejemplos:

  * ReturnType="Raw(text/plain)"
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*

**d:Paging** -especifica cómo controlar la paginación Hola recursos REST. Hola valores se utilizan en las bifurcaciones de parámetro, por ejemplo, página = {$page} & itemsperpage = Hola {$size} opciones disponibles son:

* **None:** no hay paginación disponible
* **Skip:** la paginación se expresa mediante un "skip" y "take" (arriba) lógicos. Omitir comía Traer y M elementos, a continuación, devuelve Hola siguiente N elementos. Valor de parámetro: $skip
* **Take:** toman devuelve Hola siguiente N elementos. Valor de parámetro: $take
* **PageSize:** la paginación se expresa mediante una página y un tamaño lógicos (elementos por página). Página representa la página actual de Hola que se devuelve. Valor de parámetro: $page
* **Tamaño:** tamaño representa el número de Hola de elementos devueltos por cada página. Valor de parámetro: $size

**d:AllowedHttpMethods** *(opcional)* -especifica el verbo que se controla mediante el recurso de REST de Hola. Además, restringe toohello aceptado verbo especificado valor.  Valor predeterminado = POST.  *Ejemplo:* `d:AllowedHttpMethods="GET"` hello las opciones disponibles son:

* **GET:** normalmente utilizan datos tooreturn
* **ENTRADA:** normalmente utilizan tooinsert nuevos datos
* **PUT:** normalmente utilizan datos tooupdate
* **DELETE:** toodelete datos usados

Nodos secundarios adicionales (es decir, no está cubiertos por la documentación de CSDL de Hola) en el nodo de FunctionImport Hola son:

**d:RequestBody** *(opcional)* -solicitud Hola cuerpo es tooindicate usado que Hola solicitud espera un toobe cuerpo enviado. Parámetros pueden indicarse en el cuerpo de la solicitud de saludo. Se expresa en entre corchetes, por ejemplo, {parameterName}. Estos parámetros se asignan desde Hola proporcionados por el usuario en el cuerpo de hello transfieren servicio del proveedor de toohello contenido. elemento de Hello requestBody tiene un atributo con nombre httpMethod. atributo de Hello permite a dos valores:

* **ENTRADA:** usa si la solicitud de hello es un HTTP POST
* **GET:** usa si la solicitud de hello es un HTTP GET

    Ejemplo:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces** y **d:Namespace** -este nodo describe los espacios de nombres de Hola que se definen en hello XML devuelto por la importación de funciones de hello (URI del extremo). Hola XML devuelto por el servicio de back-end de hello puede incluir cualquier número de contenido de hello toodifferentiate de espacios de nombres que se devuelve. **Es necesario todos estos espacios de nombres, si se utiliza en consultas XPath d:Map o d:Match toobe enumerado.** nodo de Hello d:Namespaces contiene una conjunto/lista de nodos de d:Namespace. Cada uno de ellos muestra un espacio de nombres utilizado en la respuesta del servicio de back-end de Hola. atributo Hola del nodo de hello d:Namespace son las siguientes de Hello:

* **d:prefix:** Hola prefijo de espacio de nombres de hello, tal como se muestra resultados de la Hola XML devueltos por el servicio de hello, por ejemplo, f:FirstName, f:LastName, donde f es el prefijo de Hola.
* **d:URI:** Hola URI completo del espacio de nombres de hello utilizado en el documento de resultado de hello. Representa el valor de hello ese prefijo hello es tooat resolver en tiempo de ejecución.

**d:ErrorHandling***(opcional)* : este nodo contiene las condiciones para el control de errores. Cada una de las condiciones de Hola se valida con el resultado de hello devuelto por el servicio del proveedor de hello contenido. Si una condición coincide con hello propuesto código de error HTTP un mensaje de error se devuelve toohello por el usuario final.

**d:ErrorHandling** *(opcional)* y **d:Condition** *(opcional)* -un nodo de condición contiene una condición que se comprueba en el resultado de hello devuelto por servicio del proveedor de Hello contenido. Hello siguientes son hello **requiere** atributos:

* **d:match:** expresión XPath que valida si se encuentra presente en el proveedor de contenido de hello un determinado nodo/valor de salida de XML. Hola XPath se ejecuta en la salida de hello y debe devolver true si la condición de hello es una coincidencia o false en caso contrario.
* **d:HttpStatusCode:** Hola código de estado HTTP que se debe devolver Marketplace en Hola Hola mayúsculas condición coincidencias. Marketplace signalizes usuario toohello de errores a través de códigos de estado HTTP. Vea una lista de los códigos de estado HTTP en https://es.wikipedia.org/wiki/Anexo:Códigos_de_estado_HTTP.
* **d:errorMessage:** mensaje de error de Hola que es devuelta – con el código de estado HTTP de hello: toohello por el usuario final. Debe ser de un mensaje de error descriptivo que no contenga secretos.

**d:Title** *(opcional)* -permite describir título Hola de función hello. valor de Hola de título de hello procede de

* Hola opcional map atributo (una expresión xpath) que especifica donde toofind título de Hola en respuesta Hola procedentes de la solicitud de servicio de Hola.
* - O - título de hello especificado como valor del nodo de Hola.

**d:Rights** *(opcional)* -Hola derechos (por ejemplo, copyright) asociados con la función hello. valor de Hola para los derechos de hello procede de:

* Hola opcional map atributo (una expresión xpath) que especifica donde toofind derechos de Hola en respuesta Hola proceden de la solicitud de servicio de Hola.
* O bien derechos de hello especificados como valor del nodo de Hola.

**d:Description** *(opcional)* : una breve descripción de la función hello. valor de Hola para descripción Hola procede de

* Hola opcional map atributo (una expresión xpath) que especifica donde toofind descripción de Hola en respuesta Hola procedentes de la solicitud de servicio de Hola.
* - O – descripción Hola especificada como valor del nodo de Hola.

**d:EmitSelfLink** - *consulte el ejemplo anterior "FunctionImport para 'Paging' a través de los datos devueltos"*

**d:EncodeParameterValue** -tooOData extensión opcional

**d:QueryResourceCost** -tooOData extensión opcional

**d:Map** -tooOData extensión opcional

**d:Headers** -tooOData extensión opcional

**d:Headers** -tooOData extensión opcional

**d:Value** -tooOData extensión opcional

**d:HttpStatusCode** -tooOData extensión opcional

**d:ErrorMessage** -tooOData extensión opcional

## <a name="parameter-node"></a>Nodo Parameter
Este nodo representa un parámetro que se exponga como parte de la plantilla URI de Hola / cuerpo que se ha especificado en el nodo de FunctionImport hello de la solicitud.

Se encuentra una página de documento de gran utilidad para obtener más información sobre el nodo de "Elemento de parámetro" hello en [aquí](http://msdn.microsoft.com/library/ee473431.aspx) (Hola de uso **versión otros** desplegable tooselect una versión diferente si es necesario tooview Hola documentación). *Ejemplo:*`<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Atributo del parámetro | Es obligatorio | Valor |
| --- | --- | --- |
| Nombre |Sí |nombre de Hello del parámetro hello. Distingue mayúsculas de minúsculas  Coincidir mayúsculas y minúsculas BaseUri Hola. **Ejemplo:**`<Property Name="IsDormant" Type="Byte" />` |
| Tipo |Sí |tipo de parámetro de Hola. Hola valor debe ser un **EDMSimpleType** o un tipo complejo que está dentro del ámbito de Hola de modelo de Hola. Para más información, consulte "Tipos que se admiten en parámetros y propiedades".  (Distingue mayúsculas de minúsculas. El primer carácter está en mayúsculas y el resto en minúsculas.)  Vea también [Tipos de modelos conceptuales (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx). **Ejemplo:**`<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |No |**En**, Out o InOut dependiendo de si el parámetro hello es una entrada, salida o parámetro de entrada/salida. ("IN" es el único disponible en Azure Marketplace). **Ejemplo:**`<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |No |longitud del parámetro de Hola Hola máxima permitida. **Ejemplo:**`<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Precision |No |precisión de Hola de parámetro hello. **Ejemplo:**`<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Escala |No |escala de Hola de parámetro hello. **Ejemplo:**`<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Hola Hola atributos que se han agregado a la especificación de CSDL toohello son:

| Atributo del parámetro | Description |
| --- | --- |
| **d:Regex***(opcional)* |Una instrucción de expresión regular usa toovalidate valor de entrada de hello para el parámetro hello. Si el valor de entrada de hello no coincide con el valor de la instrucción Hola Hola se rechaza. Esto permite toospecify también un conjunto de posibles valores, por ejemplo, ^ [0-9] +? $ tooonly Permitir números. **Ejemplo:** `&lt;Parameter Name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="Un nombre no puede contener espacios ni caracteres no alfanuméricos o distintos del inglés" d:SampleValues="George |
| **d:Enum***(opcional)* |Lista de valores válidos para el parámetro hello separada de una canalización. tipo de Hola de valores de hello necesita toomatch Hola definido por tipo de hello parámetro. Ejemplo: `inglés |
| **d.: Nullable***(opcional)* |Permite definir si un parámetro puede ser nulo. valor predeterminado de Hello es: true. Sin embargo, los parámetros que se exponen como parte de la ruta de acceso de hello en plantilla URI de hello no pueden ser null. Cuando se establece el atributo de hello toofalse para estos parámetros: Hola proporcionados por el usuario se reemplaza. **Ejemplo:**`<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue***(opcional)* |Un valor de ejemplo toodisplay como una nota toohello cliente Hola interfaz de usuario.  Es posible enumerar tooadd separados de varios valores mediante el uso de una canalización, es decir, ' un |

## <a name="entitytype-node"></a>Nodo EntityType
Este nodo representa uno de los tipos de Hola que se devuelven de Marketplace toohello del usuario final. También contiene la asignación de Hola de salida de hello devuelto por los valores de toohello del servicio del proveedor de hello contenido que se devuelven toohello por el usuario final.

Obtener más información acerca de este nodo se encuentra en [aquí](http://msdn.microsoft.com/library/bb399206.aspx) (Hola de uso **versión otros** desplegable tooselect una versión diferente si es necesario tooview Hola documentación.)

| Nombre del atributo | Es obligatorio | Valor |
| --- | --- | --- |
| Nombre |Sí |nombre de Hola Hola del tipo de entidad. **Ejemplo:**`<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |No |nombre de Hola de otro tipo de entidad que es Hola tipo base del tipo de entidad de Hola que se está definiendo. **Ejemplo:**`<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Hola Hola atributos que se han agregado a la especificación de CSDL toohello son:

**d:Map** -expresión de XPath que se ejecuta en el resultado del servicio de Hola. Hello suposición aquí es que el resultado del servicio de hello contiene un conjunto de elementos que se repiten, como una ATOM fuente donde hay un conjunto de nodos de entrada que se repiten. Cada uno de estos nodos contiene un registro. Hola XPath es toopoint especificado en el nodo repetido individuales de hello en el resultado del servicio del proveedor de hello contenido que contiene valores de hello para un registro individual. Ejemplo de salida del servicio de hello:

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Hola expresión XPath sería /foo/bar porque cada nodo de la barra de hello es hello repetir nodo Hola de salida y contiene contenido real de Hola que se devuelve toohello por el usuario final.

**Key** : Marketplace omite este atributo. Servicios web basados en REST, en general no exponen una clave principal.

## <a name="property-node"></a>Nodo Property
Este nodo contiene una propiedad del registro de hello.

Obtener más información acerca de este nodo se encuentra en [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (Hola de uso **versión otros** desplegable tooselect una versión diferente si es necesario tooview Hola documentación.) *Ejemplo:*`<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | requeridos | Valor |
| --- | --- | --- |
| Nombre |Sí |nombre de Hola de propiedad de Hola. |
| Tipo |Sí |tipo de Hola Hola del valor de propiedad. tipo de valor de propiedad de Hello debe ser un **EDMSimpleType** o un tipo complejo (indicada mediante un nombre completo) que está dentro del ámbito del modelo de Hola. Para más información, consulte Tipos de modelos conceptuales (CSDL). |
| Nullable |No |**True** (Hola el valor predeterminado) o **False** dependiendo de si la propiedad de hello puede tener un valor null. Nota: Hola versión de CSDL indicado por hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) espacio de nombres, una propiedad de tipo complejo debe tener Nullable = "False". |
| DefaultValue |No |valor predeterminado de Hola de propiedad Hola. |
| MaxLength |No |longitud máxima de Hola Hola del valor de propiedad. |
| FixedLength |No |**True** o **False** dependiendo de si el valor de propiedad de Hola se almacenarán como una cadena de longitud fiexed. |
| Precision |No |Se refiere toohello el número máximo de dígitos tooretain en valor numérico de Hola. |
| Escala |No |Número máximo de tooretain de posiciones decimales en el valor numérico de Hola. |
| Unicode |No |**True** o **False** dependiendo de si el valor de propiedad de hello ser almacenado como una cadena Unicode. |
| Collation |No |Una cadena que especifica hello toobe de secuencia utilizado en el origen de datos de Hola de intercalación. |
| ConcurrencyMode |No |**Ninguno** (Hola el valor predeterminado) o **Fixed**. Si el valor de Hola se establece demasiado**Fixed**, se usará el valor de propiedad de hello en las comprobaciones de simultaneidad optimista. |

Hola Hola atributos adicionales que se han agregado a la especificación de CSDL toohello son:

**d:Map** -expresión de XPath que se ejecuta en el servicio de Hola de salida y extrae una propiedad de salida de hello. Hola XPath especificada es relativa toohello nodo que se ha seleccionado en el XPath del nodo de hello EntityType de repetición. También es posible toospecify un tooallow XPath absoluta e incluye un recurso estático en cada uno de hello salida nodos, como por ejemplo una instrucción de copyright que se encuentra solo una vez en hello servicio original de salida pero debe estar presente en cada una de las filas de Hola Hola OData salida. Ejemplo de servicio de hello:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

expresión de XPath Hola aquí sería ./bar/baz0 tooget hello baz0 nodo servicio de proveedor de hello contenido.

**d:CharMaxLength** -para el tipo de cadena, puede especificar la longitud máxima de Hola. Consulte DataService CSDL Example

**d:IsPrimaryKey** -indica si la columna hello es clave principal de hello en hello tabla/vista. Consulte DataService CSDL Example

**d:isExposed** -determina si se expone el esquema de la tabla de hello (generalmente true). Consulte DataService CSDL Example

**d:IsView***(opcional)* : true si se basa en una vista, en lugar de en una tabla.  Consulte DataService CSDL Example

**d:Tableschema** : consulte DataService CSDL Example

**d:ColumnName** -es Hola nombre de columna Hola de tabla o vista de Hola.  Consulte DataService CSDL Example

**d:IsReturned** -es un valor booleano que determina si Hola servicio expone este cliente para toohello el valor de hello.  Consulte DataService CSDL Example

**d:IsQueryable** -es hello un valor booleano que determina si se puede utilizar la columna de hello en una consulta de base de datos.   Consulte DataService CSDL Example

**d:OrdinalPosition** -es la posición de la columna de hello numéricos de apariencia, x, en la tabla de Hola o vista de hello, donde x es de 1 toohello número de columnas de tabla de Hola.  Consulte DataService CSDL Example

**d:DatabaseDataType** -es Hola el tipo de datos de columna de hello en la base de datos de hello, es decir, el tipo de datos SQL. Consulte DataService CSDL Example

## <a name="supported-parametersproperty-types"></a>Tipos que se admiten en parámetros y propiedades
siguiente Hola es tipos de hello admitida para los parámetros y propiedades. (Distingue mayúsculas de minúsculas)

| Tipos primitivos | Description |
| --- | --- |
| Null |Representa la ausencia de Hola de un valor |
| Booleano |Representa el concepto matemático de Hola de lógica de valores binarios |
| Byte |Valor entero de 8 bits sin signo |
| DateTime |Representa una fecha y hora con valores desde las 00:00:00 del 1 de enero de 1753 d. C. a las 11:59:59 del 31 de diciembre de 9999 d. C. |
| DECIMAL |Representa valores numéricos con precisión y escala fijas. Este tipo puede describir un valor numérico comprendido entre 10 negativo ^ toopositive 255 + 1 10 ^-255 1 |
| Double |Representa un número de punto flotante con una precisión de 15 dígitos que puede representar valores con un intervalo aproximado de ± 2,23e-308 a 1,79e+308. **Usar el valor Decimal debido tooExel problema de exportación** |
| Single |Representa un número de punto flotante con una precisión de 7 dígitos que puede representar valores con un intervalo aproximado de ± 1,18e-38 a 3,40e+38. |
| Guid |Representa un valor de identificador único de 16 bytes (128 bits) |
| Int16 |Representa un valor entero de 16 bits con signo |
| Int32 |Representa un valor entero de 32 bits con signo |
| Int64 |Representa un valor entero de 64 bits con signo |
| String |Representa datos de caracteres de longitud fija o variable |

## <a name="see-also"></a>Otras referencias
* Si está interesado en conocer Hola proceso general de asignación de OData y su propósito, lea este artículo [asignación de OData del servicio de datos](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definiciones, estructuras e instrucciones.
* Si está interesado en Revisar ejemplos, lea este artículo [ejemplos de asignación de datos de servicios OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de ejemplo y comprender la sintaxis del código y el contexto.
* toohello tooreturn lo prescrito, ruta de acceso para publicar un servicio de datos de toohello Azure Marketplace, lea este artículo [Guía de publicación de servicio de datos](marketplace-publishing-data-service-creation.md).
