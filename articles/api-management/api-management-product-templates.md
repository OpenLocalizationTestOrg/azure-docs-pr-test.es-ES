---
title: Plantillas de producto de Azure API Management | Microsoft Docs
description: "Aprenda a personalizar el contenido de las páginas de producto en el portal para desarrolladores de Azure API Management."
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
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="ef3f8-103">Plantillas de producto en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ef3f8-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="ef3f8-104">Azure API Management le ofrece la posibilidad de personalizar el contenido de las páginas del portal para desarrolladores mediante un conjunto de plantillas que configuran su contenido.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="ef3f8-105">Por medio de la sintaxis [DotLiquid](http://dotliquidmarkup.org/) y el editor que prefiera, como [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) (DotLiquid para diseñadores), y un conjunto proporcionado de [recursos de cadena](api-management-template-resources.md#strings), [recursos de glifo](api-management-template-resources.md#glyphs) y [controles de página](api-management-page-controls.md) localizados, puede disponer de una gran flexibilidad para configurar el contenido de las páginas como considere oportuno mediante estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="ef3f8-106">Las plantillas de esta sección le permiten personalizar el contenido de las páginas de producto en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="ef3f8-107">Product list</span><span class="sxs-lookup"><span data-stu-id="ef3f8-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="ef3f8-108">Producto</span><span class="sxs-lookup"><span data-stu-id="ef3f8-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="ef3f8-109">En la siguiente documentación se incluyen plantillas predeterminadas de ejemplo; sin embargo, están sujetas a cambios debido a mejoras continuas.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="ef3f8-110">Puede ver las plantillas predeterminadas en vivo en el portal para desarrolladores; para ello, vaya hasta a las plantillas individuales que desee.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="ef3f8-111">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="ef3f8-112"><a name="ProductList"></a> Product list</span><span class="sxs-lookup"><span data-stu-id="ef3f8-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="ef3f8-113">La plantilla **Product list** le permite personalizar el cuerpo de la página de lista de productos en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="ef3f8-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="ef3f8-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ef3f8-115">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="ef3f8-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ef3f8-116">Controles</span><span class="sxs-lookup"><span data-stu-id="ef3f8-116">Controls</span></span>  
 <span data-ttu-id="ef3f8-117">La plantilla `Product list` puede usar los siguientes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ef3f8-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="ef3f8-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="ef3f8-119">search-control</span><span class="sxs-lookup"><span data-stu-id="ef3f8-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="ef3f8-120">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="ef3f8-120">Data model</span></span>  
  
|<span data-ttu-id="ef3f8-121">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ef3f8-121">Property</span></span>|<span data-ttu-id="ef3f8-122">Escriba</span><span class="sxs-lookup"><span data-stu-id="ef3f8-122">Type</span></span>|<span data-ttu-id="ef3f8-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef3f8-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ef3f8-124">Paginación</span><span class="sxs-lookup"><span data-stu-id="ef3f8-124">Paging</span></span>|<span data-ttu-id="ef3f8-125">Entidad [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="ef3f8-126">La información de paginación de la colección de productos.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="ef3f8-127">Filtros</span><span class="sxs-lookup"><span data-stu-id="ef3f8-127">Filtering</span></span>|<span data-ttu-id="ef3f8-128">Entidad [Filtering](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="ef3f8-129">La información de filtrado de la página de lista de productos.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="ef3f8-130">Productos</span><span class="sxs-lookup"><span data-stu-id="ef3f8-130">Products</span></span>|<span data-ttu-id="ef3f8-131">Colección de entidades de [producto](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="ef3f8-132">Los productos visibles para el usuario actual.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ef3f8-133">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="ef3f8-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
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
  
##  <span data-ttu-id="ef3f8-134"><a name="Product"></a> Product</span><span class="sxs-lookup"><span data-stu-id="ef3f8-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="ef3f8-135">La plantilla **Product list** le permite personalizar el cuerpo de la página de producto en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="ef3f8-136">![Página de producto del portal para desarrolladores](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="ef3f8-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ef3f8-137">Plantilla predeterminada</span><span class="sxs-lookup"><span data-stu-id="ef3f8-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ef3f8-138">Controles</span><span class="sxs-lookup"><span data-stu-id="ef3f8-138">Controls</span></span>  
 <span data-ttu-id="ef3f8-139">La plantilla `Product list` puede usar los siguientes [controles de página](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ef3f8-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="ef3f8-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="ef3f8-141">Modelo de datos</span><span class="sxs-lookup"><span data-stu-id="ef3f8-141">Data model</span></span>  
  
|<span data-ttu-id="ef3f8-142">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ef3f8-142">Property</span></span>|<span data-ttu-id="ef3f8-143">Escriba</span><span class="sxs-lookup"><span data-stu-id="ef3f8-143">Type</span></span>|<span data-ttu-id="ef3f8-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="ef3f8-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ef3f8-145">Producto</span><span class="sxs-lookup"><span data-stu-id="ef3f8-145">Product</span></span>|[<span data-ttu-id="ef3f8-146">Producto</span><span class="sxs-lookup"><span data-stu-id="ef3f8-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="ef3f8-147">El producto especificado.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-147">The specified product.</span></span>|  
|<span data-ttu-id="ef3f8-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="ef3f8-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="ef3f8-149">boolean</span><span class="sxs-lookup"><span data-stu-id="ef3f8-149">boolean</span></span>|<span data-ttu-id="ef3f8-150">Si el usuario actual está suscrito a este producto.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="ef3f8-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="ef3f8-151">SubscriptionState</span></span>|<span data-ttu-id="ef3f8-152">número</span><span class="sxs-lookup"><span data-stu-id="ef3f8-152">number</span></span>|<span data-ttu-id="ef3f8-153">El estado de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-153">The state of the subscription.</span></span> <span data-ttu-id="ef3f8-154">Los estados posibles son:</span><span class="sxs-lookup"><span data-stu-id="ef3f8-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="ef3f8-155">-   `0 - suspended`: la suscripción está bloqueada y el suscriptor no puede llamar a ninguna API del producto.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="ef3f8-156">-   `1 - active`: la suscripción está activa.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="ef3f8-157">-   `2 - expired`: la suscripción ha alcanzado su fecha de expiración y se ha desactivado.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="ef3f8-158">-   `3 - submitted`: el desarrollador ha realizado una solicitud de suscripción, pero esta aún no se ha aprobado ni rechazado.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="ef3f8-159">-   `4 - rejected`: un administrador ha rechazado la solicitud de suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="ef3f8-160">-   `5 - cancelled`: el desarrollador o el administrador han cancelado la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="ef3f8-161">límites</span><span class="sxs-lookup"><span data-stu-id="ef3f8-161">Limits</span></span>|<span data-ttu-id="ef3f8-162">array</span><span class="sxs-lookup"><span data-stu-id="ef3f8-162">array</span></span>|<span data-ttu-id="ef3f8-163">Esta propiedad está en desuso y no debe utilizarse.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="ef3f8-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="ef3f8-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="ef3f8-165">boolean</span><span class="sxs-lookup"><span data-stu-id="ef3f8-165">boolean</span></span>|<span data-ttu-id="ef3f8-166">Si la [delegación](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está habilitada para esta suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="ef3f8-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="ef3f8-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="ef3f8-168">string</span><span class="sxs-lookup"><span data-stu-id="ef3f8-168">string</span></span>|<span data-ttu-id="ef3f8-169">Si la delegación está habilitada, la dirección URL de la suscripción delegada.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="ef3f8-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="ef3f8-170">IsAgreed</span></span>|<span data-ttu-id="ef3f8-171">boolean</span><span class="sxs-lookup"><span data-stu-id="ef3f8-171">boolean</span></span>|<span data-ttu-id="ef3f8-172">Si el producto tiene términos, si el usuario actual ha aceptado los términos.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="ef3f8-173">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="ef3f8-173">Subscriptions</span></span>|<span data-ttu-id="ef3f8-174">Colección de entidades de [resumen de suscripción](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="ef3f8-175">Las suscripciones al producto.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="ef3f8-176">Apis</span><span class="sxs-lookup"><span data-stu-id="ef3f8-176">Apis</span></span>|<span data-ttu-id="ef3f8-177">Colección de entidades de [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="ef3f8-178">Las API de este producto.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="ef3f8-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="ef3f8-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="ef3f8-180">boolean</span><span class="sxs-lookup"><span data-stu-id="ef3f8-180">boolean</span></span>|<span data-ttu-id="ef3f8-181">Si el usuario actual es apto para suscribirse a este producto en relación con el límite de suscripción.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="ef3f8-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="ef3f8-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="ef3f8-183">boolean</span><span class="sxs-lookup"><span data-stu-id="ef3f8-183">boolean</span></span>|<span data-ttu-id="ef3f8-184">Si el usuario actual es apto para suscribirse a este producto en relación con que se permitan o no varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="ef3f8-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ef3f8-185">Ejemplo de datos de plantilla</span><span class="sxs-lookup"><span data-stu-id="ef3f8-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="ef3f8-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef3f8-186">Next steps</span></span>
<span data-ttu-id="ef3f8-187">Para más información sobre cómo trabajar con plantillas, consulte [Cómo personalizar el portal para desarrolladores de API Management mediante plantillas](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ef3f8-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>