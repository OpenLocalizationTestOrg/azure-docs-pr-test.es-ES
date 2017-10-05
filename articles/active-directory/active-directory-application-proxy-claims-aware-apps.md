---
title: "Aplicaciones compatibles con notificaciones: proxy de aplicación de Azure AD | Microsoft Docs"
description: "En este artículo se explica cómo publicar aplicaciones de ASP.NET locales que acepten notificaciones ADFS para proteger el acceso remoto a sus usuarios."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="1fc52-103">Trabajo con aplicaciones para notificaciones en Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="1fc52-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="1fc52-104">Las [aplicaciones para notificaciones](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) realizan un redireccionamiento al servicio de token de seguridad (STS).</span><span class="sxs-lookup"><span data-stu-id="1fc52-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="1fc52-105">El STS solicita las credenciales del usuario a cambio de un token y, después, redirige al usuario a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fc52-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="1fc52-106">Hay varias maneras de habilitar el Proxy de aplicación para trabajar con estos redireccionamientos.</span><span class="sxs-lookup"><span data-stu-id="1fc52-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="1fc52-107">Use este artículo para configurar la implementación en las aplicaciones para notificaciones.</span><span class="sxs-lookup"><span data-stu-id="1fc52-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1fc52-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1fc52-108">Prerequisites</span></span>
<span data-ttu-id="1fc52-109">Asegúrese de que el STS al que redirige la aplicación para notificaciones está disponible fuera de la red local.</span><span class="sxs-lookup"><span data-stu-id="1fc52-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="1fc52-110">Puede habilitar el STS exponiéndolo a través de un proxy o permitiendo las conexiones externas.</span><span class="sxs-lookup"><span data-stu-id="1fc52-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="1fc52-111">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1fc52-111">Publish your application</span></span>

1. <span data-ttu-id="1fc52-112">Publique la aplicación según las instrucciones de [Publicar aplicaciones con el proxy de aplicación](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1fc52-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="1fc52-113">Vaya a la página de la aplicación en el portal y seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1fc52-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="1fc52-114">Si elige **Azure Active Directory** como **Método de autenticación previa**, seleccione **Se desactivó el inicio de sesión único de Azure AD** como **Método de autenticación interno**.</span><span class="sxs-lookup"><span data-stu-id="1fc52-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="1fc52-115">Si elige **Paso a través** como **Método de autenticación previa**, no necesita realizar ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="1fc52-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="1fc52-116">Configuración de AD FS</span><span class="sxs-lookup"><span data-stu-id="1fc52-116">Configure ADFS</span></span>

<span data-ttu-id="1fc52-117">Puede configurar AD FS en aplicaciones para notificaciones de alguna de estas dos formas.</span><span class="sxs-lookup"><span data-stu-id="1fc52-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="1fc52-118">La primera consiste en usar dominios personalizados.</span><span class="sxs-lookup"><span data-stu-id="1fc52-118">The first is by using custom domains.</span></span> <span data-ttu-id="1fc52-119">La segunda es con WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="1fc52-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="1fc52-120">Opción 1: dominios personalizados</span><span class="sxs-lookup"><span data-stu-id="1fc52-120">Option 1: Custom domains</span></span>

<span data-ttu-id="1fc52-121">Si todas las direcciones URL internas de las aplicaciones son nombres de dominio completos, entonces puede configurar los [dominios personalizados](active-directory-application-proxy-custom-domains.md) de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1fc52-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="1fc52-122">Use los dominios personalizados para crear direcciones URL externas que sean las mismas que las direcciones URL internas.</span><span class="sxs-lookup"><span data-stu-id="1fc52-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="1fc52-123">Cuando las direcciones URL externas coinciden con las direcciones URL internas, las redirecciones de STS funcionan independientemente de que los usuarios estén en una ubicación local o remota.</span><span class="sxs-lookup"><span data-stu-id="1fc52-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="1fc52-124">Opción 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="1fc52-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="1fc52-125">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="1fc52-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="1fc52-126">Vaya a **Relying Party Trusts** (Relaciones de confianza de usuarios de confianza), haga clic con el botón derecho en la aplicación que va a publicar con el proxy de aplicación y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="1fc52-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Relaciones de confianza para usuario autenticado: haga clic con el botón derecho en el nombre de la aplicación (captura de pantalla)](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="1fc52-128">En la pestaña **Puntos de conexión**, en **Tipo de punto de conexión**, seleccione **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="1fc52-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="1fc52-129">En **URL de confianza**, escriba la dirección URL especificada en el Proxy de aplicación en **Dirección URL externa** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1fc52-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Agregar un extremo: establezca el valor de Dirección URL de confianza - captura de pantalla](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="1fc52-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1fc52-131">Next steps</span></span>
* <span data-ttu-id="1fc52-132">[Habilitar el inicio de sesión único](application-proxy-sso-overview.md) para las aplicaciones que no son compatibles con notificaciones</span><span class="sxs-lookup"><span data-stu-id="1fc52-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="1fc52-133">Habilitación de las aplicaciones de cliente nativo para interactuar con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="1fc52-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


