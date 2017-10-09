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
# <a name="product-templates-in-azure-api-management"></a>Plantillas de producto en Azure API Management
Administración de API de Azure proporciona que Hola contenido de hello toocustomize de capacidad de páginas del portal para desarrolladores con un conjunto de plantillas que configure su contenido. Usar [DotLiquid](http://dotliquidmarkup.org/) editor hello y sintaxis de su elección, como [DotLiquid a los diseñadores](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), o cambie de tamaño un conjunto proporcionado de [los recursos de cadena](api-management-template-resources.md#strings), [ Recursos de glifo](api-management-template-resources.md#glyphs), y [página controles](api-management-page-controls.md), tienen contenido de gran flexibilidad tooconfigure Hola de páginas de Hola como considere oportuno mediante estas plantillas.  
  
 las plantillas de Hello en esta sección permiten contenido de hello toocustomize de páginas de producto de hello en el portal para desarrolladores de Hola.  
  
-   [Product list](#ProductList)  
  
-   [Producto](#Product)  
  
> [!NOTE]
>  Plantillas predeterminadas de ejemplo se incluyen en hello siguiendo documentación, pero están toochange asunto debido toocontinuous mejoras. Puede ver plantillas de hello predeterminado en vivo en el portal para desarrolladores de hello desplazándose plantillas individuales toohello deseado. Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a> Product list  
 Hola **lista de productos** plantilla permite cuerpo de hello toocustomize de página de lista de productos de hello en el portal para desarrolladores de Hola.  
  
 ![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Plantilla predeterminada  
  
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
  
### <a name="controls"></a>Controles  
 Hola `Product list` plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).  
  
-   [paging-control](api-management-page-controls.md#paging-control)  
  
-   [search-control](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Modelo de datos  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Paginación|Entidad [Paging](api-management-template-data-model-reference.md#Paging).|información de paginación de Hello para la colección de productos de Hola.|  
|Filtros|Entidad [Filtering](api-management-template-data-model-reference.md#Filtering).|Hola filtrado de información para la página lista de productos de Hola.|  
|Productos|Colección de entidades de [producto](api-management-template-data-model-reference.md#Product).|Hola productos toohello visible el usuario actual.|  
  
### <a name="sample-template-data"></a>Ejemplo de datos de plantilla  
  
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
  
##  <a name="Product"></a> Product  
 Hola **producto** plantilla permite cuerpo de hello toocustomize de página del producto hello en el portal para desarrolladores de Hola.  
  
 ![Página de producto del portal para desarrolladores](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Plantilla predeterminada  
  
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
  
### <a name="controls"></a>Controles  
 Hola `Product list` plantilla puede utilizar la siguiente hello [página controles](api-management-page-controls.md).  
  
-   [subscribe-button](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Modelo de datos  
  
|Propiedad|Escriba|Descripción|  
|--------------|----------|-----------------|  
|Producto|[Producto](api-management-template-data-model-reference.md#Product)|producto de Hello especificado.|  
|IsDeveloperSubscribed|boolean|Si el usuario actual de hello es producto toothis suscrito.|  
|SubscriptionState|número|estado de Hola de suscripción de Hola. Los estados posibles son:<br /><br /> -   `0 - suspended`: Hola suscripción está bloqueada y suscriptor hello no puede llamar a las API del producto de Hola.<br />-   `1 - active`: Hola suscripción está activa.<br />-   `2 - expired`– suscripción Hola alcanza su fecha de expiración y se ha desactivado.<br />-   `3 - submitted`: solicitud de suscripción de Hola se ha realizado por el desarrollador de hello, pero ha aún no aprobado o rechazados.<br />-   `4 - rejected`: un administrador ha denegado la solicitud de suscripción de Hola.<br />-   `5 - cancelled`: se ha cancelado la suscripción Hola programador de Hola o el administrador.|  
|límites|array|Esta propiedad está en desuso y no debe utilizarse.|  
|DelegatedSubscriptionEnabled|boolean|Si la [delegación](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) está habilitada para esta suscripción.|  
|DelegatedSubscriptionUrl|cadena|Si se permite la delegación, Hola había delegada dirección URL de la suscripción.|  
|IsAgreed|boolean|Si el producto de hello tiene términos, si ha acordado usuario actual de hello toohello términos.|  
|Suscripciones|Colección de entidades de [resumen de suscripción](api-management-template-data-model-reference.md#SubscriptionSummary).|producto de toohello de Hello las suscripciones.|  
|Apis|Colección de entidades [API](api-management-template-data-model-reference.md#API).|Hola API en este producto.|  
|CannotAddBecauseSubscriptionNumberLimitReached|boolean|Si el usuario actual de hello es elegible toosubscribe toothis producto con un límite de suscripción toohello de tener en cuenta.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|boolean|Si el usuario actual de hello es elegible toosubscribe toothis producto con suscripciones de toomultiple de tener en cuenta que se permiten o no.|  
  
### <a name="sample-template-data"></a>Ejemplo de datos de plantilla  
  
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

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo trabajar con plantillas, consulte [cómo toocustomize Hola portal de administración de API para desarrolladores con plantillas de](api-management-developer-portal-templates.md).
