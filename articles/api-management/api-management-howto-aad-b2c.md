---
title: "Autorización de las cuentas de desarrollador mediante Azure Active Directory B2C - Azure API Management | Microsoft Docs"
description: Aprenda a autorizar a los usuarios para que usen Azure Active Directory B2C en API Management.
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
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="39d65-103">Procedimiento para autorizar a las cuentas de desarrollador para que usen Azure Active Directory B2C en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="39d65-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="39d65-104">Información general</span><span class="sxs-lookup"><span data-stu-id="39d65-104">Overview</span></span>
<span data-ttu-id="39d65-105">Azure Active Directory B2C es una solución de administración de identidades en la nube, destinada a aplicaciones móviles y web orientadas al consumidor.</span><span class="sxs-lookup"><span data-stu-id="39d65-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="39d65-106">Puede usarlo para administrar el acceso a su portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="39d65-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="39d65-107">Esta guía le muestra la configuración que se necesita en el servicio de API Management para integrarse con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="39d65-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="39d65-108">Para más información sobre cómo habilitar el acceso al portal para desarrolladores con Azure Active Directory clásico, consulte [Procedimiento para autorizar a las cuentas de desarrollador para que usen Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="39d65-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="39d65-109">Para completar los pasos descritos en esta guía, primero debe tener un inquilino de Azure Active Directory B2C en el que crear una aplicación.</span><span class="sxs-lookup"><span data-stu-id="39d65-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="39d65-110">Además, debe tener listas las directivas de registro e inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="39d65-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="39d65-111">Para más información, consulte [Introducción a Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="39d65-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="39d65-112">Autorización de cuentas de desarrollador con Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="39d65-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="39d65-113">Para comenzar, haga clic en **Portal para editores** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="39d65-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="39d65-114">De este modo, se abre el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="39d65-114">This takes you to the API Management publisher portal.</span></span>

   ![Portal del publicador][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="39d65-116">Si todavía no ha creado una instancia del servicio API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el [tutorial Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="39d65-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="39d65-117">En el menú **API Management**, haga clic en **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="39d65-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="39d65-118">En la pestaña **Identidades**, elija **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="39d65-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identidades externas 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="39d65-120">Anote la **URL de redireccionamiento** y cambie a Azure Active Directory B2C en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="39d65-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Identidades externas 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="39d65-122">Haga clic en el botón **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="39d65-122">Click the **Applications** button.</span></span>

  ![Registro de una aplicación nueva 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="39d65-124">Haga clic en el botón **Agregar** para crear una nueva aplicación de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="39d65-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Registro de una aplicación nueva 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="39d65-126">En la hoja **Nueva aplicación**, escriba un nombre para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="39d65-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="39d65-127">Elija **Sí** en **Aplicación web o API Web** y elija **Sí** en **Permitir flujo implícito**.</span><span class="sxs-lookup"><span data-stu-id="39d65-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="39d65-128">Después, copie la **URL de redireccionamiento** de la sección **Azure Active Directory B2C** de la pestaña **Identidades** del portal del publicador y péguela en el cuadro de texto **Dirección URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="39d65-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Registro de una aplicación nueva 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="39d65-130">Haga clic en el botón **Crear** .</span><span class="sxs-lookup"><span data-stu-id="39d65-130">Click the **Create** button.</span></span> <span data-ttu-id="39d65-131">Cuando se crea la aplicación, aparece en la hoja **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="39d65-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="39d65-132">Haga clic en el nombre de la aplicación para ver sus detalles.</span><span class="sxs-lookup"><span data-stu-id="39d65-132">Click the application name to see its details.</span></span>

  ![Registro de una aplicación nueva 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="39d65-134">En la hoja **Propiedades**, copie el **identificador de aplicación** en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="39d65-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![Identificador de aplicación 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="39d65-136">Vuelva al portal del publicador y pegue el identificador en el cuadro de texto **Id. de cliente**.</span><span class="sxs-lookup"><span data-stu-id="39d65-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![Identificador de aplicación 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="39d65-138">Vuelva a Azure Portal, haga clic en el botón **Claves** y, luego, haga clic en **Generar clave**.</span><span class="sxs-lookup"><span data-stu-id="39d65-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="39d65-139">Haga clic en **Guardar** para guardar la configuración y mostrar la **clave de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="39d65-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="39d65-140">Copie la clave en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="39d65-140">Copy the key to the clipboard.</span></span>

  ![Clave de aplicación 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="39d65-142">Vuelva al portal del publicador y pegue la clave en el cuadro de texto **Secreto del cliente** .</span><span class="sxs-lookup"><span data-stu-id="39d65-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Clave de aplicación 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="39d65-144">Especifique el nombre de dominio del inquilino de Azure Active Directory B2C en **Inquilino permitido**.</span><span class="sxs-lookup"><span data-stu-id="39d65-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Inquilino permitido][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="39d65-146">Especifique la **directiva de suscripción** y la **directiva de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="39d65-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="39d65-147">Si lo desea, también puede proporcionar la **directiva de edición de perfil** y la **directiva de restablecimiento de contraseña**.</span><span class="sxs-lookup"><span data-stu-id="39d65-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Directivas][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="39d65-149">Para más información sobre las directivas, consulte [Azure Active Directory B2C: marco de directivas extensible].</span><span class="sxs-lookup"><span data-stu-id="39d65-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="39d65-150">Una vez que especifique la configuración deseada, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="39d65-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="39d65-151">Una vez que se guardan los cambios, los desarrolladores podrán crear cuentas nuevas e iniciar sesión en el portal para desarrolladores con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="39d65-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="39d65-152">Registro de una cuenta de desarrollador con Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="39d65-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="39d65-153">Para registrar una cuenta de desarrollador con Azure Active Directory B2C, abra una nueva ventana del explorador y vaya al portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="39d65-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="39d65-154">Haga clic en el botón **Registrarse**.</span><span class="sxs-lookup"><span data-stu-id="39d65-154">Click the **Sign up** button.</span></span>

   ![Portal para desarrolladores 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="39d65-156">Elija registrarse con **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="39d65-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Portal para desarrolladores 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="39d65-158">Se le redirigirá a la directiva de registro que configuró en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="39d65-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="39d65-159">Elija registrarse con la dirección de correo electrónico o una de sus cuentas sociales existentes.</span><span class="sxs-lookup"><span data-stu-id="39d65-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39d65-160">Si Azure Active Directory B2C es la única opción habilitada en la pestaña **Identidades** del portal para editores, se le redirigirá a la directiva de registro de forma directa.</span><span class="sxs-lookup"><span data-stu-id="39d65-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![portal para desarrolladores][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="39d65-162">Una vez completado el registro, se le redirigirá de nuevo al portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="39d65-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="39d65-163">Ahora ya inició sesión en el portal para desarrolladores de la instancia del servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="39d65-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Registro completado][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="39d65-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39d65-165">Next steps</span></span>

*  <span data-ttu-id="39d65-166">[Introducción a Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="39d65-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="39d65-167">[Azure Active Directory B2C: marco de directivas extensible]</span><span class="sxs-lookup"><span data-stu-id="39d65-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="39d65-168">[Uso de una cuenta Microsoft como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="39d65-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="39d65-169">[Uso de una cuenta de Google como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="39d65-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="39d65-170">[Uso de una cuenta de LinkedIn como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="39d65-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="39d65-171">[Uso de una cuenta de Facebook como proveedor de identidades en Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="39d65-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
<span data-ttu-id="39d65-172">[Introducción a Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="39d65-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="39d65-173">[Procedimiento para autorizar a las cuentas de desarrollador para que usen Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="39d65-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="39d65-174">[Azure Active Directory B2C: marco de directivas extensible]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="39d65-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="39d65-175">[Uso de una cuenta Microsoft como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="39d65-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="39d65-176">[Uso de una cuenta de Google como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="39d65-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="39d65-177">[Uso de una cuenta de Facebook como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="39d65-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="39d65-178">[Uso de una cuenta de LinkedIn como proveedor de identidades en Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="39d65-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account