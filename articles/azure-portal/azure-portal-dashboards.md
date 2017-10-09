---
title: aaaCreate y compartir los paneles del portal Azure | Documentos de Microsoft
description: "Este artículo explica cómo toocreate y editar paneles en Hola portal de Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="665db-103">Crear y compartir paneles en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="665db-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="665db-104">Puede crear varios paneles y compartirlos con otras personas que tienen acceso tooyour Azure suscripciones.</span><span class="sxs-lookup"><span data-stu-id="665db-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="665db-105">En este artículo se lleva a cabo conceptos básicos de Hola de crear, modificar, publicar y administrar el acceso toodashboards.</span><span class="sxs-lookup"><span data-stu-id="665db-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="665db-106">Creación de un panel</span><span class="sxs-lookup"><span data-stu-id="665db-106">Create a dashboard</span></span>
<span data-ttu-id="665db-107">toocreate un panel, seleccione hello **nuevo panel** botón siguiente toohello actual del nombre del panel.</span><span class="sxs-lookup"><span data-stu-id="665db-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![crear panel](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="665db-109">Esta acción crea un panel nuevo, vacío y privado, y activa el modo de personalización, donde puede asignar un nombre al panel y agregar o reorganizar los iconos.</span><span class="sxs-lookup"><span data-stu-id="665db-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="665db-110">En este modo, Hola contraíble icono Galería toma a través del menú de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="665db-111">Hello icono galería permite buscar iconos para los recursos de Azure de varias maneras: se puede examinar [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), por tipo de recurso, por [etiqueta](../azure-resource-manager/resource-group-using-tags.md), o busque el recurso por su nombre.</span><span class="sxs-lookup"><span data-stu-id="665db-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![personalizar panel](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="665db-113">Agregar iconos arrastrándolos y colocándolos en la superficie del panel de hello siempre que lo desee.</span><span class="sxs-lookup"><span data-stu-id="665db-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="665db-114">Hay una nueva categoría denominada **General** para los iconos que no están asociados a ningún recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="665db-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="665db-115">En este ejemplo, anclar mosaico de marcado de Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="665db-116">Utilice este panel de icono tooadd tooyour contenido personalizado.</span><span class="sxs-lookup"><span data-stu-id="665db-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="665db-117">icono Hello admite texto sin formato, [sintaxis de Markdown](https://daringfireball.net/projects/markdown/syntax)y un conjunto limitado de HTML.</span><span class="sxs-lookup"><span data-stu-id="665db-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="665db-118">(Por motivos de seguridad, no puede hacer cosas como insertar `<script>` etiquetas o uso de ciertos elementos de estilo de CSS que pueden interferir con el portal de Hola.)</span><span class="sxs-lookup"><span data-stu-id="665db-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![agregar Markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="665db-120">Edición de paneles</span><span class="sxs-lookup"><span data-stu-id="665db-120">Edit a dashboard</span></span>
<span data-ttu-id="665db-121">Después de crear el panel, puede anclar iconos desde la Galería de mosaico de Hola o representación de icono de Hola de hojas.</span><span class="sxs-lookup"><span data-stu-id="665db-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="665db-122">Vamos a anclar representación Hola de nuestro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="665db-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="665db-123">O bien, puede anclar al examinar hello, o de hoja de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="665db-124">Ambos métodos tienen como resultado fijar la representación en forma de mosaico Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="665db-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![Toodashboard de PIN](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="665db-126">Después de anclar elemento hello, aparece en el panel.</span><span class="sxs-lookup"><span data-stu-id="665db-126">After pinning hello item, it appears on your dashboard.</span></span>

![ver panel](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="665db-128">Ahora que tenemos un icono de marcado y un panel de toohello anclados del grupo de recursos, podemos cambiar el tamaño y reorganizar los mosaicos de hello en un diseño más adecuado.</span><span class="sxs-lookup"><span data-stu-id="665db-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="665db-129">Al mantener el mouse y seleccionando "..." o haciendo doble clic en un icono puede ver todos los comandos contextuales de Hola para ese icono.</span><span class="sxs-lookup"><span data-stu-id="665db-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="665db-130">De forma predeterminada, hay dos elementos:</span><span class="sxs-lookup"><span data-stu-id="665db-130">By default, there are two items:</span></span>

1. <span data-ttu-id="665db-131">**Desanclar del panel** : quita Hola icono de panel de Hola</span><span class="sxs-lookup"><span data-stu-id="665db-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="665db-132">**Personalizar** : se activa el modo de personalización.</span><span class="sxs-lookup"><span data-stu-id="665db-132">**Customize** – enters customize mode</span></span>

![personalizar icono](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="665db-134">Al seleccionar Personalizar, puede cambiar el tamaño de los iconos y reordenarlos.</span><span class="sxs-lookup"><span data-stu-id="665db-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="665db-135">tooresize un icono, seleccione Hola nuevo tamaño del menú contextual de hello, como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="665db-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![cambiar tamaño del icono](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="665db-137">O bien, si el icono de hello es compatible con cualquier tamaño, puede arrastrar Hola inferior derecho toohello deseado de tamaño de las esquinas.</span><span class="sxs-lookup"><span data-stu-id="665db-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![cambiar tamaño del icono](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="665db-139">Después de cambiar el tamaño de iconos, vea el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-139">After resizing tiles, view hello dashboard.</span></span>

![ver icono](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="665db-141">Una vez haya terminado de personalizar un panel, simplemente seleccione hello **realiza personalizar** tooexit en el modo personalizar o pulse el botón derecho y seleccione **realiza personalizar** desde el menú contextual de Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="665db-142">Publicación de un panel y administración del control de acceso</span><span class="sxs-lookup"><span data-stu-id="665db-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="665db-143">Cuando se crea un panel, es privado de forma predeterminada, lo que significa que es Hola única persona que pueda ver los datos.</span><span class="sxs-lookup"><span data-stu-id="665db-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="665db-144">toomake se tooothers visibles, usar hello **recurso compartido** Hola de botón que aparece junto a otros comandos de panel.</span><span class="sxs-lookup"><span data-stu-id="665db-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![compartir panel](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="665db-146">Se le preguntará toochoose en que un grupo de recursos y suscripción para su toobe panel publicado.</span><span class="sxs-lookup"><span data-stu-id="665db-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="665db-147">tooseamlessly integrar paneles en el ecosistema de hello, hemos implementado los paneles compartidos como recursos de Azure (por lo que no se puede compartir escribiendo una dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="665db-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="665db-148">Información de toohello de acceso mostrada por la mayoría de los iconos de hello en el portal de Hola se rigen por [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665db-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="665db-149">Desde una perspectiva de control de acceso, los paneles compartidos no son distintos de una máquina virtual o de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="665db-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="665db-150">Supongamos que tiene una suscripción de Azure y los miembros del equipo se han asignado los roles de Hola de **propietario**, **colaborador**, o **lector** de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="665db-151">Los usuarios que son propietarios o colaboradores son pueda toolist, ver, crear, modificar o eliminar paneles dentro de esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="665db-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="665db-152">Los usuarios que son los lectores son capaz de toolist y ver los paneles, pero no pueden modificar ni eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="665db-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="665db-153">Los usuarios con acceso de lectura son panel compartido del tooa toomake capaz de ediciones locales, pero son toopublish no se puede esos server toohello atrás de cambios.</span><span class="sxs-lookup"><span data-stu-id="665db-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="665db-154">Sin embargo, puede hacer una copia privada de panel de Hola para su propio uso.</span><span class="sxs-lookup"><span data-stu-id="665db-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="665db-155">Como siempre, iconos individuales en el panel de Hola aplican sus propias reglas de control de acceso basadas en corresponden a los recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="665db-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="665db-156">Para mayor comodidad, portal hello de la publicación guías de experiencia que hacia un patrón donde colocar paneles en un grupo de recursos denominado **paneles**.</span><span class="sxs-lookup"><span data-stu-id="665db-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![publicar panel](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="665db-158">También puede elegir toopublish un panel tooa determinado grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="665db-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="665db-159">control de acceso de Hola para ese panel coincide con el control de acceso de Hola Hola para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="665db-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="665db-160">Los usuarios que pueden administrar recursos de hello en ese grupo de recursos también tienen acceso toohello paneles.</span><span class="sxs-lookup"><span data-stu-id="665db-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![publicar panel tooresource grupo](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="665db-162">Una vez publicado el panel, Hola **compartir + acceso** se actualice y muestran información sobre el panel publicado hello, incluido un panel de toohello de acceso de usuario de vínculo toomanage panel de control.</span><span class="sxs-lookup"><span data-stu-id="665db-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="665db-163">Este vínculo inicia Hola Role Based Access Control hoja usa toomanage acceso estándar para los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="665db-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="665db-164">Puede regresar siempre toothis vista seleccionando **recurso compartido**.</span><span class="sxs-lookup"><span data-stu-id="665db-164">You can always get back toothis view by selecting **Share**.</span></span>

![administrar control de acceso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="665db-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="665db-166">Next steps</span></span>
* <span data-ttu-id="665db-167">toomanage recursos, consulte [recursos de Azure administrar a través del portal de](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="665db-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="665db-168">toodeploy recursos, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="665db-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

