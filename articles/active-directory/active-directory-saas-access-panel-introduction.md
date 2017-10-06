---
title: "¿aaaWhat es el panel de acceso de hello en Azure Active Directory? | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse variaciones del programa Hola a tener acceso a aplicaciones SaaS del panel (explorador web, aplicación de Android, aplicación de iPhone y iPad) tooaccess."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>¿Qué es el panel de acceso de hello?

panel de acceso de Hello es un portal basado en web. Permite que un usuario con un trabajo o cuenta del centro educativo en aplicaciones de Azure Active Directory tooview y de inicio en la nube un administrador de Azure AD le haya concedido acceso a. También puede usar grupos de autoservicio y las capacidades de administración de aplicaciones a través del panel de acceso de Hola.

panel de acceso de Hola se es independiente de hello portal de Azure y realiza no has sido tu toohave una suscripción de Azure.

![Panel de acceso][1]

panel de acceso de Hello permite tooedit parte de la configuración del perfil, incluidos Hola capacidad:

- Cambiar la contraseña de hello asociado a una cuenta profesional o educativa

- Editar configuración de restablecimiento de contraseña

- Editar contacto y autenticación de factor de toomulti relacionadas de la configuración de preferencias (para las cuentas que se han toouse requiere que un administrador)

- Ver detalles de la cuenta, como el identificador de usuario, el correo electrónico alternativo, y los números de teléfono móvil y del trabajo.

- Ver e iniciar aplicaciones de basado en la nube que Hola Administrador de Azure AD le haya concedido acceso a. Para obtener más información acerca del panel de acceso de Hola desde la perspectiva de los usuarios de hello, consulte uso de panel de acceso de Hola. 

- Autoadministrar grupos. Más específicamente, el Administrador de Hola puede crear y administrar grupos de seguridad y solicitar suscripciones a grupos de seguridad en Azure AD. Para más información, consulte [Configuración de Azure Active Directory para la administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md) y [Administración del acceso a los recursos con grupos de Azure Active Directory](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Al tener acceso al panel de acceso de Hola

Puede obtener acceso al panel de acceso de hello visitando Hola siguiente dirección URL en un explorador web:`http://myapps.microsoft.com`

Si tiene la configuración de la página de inicio de sesión de marca personalizada, puede cargar esta personalización de marca mediante la anexión de final de toohello de dominio de su organización de dirección URL de hello:`http://myapps.microsoft.com/<your domain>.com`

En este caso, se puede utilizar cualquier nombre de dominio activo o comprobado que se haya configurado en Azure Portal.

![Nombre de dominio de Wingtip Toys][2]  

Necesita toodistribute Hola URL tooall a los usuarios que iniciarán sesión en tooapplications que se integran con Azure AD.

## <a name="authentication"></a>Autenticación

panel de acceso de hello tooreach, se debe autenticar a través de una cuenta profesional o educativa en Azure AD. Puede ser autenticado tooAzure AD directamente. Además, si una organización configuró la federación mediante Servicios de federación de Active Directory (AD FS) u otras tecnologías, Windows Server Active Directory puede autenticar a los usuarios.

Si tiene una suscripción de Azure u Office 365 y ha estado utilizando Hola portal de Azure o una aplicación de Office 365, puede ver lista de Hola de aplicaciones sin firmar de nuevo. No se autentican si eres están toosign solicitada en mediante Hola username y password para su cuenta de Azure AD. Si su organización ha configurado federación, escriba el nombre de usuario de hello es suficiente.

Cuando se autentique, puede interactuar con las aplicaciones de Hola que el administrador ha integrado con el directorio de Hola. toolearn toointegrate aplicaciones con Azure AD, vea [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Requisitos del explorador web

Como mínimo, panel de acceso de hello requiere un explorador que admita JavaScript y se han habilitado de CSS. Para el usuario de hello toobe firmado en tooapplications a través de basada en contraseña de inicio de sesión único (SSO), extensión del panel de acceso de hello debe instalarse en el explorador. extensión de Hola se descarga automáticamente cuando se selecciona una aplicación que está configurada para el SSO basado en contraseña.

extensión del panel de acceso de Hello está actualmente disponible para Internet Explorer 8 y versiones posteriores, Edge, Chrome y Firefox los exploradores.

## <a name="mobile-app-support"></a>Compatibilidad para aplicación móvil

equipo de Azure Active Directory Hola publica Hola mi aplicación móvil de aplicaciones. Cuando se instala la aplicación hello, puede iniciar sesión en aplicaciones de SSO basada en toopassword en dispositivos iOS y Android.

> [!NOTE]
> Puede iniciar sesión tooapplications que admitan una federación con Azure AD (incluyendo Salesforce, Google Apps, Dropbox, cuadro, Concur, Workday, Office 365 y otras más de 70 más) en prácticamente cualquier explorador web, en cualquier dispositivo, sin necesidad de una aplicación de complemento o móvil. Todos los demás [tener acceso a las experiencias de panel](https://myapps.microsoft.com/) también no requieren Hola mi toobe de aplicación móvil de las aplicaciones que se usa en un dispositivo móvil.
>
>

### <a name="my-apps-for-android"></a>Mis aplicaciones para Android

Mis aplicaciones para Android es compatible con cualquier dispositivo Android que ejecute la versión 4.1 o posterior de Android.  
Está disponible en hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![Mis aplicaciones para Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>Mis aplicaciones para iPhone y iPad

Mis aplicaciones para iOS es compatible con cualquier dispositivo iPhone o iPad que ejecute la versión 7 o posterior de iOS.  
Está disponible en hello [App Store de Apple](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![Mis aplicaciones para iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Explorador administrado para Mis aplicaciones

Mis aplicaciones también se integra en hello Intune Managed Browser. Hola Intune Managed Browser para dispositivos iOS y Android desempeña un papel clave para garantizar que los datos en dispositivos móviles se mantienen seguros. Asimismo, permite ver y explorar páginas web que podrían contener información de la compañía, además de proporcionar una experiencia de exploración web segura.  
Buscar aplicaciones de toomy de acceso rápido en la página principal del explorador administrado y en los marcadores, lo que le proporciona menos hace clic en tooreach cualquier aplicación que desee tooaccess.

Está disponible en hello [App Store de Apple](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) y [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Explorador administrado para Mis aplicaciones][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Sugerencias para la experiencia del usuario de prueba Hola

Si es un administrador de Azure y ha iniciado sesión toohello portal de Azure con una cuenta en el directorio de hello, están firmados automáticamente en el panel de acceso toohello como su cuenta actual. En este caso, puede ver todas las aplicaciones que se han asignado tooyou.

**tootest como un *diferentes* cuenta de usuario:**

1. Haga clic en el menú de usuario de hello en la esquina superior derecha de Hola de Hola portal de Azure o panel de acceso de hello y, a continuación, seleccione **cerrar sesión**. 
2. Vaya toohello [panel de acceso](http://myapps.microsoft.com).
3. En la página de inicio de sesión de hello, el nombre de usuario de tipo hello y contraseña de cuenta de hello en el directorio que desee tootest.


## <a name="starting-applications"></a>Inicio de aplicaciones

Varios tipos de aplicaciones pueden aparecer en el panel de acceso de Hola.

### <a name="office-365-applications"></a>Aplicaciones de Office 365

Si su organización utiliza aplicaciones de Office 365 y que están autorizados para ellos, las aplicaciones de Office 365 Hola aparecen en el panel de acceso.

Al hacer clic en una ventana de aplicación para una aplicación de Office 365, son toohello redirigido automáticamente con la sesión iniciada y aplicación.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación

El administrador puede agregar aplicaciones en la sección de Active Directory del portal de Azure Hola Hola con modo SSO de hello establecido demasiado**Azure AD Single Sign-On**. Solamente puede ver estas aplicaciones si el administrador haya concedido explícitamente que acceso toohello aplicaciones.

Al hacer clic en un icono para una de estas aplicaciones, se redirigen y toohello aplicación inicia sesión automáticamente.

### <a name="password-based-sso-without-identity-provisioning"></a>SSO basado en contraseña sin aprovisionamiento de identidad

El administrador puede agregar aplicaciones en la sección de Active Directory del portal de Azure Hola Hola con modo SSO de hello establecido demasiado**basado en contraseña Single Sign-On**. Todos los usuarios en el directorio de hello pueden ver todas las aplicaciones que se han configurado en este modo.

Hello primera vez, hace clic en un icono para una de estas aplicaciones, son tooinstall solicitadas Hola complemento para Internet Explorer o Chrome SSO de contraseña. instalación de Hello puede requerir toorestart el explorador web. Al devolver el panel de acceso de toohello y haga clic en icono de aplicación Hola de nuevo, se le solicitará un nombre de usuario y una contraseña para la aplicación hello. Una vez haya escrito el nombre de usuario y la contraseña, estas credenciales se almacenan de forma segura y vinculan tooyour cuenta en Azure AD.

Hola próxima vez que haga clic en ventana de la aplicación hello, iniciará sesión automáticamente en la aplicación toohello.  
No tiene tooenter sus credenciales de nuevo y o instalar Hola complemento SSO de contraseña.

Si han cambiado sus credenciales en la aplicación de terceros de destino de hello, también debe actualizar las credenciales que se almacenan en Azure AD. 

**credenciales de tooupdate:**

1. Seleccione el icono de hello en la ventana de la aplicación hello.
2. Seleccione **Actualizar credenciales** Hola a tooreenter Hola username y la contraseña de aplicación.


### <a name="password-based-sso-with-identity-provisioning"></a>SSO basado en contraseña con aprovisionamiento de identidad

El administrador puede agregar aplicaciones en hello **Active Directory** sección del portal de Azure con el modo SSO de Hola Hola establecido demasiado**basado en contraseña Single Sign-On**, junto con el aprovisionamiento de identidad.

Hello primera vez, hace clic en una ventana de aplicación para una de estas aplicaciones, son tooinstall solicitadas hello **SSO de contraseña complemento para Internet Explorer o Chrome**. instalación de Hello puede requerir toorestart el explorador web.  
Al devolver el panel de acceso de toohello y haga clic en icono de aplicación Hola de nuevo, iniciará sesión automáticamente en la aplicación toohello.

Algunas aplicaciones pueden necesitar toochange la contraseña de inicio de sesión primero en Hola. Si han cambiado sus credenciales en la aplicación de terceros de destino de hello, también debe actualizar las credenciales de Hola que se almacenan en Azure AD. 

**credenciales de tooupdate:**

1. Seleccione el icono de hello en la ventana de la aplicación hello.
2. Seleccione **Actualizar credenciales** Hola a tooreenter Hola username y la contraseña de aplicación.


### <a name="application-with-existing-sso-solutions"></a>Aplicación con soluciones SSO existentes

tooconfigure SSO para una aplicación, Hola portal de Azure proporciona una tercera opción llama **existente Single Sign-On**. Esta opción permite la toocreate administrador una aplicación de tooan de vínculo y lo coloca en el panel de acceso de Hola para los usuarios seleccionados.

Por ejemplo, si una aplicación está configurada tooauthenticate a los usuarios mediante AD FS 2.0, el administrador puede usar hello **existente Single Sign-On** opción toocreate un tooit de vínculo en el panel de acceso de Hola. Cuando se tiene acceso el vínculo de hello, se autentican a través de AD FS 2.0 o cualquier aplicación de Hola de solución SSO existente proporciona.


## <a name="next-steps"></a>Pasos siguientes

- toosee una lista de todos los temas que son la administración de tooapplication relacionados, vea hello [índice de artículos para la administración de la aplicación en Azure Active Directory](active-directory-apps-index.md).
 
- toolearn toointegrate una aplicación SaaS en Azure AD, vea hello [lista de tutoriales sobre cómo las aplicaciones de SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn más información acerca de la administración de aplicaciones con Azure AD, vea hello [Introducción toosingle-inicio de sesión y administrar el acceso a la aplicación con Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn más información acerca de aprovisionamiento de usuarios, consulte [automatizar el aprovisionamiento de usuarios y la cancelación de las aplicaciones de tooSaaS](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
