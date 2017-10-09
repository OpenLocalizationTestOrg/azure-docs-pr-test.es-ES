---
title: "aaaSave búsquedas y pin datos activos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Cómo tooarticle capacidades resaltadas en el catálogo de datos para guardar los orígenes de datos y activos de datos para su uso posterior."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="18cd1-103">Guardar búsquedas y anclar recursos de datos en Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="18cd1-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="18cd1-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="18cd1-104">Introduction</span></span>
<span data-ttu-id="18cd1-105">Azure Data Catalog proporciona funciones de detección de orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="18cd1-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="18cd1-106">Rápidamente puede buscar y filtrar los orígenes de datos de hello catálogo toolocate y conocer su finalidad prevista, lo que sea más fáciles datos correctos de Hola de toofind de trabajo de hello en cuestión.</span><span class="sxs-lookup"><span data-stu-id="18cd1-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="18cd1-107">Pero ¿qué ocurre si necesita tooregularly trabajar con hello mismos datos?</span><span class="sxs-lookup"><span data-stu-id="18cd1-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="18cd1-108">Y ¿qué ocurre si usted y otros usuarios con regularidad aportar su toohello conocimiento mismos orígenes de datos en el catálogo de hello?</span><span class="sxs-lookup"><span data-stu-id="18cd1-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="18cd1-109">En estas situaciones, tiene toorepeatedly problema Hola mismo búsquedas pueden ser ineficaces.</span><span class="sxs-lookup"><span data-stu-id="18cd1-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="18cd1-110">Aquí es donde pueden ayudar las búsquedas guardadas y los recursos de datos anclados.</span><span class="sxs-lookup"><span data-stu-id="18cd1-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="18cd1-111">Búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="18cd1-111">Saved searches</span></span>
<span data-ttu-id="18cd1-112">Una búsqueda guardada en Data Catalog es una definición de búsqueda por usuario reutilizable.</span><span class="sxs-lookup"><span data-stu-id="18cd1-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="18cd1-113">Puede definir una búsqueda, incluidos los términos, etiquetas y otros filtros de la búsqueda y, a continuación, guardarla.</span><span class="sxs-lookup"><span data-stu-id="18cd1-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="18cd1-114">Puede volver a ejecutar definición de hello Guardar búsqueda posterior tooreturn los activos de datos que coinciden con sus criterios de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="18cd1-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="18cd1-115">Creación de una búsqueda guardada</span><span class="sxs-lookup"><span data-stu-id="18cd1-115">Create a saved search</span></span>
<span data-ttu-id="18cd1-116">toocreate una búsqueda guardada, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="18cd1-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="18cd1-117">En portal del catálogo de datos de Azure hello, Hola **búsqueda actual** ventana, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="18cd1-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Vínculo Guardar en la configuración de Búsqueda actual](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="18cd1-119">Especifique los criterios de búsqueda de Hola que desee tooreuse y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="18cd1-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Nombre de la búsqueda guardada en la configuración de Búsqueda actual](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="18cd1-121">Cuando se le pida, escriba un nombre para la búsqueda guardada de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="18cd1-122">Elija un nombre que sea significativo y que describe los activos de datos Hola devueltos por las búsquedas de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="18cd1-123">Administración de búsquedas guardadas</span><span class="sxs-lookup"><span data-stu-id="18cd1-123">Manage saved searches</span></span>
<span data-ttu-id="18cd1-124">Después de haber guardado búsquedas de uno o más, un **búsquedas guardadas** opción se muestra debajo de hello **búsqueda actual** cuadro.</span><span class="sxs-lookup"><span data-stu-id="18cd1-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="18cd1-125">Cuando se expande la lista de hello, se muestran todas las búsquedas guardadas.</span><span class="sxs-lookup"><span data-stu-id="18cd1-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Lista de búsquedas guardadas](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="18cd1-127">Realice cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="18cd1-127">Do any of hello following:</span></span>

* <span data-ttu-id="18cd1-128">tooexecute una búsqueda, seleccione una búsqueda guardada en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="18cd1-129">tooview una lista de opciones de administración de una búsqueda guardada, haga clic en hello hacia abajo la flecha siguiente toohello alias.</span><span class="sxs-lookup"><span data-stu-id="18cd1-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Opción para administrar búsquedas guardadas](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="18cd1-131">tooenter un nuevo nombre para la búsqueda de hello guardado, seleccione **cambiar el nombre de**.</span><span class="sxs-lookup"><span data-stu-id="18cd1-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="18cd1-132">no se cambia la definición de la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="18cd1-133">búsqueda de tooremove Hola guardado en la lista, seleccione **eliminar**y, a continuación, confirme la eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="18cd1-134">búsqueda de hello guarda toomark como la búsqueda de forma predeterminada, seleccione **Guardar como predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="18cd1-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="18cd1-135">Si realiza una búsqueda de "vacía" desde la página principal de hello el catálogo de datos, se ejecuta la búsqueda de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="18cd1-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="18cd1-136">Además, Hola búsqueda que se marca como búsqueda predeterminada de Hola se muestra en la parte superior de Hola de hello **búsquedas guardadas** lista.</span><span class="sxs-lookup"><span data-stu-id="18cd1-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="18cd1-137">Búsquedas guardadas de la organización</span><span class="sxs-lookup"><span data-stu-id="18cd1-137">Organizational saved searches</span></span>
<span data-ttu-id="18cd1-138">Todos los usuarios de la organización pueden guardar búsquedas para su propio uso.</span><span class="sxs-lookup"><span data-stu-id="18cd1-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="18cd1-139">Los administradores del catálogo de datos también pueden guardar búsquedas para todos los usuarios dentro de la organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="18cd1-140">Cuando los administradores guardar una búsqueda, le presentará una **recurso compartido de empresa de hello** opción.</span><span class="sxs-lookup"><span data-stu-id="18cd1-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="18cd1-141">Si se selecciona este Hola de recursos compartidos de opción guarda búsqueda para todos los usuarios en la organización de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Búsquedas guardadas de la organización](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="18cd1-143">Recursos de datos anclados</span><span class="sxs-lookup"><span data-stu-id="18cd1-143">Pinned data assets</span></span>
<span data-ttu-id="18cd1-144">Las búsquedas guardadas le permiten guardar y volver a usar las definiciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="18cd1-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="18cd1-145">activos de datos de Hello devueltos por las búsquedas Hola podrían cambiar con el tiempo como contenido de Hola de cambio de catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="18cd1-146">Al anclar activos de datos, puede identificar explícitamente toomake de activos de datos específicos les sea más fácil tooaccess sin necesidad de toouse una búsqueda.</span><span class="sxs-lookup"><span data-stu-id="18cd1-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="18cd1-147">Anclar un recurso de datos es sencillo.</span><span class="sxs-lookup"><span data-stu-id="18cd1-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="18cd1-148">tooadd Hola datos activos tooyour anclado, simplemente haga clic en hello **pin** icono.</span><span class="sxs-lookup"><span data-stu-id="18cd1-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="18cd1-149">icono de Hola se muestra en la esquina de Hola de hello asset mosaico en la vista en mosaico Hola y de columna del extremo izquierdo hello en la vista de lista de hello en el portal del catálogo de datos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![icono de anclaje de Hello datos activos](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="18cd1-151">Desanclar un recurso de datos es igual de sencillo.</span><span class="sxs-lookup"><span data-stu-id="18cd1-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="18cd1-152">Simplemente haga clic en hello **Desanclar** configuración de hello tootoggle de icono para el recurso seleccionado de Hola.</span><span class="sxs-lookup"><span data-stu-id="18cd1-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![recurso de datos Hola desanclar un icono](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="18cd1-154">Hola sección Mis activos</span><span class="sxs-lookup"><span data-stu-id="18cd1-154">hello My Assets section</span></span>
<span data-ttu-id="18cd1-155">Hola catálogo de datos de página principal del portal incluye un **activos mi** sección que se muestra los activos del usuario actual de interés toohello.</span><span class="sxs-lookup"><span data-stu-id="18cd1-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="18cd1-156">Esta sección incluye tanto recursos anclados como búsquedas guardadas.</span><span class="sxs-lookup"><span data-stu-id="18cd1-156">This section includes both pinned assets and saved searches.</span></span>

![Hola sección Mis activos en la página de inicio de Hola](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="18cd1-158">Resumen</span><span class="sxs-lookup"><span data-stu-id="18cd1-158">Summary</span></span>
<span data-ttu-id="18cd1-159">Catálogo de datos de Azure proporciona capacidades que hacen que sea más fácil toodiscover Hola los orígenes de datos que necesita, por lo que usted y otros miembros de la organización pueden dedicar menos tiempo buscando datos y más tiempo a trabajar con él.</span><span class="sxs-lookup"><span data-stu-id="18cd1-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="18cd1-160">Las búsquedas guardadas y los recursos de datos anclados se basan en estas funciones centrales para que los usuarios puedan identificar fácilmente los orígenes de datos con los que trabajan repetidamente.</span><span class="sxs-lookup"><span data-stu-id="18cd1-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
