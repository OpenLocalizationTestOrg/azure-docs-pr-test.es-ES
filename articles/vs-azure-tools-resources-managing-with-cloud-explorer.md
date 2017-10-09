---
title: aaaManaging Azure recursos con el Explorador de la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse toobrowse de explorador en la nube y administrar recursos de Azure en Visual Studio."
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
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="f502c-103">Administrar los recursos de hello asociados con sus cuentas de Azure en el Explorador de Visual Studio en la nube</span><span class="sxs-lookup"><span data-stu-id="f502c-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="f502c-104">Explorador de nube permite tooview los recursos de Azure y grupos de recursos, inspeccionar sus propiedades y realizar acciones de diagnóstico para desarrolladores clave desde dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f502c-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="f502c-105">Al igual que hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), el explorador en la nube se basa en la pila de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f502c-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="f502c-106">Por lo tanto, Cloud Explorer entiende de recursos como, grupos de recursos de Azure, y de servicios de Azure, como aplicaciones lógicas y aplicaciones de API. Además, admite [control de acceso basado en rol](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="f502c-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f502c-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f502c-107">Prerequisites</span></span>
- <span data-ttu-id="f502c-108">[Visual Studio de 2017](https://www.visualstudio.com/downloads/) con hello **cargas de trabajo de Azure** seleccionado, o una versión anterior de Visual Studio con hello [Microsoft Azure SDK para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="f502c-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="f502c-109">Cuenta de Microsoft Azure: si todavía no tiene ninguna cuenta, puede [registrarse para una evaluación gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) o [activar las ventajas de suscriptor de Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="f502c-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="f502c-110">tooview el explorador en la nube, seleccione **vista** > **Explorer nube** en la barra de menús de Hola.</span><span class="sxs-lookup"><span data-stu-id="f502c-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="f502c-111">Agregar un explorador tooCloud de cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="f502c-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="f502c-112">recursos de hello tooview asociados con una cuenta de Azure, primero debe agregar cuenta de hello tooCloud explorador.</span><span class="sxs-lookup"><span data-stu-id="f502c-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="f502c-113">En **Cloud Explorer**, seleccione **Configuración de la cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="f502c-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="f502c-115">Seleccione **Agregar nueva cuenta**.</span><span class="sxs-lookup"><span data-stu-id="f502c-115">Select **Add new account**.</span></span> 

    ![Vínculo para agregar cuenta en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="f502c-117">Inicie sesión en la cuenta de Azure cuyos recursos desea toohello toobrowse.</span><span class="sxs-lookup"><span data-stu-id="f502c-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="f502c-118">Una vez iniciada la sesión tooan cuenta de Azure, se muestran las suscripciones de hello asociadas con esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="f502c-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="f502c-119">Seleccione Hola casillas de verificación de las suscripciones de cuenta de hello que desee toobrowse y, a continuación, seleccione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="f502c-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Explorador de nube: seleccione toodisplay de las suscripciones de Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="f502c-121">Después de seleccionar las suscripciones de hello cuyos recursos desea toobrowse, las suscripciones y los recursos se muestran en hello explorador en la nube.</span><span class="sxs-lookup"><span data-stu-id="f502c-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Listado de recursos de Cloud Explorer para una cuenta de Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="f502c-123">Eliminación de una cuenta de Azure de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f502c-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="f502c-124">En **Cloud Explorer**, seleccione **Configuración de la cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="f502c-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="f502c-126">Seleccione la siguiente cuenta de toohello desea tooremove, **quitar**.</span><span class="sxs-lookup"><span data-stu-id="f502c-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Icono de configuración de la cuenta de Azure en Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="f502c-128">Vista de tipos de recursos o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="f502c-128">View resource types or resource groups</span></span>
<span data-ttu-id="f502c-129">tooview los recursos de Azure, puede elegir cualquiera **tipos de recursos** o **grupos de recursos** vista.</span><span class="sxs-lookup"><span data-stu-id="f502c-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="f502c-130">En **nube explorador**, seleccione Hola lista desplegable de vista de recursos.</span><span class="sxs-lookup"><span data-stu-id="f502c-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Lista desplegable lista tooselect Hola deseado recursos del explorador de la nube](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="f502c-132">En menú contextual de hello, seleccione Vista de hello deseado:</span><span class="sxs-lookup"><span data-stu-id="f502c-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="f502c-133">**Tipos de recursos** vista - Hola común usado en hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), muestra los recursos de Azure que se clasifican por su tipo, como las aplicaciones web, las cuentas de almacenamiento y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f502c-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="f502c-134">**Grupos de recursos** ver - los recursos de Azure clasifica por grupo de recursos de Azure Hola con el que está asociados.</span><span class="sxs-lookup"><span data-stu-id="f502c-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="f502c-135">Un grupo de recursos es una agrupación de recursos de Azure, normalmente usados por una aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="f502c-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="f502c-136">toolearn más información acerca de los grupos de recursos de Azure, consulte [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f502c-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="f502c-137">Hello siguiente imagen muestra una comparación de hello dos vistas de recursos:</span><span class="sxs-lookup"><span data-stu-id="f502c-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Comparación de las vistas de recursos de Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="f502c-139">Visualización y navegación por los recursos en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f502c-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="f502c-140">toonavigate tooan recursos de Azure y ver su información en el Explorador de la nube, expanda el tipo del elemento de Hola o el grupo de recursos asociados y, a continuación, seleccione el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="f502c-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="f502c-141">Cuando seleccione un recurso, información aparece en las pestañas de hello dos - **acciones** y **propiedades** : en la parte inferior de hello del explorador de la nube.</span><span class="sxs-lookup"><span data-stu-id="f502c-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="f502c-142">**Acciones** pestaña - acciones de Hola de listas que puede realizar en el explorador en la nube para el recurso de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="f502c-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="f502c-143">También puede ver estas opciones con el botón secundario Hola recursos tooview su menú contextual.</span><span class="sxs-lookup"><span data-stu-id="f502c-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="f502c-144">**Propiedades** ficha - Propiedades de Hola de muestra del recurso de hello, como su tipo, configuración regional, grupo de recursos al que está asociado.</span><span class="sxs-lookup"><span data-stu-id="f502c-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="f502c-145">Hello siguiente imagen muestra una comparación de ejemplo de lo que ve en cada pestaña para un servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="f502c-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="f502c-146">Cada recurso tiene la acción de hello **abrir en el portal**.</span><span class="sxs-lookup"><span data-stu-id="f502c-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="f502c-147">Si elige esta acción, el Explorador de nube muestra recursos Hola seleccionado en hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f502c-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="f502c-148">Hola **abrir en el portal** característica resulta práctica para navegar por los recursos de toodeeply anidado.</span><span class="sxs-lookup"><span data-stu-id="f502c-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="f502c-149">Acciones adicionales y los valores de propiedad también pueden aparecer en función de hello recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f502c-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="f502c-150">Por ejemplo, las aplicaciones web y aplicaciones lógicas también tienen acciones de hello **abrir en el explorador** y **adjuntar depurador** además demasiado**abrir en el portal**.</span><span class="sxs-lookup"><span data-stu-id="f502c-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="f502c-151">Editores de tooopen acciones aparecen cuando se elige un blob de la cuenta de almacenamiento, una cola o una tabla.</span><span class="sxs-lookup"><span data-stu-id="f502c-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="f502c-152">Las aplicaciones de Azure tienen las propiedades **URL** y **Status**, mientras que los recursos de almacenamiento tienen propiedades de cadena de conexión y de clave.</span><span class="sxs-lookup"><span data-stu-id="f502c-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="f502c-153">Búsqueda de recursos en Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f502c-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="f502c-154">recursos de toolocate con un nombre específico en las suscripciones de cuenta de Azure, escriba el nombre de Hola Hola **búsqueda** cuadro en el explorador en la nube.</span><span class="sxs-lookup"><span data-stu-id="f502c-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Buscar recursos en Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="f502c-156">Cuando se escriben caracteres en hello **búsqueda** cuadro, solo los recursos que coinciden con los caracteres aparecen en el árbol de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f502c-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
