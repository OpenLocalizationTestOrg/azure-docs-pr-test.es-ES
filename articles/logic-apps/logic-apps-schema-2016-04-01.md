---
title: Actualizaciones de esquema, 1 de junio de 2016 (Azure Logic Apps) | Microsoft Docs
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
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="a1738-103">Actualizaciones de esquema para Azure Logic Apps, 1 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="a1738-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="a1738-104">Esta nueva versión de esquema y API de Azure Logic Apps incluye importantes mejoras que aportan una mayor confiabilidad a las aplicaciones lógicas y facilitan su uso:</span><span class="sxs-lookup"><span data-stu-id="a1738-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="a1738-105">[Ámbitos](#scopes): le permiten agrupar o anidar acciones como una colección de acciones.</span><span class="sxs-lookup"><span data-stu-id="a1738-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="a1738-106">[Condiciones y bucles](#conditions-loops): ahora son acciones de primera clase.</span><span class="sxs-lookup"><span data-stu-id="a1738-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="a1738-107">Ordenación más precisa para ejecutar acciones con la propiedad `runAfter`, sustituyendo `dependsOn`.</span><span class="sxs-lookup"><span data-stu-id="a1738-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="a1738-108">Para actualizar las aplicaciones lógicas del esquema de versión preliminar del 1 de agosto de 2015 al esquema del 1 de junio de 2016, [consulte la sección de actualización](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="a1738-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="a1738-109">Ámbitos</span><span class="sxs-lookup"><span data-stu-id="a1738-109">Scopes</span></span>

<span data-ttu-id="a1738-110">Este esquema incluye ámbitos, que le permiten agrupar acciones o anidar acciones unas dentro de otras.</span><span class="sxs-lookup"><span data-stu-id="a1738-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="a1738-111">Por ejemplo, una condición puede contener otra condición.</span><span class="sxs-lookup"><span data-stu-id="a1738-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="a1738-112">Aprenda más sobre la [sintaxis de los ámbitos](../logic-apps/logic-apps-loops-and-scopes.md), o revise este ejemplo básico de ámbitos:</span><span class="sxs-lookup"><span data-stu-id="a1738-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

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
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="a1738-113">Cambios de condiciones y bucles</span><span class="sxs-lookup"><span data-stu-id="a1738-113">Conditions and loops changes</span></span>

<span data-ttu-id="a1738-114">En las versiones anteriores del esquema, las condiciones y los bucles eran parámetros asociados a una sola acción.</span><span class="sxs-lookup"><span data-stu-id="a1738-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="a1738-115">Este esquema elimina esta limitación, por lo que las condiciones y los bucles aparecen ahora como tipos de acción.</span><span class="sxs-lookup"><span data-stu-id="a1738-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="a1738-116">Aprenda más sobre [bucles y ámbitos](../logic-apps/logic-apps-loops-and-scopes.md), o revise este ejemplo básico de una acción de condición:</span><span class="sxs-lookup"><span data-stu-id="a1738-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

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
## <a name="runafter-property"></a><span data-ttu-id="a1738-117">Propiedad "runAfter"</span><span class="sxs-lookup"><span data-stu-id="a1738-117">'runAfter' property</span></span>

<span data-ttu-id="a1738-118">La propiedad `runAfter` reemplaza a `dependsOn`, por lo que se proporciona una mayor precisión al especificar el orden de ejecución de las acciones según el estado de acciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="a1738-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="a1738-119">La propiedad `dependsOn` era sinónimo de "la acción se ejecutó correctamente", no importa cuántas veces quisiera ejecutar una acción, en función de si la acción anterior era correcta, tenía un error o se había omitido.</span><span class="sxs-lookup"><span data-stu-id="a1738-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="a1738-120">La propiedad `runAfter` ofrece esa flexibilidad como un objeto que especifica todos los nombres de acciones después de los cuales se ejecuta el objeto.</span><span class="sxs-lookup"><span data-stu-id="a1738-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="a1738-121">Esta propiedad también define una matriz de estados que son aceptables como desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="a1738-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="a1738-122">Por ejemplo, si quisiera ejecutar una acción después de que el paso A se realiza correctamente y también después de que el paso B se realiza correctamente o produce error, construiría esta propiedad `runAfter`:</span><span class="sxs-lookup"><span data-stu-id="a1738-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="a1738-123">Actualización del esquema</span><span class="sxs-lookup"><span data-stu-id="a1738-123">Upgrade your schema</span></span>

<span data-ttu-id="a1738-124">La actualización al nuevo esquema se realiza en solo unos cuantos pasos.</span><span class="sxs-lookup"><span data-stu-id="a1738-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="a1738-125">El proceso de actualización incluye ejecutar el script de actualización, guardarlo como una nueva aplicación lógica y, posiblemente, sobrescribir la antigua aplicación lógica, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="a1738-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="a1738-126">Abra la aplicación lógica en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1738-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="a1738-127">Vaya a **Overview** (Información general).</span><span class="sxs-lookup"><span data-stu-id="a1738-127">Go to **Overview**.</span></span> <span data-ttu-id="a1738-128">En la barra de herramientas de aplicaciones lógicas, elija **Actualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="a1738-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Selección del esquema de actualización][1]
   
    <span data-ttu-id="a1738-130">Se devuelve la definición actualizada, que puede copiar y pegar en una definición de recurso si es necesario.</span><span class="sxs-lookup"><span data-stu-id="a1738-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="a1738-131">Pero **se recomienda firmemente** elegir **Guardar como** para asegurarse de que todas las referencias de conexión sean válidas en la aplicación lógica actualizada.</span><span class="sxs-lookup"><span data-stu-id="a1738-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="a1738-132">En la barra de herramientas de la hoja de actualización, elija **Guardar como**.</span><span class="sxs-lookup"><span data-stu-id="a1738-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="a1738-133">Escriba el nombre y el estado de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a1738-133">Enter the logic name and status.</span></span> <span data-ttu-id="a1738-134">Para implementar la aplicación lógica actualizada, elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a1738-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="a1738-135">Confirme que la aplicación lógica actualizada funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="a1738-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1738-136">Si usa un desencadenador manual o de solicitud, la dirección URL de devolución de llamada cambia en la nueva aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a1738-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="a1738-137">Pruebe la nueva dirección URL para asegurarse de que funciona completamente.</span><span class="sxs-lookup"><span data-stu-id="a1738-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="a1738-138">Para conservar las direcciones URL anteriores, puede clonarlas a través de la aplicación lógica existente.</span><span class="sxs-lookup"><span data-stu-id="a1738-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="a1738-139">*Opcional*: para sobrescribir la aplicación lógica anterior con la nueva versión de esquema, en la barra de herramientas, elija **Clonar**, junto a **Actualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="a1738-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="a1738-140">Este paso solo es necesario si quiere mantener el mismo identificador de recurso o dirección URL del desencadenador de solicitud de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a1738-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="a1738-141">Notas de la herramienta de actualización</span><span class="sxs-lookup"><span data-stu-id="a1738-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="a1738-142">Condiciones de asignación</span><span class="sxs-lookup"><span data-stu-id="a1738-142">Mapping conditions</span></span>

<span data-ttu-id="a1738-143">En la definición actualizada, la herramienta hace todo lo posible por agrupar las acciones de bifurcación true y false como un ámbito.</span><span class="sxs-lookup"><span data-stu-id="a1738-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="a1738-144">En concreto, el patrón de diseñador de `@equals(actions('a').status, 'Skipped')` debe aparecer como una acción `else`.</span><span class="sxs-lookup"><span data-stu-id="a1738-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="a1738-145">Sin embargo, si la herramienta detecta patrones irreconocibles, podría crear condiciones distintas para la bifurcación true y false.</span><span class="sxs-lookup"><span data-stu-id="a1738-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="a1738-146">Si es necesario, puede volver a asignar acciones después de la actualización.</span><span class="sxs-lookup"><span data-stu-id="a1738-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="a1738-147">Bucle "foreach" con condición</span><span class="sxs-lookup"><span data-stu-id="a1738-147">'foreach' loop with condition</span></span>

<span data-ttu-id="a1738-148">En el nuevo esquema, puede usar la acción de filtro para replicar el patrón de un bucle `foreach` con una condición por elemento, pero este cambio debe ocurrir automáticamente al actualizar.</span><span class="sxs-lookup"><span data-stu-id="a1738-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="a1738-149">La condición se convierte en una acción de filtro delante del bucle foreach para devolver solo una matriz de elementos que coincidan con la condición, y esa matriz se pasa a la acción de foreach.</span><span class="sxs-lookup"><span data-stu-id="a1738-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="a1738-150">Para ver un ejemplo, consulte [Bucles y ámbitos](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="a1738-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="a1738-151">Etiquetas del recurso</span><span class="sxs-lookup"><span data-stu-id="a1738-151">Resource tags</span></span>

<span data-ttu-id="a1738-152">Después de actualizar, se quitan las etiquetas del recurso, por lo que debe restablecerlas para el flujo de trabajo actualizado.</span><span class="sxs-lookup"><span data-stu-id="a1738-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="a1738-153">Otros cambios</span><span class="sxs-lookup"><span data-stu-id="a1738-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="a1738-154">Cambio de nombre de desencadenador "manual" a desencadenador "request"</span><span class="sxs-lookup"><span data-stu-id="a1738-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="a1738-155">El tipo de desencadenador `manual` está en desuso y ahora se llama `request` con el tipo `http`.</span><span class="sxs-lookup"><span data-stu-id="a1738-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="a1738-156">Este cambio crea una mayor coherencia para la clase de patrón que el desencadenador suele compilar.</span><span class="sxs-lookup"><span data-stu-id="a1738-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="a1738-157">Nueva acción 'filtro'</span><span class="sxs-lookup"><span data-stu-id="a1738-157">New 'filter' action</span></span>

<span data-ttu-id="a1738-158">Para filtrar una matriz grande hasta un conjunto de elementos más pequeño, el nuevo tipo `filter` acepta una matriz y una condición, evalúa la condición de cada elemento y devuelve una matriz con los elementos que cumplen la condición.</span><span class="sxs-lookup"><span data-stu-id="a1738-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="a1738-159">Restricciones de las acciones "foreach" y "until"</span><span class="sxs-lookup"><span data-stu-id="a1738-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="a1738-160">Los bucles `foreach` y `until` están limitados a una sola acción.</span><span class="sxs-lookup"><span data-stu-id="a1738-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="a1738-161">Nueva propiedad "trackedProperties" para las acciones</span><span class="sxs-lookup"><span data-stu-id="a1738-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="a1738-162">Las acciones pueden tener ahora una propiedad adicional llamada `trackedProperties`, que está relacionada con las propiedades `runAfter` y `type`.</span><span class="sxs-lookup"><span data-stu-id="a1738-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="a1738-163">Este objeto especifica determinadas entradas o salidas de acciones que desea incluir en la telemetría de Azure Diagnostic, que se emiten como parte de un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a1738-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="a1738-164">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a1738-164">For example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a1738-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1738-165">Next Steps</span></span>
* [<span data-ttu-id="a1738-166">Creación de definiciones de flujo de trabajo para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="a1738-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="a1738-167">Creación de plantillas de implementación de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="a1738-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
