---
title: aaaResource funciones de plantilla de administrador | Documentos de Microsoft
description: "Describe Hola funciones toouse una valores tooretrieve de plantilla de Azure Resource Manager, trabajar con cadenas y valores numéricos y recuperar la información de implementación."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a>Funciones de la plantilla del Administrador de recursos de Azure
En este tema se describe todas las funciones de Hola que puede usar en una plantilla de Azure Resource Manager.

Las funciones se agregan a las plantillas al encerrarlas entre corchetes: `[` y `]`, respectivamente. Hola expresión se evalúa durante la implementación. Mientras se escribe como un literal de cadena, el resultado de hello de la evaluación de expresión de hello puede ser de un tipo diferente de JSON, como una matriz, un objeto o un entero. Al igual que en JavaScript, las llamadas de función tienen el formato `functionName(arg1,arg2,arg3)`. Hacer referencia a propiedades mediante operadores de hello [índice] y de puntos.

Las expresiones de plantilla no pueden superar los 24 576 caracteres.

Las funciones de plantilla y sus parámetros no distinguen mayúsculas de minúsculas. Por ejemplo, el Administrador de recursos resuelve **variables('var1')** y **VARIABLES('VAR1')** como Hola igual. Cuando se evalúa, a menos que la función hello expresamente modifica caso (por ejemplo, toUpper o toLower), la función hello conserva caso Hola. Es posible que determinados tipos de recursos tengan requisitos de mayúsculas independientemente de cómo se evalúen las funciones.

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a>Funciones de matriz y objeto
Resource Manager ofrece varias funciones para trabajar con matrices y objetos.

* [matriz](resource-group-template-functions-array.md#array)
* [coalesce](resource-group-template-functions-array.md#coalesce)
* [concat](resource-group-template-functions-array.md#concat)
* [contains](resource-group-template-functions-array.md#contains)
* [createArray](resource-group-template-functions-array.md#createarray)
* [empty](resource-group-template-functions-array.md#empty)
* [first](resource-group-template-functions-array.md#first)
* [intersection](resource-group-template-functions-array.md#intersection)
* [json](resource-group-template-functions-array.md#json)
* [last](resource-group-template-functions-array.md#last)
* [length](resource-group-template-functions-array.md#length)
* [min](resource-group-template-functions-array.md#min)
* [max](resource-group-template-functions-array.md#max)
* [range](resource-group-template-functions-array.md#range)
* [skip](resource-group-template-functions-array.md#skip)
* [take](resource-group-template-functions-array.md#take)
* [union](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a>Funciones de comparación
Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.

* [equals](resource-group-template-functions-comparison.md#equals)
* [less](resource-group-template-functions-comparison.md#less)
* [lessOrEquals](resource-group-template-functions-comparison.md#lessorequals)
* [greater](resource-group-template-functions-comparison.md#greater)
* [greaterOrEquals](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a>Funciones con valores de implementación
Administrador de recursos proporciona siguiente hello las funciones para obtener los valores de las secciones de plantilla de Hola y los valores relacionados toohello implementación:

* [deployment](resource-group-template-functions-deployment.md#deployment)
* [parameters](resource-group-template-functions-deployment.md#parameters)
* [variables](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a>Funciones lógicas
Administrador de recursos proporciona Hola siguientes funciones para trabajar con condiciones lógicas:

* [and](resource-group-template-functions-logical.md#and)
* [bool](resource-group-template-functions-logical.md#bool)
* [if](resource-group-template-functions-logical.md#if)
* [not](resource-group-template-functions-logical.md#not)
* [or](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a>Funciones numéricas
Administrador de recursos proporciona Hola siguientes funciones para trabajar con números enteros:

* [agregar](resource-group-template-functions-numeric.md#add)
* [copyIndex](resource-group-template-functions-numeric.md#copyindex)
* [div](resource-group-template-functions-numeric.md#div)
* [float](resource-group-template-functions-numeric.md#float)
* [int](resource-group-template-functions-numeric.md#int)
* [min](resource-group-template-functions-numeric.md#min)
* [max](resource-group-template-functions-numeric.md#max)
* [mod](resource-group-template-functions-numeric.md#mod)
* [mul](resource-group-template-functions-numeric.md#mul)
* [sub](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a>Funciones de recursos
Administrador de recursos proporciona Hola siguientes funciones para obtener valores de recurso:

* [listKeys y list{Value}](resource-group-template-functions-resource.md#listkeys)
* [providers](resource-group-template-functions-resource.md#providers)
* [reference](resource-group-template-functions-resource.md#reference)
* [resourceGroup](resource-group-template-functions-resource.md#resourcegroup)
* [resourceId](resource-group-template-functions-resource.md#resourceid)
* [suscripción](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a>Funciones de cadena
Administrador de recursos proporciona Hola siguientes funciones para trabajar con cadenas:

* [base64](resource-group-template-functions-string.md#base64)
* [base64ToJson](resource-group-template-functions-string.md#base64tojson)
* [base64ToString](resource-group-template-functions-string.md#base64tostring)
* [concat](resource-group-template-functions-string.md#concat)
* [contains](resource-group-template-functions-string.md#contains)
* [dataUri](resource-group-template-functions-string.md#datauri)
* [dataUriToString](resource-group-template-functions-string.md#datauritostring)
* [empty](resource-group-template-functions-string.md#empty)
* [endsWith](resource-group-template-functions-string.md#endswith)
* [first](resource-group-template-functions-string.md#first)
* [indexOf](resource-group-template-functions-string.md#indexof)
* [last](resource-group-template-functions-string.md#last)
* [lastIndexOf](resource-group-template-functions-string.md#lastindexof)
* [length](resource-group-template-functions-string.md#length)
* [padLeft](resource-group-template-functions-string.md#padleft)
* [replace](resource-group-template-functions-string.md#replace)
* [skip](resource-group-template-functions-string.md#skip)
* [split](resource-group-template-functions-string.md#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [cadena](resource-group-template-functions-string.md#string)
* [substring](resource-group-template-functions-string.md#substring)
* [take](resource-group-template-functions-string.md#take)
* [toLower](resource-group-template-functions-string.md#tolower)
* [toUpper](resource-group-template-functions-string.md#toupper)
* [trim](resource-group-template-functions-string.md#trim)
* [uniqueString](resource-group-template-functions-string.md#uniquestring)
* [uri](resource-group-template-functions-string.md#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md)
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md)
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md)
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla del Administrador de recursos de Azure](resource-group-template-deploy.md)

