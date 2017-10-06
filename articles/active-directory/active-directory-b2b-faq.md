---
title: "Preguntas más frecuentes de la colaboración B2B de Active Directory aaaAzure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes acerca de la colaboración B2B de Azure Active Directory."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Preguntas más frecuentes acerca de la colaboración B2B de Azure Active Directory

Estas preguntas más frecuentes (P+f) acerca de la colaboración de negocio a negocio (B2B) de Azure Active Directory (Azure AD) están actualizados periódicamente tooinclude nuevos temas.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>¿Está disponible en el portal de Azure clásico Hola colaboración B2B de Azure AD?
No. Características de colaboración AD B2B Azure solo están disponibles en hello [portal de Azure](https://portal.azure.com) y Hola [Panel de acceso](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>¿Se puede personalizar la página de inicio de sesión para que sea más intuitiva para los usuarios invitados de colaboración de B2B?
Por supuesto. Consulte nuestra [entrada del blog relativa a esta característica](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Para obtener más información acerca de cómo toocustomize su organización del inicio de sesión en la página, vea [agregar marcas toosign en y páginas de Panel de acceso de empresa](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>¿Pueden acceder los usuarios de colaboración B2B a SharePoint Online y OneDrive?
Sí. Sin embargo, es hello toosearch de capacidad para los usuarios existentes de invitado en SharePoint Online mediante el uso de selector de personas de hello **desactivar** de forma predeterminada. establecer tooturn en hello opción toosearch para usuarios invitados existente, **ShowPeoplePickerSuggestionsForGuestUsers** demasiado**en**. Puede activar esta configuración en el nivel del inquilino de Hola o en el nivel de colección de sitios de Hola. Puede cambiar esta configuración mediante cmdlets de conjunto SPOTenant y Set-SPOSite Hola. Con estos cmdlets, los miembros pueden buscar todos los usuarios existentes de invitado en el directorio de Hola. Cambios en el ámbito del inquilino de hello no afectan a los sitios de SharePoint Online que ya se ha aprovisionado.

### <a name="is-hello-csv-upload-feature-still-supported"></a>¿Es hello CSV cargar la característica es compatible todavía?
Sí. Para obtener más información acerca de cómo utilizar la característica de carga de archivo .csv de hello, consulte [en este ejemplo de PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>¿Cómo puedo personalizar mis correos electrónicos de invitación?
Puede personalizar prácticamente cualquier aspecto de proceso del autor de la invitación de hello mediante el uso de hello [B2B invitación API](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>¿Puede un usuario externo invite abandonan la organización de hello después de que se está invitado?
Administrador de organización invitar a Hola puede eliminar un usuario de invitado de la colaboración B2B de su directorio, pero usuario guest de hello no puede dejar Hola invitar a directorio de la organización por sí mismos. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>¿Pueden restablecer los usuarios invitados su método de Multi-Factor Authentication?
Sí. Los usuarios de invitado pueden restablecer su Hola de método de la autenticación multifactor igual forma que los usuarios normales.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>¿Qué organización es la responsable de las licencias de Multi-Factor Authentication?
organización de invitar a Hola realiza la autenticación multifactor. Hola invitar a la organización debe asegurarse de que la organización de hello tiene suficientes licencias para sus usuarios B2B que usen la autenticación multifactor.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>¿Qué ocurre si una organización asociada ya tiene Multi-Factor Authentication configurado? ¿Podemos confiar en su Multi-Factor Authentication y no utilizar nuestro propio Multi-Factor Authentication?
Esta característica está planeada para una versión futura, por lo, a continuación, se puede seleccionar tooexclude de socios concretos de la autenticación multifactor (Hola invitar a de su organización).

### <a name="how-can-i-use-delayed-invitations"></a>¿Cómo se usan las invitaciones diferidas?
Una organización podría desea que los usuarios de colaboración de tooadd B2B, aprovisionar tooapplications según sea necesario y, a continuación, enviar invitaciones. Puede usar Hola B2B colaboración invitación API toocustomize Hola incorporación flujo de trabajo.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>¿Puedo hacer que un usuario invitado sea un administrador limitado?
Totalmente. Para obtener más información, consulte [función de agregar invitado usuarios tooa](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>¿Permite la colaboración B2B de Azure AD B2B usuarios tooaccess Hola portal de Azure?
A menos que un usuario está asignado hello en roles de administrador global o limitado, los usuarios de colaboración B2B no requieren acceso toohello portal de Azure. Sin embargo, los usuarios de la colaboración B2B asignados rol Hola de administrador global o limitado pueden tener acceso a portal de Hola. Además, si un usuario invitado que no está asignado a uno de estos roles de administrador tiene acceso a portal de hello, Hola usuario podría ser capaz de tooaccess ciertas partes de Hola experiencia. rol de usuario de invitado de Hello tiene algunos permisos en el directorio de Hola.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>¿Puedo bloquear el acceso toohello portal de Azure para usuarios invitados?
Sí. Cuando se configura esta directiva, ser administradores y tooavoid cuidado accidentalmente bloqueo acceso toomembers.
tooblock un usuario invitado acceso toohello [portal de Azure](https://portal.azure.com), utilice una directiva de acceso condicional en hello API del modelo de implementación clásica de Windows Azure:
1. Modificar hello **todos los usuarios** para que contenga solo los miembros de grupo.
  ![modificar la captura de pantalla de hello grupo](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Cree un grupo dinámico que contenga usuarios invitados.
  ![crear captura de pantalla del grupo](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Configurar un acceso condicional directiva tooblock invitado a los usuarios de acceso al portal de hello, como se muestra en la siguiente Hola vídeo:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>¿Admite la colaboración B2B de Azure AD admite la autenticación multifactor y las cuentas de correo electrónico de consumidor?
Sí. Tanto la autenticación multifactor como las cuentas de correo electrónico de consumidor admiten para la colaboración B2B de Azure AD.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>¿Tiene pensado toosupport restablecimiento de contraseña para los usuarios de colaboración B2B de Azure AD?
Sí. A continuación encontrará detalles importantes de Hola para restablecer la contraseña de autoservicio (SSPR) para un usuario de B2B invitada desde una organización del asociado:
 
* SSPR se produce únicamente en el inquilino de hello identidad de usuario de hello B2B.
* Si el inquilino de identidad de hello es una cuenta de Microsoft, se utiliza Hola cuenta mecanismo de Autoservicio de Microsoft.
* Si inquilino de identidad de hello es un just-in-time (JIT) o de inquilino "viral", se envía un correo electrónico de restablecimiento de contraseña.
* Para otros inquilinos, se sigue el proceso SSPR estándar de hello B2B a los usuarios. Como miembro de Autoservicio para usuarios de B2B, en el contexto de hello del recurso de hello, arquitectura multiempresa está bloqueado. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>¿Está disponible el restablecimiento de contraseña para los usuarios invitados en un inquilino Just-In-Time (JIT) o "viral" que ha aceptado invitaciones con una dirección de correo electrónico laboral o académica, pero que no tiene una cuenta existente de Azure AD?
Sí. Que permite un usuario tooreset su contraseña multiempresa JIT hello, se puede enviar un correo electrónico de restablecimiento de contraseña.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>¿Proporciona Microsoft Dynamics CRM compatibilidad en línea con la colaboración B2B de Azure AD?
En la actualidad, Microsoft Dynamics CRM no proporciona compatibilidad en línea con la colaboración B2B de Azure AD. Sin embargo, tenemos previsto toosupport esto Hola futuras.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>¿Cuál es la duración de Hola de una contraseña inicial para un usuario de la colaboración B2B recién creado?
Azure AD tiene un conjunto fijo de carácter, seguridad de la contraseña y los requisitos de bloqueo de cuenta que se aplican igualmente tooall cuentas de usuario de la nube de Azure AD. Las cuentas de usuario de nube son cuentas que no se federan con otro proveedor de identidades, como 
* Cuenta Microsoft
* Facebook
* Servicios de federación de Active Directory
* Otro inquilino de nube (para la colaboración B2B)

Para cuentas federadas, directiva de contraseñas depende de la directiva de Hola que se aplica en la configuración de cuenta de Microsoft hello local hello e inquilinos del usuario.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Una organización puede querer toohave diferentes experiencias en sus aplicaciones para los usuarios de inquilinos y usuarios invitados. ¿Hay instrucciones estándar para esto? ¿Es la presencia de Hola de hello identidad proveedor notificación Hola modelo correcto toouse?
 Un usuario invitado puede usar cualquier tooauthenticate de proveedor de identidad. Para más información, consulte [Propiedades de un usuario de colaboración B2B de Azure Active Directory](active-directory-b2b-user-properties.md). Hola de uso **UserType** experiencia del usuario de toodetermine de propiedad. Hola **UserType** notificación no está incluida en el símbolo (token) de Hola. Las aplicaciones deben utilizar el directorio de hello API Graph tooquery hello para el usuario de Hola y Hola tooget UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>¿Dónde puedo encontrar un tooshare de comunidad de colaboración B2B soluciones e ideas toosubmit?
Le escuchamos constantemente tooyour comentarios, tooimprove la colaboración B2B. Le invitamos a tooshare el usuario escenarios, prácticas recomendadas y lo que le gusta la colaboración B2B de Azure AD. Unirse a la discusión de Hola Hola [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Le invitamos también se toosubmit sus ideas y vote por características futuras en [Ideas de colaboración B2B](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>¿Podemos enviar una invitación que se canjea automáticamente, por lo que Hola usuario simplemente "listo toogo"? ¿O usuario Hola siempre tiene tooclick a través de la dirección URL de canje toohello?
Invitaciones enviados por un usuario en hello invitar a la organización que también sea miembro de la organización del asociado de hello no requieren canje por usuario de hello B2B.

Se recomienda que invitar a un usuario de Hola de toojoin de organización Hola asociado invitar a la organización. [Agregar este rol de autor de la invitación de usuario toohello invitado en la organización de recursos de hello](active-directory-b2b-add-guest-to-role.md). Este usuario puede invitar a otros usuarios de la organización del asociado de hello mediante el uso de inicio de sesión de hello interfaz de usuario, las secuencias de comandos de PowerShell, o las API. A continuación, B2B colaboración a los usuarios de la organización no es necesario tooredeem sus invitaciones.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>¿Cómo funciona la colaboración B2B al socio comercial de hello invitado usa federación tooadd su propia autenticación local?
Si el socio hello tiene un inquilino de Azure AD que se federa toohello infraestructura de autenticación local, automáticamente se logra el inicio de sesión único (SSO) en local. Si el asociado de Hola no tiene un inquilino de Azure AD, se crea una cuenta de Azure AD para los nuevos usuarios. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Creía que B2B de Azure AD no aceptaba direcciones de correo electrónico gmail.com y outlook.com, y que se usaba B2C para esos tipos de cuentas
Estamos quitando las diferencias de hello entre B2B y colaboración de negocio a la empresa (B2C) en cuanto a que se admiten las identidades. identidad de Hello utilizada no es un toochoose buena razón entre usar B2B o usar B2C. Para obtener información acerca de cómo elegir la opción de colaboración, consulte [Comparación de la colaboración B2B y B2C de Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>¿Qué aplicaciones y los servicios admiten los usuarios invitados de Azure B2B?
Todas las aplicaciones integradas en Azure AD admiten usuarios de invitados de B2B para Azure. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>¿Podemos forzar la autenticación multifactor para usuarios invitados de B2B si nuestros asociados no la tienen?
Sí. Puede encontrar información en [Acceso condicional para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>En SharePoint puede definir una lista de "permitidos" o "denegados" para usuarios externos. ¿Se puede hacer esto en Azure?
Sí. La colaboración B2B de Azure AD admite listas de permitidos y de denegados. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>¿Qué licencias necesitamos toouse B2B de Azure AD?
Para obtener información acerca de las licencias de su organización necesita toouse B2B de Azure AD, consulte [colaboración B2B de Azure Active Directory licencias instrucciones](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saludo de correo electrónico de invitación de colaboración B2B de hello](active-directory-b2b-invitation-email.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Concesión de licencias de colaboración B2B de Azure AD](active-directory-b2b-licensing.md)
* [Solución de problemas de colaboración B2B de Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Personalización y API de colaboración B2B de Active Directory Azure](active-directory-b2b-api.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
