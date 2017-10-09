---
title: "plantillas de aaaProduct en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las páginas toocustomize contenido de Hola de producto de hello en el portal para desarrolladores de hello administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="3e3d4-103">Plantillas de producto en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="3e3d4-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="3e3d4-104">Administración de API de Azure proporciona que Hola contenido de hello toocustomize de capacidad de páginas del portal para desarrolladores con un conjunto de plantillas que configure su contenido.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="3e3d4-105">Usar [DotLiquid](http://dotliquidmarkup.org/) editor hello y sintaxis de su elección, como [DotLiquid a los diseñadores](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), o cambie de tamaño un conjunto proporcionado de [los recursos de cadena](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), y [página controles](api-management-page-controls.md), tienen contenido de gran flexibilidad tooconfigure Hola de páginas de Hola como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="3e3d4-106">las plantillas de Hello en esta sección permiten contenido de hello toocustomize de páginas de producto de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="3e3d4-107">Product list</span><span class="sxs-lookup"><span data-stu-id="3e3d4-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="3e3d4-108">Producto</span><span class="sxs-lookup"><span data-stu-id="3e3d4-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="3e3d4-109">Plantillas predeterminadas de ejemplo se incluyen en hello siguiendo documentación, pero están toochange asunto debido toocontinuous mejoras.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="3e3d4-110">Puede ver plantillas de hello predeterminado en vivo en el portal para desarrolladores de hello desplazándose plantillas individuales toohello deseado.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="3e3d4-111">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="3e3d4-112"><a name="ProductList"></a> Product list</span><span class="sxs-lookup"><span data-stu-id="3e3d4-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="3e3d4-113">Hola **lista de productos** plantilla permite cuerpo de hello toocustomize de página de lista de productos de hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3e3d4-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="3e3d4-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="3e3d4-115">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="3e3d4-115">Default template</span></span>  
  
```xml  
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
  
### <a name="controls"></a><span data-ttu-id="3e3d4-116">Controles</span><span class="sxs-lookup"><span data-stu-id="3e3d4-116">Controls</span></span>  
 <span data-ttu-id="3e3d4-117">Hola `Product list` plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="3e3d4-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="3e3d4-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="3e3d4-119">search-control</span><span class="sxs-lookup"><span data-stu-id="3e3d4-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="3e3d4-120">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="3e3d4-120">Data model</span></span>  
  
|<span data-ttu-id="3e3d4-121">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3e3d4-121">Property</span></span>|<span data-ttu-id="3e3d4-122">Escriba</span><span class="sxs-lookup"><span data-stu-id="3e3d4-122">Type</span></span>|<span data-ttu-id="3e3d4-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="3e3d4-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="3e3d4-124">Paginación</span><span class="sxs-lookup"><span data-stu-id="3e3d4-124">Paging</span></span>|<span data-ttu-id="3e3d4-125">Entidad [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="3e3d4-126">información de paginación de Hello para la colección de productos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="3e3d4-127">Filtros</span><span class="sxs-lookup"><span data-stu-id="3e3d4-127">Filtering</span></span>|<span data-ttu-id="3e3d4-128">Entidad [Filtering](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="3e3d4-129">Hola filtrado de información para la página lista de productos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="3e3d4-130">Productos</span><span class="sxs-lookup"><span data-stu-id="3e3d4-130">Products</span></span>|<span data-ttu-id="3e3d4-131">Colección de entidades de [producto](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="3e3d4-132">Hola productos toohello visible el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="3e3d4-133">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="3e3d4-133">Sample template data</span></span>  
  
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
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="3e3d4-134"><a name="Product"></a> Product</span><span class="sxs-lookup"><span data-stu-id="3e3d4-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="3e3d4-135">Hola **producto** plantilla permite cuerpo de hello toocustomize de página del producto hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3e3d4-136">![Página de producto del portal para desarrolladores](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="3e3d4-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="3e3d4-137">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="3e3d4-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="3e3d4-138">Controles</span><span class="sxs-lookup"><span data-stu-id="3e3d4-138">Controls</span></span>  
 <span data-ttu-id="3e3d4-139">Hola `Product list` plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="3e3d4-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="3e3d4-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="3e3d4-141">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="3e3d4-141">Data model</span></span>  
  
|<span data-ttu-id="3e3d4-142">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3e3d4-142">Property</span></span>|<span data-ttu-id="3e3d4-143">Escriba</span><span class="sxs-lookup"><span data-stu-id="3e3d4-143">Type</span></span>|<span data-ttu-id="3e3d4-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="3e3d4-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="3e3d4-145">Producto</span><span class="sxs-lookup"><span data-stu-id="3e3d4-145">Product</span></span>|[<span data-ttu-id="3e3d4-146">Producto</span><span class="sxs-lookup"><span data-stu-id="3e3d4-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="3e3d4-147">producto de Hello especificado.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-147">hello specified product.</span></span>|  
|<span data-ttu-id="3e3d4-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="3e3d4-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="3e3d4-149">boolean</span><span class="sxs-lookup"><span data-stu-id="3e3d4-149">boolean</span></span>|<span data-ttu-id="3e3d4-150">Si el usuario actual de hello es producto toothis suscrito.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="3e3d4-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="3e3d4-151">SubscriptionState</span></span>|<span data-ttu-id="3e3d4-152">número</span><span class="sxs-lookup"><span data-stu-id="3e3d4-152">number</span></span>|<span data-ttu-id="3e3d4-153">estado de Hola de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-153">hello state of hello subscription.</span></span> <span data-ttu-id="3e3d4-154">Los estados posibles son:</span><span class="sxs-lookup"><span data-stu-id="3e3d4-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="3e3d4-155">-   `0 - suspended`: Hola suscripción está bloqueada y suscriptor hello no puede llamar a las API del producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="3e3d4-156">-   `1 - active`: Hola suscripción está activa.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="3e3d4-157">-   `2 - expired`– suscripción Hola alcanza su fecha de expiración y se ha desactivado.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="3e3d4-158">-   `3 - submitted`: solicitud de suscripción de Hola se ha realizado por el desarrollador de hello, pero ha aún no aprobado o rechazados.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="3e3d4-159">-   `4 - rejected`: un administrador ha denegado la solicitud de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="3e3d4-160">-   `5 - cancelled`: se ha cancelado la suscripción Hola programador de Hola o el administrador.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="3e3d4-161">límites</span><span class="sxs-lookup"><span data-stu-id="3e3d4-161">Limits</span></span>|<span data-ttu-id="3e3d4-162">array</span><span class="sxs-lookup"><span data-stu-id="3e3d4-162">array</span></span>|<span data-ttu-id="3e3d4-163">Esta propiedad está en desuso y no debe utilizarse.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="3e3d4-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="3e3d4-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="3e3d4-165">boolean</span><span class="sxs-lookup"><span data-stu-id="3e3d4-165">boolean</span></span>|<span data-ttu-id="3e3d4-166">Si la [delegación](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está habilitada para esta suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="3e3d4-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="3e3d4-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="3e3d4-168">cadena</span><span class="sxs-lookup"><span data-stu-id="3e3d4-168">string</span></span>|<span data-ttu-id="3e3d4-169">Si se permite la delegación, Hola había delegada dirección URL de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="3e3d4-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="3e3d4-170">IsAgreed</span></span>|<span data-ttu-id="3e3d4-171">boolean</span><span class="sxs-lookup"><span data-stu-id="3e3d4-171">boolean</span></span>|<span data-ttu-id="3e3d4-172">Si el producto de hello tiene términos, si ha acordado usuario actual de hello toohello términos.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="3e3d4-173">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="3e3d4-173">Subscriptions</span></span>|<span data-ttu-id="3e3d4-174">Colección de entidades de [resumen de suscripción](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="3e3d4-175">producto de toohello de Hello las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="3e3d4-176">Apis</span><span class="sxs-lookup"><span data-stu-id="3e3d4-176">Apis</span></span>|<span data-ttu-id="3e3d4-177">Colección de entidades [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="3e3d4-178">Hola API en este producto.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="3e3d4-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="3e3d4-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="3e3d4-180">boolean</span><span class="sxs-lookup"><span data-stu-id="3e3d4-180">boolean</span></span>|<span data-ttu-id="3e3d4-181">Si el usuario actual de hello es elegible toosubscribe toothis producto con un límite de suscripción toohello de tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="3e3d4-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="3e3d4-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="3e3d4-183">boolean</span><span class="sxs-lookup"><span data-stu-id="3e3d4-183">boolean</span></span>|<span data-ttu-id="3e3d4-184">Si el usuario actual de hello es elegible toosubscribe toothis producto con suscripciones de toomultiple de tener en cuenta que se permiten o no.</span><span class="sxs-lookup"><span data-stu-id="3e3d4-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="3e3d4-185">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="3e3d4-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="3e3d4-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e3d4-186">Next steps</span></span>
<span data-ttu-id="3e3d4-187">Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3e3d4-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
