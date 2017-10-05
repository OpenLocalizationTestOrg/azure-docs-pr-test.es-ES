---
title: "Personalización del portal para desarrolladores para API Management mediante plantillas - Azure| Microsoft Docs"
description: "Obtenga información sobre cómo personalizar el portal para desarrolladores para Administración de API de Azure mediante plantillas"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 40d25726d31d2018785b77d169a8811c565316bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-customize-the-azure-api-management-developer-portal-using-templates"></a><span data-ttu-id="78f67-103">Cómo personalizar el portal para desarrolladores de Administración de API de Azure mediante plantillas</span><span class="sxs-lookup"><span data-stu-id="78f67-103">How to customize the Azure API Management developer portal using templates</span></span>

<span data-ttu-id="78f67-104">Existen tres maneras fundamentales de personalizar el portal para desarrolladores en Azure API Management:</span><span class="sxs-lookup"><span data-stu-id="78f67-104">There are three fundamental ways to customize the developer portal in Azure API Management:</span></span>

* <span data-ttu-id="78f67-105">[Editar el contenido de las páginas estáticas y los elementos de diseño de página][modify-content-layout]</span><span class="sxs-lookup"><span data-stu-id="78f67-105">[Edit the contents of static pages and page layout elements][modify-content-layout]</span></span>
* <span data-ttu-id="78f67-106">[Actualizar los estilos usados para los elementos de página en el portal para desarrolladores] [ customize-styles]</span><span class="sxs-lookup"><span data-stu-id="78f67-106">[Update the styles used for page elements across the developer portal][customize-styles]</span></span>
* <span data-ttu-id="78f67-107">[Modificar las plantillas que se usan para las páginas generadas por el portal de] [ portal-templates] (que se explica en esta guía)</span><span class="sxs-lookup"><span data-stu-id="78f67-107">[Modify the templates used for pages generated by the portal][portal-templates] (explained in this guide)</span></span>

<span data-ttu-id="78f67-108">Las plantillas se usan para personalizar el contenido de las páginas del portal para desarrolladores generadas por el sistema (por ejemplo, documentos de API, productos, autenticación de usuario, etc.).</span><span class="sxs-lookup"><span data-stu-id="78f67-108">Templates are used to customize the content of system-generated developer portal pages (e.g. API docs, products, user authentication, etc.).</span></span> <span data-ttu-id="78f67-109">Mediante la sintaxis [DotLiquid](http://dotliquidmarkup.org/) y un conjunto proporcionado de recursos de cadena localizada, iconos y controles de página, dispone de una gran flexibilidad para configurar el contenido de las páginas según le convenga.</span><span class="sxs-lookup"><span data-stu-id="78f67-109">Using [DotLiquid](http://dotliquidmarkup.org/) syntax, and a provided set of localized string resources, icons, and page controls, you have great flexibility to configure the content of the pages as you see fit.</span></span>

## <a name="developer-portal-templates-overview"></a><span data-ttu-id="78f67-110">Información general sobre las plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="78f67-110">Developer portal templates overview</span></span>
<span data-ttu-id="78f67-111">La edición de las reglas de estilo se realiza en el **portal para desarrolladores** durante el inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="78f67-111">Editing templates is done from the **Developer portal** while being logged in as an administrator.</span></span> <span data-ttu-id="78f67-112">Para llegar hasta allí, primero abra Azure Portal y haga clic en **Portal para editores** en la barra de herramientas de servicios de su instancia de API Management.</span><span class="sxs-lookup"><span data-stu-id="78f67-112">To get there first open the Azure Portal and  click **Publisher portal** from the service toolbar of your API Management instance.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="78f67-114">A continuación, haga clic en **Portal para desarrolladores de** en la parte superior derecha.</span><span class="sxs-lookup"><span data-stu-id="78f67-114">Then click on **Developer portal** on the top-right.</span></span> 

![Menú del portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="78f67-116">Para acceder a las plantillas del portal para desarrolladores, haga clic en el icono de personalización de la izquierda para mostrar el menú de personalización y haga clic en **Plantillas**.</span><span class="sxs-lookup"><span data-stu-id="78f67-116">To access the developer portal templates, click the customize icon on the left to display the customization menu, and click **Templates**.</span></span>

![Plantillas del portal para desarrolladores][api-management-customize-menu]

<span data-ttu-id="78f67-118">La lista de plantillas muestra varias categorías de plantillas que abarcan las distintas páginas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="78f67-118">The templates list displays several categories of templates covering the different pages in the developer portal.</span></span> <span data-ttu-id="78f67-119">Cada plantilla es diferente, pero los pasos para editarlas y publicar los cambios son los mismos.</span><span class="sxs-lookup"><span data-stu-id="78f67-119">Each template is different, but the steps to edit them and publish the changes are the same.</span></span> <span data-ttu-id="78f67-120">Para editar una plantilla, haga clic en el nombre.</span><span class="sxs-lookup"><span data-stu-id="78f67-120">To edit a template, click the name of the template.</span></span>

![Plantillas del portal para desarrolladores][api-management-templates-menu]

<span data-ttu-id="78f67-122">Cuando hace clic en una plantilla, se abre la página del portal para desarrolladores que se puede personalizar con esa plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f67-122">Clicking a template takes you to the developer portal page that is customizable by that template.</span></span> <span data-ttu-id="78f67-123">En este ejemplo se muestra la plantilla **Lista de productos** .</span><span class="sxs-lookup"><span data-stu-id="78f67-123">In this example the **Product list** template is displayed.</span></span> <span data-ttu-id="78f67-124">La plantilla **Lista de productos** controla el área de la pantalla que se indica con un rectángulo rojo.</span><span class="sxs-lookup"><span data-stu-id="78f67-124">The **Product list** template controls the area of the screen indicated by the red rectangle.</span></span> 

![Plantilla de lista de productos][api-management-developer-portal-templates-overview]

<span data-ttu-id="78f67-126">Algunas plantillas, como las plantillas **Perfil de usuario** , personalizan partes diferentes de la misma página.</span><span class="sxs-lookup"><span data-stu-id="78f67-126">Some templates, like the **User Profile** templates, customize different parts of the same page.</span></span> 

![Plantillas de perfil de usuario][api-management-user-profile-templates]

<span data-ttu-id="78f67-128">El editor de cada plantilla del portal para desarrolladores tiene dos secciones que se muestran en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="78f67-128">The editor for each developer portal template has two sections displayed at the bottom of the page.</span></span> <span data-ttu-id="78f67-129">El lado izquierdo muestra el panel de edición de la plantilla y el lado derecho muestra el modelo de datos de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f67-129">The left-hand side displays the editing pane for the template, and the right-hand side displays the data model for the template.</span></span> 

<span data-ttu-id="78f67-130">El panel de edición de plantillas contiene el marcado que controla la apariencia y el comportamiento de la página correspondiente en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="78f67-130">The template editing pane contains the markup that controls the appearance and behavior of the corresponding page in the developer portal.</span></span> <span data-ttu-id="78f67-131">El marcado de la plantilla usa la sintaxis [DotLiquid](http://dotliquidmarkup.org/) .</span><span class="sxs-lookup"><span data-stu-id="78f67-131">The markup in the template uses the [DotLiquid](http://dotliquidmarkup.org/) syntax.</span></span> <span data-ttu-id="78f67-132">Un editor popular de DotLiquid es [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers).</span><span class="sxs-lookup"><span data-stu-id="78f67-132">One popular editor for DotLiquid is [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers).</span></span> <span data-ttu-id="78f67-133">Todos los cambios que se realizan en la plantilla durante la edición se muestran en tiempo real en el explorador, pero no son visibles para los clientes mientras no se [guarda](#to-save-a-template) y se [publica](#to-publish-a-template) la plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f67-133">Any changes made to the template during editing are displayed in real-time in the browser, but are not visible to your customers until you [save](#to-save-a-template) and [publish](#to-publish-a-template) the template.</span></span>

![Marcado de plantilla][api-management-template]

<span data-ttu-id="78f67-135">El panel **Template data** (Datos de plantilla) proporciona indicaciones sobre el modelo de datos de las entidades que están disponibles para su uso en una plantilla determinada.</span><span class="sxs-lookup"><span data-stu-id="78f67-135">The **Template data** pane provides a guide to the data model for the entities that are available for use in a particular template.</span></span> <span data-ttu-id="78f67-136">Dichas indicaciones consisten en los datos actuales que se muestran actualmente en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="78f67-136">It provides this guide by displaying the live data that are currently displayed in the developer portal.</span></span> <span data-ttu-id="78f67-137">Para expandir los paneles de plantilla, haga clic en el rectángulo de la esquina superior derecha del panel **Template data** (Datos de plantilla).</span><span class="sxs-lookup"><span data-stu-id="78f67-137">You can expand the template panes by clicking the rectangle in the upper-right corner of the **Template data** pane.</span></span>

![Modelo de datos de plantilla][api-management-template-data]

<span data-ttu-id="78f67-139">En el ejemplo anterior, se muestran en el portal para desarrolladores dos productos que se recuperaron de los datos mostrados en el panel **Template data** (Datos de plantilla), tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="78f67-139">In the previous example there are two products displayed in the developer portal that were retrieved from the data displayed in the **Template data** pane, as shown in the following example.</span></span>

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

<span data-ttu-id="78f67-140">El marcado de la plantilla **Lista de productos** procesa los datos para proporcionar el resultado deseado. Para ello, itere a través de la colección de productos para mostrar información y un vínculo a cada producto.</span><span class="sxs-lookup"><span data-stu-id="78f67-140">The markup in the **Product list** template processes the data to provide the desired output by iterating through the collection of products to display information and a link to each individual product.</span></span> <span data-ttu-id="78f67-141">Observe los elementos `<search-control>` y `<page-control>` del marcado.</span><span class="sxs-lookup"><span data-stu-id="78f67-141">Note the `<search-control>` and `<page-control>` elements in the markup.</span></span> <span data-ttu-id="78f67-142">Controlan la presentación de la búsqueda y los controles de paginación en la página.</span><span class="sxs-lookup"><span data-stu-id="78f67-142">These control the display of the searching and paging controls on the page.</span></span> <span data-ttu-id="78f67-143">`ProductsStrings|PageTitleProducts` es una referencia de cadena localizada que contiene el texto del encabezado `h2` de la página.</span><span class="sxs-lookup"><span data-stu-id="78f67-143">`ProductsStrings|PageTitleProducts` is a localized string reference that contains the `h2` header text for the page.</span></span> <span data-ttu-id="78f67-144">Para obtener una lista de recursos de cadena, controles de página e iconos disponibles para su uso en plantillas del portal para desarrolladores, consulte la [referencia de plantillas del portal para desarrolladores de API Management](api-management-developer-portal-templates-reference.md).</span><span class="sxs-lookup"><span data-stu-id="78f67-144">For a list of string resources, page controls, and icons available for use in developer portal templates, see [API Management developer portal templates reference](api-management-developer-portal-templates-reference.md).</span></span>

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="to-save-a-template"></a><span data-ttu-id="78f67-145">Para guardar una plantilla</span><span class="sxs-lookup"><span data-stu-id="78f67-145">To save a template</span></span>
<span data-ttu-id="78f67-146">Para guardar una plantilla, haga clic en guardar en el editor de plantillas.</span><span class="sxs-lookup"><span data-stu-id="78f67-146">To save a template, click save in the template editor.</span></span>

![Guardar plantilla][api-management-save-template]

<span data-ttu-id="78f67-148">Los cambios guardados no se activan en el portal para desarrolladores mientras no se publiquen.</span><span class="sxs-lookup"><span data-stu-id="78f67-148">Saved changes are not live in the developer portal until they are published.</span></span>

## <a name="to-publish-a-template"></a><span data-ttu-id="78f67-149">Para publicar una plantilla</span><span class="sxs-lookup"><span data-stu-id="78f67-149">To publish a template</span></span>
<span data-ttu-id="78f67-150">Las plantillas guardadas se pueden publicar individualmente o todas juntas.</span><span class="sxs-lookup"><span data-stu-id="78f67-150">Saved templates can be published either individually, or all together.</span></span> <span data-ttu-id="78f67-151">Para publicar una plantilla individual, haga clic en publicar en el editor de plantillas.</span><span class="sxs-lookup"><span data-stu-id="78f67-151">To publish an individual template, click publish in the template editor.</span></span>

![Publicar plantilla][api-management-publish-template]

<span data-ttu-id="78f67-153">Haga clic en **Sí** para confirmar y hacer que la plantilla se active en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="78f67-153">Click **Yes** to confirm and make the template live on the developer portal.</span></span>

![Confirmar publicación][api-management-publish-template-confirm]

<span data-ttu-id="78f67-155">Para publicar todas las versiones de plantillas actualmente sin publicar, haga clic en **Publicar** en la lista de plantillas.</span><span class="sxs-lookup"><span data-stu-id="78f67-155">To publish all currently unpublished template versions, click **Publish** in the templates list.</span></span> <span data-ttu-id="78f67-156">Las plantillas no publicadas se indican con un asterisco después del nombre de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f67-156">Unpublished templates are designated by an asterisk following the template name.</span></span> <span data-ttu-id="78f67-157">En este ejemplo, se van a publicar las plantillas **Lista de productos** y **Producto**.</span><span class="sxs-lookup"><span data-stu-id="78f67-157">In this example, the **Product list** and **Product** templates are being published.</span></span>

![Publicar plantillas][api-management-publish-templates]

<span data-ttu-id="78f67-159">Haga clic en **Publicar personalizaciones** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="78f67-159">Click **Publish customizations** to confirm.</span></span>

![Confirmar publicación][api-management-publish-customizations]

<span data-ttu-id="78f67-161">Las plantillas recién publicadas entran en vigor de inmediato en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="78f67-161">Newly published templates are effective immediately in the developer portal.</span></span>

## <a name="to-revert-a-template-to-the-previous-version"></a><span data-ttu-id="78f67-162">Para revertir una plantilla a la versión anterior</span><span class="sxs-lookup"><span data-stu-id="78f67-162">To revert a template to the previous version</span></span>
<span data-ttu-id="78f67-163">Para revertir una plantilla a la versión publicada anterior, haga clic en revertir en el editor de plantillas.</span><span class="sxs-lookup"><span data-stu-id="78f67-163">To revert a template to the previous published version, click revert in the template editor.</span></span>

![Revertir plantilla][api-management-revert-template]

<span data-ttu-id="78f67-165">Haga clic en **Sí** para continuar.</span><span class="sxs-lookup"><span data-stu-id="78f67-165">Click **Yes** to confirm.</span></span>

![Confirm][api-management-revert-template-confirm]

<span data-ttu-id="78f67-167">La versión de una plantilla publicada anteriormente estará activa en el portal para desarrolladores en cuanto se complete la operación de reversión.</span><span class="sxs-lookup"><span data-stu-id="78f67-167">The previously published version of a template is live in the developer portal once the revert operation is complete.</span></span>

## <a name="to-restore-a-template-to-the-default-version"></a><span data-ttu-id="78f67-168">Para restaurar una plantilla a la versión predeterminada</span><span class="sxs-lookup"><span data-stu-id="78f67-168">To restore a template to the default version</span></span>
<span data-ttu-id="78f67-169">La restauración de las plantillas a su versión predeterminada es un proceso que consta de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="78f67-169">Restoring templates to their default version is a two-step process.</span></span> <span data-ttu-id="78f67-170">Primero deben restaurarse las plantillas y después deben publicarse las versiones restauradas.</span><span class="sxs-lookup"><span data-stu-id="78f67-170">First the templates must be restored, and then the restored versions must be published.</span></span>

<span data-ttu-id="78f67-171">Para restaurar una sola plantilla a la versión predeterminada, haga clic en restaurar en el editor de plantillas.</span><span class="sxs-lookup"><span data-stu-id="78f67-171">To restore a single template to the default version click restore in the template editor.</span></span>

![Revertir plantilla][api-management-reset-template]

<span data-ttu-id="78f67-173">Haga clic en **Sí** para continuar.</span><span class="sxs-lookup"><span data-stu-id="78f67-173">Click **Yes** to confirm.</span></span>

![Confirm][api-management-reset-template-confirm]

<span data-ttu-id="78f67-175">Para restaurar todas las plantillas a las versiones predeterminadas, haga clic en **Restore default templates** (Restaurar plantillas predeterminadas) en la lista de plantillas.</span><span class="sxs-lookup"><span data-stu-id="78f67-175">To restore all templates to their default versions, click **Restore default templates** on the template list.</span></span>

![Restaurar plantillas][api-management-restore-templates]

<span data-ttu-id="78f67-177">Las plantillas restauradas deben publicarse individualmente o a la vez siguiendo los pasos descritos en [Para publicar una plantilla](#to-publish-a-template).</span><span class="sxs-lookup"><span data-stu-id="78f67-177">The restored templates must then be published individually or all at once by following the steps in [To publish a template](#to-publish-a-template).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78f67-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78f67-178">Next steps</span></span>
<span data-ttu-id="78f67-179">Para obtener información de referencia sobre plantillas del portal para desarrolladores, recursos de cadena, iconos y controles de página, consulte la [referencia de plantillas del portal para desarrolladores de Administración de API](api-management-developer-portal-templates-reference.md).</span><span class="sxs-lookup"><span data-stu-id="78f67-179">For reference information for developer portal templates, string resources, icons, and page controls, see [API Management developer portal templates reference](api-management-developer-portal-templates-reference.md).</span></span>

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png






