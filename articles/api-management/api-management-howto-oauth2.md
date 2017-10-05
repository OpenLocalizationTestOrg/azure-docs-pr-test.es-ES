---
title: "Autorización de las cuentas de desarrollador mediante OAuth 2.0 en Azure API Management | Microsoft Docs"
description: "Obtenga información acerca de cómo autorizar a los usuarios para que utilicen OAuth 2.0 en Administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="1052f-103">Procedimiento para autorizar a las cuentas de desarrollador para que usen OAuth 2.0 en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="1052f-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="1052f-104">Muchas API admiten [OAuth 2.0](http://oauth.net/2/) para proteger la API y garantizar que solo usuarios válidos obtengan acceso y que, además, solo puedan tener acceso a los recursos para los que estén autorizados.</span><span class="sxs-lookup"><span data-stu-id="1052f-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="1052f-105">Para usar la consola interactiva para desarrolladores de la Administración de API de Azure, el servicio permite configurar la instancia del servicio para que funcione con la API habilitada para OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="1052f-106"><a name="prerequisites"> </a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1052f-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="1052f-107">En esta guía se explica cómo configurar la instancia del servicio Administración de API para que use la autorización OAuth 2.0 con las cuentas de desarrollador, pero no se explica cómo configurar un proveedor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="1052f-108">Aunque los proveedores de OAuth 2.0 tienen configuraciones diferentes, los pasos son similares y se precisa la misma información para configurar OAuth 2.0 en la instancia del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="1052f-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="1052f-109">Este tema muestra ejemplos donde Azure Active Directory actúa como proveedor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="1052f-110">Para obtener más información sobre cómo configurar OAuth 2.0 con Azure Active Directory, consulte el ejemplo de [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet].</span><span class="sxs-lookup"><span data-stu-id="1052f-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="1052f-111"><a name="step1"> </a>Configurar un servidor de autorización OAuth 2.0 en Administración de API</span><span class="sxs-lookup"><span data-stu-id="1052f-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="1052f-112">Para comenzar, haga clic en **Portal para editores** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="1052f-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="1052f-114">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1052f-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="1052f-115">Haga clic en **Seguridad** en el menú **API Management** de la izquierda, haga clic en **OAuth 2.0** y, después, en **Agregar servidor de autorización**.</span><span class="sxs-lookup"><span data-stu-id="1052f-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="1052f-117">Al hacer clic en **Agregar servidor de autorización**, se muestra el formulario para un nuevo servidor de autorización.</span><span class="sxs-lookup"><span data-stu-id="1052f-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![Nuevo servidor][api-management-oauth2-server-1]

<span data-ttu-id="1052f-119">Escriba un nombre y una descripción opcional en los campos **Nombre** y **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="1052f-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="1052f-120">Estos campos sirven para identificar el servidor de autorización OAuth 2.0 en la instancia del servicio Administración de API y los valores que contienen no proceden del servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="1052f-121">Escriba la **URL de la página de registro de cliente**.</span><span class="sxs-lookup"><span data-stu-id="1052f-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="1052f-122">En esta página, los usuarios pueden crear y administrar sus cuentas. Puede variar en función del proveedor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="1052f-123">La **URL de la página de registro de cliente** señala a la página que los usuarios pueden utilizar para crear y configurar sus propias cuentas para proveedores de OAuth 2.0 que admiten la administración de usuarios de las cuentas.</span><span class="sxs-lookup"><span data-stu-id="1052f-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="1052f-124">Algunas organizaciones no configuran ni usan esta funcionalidad, aunque la admita el proveedor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="1052f-125">Si el proveedor de OAuth 2.0 no tiene configurada la administración de usuarios de las cuentas, especifique aquí una URL de marcador de posición, por ejemplo, la URL de su empresa o una URL como `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="1052f-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="1052f-126">La sección siguiente del formulario contiene la configuración de los **Tipos de concesión de código de autorización**, la **URL del punto de conexión de autorización** y el **Método de solicitud de autorización**.</span><span class="sxs-lookup"><span data-stu-id="1052f-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nuevo servidor][api-management-oauth2-server-2]

<span data-ttu-id="1052f-128">Active las casillas de los **Tipos de concesión de código de autorización** que desee.</span><span class="sxs-lookup"><span data-stu-id="1052f-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="1052f-129">**Código de autorización** se especifica de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1052f-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="1052f-130">Escriba la **URL del extremo de autorización**.</span><span class="sxs-lookup"><span data-stu-id="1052f-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="1052f-131">En Azure Active Directory, esta URL será similar a la siguiente, donde se reemplaza `<client_id>` por el identificador de cliente que identifica la aplicación en el servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="1052f-132">El **Método de solicitud de autorización** especifica cómo se envía la solicitud de autorización al servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="1052f-133">El valor predeterminado es **GET** .</span><span class="sxs-lookup"><span data-stu-id="1052f-133">By default **GET** is selected.</span></span>

<span data-ttu-id="1052f-134">En la sección siguiente, se especifican la **URL del punto de conexión de token**, los **Métodos de autenticación de cliente**, el **Método de envío de tokens de acceso** y el **Ámbito predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="1052f-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nuevo servidor][api-management-oauth2-server-3]

<span data-ttu-id="1052f-136">En un servidor OAuth 2.0 de Azure Active Directory, la **URL del punto de conexión de token** tendrá el formato siguiente, donde `<APPID>` tiene el formato de `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="1052f-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="1052f-137">Los valores predeterminados para **Métodos de autenticación de cliente** y **Método de envío de tokens de acceso** son **Básico** y **Encabezado de autorización** respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1052f-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="1052f-138">Estos valores se configuran en esta sección del formulario, junto con el **Ámbito predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="1052f-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="1052f-139">La sección **Credenciales de cliente** contiene el **Id. de cliente** y el **Secreto del cliente** que se obtienen durante los procesos de creación y configuración del servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="1052f-140">Al especificar el **Id. de cliente** y el **Secreto del cliente**, se genera el **uri de redirección** para el **código de autorización**.</span><span class="sxs-lookup"><span data-stu-id="1052f-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="1052f-141">Con este URI se configura la URL de respuesta en la configuración del servidor OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![Nuevo servidor][api-management-oauth2-server-4]

<span data-ttu-id="1052f-143">Si **Tipos de concesión de código de autorización** se establece en **Contraseña de propietario de recursos**, las credenciales se especifican con la sección **Credenciales de contraseña de propietario de recursos**. De no ser así, puede dejarse en blanco.</span><span class="sxs-lookup"><span data-stu-id="1052f-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![Nuevo servidor][api-management-oauth2-server-5]

<span data-ttu-id="1052f-145">Cuando complete el formulario, haga clic en **Guardar** para guardar la configuración del servidor de autorización OAuth 2.0 de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="1052f-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="1052f-146">Cuando se guarda la configuración del servidor, pueden configurarse las API para que usen estos valores, conforme a la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="1052f-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="1052f-147"><a name="step2"> </a>Configurar una API para que use la autorización de usuario OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="1052f-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="1052f-148">Haga clic en **API** en el menú **API Management** de la izquierda, en el nombre de la API en cuestión, en **Seguridad** y, después, active la casilla **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="1052f-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![Autorización de usuario][api-management-user-authorization]

<span data-ttu-id="1052f-150">Seleccione el **Servidor de autorización** que quiera en la lista desplegable y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1052f-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![Autorización de usuario][api-management-user-authorization-save]

## <span data-ttu-id="1052f-152"><a name="step3"> </a>Probar la autorización de usuario OAuth 2.0 en el portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="1052f-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="1052f-153">Tras configurar el servidor de autorización OAuth 2.0 y las API para que usen dicho servidor, puede probarlo. Para ello, vaya al portal para desarrolladores y llame a una API.</span><span class="sxs-lookup"><span data-stu-id="1052f-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="1052f-154">Haga clic en **Portal para desarrolladores** en el menú superior derecho.</span><span class="sxs-lookup"><span data-stu-id="1052f-154">Click **Developer portal** in the top right menu.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="1052f-156">Haga clic en **API** en el menú superior y seleccione **API eco**.</span><span class="sxs-lookup"><span data-stu-id="1052f-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![API eco][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="1052f-158">Si solamente tiene una API configurada o visible en su cuenta, al hacer clic en API irá directamente a las operaciones de dicha API.</span><span class="sxs-lookup"><span data-stu-id="1052f-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="1052f-159">Seleccione la operación **Recurso GET**, haga clic en **Abrir consola** y seleccione **Código de autorización** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1052f-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="1052f-161">Al seleccionar **Código de autorización** , se abre una ventana emergente con el formulario de suscripción del proveedor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1052f-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="1052f-162">En este ejemplo, Azure Active Directory ha proporcionado el formulario de suscripción.</span><span class="sxs-lookup"><span data-stu-id="1052f-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="1052f-163">Si ha deshabilitado los elementos emergentes, el explorador le solicitará que los habilite.</span><span class="sxs-lookup"><span data-stu-id="1052f-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="1052f-164">Cuando los habilite, seleccione **Código de autorización** de nuevo y se mostrará el formulario de suscripción.</span><span class="sxs-lookup"><span data-stu-id="1052f-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![Iniciar sesión][api-management-oauth2-signin]

<span data-ttu-id="1052f-166">Tras iniciar sesión, los **Encabezados de solicitud** se rellenan con el encabezado `Authorization : Bearer` que autoriza la solicitud.</span><span class="sxs-lookup"><span data-stu-id="1052f-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Token de encabezado de solicitud][api-management-request-header-token]

<span data-ttu-id="1052f-168">Llegado a este punto, puede configurar los valores que desea para los demás parámetros y enviar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="1052f-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1052f-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1052f-169">Next steps</span></span>
<span data-ttu-id="1052f-170">Para obtener más información acerca del uso de OAuth 2.0 y Administración de API, vea el siguiente vídeo y el [artículo](api-management-howto-protect-backend-with-aad.md)que lo acompaña.</span><span class="sxs-lookup"><span data-stu-id="1052f-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

