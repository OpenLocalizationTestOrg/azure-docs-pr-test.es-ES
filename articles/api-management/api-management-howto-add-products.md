---
title: "aaaHow toocreate y publicar un producto en la administración de API de Azure"
description: "Obtenga información acerca de cómo toocreate y publicar productos en la administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="93687-103">¿Cómo toocreate y publicar un producto en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="93687-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="93687-104">En la administración de API de Azure, un producto contiene una o varias API, así como de los términos de uso hello y cuota de uso.</span><span class="sxs-lookup"><span data-stu-id="93687-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="93687-105">Una vez que se publica un producto, los desarrolladores pueden suscribirse toohello producto y empezar a API del producto de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="93687-106">tema de Hola proporciona una guía toocreating un producto, agregar una API y publicarlo para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="93687-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="93687-107"><a name="create-product"></a>Creación de un producto</span><span class="sxs-lookup"><span data-stu-id="93687-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="93687-108">Las operaciones se agregan y configuran tooan API en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="93687-109">tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="93687-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="93687-111">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="93687-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="93687-112">Haga clic en **productos** en el menú Hola Hola toodisplay izquierdo Hola **productos** página y haga clic en **agregar producto**.</span><span class="sxs-lookup"><span data-stu-id="93687-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Productos][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="93687-115">Escriba un nombre descriptivo para el producto de Hola Hola **nombre** campo y una descripción de producto de Hola Hola **descripción** campo.</span><span class="sxs-lookup"><span data-stu-id="93687-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="93687-116">Los productos de API Management pueden tener el estado **Abierto** o **Protegido**.</span><span class="sxs-lookup"><span data-stu-id="93687-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="93687-117">Productos protegidos deben estar suscrito toobefore pueden usarse, mientras está abierto productos pueden utilizarse sin una suscripción.</span><span class="sxs-lookup"><span data-stu-id="93687-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="93687-118">Comprobar **requieren suscripción** toocreate un producto protegido que requiere una suscripción.</span><span class="sxs-lookup"><span data-stu-id="93687-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="93687-119">Se trata de una configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-119">This is hello default setting.</span></span>

<span data-ttu-id="93687-120">Comprobar **requieren la aprobación de suscripción** si desea un tooreview administrador y Aceptar o rechazar suscripción intenta toothis producto.</span><span class="sxs-lookup"><span data-stu-id="93687-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="93687-121">Si Hola casilla está desactivada, los intentos de suscripción será aprobada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="93687-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="93687-122">Para obtener más información sobre las suscripciones, vea [producto de vista suscriptores tooa][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="93687-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="93687-123">tooallow developer cuentas toosubscribe producto de toohello varias veces, compruebe hello **permitir múltiples suscripciones** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="93687-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="93687-124">Si esta casilla no está activada, cada cuenta de desarrollador puede suscribirse solo un producto de toohello sola vez.</span><span class="sxs-lookup"><span data-stu-id="93687-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Suscripciones múltiples ilimitadas][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="93687-126">recuento de hello toolimit de varias suscripciones simultáneas, comprobar hello **limitar el número de suscripciones simultáneas a** casilla de verificación y especifique el límite de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="93687-127">En el siguiente ejemplo de Hola, suscripciones simultáneas son toofour limitado por cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="93687-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Para varias suscripciones][api-management-four-multiple-subscriptions]

<span data-ttu-id="93687-129">Una vez configuradas todas las nuevas opciones de producto, haga clic en **guardar** nuevo producto de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Productos][api-management-products-page]

> <span data-ttu-id="93687-131">De forma predeterminada no están publicados nuevos productos y son visible toohello solo **administradores** grupo.</span><span class="sxs-lookup"><span data-stu-id="93687-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="93687-132">tooconfigure un producto, haga clic en el nombre de producto de hello en hello **productos** ficha.</span><span class="sxs-lookup"><span data-stu-id="93687-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="93687-133"><a name="add-apis"></a>Producto de tooa agregar API</span><span class="sxs-lookup"><span data-stu-id="93687-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="93687-134">Hola **productos** página contiene cuatro vínculos de configuración: **resumen**, **configuración**, **visibilidad**, y  **Los suscriptores**.</span><span class="sxs-lookup"><span data-stu-id="93687-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="93687-135">Hola **resumen** ficha es donde puede agregar las API y publicar o cancelar la publicación de un producto.</span><span class="sxs-lookup"><span data-stu-id="93687-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Resumen][api-management-new-product-summary]

<span data-ttu-id="93687-137">Antes de publicar un producto necesario tooadd una o varias API.</span><span class="sxs-lookup"><span data-stu-id="93687-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="93687-138">toodo, haga clic en **tooproduct agregar API**.</span><span class="sxs-lookup"><span data-stu-id="93687-138">toodo this, click **Add API tooproduct**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="93687-140">Seleccione Hola deseado API y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="93687-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="93687-141"><a name="add-description"></a>Producto de agregar información descriptiva tooa</span><span class="sxs-lookup"><span data-stu-id="93687-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="93687-142">Hola **configuración** pestaña le permite tooprovide información detallada sobre el producto de hello como su propósito, hello las API que proporciona acceso a y otra información útil.</span><span class="sxs-lookup"><span data-stu-id="93687-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="93687-143">contenido de Hola está destinada a los desarrolladores de Hola que llamará a la API de Hola y pueden escribirse en texto sin formato o en formato HTML.</span><span class="sxs-lookup"><span data-stu-id="93687-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="93687-145">Comprobar **requieren suscripción** toocreate un producto protegido que requiera un toobe de suscripción se usan o desactive Hola casilla toocreate un producto abierto que se pueda llamar sin una suscripción.</span><span class="sxs-lookup"><span data-stu-id="93687-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="93687-146">Seleccione **requieren la aprobación de suscripción** si desea toomanually aprobar todas las solicitudes de suscripción de producto.</span><span class="sxs-lookup"><span data-stu-id="93687-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="93687-147">De forma predeterminada, todas las suscripciones de productos se conceden automáticamente.</span><span class="sxs-lookup"><span data-stu-id="93687-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="93687-148">tooallow developer cuentas toosubscribe producto de toohello varias veces, compruebe hello **permitir múltiples suscripciones** casilla de verificación y, opcionalmente, especifique un límite.</span><span class="sxs-lookup"><span data-stu-id="93687-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="93687-149">Si esta casilla no está activada, cada cuenta de desarrollador puede suscribirse solo un producto de toohello sola vez.</span><span class="sxs-lookup"><span data-stu-id="93687-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="93687-150">Si lo desea, rellene hello **términos de uso** campo donde se describen los términos de Hola de uso de producto de Hola que deben aceptar los suscriptores de producto del pedido toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="93687-151"><a name="publish-product"></a>Publicación de un producto</span><span class="sxs-lookup"><span data-stu-id="93687-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="93687-152">Para poder llamar a las API de hello en un producto, se debe publicar el producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="93687-153">En hello **resumen** , haga clic para el producto de hello **publicar**y, a continuación, haga clic en **Sí, publicarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="93687-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="93687-154">toomake privado producto publicados anteriormente, haga clic en **Unpublish**.</span><span class="sxs-lookup"><span data-stu-id="93687-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="93687-156"><a name="make-visible"></a>Realizar un toodevelopers visible del producto</span><span class="sxs-lookup"><span data-stu-id="93687-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="93687-157">Hola **visibilidad** pestaña le permite toochoose qué roles son toosee capaz de producto de hello en el portal para desarrolladores de Hola y suscriben toohello producto.</span><span class="sxs-lookup"><span data-stu-id="93687-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="93687-159">tooenable o deshabilitar visibilidad de un producto para programadores de hello en un grupo, compruebe o desactive Hola casilla situada junto a grupo de hello y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="93687-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="93687-160">Para obtener más información, consulte [cómo para desarrolladores de toomanage grupos toocreate y usar las cuentas de administración de API de Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="93687-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="93687-161"><a name="view-subscribers"></a>Producto de tooa de los suscriptores de vista</span><span class="sxs-lookup"><span data-stu-id="93687-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="93687-162">Hola **suscriptores** ficha enumera los desarrolladores de Hola que se han suscrito toohello producto.</span><span class="sxs-lookup"><span data-stu-id="93687-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="93687-163">Hello detalles y la configuración para cada programador puede verse haciendo clic en el nombre del desarrollador de Hola.</span><span class="sxs-lookup"><span data-stu-id="93687-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="93687-164">En este ejemplo no los desarrolladores han suscrito aún toohello producto.</span><span class="sxs-lookup"><span data-stu-id="93687-164">In this example no developers have yet subscribed toohello product.</span></span>

![Desarrolladores][api-management-developer-list]

## <span data-ttu-id="93687-166"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93687-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="93687-167">Una vez Hola deseado las API se agregan y se publica el producto de hello, los desarrolladores pueden suscribirse toohello producto y comenzar toocall Hola API.</span><span class="sxs-lookup"><span data-stu-id="93687-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="93687-168">Para obtener un tutorial que demuestre estos elementos, además de la configuración avanzada del producto, consulte el artículo que versa sobre la [creación y definición de configuraciones de productos avanzadas en Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="93687-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="93687-169">Para obtener más información sobre cómo trabajar con productos, vea Hola después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="93687-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
