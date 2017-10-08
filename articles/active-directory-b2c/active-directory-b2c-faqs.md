---
title: "Preguntas más frecuentes acerca de Azure AD B2C | Microsoft Docs"
description: "Preguntas más frecuentes acerca de Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: preguntas más frecuentes (P+F) 
Esta página responde a las preguntas más frecuentes sobre Hola B2C de Azure Active Directory (Azure AD). Siga comprobando si hay actualizaciones.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>¿Puedo usar las características de Azure AD B2C en mi inquilino de Azure de AD existente, basado en empleados?
Azure AD y Azure AD B2C ofertas de producto independiente y no pueden coexistir en hello mismo inquilino.  Un inquilino de Azure AD representa una organización.  Un inquilino de Azure AD B2C representa una colección de toobe de identidades que se utiliza con aplicaciones de usuario de confianza.  Con las directivas personalizadas (en vista previa pública), Azure AD B2C puede federar tooAzure AD permitir autenticación de los empleados de una organización.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>¿Puedo usar inicio de sesión social de Azure AD B2C tooprovide (Facebook y Google +) en Office 365?
Azure AD B2C no puede ser usuarios tooauthenticate usado para Microsoft Office 365.  Azure AD es la solución de Microsoft para la administración de aplicaciones de tooSaaS de acceso de empleados y tiene características diseñadas para este propósito, como el acceso condicional y de la licencia.  Azure AD B2C proporciona una plataforma de administración de identidades y acceso para la creación de aplicaciones web y móviles.  Una vez Azure AD B2C inquilino de Azure AD tooan toofederate configurado, inquilino de Azure AD Hola administra tooapplications de acceso de empleados que se basan en Azure AD B2C.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>¿Qué son las cuentas locales en Azure AD B2C? ¿En qué se distinguen de las cuentas de trabajo o educativas en Azure AD?
En un inquilino de Azure AD, los usuarios que pertenezcan toohello inquilino inicie sesión con una dirección de correo electrónico de formulario de hello `<xyz>@<tenant domain>`.  Hola `<tenant domain>` es uno de hello comprobado Hola iniciales o inquilino de dominios en hello `<...>.onmicrosoft.com` dominio. Este tipo de cuenta es una cuenta profesional o educativa.

En un inquilino de Azure AD B2C, mayoría de las aplicaciones desea usuario hello en toosign con cualquier dirección de correo electrónico arbitrario (por ejemplo, joe@comcast.net, bob@gmail.com, sarah@contoso.com, o jim@live.com). Este tipo de cuenta es una cuenta local.  También se admiten nombres de usuario arbitrarios tales como cuentas locales (por ejemplo, joe, bob, sarah o jim). Puede elegir uno de estos dos tipos de cuenta local mediante la configuración de Azure AD B2C Hola portal de Azure.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>¿Qué proveedores de identidades sociales se admiten ahora? ¿Las que hacer planear toosupport Hola futuras?
Actualmente admitimos Facebook, Google+, LinkedIn, Amazon, Twitter (versión preliminar), WeChat (versión preliminar), Weibo (versión preliminar) y QQ (versión preliminar). Agregaremos compatibilidad con otros proveedores de identidades sociales conocidos en función de la demanda del cliente.

Azure AD B2C también ha agregado compatibilidad para [directivas personalizadas](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Estos [directivas personalizadas de](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) permitir que un desarrollador toocreate su propia directiva que con cualquier proveedor de identidad que admite [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) o SAML. 

Empiece a trabajar con directivas personalizadas consultando nuestro [paquete de inicio de directivas personalizadas](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>¿Puedo configurar ámbitos toogather obtener más información acerca de los consumidores de distintos proveedores de identidades sociales?
No, pero esta característica está en nuestro mapa de ruta. ámbitos de Hello predeterminada usados para nuestro conjunto de proveedores de identidades sociales compatible son:

* Facebook: correo electrónico
* Google+: correo electrónico
* Cuenta Microsoft: perfil de correo electrónico de OpenID
* Amazon: perfil
* LinkedIn: r_emailaddress r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>¿Mi aplicación tiene toobe ejecutar en Azure para funcione con Azure AD B2C?
No, puede hospedar la aplicación en cualquier lugar (en nube de Hola o de forma local). Todo lo que necesita toointeract con Azure AD B2C es Hola toosend de capacidad y recibir las solicitudes HTTP en los puntos de conexión es accesibles públicamente.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Tengo varios inquilinos de Azure AD B2C. ¿Cómo puedo administrar ellos en hello portal de Azure?
Antes de abrir 'Azure AD B2C' en el menú del lado izquierdo de Hola de hello portal de Azure, debe cambiar al directorio de hello desea toomanage.  Cambiar directorios, haga clic en su identidad en hello parte superior derecha Hola portal de Azure, a continuación, elija un directorio en hello desplegable que aparece.  Para un paso a paso con imágenes, vea [desplácese tooAzure AD B2C configuración](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>¿Cómo se personalizan los correos electrónicos de comprobación (contenido de Hola y Hola "de:" campo) enviado por Azure AD B2C?
Puede usar hello [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md) toocustomize contenido de Hola de correos electrónicos de comprobación. En concreto, se pueden personalizar estos dos elementos de correo electrónico de hello:

* **Logotipo de banner**: se muestra en hello esquina inferior derecha.
* **Color de fondo**: se muestra en la parte superior de Hola.

    ![Captura de pantalla de un correo electrónico de comprobación personalizado](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

firma de correo electrónico de Hello contiene nombre del inquilino de hello B2C que proporcionó cuando se creó por primera vez el inquilino de hello B2C. Puede cambiar el nombre hello usando estas instrucciones:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) como Hola Administrador de la suscripción.
1. Navegue a inquilino tooyour B2C.
1. Haga clic en hello **configurar** ficha.
1. Hola de cambio **nombre** campo hello **propiedades del directorio** sección.
1. Haga clic en **guardar** final Hola de página Hola.

Actualmente no hay ningún hello toochange de manera "de:" campo de correo electrónico de Hola. Votar sobre [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) está interesado en Personalizar cuerpo Hola de correo electrónico de comprobación de Hola.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>¿Cómo puedo migrar mi existentes de los nombres de usuario, contraseñas y perfiles de mi tooAzure de base de datos AD B2C?
Puede usar hello Azure AD Graph API toowrite la herramienta de migración. Vea hello [ejemplo de API Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) para obtener más información.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>¿Qué directiva de contraseñas se utiliza para las cuentas locales en Azure AD B2C?
Hello Azure AD B2C directiva de contraseñas para cuentas locales se basa en la directiva de Hola para Azure AD. Azure AD B2C del inicio de sesión, inicio de sesión o inicio de sesión y contraseña restablecer la intensidad de las directivas utiliza Hola "contraseña" y no expiran las contraseñas. Hola de lectura [directiva de contraseñas de Azure AD](https://msdn.microsoft.com/library/azure/jj943764.aspx) para obtener más detalles.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>¿Puedo usar Azure AD Connect toomigrate las identidades de consumidor que están almacenadas en mi tooAzure de Active Directory local AD B2C?
No, Azure AD Connect no está diseñada toowork con Azure AD B2C. Considere el uso de hello [API Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) para la migración de usuario.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>¿Mi aplicación puede abrir páginas de Azure AD B2C dentro de un iFrame?
No, por motivos de seguridad, las páginas de Azure AD B2C no se pueden abrir dentro de un iFrame.  Nuestro servicio se comunica con hello explorador tooprohibit iFrames.  Hola Comunidad de seguridad en general y Hola especificación OAUTH2, recomienda no usar iFrames para experiencias de identidad debido toohello riesgo de levantamiento haga clic en.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>¿Funciona Azure AD B2C con sistemas CRM, como Microsoft Dynamics?
La integración básica con el portal de Microsoft Dynamics 365 está disponible.  Vea [toouse configurar Dynamics 365 Portal Azure AD B2C para la autenticación](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>¿Funciona Azure AD B2C con SharePoint local 2016 o una versión anterior?
Azure AD B2C no está pensada para hello SharePoint externo asociado escenario de uso compartido; vea [B2B de Azure AD](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) en su lugar.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>¿Debo usar Azure AD B2C o B2B toomanage externas identidades?
Lea este artículo sobre [identidades externas](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn más sobre la aplicación hello adecuados características tooyour escenarios de identidad externa.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>¿Qué características de auditoría e informes proporciona Azure AD B2C? ¿Son iguales que Hola como en Azure AD Premium?
No, Azure AD B2C admite Hola al mismo conjunto de informes como Azure AD Premium. Sin embargo, hay muchos elementos en común:

* Hola inicio de sesión en los informes proporcionan un registro de cada inicio de sesión con detalles reducidas.
* Informes de auditoría están disponibles en hello portal de Azure, en Azure Active Directory > registros de auditoría de la actividad > elija B2C y aplicar filtros según sea necesario. Se cubren tanto la actividad administrativa como la actividad de la aplicación. 
* Un informe de uso, que cubre el número de usuarios, el número de inicios de sesión y el volumen de MFA está disponible en la [API de informes de uso](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>¿Puedo localizar Hola interfaz de usuario de páginas servidas por Azure AD B2C? ¿Qué idiomas se admiten?
Sí.  Obtenga información sobre la [personalización de lenguaje](active-directory-b2c-reference-language-customization.md), que se encuentra en versión preliminar pública.  Proporcionamos las traducciones de 36 idiomas, y pueden invalidar cualquier cadena toosuit sus necesidades.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>¿Puedo usar mis propias direcciones URL en las páginas de registro y de inicio que proporciona Azure AD B2C? ¿Por ejemplo, ¿puedo cambiar dirección URL de Hola de login.microsoftonline.com toologin.contoso.com?
Actualmente, no. Esta característica está en nuestro mapa de ruta. Comprobar el dominio en hello **dominios** ficha en el portal de Azure clásico hello no lograr este objetivo.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>¿Cómo puedo eliminar al inquilino de Azure AD B2C?
Siga estos pasos toodelete su inquilino de Azure AD B2C:

1. Siga estos pasos demasiado[desplácese tooAzure AD B2C configuración](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
1. Navegue toohello **aplicaciones**, **proveedores de identidades**, y **todas las directivas** y elimine todas las entradas de hello en cada uno de ellos.
1. Ahora, inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) como Hola Administrador de la suscripción. (Use Hola mismo trabajo o educativa cuenta u Hola la misma cuenta de Microsoft que usa toosign hacia arriba para Azure.)
1. Navegar por la extensión de Active Directory toohello Hola izquierda y haga clic en el inquilino B2C.
1. Haga clic en hello **usuarios** ficha.
1. Seleccione cada usuario a su vez, (exclude Hola Administrador de suscripciones de usuario inició sesión como). Haga clic en **eliminar** final Hola de página de Hola y haga clic en **Sí** cuando se le solicite.
1. Haga clic en hello **aplicaciones** ficha.
1. Seleccione **aplicaciones tiene mi compañía** en hello **mostrar** campo de lista desplegable y haga clic en Hola marca de verificación.
1. Una aplicación llamada "**b2c-extensions-app**". Haga clic en **eliminar** final Hola de página de Hola y haga clic en **Sí** cuando se le solicite.
1. Navegar por extensión de Active Directory toohello nuevo y seleccione al inquilino B2C.
1. Haga clic en **eliminar** final Hola de página Hola. proceso de hello toocomplete, siga las instrucciones de hello en pantalla de bienvenida.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>¿Puedo obtener Azure AD B2C como parte de Enterprise Mobility Suite?
No, Azure AD B2C es un servicio de Azure de pago por uso y no forma parte de Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>¿Cómo puedo informar sobre problemas con Azure AD B2C?
Consulte [Versión preliminar de Azure Active Directory B2C: presentación de solicitudes de soporte técnico](active-directory-b2c-support.md).
