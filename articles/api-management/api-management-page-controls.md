---
title: "Controles de página de Azure API Management | Microsoft Docs"
description: "Aprenda sobre los controles de página disponibles para su uso en las plantillas del portal para desarrolladores de Azure API Management."
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
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="792a3-103">Controles de página de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="792a3-103">Azure API Management page controls</span></span>
<span data-ttu-id="792a3-104">Azure API Management proporciona los siguientes controles para su uso en las plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="792a3-105">Para usar un control, colóquelo en la ubicación deseada en la plantilla del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="792a3-106">Algunos controles, como el control [app-actions](#app-actions), tienen parámetros, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="792a3-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="792a3-107">Los valores de los parámetros se pasan como parte del modelo de datos de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="792a3-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="792a3-108">En la mayoría de los casos, puede pegarlos simplemente en el ejemplo proporcionado para cada control para que funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="792a3-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="792a3-109">Para más información sobre los valores de parámetros, puede ver la sección del modelo de datos de cada plantilla en la que se puede usar un control.</span><span class="sxs-lookup"><span data-stu-id="792a3-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="792a3-110">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="792a3-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="792a3-111">Controles de página de las plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="792a3-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="792a3-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="792a3-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="792a3-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="792a3-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="792a3-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="792a3-115">providers</span><span class="sxs-lookup"><span data-stu-id="792a3-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="792a3-116">search-control</span><span class="sxs-lookup"><span data-stu-id="792a3-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="792a3-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="792a3-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="792a3-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="792a3-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="792a3-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="792a3-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="792a3-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="792a3-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="792a3-121">El control `app-actions` proporciona una interfaz de usuario para la interacción con aplicaciones en la página del perfil de usuario del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="792a3-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "Control app-actions de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-123">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-124">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-124">Parameters</span></span>  
  
|<span data-ttu-id="792a3-125">Parámetro</span><span class="sxs-lookup"><span data-stu-id="792a3-125">Parameter</span></span>|<span data-ttu-id="792a3-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="792a3-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="792a3-127">appId</span><span class="sxs-lookup"><span data-stu-id="792a3-127">appId</span></span>|<span data-ttu-id="792a3-128">Identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="792a3-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-129">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-129">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-130">El control `app-actions` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-131">Applications</span><span class="sxs-lookup"><span data-stu-id="792a3-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="792a3-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="792a3-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="792a3-133">El control `basic-signin` ofrece un control para la recolección de información de inicio de sesión del usuario en la página de inicio de sesión del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="792a3-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "Control basic-signin de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-135">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-136">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-136">Parameters</span></span>  
 <span data-ttu-id="792a3-137">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="792a3-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-138">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-138">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-139">El control `basic-signin` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-140">Sign in</span><span class="sxs-lookup"><span data-stu-id="792a3-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="792a3-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="792a3-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="792a3-142">El control `paging-control` proporciona funcionalidad de paginación en las páginas del portal para desarrolladores que muestran una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="792a3-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="792a3-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "Paging control de APIM ")</span><span class="sxs-lookup"><span data-stu-id="792a3-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-144">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-145">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-145">Parameters</span></span>  
 <span data-ttu-id="792a3-146">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="792a3-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-147">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-147">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-148">El control `paging-control` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-149">API list</span><span class="sxs-lookup"><span data-stu-id="792a3-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="792a3-150">Issue list</span><span class="sxs-lookup"><span data-stu-id="792a3-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="792a3-151">Product list</span><span class="sxs-lookup"><span data-stu-id="792a3-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="792a3-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="792a3-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="792a3-153">El control `providers` proporciona un control para la selección de proveedores de autenticación en la página de inicio de sesión del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="792a3-154">![control providers](./media/api-management-page-controls/APIM-providers-control.png "Control providers de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-155">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-156">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-156">Parameters</span></span>  
 <span data-ttu-id="792a3-157">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="792a3-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-158">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-158">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-159">El control `providers` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-160">Sign in</span><span class="sxs-lookup"><span data-stu-id="792a3-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="792a3-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="792a3-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="792a3-162">El control `search-control` proporciona funcionalidad de búsqueda en las páginas del portal para desarrolladores que muestran una lista de elementos.</span><span class="sxs-lookup"><span data-stu-id="792a3-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="792a3-163">![search control](./media/api-management-page-controls/APIM-search-control.png "Search control de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-164">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-165">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-165">Parameters</span></span>  
 <span data-ttu-id="792a3-166">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="792a3-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-167">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-167">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-168">El control `search-control` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-169">API list</span><span class="sxs-lookup"><span data-stu-id="792a3-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="792a3-170">Product list</span><span class="sxs-lookup"><span data-stu-id="792a3-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="792a3-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="792a3-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="792a3-172">El control `sign-up` proporciona un control para la recolección de información de perfil de usuario en la página de inicio de sesión del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="792a3-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "Sign-up control de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-174">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-175">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-175">Parameters</span></span>  
 <span data-ttu-id="792a3-176">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="792a3-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-177">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-177">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-178">El control `sign-up` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-179">Sign up</span><span class="sxs-lookup"><span data-stu-id="792a3-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="792a3-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="792a3-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="792a3-181">El control `subscribe-button` proporciona un control para la suscripción de un usuario a un producto.</span><span class="sxs-lookup"><span data-stu-id="792a3-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="792a3-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "Control subscribe-button de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-183">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-184">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-184">Parameters</span></span>  
 <span data-ttu-id="792a3-185">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="792a3-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-186">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-186">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-187">El control `subscribe-button` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-188">Producto</span><span class="sxs-lookup"><span data-stu-id="792a3-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="792a3-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="792a3-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="792a3-190">El control `subscription-cancel` proporciona un control para la cancelación de una suscripción a un producto en la página de perfil de usuario del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="792a3-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Control subscription-cancel de APIM")</span><span class="sxs-lookup"><span data-stu-id="792a3-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="792a3-192">Uso</span><span class="sxs-lookup"><span data-stu-id="792a3-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="792a3-193">parameters</span><span class="sxs-lookup"><span data-stu-id="792a3-193">Parameters</span></span>  
  
|<span data-ttu-id="792a3-194">Parámetro</span><span class="sxs-lookup"><span data-stu-id="792a3-194">Parameter</span></span>|<span data-ttu-id="792a3-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="792a3-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="792a3-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="792a3-196">subscriptionId</span></span>|<span data-ttu-id="792a3-197">Identificador de la suscripción para cancelar.</span><span class="sxs-lookup"><span data-stu-id="792a3-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="792a3-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="792a3-198">cancelUrl</span></span>|<span data-ttu-id="792a3-199">Dirección URL de cancelación de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="792a3-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="792a3-200">Plantillas del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="792a3-200">Developer portal templates</span></span>  
 <span data-ttu-id="792a3-201">El control `subscription-cancel` se puede usar en las siguientes plantillas del portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="792a3-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="792a3-202">Producto</span><span class="sxs-lookup"><span data-stu-id="792a3-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="792a3-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="792a3-203">Next steps</span></span>
<span data-ttu-id="792a3-204">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="792a3-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>