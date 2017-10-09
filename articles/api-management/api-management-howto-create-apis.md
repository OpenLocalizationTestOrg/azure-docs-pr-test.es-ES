---
title: "aaaHow toocreate las API de administración de API de Azure"
description: "Obtenga información acerca de cómo toocreate y configurar las API de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="b3b62-103">¿Cómo toocreate las API de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="b3b62-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="b3b62-104">En Administración de API, una API representa un conjunto de operaciones que puede invocarse por las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="b3b62-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="b3b62-105">Nuevas API se crean en el portal para desarrolladores de hello y, a continuación, Hola deseado se agregan las operaciones.</span><span class="sxs-lookup"><span data-stu-id="b3b62-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="b3b62-106">Una vez que se agregan las operaciones de hello, Hola API se agrega tooa producto y se puede publicar.</span><span class="sxs-lookup"><span data-stu-id="b3b62-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="b3b62-107">Una vez publicada una API, puede ser suscrita tooand utilizado por los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="b3b62-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="b3b62-108">Esta guía muestra el primer paso de hello en proceso de hello: cómo toocreate y configurar una nueva API de administración de API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="b3b62-109">Para obtener más información sobre las operaciones de agregar y publicar un producto, consulte [cómo tooadd operaciones tooan API] [ How tooadd operations tooan API] y [cómo toocreate y publicar un producto] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="b3b62-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="b3b62-110"><a name="create-new-api"></a>Creación de una API</span><span class="sxs-lookup"><span data-stu-id="b3b62-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="b3b62-111">Las API se crean y configuran en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3b62-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="b3b62-112">tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="b3b62-114">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b3b62-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="b3b62-115">Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **agregar API**.</span><span class="sxs-lookup"><span data-stu-id="b3b62-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="b3b62-117">Hola de uso **agregar nueva API** tooconfigure ventana Hola nueva API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Add new API][api-management-add-new-api]

<span data-ttu-id="b3b62-119">Hola después campos es tooconfigure usado Hola nueva API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="b3b62-120">**Nombre de la API Web** proporciona un nombre único y descriptivo para hello API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="b3b62-121">Se muestra en los portales de desarrollador y el publicador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3b62-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="b3b62-122">**Dirección URL del servicio Web** referencias Hola implementa Hola API de servicio HTTP.</span><span class="sxs-lookup"><span data-stu-id="b3b62-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="b3b62-123">Administración de API reenvía las solicitudes de toothis dirección.</span><span class="sxs-lookup"><span data-stu-id="b3b62-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="b3b62-124">**Sufijo de URL de la API de Web** es toohello anexado dirección URL base del servicio de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3b62-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="b3b62-125">dirección URL base de Hello es común para todas las API hospedadas en una instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="b3b62-126">Administración de API distingue API mediante su sufijo y, por tanto, el sufijo de hello debe ser único para todas las API de un publicador determinado.</span><span class="sxs-lookup"><span data-stu-id="b3b62-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="b3b62-127">**Esquema de dirección URL de la API de Web** determina qué protocolos pueden ser utilizados tooaccess Hola API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="b3b62-128">HTTPs es el protocolo especificado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b3b62-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="b3b62-129">toooptionally agregar este nuevo producto tooa de API, haga clic en hello **productos (opcionales)** lista desplegable y elija un producto.</span><span class="sxs-lookup"><span data-stu-id="b3b62-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="b3b62-130">Este paso puede ser varias repetidas veces tooadd Hola API toomultiple productos.</span><span class="sxs-lookup"><span data-stu-id="b3b62-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="b3b62-131">Una vez Hola deseado se configuran los valores, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="b3b62-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="b3b62-132">Una vez creada la nueva API de hello, hello página de resumen de la API de Hola se muestra en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3b62-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API summary][api-management-api-summary]

## <span data-ttu-id="b3b62-134"><a name="configure-api-settings"></a>Definición de la configuración de la API</span><span class="sxs-lookup"><span data-stu-id="b3b62-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="b3b62-135">Puede usar hello **configuración** ficha tooverify y editar configuración de Hola de una API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="b3b62-136">**Nombre de la API Web**, **dirección URL del servicio Web**, y **sufijo de URL de la API de Web** se establecen inicialmente cuando Hola API se crea y se puede modificar aquí.</span><span class="sxs-lookup"><span data-stu-id="b3b62-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="b3b62-137">**Descripción** proporciona una descripción opcional, y **esquema de dirección URL de Web API** determina qué protocolos pueden ser utilizados tooaccess Hola API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![API settings][api-management-api-settings]

<span data-ttu-id="b3b62-139">autenticación de puerta de enlace de tooconfigure hello back-end de servicio API de implementación hello, seleccione hello **seguridad** Hola de pestaña. **con credenciales** desplegable puede ser usado tooconfigure **HTTP básico** o **certificados de cliente** autenticación.</span><span class="sxs-lookup"><span data-stu-id="b3b62-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="b3b62-140">la autenticación básica HTTP toouse, simplemente escriba las credenciales de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="b3b62-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="b3b62-141">Para obtener información sobre el uso de autenticación de certificado de cliente, consulte [cómo toosecure servicios de back-end con cliente de certificado autenticación de administración de API de Azure][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b3b62-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="b3b62-142">Hola **seguridad** ficha también puede ser utilizado tooconfigure **autorización del usuario** mediante OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="b3b62-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="b3b62-143">Para obtener más información, consulte [cómo tooauthorize developer cuentas con OAuth 2.0 en la administración de API de Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b3b62-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Basic authentication settings][api-management-api-settings-credentials]

<span data-ttu-id="b3b62-145">Haga clic en **guardar** toosave los cambios que realice toohello configuración de la API.</span><span class="sxs-lookup"><span data-stu-id="b3b62-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="b3b62-146"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3b62-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="b3b62-147">Una vez que se crea una API y configuración de hello, pasos siguientes hello tooadd Hola operaciones toohello API, agregar Hola API tooa producto y publicarlo para que esté disponible para los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="b3b62-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="b3b62-148">Para obtener más información, vea Hola siguientes artículos.</span><span class="sxs-lookup"><span data-stu-id="b3b62-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="b3b62-149">[¿Cómo tooadd operaciones tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="b3b62-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="b3b62-150">[¿Cómo toocreate y publicación de productos][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="b3b62-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
