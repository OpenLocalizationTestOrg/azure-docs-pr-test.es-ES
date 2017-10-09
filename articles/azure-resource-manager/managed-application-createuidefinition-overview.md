---
title: "aaaUnderstand Crear definición de interfaz de usuario para las aplicaciones administradas de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate las definiciones de interfaz de usuario para las aplicaciones administradas de Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Introducción a CreateUiDefinition
Este documento presentan conceptos básicos de Hola de un CreateUiDefinition, que se utiliza la interfaz de usuario de Hola Hola toogenerate portal Azure para crear una aplicación administrada.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition siempre contiene tres propiedades: 

* handler
* versión
* parameters

Para las aplicaciones administradas, siempre debería ser el controlador `Microsoft.Compute.MultiVm`, y la versión de Hola compatible más reciente es `0.1.2-preview`.

esquema de Hola de propiedad de los parámetros de hello depende de la combinación de hello del controlador especificado de Hola y la versión. Para las aplicaciones administradas, son propiedades de hello admitida `basics`, `steps`, y `outputs`. propiedades conceptos básicos y pasos Hello contienen hello _elementos_ , como cuadros de texto y listas desplegables - toobe muestra de Hola portal de Azure. salidas de Hello propiedad es toomap usa valores de salida de hello de Hola elementos especificados toohello parámetros de plantilla de implementación de hello Azure Resource Manager.

Se recomienda incluir `$schema`, aunque es opcional. Si se especifica, Hola valor para `version` debe coincidir con la versión de Hola Hola `$schema` URI.

## <a name="basics"></a>Aspectos básicos
paso de conceptos básicos de Hello siempre es Hola primer paso para genera al portal de Azure Hola analiza un CreateUiDefinition con un asistente Hola. Además se especifican los elementos de Hola de toodisplaying en `basics`, portal de hello inserta elementos de suscripción de los usuarios toochoose hello, grupo de recursos y ubicación para la implementación de Hola. Por lo general, los elementos que consultan los parámetros de toda la implementación, tal como el nombre de un clúster o el Administrador de credenciales, Hola deberían ir en este paso.

Si el comportamiento de un elemento depende de la suscripción del usuario de hello, el grupo de recursos o la ubicación, ese elemento no puede utilizarse en aspectos básicos. Por ejemplo, **Microsoft.Compute.SizeSelector** depende suscripción y ubicación toodetermine Hola lista del usuario de hello de los tamaños disponibles. Por lo tanto, **Microsoft.Compute.SizeSelector** solo puede utilizarse en steps. Por lo general, solo elementos de hello **Microsoft.Common** espacio de nombres puede usarse en aspectos básicos. Aunque algunos elementos en otros espacios de nombres (como **Microsoft.Compute.Credentials**) que no dependen de contexto del usuario de hello, todavía se permiten.

## <a name="steps"></a>Pasos
propiedad de pasos de Hello puede contener cero o más toodisplay pasos adicionales después de conceptos básicos, cada uno de los cuales contiene uno o más elementos. Considere la posibilidad de agregar pasos por rol o de la capa de aplicación Hola va a implementar. Por ejemplo, agregue un paso de las entradas para los nodos maestros de Hola y un paso para nodos de trabajador de hello en un clúster.

## <a name="outputs"></a>Salidas
portal de Azure Hello usa hello `outputs` elementos de propiedad toomap de `basics` y `steps` toohello parámetros de plantilla de implementación de hello Azure Resource Manager. claves de Hola de este diccionario son nombres de Hola Hola de parámetros de plantilla y valores de hello son propiedades de los objetos de salida de hello de los elementos de hello al que hace referencia.

## <a name="functions"></a>Functions
Similar demasiado[funciones de plantilla](resource-group-template-functions.md) en Azure Resource Manager (tanto en la sintaxis y las funciones), CreateUiDefinition proporciona funciones para trabajar con elementos entradas y salidas, así como características, como instrucciones condicionales.

## <a name="next-steps"></a>Pasos siguientes
El esquema de CreateUiDefinition en sí es simple. profundidad real de Hola de procede de todas las funciones, qué Hola siguientes documentos se describen en detalle maravillosa y elementos de hello admitida:

- [Elementos](managed-application-createuidefinition-elements.md)
- [Funciones](managed-application-createuidefinition-functions.md)

Hay disponible un esquema JSON actual para CreateUiDefinition aquí: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Las versiones posteriores estarán disponibles en hello misma ubicación. Reemplace hello `0.1.2-preview` parte de la dirección URL de Hola y Hola `version` valor con el identificador de la versión de Hola piensa toouse. los identificadores de versión de Hola compatibles actualmente son `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, y `0.1.2-preview`.
