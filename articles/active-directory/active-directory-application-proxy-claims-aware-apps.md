---
title: "aplicaciones con reconocimiento de aaaClaims - Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "¿Cómo toopublish local de las aplicaciones de ASP.NET que aceptan notificaciones ADFS para proteger el acceso remoto por los usuarios."
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
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="ca258-103">Trabajo con aplicaciones para notificaciones en Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="ca258-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="ca258-104">[Aplicaciones para notificaciones](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) realizar un servicio de Token de seguridad (STS) de toohello de redirección.</span><span class="sxs-lookup"><span data-stu-id="ca258-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="ca258-105">Hola STS solicita las credenciales de usuario de Hola a cambio de un token y, a continuación, redirige aplicación toohello de hello usuario.</span><span class="sxs-lookup"><span data-stu-id="ca258-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="ca258-106">Hay algunas maneras tooenable Proxy de aplicación toowork con estas redirecciones.</span><span class="sxs-lookup"><span data-stu-id="ca258-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="ca258-107">Use este artículo tooconfigure la implementación para las aplicaciones para notificaciones.</span><span class="sxs-lookup"><span data-stu-id="ca258-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ca258-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ca258-108">Prerequisites</span></span>
<span data-ttu-id="ca258-109">Asegúrese de que ese Hola STS que Hola aplicación para notificaciones redirige toois disponible fuera de la red local.</span><span class="sxs-lookup"><span data-stu-id="ca258-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="ca258-110">Puede hacer Hola STS disponibles mediante la exposición a través de un proxy o puede permitir que fuera de las conexiones.</span><span class="sxs-lookup"><span data-stu-id="ca258-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="ca258-111">Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ca258-111">Publish your application</span></span>

1. <span data-ttu-id="ca258-112">Publicar su aplicación según las instrucciones de toohello descritas en [publicar aplicaciones con Proxy de aplicación](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca258-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="ca258-113">Navegar por la página de aplicación toohello Hola portal y seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ca258-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="ca258-114">Si elige **Azure Active Directory** como **Método de autenticación previa**, seleccione **Se desactivó el inicio de sesión único de Azure AD** como **Método de autenticación interno**.</span><span class="sxs-lookup"><span data-stu-id="ca258-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="ca258-115">Si ha elegido **Passthrough** como su **método de autenticación previa**, no es necesario toochange nada.</span><span class="sxs-lookup"><span data-stu-id="ca258-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="ca258-116">Configuración de AD FS</span><span class="sxs-lookup"><span data-stu-id="ca258-116">Configure ADFS</span></span>

<span data-ttu-id="ca258-117">Puede configurar AD FS en aplicaciones para notificaciones de alguna de estas dos formas.</span><span class="sxs-lookup"><span data-stu-id="ca258-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="ca258-118">Hola en primer lugar es mediante el uso de dominios personalizados.</span><span class="sxs-lookup"><span data-stu-id="ca258-118">hello first is by using custom domains.</span></span> <span data-ttu-id="ca258-119">en segundo lugar es Hola con WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="ca258-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="ca258-120">Opción 1: dominios personalizados</span><span class="sxs-lookup"><span data-stu-id="ca258-120">Option 1: Custom domains</span></span>

<span data-ttu-id="ca258-121">Si todas las direcciones URL internas de Hola para las aplicaciones son nombres completos (FQDN) de nombres de dominio, puede configurar [dominios personalizados](active-directory-application-proxy-custom-domains.md) para sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ca258-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="ca258-122">Use Hola dominios personalizados toocreate direcciones URL externas que son Hola igual Hola direcciones URL internas.</span><span class="sxs-lookup"><span data-stu-id="ca258-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="ca258-123">Cuando las direcciones URL externas coincide con las direcciones URL internas, las redirecciones de STS de hello funcionar independientemente de los usuarios estén local o remoto.</span><span class="sxs-lookup"><span data-stu-id="ca258-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="ca258-124">Opción 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="ca258-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="ca258-125">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="ca258-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="ca258-126">Vaya demasiado**Veracidades**, haga doble clic en la aplicación hello se publica con el Proxy de aplicación y elija **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="ca258-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Relaciones de confianza para usuario autenticado: haga clic con el botón derecho en el nombre de la aplicación (captura de pantalla)](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="ca258-128">En hello **extremos** ficha **tipo de extremo**, seleccione **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="ca258-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="ca258-129">En **dirección URL de confianza**, escriba dirección URL de Hola que escribió en hello Proxy de aplicación en **dirección URL externa** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ca258-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Agregar un extremo: establezca el valor de Dirección URL de confianza - captura de pantalla](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="ca258-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca258-131">Next steps</span></span>
* <span data-ttu-id="ca258-132">[Habilitar el inicio de sesión único](application-proxy-sso-overview.md) para las aplicaciones que no son compatibles con notificaciones</span><span class="sxs-lookup"><span data-stu-id="ca258-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="ca258-133">Habilitar toointeract de aplicaciones de cliente nativo con aplicaciones de servidor proxy</span><span class="sxs-lookup"><span data-stu-id="ca258-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


