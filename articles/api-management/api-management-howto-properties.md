---
title: "propiedades de toouse aaaHow en las directivas de administración de API de Azure"
description: "Obtenga información acerca de cómo toouse propiedades en las directivas de administración de API de Azure."
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
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="9bff3-103">¿Cómo toouse propiedades en las directivas de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="9bff3-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="9bff3-104">Las directivas de administración de API son una capacidad eficaz del sistema de Hola que permiten a publicador hello toochange comportamiento de Hola de hello API a través de la configuración.</span><span class="sxs-lookup"><span data-stu-id="9bff3-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="9bff3-105">Las directivas son una colección de instrucciones que se ejecutan secuencialmente en la solicitud de Hola o respuesta de una API.</span><span class="sxs-lookup"><span data-stu-id="9bff3-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="9bff3-106">Las instrucciones de las directivas se pueden crear con valores de texto literal, expresiones de directiva y propiedades.</span><span class="sxs-lookup"><span data-stu-id="9bff3-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="9bff3-107">Cada instancia de servicio de administración de API tiene una colección de propiedades de pares clave/valor que las instancias de servicio de toohello global.</span><span class="sxs-lookup"><span data-stu-id="9bff3-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="9bff3-108">Estas propiedades pueden ser valores de cadena constante toomanage usados a través de todas las directivas y configuración de la API.</span><span class="sxs-lookup"><span data-stu-id="9bff3-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="9bff3-109">Cada propiedad tiene los siguientes atributos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="9bff3-110">Atributo</span><span class="sxs-lookup"><span data-stu-id="9bff3-110">Attribute</span></span> | <span data-ttu-id="9bff3-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="9bff3-111">Type</span></span> | <span data-ttu-id="9bff3-112">Description</span><span class="sxs-lookup"><span data-stu-id="9bff3-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9bff3-113">Nombre</span><span class="sxs-lookup"><span data-stu-id="9bff3-113">Name</span></span> |<span data-ttu-id="9bff3-114">cadena</span><span class="sxs-lookup"><span data-stu-id="9bff3-114">string</span></span> |<span data-ttu-id="9bff3-115">nombre de Hola de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-115">hello name of hello property.</span></span> <span data-ttu-id="9bff3-116">Puede contener solo letras, dígitos, puntos, guiones o caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="9bff3-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="9bff3-117">Valor</span><span class="sxs-lookup"><span data-stu-id="9bff3-117">Value</span></span> |<span data-ttu-id="9bff3-118">cadena</span><span class="sxs-lookup"><span data-stu-id="9bff3-118">string</span></span> |<span data-ttu-id="9bff3-119">valor de Hola de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-119">hello value of hello property.</span></span> <span data-ttu-id="9bff3-120">No puede estar vacío ni contener solo espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="9bff3-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="9bff3-121">Secret</span><span class="sxs-lookup"><span data-stu-id="9bff3-121">Secret</span></span> |<span data-ttu-id="9bff3-122">boolean</span><span class="sxs-lookup"><span data-stu-id="9bff3-122">boolean</span></span> |<span data-ttu-id="9bff3-123">Determina si el valor de hello es un secreto y debe cifrarse o no.</span><span class="sxs-lookup"><span data-stu-id="9bff3-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="9bff3-124">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="9bff3-124">Tags</span></span> |<span data-ttu-id="9bff3-125">matriz de cadena</span><span class="sxs-lookup"><span data-stu-id="9bff3-125">array of string</span></span> |<span data-ttu-id="9bff3-126">Opcional de etiquetas que cuando se proporciona puede ser la lista de propiedades de hello toofilter usado.</span><span class="sxs-lookup"><span data-stu-id="9bff3-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="9bff3-127">Propiedades se configuran en el portal para desarrolladores de hello en hello **propiedades** ficha. En el siguiente ejemplo de Hola, se configuran tres propiedades.</span><span class="sxs-lookup"><span data-stu-id="9bff3-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Propiedades][api-management-properties]

<span data-ttu-id="9bff3-129">Los valores de propiedad pueden contener cadenas literales y [expresiones de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bff3-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="9bff3-130">Hello tabla siguiente muestran Hola anterior ejemplo tres propiedades y sus atributos.</span><span class="sxs-lookup"><span data-stu-id="9bff3-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="9bff3-131">Hola valo `ExpressionProperty` es una expresión de directiva que devuelve una cadena que contiene Hola fecha y hora actuales.</span><span class="sxs-lookup"><span data-stu-id="9bff3-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="9bff3-132">Hola propiedad `ContosoHeaderValue` está marcada como un secreto, por lo que no se muestra su valor.</span><span class="sxs-lookup"><span data-stu-id="9bff3-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="9bff3-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="9bff3-133">Name</span></span> | <span data-ttu-id="9bff3-134">Valor</span><span class="sxs-lookup"><span data-stu-id="9bff3-134">Value</span></span> | <span data-ttu-id="9bff3-135">Secret</span><span class="sxs-lookup"><span data-stu-id="9bff3-135">Secret</span></span> | <span data-ttu-id="9bff3-136">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="9bff3-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9bff3-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="9bff3-137">ContosoHeader</span></span> |<span data-ttu-id="9bff3-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="9bff3-138">TrackingId</span></span> |<span data-ttu-id="9bff3-139">False</span><span class="sxs-lookup"><span data-stu-id="9bff3-139">False</span></span> |<span data-ttu-id="9bff3-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="9bff3-140">Contoso</span></span> |
| <span data-ttu-id="9bff3-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="9bff3-141">ContosoHeaderValue</span></span> |<span data-ttu-id="9bff3-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="9bff3-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="9bff3-143">True</span><span class="sxs-lookup"><span data-stu-id="9bff3-143">True</span></span> |<span data-ttu-id="9bff3-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="9bff3-144">Contoso</span></span> |
| <span data-ttu-id="9bff3-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="9bff3-145">ExpressionProperty</span></span> |<span data-ttu-id="9bff3-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="9bff3-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="9bff3-147">False</span><span class="sxs-lookup"><span data-stu-id="9bff3-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="9bff3-148">toouse una propiedad</span><span class="sxs-lookup"><span data-stu-id="9bff3-148">toouse a property</span></span>
<span data-ttu-id="9bff3-149">nombre de la propiedad de contexto Hola dentro de un par de llaves doble, toouse una propiedad en una directiva, como `{{ContosoHeader}}`, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="9bff3-150">En este ejemplo, `ContosoHeader` se usa como nombre de Hola de un encabezado en un `set-header` directiva, y `ContosoHeaderValue` se utiliza como valor de Hola de ese encabezado.</span><span class="sxs-lookup"><span data-stu-id="9bff3-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="9bff3-151">Cuando esta directiva se evalúa durante una solicitud o respuesta toohello administración de API puerta de enlace, `{{ContosoHeader}}` y `{{ContosoHeaderValue}}` se reemplazan con sus respectivos valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="9bff3-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="9bff3-152">Propiedades que se pueden usar como atributo completa o valores de elemento, como se muestra en el ejemplo anterior de hello, pero también pueden inserta o combina con parte de una expresión de texto literal, como se muestra en el siguiente ejemplo de Hola:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="9bff3-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="9bff3-153">Las propiedades también pueden contener expresiones de directiva.</span><span class="sxs-lookup"><span data-stu-id="9bff3-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="9bff3-154">En el siguiente ejemplo de Hola Hola `ExpressionProperty` se utiliza.</span><span class="sxs-lookup"><span data-stu-id="9bff3-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="9bff3-155">Cuando esta directiva se evalúa, se reemplaza `{{ExpressionProperty}}` por su valor: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="9bff3-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="9bff3-156">Puesto que el valor de hello es una expresión de directiva, Hola expresión se evalúa y directiva de hello continúa con su ejecución.</span><span class="sxs-lookup"><span data-stu-id="9bff3-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="9bff3-157">Puede probar este comando en el portal para desarrolladores de hello mediante una llamada a una operación que tiene una directiva con propiedades en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="9bff3-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="9bff3-158">En el siguiente ejemplo de Hola, se llama a una operación con hello dos anterior ejemplo `set-header` directivas con propiedades.</span><span class="sxs-lookup"><span data-stu-id="9bff3-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="9bff3-159">Tenga en cuenta que la respuesta hello contiene dos encabezados personalizados que se configuraron mediante directivas con propiedades.</span><span class="sxs-lookup"><span data-stu-id="9bff3-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![portal para desarrolladores][api-management-send-results]

<span data-ttu-id="9bff3-161">Si observa hello [seguimiento de API Inspector](api-management-howto-api-inspector.md) para una llamada que incluye dos directivas de ejemplo Hola anterior con propiedades, puede ver dos hello `set-header` directivas con valores de propiedad de hello insertadas, así como la expresión de directiva de Hola evaluación de la propiedad de Hola que contiene la expresión de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![Seguimiento de API Inspector][api-management-api-inspector-trace]

<span data-ttu-id="9bff3-163">Tenga en cuenta que, a pesar de que los valores de propiedad pueden contener expresiones de directiva, no pueden contener otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="9bff3-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="9bff3-164">Si el texto que contiene una referencia de propiedad se utiliza para un valor de propiedad, como `Property value text {{MyProperty}}`, que referencia de propiedad no se reemplazan y se van a incluir como parte del valor de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="9bff3-165">toocreate una propiedad</span><span class="sxs-lookup"><span data-stu-id="9bff3-165">toocreate a property</span></span>
<span data-ttu-id="9bff3-166">toocreate una propiedad, haga clic en **Agregar propiedad** en hello **propiedades** ficha.</span><span class="sxs-lookup"><span data-stu-id="9bff3-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Agregar propiedad][api-management-properties-add-property-menu]

<span data-ttu-id="9bff3-168">Los campos **Nombre** y **Valor** son necesarios.</span><span class="sxs-lookup"><span data-stu-id="9bff3-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="9bff3-169">Si este valor de propiedad es un secreto, compruebe hello **se trata de un secreto** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="9bff3-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="9bff3-170">Escriba uno o más toohelp etiquetas opcional con las propiedades de la organización y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="9bff3-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Agregar propiedad][api-management-properties-add-property]

<span data-ttu-id="9bff3-172">Cuando se guarda una nueva propiedad, Hola **propiedades de búsqueda** cuadro de texto se rellena con el nombre de Hola de hello nueva propiedad y se muestra la nueva propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bff3-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="9bff3-173">Borrar todas las propiedades de toodisplay hello **propiedades de búsqueda** cuadro de texto y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9bff3-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Propiedades][api-management-properties-property-saved]

<span data-ttu-id="9bff3-175">Para obtener información acerca de cómo crear una propiedad mediante la API de REST de hello, consulte [crear una propiedad mediante la API de REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="9bff3-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="9bff3-176">tooedit una propiedad</span><span class="sxs-lookup"><span data-stu-id="9bff3-176">tooedit a property</span></span>
<span data-ttu-id="9bff3-177">tooedit una propiedad, haga clic en **editar** lateral Hola propiedad tooedit.</span><span class="sxs-lookup"><span data-stu-id="9bff3-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Editar propiedad][api-management-properties-edit]

<span data-ttu-id="9bff3-179">Realice los cambios necesarios y haga clic en **Save (Guardar)**.</span><span class="sxs-lookup"><span data-stu-id="9bff3-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="9bff3-180">Si cambia el nombre de la propiedad de hello, las directivas que hacen referencia a esa propiedad son nombre nuevo de hello toouse actualizan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9bff3-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Editar propiedad][api-management-properties-edit-property]

<span data-ttu-id="9bff3-182">Para obtener información acerca de cómo modificar una propiedad mediante la API de REST de hello, consulte [editar una propiedad mediante la API de REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="9bff3-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="9bff3-183">toodelete una propiedad</span><span class="sxs-lookup"><span data-stu-id="9bff3-183">toodelete a property</span></span>
<span data-ttu-id="9bff3-184">toodelete una propiedad, haga clic en **eliminar** lateral Hola propiedad toodelete.</span><span class="sxs-lookup"><span data-stu-id="9bff3-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Eliminar propiedad][api-management-properties-delete]

<span data-ttu-id="9bff3-186">Haga clic en **Sí, eliminarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="9bff3-186">Click **Yes, delete it** tooconfirm.</span></span>

![Confirmar eliminación][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="9bff3-188">Si las directivas hace referencia a la propiedad de hello, no se podrá toosuccessfully eliminarlo hasta que quite la propiedad Hola de todas las directivas que lo usan.</span><span class="sxs-lookup"><span data-stu-id="9bff3-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="9bff3-189">Para obtener información acerca de cómo eliminar una propiedad mediante la API de REST de hello, consulte [eliminar una propiedad mediante la API de REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="9bff3-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="9bff3-190">propiedades de toosearch y filtrado</span><span class="sxs-lookup"><span data-stu-id="9bff3-190">toosearch and filter properties</span></span>
<span data-ttu-id="9bff3-191">Hola **propiedades** ficha incluye buscar y filtrar toohelp capacidades administrar sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="9bff3-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="9bff3-192">lista de propiedades de hello toofilter por nombre de propiedad, escriba un término de búsqueda en hello **propiedades de búsqueda** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9bff3-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="9bff3-193">Borrar todas las propiedades de toodisplay hello **propiedades de búsqueda** cuadro de texto y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9bff3-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="9bff3-195">lista de propiedades de hello toofilter por los valores de etiqueta, escriba una o más etiquetas en hello **filtrar por etiquetas** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9bff3-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="9bff3-196">Borrar todas las propiedades de toodisplay hello **filtrar por etiquetas** cuadro de texto y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9bff3-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filtrar][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="9bff3-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9bff3-198">Next steps</span></span>
* <span data-ttu-id="9bff3-199">Obtenga más información sobre cómo trabajar con directivas</span><span class="sxs-lookup"><span data-stu-id="9bff3-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="9bff3-200">Directivas de Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="9bff3-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="9bff3-201">Referencia de directiva</span><span class="sxs-lookup"><span data-stu-id="9bff3-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="9bff3-202">Policy expressions (Expresiones de directiva)</span><span class="sxs-lookup"><span data-stu-id="9bff3-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="9bff3-203">Vea un vídeo de introducción.</span><span class="sxs-lookup"><span data-stu-id="9bff3-203">Watch a video overview</span></span>
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

