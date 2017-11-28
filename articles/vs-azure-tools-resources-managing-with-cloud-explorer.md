---
title: "Administración de recursos de Azure con Cloud Explorer | Microsoft Docs"
description: "Obtenga más información sobre cómo usar Cloud Explorer para examinar y administrar recursos de Azure en Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="9b96c-103">Administración de los recursos asociados con las cuentas de Azure en Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9b96c-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="9b96c-104">Cloud Explorer le permite consultar sus recursos y grupos de recursos de Azure, inspeccionar sus propiedades y realizar acciones de diagnóstico de desarrollador clave desde dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b96c-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="9b96c-105">Del mismo modo que [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer se basa en la pila de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b96c-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="9b96c-106">Por lo tanto, Cloud Explorer entiende de recursos como, grupos de recursos de Azure, y de servicios de Azure, como aplicaciones lógicas y aplicaciones de API. Además, admite [control de acceso basado en rol](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="9b96c-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9b96c-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b96c-107">Prerequisites</span></span>
- <span data-ttu-id="9b96c-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) con la **carga de trabajo de Azure** seleccionada o una versión anterior de Visual Studio con [Microsoft Azure SDK para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="9b96c-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="9b96c-109">Cuenta de Microsoft Azure: si todavía no tiene ninguna cuenta, puede [registrarse para una evaluación gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) o [activar las ventajas de suscriptor de Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="9b96c-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="9b96c-110">Para ver Cloud Explorer, seleccione **Ver** > **Cloud Explorer** en la barra de menús.</span><span class="sxs-lookup"><span data-stu-id="9b96c-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="9b96c-111">Incorporación de una cuenta de Azure en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9b96c-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="9b96c-112">Para consultar los recursos asociados con una cuenta de Azure, primero debe agregarla a Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9b96c-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="9b96c-113">En **Cloud Explorer**, seleccione **Configuración de la cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="9b96c-115">Seleccione **Agregar nueva cuenta**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-115">Select **Add new account**.</span></span> 

    ![Vínculo para agregar cuenta en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="9b96c-117">Inicie sesión en la cuenta de Azure cuyos recursos desea examinar.</span><span class="sxs-lookup"><span data-stu-id="9b96c-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="9b96c-118">Una vez que inicie sesión en una cuenta de Azure, se muestran las suscripciones asociadas con esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="9b96c-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="9b96c-119">Active las casillas de las suscripciones de cuenta que desea examinar y, luego, seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: seleccione las suscripciones de Azure que se van a mostrar](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="9b96c-121">Después de seleccionar las suscripciones cuyos recursos desea examinar, tanto las suscripciones como los recursos aparecerán en Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9b96c-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Listado de recursos de Cloud Explorer para una cuenta de Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="9b96c-123">Eliminación de una cuenta de Azure de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9b96c-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="9b96c-124">En **Cloud Explorer**, seleccione **Configuración de la cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="9b96c-126">Seleccione **Quitar** junto a la cuenta que desea quitar.</span><span class="sxs-lookup"><span data-stu-id="9b96c-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="9b96c-128">Vista de tipos de recursos o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="9b96c-128">View resource types or resource groups</span></span>
<span data-ttu-id="9b96c-129">Para ver los recursos de Azure, puede elegir la vista **Tipos de recursos** o **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="9b96c-130">En **Cloud Explorer**, seleccione la lista desplegable de vistas de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b96c-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![Lista desplegable de Cloud Explorer para seleccionar la vista de recursos deseada](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="9b96c-132">En el menú contextual, seleccione la vista deseada:</span><span class="sxs-lookup"><span data-stu-id="9b96c-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="9b96c-133">Vista **Tipos de recursos**: la vista común que se usa en [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040). Muestra los recursos de Azure clasificados según su tipo, como aplicaciones web, cuentas de almacenamiento y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9b96c-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="9b96c-134">Vista **Grupos de recursos**: clasifica los recursos de Azure según el grupo de recursos de Azure al que están asociados.</span><span class="sxs-lookup"><span data-stu-id="9b96c-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="9b96c-135">Un grupo de recursos es una agrupación de recursos de Azure, normalmente usados por una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="9b96c-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="9b96c-136">Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b96c-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="9b96c-137">La imagen siguiente muestra una comparación de ambas vistas de recursos:</span><span class="sxs-lookup"><span data-stu-id="9b96c-137">The following image shows a comparison of the two resource views:</span></span>

    ![Comparación de las vistas de recursos de Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="9b96c-139">Visualización y navegación por los recursos en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9b96c-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="9b96c-140">Para navegar a un recurso de Azure y consultar su información en Cloud Explorer, expanda el tipo del elemento o el grupo de recursos asociado y, luego, seleccione el recurso.</span><span class="sxs-lookup"><span data-stu-id="9b96c-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="9b96c-141">Cuando selecciona un recurso, aparece información en las dos pestañas, **Acciones** y **Propiedades**, que se encuentran en la parte inferior de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9b96c-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="9b96c-142">Pestaña **Acciones**: muestra las acciones que puede realizar en Cloud Explorer con el recurso seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9b96c-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="9b96c-143">También puede ver estas opciones si hace clic con el botón derecho en el recurso para ver el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="9b96c-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="9b96c-144">Pestaña **Propiedades**: muestra las propiedades del recurso, como su tipo, configuración local y grupo de recursos al que está asociado.</span><span class="sxs-lookup"><span data-stu-id="9b96c-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="9b96c-145">La imagen siguiente muestra un ejemplo de comparación de lo que ve en cada pestaña para una instancia de App Service:</span><span class="sxs-lookup"><span data-stu-id="9b96c-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="9b96c-146">Cada recurso tiene la acción **Abrir en el portal**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="9b96c-147">Cuando se selecciona esta acción, Cloud Explorer muestra el recurso seleccionado en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9b96c-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="9b96c-148">La característica **Abrir en el portal** es especialmente útil para navegar a los recursos profundamente anidados.</span><span class="sxs-lookup"><span data-stu-id="9b96c-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="9b96c-149">También pueden aparecer acciones adicionales y valores de propiedad basados en el recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b96c-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="9b96c-150">Por ejemplo, las aplicaciones web y lógicas también tienen las acciones **Abrir en el explorador** y **Adjuntar depurador**, además de **Abrir en el portal**.</span><span class="sxs-lookup"><span data-stu-id="9b96c-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="9b96c-151">Cuando se elige un blob, una cola o una tabla de cuenta de almacenamiento, aparecen acciones para abrir editores.</span><span class="sxs-lookup"><span data-stu-id="9b96c-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="9b96c-152">Las aplicaciones de Azure tienen las propiedades **URL** y **Status**, mientras que los recursos de almacenamiento tienen propiedades de cadena de conexión y de clave.</span><span class="sxs-lookup"><span data-stu-id="9b96c-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="9b96c-153">Búsqueda de recursos en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9b96c-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="9b96c-154">Para buscar recursos con un nombre específico en las suscripciones de cuenta de Azure, escriba el nombre en el cuadro de **búsqueda** en Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9b96c-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![Buscar recursos en Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="9b96c-156">A medida que escribe caracteres en el cuadro de **búsqueda**, solo los recursos que coinciden con los caracteres aparecen en el árbol de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b96c-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
