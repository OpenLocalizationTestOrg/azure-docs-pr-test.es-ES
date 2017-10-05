---
title: "Creación de API en Administración de API de Azure"
description: "Obtenga información acerca de cómo crear y configurar las API en Administración de API de Azure."
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="16c4a-103">Creación de API en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="16c4a-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="16c4a-104">En Administración de API, una API representa un conjunto de operaciones que puede invocarse por las aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="16c4a-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="16c4a-105">Se crean nuevas API en el portal del publicador y luego se agregan las operaciones deseadas.</span><span class="sxs-lookup"><span data-stu-id="16c4a-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="16c4a-106">Una vez agregadas las operaciones, la API se agrega a un producto y se puede publicar.</span><span class="sxs-lookup"><span data-stu-id="16c4a-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="16c4a-107">Una vez publicada una API, pueden usarla y suscribirse a ella los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="16c4a-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="16c4a-108">Esta guía muestra el primer paso del proceso: cómo crear y configurar una nueva API en Administración de API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="16c4a-109">Para obtener más información sobre cómo agregar operaciones y publicar un producto, consulte [Incorporación de operaciones a una API][How to add operations to an API] y [Creación y publicación de un producto][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="16c4a-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="16c4a-110"><a name="create-new-api"> </a>Creación de una API</span><span class="sxs-lookup"><span data-stu-id="16c4a-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="16c4a-111">Las API se crean y se configuran en el portal del publicador.</span><span class="sxs-lookup"><span data-stu-id="16c4a-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="16c4a-112">Para obtener acceso al portal del publicador, haga clic en el **portal del publicador** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="16c4a-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="16c4a-114">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="16c4a-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="16c4a-115">Haga clic en **API** en el menú **API Management** de la izquierda y haga clic en **Agregar API**.</span><span class="sxs-lookup"><span data-stu-id="16c4a-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Create API][api-management-create-api]

<span data-ttu-id="16c4a-117">Use la ventana **Agregar nueva API** para configurar la nueva API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-117">Use the **Add new API** window to configure the new API.</span></span>

![Agregar nueva API][api-management-add-new-api]

<span data-ttu-id="16c4a-119">Para configurar la nueva API se usan los campos siguientes.</span><span class="sxs-lookup"><span data-stu-id="16c4a-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="16c4a-120">**nombre de la API web** ofrece un nombre único y descriptivo para la API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="16c4a-121">Se muestra en el portal para desarrolladores y en el portal del publicador.</span><span class="sxs-lookup"><span data-stu-id="16c4a-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="16c4a-122">**URL de servicio Web** hace referencia al servicio HTTP que implementa la API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="16c4a-123">Administración de API envía las solicitudes a esta dirección.</span><span class="sxs-lookup"><span data-stu-id="16c4a-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="16c4a-124">**Sufijo de dirección URL API web** se anexa a la dirección URL base para el servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="16c4a-125">La dirección URL base es común para todas las API hospedadas en una instancia del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="16c4a-126">Administración de API distingue las API por su sufijo, por lo que el sufijo debe ser único para cada API de un publicador determinado.</span><span class="sxs-lookup"><span data-stu-id="16c4a-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="16c4a-127">**Esquema de URL de la API web** determina qué protocolos se pueden usar para tener acceso a la API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="16c4a-128">HTTPs es el protocolo especificado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="16c4a-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="16c4a-129">Para agregar opcionalmente esta nueva API a un producto, haga clic en el desplegable **Productos (opcional)** y elija un producto.</span><span class="sxs-lookup"><span data-stu-id="16c4a-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="16c4a-130">Este paso se puede repetir varias veces para agregar la API a varios productos.</span><span class="sxs-lookup"><span data-stu-id="16c4a-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="16c4a-131">Una vez configurados los valores que se desean, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="16c4a-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="16c4a-132">Una vez creada la nueva API, su página de resumen se mostrará en el portal para editores.</span><span class="sxs-lookup"><span data-stu-id="16c4a-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![API summary][api-management-api-summary]

## <span data-ttu-id="16c4a-134"><a name="configure-api-settings"> </a>Definición de la configuración de la API</span><span class="sxs-lookup"><span data-stu-id="16c4a-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="16c4a-135">Puede usar la pestaña **Configuración** para comprobar y editar la configuración de una API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="16c4a-136">**Nombre de la API web**, **URL de servicio web** y **Sufijo de URL de la API web** se establecen inicialmente al crear la API y se pueden modificar aquí.</span><span class="sxs-lookup"><span data-stu-id="16c4a-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="16c4a-137">**Descripción** proporciona una descripción opcional y **Esquema de URL de la API web** determina qué protocolos se pueden usar para tener acceso a la API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![API settings][api-management-api-settings]

<span data-ttu-id="16c4a-139">Para configurar la autenticación de puerta de enlace para el servicio back-end que implementa la API, seleccione la pestaña **Seguridad** .</span><span class="sxs-lookup"><span data-stu-id="16c4a-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="16c4a-140">El menú desplegable **Con credenciales** se puede usar para configurar la **HTTP básica** o **Certificados de cliente**.</span><span class="sxs-lookup"><span data-stu-id="16c4a-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="16c4a-141">Para usar la autenticación básica HTTP, solo tiene que escribir las credenciales que quiera.</span><span class="sxs-lookup"><span data-stu-id="16c4a-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="16c4a-142">Para obtener información sobre el uso de la autenticación de certificados de cliente, consulte [Cómo asegurar servicios back-end con la autenticación de certificados de cliente en Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="16c4a-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="16c4a-143">La pestaña **Seguridad** también se puede usar para configurar la **Autorización de usuario** con OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16c4a-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="16c4a-144">Para obtener más información, consulte [Procedimiento para autorizar a las cuentas de desarrollador para que usen OAuth 2.0 en Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="16c4a-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Basic authentication settings][api-management-api-settings-credentials]

<span data-ttu-id="16c4a-146">Haga clic en **Guardar** para guardar los cambios que efectúe en la configuración de la API.</span><span class="sxs-lookup"><span data-stu-id="16c4a-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="16c4a-147"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16c4a-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="16c4a-148">Una vez creada una API y definida la configuración, los pasos siguientes permiten agregar las operaciones a la API, agregar la API a un producto y publicarlo para ponerlo a disposición de los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="16c4a-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="16c4a-149">Para obtener más información, consulte los siguientes artículos.</span><span class="sxs-lookup"><span data-stu-id="16c4a-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="16c4a-150">[Incorporación de operaciones a una API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="16c4a-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="16c4a-151">[Creación y publicación de un producto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="16c4a-151">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
