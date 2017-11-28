---
title: comportamiento de aaaOverride HTTP mediante el motor de reglas de Azure CDN Hola | Documentos de Microsoft
description: "motor de reglas de Hello permite toocustomize cómo se administran las solicitudes HTTP CDN de Azure, como el bloqueo de entrega de Hola de determinados tipos de contenido, definir una directiva de almacenamiento en caché y modificar los encabezados HTTP."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="5234e-103">Invalidar el comportamiento HTTP mediante el motor de reglas de Azure CDN Hola</span><span class="sxs-lookup"><span data-stu-id="5234e-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="5234e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5234e-104">Overview</span></span>
<span data-ttu-id="5234e-105">motor de reglas de Hello permite toocustomize cómo se administran las solicitudes HTTP, por ejemplo, bloqueo de entrega de Hola de determinados tipos de contenido, definir una directiva de almacenamiento en caché y modificar los encabezados HTTP.</span><span class="sxs-lookup"><span data-stu-id="5234e-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="5234e-106">Este tutorial mostrará cómo crear una regla que cambiará el comportamiento de los activos de la red CDN de almacenamiento en caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="5234e-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="5234e-107">También hay contenido de vídeo en hello "[Vea también](#see-also)" sección.</span><span class="sxs-lookup"><span data-stu-id="5234e-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="5234e-108">Para una sintaxis de toohello de referencia de forma detallada, vea [referencia de motor de reglas](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5234e-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="5234e-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="5234e-109">Tutorial</span></span>
1. <span data-ttu-id="5234e-110">En la hoja de perfil CDN Hola, haga clic en hello **administrar** botón.</span><span class="sxs-lookup"><span data-stu-id="5234e-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Botón de administración de hoja de perfil de red CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="5234e-112">se abre el portal de administración de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="5234e-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="5234e-113">Haga clic en hello **HTTP grandes** ficha, seguido de **motor de reglas de**.</span><span class="sxs-lookup"><span data-stu-id="5234e-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="5234e-114">Se muestran las opciones para una nueva regla.</span><span class="sxs-lookup"><span data-stu-id="5234e-114">Options for a new rule are displayed.</span></span>
   
    ![Opciones de nueva regla de CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="5234e-116">orden de Hello en el que se muestran varias reglas afecta a cómo se controlan.</span><span class="sxs-lookup"><span data-stu-id="5234e-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="5234e-117">Una regla subsiguientes puede invalidar las acciones de hello especificadas por una regla anterior.</span><span class="sxs-lookup"><span data-stu-id="5234e-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="5234e-118">Escriba un nombre en hello **nombre / descripción** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="5234e-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="5234e-119">Identificar el tipo de saludo de solicitudes Hola regla se aplicará a.</span><span class="sxs-lookup"><span data-stu-id="5234e-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="5234e-120">De forma predeterminada, Hola **siempre** está seleccionada la condición de coincidencia.</span><span class="sxs-lookup"><span data-stu-id="5234e-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="5234e-121">Usará **Siempre** para este tutorial, así pues, deje esa opción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="5234e-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condición de coincidencia de red CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="5234e-123">Hay muchos tipos de coincidencia de las condiciones disponibles en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="5234e-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="5234e-124">Al hacer clic en hello azul icono informativo toohello izquierda de condición de coincidencia de Hola explicará condición Hola actualmente seleccionado en detalle.</span><span class="sxs-lookup"><span data-stu-id="5234e-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="5234e-125">Para hello lista completa de las expresiones condicionales en detalle, consulte [expresiones condicionales de motor de reglas](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="5234e-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="5234e-126">Para hello lista completa de las condiciones de coincidencia de forma detallada, consulte [coincide con condiciones del motor de reglas](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="5234e-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="5234e-127">Haga clic en hello  **+**  aparece al lado demasiado**características** tooadd una nueva característica.</span><span class="sxs-lookup"><span data-stu-id="5234e-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="5234e-128">En la lista desplegable de Hola Hola izquierda, seleccione **Force interno Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="5234e-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="5234e-129">En el cuadro de texto hello que aparece, escriba **300**.</span><span class="sxs-lookup"><span data-stu-id="5234e-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="5234e-130">Deje Hola restantes valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="5234e-130">Leave hello remaining default values.</span></span>
   
   ![Característica de CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="5234e-132">Como con las condiciones de coincidencia, haga clic en hello azul icono informativo toohello dejó de hello nueva característica mostrará información sobre esta característica.</span><span class="sxs-lookup"><span data-stu-id="5234e-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="5234e-133">En caso de hello de **Force interno Max-Age**, nos estamos reemplazar del recurso de hello **Cache-Control** y **Expires** encabezados toocontrol al nodo del borde CDN Hola actualizará Hola activo a partir de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="5234e-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="5234e-134">Nuestro ejemplo de 300 segundos significa el nodo del borde CDN Hola almacenarán en caché activo de Hola durante 5 minutos antes de actualizar los activos de Hola desde su origen.</span><span class="sxs-lookup"><span data-stu-id="5234e-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="5234e-135">Para hello lista completa de características de forma detallada, consulte [detalles de característica de motor de reglas](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="5234e-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="5234e-136">Haga clic en hello **agregar** nueva regla de botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="5234e-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="5234e-137">nueva regla de Hello ahora está en espera de aprobación.</span><span class="sxs-lookup"><span data-stu-id="5234e-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="5234e-138">Una vez aprobada, estado de hello cambiará de **XML pendiente** demasiado**XML Active**.</span><span class="sxs-lookup"><span data-stu-id="5234e-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5234e-139">Cambios de reglas pueden tardar too90 minutos toopropagate a través de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="5234e-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="5234e-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="5234e-140">See also</span></span>
* [<span data-ttu-id="5234e-141">Información general de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="5234e-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="5234e-142">Referencia del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="5234e-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="5234e-143">Condiciones de coincidencia del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="5234e-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="5234e-144">Expresiones condicionales del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="5234e-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="5234e-145">Funciones del motor de reglas</span><span class="sxs-lookup"><span data-stu-id="5234e-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="5234e-146">Invalidar el comportamiento HTTP predeterminado mediante el motor de reglas de Hola</span><span class="sxs-lookup"><span data-stu-id="5234e-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="5234e-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (Azure Fridays: Características nuevas y eficaces de la edición Premium de CDN de Azure) (vídeo)</span><span class="sxs-lookup"><span data-stu-id="5234e-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>