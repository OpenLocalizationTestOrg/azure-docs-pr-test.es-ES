---
title: "controles de página de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de los controles de página de hello disponibles para su uso en plantillas del portal de desarrollador en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="1e068-103">Controles de página de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1e068-103">Azure API Management page controls</span></span>
<span data-ttu-id="1e068-104">Administración de API de Azure proporciona Hola siguientes controles para su uso en plantillas del portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="1e068-105">toouse un control, póngalo en ubicación de hello deseado en la plantilla del portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="1e068-106">Algunos controles, como hello [aplicación acciones](#app-actions) controlar, tienen parámetros, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="1e068-107">valores de Hello para parámetros de Hola se pasan como parte del modelo de datos de hello para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="1e068-108">En la mayoría de los casos, simplemente puede pegar en hello previstas ejemplo para cada control se toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="1e068-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="1e068-109">Para obtener más información sobre los valores de parámetro hello, puede ver la sección de modelo de datos de Hola para cada plantilla en la que se utiliza un control.</span><span class="sxs-lookup"><span data-stu-id="1e068-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="1e068-110">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="1e068-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="1e068-111">Controles de página de las plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="1e068-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="1e068-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="1e068-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="1e068-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="1e068-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="1e068-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="1e068-115">providers</span><span class="sxs-lookup"><span data-stu-id="1e068-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="1e068-116">search-control</span><span class="sxs-lookup"><span data-stu-id="1e068-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="1e068-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="1e068-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="1e068-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="1e068-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="1e068-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="1e068-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="1e068-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="1e068-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="1e068-121">Hola `app-actions` control proporciona una interfaz de usuario para interactuar con las aplicaciones en la página de perfil de usuario de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1e068-122">![app&amp;#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "Control app-actions de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-123">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-124">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-124">Parameters</span></span>  
  
|<span data-ttu-id="1e068-125">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1e068-125">Parameter</span></span>|<span data-ttu-id="1e068-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e068-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1e068-127">appId</span><span class="sxs-lookup"><span data-stu-id="1e068-127">appId</span></span>|<span data-ttu-id="1e068-128">Hola Id. de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1e068-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-129">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-129">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-130">Hola `app-actions` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-131">Applications</span><span class="sxs-lookup"><span data-stu-id="1e068-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="1e068-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="1e068-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="1e068-133">Hola `basic-signin` control proporciona un control de inicio de sesión de usuario recopilar información en hello iniciar sesión en la página de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1e068-134">![basic&amp;#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "Control basic-signin de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-135">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-136">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-136">Parameters</span></span>  
 <span data-ttu-id="1e068-137">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1e068-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-138">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-138">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-139">Hola `basic-signin` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-140">Sign in</span><span class="sxs-lookup"><span data-stu-id="1e068-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="1e068-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="1e068-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="1e068-142">Hola `paging-control` proporciona funcionalidad de paginación en developer páginas del portal que muestran una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="1e068-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="1e068-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "Paging control de APIM ")</span><span class="sxs-lookup"><span data-stu-id="1e068-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-144">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-145">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-145">Parameters</span></span>  
 <span data-ttu-id="1e068-146">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1e068-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-147">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-147">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-148">Hola `paging-control` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-149">API list</span><span class="sxs-lookup"><span data-stu-id="1e068-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="1e068-150">Issue list</span><span class="sxs-lookup"><span data-stu-id="1e068-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="1e068-151">Product list</span><span class="sxs-lookup"><span data-stu-id="1e068-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="1e068-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="1e068-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="1e068-153">Hola `providers` control proporciona un control para la selección de proveedores de autenticación de inicio de sesión de hello en la página de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1e068-154">![control providers](./media/api-management-page-controls/APIM-providers-control.png "Control providers de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-155">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-156">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-156">Parameters</span></span>  
 <span data-ttu-id="1e068-157">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1e068-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-158">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-158">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-159">Hola `providers` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-160">Sign in</span><span class="sxs-lookup"><span data-stu-id="1e068-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="1e068-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="1e068-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="1e068-162">Hola `search-control` proporciona funcionalidad de búsqueda en developer páginas del portal que muestran una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="1e068-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="1e068-163">![search control](./media/api-management-page-controls/APIM-search-control.png "Search control de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-164">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-165">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-165">Parameters</span></span>  
 <span data-ttu-id="1e068-166">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1e068-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-167">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-167">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-168">Hola `search-control` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-169">API list</span><span class="sxs-lookup"><span data-stu-id="1e068-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="1e068-170">Product list</span><span class="sxs-lookup"><span data-stu-id="1e068-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="1e068-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="1e068-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="1e068-172">Hola `sign-up` control proporciona un control para recopilar información de perfil de usuario en la página de portal para desarrolladores de Hola de registro Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1e068-173">![sign&amp;#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "Sign-up control de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-174">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-175">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-175">Parameters</span></span>  
 <span data-ttu-id="1e068-176">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1e068-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-177">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-177">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-178">Hola `sign-up` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-179">Sign up</span><span class="sxs-lookup"><span data-stu-id="1e068-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="1e068-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="1e068-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="1e068-181">Hola `subscribe-button` proporciona un control para suscribirse a un producto de tooa de usuario.</span><span class="sxs-lookup"><span data-stu-id="1e068-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="1e068-182">![subscribe&amp;#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "Control subscribe-button de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-183">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-184">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-184">Parameters</span></span>  
 <span data-ttu-id="1e068-185">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="1e068-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-186">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-186">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-187">Hola `subscribe-button` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-188">Producto</span><span class="sxs-lookup"><span data-stu-id="1e068-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="1e068-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="1e068-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="1e068-190">Hola `subscription-cancel` control proporciona un control para cancelar un producto de tooa de suscripción en la página de perfil de usuario de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e068-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1e068-191">![subscription&amp;#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Control subscription-cancel de APIM")</span><span class="sxs-lookup"><span data-stu-id="1e068-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1e068-192">Uso</span><span class="sxs-lookup"><span data-stu-id="1e068-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="1e068-193">parameters</span><span class="sxs-lookup"><span data-stu-id="1e068-193">Parameters</span></span>  
  
|<span data-ttu-id="1e068-194">Parámetro</span><span class="sxs-lookup"><span data-stu-id="1e068-194">Parameter</span></span>|<span data-ttu-id="1e068-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="1e068-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1e068-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="1e068-196">subscriptionId</span></span>|<span data-ttu-id="1e068-197">Id. de Hola de hello toocancel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e068-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="1e068-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="1e068-198">cancelUrl</span></span>|<span data-ttu-id="1e068-199">suscripción de Hello cancelar la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1e068-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="1e068-200">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1e068-200">Developer portal templates</span></span>  
 <span data-ttu-id="1e068-201">Hola `subscription-cancel` control puede usarse en hello siguiendo las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="1e068-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="1e068-202">Producto</span><span class="sxs-lookup"><span data-stu-id="1e068-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="1e068-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e068-203">Next steps</span></span>
<span data-ttu-id="1e068-204">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1e068-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
