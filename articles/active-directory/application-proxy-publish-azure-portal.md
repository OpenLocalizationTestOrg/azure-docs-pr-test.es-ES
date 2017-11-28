---
title: "aplicaciones de aaaPublish con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Publicar en la nube local aplicaciones toohello con el Proxy de aplicación de Azure AD en hello portal de Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="feff7-103">Publicación de aplicaciones mediante el proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="feff7-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="feff7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="feff7-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="feff7-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="feff7-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="feff7-106">Proxy de aplicación de Azure Active Directory (AD) le ayuda a los trabajadores remotos mediante la publicación de toobe de aplicaciones local tiene acceso a través de hello internet.</span><span class="sxs-lookup"><span data-stu-id="feff7-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="feff7-107">Puede publicar estas aplicaciones a través de hello tooprovide portal Azure el acceso remoto seguro desde fuera de la red.</span><span class="sxs-lookup"><span data-stu-id="feff7-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="feff7-108">Este artículo le guiará a través de hello pasos toopublish una aplicación local con el Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="feff7-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="feff7-109">Después de completar este artículo, los usuarios le puede tooaccess capaz de la aplicación de forma remota.</span><span class="sxs-lookup"><span data-stu-id="feff7-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="feff7-110">Podrá tooconfigure listo con características adicionales para la aplicación hello como un único inicio de sesión, información personalizada y requisitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="feff7-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="feff7-111">Si tiene tooApplication nuevo Proxy, obtener más información sobre esta característica con el artículo hello [cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="feff7-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="feff7-112">Publicación de una aplicación local para el acceso remoto</span><span class="sxs-lookup"><span data-stu-id="feff7-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="feff7-113">Siga estos pasos toopublish sus aplicaciones con Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="feff7-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="feff7-114">Si ya no ha descargado y ha configurado un conector para su organización, vaya demasiado[empezar a trabajar con el Proxy de aplicación e instalar el conector de hello](active-directory-application-proxy-enable.md) primero y, a continuación, publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="feff7-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="feff7-115">Si va a probar los Proxy de aplicación para hello primera vez, elija una aplicación que está configurada para autenticación basada en contraseña.</span><span class="sxs-lookup"><span data-stu-id="feff7-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="feff7-116">Proxy de aplicación es compatible con otros tipos de autenticación, pero en aplicaciones basadas en contraseña son hello tooget más fácil seguridad a trabajar de inmediato.</span><span class="sxs-lookup"><span data-stu-id="feff7-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="feff7-117">Inicie sesión como administrador en hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="feff7-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="feff7-118">Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="feff7-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Adición de una aplicación empresarial](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="feff7-120">Seleccione **Todo** y, después, seleccione **Aplicación local**.</span><span class="sxs-lookup"><span data-stu-id="feff7-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Adición de su propia aplicación](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="feff7-122">Proporcionar Hola después de obtener información acerca de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="feff7-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="feff7-123">**Nombre**: nombre de Hola de aplicación Hola que va a aparecer en el panel de acceso de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="feff7-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="feff7-124">**Dirección URL interna**: Hola dirección URL que usan la aplicación de hello tooaccess desde dentro de su red privada.</span><span class="sxs-lookup"><span data-stu-id="feff7-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="feff7-125">Puede proporcionar una ruta de acceso específica de toopublish de servidor de back-end de hello, mientras está sin publicar rest Hola de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="feff7-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="feff7-126">De esta manera, puede publicar sitios diferentes en Hola el mismo servidor que las diferentes aplicaciones y asigne cada uno de sus propias reglas de acceso y nombre.</span><span class="sxs-lookup"><span data-stu-id="feff7-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="feff7-127">Si publica una ruta de acceso, asegúrese de que incluye todas las imágenes necesarias de hello, scripts y hojas de estilos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="feff7-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="feff7-128">Por ejemplo, si la aplicación está en https://yourapp/app y usa las imágenes que se encuentra en https://yourapp/media, debe publicar https://yourapp/ como ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="feff7-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="feff7-129">Esta dirección URL interna no tiene página de aterrizaje de hello toobe que verán los usuarios.</span><span class="sxs-lookup"><span data-stu-id="feff7-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="feff7-130">Para más información, consulte [Establecimiento de una página principal personalizada para aplicaciones publicadas mediante el proxy de aplicación de Azure AD](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="feff7-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="feff7-131">**Dirección URL externa**: Hola dirección los usuarios irá tooin orden tooaccess aplicación hello desde fuera de la red.</span><span class="sxs-lookup"><span data-stu-id="feff7-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="feff7-132">Si no desea dominio de Proxy de aplicación de toouse Hola predeterminado, que conozca [dominios personalizados en el Proxy de aplicación de Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="feff7-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="feff7-133">**Autenticación previa**: cómo los Proxy de aplicación comprueba los usuarios antes de concederles acceso tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="feff7-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="feff7-134">Azure Active Directory: Proxy de aplicación redirige toosign de los usuarios con Azure AD, que autentica los permisos para el directorio de Hola y de aplicación.</span><span class="sxs-lookup"><span data-stu-id="feff7-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="feff7-135">Se recomienda mantener esta opción como valor predeterminado de hello, por lo que puede aprovechar las características de seguridad de Azure AD como acceso condicional y la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="feff7-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="feff7-136">Acceso directo: Los usuarios no tengan tooauthenticate con aplicaciones de Azure Active Directory tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="feff7-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="feff7-137">Todavía puede configurar los requisitos de autenticación en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="feff7-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="feff7-138">**Grupo de conectores**: conectores proceso Hola acceso remoto tooyour aplicación y grupos de conectores que le ayudarán a organizar los conectores y las aplicaciones por región, red o propósito.</span><span class="sxs-lookup"><span data-stu-id="feff7-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="feff7-139">Si no tiene ningún grupo de conector creado todavía, la aplicación se asigna demasiado**predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="feff7-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Configuración de la aplicación](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="feff7-141">Si es necesario, configure opciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="feff7-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="feff7-142">En la mayoría de las aplicaciones, debe mantener esta configuración en su estado predeterminado.</span><span class="sxs-lookup"><span data-stu-id="feff7-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="feff7-143">**Tiempo de espera de aplicación de back-end**: establezca este valor demasiado**largo** únicamente si la aplicación es lenta tooauthenticate y conectarse.</span><span class="sxs-lookup"><span data-stu-id="feff7-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="feff7-144">**Traducir las direcciones URL en encabezados**: mantener este valor como **Sí** a menos que la aplicación requiere el encabezado de host original de hello en solicitud de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="feff7-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="feff7-145">**Traducir las direcciones URL en el cuerpo de la aplicación**: mantener este valor como **No** a menos que tienen aplicaciones locales HTML codificado vínculos tooother y no usar dominios personalizados.</span><span class="sxs-lookup"><span data-stu-id="feff7-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="feff7-146">Para más información, consulte sobre la [traducción de vínculos con el proxy de aplicación](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="feff7-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configuración de la aplicación](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="feff7-148">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="feff7-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="feff7-149">Adición de un usuario de prueba</span><span class="sxs-lookup"><span data-stu-id="feff7-149">Add a test user</span></span> 

<span data-ttu-id="feff7-150">tootest que la aplicación se publicó correctamente, agregue una cuenta de usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="feff7-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="feff7-151">Compruebe que esta cuenta ya tiene permisos tooaccess Hola aplicación desde dentro de la red corporativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="feff7-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="feff7-152">En la hoja de inicio rápido de hello, seleccione **asigna a un usuario para realizar pruebas**.</span><span class="sxs-lookup"><span data-stu-id="feff7-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Asignar un usuario de prueba](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="feff7-154">En usuarios de Hola y hoja de grupos, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="feff7-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Agregar un usuario o grupo](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="feff7-156">En la hoja de hello Agregar asignación, seleccione **usuarios y grupos** a continuación, elija la cuenta de hello desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="feff7-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="feff7-157">Seleccione **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="feff7-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="feff7-158">Prueba de la aplicación publicada</span><span class="sxs-lookup"><span data-stu-id="feff7-158">Test your published app</span></span>

<span data-ttu-id="feff7-159">En el explorador, navegue toohello dirección URL externa que configuró durante Hola publicar paso.</span><span class="sxs-lookup"><span data-stu-id="feff7-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="feff7-160">Debería ver la pantalla de inicio de Hola y ser capaz de toosign con cuenta de prueba de hello configurar.</span><span class="sxs-lookup"><span data-stu-id="feff7-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Prueba de la aplicación publicada](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="feff7-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="feff7-162">Next steps</span></span>
- <span data-ttu-id="feff7-163">[Descargar conectores](active-directory-application-proxy-enable.md) y [crear grupos de conectores](active-directory-application-proxy-connectors-azure-portal.md) toopublish aplicaciones en ubicaciones y redes independientes.</span><span class="sxs-lookup"><span data-stu-id="feff7-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="feff7-164">[Configure el inicio de sesión único](application-proxy-sso-azure-portal.md) para la aplicación publicada recientemente.</span><span class="sxs-lookup"><span data-stu-id="feff7-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
