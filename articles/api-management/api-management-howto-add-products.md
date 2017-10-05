---
title: "Creación y publicación de un producto en Administración de API de Azure"
description: "Obtenga información acerca de cómo crear y publicar productos en Administración de API de Azure."
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="9a0dd-103">Creación y publicación de un producto en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="9a0dd-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="9a0dd-104">En Administración de API de Azure, un producto contiene una o varias API, así como una cuota de uso y los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="9a0dd-105">Una vez publicado un producto, los desarrolladores pueden suscribirse al producto y comenzar a usar las API del producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="9a0dd-106">Este tema ofrece una guía para crear un producto, agregarle una API y publicarlo para los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="9a0dd-107"><a name="create-product"> </a>Creación de un producto</span><span class="sxs-lookup"><span data-stu-id="9a0dd-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="9a0dd-108">Las operaciones se agregan y se configuran para una API en el portal del publicador.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="9a0dd-109">Para obtener acceso al portal del publicador, haga clic en el **portal del publicador** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="9a0dd-111">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9a0dd-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="9a0dd-112">Haga clic en **Productos** en el menú de la izquierda para mostrar la página **Productos** y haga clic en **Agregar producto**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Productos][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="9a0dd-115">Escriba un nombre descriptivo para el producto en el campo **Nombre** y una descripción del producto en el campo **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="9a0dd-116">Los productos de API Management pueden tener el estado **Abierto** o **Protegido**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="9a0dd-117">Para poder usar los productos protegidos es necesario suscribirse antes a ellos, mientras que los productos abiertos pueden usarse sin suscripción.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="9a0dd-118">Active la opción **Requerir suscripción** para crear un producto protegido que requiera una suscripción.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="9a0dd-119">Esta es la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-119">This is the default setting.</span></span>

<span data-ttu-id="9a0dd-120">Active **Requerir aprobación de suscripción** si desea que un administrador revise y acepte o rechace los intentos de suscripción a este producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="9a0dd-121">Si la casilla no se activa, los intentos de suscripción se autoaprobarán.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="9a0dd-122">Para obtener más información sobre suscripciones, consulte [Vista de los suscriptores de un producto][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="9a0dd-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="9a0dd-123">Para permitir que las cuentas de desarrollador se suscriban varias veces al producto, active la casilla **Permitir varias suscripciones** .</span><span class="sxs-lookup"><span data-stu-id="9a0dd-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="9a0dd-124">Si esta casilla no está activada, cada cuenta de desarrollador puede suscribirse una sola vez al producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Suscripciones múltiples ilimitadas][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="9a0dd-126">Para limitar el número de suscripciones múltiples simultáneas, active la casilla **Limitar el número de suscripciones simultáneas a** y escriba el límite de suscripción.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="9a0dd-127">En el ejemplo siguiente, las suscripciones simultáneas se limitan a cuatro por cada cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Para varias suscripciones][api-management-four-multiple-subscriptions]

<span data-ttu-id="9a0dd-129">Una vez configuradas todas las opciones del nuevo producto, haga clic en **Guardar** para crear el nuevo producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Productos][api-management-products-page]

> <span data-ttu-id="9a0dd-131">De forma predeterminada, los nuevos productos no se publican y solo son visibles para el grupo **Administradores**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="9a0dd-132">Para configurar un producto, haga clic en el nombre del producto en la pestaña **Productos** .</span><span class="sxs-lookup"><span data-stu-id="9a0dd-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="9a0dd-133"><a name="add-apis"> </a>Incorporación de API a un producto</span><span class="sxs-lookup"><span data-stu-id="9a0dd-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="9a0dd-134">La página **Productos** contiene cuatro vínculos de configuración: **Resumen**, **Configuración**, **Visibilidad** y **Suscriptores**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="9a0dd-135">En la pestaña **Resumen** puede agregar API y publicar o anular la publicación de un producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Resumen][api-management-new-product-summary]

<span data-ttu-id="9a0dd-137">Antes de publicar el producto, debe agregar una o más API.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="9a0dd-138">Para ello, haga clic en **Agregar API al producto**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-138">To do this, click **Add API to product**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="9a0dd-140">Seleccione las API que desee y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="9a0dd-141"><a name="add-description"> </a>Incorporación de información descriptiva a un producto</span><span class="sxs-lookup"><span data-stu-id="9a0dd-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="9a0dd-142">La pestaña **Configuración** permite proporcionar información detallada sobre el producto como, por ejemplo, su finalidad, las API a las que ofrece acceso y otra información útil.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="9a0dd-143">El contenido se dirige a los desarrolladores que llamarán a la API y pueden escribirse en texto sin formato o marcado HTML.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="9a0dd-145">Active **Requerir suscripción** para crear un producto protegido que requiera una suscripción para usarse o, desactive la casilla de verificación para crear un producto abierto al que se pueda llamar sin una suscripción.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="9a0dd-146">Seleccione **Requerir aprobación de suscripción** si desea aprobar manualmente todas las solicitudes de suscripción de productos.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="9a0dd-147">De forma predeterminada, todas las suscripciones de productos se conceden automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="9a0dd-148">Para permitir que las cuentas de desarrollador se suscriban varias veces al nuevo producto, active la casilla **Permitir varias suscripciones** y, opcionalmente, especifique un límite.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="9a0dd-149">Si esta casilla no está activada, cada cuenta de desarrollador puede suscribirse una sola vez al producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="9a0dd-150">Opcionalmente, rellene el campo **Términos de uso** que describe los términos de uso del producto que los suscriptores deben aceptar para usar el producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="9a0dd-151"><a name="publish-product"> </a>Publicación de un producto</span><span class="sxs-lookup"><span data-stu-id="9a0dd-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="9a0dd-152">Para poder llamar a las API de un producto, este debe publicarse.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="9a0dd-153">En la pestaña **Resumen** correspondiente al producto, haga clic en **Publicar**, y luego en **Sí, publicarlo** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="9a0dd-154">Para convertir en privado un producto previamente publicado, haga clic en **Anular publicación**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-154">To make a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="9a0dd-156"><a name="make-visible"> </a>Visibilidad de un producto para los desarrolladores</span><span class="sxs-lookup"><span data-stu-id="9a0dd-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="9a0dd-157">La pestaña **Visibilidad** permite elegir los roles que pueden ver el producto en el portal para desarrolladores y suscribirse al producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="9a0dd-159">Para habilitar o deshabilitar la visibilidad de un producto para los desarrolladores de un grupo, active o desactive la casilla situada junto al grupo y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="9a0dd-160">Para obtener más información, consulte [Creación y uso de grupos para administrar cuentas de desarrollador en Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9a0dd-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="9a0dd-161"><a name="view-subscribers"> </a>Vista de los suscriptores de un producto</span><span class="sxs-lookup"><span data-stu-id="9a0dd-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="9a0dd-162">La pestaña **Suscriptores** muestra la lista de desarrolladores que se han suscrito al producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="9a0dd-163">Los detalles y la configuración de cada desarrollador se pueden ver haciendo clic en el nombre del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="9a0dd-164">En este ejemplo, ningún desarrollador se ha suscrito todavía al producto.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-164">In this example no developers have yet subscribed to the product.</span></span>

![Desarrolladores][api-management-developer-list]

## <span data-ttu-id="9a0dd-166"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a0dd-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="9a0dd-167">Una vez agregadas las API que se deseen y publicado el producto, los desarrolladores pueden suscribirse al producto y comenzar a llamar a las API.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="9a0dd-168">Para obtener un tutorial que demuestre estos elementos, además de la configuración avanzada del producto, consulte el artículo que versa sobre la [creación y definición de configuraciones de productos avanzadas en Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9a0dd-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="9a0dd-169">Para obtener más información acerca de cómo trabajar con los productos, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="9a0dd-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
