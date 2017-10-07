---
title: "las cuentas de desarrollador aaaAuthorize mediante OAuth 2.0 en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthorize mediante OAuth 2.0 en administración de API."
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
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="0e59f-103">Cómo tooauthorize developer cuentas con OAuth 2.0 en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="0e59f-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="0e59f-104">Muchas API admiten [OAuth 2.0](http://oauth.net/2/) toosecure Hola API y asegúrese de que sólo los usuarios válidos tienen acceso y sólo puede tener acceso a recursos toowhich que tienen derecho.</span><span class="sxs-lookup"><span data-stu-id="0e59f-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="0e59f-105">En consola para desarrolladores interactiva de administración de API de orden toouse Azure con estas API, Hola servicio le permite tooconfigure su toowork de la instancia de servicio con su OAuth 2.0 habilitado API.</span><span class="sxs-lookup"><span data-stu-id="0e59f-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="0e59f-106"><a name="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e59f-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="0e59f-107">Esta guía le mostrará cómo tooconfigure su toouse de instancia de servicio de administración de API autorización de OAuth 2.0 para desarrolladores de cuentas, pero no muestra cómo el proveedor de tooconfigure un OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="0e59f-108">configuración de Hola para cada proveedor es diferente, aunque Hola pasos son similares, y partes de hello necesaria de información que se usa para configurar OAuth 2.0 en su instancia de servicio de administración de API de OAuth 2.0 Hola igual.</span><span class="sxs-lookup"><span data-stu-id="0e59f-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="0e59f-109">Este tema muestra ejemplos donde Azure Active Directory actúa como proveedor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="0e59f-110">Para obtener más información sobre la configuración de OAuth 2.0 con Azure Active Directory, vea hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0e59f-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="0e59f-111"><a name="step1"></a>Configurar un servidor de autorización OAuth 2.0 en Administración de API</span><span class="sxs-lookup"><span data-stu-id="0e59f-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="0e59f-112">tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="0e59f-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="0e59f-114">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="0e59f-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="0e59f-115">Haga clic en **seguridad** de hello **administración de API** menú hello, haga clic en **OAuth 2.0**y, a continuación, haga clic en **Agregar servidor de autorización**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="0e59f-117">Después de hacer clic **Agregar servidor de autorización**, se muestra el formulario de servidor de autorización nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="0e59f-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Nuevo servidor][api-management-oauth2-server-1]

<span data-ttu-id="0e59f-119">Escriba un nombre y una descripción opcional en hello **nombre** y **descripción** campos.</span><span class="sxs-lookup"><span data-stu-id="0e59f-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e59f-120">Estos campos son servidor de autorización de hello OAuth 2.0 tooidentify utilizados dentro de la instancia del servicio de administración de API actual de Hola y sus valores no proceden de servidor hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="0e59f-121">Escriba hello **dirección URL de página de registro de cliente**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="0e59f-122">Esta página es donde los usuarios pueden crear y administrar sus cuentas y varía en función de proveedor de hello OAuth 2.0 que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="0e59f-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="0e59f-123">Hola **dirección URL de página de registro de cliente** puntos de toohello página que los usuarios pueden usar toocreate y configurar sus propias cuentas para los proveedores de OAuth 2.0 que admiten la administración de usuarios de cuentas.</span><span class="sxs-lookup"><span data-stu-id="0e59f-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="0e59f-124">Algunas organizaciones no configurar ni utilizar esta funcionalidad, incluso si el proveedor de hello OAuth 2.0 lo admite.</span><span class="sxs-lookup"><span data-stu-id="0e59f-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="0e59f-125">Si el proveedor de OAuth 2.0 no tiene administración de usuarios de cuentas configuradas, escriba una marcador de posición URL aquí como dirección URL de Hola de su empresa, o una dirección URL como `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="0e59f-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="0e59f-126">Hola siguiente sección de formulario de hello contiene hello **tipos de concesión de código de autorización**, **dirección URL del extremo de autorización**, y **método de solicitud de autorización** configuración.</span><span class="sxs-lookup"><span data-stu-id="0e59f-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nuevo servidor][api-management-oauth2-server-2]

<span data-ttu-id="0e59f-128">Especificar hello **tipos de concesión de código de autorización** mediante la comprobación de tipos de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="0e59f-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="0e59f-129">**Código de autorización** se especifica de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0e59f-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="0e59f-130">Escriba hello **dirección URL del extremo de autorización**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="0e59f-131">Para Azure Active Directory, esta URL será similar toohello después de la dirección URL, donde `<client_id>` se reemplaza con el Id. de cliente de Hola que identifica el servidor de aplicaciones toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="0e59f-132">Hola **método de solicitud de autorización** especifica la solicitud de autorización de Hola se envía server toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="0e59f-133">El valor predeterminado es **GET** .</span><span class="sxs-lookup"><span data-stu-id="0e59f-133">By default **GET** is selected.</span></span>

<span data-ttu-id="0e59f-134">Hola siguiente sección es donde hello **dirección URL del extremo de Token**, **métodos de autenticación de cliente**, **token de acceso de método de envío**, y **ámbitopredeterminado** se especifican.</span><span class="sxs-lookup"><span data-stu-id="0e59f-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nuevo servidor][api-management-oauth2-server-3]

<span data-ttu-id="0e59f-136">Para un servidor de Azure Active Directory OAuth 2.0, Hola **dirección URL del extremo de Token** tendrá Hola siguiendo el formato, donde `<APPID>` tiene el formato de Hola de `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="0e59f-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="0e59f-137">Hola configuración predeterminada para **métodos de autenticación de cliente** es **básica**, y **token de acceso de método de envío** es **encabezado de autorización**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="0e59f-138">Estos valores se configuran en esta sección del formulario de hello, junto con hello **ámbito predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="0e59f-139">Hola **las credenciales de cliente** sección contiene Hola **Id. de cliente** y **secreto de cliente**, que se obtiene durante el proceso de creación y configuración de Hola de su OAuth 2.0 servidor.</span><span class="sxs-lookup"><span data-stu-id="0e59f-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="0e59f-140">Una vez Hola **Id. de cliente** y **secreto de cliente** se especifican, hello **redirect_uri** para hello **código de autorización** se genera.</span><span class="sxs-lookup"><span data-stu-id="0e59f-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="0e59f-141">Este URI es la dirección URL de respuesta de hello tooconfigure usado en la configuración del servidor de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Nuevo servidor][api-management-oauth2-server-4]

<span data-ttu-id="0e59f-143">Si **tipos de concesión de código de autorización** se establece demasiado**contraseña de propietario de recurso**, hello **credenciales de contraseña de propietario de recurso** sección es toospecify usa las credenciales; en caso contrario, puede dejarlo en blanco.</span><span class="sxs-lookup"><span data-stu-id="0e59f-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Nuevo servidor][api-management-oauth2-server-5]

<span data-ttu-id="0e59f-145">Una vez completada la forma de hello, haga clic en **guardar** configuración del servidor de autorización de toosave Hola API administración OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="0e59f-146">Una vez que se guarda la configuración del servidor hello, puede configurar las API toouse esta configuración, tal y como se muestra en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e59f-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="0e59f-147"><a name="step2"></a>Configurar un toouse API autorización de usuario de OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="0e59f-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="0e59f-148">Haga clic en **API** de hello **administración de API** menú Hola izquierda, haga clic en nombre de Hola de API de hello deseado, haga clic en **seguridad**y, a continuación, active casilla de Hola de **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Autorización de usuario][api-management-user-authorization]

<span data-ttu-id="0e59f-150">Seleccione Hola deseado **servidor de autorización** desde la lista desplegable de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Autorización de usuario][api-management-user-authorization-save]

## <span data-ttu-id="0e59f-152"><a name="step3"></a>Probar la autorización del usuario hello OAuth 2.0 en hello Portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="0e59f-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="0e59f-153">Una vez configurado el servidor de autorización de OAuth 2.0 y configura su toouse API ese servidor, puede probarlo va toohello Portal para desarrolladores y llamando a una API.</span><span class="sxs-lookup"><span data-stu-id="0e59f-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="0e59f-154">Haga clic en **portal para desarrolladores de** en el menú superior derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e59f-154">Click **Developer portal** in hello top right menu.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="0e59f-156">Haga clic en **API** en el menú superior de Hola y seleccione **API de eco**.</span><span class="sxs-lookup"><span data-stu-id="0e59f-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![API eco][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="0e59f-158">Si tiene sólo una API configurada o cuenta tooyour visible, a continuación, haga clic en las API le lleva directamente operaciones toohello para la API.</span><span class="sxs-lookup"><span data-stu-id="0e59f-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="0e59f-159">Seleccione hello **obtener recursos** operación, haga clic en **abrir la consola de**y, a continuación, seleccione **código de autorización** en Hola de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="0e59f-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="0e59f-161">Cuando **código de autorización** está seleccionado, se muestra una ventana emergente con forma de inicio de sesión de hello del proveedor de hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e59f-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="0e59f-162">En este ejemplo se proporciona formulario de inicio de sesión de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e59f-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="0e59f-163">Si tiene elementos emergentes deshabilitado estará solicita tooenable les explorador Hola.</span><span class="sxs-lookup"><span data-stu-id="0e59f-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="0e59f-164">Después de habilitarlas, seleccione **código de autorización** nuevo y Hola se mostrará el formulario de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0e59f-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![Iniciar sesión][api-management-oauth2-signin]

<span data-ttu-id="0e59f-166">Una vez que haya iniciado sesión, Hola **encabezados de solicitud** se rellenan con un `Authorization : Bearer` encabezado que autoriza la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0e59f-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Token de encabezado de solicitud][api-management-request-header-token]

<span data-ttu-id="0e59f-168">En este momento puede configurar los valores de hello deseado de los parámetros restantes de Hola y enviar solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="0e59f-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0e59f-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e59f-169">Next steps</span></span>
<span data-ttu-id="0e59f-170">Para obtener más información sobre el uso de OAuth 2.0 y administración de API, consulte el siguiente de Hola que lo acompaña y vídeo [artículo](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="0e59f-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

