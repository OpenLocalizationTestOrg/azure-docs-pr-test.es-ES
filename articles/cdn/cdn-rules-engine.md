---
title: "Invalidación del comportamiento HTTP mediante el motor de reglas de la red CDN de Azure | Microsoft Docs"
description: "El motor de reglas permite personalizar cómo la red CDN de Azure controla las solicitudes HTTP, como el bloqueo de la entrega de determinados tipos de contenido, la definición de una directiva de almacenamiento en caché y la modificación de encabezados HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="efb32-103">Invalidación del comportamiento HTTP mediante el motor de reglas de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="efb32-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="efb32-104">Información general</span><span class="sxs-lookup"><span data-stu-id="efb32-104">Overview</span></span>
<span data-ttu-id="efb32-105">El motor de reglas le permite personalizar cómo se controlan las solicitudes HTTP, tales como el bloqueo de la entrega de determinados tipos de contenido, la definición de una directiva de almacenamiento en caché y la modificación de encabezados HTTP.</span><span class="sxs-lookup"><span data-stu-id="efb32-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="efb32-106">En este tutorial se mostrará la creación de una regla que cambiará el comportamiento del almacenamiento en caché de los recursos de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="efb32-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="efb32-107">También hay contenido de vídeo en la sección "[Consulte también](#see-also)".</span><span class="sxs-lookup"><span data-stu-id="efb32-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="efb32-108">Para consultar la sintaxis de forma detallada, vea la [Referencia del motor de reglas](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="efb32-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="efb32-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="efb32-109">Tutorial</span></span>
1. <span data-ttu-id="efb32-110">En la hoja de perfil de CDN, haga clic en el botón **Administrar** .</span><span class="sxs-lookup"><span data-stu-id="efb32-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="efb32-112">Se abre el portal de administración de CDN.</span><span class="sxs-lookup"><span data-stu-id="efb32-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="efb32-113">Haga clic en la pestaña **HTTP Large** (HTTP grande) y, después, en **Motor de reglas**.</span><span class="sxs-lookup"><span data-stu-id="efb32-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="efb32-114">Se muestran las opciones para una nueva regla.</span><span class="sxs-lookup"><span data-stu-id="efb32-114">Options for a new rule are displayed.</span></span>
   
    ![Opciones de nueva regla de CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="efb32-116">El orden en que se muestran varias reglas afecta a la manera en que se controlan.</span><span class="sxs-lookup"><span data-stu-id="efb32-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="efb32-117">Una regla posterior puede invalidar las acciones especificadas por una regla anterior.</span><span class="sxs-lookup"><span data-stu-id="efb32-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="efb32-118">Escriba un nombre en el cuadro de texto **Nombre/Descripción** .</span><span class="sxs-lookup"><span data-stu-id="efb32-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="efb32-119">Identifique el tipo de solicitudes al que se aplicará la regla.</span><span class="sxs-lookup"><span data-stu-id="efb32-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="efb32-120">De forma predeterminada, se selecciona la condición de coincidencia **Siempre** .</span><span class="sxs-lookup"><span data-stu-id="efb32-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="efb32-121">Usará **Siempre** para este tutorial, así pues, deje esa opción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="efb32-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condición de coincidencia de red CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="efb32-123">Hay muchos tipos de condiciones de coincidencia disponibles en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="efb32-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="efb32-124">Haga clic en el icono de información azul de la izquierda de la condición de coincidencia para ver una explicación de la condición seleccionada actualmente en detalle.</span><span class="sxs-lookup"><span data-stu-id="efb32-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="efb32-125">Para obtener la lista completa de las expresiones condicionales en detalle, consulte las [Expresiones condicionales del motor de reglas](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="efb32-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="efb32-126">Para obtener la lista completa de las condiciones de coincidencia en detalle, consulte las [Condiciones de coincidencia del motor de reglas](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="efb32-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="efb32-127">Haga clic en el botón **+** que está al lado de **Características** para agregar una nueva característica.</span><span class="sxs-lookup"><span data-stu-id="efb32-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="efb32-128">En la lista desplegable de la izquierda, seleccione **Aplicar Max-Age interno**.</span><span class="sxs-lookup"><span data-stu-id="efb32-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="efb32-129">En el cuadro de texto que aparece, escriba **300**.</span><span class="sxs-lookup"><span data-stu-id="efb32-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="efb32-130">Deje los valores predeterminados restantes.</span><span class="sxs-lookup"><span data-stu-id="efb32-130">Leave the remaining default values.</span></span>
   
   ![Característica de CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="efb32-132">Como con las condiciones de coincidencia, haga clic en el icono informativo azul de la izquierda de la nueva característica para ver la información sobre esta característica.</span><span class="sxs-lookup"><span data-stu-id="efb32-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="efb32-133">In the case of **Force Internal Max-Age**, vamos a invalidar los encabezados **Cache-Control** y **Expires** del recurso para controlar en qué momento el nodo del borde CDN va a actualizar el recurso desde el origen.</span><span class="sxs-lookup"><span data-stu-id="efb32-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="efb32-134">Nuestro ejemplo de 300 segundos significa que el nodo perimetral de CDN almacenará en caché el activo durante 5 minutos antes de actualizar el activo desde su origen.</span><span class="sxs-lookup"><span data-stu-id="efb32-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="efb32-135">Para obtener la lista completa de las características en detalle, consulte la [Información detallada de las características del motor de reglas](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="efb32-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="efb32-136">Haga clic en el botón **Agregar** para guardar la nueva regla.</span><span class="sxs-lookup"><span data-stu-id="efb32-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="efb32-137">La nueva regla ahora está pendiente de aprobación.</span><span class="sxs-lookup"><span data-stu-id="efb32-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="efb32-138">Una vez que se haya aprobado, el estado cambiará de **Pending XML** (XML pendiente) a **Active XML** (XML activo).</span><span class="sxs-lookup"><span data-stu-id="efb32-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="efb32-139">Los cambios de las reglas pueden tardar hasta 90 minutos en propagarse a través de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="efb32-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="efb32-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="efb32-140">See also</span></span>
* [<span data-ttu-id="efb32-141">Información general de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="efb32-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="efb32-142">Referencia del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="efb32-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="efb32-143">Condiciones de coincidencia del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="efb32-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="efb32-144">Expresiones condicionales del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="efb32-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="efb32-145">Funciones del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="efb32-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="efb32-146">Invalidación del comportamiento HTTP predeterminado mediante el motor de reglas</span><span class="sxs-lookup"><span data-stu-id="efb32-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="efb32-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (Azure Fridays: Características nuevas y eficaces de la edición Premium de CDN de Azure) (vídeo)</span><span class="sxs-lookup"><span data-stu-id="efb32-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>