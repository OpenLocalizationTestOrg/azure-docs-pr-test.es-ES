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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="66af3-103">Actualizaciones de esquema para Azure Logic Apps, 1 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="66af3-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="66af3-104">Este nuevo esquema y la API de la versión para las aplicaciones lógicas de Azure incluye mejoras claves que hacen que las aplicaciones lógicas más toouse más fácil y confiable:</span><span class="sxs-lookup"><span data-stu-id="66af3-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="66af3-105">[Ámbitos](#scopes): le permiten agrupar o anidar acciones como una colección de acciones.</span><span class="sxs-lookup"><span data-stu-id="66af3-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="66af3-106">[Condiciones y bucles](#conditions-loops): ahora son acciones de primera clase.</span><span class="sxs-lookup"><span data-stu-id="66af3-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="66af3-107">Ordenación más precisa para ejecutar acciones con hello `runAfter` propiedad, reemplazar`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="66af3-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="66af3-108">tooupgrade las aplicaciones lógicas de Hola 1 de agosto de 2015, obtenga una vista previa toohello 1 de junio de 2016 de esquema [desproteger la sección actualización de hello](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="66af3-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="66af3-109">Ámbitos</span><span class="sxs-lookup"><span data-stu-id="66af3-109">Scopes</span></span>

<span data-ttu-id="66af3-110">Este esquema incluye ámbitos, que le permiten agrupar acciones o anidar acciones unas dentro de otras.</span><span class="sxs-lookup"><span data-stu-id="66af3-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="66af3-111">Por ejemplo, una condición puede contener otra condición.</span><span class="sxs-lookup"><span data-stu-id="66af3-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="66af3-112">Aprenda más sobre la [sintaxis de los ámbitos](../logic-apps/logic-apps-loops-and-scopes.md), o revise este ejemplo básico de ámbitos:</span><span class="sxs-lookup"><span data-stu-id="66af3-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

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
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="66af3-113">Cambios de condiciones y bucles</span><span class="sxs-lookup"><span data-stu-id="66af3-113">Conditions and loops changes</span></span>

<span data-ttu-id="66af3-114">En las versiones anteriores del esquema, las condiciones y los bucles eran parámetros asociados a una sola acción.</span><span class="sxs-lookup"><span data-stu-id="66af3-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="66af3-115">Este esquema elimina esta limitación, por lo que las condiciones y los bucles aparecen ahora como tipos de acción.</span><span class="sxs-lookup"><span data-stu-id="66af3-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="66af3-116">Aprenda más sobre [bucles y ámbitos](../logic-apps/logic-apps-loops-and-scopes.md), o revise este ejemplo básico de una acción de condición:</span><span class="sxs-lookup"><span data-stu-id="66af3-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

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
## <a name="runafter-property"></a><span data-ttu-id="66af3-117">Propiedad "runAfter"</span><span class="sxs-lookup"><span data-stu-id="66af3-117">'runAfter' property</span></span>

<span data-ttu-id="66af3-118">Hola `runAfter` propiedad reemplaza `dependsOn`, lo que proporciona mayor precisión cuando se especifica el orden de hello ejecutar acciones de acuerdo con el estado de Hola de acciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="66af3-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="66af3-119">Hola `dependsOn` propiedad era sinónimo de "acción de Hola se ejecutó y se realizó correctamente", independientemente de cuántas veces desea tooexecute una acción, en función de si la acción anterior Hola fue correcta, no se pudo o se omite.</span><span class="sxs-lookup"><span data-stu-id="66af3-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="66af3-120">Hola `runAfter` propiedad proporciona la flexibilidad como un objeto que especifica todos Hola transcurrido el cual hello objeto ejecuta los nombres de acción.</span><span class="sxs-lookup"><span data-stu-id="66af3-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="66af3-121">Esta propiedad también define una matriz de estados que son aceptables como desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="66af3-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="66af3-122">Por ejemplo, si deseara toorun después de un paso se realiza correctamente y también después paso B se realiza correctamente o se produce un error, crear esto `runAfter` propiedad:</span><span class="sxs-lookup"><span data-stu-id="66af3-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="66af3-123">Actualización del esquema</span><span class="sxs-lookup"><span data-stu-id="66af3-123">Upgrade your schema</span></span>

<span data-ttu-id="66af3-124">Actualizar toohello nuevo esquema solo tiene unos pocos pasos.</span><span class="sxs-lookup"><span data-stu-id="66af3-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="66af3-125">Hello proceso de actualización incluye ejecutar script de actualización de hello, guardar como una nueva aplicación de lógica y, si lo desea, posiblemente sobrescribiendo la aplicación de lógica de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="66af3-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="66af3-126">Hola portal de Azure, abra la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66af3-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="66af3-127">Vaya demasiado**Introducción**.</span><span class="sxs-lookup"><span data-stu-id="66af3-127">Go too**Overview**.</span></span> <span data-ttu-id="66af3-128">En la barra de herramientas de aplicación de lógica de hello, elija **actualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="66af3-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Selección del esquema de actualización][1]
   
    <span data-ttu-id="66af3-130">Hello definición actualizada se devuelve, que puede copiar y pegar en una definición de recursos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="66af3-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="66af3-131">Sin embargo, se **recomienda** elige **Guardar como** toomake seguro de que todas las referencias de conexión son válidas en hello actualiza la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66af3-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="66af3-132">En la barra de herramientas de actualización de hoja de hello, elija **Guardar como**.</span><span class="sxs-lookup"><span data-stu-id="66af3-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="66af3-133">Escriba el nombre de la lógica de Hola y el estado.</span><span class="sxs-lookup"><span data-stu-id="66af3-133">Enter hello logic name and status.</span></span> <span data-ttu-id="66af3-134">toodeploy la aplicación lógica actualizado, elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="66af3-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="66af3-135">Confirme que la aplicación lógica actualizada funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="66af3-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="66af3-136">Si usas un desencadenador manual o de solicitud, dirección URL de devolución de llamada de hello cambia en la nueva aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="66af3-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="66af3-137">Experiencia de prueba Hola nueva dirección URL toomake seguro hello-to-end.</span><span class="sxs-lookup"><span data-stu-id="66af3-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="66af3-138">toopreserve URL anterior, puede clonar a través de la aplicación lógica existente.</span><span class="sxs-lookup"><span data-stu-id="66af3-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="66af3-139">*Opcional* toooverwrite la aplicación lógica anterior con la versión de esquema nuevo hello, en la barra de herramientas de hello, elija **clon**, al lado de demasiado**actualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="66af3-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="66af3-140">Este paso es necesario únicamente si desea tookeep Hola mismo recurso Id. de solicitud de desencadenador dirección URL o de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="66af3-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="66af3-141">Notas de la herramienta de actualización</span><span class="sxs-lookup"><span data-stu-id="66af3-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="66af3-142">Condiciones de asignación</span><span class="sxs-lookup"><span data-stu-id="66af3-142">Mapping conditions</span></span>

<span data-ttu-id="66af3-143">En la definición de hello actualizado, herramienta de hello realiza un mayor esfuerzo en Agrupar acciones de bifurcación true y false como un ámbito.</span><span class="sxs-lookup"><span data-stu-id="66af3-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="66af3-144">En concreto, patrón diseñador Hola de `@equals(actions('a').status, 'Skipped')` debería aparecer como un `else` acción.</span><span class="sxs-lookup"><span data-stu-id="66af3-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="66af3-145">Sin embargo, si herramienta Hola detecta patrones irreconocibles, herramienta de hello podría crear condiciones individuales para true hello y rama false Hola.</span><span class="sxs-lookup"><span data-stu-id="66af3-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="66af3-146">Si es necesario, puede volver a asignar acciones después de la actualización.</span><span class="sxs-lookup"><span data-stu-id="66af3-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="66af3-147">Bucle "foreach" con condición</span><span class="sxs-lookup"><span data-stu-id="66af3-147">'foreach' loop with condition</span></span>

<span data-ttu-id="66af3-148">En el nuevo esquema de hello, puede usar patrón hello tooreplicate de acción de filtro de Hola de un `foreach` bucle con una condición por cada elemento, pero este cambio debe ocurrir automáticamente cuando se actualiza.</span><span class="sxs-lookup"><span data-stu-id="66af3-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="66af3-149">condición de Hola se convierte en una acción de filtrado antes de un bucle foreach Hola para devolver solo una matriz de elementos que coinciden con la condición de Hola y esa matriz se pasa a la acción de foreach Hola.</span><span class="sxs-lookup"><span data-stu-id="66af3-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="66af3-150">Para ver un ejemplo, consulte [Bucles y ámbitos](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="66af3-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="66af3-151">Etiquetas del recurso</span><span class="sxs-lookup"><span data-stu-id="66af3-151">Resource tags</span></span>

<span data-ttu-id="66af3-152">Después de actualizar, se quitan las etiquetas del recurso, por lo que debe restablecer de flujo de trabajo de hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="66af3-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="66af3-153">Otros cambios</span><span class="sxs-lookup"><span data-stu-id="66af3-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="66af3-154">Cambiar el nombre de desencadenador 'manual' too'request' desencadenador</span><span class="sxs-lookup"><span data-stu-id="66af3-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="66af3-155">Hola `manual` tipo de desencadenador se ha desusado y se cambia el nombre demasiado`request` con tipo `http`.</span><span class="sxs-lookup"><span data-stu-id="66af3-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="66af3-156">Este cambio crea más coherencia de tipo hello del patrón de Hola desencadenador es toobuild usado.</span><span class="sxs-lookup"><span data-stu-id="66af3-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="66af3-157">Nueva acción 'filtro'</span><span class="sxs-lookup"><span data-stu-id="66af3-157">New 'filter' action</span></span>

<span data-ttu-id="66af3-158">una matriz grande hacia abajo tooa conjunto más pequeño de elementos, new hello toofilter `filter` tipo acepta una matriz y una condición, se evalúa como condición de Hola para cada elemento y devuelve una matriz con los elementos que cumplen la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="66af3-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="66af3-159">Restricciones de las acciones "foreach" y "until"</span><span class="sxs-lookup"><span data-stu-id="66af3-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="66af3-160">Hola `foreach` y `until` bucle están restringidos tooa única acción.</span><span class="sxs-lookup"><span data-stu-id="66af3-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="66af3-161">Nueva propiedad "trackedProperties" para las acciones</span><span class="sxs-lookup"><span data-stu-id="66af3-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="66af3-162">Acciones ahora pueden tener una propiedad adicional denominada `trackedProperties`, que es el mismo nivel toohello `runAfter` y `type` propiedades.</span><span class="sxs-lookup"><span data-stu-id="66af3-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="66af3-163">Este objeto especifica algunas entradas de acción o salidas que desea tooinclude de telemetría de diagnóstico de Azure hello, genera como parte de un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="66af3-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="66af3-164">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="66af3-164">For example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="66af3-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66af3-165">Next Steps</span></span>
* [<span data-ttu-id="66af3-166">Creación de definiciones de flujo de trabajo para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="66af3-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="66af3-167">Creación de plantillas de implementación de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="66af3-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
