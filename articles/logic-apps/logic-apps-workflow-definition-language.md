---
title: "esquema del lenguaje de definición de aaaWorkflow - Azure Logic Apps | Documentos de Microsoft"
description: "Definir flujos de trabajo basados en el esquema de definición de flujo de trabajo de Hola para las aplicaciones lógicas de Azure"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Esquema del lenguaje de definición de flujo de trabajo - Azure Logic Apps

Una definición de flujo de trabajo contiene lógica real de Hola que se ejecuta como parte de la aplicación lógica. Esta definición incluye uno o más desencadenadores que se inicie la aplicación de la lógica de hello y una o varias acciones para tootake de aplicación lógica de Hola.  
  
## <a name="basic-workflow-definition-structure"></a>Estructura de la definición de flujo de trabajo básica

Esta es la estructura básica de Hola de una definición de flujo de trabajo:  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Hola [API de REST de administración de flujo de trabajo](https://docs.microsoft.com/rest/api/logic/workflows) documentación contiene información acerca de cómo toocreate y administrar flujos de trabajo de aplicación lógica.
  
|Nombre del elemento|Obligatorio|Descripción|  
|------------------|--------------|-----------------|  
|$schema|No|Especifica la ubicación de hello para el archivo de esquema JSON de Hola que describe la versión de Hola del lenguaje de definición de Hola. Esta ubicación es necesaria cuando se hace referencia a una definición externamente. Este documento, la ubicación de hello es: <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|No|Especifica la versión de la definición de Hola. Al implementar un flujo de trabajo mediante la definición de hello, puede usar esta seguro de que se utiliza la definición de derecho de hello toomake de valor.|  
|parameters|No|Especifica parámetros de los datos de tooinput usan en la definición de Hola. Se puede definir un máximo de 50 parámetros.|  
|Desencadenadores|No|Especifica la información de los desencadenadores de Hola que inician el flujo de trabajo de Hola. Se pueden definir 10 desencadenadores como máximo.|  
|actions|No|Especifica las acciones que se realizan mientras se ejecuta el flujo de Hola. Se puede definir un máximo de 250 acciones.|  
|outputs|No|Especifica información sobre recursos de hello implementado. Se puede definir un máximo de 10 salidas.|  
  
## <a name="parameters"></a>parameters

Esta sección especifica todos los parámetros de Hola que se usan en la definición de flujo de trabajo de Hola durante la implementación. Todos los parámetros se deben declarar en esta sección antes de que se puedan utilizar en otras secciones de definición de Hola.  
  
Hello en el ejemplo siguiente se muestra hello estructura de una definición de parámetro:  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Nombre del elemento|Obligatorio|Descripción|  
|------------------|--------------|-----------------|  
|type|Sí|**Tipo**: string <p> **Declaración**: `"parameters": {"parameter1": {"type": "string"}` <p> **Especificación**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tipo**: securestring <p> **Declaración**: `"parameters": {"parameter1": {"type": "securestring"}}` <p> **Especificación**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tipo**: int <p> **Declaración**: `"parameters": {"parameter1": {"type": "int"}}` <p> **Especificación**: `"parameters": {"parameter1": {"value" : 5}}` <p> **Tipo**: bool <p> **Declaración**: `"parameters": {"parameter1": {"type": "bool"}}` <p> **Especificación**: `"parameters": {"parameter1": { "value": true }}` <p> **Tipo**: array <p> **Declaración**: `"parameters": {"parameter1": {"type": "array"}}` <p> **Especificación**: `"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Tipo**: object <p> **Declaración**: `"parameters": {"parameter1": {"type": "object"}}` <p> **Especificación**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Tipo**: secureobject <p> **Declaración**: `"parameters": {"parameter1": {"type": "object"}}` <p> **Especificación**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Nota:** hello `securestring` y `secureobject` tipos no se devuelven en `GET` operaciones. Todas las contraseñas, claves y secretos deben usar este tipo.|  
|defaultValue|No|Especifica el valor predeterminado de hello para el parámetro hello cuando se especifica ningún valor en tiempo de Hola Hola recurso se haya creado.|  
|allowedValues|No|Especifica una matriz de valores permitidos para el parámetro hello.|  
|metadata|No|Especifica información adicional sobre el parámetro hello, por ejemplo, una descripción legible o datos de tiempo de diseño que usa Visual Studio u otras herramientas.|  
  
Este ejemplo muestra cómo puede usar un parámetro en la sección de cuerpo de Hola de una acción:  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 Los parámetros también pueden utilizarse en las salidas.  
  
## <a name="triggers-and-actions"></a>Desencadenadores y acciones  

Desencadenadores y acciones especifican llamadas de Hola que pueden participar en la ejecución de flujo de trabajo. Para más información acerca de esta sección, consulte [Acciones y desencadenadores de flujo de trabajo](logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>Salidas  

Las salidas especifican la información que se puede devolver desde una ejecución de flujo de trabajo. Por ejemplo, si tiene un estado concreto o un valor que quiera tootrack para cada ejecución, puede incluir que los datos de hello ejecutan salidas. datos Hola aparecen en hello API de REST de administración para que se ejecutan y en la administración de hello interfaz de usuario para que se ejecutan en hello portal de Azure. También puede presentarse dichos sistemas externos de salidas tooother como Power BI para crear paneles. Salidas son *no* utiliza toorespond tooincoming solicitudes en hello API de REST de servicio. toorespond tooan solicitud entrante con hello `response` tipo de acción, este es un ejemplo:
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Nombre del elemento|Obligatorio|Descripción|  
|------------------|--------------|-----------------|  
|key1|Sí|Especifica el identificador de clave de hello para la salida de hello. Reemplace **key1** con un nombre que desea que la salida de hello tooidentify toouse.|  
|value|Sí|Especifica el valor de Hola de salida de hello.|  
|type|Sí|Especifica el tipo de hello para el valor de Hola que se especificó. Los tipos de valores posibles son: <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>Expresiones  

Pueden ser literales de valores JSON en la definición de hello, o pueden ser expresiones que se evalúan cuando se utiliza la definición de Hola. Por ejemplo:  
  
```json
"name": "value"
```

 o  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Algunas expresiones obtienen sus valores de acciones en tiempo de ejecución que no puedan existir en el principio de saludo de la ejecución de Hola. Puede usar **funciones** toohelp recuperar algunos de estos valores.  
  
Las expresiones pueden aparecer en cualquier lugar de un valor de cadena JSON y devolver siempre otro valor JSON. Cuando un valor JSON se ha determinado toobe una expresión, se extrae el cuerpo de Hola de expresión de hello quitando hello-arroba (@). Si se necesita una cadena literal que empiece por @, debe convertirse mediante el uso de @@. Hello en los ejemplos siguientes muestran cómo se evalúan las expresiones.  
  
|Valor JSON|Resultado|  
|----------------|------------|  
|"parameters"|se devuelven Hola caracteres 'parameters'.|  
|"parameters[1]"|se devuelven Hola caracteres 'parameters [1]'.|  
|"@@"|Se devuelve una cadena de 1 carácter que contiene "@".|  
|" @"|Se devuelve una cadena de 2 caracteres que contienen " @".|  
  
Con la *interpolación de cadena*, las expresiones también pueden aparecer dentro de cadenas donde las expresiones se ajustan en `@{ ... }`. Por ejemplo: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

resultado de Hello siempre es una cadena, lo que hace esta toohello similar característica `concat` función. Supongamos que ha definido `myNumber` como `42` y `myString` como `sampleString`:  
  
|Valor JSON|Resultado|  
|----------------|------------|  
|"@parameters("myString")"|Devuelve `sampleString` como una cadena.|  
|"@{parameters("myString")}"|Devuelve `sampleString` como una cadena.|  
|"@parameters("myNumber")"|Devuelve `42` como un *número*.|  
|"@{parameters("myNumber")}"|Devuelve `42` como una *cadena*.|  
|"Answer is: @{parameters("myNumber")}"|Devuelve Hola cadena `Answer is: 42`.|  
|"@concat("Answer is: ", string(parameters("myNumber")))"|Devuelve una cadena Hola`Answer is: 42`|  
|"Answer is: @@{parameters("myNumber")}"|Devuelve Hola cadena `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>Operadores  

Los operadores son caracteres de Hola que puede usar en expresiones o funciones. 
  
|operador|Descripción|  
|--------------|-----------------|  
|.|operador de punto de Hello permite tooreference propiedades de un objeto|  
|?|operador de signo de interrogación Hola le permite hacer referencia a propiedades null de un objeto sin indicar un error en tiempo de ejecución. Por ejemplo, puede usar este valor de null de expresión toohandle desencadenar salidas: <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|la comilla simple de Hello es literales de cadena de manera única de hello toowrap. No puede usar comillas dobles dentro de expresiones porque esta puntuación entra en conflicto con la oferta JSON de Hola que contiene la expresión completa de Hola.|  
|[]|Hola corchetes pueden tooget usa un valor de una matriz con un índice específico. Por ejemplo, si tiene una acción que pasa `range(0,10)`en toohello `forEach` función, puede usar esta función tooget productos de matrices:  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Functions  

También puede llamar a funciones dentro de expresiones. Hello tabla siguiente muestran las funciones de Hola que pueden usarse en una expresión.  
  
|Expression|Evaluación|  
|----------------|----------------|  
|"@function("Hello")"|Llamadas Hola a miembro de función de la definición de hello con la cadena literal hello Hello como primer parámetro de Hola.|  
|"@function("It"s Cool!")"|Llama a miembros de función de Hola de definición de hello con la cadena literal hello '' s Cool!' como primer parámetro de Hola|  
|"@function().prop1"|Devuelve Hola valor de propiedad prop1 de Hola de hello `myfunction` miembro de la definición de Hola.|  
|"@function("Hello").prop1"|Llamadas Hola a miembro de función de la definición de hello con la cadena literal hello 'Hello' como Hola primer parámetro y devuelve Hola propiedad prop1 del objeto de Hola.|  
|"@function(parameters("Hello"))"|Se evalúa como parámetro de Hello hello y pasa Hola valor toofunction|  
  
### <a name="referencing-functions"></a>Referencias a funciones  

Puede usar estos resultados de tooreference de funciones de otras acciones de aplicación lógica de Hola o valores que pasa cuando se creó la aplicación de la lógica de hello. Por ejemplo, puede hacer referencia datos Hola desde un paso toouse en otro.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|parameters|Devuelve un valor de parámetro que se define en la definición de Hola. <p>`parameters('password')` <p> **Número de parámetro**: 1 <p> **Nombre**: parámetro <p> **Descripción**: necesaria. nombre de Hello del parámetro hello cuyos valores desea.|  
|action|Permite una expresión tooderive su valor de otro nombre JSON y pares de valor o salida de hello de acción de hello actual en tiempo de ejecución. propiedad Hola representada propertyPath en el siguiente ejemplo de Hola es opcional. Si no se especifica propertyPath, referencia de hello es objeto de acción completa toohello. Esta función solo puede utilizarse dentro de las condiciones do-until de una acción. <p>`action().outputs.body.propertyPath`|  
|actions|Permite una expresión tooderive su valor de otro nombre JSON y pares de valor o la salida de hello de acción de hello en tiempo de ejecución. Estas expresiones declaran explícitamente que una acción depende de otra. propiedad Hola representada propertyPath en el siguiente ejemplo de Hola es opcional. Si no se especifica propertyPath, referencia de hello es objeto de acción completa toohello. Puede utilizar este elemento de cualquiera u Hola condiciones dependencias de toospecify de elemento, pero no es necesario toouse ambos para hello mismo recurso dependiente. <p>`actions('myAction').outputs.body.propertyPath` <p> **Número de parámetro**: 1 <p> **Nombre**: nombre de acción <p> **Descripción**: necesaria. nombre de Hola de acción de hello cuyos valores desea. <p> Las propiedades disponibles en el objeto de acción de hello son: <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Vea hello [API de Rest](http://go.microsoft.com/fwlink/p/?LinkID=850646) para obtener más información sobre las propiedades.|
|trigger|Permite una expresión tooderive su valor de otro nombre JSON y pares de valor o la salida de hello de desencadenador de hello en tiempo de ejecución. propiedad Hola representada propertyPath en el siguiente ejemplo de Hola es opcional. Si no se especifica propertyPath, referencia de hello es objeto de todo desencadenador de toohello. <p>`trigger().outputs.body.propertyPath` <p>Cuando se utiliza dentro de entradas de un desencadenador, función hello devuelve resultados de Hola de ejecución anterior de Hola. Sin embargo, cuando se utiliza dentro de la condición del desencadenador, Hola `trigger` función devuelve resultados de Hola de ejecución actual de Hola. <p> Las propiedades disponibles en el objeto de desencadenador de hello son: <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Vea hello [API de Rest](http://go.microsoft.com/fwlink/p/?LinkID=850644) para obtener más información sobre las propiedades.|
|actionOutputs|Esta función es una abreviatura de `actions('actionName').outputs` <p> **Número de parámetro**: 1 <p> **Nombre**: nombre de acción <p> **Descripción**: necesaria. nombre de Hola de acción de hello cuyos valores desea.|  
|actionBody y body|Estas funciones son una abreviatura de `actions('actionName').outputs.body` <p> **Número de parámetro**: 1 <p> **Nombre**: nombre de acción <p> **Descripción**: necesaria. nombre de Hola de acción de hello cuyos valores desea.|  
|triggerOutputs|Esta función es una abreviatura de `trigger().outputs`|  
|triggerBody|Esta función es una abreviatura de `trigger().outputs.body`|  
|item|Cuando se utiliza dentro de una acción de repetición, esta función devuelve el elemento de matriz de Hola para esta iteración de acción de Hola Hola. Por ejemplo, si tiene una acción que se ejecuta para cada elemento de una matriz de mensajes, puede usar esta sintaxis: <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Funciones de colección  

Estas funciones operan sobre colecciones y generalmente aplicarán tooArrays, cadenas y, a veces diccionarios.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|contains|Devuelve true si el diccionario contiene una clave, la lista contiene un valor o la cadena contiene una subcadena. Por ejemplo, esta función devuelve `true`: <p>`contains('abacaba','aca')` <p> **Número de parámetro**: 1 <p> **Nombre**: dentro de la colección <p> **Descripción**: necesaria. Hola colección toosearch dentro. <p> **Número de parámetro**: 2 <p> **Nombre**: objeto de búsqueda <p> **Descripción**: necesaria. Hola toofind de objeto dentro de hello **dentro de la colección**.|  
|length|Devuelve Hola número de elementos de una matriz o una cadena. Por ejemplo, esta función devuelve `3`:  <p>`length('abc')` <p> **Número de parámetro**: 1 <p> **Nombre**: colección <p> **Descripción**: necesaria. colección de Hello qué tooget Hola hasta alcanzar la longitud.|  
|empty|Devuelve true si el objeto, matriz o cadena están vacíos. Por ejemplo, esta función devuelve `true`: <p>`empty('')` <p> **Número de parámetro**: 1 <p> **Nombre**: colección <p> **Descripción**: necesaria. Hola colección toocheck si está vacía.|  
|intersección|Devuelve una única matriz u objeto que tiene elementos comunes entre las matrices o los objetos en los que se pasan. Por ejemplo, esta función devuelve `[1, 2]`: <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>parámetros de Hello para la función de hello pueden ser un conjunto de objetos o un conjunto de matrices (no una combinación de ambos). Si hay dos objetos con hello mismo nombre, objeto última de hello con ese nombre aparece en el objeto final Hola. <p> **Número de parámetro**: 1 ... *n* <p> **Nombre**: colección *n* <p> **Descripción**: necesaria. Hola tooevaluate de colecciones. Debe ser un objeto en todas las colecciones que se pasa en tooappear en el resultado de hello.|  
|union|Devuelve una matriz único o un objeto con todos los elementos de Hola que se pasan en la matriz o cualquier objeto de función toothis. Por ejemplo, esta función devuelve `[1, 2, 3, 10, 101]`: <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>parámetros de Hello para la función de hello pueden ser un conjunto de objetos o un conjunto de matrices (no una mezcla de dichos productos). Si hay dos objetos con el mismo nombre de hello en el resultado final de hello, último objeto con ese nombre de hello aparece en objeto final Hola. <p> **Número de parámetro**: 1 ... *n* <p> **Nombre**: colección *n* <p> **Descripción**: necesaria. Hola tooevaluate de colecciones. Un objeto que aparece en cualquiera de las colecciones de hello también aparece en el resultado de hello.|  
|first|Devuelve Hola el primer elemento de matriz de Hola o cadena que se pasa. Por ejemplo, esta función devuelve `0`: <p>`first([0,2,3])` <p> **Número de parámetro**: 1 <p> **Nombre**: colección <p> **Descripción**: necesaria. Hola tootake Hola primer objeto de colección.|  
|last|Devuelve Hola último elemento de matriz de Hola o cadena que se pasa. Por ejemplo, esta función devuelve `3`: <p>`last('0123')` <p> **Número de parámetro**: 1 <p> **Nombre**: colección <p> **Descripción**: necesaria. Hola tootake Hola último objeto de colección.|  
|take|Devuelve Hola primero **recuento** pasan los elementos de matriz de Hola o de cadena. Por ejemplo, esta función devuelve `[1, 2]`:  <p>`take([1, 2, 3, 4], 2)` <p> **Número de parámetro**: 1 <p> **Nombre**: colección <p> **Descripción**: necesaria. colección de Hola desde donde tootake Hola primero **recuento** objetos. <p> **Número de parámetro**: 2 <p> **Nombre**: recuento <p> **Descripción**: necesaria. Hola número de objetos tootake de hello **colección**. Debe ser un entero positivo.|  
|skip|Devuelve elementos de matriz de hello empezando por el índice de Hola **recuento**. Por ejemplo, esta función devuelve `[3, 4]`: <p>`skip([1, 2 ,3 ,4], 2)` <p> **Número de parámetro**: 1 <p> **Nombre**: colección <p> **Descripción**: necesaria. Hola Hola de colección tooskip primero **recuento** objetos de. <p> **Número de parámetro**: 2 <p> **Nombre**: recuento <p> **Descripción**: necesaria. Hola número de objetos tooremove desde la parte frontal de Hola de **colección**. Debe ser un entero positivo.|  
|join|Devuelve una cadena con cada elemento de una matriz unido por un delimitador, por ejemplo, devuelve `"1,2,3,4"`:<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: colección<br /><br /> **Descripción**: necesaria. elementos de toojoin de recopilación de Hola de.<br /><br /> **Número de parámetro**: 2<br /><br /> **Nombre**: delimitador<br /><br /> **Descripción**: necesaria. Hola cadena toodelimit los elementos con.|  
  
### <a name="string-functions"></a>Funciones de cadena

Hola siguiendo las funciones solo aplica toostrings. También puede utilizar algunas funciones de colección en las cadenas.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|concat|Combina cualquier número de cadenas. Por ejemplo, si el parámetro 1 es `p1`, esta función devuelve `somevalue-p1-somevalue`: <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Número de parámetro**: 1 ... *n* <p> **Nombre**: cadena *n* <p> **Descripción**: necesaria. Hola toocombine de cadenas en una sola cadena.|  
|substring|Devuelve un subconjunto de caracteres de una cadena. Por ejemplo, esta función devuelve `abc`: <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola desde qué Hola se toma la subcadena. <p> **Número de parámetro**: 2 <p> **Nombre**: índice de inicio <p> **Descripción**: necesaria. índice de Hello de la que comienza la subcadena de hello en el parámetro 1. <p> **Número de parámetro**: 3 <p> **Nombre**: longitud <p> **Descripción**: necesaria. longitud de Hola de hello subcadena.|  
|replace|Reemplaza una cadena con una cadena determinada. Por ejemplo, esta función devuelve `hello new string`: <p>`replace('hello old string', 'old', 'new')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola que se busca el parámetro 2 y se actualizan con el parámetro 3, cuando se encuentra el parámetro 2 en el parámetro 1. <p> **Número de parámetro**: 2 <p> **Nombre**: cadena antigua <p> **Descripción**: necesaria. Hola tooreplace de cadena con el parámetro 3, cuando se encuentra una coincidencia en el parámetro 1 <p> **Número de parámetro**: 3 <p> **Nombre**: cadena nueva <p> **Descripción**: necesaria. Hola cadena que es usado tooreplace Hola cadena en el parámetro 2 cuando se encuentra una coincidencia en el parámetro 1.|  
|GUID|Esta función genera una cadena única global (GUID). Por ejemplo, esta función puede generar este GUID: `c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Número de parámetro**: 1 <p> **Nombre**: formato <p> **Descripción**: opcional. Un especificador de formato único que indica [cómo tooformat Hola valo este Guid](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). parámetro de formato de Hello puede ser "N", "D", "B", "P" o "X". Si no se proporciona el formato, se utiliza "D".|  
|toLower|Convierte una cadena toolowercase. Por ejemplo, esta función devuelve `two by two is four`: <p>`toLower('Two by Two is Four')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. Hola cadena tooconvert toolower entre mayúsculas y minúsculas. Si un carácter de cadena hello no tiene un equivalente en minúsculas, caracteres de Hola se incluye sin modificar en hello devuelve la cadena.|  
|toUpper|Convierte una cadena toouppercase. Por ejemplo, esta función devuelve `TWO BY TWO IS FOUR`: <p>`toUpper('Two by Two is Four')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. Hola cadena tooconvert tooupper entre mayúsculas y minúsculas. Si un carácter de cadena hello no tiene un equivalente en mayúsculas, caracteres de Hola se incluye sin modificar en hello devuelve la cadena.|  
|indexof|Buscar índice Hola de un valor dentro de un caso de cadena y minúsculas. Por ejemplo, esta función devuelve `7`: <p>`indexof('hello, world.', 'world')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola que puede contener el valor de Hola. <p> **Número de parámetro**: 2 <p> **Nombre**: cadena <p> **Descripción**: necesaria. índice de Hello value toosearch Hola de.|  
|lastindexof|Buscar el último índice de un valor dentro de un caso de la cadena de Hola y minúsculas. Por ejemplo, esta función devuelve `3`: <p>`lastindexof('foofoo', 'foo')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola que puede contener el valor de Hola. <p> **Número de parámetro**: 2 <p> **Nombre**: cadena <p> **Descripción**: necesaria. índice de Hello value toosearch Hola de.|  
|startswith|Comprueba si la cadena de hello empieza con un caso de valor y minúsculas. Por ejemplo, esta función devuelve `true`: <p>`startswith('hello, world', 'hello')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola que puede contener el valor de Hola. <p> **Número de parámetro**: 2 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hello valor Hola puede empezar por.|  
|endswith|Comprueba si la cadena de hello termina con un caso de valor y minúsculas. Por ejemplo, esta función devuelve `true`: <p>`endswith('hello, world', 'world')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola que puede contener el valor de Hola. <p> **Número de parámetro**: 2 <p> **Nombre**: cadena <p> **Descripción**: necesaria. Hola valor Hola cadena puede terminar con.|  
|split|Divide la cadena de hello con un separador. Por ejemplo, esta función devuelve `["a", "b", "c"]`: <p>`split('a;b;c',';')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena de Hola que se divide. <p> **Número de parámetro**: 2 <p> **Nombre**: cadena <p> **Descripción**: necesaria. separador de Hola.|  
  
### <a name="logical-functions"></a>Funciones lógicas  

Estas funciones son útiles en las condiciones y pueden ser cualquier tipo de lógica de tooevaluate usado.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|equals|Devuelve true si dos valores son iguales. Por ejemplo, si el parámetro 1 es someValue, esta función devuelve `true`: <p>`equals(parameters('parameter1'), 'someValue')` <p> **Número de parámetro**: 1 <p> **Nombre**: objeto 1 <p> **Descripción**: necesaria. Hola toocompare objeto demasiado**objeto 2**. <p> **Número de parámetro**: 2 <p> **Nombre**: objeto 2 <p> **Descripción**: necesaria. Hola toocompare objeto demasiado**1 objeto**.|  
|less|Devuelve true si el primer argumento de hello es menor que hello en segundo lugar. Tenga en cuenta que solo pueden ser valores de tipo integer, float o string. Por ejemplo, esta función devuelve `true`: <p>`less(10,100)` <p> **Número de parámetro**: 1 <p> **Nombre**: objeto 1 <p> **Descripción**: necesaria. Hola toocheck objeto si es menor que **objeto 2**. <p> **Número de parámetro**: 2 <p> **Nombre**: objeto 2 <p> **Descripción**: necesaria. Hola toocheck objeto si es mayor que **1 objeto**.|  
|lessOrEquals|Devuelve true si el primer argumento de hello es menor que o igual a toohello en segundo lugar. Tenga en cuenta que solo pueden ser valores de tipo integer, float o string. Por ejemplo, esta función devuelve `true`: <p>`lessOrEquals(10,10)` <p> **Número de parámetro**: 1 <p> **Nombre**: objeto 1 <p> **Descripción**: necesaria. Hola toocheck objeto si es menor o igual a demasiado**objeto 2**. <p> **Número de parámetro**: 2 <p> **Nombre**: objeto 2 <p> **Descripción**: necesaria. Hola toocheck objeto si es mayor que o igual a demasiado**1 objeto**.|  
|greater|Devuelve true si el primer argumento de hello es mayor que hello en segundo lugar. Tenga en cuenta que solo pueden ser valores de tipo integer, float o string. Por ejemplo, esta función devuelve `false`:  <p>`greater(10,10)` <p> **Número de parámetro**: 1 <p> **Nombre**: objeto 1 <p> **Descripción**: necesaria. Hola toocheck objeto si es mayor que **objeto 2**. <p> **Número de parámetro**: 2 <p> **Nombre**: objeto 2 <p> **Descripción**: necesaria. Hola toocheck objeto si es menor que **1 objeto**.|  
|greaterOrEquals|Devuelve true si el primer argumento de Hola es igual o mayor que toohello en segundo lugar. Tenga en cuenta que solo pueden ser valores de tipo integer, float o string. Por ejemplo, esta función devuelve `false`: <p>`greaterOrEquals(10,100)` <p> **Número de parámetro**: 1 <p> **Nombre**: objeto 1 <p> **Descripción**: necesaria. Hola toocheck objeto si es mayor que o igual a demasiado**objeto 2**. <p> **Número de parámetro**: 2 <p> **Nombre**: objeto 2 <p> **Descripción**: necesaria. Hola toocheck objeto si es menor o igual demasiado**1 objeto**.|  
|y|Devuelve true si ambos parámetros son true. Ambos argumentos deben toobe booleanos. Por ejemplo, esta función devuelve `false`: <p>`and(greater(1,10),equals(0,0))` <p> **Número de parámetro**: 1 <p> **Nombre**: booleano 1 <p> **Descripción**: necesaria. Hola primer argumento que debe ser `true`. <p> **Número de parámetro**: 2 <p> **Nombre**: booleano 2 <p> **Descripción**: necesaria. Hola segundo argumento debe ser `true`.|  
|o|Devuelve true si alguno de los parámetros es true. Ambos argumentos deben toobe booleanos. Por ejemplo, esta función devuelve `true`: <p>`or(greater(1,10),equals(0,0))` <p> **Número de parámetro**: 1 <p> **Nombre**: booleano 1 <p> **Descripción**: necesaria. Hola primer argumento que puede ser `true`. <p> **Número de parámetro**: 2 <p> **Nombre**: booleano 2 <p> **Descripción**: necesaria. Hola segundo argumento puede ser `true`.|  
|not|Devuelve true si son parámetros de hello `false`. Ambos argumentos deben toobe booleanos. Por ejemplo, esta función devuelve `true`: <p>`not(contains('200 Success','Fail'))` <p> **Número de parámetro**: 1 <p> **Nombre**: booleano <p> **Descripción**: devuelve true si son parámetros de hello `false`. Ambos argumentos deben toobe booleanos. Esta función devuelve `true`: `not(contains('200 Success','Fail'))`|  
|if|Devuelve un valor especificado en función de si generó expresión hello `true` o `false`.  Por ejemplo, esta función devuelve `"yes"`: <p>`if(equals(1, 1), 'yes', 'no')` <p> **Número de parámetro**: 1 <p> **Nombre**: expresión <p> **Descripción**: necesaria. Debe devolver un valor booleano que determina qué expresión Hola de valor. <p> **Número de parámetro**: 2 <p> **Nombre**: true <p> **Descripción**: necesaria. Hola valor tooreturn si expresión de hello es `true`. <p> **Número de parámetro**: 3 <p> **Nombre**: false <p> **Descripción**: necesaria. Hola valor tooreturn si expresión de hello es `false`.|  
  
### <a name="conversion-functions"></a>Funciones de conversión  

Estas funciones son utilizado tooconvert entre cada uno de los tipos nativos en lenguaje de Hola Hola:  
  
- cadena  
  
- integer  
  
- float  
  
- boolean  
  
- arrays  
  
- dictionaries  

-   forms  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|int|Conversión de un entero de hello parámetro tooan. Por ejemplo, esta función devuelve 100 como un número, en lugar de una cadena: <p>`int('100')` <p> **Número de parámetro**: 1 <p> **Nombre**: valor <p> **Descripción**: necesaria. Hola valor entero convertido tooan.|  
|cadena|Convertir la cadena de tooa de parámetros de Hola. Por ejemplo, esta función devuelve `'10'`: <p>`string(10)` <p>También puede convertir una cadena de tooa de objeto. Por ejemplo, si hello `myPar` parámetro es un objeto con una propiedad `abc : xyz`, a continuación, esta función devuelve `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Número de parámetro**: 1 <p> **Nombre**: valor <p> **Descripción**: necesaria. Hola valor de cadena de tooa convertido.|  
|json|Convertir el valor de tipo JSON de hello parámetro tooa y es hello opuesto de `string()`. Por ejemplo, esta función devuelve `[1,2,3]` como una matriz, en lugar de una cadena: <p>`json('[1,2,3]')` <p>Del mismo modo, puede convertir un objeto de cadena tooan. Por ejemplo, esta función devuelve `{ "abc" : "xyz" }`: <p>`json('{"abc" : "xyz"}')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. Hola cadena que es el valor de tipo nativo tooa convertido. <p>Hola `json()` función es compatible con XML de entrada demasiado. Por ejemplo, hello valor del parámetro de: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>es toothis convertir JSON: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|float|Convertir un número de punto flotante de hello parámetro argumento tooa. Por ejemplo, esta función devuelve `10.333`: <p>`float('10.333')` <p> **Número de parámetro**: 1 <p> **Nombre**: valor <p> **Descripción**: necesaria. Hola valor que es el número de punto flotante de tooa convertido.|  
|booleano|Convertir Hola parámetro tooa un valor booleano. Por ejemplo, esta función devuelve `false`: <p>`bool(0)` <p> **Número de parámetro**: 1 <p> **Nombre**: valor <p> **Descripción**: necesaria. Hola valor convertido tooa booleano.|  
|coalesce|Devuelve objeto no null de la primera hello en los argumentos de hello pasada en. **Nota**: Una cadena vacía no es null. Por ejemplo, si no se definen los parámetros 1 y 2, esta función devuelve `fallback`:  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Número de parámetro**: 1 ... *n* <p> **Nombre**: objeto*n* <p> **Descripción**: necesaria. Hola objetos toocheck si hay valores null.|  
|base64|Devuelve Hola representación base64 de la cadena de entrada de Hola. Por ejemplo, esta función devuelve `c29tZSBzdHJpbmc=`: <p>`base64('some string')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena 1 <p> **Descripción**: necesaria. Hola tooencode de cadena en la representación en base 64.|  
|base64ToBinary|Devuelve una representación binaria de una cadena codificada en base64. Por ejemplo, esta función devuelve la representación binaria de Hola de `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena codificada en base64 de Hola.|  
|base64ToString|Devuelve una representación de cadena de una cadena codificada en base64. Por ejemplo, esta función devuelve `some string`: <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. cadena codificada en base64 de Hola.|  
|Binary|Devuelve una representación binaria de un valor.  Por ejemplo, esta función devuelve la representación binaria de `some string`: <p>`binary('some string')` <p> **Número de parámetro**: 1 <p> **Nombre**: valor <p> **Descripción**: necesaria. valor de Hola que es toobinary convertido.|  
|dataUriToBinary|Devuelve una representación binaria de un identificador URI de datos. Por ejemplo, esta función devuelve la representación binaria de Hola de `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. representación en forma de URI tooconvert toobinary de datos de Hola.|  
|dataUriToString|Devuelve una representación de cadena de un identificador URI de datos. Por ejemplo, esta función devuelve `some string`: <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena<p> **Descripción**: necesaria. representación en forma de URI tooconvert tooString de datos de Hola.|  
|dataUri|Devuelve un identificador URI de datos de un valor. Por ejemplo, esta función devuelve este identificador URI de datos`text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`: <p>`dataUri('some string')` <p> **Número de parámetro**: 1<p> **Nombre**: valor<p> **Descripción**: necesaria. Hola valor tooconvert toodata URI.|  
|decodeBase64|Devuelve una representación de cadena de una cadena en base64 de entrada. Por ejemplo, esta función devuelve `some string`: <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: devuelve una representación de cadena de una cadena en base64 de entrada.|  
|encodeUriComponent|Cadena de Hola de escapes de dirección URL que se pasa. Por ejemplo, esta función devuelve `You+Are%3ACool%2FAwesome`: <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. caracteres de tooescape unsafe para la dirección URL de cadena Hola de.|  
|decodeUriComponent|Cadena de hello anular escapes de dirección URL que se pasa. Por ejemplo, esta función devuelve `You Are:Cool/Awesome`: <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. caracteres de Hello cadena toodecode Hola unsafe para la dirección URL de.|  
|decodeDataUri|Devuelve una representación binaria de una cadena de identificador URI de datos de entrada. Por ejemplo, esta función devuelve la representación binaria de Hola de `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena <p> **Descripción**: necesaria. Hola dataURI toodecode en una representación binaria.|  
|uriComponent|Devuelve una representación codificada de un identificador URI de un valor. Por ejemplo, esta función devuelve `You+Are%3ACool%2FAwesome`: <p>`uriComponent('You Are:Cool/Awesome')` <p> **Número de parámetro**: 1<p> **Nombre**: cadena <p> **Descripción**: necesaria. Hola toobe de cadena codificada con un URI.|  
|uriComponentToBinary|Devuelve una representación binaria de una cadena codificada como URI. Por ejemplo, esta función devuelve la representación binaria de `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Número de parámetro**: 1 <p> **Nombre**: cadena<p> **Descripción**: necesaria. cadena codificada en Hello URI.|  
|uriComponentToString|Devuelve una representación de cadena de una cadena codificada como URI. Por ejemplo, esta función devuelve `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Número de parámetro**: 1<p> **Nombre**: cadena<p> **Descripción**: necesaria. cadena codificada en Hello URI.|  
|xml|Devuelve una representación XML del valor de Hola. Por ejemplo, esta función devuelve contenido XML representado por `'\<name>Alan\</name>'`: <p>`xml('\<name>Alan\</name>')` <p>Hola `xml()` función es compatible con objeto JSON de entrada demasiado. Por ejemplo, Hola parámetro `{ "abc": "xyz" }` es tooXML convertir contenido:`\<abc>xyz\</abc>` <p> **Número de parámetro**: 1<p> **Nombre**: valor<p> **Descripción**: necesaria. Hola valor tooconvert tooXML.|  
|xpath|Devuelve una matriz de nodos XML que coinciden con hello expresión de xpath de un valor que se evalúa como expresión de xpath de Hola. <p> **Ejemplo 1** <p>Supongamos que Hola valor del parámetro `p1` es una representación de cadena de este código XML: <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Este código: `xpath(xml(parameters('p1'), '/lab/robot/name')` <p>devuelve <p>`[ <name>R1</name>, <name>R2</name> ]` <p>mientras que este otro: <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>devuelve <p>`13` <p> <p> **Ejemplo 2** <p>Hola determinada siguen contenido XML: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Este código: `@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>o este código: <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>devuelve <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>Y este código: `@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>devuelve <p>``xyz`` <p> **Número de parámetro**: 1 <p> **Nombre**: Xml <p> **Descripción**: necesaria. XML de Hello en qué tooevaluate Hola XPath expresión. <p> **Número de parámetro**: 2 <p> **Nombre**: XPath <p> **Descripción**: necesaria. Hola tooevaluate de expresión de XPath.|  
|array|Convertir Hola parámetro tooan matriz. Por ejemplo, esta función devuelve `["abc"]`: <p>`array('abc')` <p> **Número de parámetro**: 1 <p> **Nombre**: valor <p> **Descripción**: necesaria. valor de Hola que es matriz tooan convertido.|
|createArray|Crea una matriz de parámetros de Hola. Por ejemplo, esta función devuelve `["a", "c"]`: <p>`createArray('a', 'c')` <p> **Número de parámetro**: 1 ... *n* <p> **Nombre**: cualquiera *n* <p> **Descripción**: necesaria. Hola toocombine de valores en una matriz.|
|triggerFormDataValue|Devuelve un valor único con el mismo nombre de clave de Hola de datos del formulario o la salida de desencadenador codificados de formulario.  Si hay varias coincidencias, se producirá un error.  Por ejemplo, se devolverá el siguiente Hola `bar`:`triggerFormDataValue('foo')`<br /><br />**Número de parámetro**: 1<br /><br />**Nombre**: nombre de clave<br /><br />**Descripción**: necesaria. nombre de la clave de Hola de tooreturn de valor de datos de formulario de Hola.|
|triggerFormDataMultiValues|Devuelve una matriz de valores que coinciden con el nombre de clave de Hola de datos del formulario o la salida de desencadenador codificados de formulario.  Por ejemplo, se devolverá el siguiente Hola `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Número de parámetro**: 1<br /><br />**Nombre**: nombre de clave<br /><br />**Descripción**: necesaria. nombre de clave de Hola Hola de datos de formulario valores tooreturn.|
|triggerMultipartBody|Devuelve Hola cuerpo de una parte de una salida de varias partes de desencadenador de Hola.<br /><br />**Número de parámetro**: 1<br /><br />**Nombre**: índice<br /><br />**Descripción**: necesaria. índice de Hola de hello parte tooretrieve.|
|formDataValue|Devuelve un valor único con el mismo nombre de clave de Hola de datos del formulario o de salida de la acción codificados de formulario.  Si hay varias coincidencias, se producirá un error.  Por ejemplo, se devolverá el siguiente Hola `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Número de parámetro**: 1<br /><br />**Nombre**: nombre de acción<br /><br />**Descripción**: necesaria. nombre de Hola de acción de hello con un formulario de datos o respuesta codificada de forma.<br /><br />**Número de parámetro**: 2<br /><br />**Nombre**: nombre de clave<br /><br />**Descripción**: necesaria. nombre de la clave de Hola de tooreturn de valor de datos de formulario de Hola.|
|formDataMultiValues|Devuelve una matriz de valores que coinciden con el nombre de clave de Hola de datos del formulario o de salida de la acción codificados de formulario.  Por ejemplo, se devolverá el siguiente Hola `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Número de parámetro**: 1<br /><br />**Nombre**: nombre de acción<br /><br />**Descripción**: necesaria. nombre de Hola de acción de hello con un formulario de datos o respuesta codificada de forma.<br /><br />**Número de parámetro**: 2<br /><br />**Nombre**: nombre de clave<br /><br />**Descripción**: necesaria. nombre de clave de Hola Hola de datos de formulario valores tooreturn.|
|multipartBody|Devuelve Hola cuerpo de una parte de una salida de varias partes de una acción.<br /><br />**Número de parámetro**: 1<br /><br />**Nombre**: nombre de acción<br /><br />**Descripción**: necesaria. nombre de Hola de acción de hello con una respuesta de varias partes.<br /><br />**Número de parámetro**: 2<br /><br />**Nombre**: índice<br /><br />**Descripción**: necesaria. índice de Hola de hello parte tooretrieve.|

### <a name="math-functions"></a>Funciones matemáticas  

Estas funciones pueden utilizarse para ambos tipos de números: **enteros** y **flotantes**.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|agregar|Devuelve el resultado de hello de sumar dos números de Hola. Por ejemplo, esta función devuelve `20.333`: <p>`add(10,10.333)` <p> **Número de parámetro**: 1 <p> **Nombre**: sumando 1 <p> **Descripción**: necesaria. Hola tooadd número demasiado**sumando 2**. <p> **Número de parámetro**: 2 <p> **Nombre**: sumando 2 <p> **Descripción**: necesaria. Hola tooadd número demasiado**sumando 1**.|  
|sub|Devuelve el resultado de hello de restar dos números. Por ejemplo, esta función devuelve `-0.333`: <p>`sub(10,10.333)` <p> **Número de parámetro**: 1 <p> **Nombre**: minuendo <p> **Descripción**: necesaria. número de Hola que **sustraendo** se quitará. <p> **Número de parámetro**: 2 <p> **Nombre**: sustraendo <p> **Descripción**: necesaria. Hola tooremove número de hello **minuendo**.|  
|mul|Devuelve el resultado de hello de la multiplicación de dos números de Hola. Por ejemplo, esta función devuelve `103.33`: <p>`mul(10,10.333)` <p> **Número de parámetro**: 1 <p> **Nombre**: multiplicando 1 <p> **Descripción**: necesaria. Hola número toomultiply **multiplicando 2** con. <p> **Número de parámetro**: 2 <p> **Nombre**: multiplicando 2 <p> **Descripción**: necesaria. Hola número toomultiply **multiplicando 1** con.|  
|div|Devuelve el resultado de hello de dividir dos números de Hola. Por ejemplo, esta función devuelve `1.0333`: <p>`div(10.333,10)` <p> **Número de parámetro**: 1 <p> **Nombre**: dividendo <p> **Descripción**: necesaria. Hola toodivide número por hello **Divisor**. <p> **Número de parámetro**: 2 <p> **Nombre**: divisor <p> **Descripción**: necesaria. Hola número toodivide Hola **dividendo** por.|  
|mod|Devuelve el resto de hello después de dividir dos números de hello (módulo). Por ejemplo, esta función devuelve `2`: <p>`mod(10,4)` <p> **Número de parámetro**: 1 <p> **Nombre**: dividendo <p> **Descripción**: necesaria. Hola toodivide número por hello **Divisor**. <p> **Número de parámetro**: 2 <p> **Nombre**: divisor <p> **Descripción**: necesaria. Hola número toodivide Hola **dividendo** por. Después de la división de hello, se toma el resto de Hola.|  
|Min|Hay dos patrones diferentes para llamar a esta función. <p>Aquí `min` toma una matriz y devuelve la función hello `0`: <p>`min([0,1,2])` <p>Como alternativa, esta función puede tomar una lista de valores separada por comas y también devuelve `0`: <p>`min(0,1,2)` <p> **Tenga en cuenta**: todos los valores deben ser números, por lo que si el parámetro hello es una matriz, matriz de hello tiene tooonly tienen un número. <p> **Número de parámetro**: 1 <p> **Nombre**: recopilación o valor <p> **Descripción**: necesaria. Una matriz de valor mínimo de valores toofind Hola u Hola primer valor de un conjunto. <p> **Número de parámetro**: 2 ... *n* <p> **Nombre**: valor *n* <p> **Descripción**: opcional. Si el primer parámetro de hello es un valor, a continuación, puede pasar valores adicionales y hello mínimo de todos los valores pasados se devuelve.|  
|max|Hay dos patrones diferentes para llamar a esta función. <p>Aquí `max` toma una matriz y devuelve la función hello `2`: <p>`max([0,1,2])` <p>Como alternativa, esta función puede tomar una lista de valores separada por comas y también devuelve `2`: <p>`max(0,1,2)` <p> **Tenga en cuenta**: todos los valores deben ser números, por lo que si el parámetro hello es una matriz, matriz de hello tiene tooonly tienen un número. <p> **Número de parámetro**: 1 <p> **Nombre**: recopilación o valor <p> **Descripción**: necesaria. Una matriz de valores toofind hello más alto u Hola primer valor de un conjunto. <p> **Número de parámetro**: 2 ... *n* <p> **Nombre**: valor *n* <p> **Descripción**: opcional. Si el primer parámetro de hello es un valor, a continuación, puede pasar valores adicionales y hello máximo de todos los valores pasados se devuelve.|  
|range|Genera una matriz de enteros a partir de un número determinado. Definir la longitud de Hola de hello devuelve la matriz. <p>Por ejemplo, esta función devuelve `[3,4,5,6]`: <p>`range(3,4)` <p> **Número de parámetro**: 1 <p> **Nombre**: índice de inicio <p> **Descripción**: necesaria. primer entero de Hello en la matriz de Hola. <p> **Número de parámetro**: 2 <p> **Nombre**: recuento <p> **Descripción**: necesaria. Este valor es el número de Hola de enteros que se encuentra en la matriz de Hola.|  
|rand|Genera un aleatorio entero dentro de hello especifica el intervalo (inclusivo únicamente en el primer extremo). Por ejemplo, esta función puede devolver `0` o "1": <p>`rand(0,2)` <p> **Número de parámetro**: 1 <p> **Nombre**: mínimo <p> **Descripción**: necesaria. Hola menor número entero que se pueden devolver. <p> **Número de parámetro**: 2 <p> **Nombre**: máximo <p> **Descripción**: necesaria. Este valor es el entero siguiente Hola después entero más alto de Hola que podría devolver.|  
  
### <a name="date-functions"></a>Funciones de fecha  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|utcnow|Devuelve Hola marca de tiempo actual como una cadena, por ejemplo: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Número de parámetro**: 1 <p> **Nombre**: formato <p> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|addseconds|Agrega un número entero de segundos tooa cadena marca de tiempo pasado. número de Hola de segundos puede ser positivo o negativo. De forma predeterminada, el resultado de hello es una cadena en ISO 8601 formato ("o"), a menos que se proporcione un especificador de formato. Por ejemplo: `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Número de parámetro**: 1 <p> **Nombre**: marca de tiempo <p> **Descripción**: necesaria. Una cadena que contiene el tiempo de presentación. <p> **Número de parámetro**: 2 <p> **Nombre**: segundos <p> **Descripción**: necesaria. número de Hola de tooadd segundos. Puede ser negativo toosubtract segundos. <p> **Número de parámetro**: 3 <p> **Nombre**: formato <p> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|addminutes|Agrega un número entero de minutos tooa cadena marca de tiempo pasado. número de Hola de minutos puede ser positivo o negativo. De forma predeterminada, el resultado de hello es una cadena en ISO 8601 formato ("o"), a menos que se proporcione un especificador de formato. Por ejemplo: `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Número de parámetro**: 1 <p> **Nombre**: marca de tiempo <p> **Descripción**: necesaria. Una cadena que contiene el tiempo de presentación. <p> **Número de parámetro**: 2 <p> **Nombre**: minutos <p> **Descripción**: necesaria. número de Hola de tooadd minutos. Puede ser negativo toosubtract minutos. <p> **Número de parámetro**: 3 <p> **Nombre**: formato <p> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|addhours|Agrega un número entero de horas tooa cadena marca de tiempo pasado. número de Hola de horas puede ser positivo o negativo. De forma predeterminada, el resultado de hello es una cadena en ISO 8601 formato ("o"), a menos que se proporcione un especificador de formato. Por ejemplo: `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Número de parámetro**: 1 <p> **Nombre**: marca de tiempo <p> **Descripción**: necesaria. Una cadena que contiene el tiempo de presentación. <p> **Número de parámetro**: 2 <p> **Nombre**: horas <p> **Descripción**: necesaria. número de Hola de tooadd horas. Puede ser negativo toosubtract horas. <p> **Número de parámetro**: 3 <p> **Nombre**: formato <p> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|adddays|Agrega un número entero de días tooa cadena marca de tiempo pasado. número de Hola de días puede ser positivo o negativo. De forma predeterminada, el resultado de hello es una cadena en ISO 8601 formato ("o"), a menos que se proporcione un especificador de formato. Por ejemplo: `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Número de parámetro**: 1 <p> **Nombre**: marca de tiempo <p> **Descripción**: necesaria. Una cadena que contiene el tiempo de presentación. <p> **Número de parámetro**: 2 <p> **Nombre**: días <p> **Descripción**: necesaria. número de Hola de tooadd días. Puede ser negativo toosubtract días. <p> **Número de parámetro**: 3 <p> **Nombre**: formato <p> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|formatDateTime|Devuelve una cadena en formato de fecha. De forma predeterminada, el resultado de hello es una cadena en ISO 8601 formato ("o"), a menos que se proporcione un especificador de formato. Por ejemplo: `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Número de parámetro**: 1 <p> **Nombre**: fecha <p> **Descripción**: necesaria. Una cadena que contiene la fecha de Hola. <p> **Número de parámetro**: 2 <p> **Nombre**: formato <p> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|startOfHour|Hola devuelve iniciar de hello hora tooa cadena marca de tiempo pasado. Por ejemplo: `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.<br /><br />**Número de parámetro**: 2<br /><br /> **Nombre**: formato<br /><br /> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").|  
|startOfDay|Hola devuelve iniciar de hello día tooa cadena marca de tiempo pasado. Por ejemplo: `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.<br /><br />**Número de parámetro**: 2<br /><br /> **Nombre**: formato<br /><br /> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").| 
|startOfMonth|Hola devuelve iniciar de hello mes tooa cadena marca de tiempo pasado. Por ejemplo: `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.<br /><br />**Número de parámetro**: 2<br /><br /> **Nombre**: formato<br /><br /> **Descripción**: opcional. Ya sea un [único carácter especificador de formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o un [modelo de formato personalizado](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) que indica cómo tooformat Hola valor de esta marca de tiempo. Si no se proporciona el formato, se utiliza el formato ISO 8601 hello ("o").| 
|dayOfWeek|Devuelve Hola día del componente de la semana de una marca de tiempo de la cadena.  El valor del domingo es 0, el del lunes es 1 y así sucesivamente. Por ejemplo: `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.| 
|dayOfMonth|Devuelve Hola día del componente de mes de una marca de tiempo de la cadena. Por ejemplo: `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.| 
|dayOfYear|Devuelve Hola día del componente de año de una marca de tiempo de la cadena. Por ejemplo: `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.| 
|ticks|Hola devuelve tics propiedad de una marca de tiempo de la cadena. Por ejemplo: `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Número de parámetro**: 1<br /><br /> **Nombre**: marca de tiempo<br /><br /> **Descripción**: necesaria. Se trata de una cadena que contiene el tiempo de presentación.| 
  
### <a name="workflow-functions"></a>Funciones de flujo de trabajo  

Estas funciones le ayudará a obtener información acerca de hello propio flujo de trabajo en tiempo de ejecución.  
  
|Nombre de función|Descripción|  
|-------------------|-----------------|  
|listCallbackUrl|Devuelve una acción o un desencadenador de cadena toocall tooinvoke Hola. <p> **Nota**: Esta función solo puede utilizarse en **httpWebhook** y **apiConnectionWebhook**, no en **manual**, **recurrence**, **http** o **apiConnection**. <p>Por ejemplo, hello `listCallbackUrl()` función devuelve: <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|flujo de trabajo|Esta función proporciona todos los detalles de Hola para hello propio flujo de trabajo en tiempo de ejecución de Hola. <p> Las propiedades disponibles en el objeto de flujo de trabajo de hello son: <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> Hola valo hello `run` propiedad es un objeto con las siguientes propiedades: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Vea hello [API de Rest](http://go.microsoft.com/fwlink/p/?LinkID=525617) para obtener más información sobre las propiedades.<p> Por ejemplo, tooget Hola nombre de hello actual ejecutar, use hello `"@workflow().run.name"` expresión. |

## <a name="next-steps"></a>Pasos siguientes

[Acciones y desencadenadores de flujo de trabajo](logic-apps-workflow-actions-triggers.md)
