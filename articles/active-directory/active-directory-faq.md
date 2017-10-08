---
title: "Preguntas más frecuentes de Active Directory aaaAzure | Documentos de Microsoft"
description: "P+F de directorio Active Azure responde a preguntas acerca de cómo tener acceso tooaccess Azure y Azure Active Directory, la administración de contraseñas y aplicación."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>P+F de Azure Active Directory
Azure Active Directory (Azure AD) es una completa solución de identidad como servicio (IDaaS) que abarca todos los aspectos de la identidad, la administración de acceso y la seguridad.

Para más información, consulte [¿Qué es Azure Active Directory?](active-directory-whatis.md)


## <a name="access-azure-and-azure-active-directory"></a>Acceso a Azure y a Azure Active Directory
**P: ¿por qué obtengo "se encontró ninguna suscripción" cuando intento tooaccess Azure AD en hello portal de Azure clásico?**

**R:** tooaccess Hola portal de Azure clásico, cada usuario necesita permisos con una suscripción de Azure. Si tiene una suscripción de pago de Office 365 o Azure AD, vaya demasiado[http://aka.ms/accessAAD](http://aka.ms/accessAAD) para un paso de activación de un solo uso. De lo contrario, necesitará una segunda tooactivate [cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/) o una suscripción de pago.

Para más información, consulte:

* [Asociación de las suscripciones de Azure con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Administrar el directorio de hello para la suscripción a Office 365 en Azure](active-directory-manage-o365-subscription.md)

- - -
**P: ¿cuál es la relación de hello entre AD de Azure, Office 365 y Azure?**

**R:** Azure AD proporciona funcionalidades comunes de identidad y acceso tooall los servicios web. Si utilizas Office 365, Microsoft Azure, Intune, u otros usuarios, está ya usa Azure AD toohelp activar administración de inicio de sesión y acceso para todos estos servicios.

Todos los usuarios que se configuran los servicios web toouse se definen como cuentas de usuario en una o varias instancias de Azure AD. Puede configurar gratis en estas cuentas las funcionalidades de Azure AD, como el acceso a aplicaciones en la nube.

Los servicios de pago de Azure AD, como Enterprise Mobility + Security, complementan otros servicios web como Office 365 y Microsoft Azure con completas soluciones de administración y seguridad para empresas.
- - -
**P: ¿por qué puedo iniciar sesión en el portal de Azure toohello pero no Hola portal de Azure clásico?**

**R:** hello portal de Azure no requieren una suscripción válida y portal clásico de hello requieren una suscripción válida.  Si no tiene una suscripción, no puede iniciar sesión en el portal clásico de toohello.
- - -
**P: ¿Cuáles son las diferencias de hello entre el Administrador de la suscripción y Administrador de directorios?**

**R:** de forma predeterminada, se asignan roles de administrador de la suscripción de hello al suscribirse a Azure. Un administrador de suscripciones que puede usar una cuenta de Microsoft o un trabajo o escuela cuenta del directorio de Hola que Hola suscripción de Azure está asociada.  Este rol es servicios autorizados toomanage Hola portal de Azure.

Si otras personas necesitan toosign en y acceder a los servicios por utilizando Hola misma suscripción, puede agregarlas como coadministradores. Este rol tiene Hola mismo privilegios de acceso como Hola, Administrador de servicio, pero no se puede cambiar la asociación de Hola de directorios de tooAzure de suscripciones.  Para obtener más información sobre los administradores de suscripciones, vea [cómo tooadd o cambiar roles de administrador de Azure](../billing-add-change-azure-subscription-administrator.md) y [suscripciones de Azure están asociadas con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


Azure AD tiene un conjunto diferente de características relacionadas con la identidad y el directorio de Hola de toomanage de roles de administrador.  Estos administradores se tiene acceso toovarious características Hola portal de Azure u Hola portal de Azure clásico. la función de administrador de Hello determina qué pueden hacer, como crear o editar usuarios, asignar roles administrativos tooothers, restablecer contraseñas de usuario, administrar licencias de usuario o administrar dominios.  Para más información sobre los administración de Azure AD y sus roles, consulte [Asignación de roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md).

Además, los servicios de pago de Azure AD, como Enterprise Mobility + Security, complementan otros servicios web como Office 365 y Microsoft Azure con completas soluciones de administración y seguridad para empresas.

- - -
**P: ¿Existe un informe que muestra cuándo expirarán mis licencias de usuario de Azure AD?**

**R**: No.  No está disponible actualmente.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Introducción a Azure AD híbrido


**P: ¿Cómo dejo un inquilino cuando se me ha agregado como colaborador?**

**R:** cuando se agregan tooanother el inquilino de organización como un colaborador, puede usar Hola "inquilino selector" en hello superior derecho tooswitch entre los inquilinos.  Actualmente, no hay ningún hello tooleave de manera invitar a la organización y Microsoft está trabajando en proporcionar esta funcionalidad.  Hasta que esta característica está disponible, puede pedir Hola invitar a tooremove de organización de su inquilino.
- - -
**P: ¿Cómo puedo conectarme mi tooAzure de directorio local AD?**

**R:** puede conectar su tooAzure de directorio local AD mediante Azure AD Connect.

Para más información, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

- - -
**P: ¿Cómo se configura el SSO entre mi directorio local y las aplicaciones de nube?**

**R:** solo necesita tooset el inicio de sesión único (SSO) entre el directorio local y Azure AD. Siempre y cuando tiene acceso a las aplicaciones de nube mediante Azure AD, servicio de hello automáticamente las unidades de los usuarios toocorrectly autenticarse con sus credenciales locales.

La implementación del SSO desde el entorno local se puede lograr fácilmente con soluciones de federación como Active Directory Federation Services (AD FS) o configurando la sincronización de la sincronización de hash de contraseña. Puede implementar fácilmente ambas opciones usando el Asistente de configuración de hello Azure AD Connect.

Para más información, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

- - -
**P: ¿Proporciona Azure AD un portal de autoservicio para usuarios en mi organización?**

**R:** Sí, Azure AD le proporciona hello [Panel de acceso de Azure AD](http://myapps.microsoft.com) de usuario de autoservicio y acceso a la aplicación. Si es un cliente de Office 365, puede encontrar muchas de hello mismas capacidades en el portal de Office 365 Hola.

Para obtener más información, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

- - -
**P: ¿Me ayuda Azure AD a administrar la infraestructura local?**

**R:** Sí. edición de Azure AD Premium Hola proporciona Azure AD Connect Health. Mantenimiento de Azure AD Connect le ayuda a supervisar y comprender mejor su identidad local hello y la infraestructura de servicios de sincronización.  

Para obtener más información, consulte [supervisar los servicios de infraestructura y la sincronización de identidad local en la nube de hello](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Administración de contraseñas
**P: ¿Puedo usar la escritura diferida de contraseñas de Azure AD sin sincronización de contraseñas? (En este escenario, es posible toouse Azure AD restablecimiento de contraseña de autoservicio (SSPR) con contraseña contraseñas de reescritura y almacena en la nube de hello?)**

**R:** no es necesario toosynchronize su Active Directory contraseñas tooAzure AD tooenable reescritura. En un entorno federado, Azure AD inicio de sesión único (SSO) se basa en usuarios de hello locales directory tooauthenticate Hola. Este escenario no requiere Hola local contraseña toobe realiza un seguimiento en Azure AD.

- - -
**P: ¿cuánto tarda para un toobe contraseña reescrito tooActive directorio local?**

**R:** La escritura diferida de contraseñas funciona en tiempo real.

Para más información, consulte [Introducción a la administración de contraseñas](active-directory-passwords-getting-started.md).

- - -
**P: ¿Puedo usar la escritura diferida de contraseñas con las que administra un administrador?**

**R:** Sí, si dispone de reescritura de contraseña habilitada, las operaciones de contraseña de hello realizadas por un administrador se reescriben entorno local de tooyour.  

Para obtener respuestas más preguntas relacionadas con toopassword, consulte [preguntas más frecuentes sobre la administración de contraseñas](active-directory-passwords-faq.md).
- - -
**P: ¿Qué puedo hacer si no recuerdo mi contraseña de AD de existente Office 365 o SQL Azure al intentar toochange mi contraseña?**

**R:** En este tipo de situaciones, dispone de un par de opciones.  Use el restablecimiento de la contraseña de autoservicio (SSPR), si está disponible.  El funcionamiento de SSPR dependerá de cómo esté configurado.  Para obtener más información, consulte [cómo restablecer contraseña Hola trabajo portal](active-directory-passwords-best-practices.md).

Para los usuarios de Office 365, el administrador puede restablecer contraseña Hola siguiendo los pasos de Hola que se describen en [restablecer contraseñas de usuario](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Para cuentas de Azure AD, administradores pueden restablecer las contraseñas mediante el uso de uno de los siguientes hello:

- [Restablecer las cuentas de hello portal de Azure](active-directory-users-reset-password-azure-portal.md)
- [Restablecimiento de cuentas en el portal clásico de Hola](active-directory-create-users-reset-password.md)
- [Uso de PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Seguridad
**P: ¿Se bloquean las cuentas después de un número determinado de intentos erróneos o se usa una estrategia más sofisticada?**</br>
Se usa una cuenta de toolock estrategia más sofisticadas.  Esto se basa en IP Hola de solicitud de Hola y contraseñas de hello escritas. duración de Hola de bloqueo de hello también aumenta en función de probabilidad de Hola que es un ataque.  

**P: determinadas de contraseñas (comunes) obtengan rechazadas con hello mensajes 'esta contraseña ha sido usado toomany veces', hace referencia este toopasswords usado en hello actual active directory?**</br>
Esto refiere toopasswords global comunes, como las variantes de "Password" y "123456".

**P: ¿Se bloqueará una solicitud de inicio de sesión de origen dudoso (botnets, punto de conexión Tor) en un inquilino B2C o se requerirá un inquilino de la edición Básica o Premium?**</br>
Tenemos una puerta de enlace que filtra las solicitudes y proporciona alguna protección contra los botnets, y se aplica a todos los inquilinos B2C.

## <a name="application-access"></a>Acceso a las aplicaciones
**P: ¿Dónde puedo encontrar una lista de las aplicaciones preintegradas en Azure AD y sus funcionalidades?**

**R:** Azure AD cuenta con más de 2 600 aplicaciones preintegradas de Microsoft, proveedores de servicios de aplicaciones y asociados. Todas las aplicaciones preintegradas deben ser compatibles con el inicio de sesión único (SSO). SSO permite usar las aplicaciones de su tooaccess de credenciales de la organización. Algunas de las aplicaciones de hello también admiten automatizada de aprovisionamiento y cancelación del aprovisionamiento.

Para obtener una lista completa de las aplicaciones previamente integradas de hello, vea hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**P: ¿qué ocurre si hello aplicación que necesario no está en marketplace de hello Azure AD?**

**R:** Con Azure AD Premium puede agregar y configurar cualquier aplicación. Según las funcionalidades de la aplicación y sus preferencias, puede configurar el SSO y el aprovisionamiento automatizado.  

Para más información, consulte:

* [Configurar tooapplications de inicio de sesión único que no están en la Galería de aplicaciones de Azure Active Directory Hola](active-directory-saas-custom-apps.md)
* [Uso de SCIM tooenable el aprovisionamiento automático de usuarios y grupos de Azure Active Directory tooapplications](active-directory-scim-provisioning.md)

- - -
**P: ¿cómo los usuarios iniciar sesión tooapplications mediante Azure AD?**

**R:** Azure AD proporciona varias maneras para los usuarios tooview y acceder a sus aplicaciones, como:

* panel de acceso de Hello Azure AD
* iniciador de la aplicación Hello Office 365
* Aplicaciones de toofederated de inicio de sesión directo
* Vínculos profundos toofederated, basada en contraseña, o aplicaciones existentes

Para obtener más información, consulte [implementación Azure AD integrado aplicaciones toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**P: ¿Cuáles son maneras diferentes de hello Azure AD permite la autenticación y tooapplications de inicio de sesión único?**

**R:** Azure AD admite muchos protocolos estandarizados para la autenticación y la autorización, como SAML 2.0, OpenID Connect, OAuth 2.0 y WS-Federation. Además, Azure AD admite las funcionalidades de inicio de sesión automatizado y de almacenamiento de contraseñas para las aplicaciones que solo sean compatibles con la autenticación basada en formularios.  

Para más información, consulte:

* [Escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md)
* [Protocolos de autenticación de Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [¿Cómo funciona el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**P: ¿Puedo agregar aplicaciones que ejecuto de manera local?**

**R:** Proxy de aplicación de Azure AD proporciona acceso seguro y sencillo de aplicaciones web tooon locales que elija. Puede tener acceso a estas aplicaciones en hello igual que obtiene acceso a su software como un servicio (SaaS) de aplicaciones de Azure AD. No es necesario para un servidor VPN o toochange la infraestructura de red.  

Para obtener más información, consulte [cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md).

- - -
**P: ¿Cómo requiero la autenticación multifactor para usuarios con acceso a una aplicación determinada?**

**R:** Con el acceso condicional de Azure AD, puede asignar una directiva de acceso única a cada aplicación. En la directiva, puede requerir la autenticación multifactor siempre y cuando los usuarios no están conectados toohello red local.  

Para obtener más información, consulte [proteger el acceso tooOffice 365 y otras aplicaciones conectadas tooAzure Active Directory](active-directory-conditional-access.md).

- - -
**P: ¿Qué es el aprovisionamiento automático de usuarios para aplicaciones SaaS?**

**R:** creación de hello tooautomate usan Azure AD, mantenimiento y eliminación de identidades de usuario en muchas aplicaciones de SaaS populares en la nube.

Para obtener más información, consulte [automatizar el aprovisionamiento de usuario y la cancelación tooSaaS aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md).

- - -
**P: ¿Puedo configurar una conexión LDAP segura con Azure Active Directory?**

**R**: No. Azure AD no es compatible con el protocolo LDAP de Hola.
