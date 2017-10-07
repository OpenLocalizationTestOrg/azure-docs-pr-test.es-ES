---
title: "conceptos de desarrollador de catálogo aaaData | Documentos de Microsoft"
description: "Conceptos clave de toohello de introducción en el modelo conceptual de catálogo de datos de Azure, tal como se expone a través de Hola API de REST de catálogo."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Conceptos para desarrolladores del Catálogo de datos de Azure
**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que proporciona capacidades de detección de origen de datos y para metadatos de origen de datos de micromecenazgo. Los desarrolladores pueden usar el servicio de Hola a través de sus API de REST. Descripción de los conceptos de hello implementados en el servicio de hello es importante para los desarrolladores integrar toosuccessfully con **el catálogo de datos**.

## <a name="key-concepts"></a>Conceptos clave
Hola **el catálogo de datos** modelo conceptual se basa en cuatro conceptos claves: Hola **catálogo**, **usuarios**, **activos**y **Anotaciones**.

![concepto][1]

*Figura 1: Modelo conceptual simplificado del Catálogo de datos de Azure*

### <a name="catalog"></a>Catálogo
A **catálogo** es el contenedor de nivel superior de Hola para todos los metadatos de una organización almacena de Hola. Se permite un **catálogo** por cuenta de Azure. Los catálogos son ligada tooan suscripción de Azure, pero solo una **catálogo** pueden crearse para cualquier cuenta de Azure determinado, incluso aunque una cuenta puede tener varias suscripciones.

Un catálogo contiene **usuarios** y **recursos**.

### <a name="users"></a>Usuarios
Los usuarios son entidades de seguridad que tienen permisos tooperform acciones (realizar búsquedas en el catálogo de hello, agregar, editar o eliminar elementos, etc.) en hello catálogo.

Existen diferentes roles que un usuario puede tener. Para obtener información sobre roles, consulte sección Hola Roles y la autorización.

Se pueden agregar usuarios individuales y grupos de seguridad.

Catálogo de datos de Azure usa Azure Active Directory para la administración de identidades y acceso. Cada usuario de catálogo debe ser miembro del programa Hola a Active Directory para la cuenta de hello.

### <a name="assets"></a>Recursos
Un **catálogo** contiene recursos de datos. **Activos** son unidad Hola de granularidad administrado por catálogo Hola.

granularidad de Hola de un recurso varía según el origen de datos. Para una o Base de datos SQL Server o de Oracle, un recurso puede ser una tabla o una vista. Para SQL Server Analysis Services, un recurso puede ser una medida, una dimensión o un indicador clave de rendimiento (KPI). Para SQL Server Reporting Services, un recurso es un informe.

Un **Asset** es Hola para agrega o quitar en un catálogo. Es unidad Hola de resultados que obtendrá de **búsqueda**.

Un **Recurso** está compuesto por su nombre, ubicación y tipo, así como de las anotaciones que lo describen.

### <a name="annotations"></a>anotaciones
Las anotaciones son elementos que representan los metadatos acerca de los recursos.

Ejemplos de las anotaciones incluyen descripciones, etiquetas, esquemas, documentación, etc. Una lista completa de tipos de recurso de Hola y tipos de anotación se encuentran en hello sección del modelo de objeto de recurso.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Anotaciones de micromecenazgo y perspectiva del usuario (multiplicidad de opinión)
Un aspecto clave del catálogo de datos de Azure es cómo admite crowdsourcing Hola de metadatos en el sistema de Hola. Como enfoque de wiki tooa opuestos: donde sólo hay una opinión y Hola último escritor gana: modelo del catálogo de datos de Azure Hola permite varias opiniones toolive en paralelo en el sistema de Hola.

Este método refleja Hola mundo real de los datos empresariales que usuarios diferentes pueden tener distintas perspectivas en un recurso:

* Un administrador de base de datos puede proporcionar información sobre los contratos de nivel de servicio o la ventana de procesamiento disponibles Hola de las operaciones masivas ETL
* Un administrador de datos puede proporcionar información sobre Hola business procesos toowhich Hola activo se aplica o clasificaciones Hola Hola business aplicada tooit
* Un analista financiero puede proporcionar información acerca de cómo se usan los datos de Hola durante tareas de informes de final de período

toosupport en este ejemplo, cada usuario: Hola DBA, Administrador de datos de Hola y Hola analista: puede agregar una descripción tooa única tabla que se ha registrado en el catálogo de Hola. Todas las descripciones se mantienen en el sistema de hello y, en el portal del catálogo de datos de Azure Hola se muestran todas las descripciones.

Este patrón es aplicado toomost de elementos de hello en el modelo de objetos de hello, por lo que los tipos de objeto en la carga JSON de hello son a menudo las matrices de propiedades que cabría esperar un singleton.

Por ejemplo, en activos de hello raíz es una matriz de objetos de descripción. propiedad de la matriz de Hola se denomina "Descripción". Un objeto de descripción tiene una propiedad: description. patrón de Hello es que cada usuario que descripción de tipos Obtiene un objeto de descripción creado para valor de hello proporcionado por el usuario de Hola.

Hola UX, a continuación, puede elegir cómo toodisplay Hola combinación. A continuación se muestran tres modelos diferentes para mostrar.

* patrón de Hello más sencillo es "All". En este modelo, se muestran todos los objetos de hello en una vista de lista. portal del catálogo de datos de Azure Hola UX utiliza este patrón de descripción.
* Otro patrón es "Merge". En este modelo, todos los valores de hello de usuarios diferentes de Hola se combinan, con duplicado quitado. Ejemplos de este patrón en el portal del catálogo de datos de Azure Hola UX son propiedades de etiquetas y expertos de Hola.
* Un tercer patrón es "el último escritor gana". En este modelo, se muestra solo hello más reciente valor escrito. friendlyName es un ejemplo de este patrón.

## <a name="asset-object-model"></a>Modelo de objeto de recurso
Como se mencionó en la sección de conceptos clave de hello, Hola **el catálogo de datos** modelo de objetos incluye elementos, que pueden ser activos o anotaciones. Los elementos tienen propiedades, que pueden ser optional o required. Algunas propiedades aplican tooall elementos. Algunas propiedades aplican tooall activos. Algunas propiedades aplican toospecific solo los tipos de recurso.

### <a name="system-properties"></a>Propiedades del sistema
<table><tr><td><b>Nombre de la propiedad</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr><tr><td>timestamp</td><td>DateTime</td><td>último elemento de hello tiempo Hola se ha modificado. Este campo se genera por servidor hello cuando se inserta un elemento y cada vez que se actualiza un elemento. Hello valor de esta propiedad se pasa por alto en la entrada de las operaciones de publicación.</td></tr><tr><td>id</td><td>Identificador URI</td><td>Dirección url absoluta del elemento de hello (solo lectura). Es Hola URI direccionable único para el elemento de saludo.  Hello valor de esta propiedad se pasa por alto en la entrada de las operaciones de publicación.</td></tr><tr><td>type</td><td>String</td><td>tipo de Hola de activo de hello (solo lectura).</td></tr><tr><td>ETag</td><td>String</td><td>Una cadena correspondiente toohello versión de Hola elemento que puede usarse para el control de simultaneidad optimista al realizar operaciones que actualizan los elementos de catálogo de Hola. "*" puede ser cualquier valor de toomatch usado.</td></tr></table>

### <a name="common-properties"></a>Propiedades comunes
Estas propiedades aplican tipos de activos de tooall raíz y todos los tipos de anotación.

<table>
<tr><td><b>Nombre de la propiedad</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr>
<tr><td>fromSourceSystem</td><td>Booleano</td><td>Indica si los datos del elemento derivan de un sistema de origen (como base de datos de SQL Server, base de datos de Oracle) o creados por un usuario.</td></tr>
</table>

### <a name="common-root-properties"></a>Propiedades de raíz comunes
<p>
Estas propiedades aplican tipos de activos de tooall raíz.

<table><tr><td><b>Nombre de la propiedad</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr><tr><td>name</td><td>String</td><td>Un nombre derivado de la información de ubicación de origen de datos de Hola</td></tr><tr><td>dsl</td><td>DataSourceLocation</td><td>Unívocamente describe el origen de datos de Hola y es uno de los identificadores de hello para el activo de Hola. (Consulte la sección de identidad dual).  estructura de Hola de hello dsl varía en función del protocolo de Hola y tipo de origen.</td></tr><tr><td>dataSource</td><td>DataSourceInfo</td><td>Obtener más detalles sobre el tipo de Hola de activo.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Describe el usuario de Hola que registró más recientemente de este recurso.  Contiene el identificador único de hello para el usuario de hello (Hola upn) y un nombre para mostrar (lastName y firstName).</td></tr><tr><td>containerId</td><td>String</td><td>Identificador del recurso de contenedor de Hola Hola origen de datos. Esta propiedad no se admite para el tipo de contenedor de Hola.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Propiedades comunes de anotación no de singleton
Estas propiedades aplican tipos de anotación no singleton tooall (anotaciones, que permiten toobe varios por cada recurso).

<table>
<tr><td><b>Nombre de la propiedad</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr>
<tr><td>key</td><td>String</td><td>Clave que identifica de forma única anotación hello en la colección actual de hello especificado por el usuario. longitud de clave de Hello no puede superar los 256 caracteres.</td></tr>
</table>

### <a name="root-asset-types"></a>Tipos de recursos de raíz
Tipos de activos de raíz son Hola de esos tipos que representan varios tipos de recursos de datos que se pueden registrar en el catálogo de Hola. Para cada tipo de raíz, hay una vista, que describe los activos y las anotaciones que se incluyen en la vista de Hola. Nombre de la vista debe usarse en el segmento de dirección url de hello correspondiente {view_name} al publicar un activo mediante la API de REST.

<table><tr><td><b>Tipo de recurso (nombre de la vista)</b></td><td><b>Propiedades adicionales</b></td><td><b>Tipo de datos</b></td><td><b>Anotaciones permitidas</b></td><td><b>Comentarios</b></td></tr><tr><td>Tabla ("tables")</td><td></td><td></td><td>Description<p>FriendlyName<p>Etiqueta<p>Esquema<p>ColumnDescription<p>ColumnTag<p> Experto<p>Vista previa<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Documentación<p></td><td>Una tabla representa datos tabulares.  Por ejemplo, una tabla SQL, una vista SQL, una tabla del modelo tabular de Analysis Services, una dimensión multidimensional de Analysis Services, una tabla de Oracle, etc.   </td></tr><tr><td>Medidas ("measures")</td><td></td><td></td><td>Description<p>FriendlyName<p>Etiqueta<p>Experto<p>AccessInstruction<p>Documentación<p></td><td>Este tipo representa una medida de Analysis Services.</td></tr><tr><td></td><td>measure</td><td>Columna</td><td></td><td>Medida de metadatos que describen Hola</td></tr><tr><td></td><td>isCalculated </td><td>Booleano</td><td></td><td>Especifica si se calcula la medida de Hola o no.</td></tr><tr><td></td><td>measureGroup</td><td>String</td><td></td><td>Contenedor físico de medida</td></tr><td>KPI ("kpis")</td><td></td><td></td><td>Description<p>FriendlyName<p>Etiqueta<p>Experto<p>AccessInstruction<p>Documentación</td><td></td></tr><tr><td></td><td>measureGroup</td><td>String</td><td></td><td>Contenedor físico de medida</td></tr><tr><td></td><td>goalExpression</td><td>String</td><td></td><td>Una expresión numérica MDX o cálculo que devuelve el valor de destino de Hola de hello KPI.</td></tr><tr><td></td><td>valueExpression</td><td>String</td><td></td><td>Una expresión numérica MDX que devuelve el valor real de Hola de hello KPI.</td></tr><tr><td></td><td>statusExpression</td><td>String</td><td></td><td>Una expresión MDX que representa el estado de Hola de hello KPI en un punto determinado en el tiempo.</td></tr><tr><td></td><td>trendExpression</td><td>String</td><td></td><td>Una expresión MDX que evalúa el valor de Hola de hello KPI con el tiempo. tendencia de Hello puede ser cualquier criterio basado en tiempo que es útil en un contexto empresarial concreto.</td>
<tr><td>Informe ("reports")</td><td></td><td></td><td>Description<p>FriendlyName<p>Etiqueta<p>Experto<p>AccessInstruction<p>Documentación<p></td><td>Este tipo representa un informe de SQL Server Reporting Services </td></tr><tr><td></td><td>assetCreatedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>String</td><td></td><td></td></tr><tr><td>Contenedor ("containers")</td><td></td><td></td><td>Description<p>FriendlyName<p>Etiqueta<p>Experto<p>AccessInstruction<p>Documentación<p></td><td>Este tipo representa un contenedor de otros activos, como una base de datos SQL, un contenedor de blobs de Azure o un modelo de Analysis Services.</td></tr></table>

### <a name="annotation-types"></a>Tipos de anotación
Tipos de anotación representan tipos de metadatos que se pueden asignar a tipos de tooother de catálogo de Hola.

<table>
<tr><td><b>Tipo de anotación (nombre de la vista anidada)</b></td><td><b>Propiedades adicionales</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr>

<tr><td>Descripción ("descriptions")</td><td></td><td></td><td>Esta propiedad contiene una descripción para un recurso. Cada usuario del sistema de hello puede agregar su propia descripción.  Solo el usuario puede editar el objeto de descripción de Hola.  (Propietarios de activos y administradores pueden eliminar el objeto de descripción de hello pero no editarlo). sistema de Hello mantiene las descripciones de los usuarios por separado.  Por lo tanto, hay una matriz de descripciones de cada recurso (uno para cada usuario que ha contribuido sus conocimientos sobre los activos de hello, de toopossibly suma uno que contiene información derivada del origen de datos de hello).</td></tr>
<tr><td></td><td>description</td><td>cadena</td><td>Una descripción breve (2-3 líneas) del recurso de Hola</td></tr>

<tr><td>Etiqueta ("tags")</td><td></td><td></td><td>Esta propiedad define una etiqueta para un recurso. Cada usuario del sistema de hello puede agregar varias etiquetas para un activo.  Solo el usuario de Hola que crea objetos de la etiqueta puede modificarlos.  (Los propietarios de activos y administradores pueden elimine Hola etiqueta objeto, pero no editarlo). sistema de Hello mantiene las etiquetas de los usuarios por separado.  Por lo tanto, hay una matriz de objetos Tag en cada recurso.</td></tr>
<tr><td></td><td>etiqueta</td><td>cadena</td><td>Un recurso de Hola que describen de etiqueta.</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>Esta propiedad contiene un nombre descriptivo para un recurso. FriendlyName es una anotación de singleton y solo FriendlyName puede agregarse tooan activo.  Solo el usuario de Hola que creó el objeto FriendlyName puede modificarla. (Los propietarios de activos y administradores pueden elimine Hola FriendlyName objeto, pero no editarlo). sistema de Hello mantiene los nombres descriptivos de los usuarios por separado.</td></tr>
<tr><td></td><td>friendlyName</td><td>cadena</td><td>Un nombre descriptivo del recurso de Hola.</td></tr>

<tr><td>Esquema ("schema")</td><td></td><td></td><td>Hola esquema describe la estructura de Hola de datos de Hola.  Enumera los nombres de atributo (columna, atributo, campo, etc.) de hello, tipos y otros metadatos.  Esta información se deriva del origen de datos de Hola.  El esquema es una anotación de singleton: solo puede agregarse un esquema a un recurso.</td></tr>
<tr><td></td><td>columnas</td><td>Column[]</td><td>Una matriz de objetos de columna. Columna de Hola se describe con información derivada del origen de datos de Hola.</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>Esta propiedad contiene una descripción para una columna.  Cada usuario del sistema de hello puede agregar sus propias descripciones para varias columnas (a lo sumo uno por columna). Solo el usuario de Hola que crea objetos de ColumnDescription puede modificarlos.  (Los propietarios de activos y administradores pueden elimine hello ColumnDescription objeto, pero no editarlo). sistema de Hello mantiene las descripciones de columna del usuario por separado.  Por lo tanto, hay una matriz de objetos de ColumnDescription en cada activo (uno por cada columna para cada usuario que ha contribuido sus conocimientos acerca de la columna de hello además toopossibly uno que contenga información derivada del origen de datos de hello).  Hola ColumnDescription es flexible enlazado toohello esquema para que puedas no está sincronizado. Hola ColumnDescription puede describir una columna que ya no existe en el esquema de Hola.  Es una descripción de tookeep de sistema de escritura de toohello y el esquema sincronizado.  origen de datos de Hello también puede tener información de descripción de columnas y son objetos ColumnDescription adicionales que se crean cuando se ejecuta la herramienta de Hola.</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nombre de Hola de columna de hello a que esta descripción se refiere.</td></tr>
<tr><td></td><td>description</td><td>String</td><td>una breve descripción (2-3 líneas) de la columna de Hola.</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>Esta propiedad contiene una etiqueta para una columna. Cada usuario del sistema de hello puede agregar varias etiquetas para una columna determinada y puede agregar etiquetas de varias columnas. Solo el usuario de Hola que crea objetos de ColumnTag puede modificarlos. (Los propietarios de activos y administradores pueden elimine hello ColumnTag objeto, pero no editarlo). sistema de Hello mantiene las etiquetas de columna de estos usuarios por separado.  Por lo tanto, hay una matriz de objetos ColumnTag en cada recurso.  Hola ColumnTag es flexible enlazado toohello esquema para que puedas no está sincronizado. Hola ColumnTag puede describir una columna que ya no existe en el esquema de Hola.  Es la etiqueta de columna de toohello escritor tookeep y esquema sincronizado.</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nombre de Hola de columna de hello a que esta etiqueta se refiere.</td></tr>
<tr><td></td><td>etiqueta</td><td>String</td><td>Una columna de Hola que describen de etiqueta.</td></tr>

<tr><td>Experto ("experts")</td><td></td><td></td><td>Esta propiedad contiene un usuario que se considera a un experto en el conjunto de datos de Hola. opinions(descriptions) burbujas toohello parte superior los expertos Hello de hello UX al enumerar las descripciones. Cada usuario puede especificar sus propios expertos. Solo el usuario puede editar el objeto de expertos de Hola. (Propietarios activos y administradores pueden eliminar objetos experto de Hola pero no editarlo).</td></tr>
<tr><td></td><td>expert</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Vista previa ("previews")</td><td></td><td></td><td>vista previa de Hello contiene una instantánea de las 20 filas superior Hola de datos de los activos de Hola. La vista previa solo tiene sentido para algunos tipos de recursos (tiene sentido para las tablas, pero no para las medidas).</td></tr>
<tr><td></td><td>Vista previa</td><td>object[]</td><td>Matriz de objetos que representan una columna.  Cada objeto tiene una propiedad de asignación de columna de tooa con un valor para esa columna para la fila de Hola.</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>cadena</td><td>tipo de mime de Hola de hello contenido.</td></tr>
<tr><td></td><td>contenido</td><td>cadena</td><td>instrucciones de Hello sobre cómo tooget tener acceso a toothis datos activos. Hola contenido podría ser una dirección URL, una dirección de correo electrónico o un conjunto de instrucciones.</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>número de Hola de filas en el conjunto de datos de Hola</td></tr>
<tr><td></td><td>size</td><td>long</td><td>tamaño de Hello en bytes del conjunto de datos de Hola.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>cadena</td><td>se modifica el esquema de Hola de Hello última hora</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>cadena</td><td>se modificó el conjunto de datos de tiempo último de Hola Hola (los datos se ha agregado, modificado o eliminar)</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnas</td></td><td>ColumnDataProfile[]</td><td>Matriz de perfiles de datos de columna.</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nombre de Hola de columna de hello a que esta clasificación se refiere.</td></tr>
<tr><td></td><td>clasificación</td><td>String</td><td>clasificación de Hola de datos de hello en esta columna.</td></tr>

<tr><td>Documentación ("documentation")</td><td></td><td></td><td>Un activo dado solo puede tener una documentación asociada con él.</td></tr>
<tr><td></td><td>mimeType</td><td>cadena</td><td>tipo de mime de Hola de hello contenido.</td></tr>
<tr><td></td><td>contenido</td><td>cadena</td><td>contenido de la documentación de Hola.</td></tr>

</table>

### <a name="common-types"></a>Tipos comunes
Tipos comunes pueden usarse como tipos de Hola para las propiedades, pero no son elementos.

<table>
<tr><td><b>Tipo común</b></td><td><b>Propiedades</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sourceType</td><td>cadena</td><td>Describe el tipo de saludo de origen de datos.  Por ejemplo: SQL Server, Base de datos de Oracle, etc.  </td></tr>
<tr><td></td><td>objectType</td><td>cadena</td><td>Describe el tipo de saludo del objeto de origen de datos de Hola. Por ejemplo, tabla, vista de SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>protocolo</td><td>string</td><td>Necesario. Describe una toocommunicate de protocolo que se utiliza con el origen de datos de Hola. Por ejemplo, "tds" para SQl Server, "oracle" para Oracle, etc. Consulte demasiado[especificación de referencia - DSL estructura del origen de datos](data-catalog-dsr.md) para lista de Hola de protocolos actualmente admitidos.</td></tr>
<tr><td></td><td>address</td><td>Diccionario<string, object></td><td>Necesario. Dirección es un conjunto de protocolo de toohello específico de datos que es el origen de datos de hello tooidentify usado al que hace referencia. Hola dirección datos como ámbito tooa protocolo en particular, lo que significa que no tiene sentido sin conocer el protocolo de Hola.</td></tr>
<tr><td></td><td>Autenticación</td><td>string</td><td>Opcional. esquema de autenticación de Hello usa toocommunicate con origen de datos de Hola. Por ejemplo, windows, oauth, etc.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Diccionario<string, object></td><td>Opcional. Información adicional acerca de cómo el origen de datos de tooconnect tooa.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>Hola back-end no realiza ninguna validación de propiedades proporcionadas con AAD durante la publicación.</td></tr>
<tr><td></td><td>upn</td><td>string</td><td>Dirección de correo electrónico única del usuario. Debe especificarse si no se proporciona el Id. de objeto o en el contexto de Hola de propiedad "lastRegisteredBy", en caso contrario, opcional.</td></tr>
<tr><td></td><td>objectId</td><td>Guid</td><td>Identidad AAD de grupo de seguridad o usuario. Opcional. Debe especificarse si no se proporciona UPN; de lo contrario, es opcional.</td></tr>
<tr><td></td><td>firstName</td><td>string</td><td>Nombre de usuario (para fines de presentación). Opcional. Solo es válido en el contexto de Hola de propiedad "lastRegisteredBy". No se puede especificar al proporcionar la entidad de seguridad para "roles", "permisos" y "expertos".</td></tr>
<tr><td></td><td>lastName</td><td>string</td><td>Apellidos del usuario (para fines de presentación). Opcional. Solo es válido en el contexto de Hola de propiedad "lastRegisteredBy". No se puede especificar al proporcionar la entidad de seguridad para "roles", "permisos" y "expertos".</td></tr>

<tr><td>Columna</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>cadena</td><td>Nombre de columna de Hola o atributo.</td></tr>
<tr><td></td><td>type</td><td>cadena</td><td>tipo de datos de columna de Hola o el atributo. tipos permitidos de Hola dependen del tipo de origen de datos del recurso de Hola.  Solo se admite un subconjunto de tipos.</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>longitud máxima de Hello permitida para la columna de Hola o el atributo. Derivada del origen de datos. Solo tipos de origen de toosome es aplicable.</td></tr>
<tr><td></td><td>precision</td><td>byte</td><td>precisión de Hola para hello columna o atributo. Derivada del origen de datos. Solo tipos de origen de toosome es aplicable.</td></tr>
<tr><td></td><td>isNullable</td><td>Booleano</td><td>Si es la columna de hello permiten toohave un valor null o no. Derivada del origen de datos. Solo tipos de origen de toosome es aplicable.</td></tr>
<tr><td></td><td>expresión</td><td>cadena</td><td>Si el valor de hello es una columna calculada, este campo contiene la expresión Hola que expresa el valor de Hola. Derivada del origen de datos. Solo tipos de origen de toosome es aplicable.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>cadena</td><td>nombre de Hola de columna de Hola</td></tr>
<tr><td></td><td>type </td><td>cadena</td><td>tipo de Hola de columna de Hola</td></tr>
<tr><td></td><td>Min </td><td>cadena</td><td>valor mínimo de Hola Hola conjunto de datos</td></tr>
<tr><td></td><td>max </td><td>cadena</td><td>valor máximo de Hola Hola conjunto de datos</td></tr>
<tr><td></td><td>avg </td><td>double</td><td>valor promedio de Hola Hola conjunto de datos</td></tr>
<tr><td></td><td>stdev </td><td>double</td><td>desviación estándar de Hello para el conjunto de datos de Hola</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>recuento de Hola de valores null en el conjunto de datos de Hola</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>recuento de Hola de valores distintos en el conjunto de datos de Hola</td></tr>


</table>

## <a name="asset-identity"></a>Identidad de recursos
Catálogo de datos de Azure usa "protocol" y las propiedades de identidad de bolsa de propiedades "address" hello de hello DataSourceLocation "dsl" propiedad toogenerate identidad del activo de hello, que es usado tooaddress Hola asset dentro de hello catálogo.
Por ejemplo, el protocolo de "tds" hello tiene propiedades de identidad "server", "base de datos", "schema" y "objeto". combinaciones de Hola de protocolo de Hola y propiedades de identidad de Hola son utilizados toogenerate Hola identidad de hello activos de tabla de SQL Server.
Catálogo de datos de Azure proporciona varios protocolos de origen de datos integrados que se enumeran en [Especificación de referencia de origen de datos: estructura de DSL](data-catalog-dsr.md).
Hello conjunto de protocolos admitidos se puede extender mediante programación (consulte la referencia de la API de REST de catálogo tooData). Los administradores de hello catálogo pueden registrar los protocolos de origen de datos personalizado. Hello tabla siguiente describen propiedades necesarias de hello tooregister un protocolo personalizado.

### <a name="custom-data-source-protocol-specification"></a>Especificación del protocolo de orígenes de datos personalizados
<table>
<tr><td><b>Tipo</b></td><td><b>Propiedades</b></td><td><b>Tipo de datos</b></td><td><b>Comentarios</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>espacio de nombres</td><td>cadena</td><td>espacio de nombres de Hello del protocolo de Hola. Namespace debe ser de 1 too255 caracteres, contener uno o más partes no vacías separadas por punto (.). Cada parte debe estar entre 1 too255 caracteres, comenzar con una letra y contener sólo letras y números.</td></tr>
<tr><td></td><td>name</td><td>cadena</td><td>nombre de Hello del protocolo de Hola. Nombre debe tener entre 1 too255 caracteres, comenzar con una letra y contener solo letras, números y caracteres de guión (-) Hola.</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty[]</td><td>Lista de propiedades de identidad, debe contener al menos una, pero no más de 20 propiedades. Por ejemplo: "server", "base de datos", "esquema", "object" es propiedades de identidad de protocolo de "tds" Hola.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet[]</td><td>Lista de conjuntos de identidades. Define conjuntos de propiedades de identidad que representan la identidad del recurso válido. Debe contener al menos una, pero no más de 20 propiedades. Por ejemplo: {"server", "database", "schema" y "object"} es un conjunto de identidades para el protocolo "tds", que define la identidad del recurso de tabla de Sql Server.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>cadena</td><td>nombre de Hola de propiedad de Hola. Nombre debe ser de 1 too100 caracteres, empiece con una letra y puede contener sólo letras y números.</td></tr>
<tr><td></td><td>type</td><td>cadena</td><td>tipo de Hola de propiedad de Hola. Valores admitidos: "bool", "boolean", "byte", "guid", "int", "integer", "long", "string", "url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>booleano</td><td>Indica si se ignoran las mayúsculas y minúsculas al usar el valor de la propiedad. Solo puede especificarse para las propiedades de tipo "string". El valor predeterminado es False.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool[]</td><td>Indica si se debe omitir el caso de cada segmento de ruta de acceso de la dirección url de Hola. Solo puede especificarse para las propiedades de tipo "url". El valor predeterminado es [false].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>cadena</td><td>nombre de Hello del conjunto de identidades de Hola.</td></tr>
<tr><td></td><td>propiedades</td><td>string[]</td><td>Hola lista de propiedades de identidad incluidas en esta identidad de conjunto. No puede contener duplicados. Cada propiedad de identidad se ha establecido al que hace referencia debe definirse en lista de Hola de "identityProperties" del protocolo de Hola.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Roles y autorización
Catálogo de datos de Microsoft Azure proporciona capacidades de autorización para las operaciones CRUD en recursos y anotaciones.

## <a name="key-concepts"></a>Conceptos clave
Hola el catálogo de datos utiliza dos mecanismos de autorización:

* Autorización basada en roles
* Autorización basada en permisos

### <a name="roles"></a>Roles
Existen tres roles: **Administrador**, **Propietario** y **Colaborador**.  Cada rol tiene su ámbito y derechos, que se resumen en hello en la tabla siguiente.

<table><tr><td><b>Rol</b></td><td><b>Ámbito</b></td><td><b>Derechos</b></td></tr><tr><td>Administrador</td><td>Catálogo (todos los activos/anotaciones en hello catálogo)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Propietario</td><td>Cada recurso (elemento raíz)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Colaborador</td><td>Cada recurso y anotación individual</td><td>Actualización de lectura eliminar ViewRoles Nota: se revocan todos los derechos de hello si Hola derecho de lectura en elemento Hola se revocará de hello colaborador</td></tr></table>

> [!NOTE]
> **Lectura**, **actualización**, **eliminar**, **ViewRoles** derechos son aplicables tooany elemento (activo o anotación) mientras **TakeOwnership**, **Cambiarpropiedad**, **ChangeVisibility**, **ViewPermissions** son sólo aplicables toohello raíz activo.
> 
> **Eliminar** derecha aplica tooan elemento y los subelementos o elemento único aparecen debajo de él. Por ejemplo, la eliminación de un recurso también eliminará todas las anotaciones de ese recurso.
> 
> 

### <a name="permissions"></a>Permisos
Un permiso es un lista de entradas de control de acceso. Cada entrada de control de acceso asigna el conjunto de entidad de seguridad de tooa de derechos. Permisos solo se pueden especificar en un recurso (es decir, el elemento raíz) y aplican toohello activos y los subelementos.

Durante el saludo **el catálogo de datos** una vista previa, solo **lectura** derecha se admite en hello permisos tooenable escenario toorestrict visibilidad en la lista de un recurso.

De forma predeterminada, cualquier usuario autenticado tiene **lectura** derecho para cualquier elemento de catálogo de Hola a menos que la visibilidad está restringida toohello conjunto de permisos de hello las entidades de.

## <a name="rest-api"></a>API de REST
**COLOCAR** y **POST** solicitudes de elementos de vista pueden ser utilizados toocontrol roles y permisos: en la carga de tooitem de suma, se pueden especificar dos propiedades del sistema **roles** y  **permisos**.

> [!NOTE]
> **permisos** sólo el elemento de raíz tooa aplicables.
> 
> **Propietario** elemento raíz del rol de tooa solo es aplicable.
> 
> De forma predeterminada cuando se crea un elemento en el catálogo de hello su **colaborador** se establece toohello del usuario autenticado actualmente. Si se debe actualizar todos los usuarios, elemento **colaborador** debe establecerse demasiado&lt;todos&gt; entidad de seguridad especial en hello **roles** propiedad cuando elemento publicó por primera vez () Consulte toohello siguiente ejemplo). **Colaborador** no se puede cambiar y Hola permanece igual durante el tiempo de vida de un elemento (incluso **administrador** o **propietario** no tiene Hola toochange derecho Hola  **Colaborador**). Hola sólo valor admitido para el establecimiento explícito de Hola de hello **colaborador** es &lt;todos&gt;: **colaborador** sólo puede ser un usuario que ha creado un elemento o &lt; Todos los usuarios&gt;.
> 
> 

### <a name="examples"></a>Ejemplos
**Establecer colaborador demasiado&lt;todos&gt; al publicar un elemento.**
La entidad de seguridad especial &lt;Todos&gt; tiene el elemento objectId "00000000-0000-0000-0000-000000000201".
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Algunas implementaciones de cliente HTTP pueden automáticamente volver a emitir las solicitudes en tooa de respuesta 302 desde servidor hello, pero normalmente retirar los encabezados de autorización de solicitud de saludo. Puesto que el encabezado de autorización hello es necesario toomake solicitudes tooAzure el catálogo de datos, debe asegurarse de encabezado de autorización de hello todavía está disponible cuando se vuelve a emitir una ubicación de redirección de tooa solicitud especificada por el catálogo de datos. Hello código de ejemplo siguiente muestra mediante el objeto de .NET HttpWebRequest Hola.
> 
> 

**Cuerpo**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Asignar propietarios y restringir la visibilidad de un elemento raíz existente**: **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> En PUT, no requiere una carga de elemento en el cuerpo de Hola toospecify: PUT puede ser usado tooupdate solo roles o permisos.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
