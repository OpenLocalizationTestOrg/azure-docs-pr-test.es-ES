---
title: "las cuentas de desarrollador de aaaAuthorize mediante el uso de Azure Active Directory B2C: administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthorize mediante Azure Active Directory B2C en administración de API."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="efc84-103">¿Cómo tooauthorize developer cuentas con Azure Active Directory B2C en administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="efc84-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="efc84-104">Información general</span><span class="sxs-lookup"><span data-stu-id="efc84-104">Overview</span></span>
<span data-ttu-id="efc84-105">Azure Active Directory B2C es una solución de administración de identidades en la nube, destinada a aplicaciones móviles y web orientadas al consumidor.</span><span class="sxs-lookup"><span data-stu-id="efc84-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="efc84-106">Puede usar portal para desarrolladores de toomanage acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="efc84-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="efc84-107">Esta guía se muestra hello configuración necesaria en su toointegrate de servicio de administración de API con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="efc84-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="efc84-108">Para obtener información acerca de cómo habilitar el portal para desarrolladores de acceso toohello mediante clásico Azure Active Directory, vea [cómo tooauthorize developer cuentas con Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="efc84-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="efc84-109">pasos de hello toocomplete de esta guía, debe primero tienes un toocreate del inquilino de Azure Active Directory B2C una aplicación en.</span><span class="sxs-lookup"><span data-stu-id="efc84-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="efc84-110">Además, necesita las directivas de suscripción y signin toohave listo.</span><span class="sxs-lookup"><span data-stu-id="efc84-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="efc84-111">Para más información, consulte [Introducción a Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="efc84-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="efc84-112">Autorización de cuentas de desarrollador con Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="efc84-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="efc84-113">tooget iniciado, haga clic en **portal para desarrolladores de** Hola portal de Azure para su servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="efc84-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="efc84-114">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="efc84-114">This takes you toohello API Management publisher portal.</span></span>

   ![Portal del publicador][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="efc84-116">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [empezar a trabajar con el tutorial de administración de API de Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="efc84-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="efc84-117">En hello **administración de API** menú, haga clic en **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="efc84-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="efc84-118">En hello **identidades** ficha, elija **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="efc84-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identidades externas 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="efc84-120">Tome nota de hello **dirección URL de redireccionamiento** y cambiar tooAzure B2C de Active Directory en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="efc84-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Identidades externas 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="efc84-122">Haga clic en hello **aplicaciones** botón.</span><span class="sxs-lookup"><span data-stu-id="efc84-122">Click hello **Applications** button.</span></span>

  ![Registro de una aplicación nueva 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="efc84-124">Haga clic en hello **agregar** botón aplicación toocreate un nuevo B2C de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efc84-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Registro de una aplicación nueva 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="efc84-126">Hola **nueva aplicación** hoja, escriba un nombre para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="efc84-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="efc84-127">Elija **Sí** en **Aplicación web o API Web** y elija **Sí** en **Permitir flujo implícito**.</span><span class="sxs-lookup"><span data-stu-id="efc84-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="efc84-128">A continuación, Hola copia **dirección URL de redireccionamiento** de hello **Azure Active Directory B2C** sección de hello **identidades** pestaña en el portal para desarrolladores de Hola y pegarlos en hello **Dirección URL de respuesta** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="efc84-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Registro de una aplicación nueva 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="efc84-130">Haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="efc84-130">Click hello **Create** button.</span></span> <span data-ttu-id="efc84-131">Cuando se crea la aplicación hello, aparece en hello **aplicaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="efc84-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="efc84-132">Haga clic en toosee de nombre de aplicación Hola sus detalles.</span><span class="sxs-lookup"><span data-stu-id="efc84-132">Click hello application name toosee its details.</span></span>

  ![Registro de una aplicación nueva 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="efc84-134">De hello **propiedades** hoja, Hola copia **Id. de aplicación** toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="efc84-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![Identificador de aplicación 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="efc84-136">Cambie portal para desarrolladores de toohello atrás y pegue el identificador hello en hello **Id. de cliente** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="efc84-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![Identificador de aplicación 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="efc84-138">Cambiar atrás toohello portal de Azure, haga clic en hello **claves** botón y, a continuación, haga clic en **Generate key**.</span><span class="sxs-lookup"><span data-stu-id="efc84-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="efc84-139">Haga clic en **guardar** toosave Hola Hola de configuración y la presentación **clave de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="efc84-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="efc84-140">Copie el Portapapeles de hello toohello clave.</span><span class="sxs-lookup"><span data-stu-id="efc84-140">Copy hello key toohello clipboard.</span></span>

  ![Clave de aplicación 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="efc84-142">Conmutador toohello atrás portal y pegar Hola clave del publicador en hello **secreto de cliente** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="efc84-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Clave de aplicación 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="efc84-144">Especificar nombre de dominio de hello del inquilino de Azure Active Directory B2C hello en **inquilino permite**.</span><span class="sxs-lookup"><span data-stu-id="efc84-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Inquilino permitido][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="efc84-146">Especificar hello **directiva de suscripción** y **Signin directiva**.</span><span class="sxs-lookup"><span data-stu-id="efc84-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="efc84-147">Si lo desea, también puede proporcionar hello **directiva de edición de perfil** y **políticas para restablecer la contraseña**.</span><span class="sxs-lookup"><span data-stu-id="efc84-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Directivas][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="efc84-149">Para más información sobre las directivas, consulte [Azure Active Directory B2C: marco de directivas extensible].</span><span class="sxs-lookup"><span data-stu-id="efc84-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="efc84-150">Una vez que haya especificado la configuración deseada de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="efc84-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="efc84-151">Una vez guardados los cambios de hello, los programadores pueden toocreate capaz de nuevas cuentas e inicie sesión en el portal para desarrolladores de toohello mediante Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="efc84-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="efc84-152">Registro de una cuenta de desarrollador con Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="efc84-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="efc84-153">toosign a una cuenta de desarrollador utilizando B2C Directory activa de Azure, abra una nueva ventana del explorador y vaya portal para desarrolladores de toohello.</span><span class="sxs-lookup"><span data-stu-id="efc84-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="efc84-154">Haga clic en hello **registrarse** botón.</span><span class="sxs-lookup"><span data-stu-id="efc84-154">Click hello **Sign up** button.</span></span>

   ![Portal para desarrolladores 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="efc84-156">Elija toosign con **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="efc84-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Portal para desarrolladores 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="efc84-158">Está redirigido toohello directiva de suscripción que configuró en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="efc84-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="efc84-159">Elegir toosign mediante su dirección de correo electrónico o una de las cuentas existentes sociales.</span><span class="sxs-lookup"><span data-stu-id="efc84-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="efc84-160">Si Azure Active Directory B2C es Hola única opción habilitada en hello **identidades** ficha en el portal para desarrolladores de hello, podrá toohello redirigida directiva de suscripción directamente.</span><span class="sxs-lookup"><span data-stu-id="efc84-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![portal para desarrolladores][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="efc84-162">Una vez completada signup hello, está portal para desarrolladores de toohello atrás redirigida.</span><span class="sxs-lookup"><span data-stu-id="efc84-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="efc84-163">Ahora ha iniciado sesión en el portal para desarrolladores de toohello para la instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="efc84-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Registro completado][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="efc84-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efc84-165">Next steps</span></span>

*  <span data-ttu-id="efc84-166">[Introducción a Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="efc84-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="efc84-167">[Azure Active Directory B2C: marco de directivas extensible]</span><span class="sxs-lookup"><span data-stu-id="efc84-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="efc84-168">[Uso de una cuenta Microsoft como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="efc84-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="efc84-169">[Uso de una cuenta de Google como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="efc84-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="efc84-170">[Uso de una cuenta de LinkedIn como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="efc84-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="efc84-171">[Uso de una cuenta de Facebook como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="efc84-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

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
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Introducción a Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[cómo tooauthorize developer cuentas con Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: marco de directivas extensible]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Uso de una cuenta Microsoft como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Uso de una cuenta de Google como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Uso de una cuenta de Facebook como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Uso de una cuenta de LinkedIn como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
