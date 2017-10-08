---
title: aaaHow tooIntegrate con Azure Active Directory | Documentos de Microsoft
description: "Un toobenefits de guía de y recursos para la integración con Azure Active Directory."
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Integración con Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory proporciona a las organizaciones administración de identidades empresariales para aplicaciones en la nube.  Integración de Azure AD ofrece a los usuarios una experiencia de inicio de sesión simplificada y ayuda a la aplicación cumple la directiva de tooIT.

## <a name="how-toointegrate"></a>Cómo tooIntegrate
Hay varias maneras para su toointegrate de aplicación con Azure AD.  Aprovechar muchos o algunos de estos escenarios es apropiado para su aplicación.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Compatibilidad con Azure AD como una manera tooSign en tooYour aplicación
**Reduzca la fricción de inicio de sesión y reduzca los costes de soporte técnico.** Con Azure AD toosign en tooyour aplicación, los usuarios no tienen una tooremember más de nombre y una contraseña.  Como desarrollador, podrá tener un menor toostore de contraseña y proteger.  No tener los restablecimientos de contraseña olvidada de toohandle puede ser un ahorro significativo por sí sola.  Azure AD potencia de inicio de sesión para algunos de los más populares aplicaciones de nube de Hola a todos, incluido Office 365 y Microsoft Azure.  Con centenares de millones a los usuarios de millones de organizaciones, lo más probable es el usuario ya ha iniciado sesión tooAzure AD.  Más información sobre la [adición de compatibilidad para el inicio de sesión de Azure AD](active-directory-authentication-scenarios.md).

**Simplifique el registro de la aplicación.**  Durante el registro de la aplicación, Azure AD puede enviar información esencial acerca de un usuario para que pueda rellenar previamente el formulario de registro o eliminarlo completamente.  Los usuarios pueden suscribirse para la aplicación con su cuenta de Azure AD a través de un toothose similar de experiencia de consentimiento familiar que se encuentran en redes sociales y aplicaciones móviles.  Cualquier usuario puede registre e inicie sesión en la aplicación tooan que se integra con Azure AD sin necesidad de intervención de TI.  Más información sobre el [registro de la aplicación para el inicio de sesión con la cuenta de Azure AD](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Buscar usuarios, administrar el aprovisionamiento de usuarios y controlar el acceso tooYour aplicación
**Buscar usuarios en el directorio de Hola.**  Usar Hola API Graph toohelp usuarios búsqueda y exploración de otras personas de su organización al invitar a otros usuarios o conceder acceso, en lugar de tootype direcciones de correo electrónico.  Los usuarios pueden examinar mediante una interfaz de estilo de la libreta de dirección conocida, incluida la visualización de detalles de Hola de jerarquía organizativa de Hola.  Obtener más información sobre hello [API Graph](active-directory-graph-api.md).

**Vuelva a usar las listas de distribución y grupos de Active Directory que el cliente ya está administrando.**  Azure AD contiene grupos de Hola que su cliente ya está usando para la distribución de correo electrónico y administrar el acceso.  Con API Graph hello, volver a usar estos grupos en lugar de requerir la toocreate del cliente y administrar un conjunto independiente de grupos en la aplicación.  Información del grupo también pueden enviarse aplicación tooyour en tokens de inicio de sesión.  Obtener más información sobre hello [API Graph](active-directory-graph-api.md).

**Toocontrol de uso de Azure AD que tenga acceso tooyour aplicación.**  Los administradores y propietarios de las aplicaciones de Azure AD pueden asignar acceso tooapplications toospecific usuarios y grupos.  Con hello API Graph, puede leer esta lista y usarlo toocontrol aprovisionamiento y cancelación del aprovisionamiento de recursos y acceso a la aplicación.

**Utilice Azure AD para roles basados en el control de acceso.**  Los administradores y propietarios de aplicaciones pueden asignar a los usuarios y grupos tooroles que definen al registrar la aplicación en Azure AD.  Información de la función se envía la aplicación tooyour en tokens de inicio de sesión y también se puede leer utilizando Hola API Graph.  Obtenga más información sobre [uso de Azure AD para la autorización](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Obtener perfil del acceso tooUser, calendario, correo electrónico, contactos, archivos etc.
**Azure AD es el servidor de autorización de Hola para Office 365 y otros servicios empresariales de Microsoft.**  Si admite Azure AD para inicio de sesión en aplicaciones de tooyour o compatibilidad con vinculación mediante OAuth 2.0 las cuentas de usuario de AD tooAzure de cuentas usuario actual, puede solicitar perfil lectura y acceso de escritura tooa usuario, calendario, correo electrónico, contactos, archivos y otra información.  Perfectamente puede escribir calendario de eventos toouser y leer o escribir archivos tootheir OneDrive.  Obtenga más información sobre [acceso Hola API de Office 365](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Promover la aplicación en Azure hello y catálogos de soluciones de Office 365
**Promover la aplicación toohello millones de organizaciones que ya está usando Azure AD.**  Los usuarios que buscan y examinan estos catálogos de soluciones ya están usando uno o más servicios en la nube, lo que los convierte en clientes de servicio en la nube cualificados.  Más información acerca de la promoción de la aplicación en [hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**Cuando los usuarios registrar la aplicación, aparecerá en el panel de acceso de Azure AD y en el iniciador de aplicaciones de Office 365.**  Los usuarios será capaz de tooquickly y tooyour devuelto fácilmente aplicaciones más adelante, mejorar la interacción del usuario.  Obtener más información sobre hello [panel de acceso de Azure AD](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Comunicación segura de dispositivo a servicio y de servicio a servicio
**Con Azure AD para la administración de identidades de dispositivos y servicios reduce el código de hello necesita toowrite y permite el acceso de toomanage de TI.**  Dispositivos y servicios pueden obtener tokens de Azure AD con OAuth y usar esas API de web tooaccess de símbolos (tokens).  Con Azure AD puede evitar escribir código de autenticación complejo.  Puesto que las identidades de Hola de los dispositivos y servicios de Hola se almacenan en Azure AD, TI puede administrar las claves y la revocación en un solo lugar en lugar de tener toodo esto por separado en la aplicación.

## <a name="benefits-of-integration"></a>Ventajas de la integración
Integración con Azure AD incluye ventajas que no requieren código adicional toowrite.

### <a name="integration-with-enterprise-identity-management"></a>Integración con administración de identidades empresariales
**Ayude a su aplicación a cumplir las políticas de TI.**  Las organizaciones integran sus sistemas de administración de identidades empresarial con Azure AD, por lo que cuando una persona que abandona una organización, automáticamente perderá acceso tooyour aplicación sin tootake de TI que requieren pasos adicionales.  TI puede administrar quién puede tener acceso a la aplicación y determinar qué directivas de acceso son necesarias, para la autenticación multifactor, ejemplo reduciendo su toocomply de necesidad toowrite código con las directivas corporativas complejas.  Azure AD proporciona a los administradores con un registro de auditoría detallada de quién firmó en aplicación tooyour, por lo que TI puede realizar un seguimiento de uso.

**Azure AD amplía nube toohello de Active Directory para que la aplicación pueda integrar con AD.**  Muchas organizaciones mundo Hola usan Active Directory como su inicio de sesión en la entidad de seguridad y el sistema de administración de identidades y requieren su toowork de aplicaciones con AD.  Integración con Azure AD para la integración de la aplicación con Active Directory

### <a name="advanced-security-features"></a>Características de seguridad avanzadas
**Multi-factor authentication.**  Azure AD proporciona Multi-factor Authentication nativa.  Los administradores de TI pueden requerir la autenticación multifactor tooaccess su aplicación, para que no tenga toocode esta compatibilidad usted mismo.  Obtenga más información sobre [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Detección de inicio de sesión erróneo.**  Azure AD procesa inicios de sesión de más de mil millones día, durante el uso de máquina actividad sospechosa de toodetect algoritmos de aprendizaje y notificar a los administradores de TI de posibles problemas.  Por compatibilidad con inicio de sesión en Azure AD, la aplicación presenta ventajas de Hola de esta protección. Más información sobre la [visualización del informe de acceso de Azure Active Directory](../active-directory-view-access-usage-reports.md).

**Acceso condicional.**  Además pueden requerir los administradores de autenticación multifactor toomulti, se cumplen determinadas condiciones antes de que los usuarios pueden iniciar sesión tooyour aplicación.  Las condiciones que se pueden establecer incluir intervalo de direcciones IP de Hola de dispositivos de cliente, la pertenencia en grupos especificados y el estado de hello de dispositivo de Hola que se usa para el acceso.  Más información sobre el [acceso condicional de Azure Active Directory](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Desarrollo sencillo
**Protocolos estándar del sector.**  Microsoft es toosupporting confirma los estándares del sector.  Azure AD admite los protocolos de autenticación de SAML 2.0, OpenID Connect 1.0, OAuth 2.0 y 1.2 de WS-Federation de Hola.  Hola API Graph es compatible con 4.0 de OData.  Si la aplicación ya admite Hola SAML 2.0 o protocolos de OpenID Connect 1.0 para inicio de sesión federada, agregar compatibilidad con Azure AD puede ser sencilla.  Más información sobre los [protocolos de autenticación admitidos de Azure AD](active-directory-authentication-protocols.md).

**Abra las bibliotecas de código abierto.**  Microsoft proporciona bibliotecas de código abierto totalmente compatible para el desarrollo de toospeed popular de lenguajes y plataformas.  código fuente de Hello es bajo licencia Apache 2.0 y son toofork libre y contribuir toohello atrás proyectos.  Más información sobre las [bibliotecas de autenticación de Azure AD](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Alta disponibilidad y presencia en todo el mundo
**Azure AD se implementa en centros de datos Hola mundo y administrado y supervisado alrededor de reloj de Hola.**  Azure AD es Hola sistema de administración de identidades de Microsoft Azure y Office 365 y se implementa en los centros de 28 datos alrededor de Hola a todos.  Datos de directorio se garantiza que los centros de datos de toobe replican tooat tres mínimos.  Equilibradores de carga global asegurarse a los usuarios acceder a la copia más cercana de Hola de Azure AD que contienen sus datos automáticamente vuelve a enrutar las solicitudes tooother centros de datos si se detecta un problema.

## <a name="next-steps"></a>Pasos siguientes
[Introducción a la escritura de código](active-directory-developers-guide.md#get-started)

[Inicio de sesión de usuario con Azure AD](active-directory-authentication-scenarios.md)

