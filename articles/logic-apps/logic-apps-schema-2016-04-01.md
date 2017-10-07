---
title: aaaSchema actualiza junio-1-2016 - Azure Logic Apps | Documentos de Microsoft
description: "Creación de definiciones de JSON para Azure Logic Apps con la versión de esquema del 1 de junio de 2016"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Actualizaciones de esquema para Azure Logic Apps, 1 de junio de 2016

Este nuevo esquema y la API de la versión para las aplicaciones lógicas de Azure incluye mejoras claves que hacen que las aplicaciones lógicas más toouse más fácil y confiable:

* [Ámbitos](#scopes): le permiten agrupar o anidar acciones como una colección de acciones.
* [Condiciones y bucles](#conditions-loops): ahora son acciones de primera clase.
* Ordenación más precisa para ejecutar acciones con hello `runAfter` propiedad, reemplazar`dependsOn`

tooupgrade las aplicaciones lógicas de Hola 1 de agosto de 2015, obtenga una vista previa toohello 1 de junio de 2016 de esquema [desproteger la sección actualización de hello](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Ámbitos

Este esquema incluye ámbitos, que le permiten agrupar acciones o anidar acciones unas dentro de otras. Por ejemplo, una condición puede contener otra condición. Aprenda más sobre la [sintaxis de los ámbitos](../logic-apps/logic-apps-loops-and-scopes.md), o revise este ejemplo básico de ámbitos:

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a>Cambios de condiciones y bucles

En las versiones anteriores del esquema, las condiciones y los bucles eran parámetros asociados a una sola acción. Este esquema elimina esta limitación, por lo que las condiciones y los bucles aparecen ahora como tipos de acción. Aprenda más sobre [bucles y ámbitos](../logic-apps/logic-apps-loops-and-scopes.md), o revise este ejemplo básico de una acción de condición:

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a>Propiedad "runAfter"

Hola `runAfter` propiedad reemplaza `dependsOn`, lo que proporciona mayor precisión cuando se especifica el orden de hello ejecutar acciones de acuerdo con el estado de Hola de acciones anteriores.

Hola `dependsOn` propiedad era sinónimo de "acción de Hola se ejecutó y se realizó correctamente", independientemente de cuántas veces desea tooexecute una acción, en función de si la acción anterior Hola fue correcta, no se pudo o se omite. Hola `runAfter` propiedad proporciona la flexibilidad como un objeto que especifica todos Hola transcurrido el cual hello objeto ejecuta los nombres de acción. Esta propiedad también define una matriz de estados que son aceptables como desencadenadores. Por ejemplo, si deseara toorun después de un paso se realiza correctamente y también después paso B se realiza correctamente o se produce un error, crear esto `runAfter` propiedad:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Actualización del esquema

Actualizar toohello nuevo esquema solo tiene unos pocos pasos. Hello proceso de actualización incluye ejecutar script de actualización de hello, guardar como una nueva aplicación de lógica y, si lo desea, posiblemente sobrescribiendo la aplicación de lógica de hello anterior.

1. Hola portal de Azure, abra la aplicación lógica.

2. Vaya demasiado**Introducción**. En la barra de herramientas de aplicación de lógica de hello, elija **actualizar esquema**.
   
    ![Selección del esquema de actualización][1]
   
    Hello definición actualizada se devuelve, que puede copiar y pegar en una definición de recursos si es necesario. 
    Sin embargo, se **recomienda** elige **Guardar como** toomake seguro de que todas las referencias de conexión son válidas en hello actualiza la aplicación lógica.

3. En la barra de herramientas de actualización de hoja de hello, elija **Guardar como**.

4. Escriba el nombre de la lógica de Hola y el estado. toodeploy la aplicación lógica actualizado, elija **crear**.

5. Confirme que la aplicación lógica actualizada funciona según lo previsto.
   
   > [!NOTE]
   > Si usas un desencadenador manual o de solicitud, dirección URL de devolución de llamada de hello cambia en la nueva aplicación de lógica. Experiencia de prueba Hola nueva dirección URL toomake seguro hello-to-end. toopreserve URL anterior, puede clonar a través de la aplicación lógica existente.

6. *Opcional* toooverwrite la aplicación lógica anterior con la versión de esquema nuevo hello, en la barra de herramientas de hello, elija **clon**, al lado de demasiado**actualizar esquema**. Este paso es necesario únicamente si desea tookeep Hola mismo recurso Id. de solicitud de desencadenador dirección URL o de la aplicación lógica.

### <a name="upgrade-tool-notes"></a>Notas de la herramienta de actualización

#### <a name="mapping-conditions"></a>Condiciones de asignación

En la definición de hello actualizado, herramienta de hello realiza un mayor esfuerzo en Agrupar acciones de bifurcación true y false como un ámbito. En concreto, patrón diseñador Hola de `@equals(actions('a').status, 'Skipped')` debería aparecer como un `else` acción. Sin embargo, si herramienta Hola detecta patrones irreconocibles, herramienta de hello podría crear condiciones individuales para true hello y rama false Hola. Si es necesario, puede volver a asignar acciones después de la actualización.

#### <a name="foreach-loop-with-condition"></a>Bucle "foreach" con condición

En el nuevo esquema de hello, puede usar patrón hello tooreplicate de acción de filtro de Hola de un `foreach` bucle con una condición por cada elemento, pero este cambio debe ocurrir automáticamente cuando se actualiza. condición de Hola se convierte en una acción de filtrado antes de un bucle foreach Hola para devolver solo una matriz de elementos que coinciden con la condición de Hola y esa matriz se pasa a la acción de foreach Hola. Para ver un ejemplo, consulte [Bucles y ámbitos](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Etiquetas del recurso

Después de actualizar, se quitan las etiquetas del recurso, por lo que debe restablecer de flujo de trabajo de hello actualizado.

## <a name="other-changes"></a>Otros cambios

### <a name="renamed-manual-trigger-toorequest-trigger"></a>Cambiar el nombre de desencadenador 'manual' too'request' desencadenador

Hola `manual` tipo de desencadenador se ha desusado y se cambia el nombre demasiado`request` con tipo `http`. Este cambio crea más coherencia de tipo hello del patrón de Hola desencadenador es toobuild usado.

### <a name="new-filter-action"></a>Nueva acción 'filtro'

una matriz grande hacia abajo tooa conjunto más pequeño de elementos, new hello toofilter `filter` tipo acepta una matriz y una condición, se evalúa como condición de Hola para cada elemento y devuelve una matriz con los elementos que cumplen la condición de Hola.

### <a name="restrictions-for-foreach-and-until-actions"></a>Restricciones de las acciones "foreach" y "until"

Hola `foreach` y `until` bucle están restringidos tooa única acción.

### <a name="new-trackedproperties-for-actions"></a>Nueva propiedad "trackedProperties" para las acciones

Acciones ahora pueden tener una propiedad adicional denominada `trackedProperties`, que es el mismo nivel toohello `runAfter` y `type` propiedades. Este objeto especifica algunas entradas de acción o salidas que desea tooinclude de telemetría de diagnóstico de Azure hello, genera como parte de un flujo de trabajo. Por ejemplo:

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
* [Creación de definiciones de flujo de trabajo para aplicaciones lógicas](../logic-apps/logic-apps-author-definitions.md)
* [Creación de plantillas de implementación de aplicaciones lógicas](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
