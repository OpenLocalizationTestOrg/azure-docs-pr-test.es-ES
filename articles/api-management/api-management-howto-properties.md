---
title: "Uso de propiedades en directivas de Administración de API de Azure"
description: "Aprenda a usar las propiedades en directivas de Administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="331e3-103">Uso de propiedades en directivas de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="331e3-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="331e3-104">En Administración de API, las directivas constituyen una eficaz funcionalidad del sistema que permite al editor cambiar el comportamiento de la API a través de la configuración.</span><span class="sxs-lookup"><span data-stu-id="331e3-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="331e3-105">Las directivas son una colección de declaraciones que se ejecutan secuencialmente en la solicitud o respuesta de una API.</span><span class="sxs-lookup"><span data-stu-id="331e3-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="331e3-106">Las instrucciones de las directivas se pueden crear con valores de texto literal, expresiones de directiva y propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="331e3-107">Cada instancia del servicio de Administración de API tiene una colección de propiedades de pares clave-valor que son globales para la instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="331e3-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="331e3-108">Estas propiedades se pueden utilizar para administrar los valores constantes de la cadena en todas las directivas y la configuración de API.</span><span class="sxs-lookup"><span data-stu-id="331e3-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="331e3-109">Cada propiedad tiene también los siguientes atributos.</span><span class="sxs-lookup"><span data-stu-id="331e3-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="331e3-110">Atributo</span><span class="sxs-lookup"><span data-stu-id="331e3-110">Attribute</span></span> | <span data-ttu-id="331e3-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="331e3-111">Type</span></span> | <span data-ttu-id="331e3-112">Description</span><span class="sxs-lookup"><span data-stu-id="331e3-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="331e3-113">Nombre</span><span class="sxs-lookup"><span data-stu-id="331e3-113">Name</span></span> |<span data-ttu-id="331e3-114">string</span><span class="sxs-lookup"><span data-stu-id="331e3-114">string</span></span> |<span data-ttu-id="331e3-115">El nombre de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="331e3-115">The name of the property.</span></span> <span data-ttu-id="331e3-116">Puede contener solo letras, dígitos, puntos, guiones o caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="331e3-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="331e3-117">Valor</span><span class="sxs-lookup"><span data-stu-id="331e3-117">Value</span></span> |<span data-ttu-id="331e3-118">string</span><span class="sxs-lookup"><span data-stu-id="331e3-118">string</span></span> |<span data-ttu-id="331e3-119">El valor de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="331e3-119">The value of the property.</span></span> <span data-ttu-id="331e3-120">No puede estar vacío ni contener solo espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="331e3-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="331e3-121">Secret</span><span class="sxs-lookup"><span data-stu-id="331e3-121">Secret</span></span> |<span data-ttu-id="331e3-122">boolean</span><span class="sxs-lookup"><span data-stu-id="331e3-122">boolean</span></span> |<span data-ttu-id="331e3-123">Determina si el valor es secreto y si se debe cifrar.</span><span class="sxs-lookup"><span data-stu-id="331e3-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="331e3-124">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="331e3-124">Tags</span></span> |<span data-ttu-id="331e3-125">matriz de cadena</span><span class="sxs-lookup"><span data-stu-id="331e3-125">array of string</span></span> |<span data-ttu-id="331e3-126">Etiquetas opcionales que, cuando se proporcionan, pueden usarse para filtrar la lista de propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="331e3-127">Las propiedades se configuran en el portal del editor, en la pestaña **Properties (Propiedades)** .</span><span class="sxs-lookup"><span data-stu-id="331e3-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="331e3-128">En el ejemplo siguiente, se configuran tres propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-128">In the following example, three properties are configured.</span></span>

![Properties (Propiedades)][api-management-properties]

<span data-ttu-id="331e3-130">Los valores de propiedad pueden contener cadenas literales y [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="331e3-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="331e3-131">En la siguiente tabla se muestran las tres propiedades de ejemplo anteriores y sus atributos.</span><span class="sxs-lookup"><span data-stu-id="331e3-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="331e3-132">El valor de `ExpressionProperty` es una expresión de directiva que devuelve una cadena que contiene la fecha y la hora actuales.</span><span class="sxs-lookup"><span data-stu-id="331e3-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="331e3-133">La propiedad `ContosoHeaderValue` está marcada como secreta, por lo que no se muestra su valor.</span><span class="sxs-lookup"><span data-stu-id="331e3-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="331e3-134">Nombre</span><span class="sxs-lookup"><span data-stu-id="331e3-134">Name</span></span> | <span data-ttu-id="331e3-135">Valor</span><span class="sxs-lookup"><span data-stu-id="331e3-135">Value</span></span> | <span data-ttu-id="331e3-136">Secret</span><span class="sxs-lookup"><span data-stu-id="331e3-136">Secret</span></span> | <span data-ttu-id="331e3-137">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="331e3-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="331e3-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="331e3-138">ContosoHeader</span></span> |<span data-ttu-id="331e3-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="331e3-139">TrackingId</span></span> |<span data-ttu-id="331e3-140">False</span><span class="sxs-lookup"><span data-stu-id="331e3-140">False</span></span> |<span data-ttu-id="331e3-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="331e3-141">Contoso</span></span> |
| <span data-ttu-id="331e3-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="331e3-142">ContosoHeaderValue</span></span> |<span data-ttu-id="331e3-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="331e3-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="331e3-144">True</span><span class="sxs-lookup"><span data-stu-id="331e3-144">True</span></span> |<span data-ttu-id="331e3-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="331e3-145">Contoso</span></span> |
| <span data-ttu-id="331e3-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="331e3-146">ExpressionProperty</span></span> |<span data-ttu-id="331e3-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="331e3-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="331e3-148">False</span><span class="sxs-lookup"><span data-stu-id="331e3-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="331e3-149">Uso de una propiedad</span><span class="sxs-lookup"><span data-stu-id="331e3-149">To use a property</span></span>
<span data-ttu-id="331e3-150">Para utilizar una propiedad en una directiva, coloque el nombre de la propiedad dentro de un par doble de llaves (como `{{ContosoHeader}}`), de la misma forma que se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="331e3-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="331e3-151">En este ejemplo, `ContosoHeader` se utiliza como el nombre de un encabezado en una directiva `set-header`, y `ContosoHeaderValue` se utiliza como valor de ese encabezado.</span><span class="sxs-lookup"><span data-stu-id="331e3-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="331e3-152">Cuando esta directiva se evalúa durante una solicitud o responde a la pasarela de Administración de API, `{{ContosoHeader}}` y `{{ContosoHeaderValue}}` se reemplazan por sus respectivos valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="331e3-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="331e3-153">Las propiedades se pueden utilizar como atributo completo como o valores de elemento (tal como se muestra en el ejemplo anterior), pero también se pueden insertar o combinar con parte de una expresión de texto literal, como en el ejemplo siguiente: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="331e3-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="331e3-154">Las propiedades también pueden contener expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="331e3-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="331e3-155">En el ejemplo siguiente, se utiliza la propiedad `ExpressionProperty`.</span><span class="sxs-lookup"><span data-stu-id="331e3-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="331e3-156">Cuando esta directiva se evalúa, se reemplaza `{{ExpressionProperty}}` por su valor: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="331e3-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="331e3-157">Puesto que el valor es una expresión de directiva, la expresión se evalúa y la directiva continúa con su ejecución.</span><span class="sxs-lookup"><span data-stu-id="331e3-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="331e3-158">Puede probarlo en el portal para desarrolladores si llama a una operación que tenga dentro de su ámbito una directiva con propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="331e3-159">En el ejemplo siguiente, se llama a una operación con las dos directivas `set-header` de ejemplo anteriores con propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="331e3-160">Tenga en cuenta que la respuesta contiene dos encabezados personalizados que se han configurado mediante directivas con propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![portal para desarrolladores][api-management-send-results]

<span data-ttu-id="331e3-162">Si busca en el [seguimiento de API Inspector](api-management-howto-api-inspector.md) una llamada que incluya las dos directivas de ejemplo anteriores con propiedades, verá las dos directivas `set-header` con los valores de propiedad insertados, así como la evaluación de la expresión de directiva para la propiedad que la contiene.</span><span class="sxs-lookup"><span data-stu-id="331e3-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![Seguimiento de API Inspector][api-management-api-inspector-trace]

<span data-ttu-id="331e3-164">Tenga en cuenta que, a pesar de que los valores de propiedad pueden contener expresiones de directiva, no pueden contener otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="331e3-165">Si se utiliza texto que contiene una referencia de propiedad para un valor de propiedad, como `Property value text {{MyProperty}}`, esa referencia de propiedad no se reemplazará y se incluirá como parte del valor de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="331e3-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="331e3-166">Creación de una propiedad</span><span class="sxs-lookup"><span data-stu-id="331e3-166">To create a property</span></span>
<span data-ttu-id="331e3-167">Para crear una propiedad, haga clic en **Agregar propiedad** en la pestaña **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="331e3-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Agregar propiedad][api-management-properties-add-property-menu]

<span data-ttu-id="331e3-169">Los campos **Nombre** y **Valor** son necesarios.</span><span class="sxs-lookup"><span data-stu-id="331e3-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="331e3-170">Si el valor de esta propiedad es un secreto, marque la casilla de verificación **This is a secret (Es secreto)** .</span><span class="sxs-lookup"><span data-stu-id="331e3-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="331e3-171">Escriba una o varias etiquetas opcionales para ayudar a organizar las propiedades y haga clic en **Save (Guardar)**.</span><span class="sxs-lookup"><span data-stu-id="331e3-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Agregar propiedad][api-management-properties-add-property]

<span data-ttu-id="331e3-173">Cuando se guarda una nueva propiedad, el cuadro de texto **Search property (Buscar propiedad)** se rellena con el nombre de la nueva propiedad y esta se muestra.</span><span class="sxs-lookup"><span data-stu-id="331e3-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="331e3-174">Para mostrar todas las propiedades, borre el cuadro de texto **Search property (Buscar propiedad)** y pulse la tecla Entrar.</span><span class="sxs-lookup"><span data-stu-id="331e3-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Properties (Propiedades)][api-management-properties-property-saved]

<span data-ttu-id="331e3-176">Para obtener información sobre cómo crear una propiedad mediante la API de REST, consulte [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)(Creación de una propiedad mediante la API de REST).</span><span class="sxs-lookup"><span data-stu-id="331e3-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="331e3-177">Edición de una propiedad</span><span class="sxs-lookup"><span data-stu-id="331e3-177">To edit a property</span></span>
<span data-ttu-id="331e3-178">Para editar una propiedad, haga clic en **Edit (Editar)** junto a la propiedad que se va a editar.</span><span class="sxs-lookup"><span data-stu-id="331e3-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Editar propiedad][api-management-properties-edit]

<span data-ttu-id="331e3-180">Realice los cambios necesarios y haga clic en **Save (Guardar)**.</span><span class="sxs-lookup"><span data-stu-id="331e3-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="331e3-181">Si cambia el nombre de propiedad, las directivas que hagan referencia a esa propiedad se actualizarán automáticamente para utilizar el nuevo nombre.</span><span class="sxs-lookup"><span data-stu-id="331e3-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Editar propiedad][api-management-properties-edit-property]

<span data-ttu-id="331e3-183">Para obtener información sobre cómo editar una propiedad mediante la API de REST, consulte [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)(Edición de una propiedad mediante la API de REST).</span><span class="sxs-lookup"><span data-stu-id="331e3-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="331e3-184">Eliminación de una propiedad</span><span class="sxs-lookup"><span data-stu-id="331e3-184">To delete a property</span></span>
<span data-ttu-id="331e3-185">Para eliminar una propiedad, haga clic en **Delete (Eliminar)** junto a la propiedad que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="331e3-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Eliminar propiedad][api-management-properties-delete]

<span data-ttu-id="331e3-187">Haga clic en **Sí, eliminar** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="331e3-187">Click **Yes, delete it** to confirm.</span></span>

![Confirmar eliminación][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="331e3-189">Si se hace referencia a la propiedad mediante alguna directiva, podrá eliminarla correctamente hasta que quite la propiedad de todas las directivas que la utilicen.</span><span class="sxs-lookup"><span data-stu-id="331e3-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="331e3-190">Para obtener información sobre cómo eliminar una propiedad mediante la API de REST, consulte [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)(Eliminación de una propiedad mediante la API de REST).</span><span class="sxs-lookup"><span data-stu-id="331e3-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="331e3-191">Búsqueda y filtrado de propiedades</span><span class="sxs-lookup"><span data-stu-id="331e3-191">To search and filter properties</span></span>
<span data-ttu-id="331e3-192">En la pestaña **Properties (Propiedades)** se incluyen las funcionalidades de búsqueda y filtrado para ayudarle a administrar las propiedades.</span><span class="sxs-lookup"><span data-stu-id="331e3-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="331e3-193">Para filtrar la lista de propiedades por el nombre de la propiedad, escriba un término de búsqueda en el cuadro de texto **Search property (Buscar propiedad)** .</span><span class="sxs-lookup"><span data-stu-id="331e3-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="331e3-194">Para mostrar todas las propiedades, borre el cuadro de texto **Search property (Buscar propiedad)** y pulse la tecla Entrar.</span><span class="sxs-lookup"><span data-stu-id="331e3-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="331e3-196">Para filtrar la lista de propiedades por valores de etiqueta, escriba una o varias etiquetas en el cuadro de texto **Filtrar por etiquetas** .</span><span class="sxs-lookup"><span data-stu-id="331e3-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="331e3-197">Para mostrar todas las propiedades, borre el cuadro de texto **Filter by tags (Filtrar por etiquetas)** y pulse la tecla Entrar.</span><span class="sxs-lookup"><span data-stu-id="331e3-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filtrar][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="331e3-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="331e3-199">Next steps</span></span>
* <span data-ttu-id="331e3-200">Obtenga más información sobre cómo trabajar con directivas</span><span class="sxs-lookup"><span data-stu-id="331e3-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="331e3-201">Directivas de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="331e3-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="331e3-202">Referencia de directiva</span><span class="sxs-lookup"><span data-stu-id="331e3-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="331e3-203">Policy expressions (Expresiones de directiva)</span><span class="sxs-lookup"><span data-stu-id="331e3-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="331e3-204">Vea un vídeo de introducción.</span><span class="sxs-lookup"><span data-stu-id="331e3-204">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

