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
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>¿Cómo tooauthorize developer cuentas con Azure Active Directory B2C en administración de API de Azure
## <a name="overview"></a>Información general
Azure Active Directory B2C es una solución de administración de identidades en la nube, destinada a aplicaciones móviles y web orientadas al consumidor. Puede usar portal para desarrolladores de toomanage acceso tooyour. Esta guía se muestra hello configuración necesaria en su toointegrate de servicio de administración de API con Azure Active Directory B2C. Para obtener información acerca de cómo habilitar el portal para desarrolladores de acceso toohello mediante clásico Azure Active Directory, vea [cómo tooauthorize developer cuentas con Azure Active Directory].

> [!NOTE]
> pasos de hello toocomplete de esta guía, debe primero tienes un toocreate del inquilino de Azure Active Directory B2C una aplicación en. Además, necesita las directivas de suscripción y signin toohave listo. Para más información, consulte [Introducción a Azure Active Directory B2C].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Autorización de cuentas de desarrollador con Azure Active Directory B2C

1. tooget iniciado, haga clic en **portal para desarrolladores de** Hola portal de Azure para su servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API.

   ![Portal del publicador][api-management-management-console]

   > [!NOTE]
   > Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [empezar a trabajar con el tutorial de administración de API de Azure][Get started with Azure API Management].

2. En hello **administración de API** menú, haga clic en **seguridad**. En hello **identidades** ficha, elija **Azure Active Directory B2C**.

  ![Identidades externas 1][api-management-howto-aad-b2c-security-tab]

3. Tome nota de hello **dirección URL de redireccionamiento** y cambiar tooAzure B2C de Active Directory en hello portal de Azure.

  ![Identidades externas 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Haga clic en hello **aplicaciones** botón.

  ![Registro de una aplicación nueva 1][api-management-howto-aad-b2c-portal-menu]

5. Haga clic en hello **agregar** botón aplicación toocreate un nuevo B2C de Azure Active Directory.

  ![Registro de una aplicación nueva 2][api-management-howto-aad-b2c-add-button]

6. Hola **nueva aplicación** hoja, escriba un nombre para la aplicación hello. Elija **Sí** en **Aplicación web o API Web** y elija **Sí** en **Permitir flujo implícito**. A continuación, Hola copia **dirección URL de redireccionamiento** de hello **Azure Active Directory B2C** sección de hello **identidades** pestaña en el portal para desarrolladores de Hola y pegarlos en hello **Dirección URL de respuesta** cuadro de texto.

  ![Registro de una aplicación nueva 3][api-management-howto-aad-b2c-app-details]

7. Haga clic en hello **crear** botón. Cuando se crea la aplicación hello, aparece en hello **aplicaciones** hoja. Haga clic en toosee de nombre de aplicación Hola sus detalles.

  ![Registro de una aplicación nueva 4][api-management-howto-aad-b2c-app-created]

8. De hello **propiedades** hoja, Hola copia **Id. de aplicación** toohello Portapapeles.

  ![Identificador de aplicación 1][api-management-howto-aad-b2c-app-id]

9. Cambie portal para desarrolladores de toohello atrás y pegue el identificador hello en hello **Id. de cliente** cuadro de texto.

  ![Identificador de aplicación 2][api-management-howto-aad-b2c-client-id]

10. Cambiar atrás toohello portal de Azure, haga clic en hello **claves** botón y, a continuación, haga clic en **Generate key**. Haga clic en **guardar** toosave Hola Hola de configuración y la presentación **clave de aplicación**. Copie el Portapapeles de hello toohello clave.

  ![Clave de aplicación 1][api-management-howto-aad-b2c-app-key]

11. Conmutador toohello atrás portal y pegar Hola clave del publicador en hello **secreto de cliente** cuadro de texto.

  ![Clave de aplicación 2][api-management-howto-aad-b2c-client-secret]

12. Especificar nombre de dominio de hello del inquilino de Azure Active Directory B2C hello en **inquilino permite**.

  ![Inquilino permitido][api-management-howto-aad-b2c-allowed-tenant]

13. Especificar hello **directiva de suscripción** y **Signin directiva**. Si lo desea, también puede proporcionar hello **directiva de edición de perfil** y **políticas para restablecer la contraseña**.

  ![Directivas][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Para más información sobre las directivas, consulte [Azure Active Directory B2C: marco de directivas extensible].

14. Una vez que haya especificado la configuración deseada de hello, haga clic en **guardar**.

  Una vez guardados los cambios de hello, los programadores pueden toocreate capaz de nuevas cuentas e inicie sesión en el portal para desarrolladores de toohello mediante Azure Active Directory B2C.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Registro de una cuenta de desarrollador con Azure Active Directory B2C

1. toosign a una cuenta de desarrollador utilizando B2C Directory activa de Azure, abra una nueva ventana del explorador y vaya portal para desarrolladores de toohello. Haga clic en hello **registrarse** botón.

   ![Portal para desarrolladores 1][api-management-howto-aad-b2c-dev-portal]

2. Elija toosign con **Azure Active Directory B2C**.

   ![Portal para desarrolladores 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Está redirigido toohello directiva de suscripción que configuró en la sección anterior de Hola. Elegir toosign mediante su dirección de correo electrónico o una de las cuentas existentes sociales.

   > [!NOTE]
   > Si Azure Active Directory B2C es Hola única opción habilitada en hello **identidades** ficha en el portal para desarrolladores de hello, podrá toohello redirigida directiva de suscripción directamente.

   ![portal para desarrolladores][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Una vez completada signup hello, está portal para desarrolladores de toohello atrás redirigida. Ahora ha iniciado sesión en el portal para desarrolladores de toohello para la instancia de servicio de administración de API.

    ![Registro completado][api-management-registration-complete]

## <a name="next-steps"></a>Pasos siguientes

*  [Introducción a Azure Active Directory B2C]
*  [Azure Active Directory B2C: marco de directivas extensible]
*  [Uso de una cuenta Microsoft como proveedor de identidades en Azure Active Directory B2C]
*  [Uso de una cuenta de Google como proveedor de identidades en Azure Active Directory B2C]
*  [Uso de una cuenta de LinkedIn como proveedor de identidades en Azure Active Directory B2C]
*  [Uso de una cuenta de Facebook como proveedor de identidades en Azure Active Directory B2C]




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
