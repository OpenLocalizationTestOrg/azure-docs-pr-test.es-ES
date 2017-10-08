---
title: "aaaGet iniciado la integración de Azure AD con aplicaciones | Documentos de Microsoft"
description: "Este artículo es una guía de introducción a la integración de Azure Active Directory (AD) con aplicaciones locales y de nube."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Guía de introducción a la integración de Azure Active Directory con las aplicaciones
## <a name="overview"></a>Información general
Este tema es toogive previsto que una guía básica para la integración de aplicaciones con Azure Active Directory (AD). Cada una de las siguientes secciones de hello contienen un breve resumen de un tema más detallado para que pueda identificar qué partes de esta guía de introducción son tooyou relevante.  Siga los vínculos de Hola para un análisis más profundo sobre cada tema.

## <a name="before-you-begin-take-inventory"></a>Antes de comenzar, realizar un inventario
Antes de saltar toointegrating aplicaciones con Azure AD, es importante tooknow en el que es y dónde quiere toogo.  Hello siguientes preguntas son previsto toohelp pensar en el proyecto de integración de aplicaciones de Azure AD.

### <a name="application-inventory"></a>Inventario de aplicaciones
* ¿Dónde están todas las aplicaciones? ¿De quiénes son?
* ¿Qué tipo de autenticación necesitan las aplicaciones?
* ¿Quién tiene acceso toowhich aplicaciones?
* ¿Desea toodeploy una nueva aplicación?
  * ¿La integrará de forma interna y la implementará en una instancia de proceso de Azure?
  * ¿Va a utilizar uno que está disponible en hello Galería de aplicaciones de Azure?

### <a name="user-and-group-inventory"></a>Inventario de usuarios y grupos
* ¿Dónde residen las cuentas de usuario?
  * Active Directory local
  * Azure AD
  * Dentro de una base de datos de aplicaciones independiente de su propiedad
  * En aplicaciones no sancionadas
  * Todos Hola anterior
* ¿Qué permisos y asignaciones de rol tienen actualmente los usuarios individuales? ¿Necesita tooreview su acceso o ¿está seguro de que las asignaciones de acceso y el rol de usuario son adecuadas ahora?
* ¿Ya están los grupos establecidos en su Active Directory local?
  * ¿Cómo están organizados los grupos?
  * ¿Quiénes son los miembros del grupo de hello?
  * ¿Qué asignaciones de permisos o roles tienen actualmente grupos Hola?
* ¿Necesitará tooclean seguridad bases de datos de usuario o grupo antes de integrar?  (Esta es una pregunta bastante importante. Entrada y salida de elementos no utilizados).

### <a name="access-management-inventory"></a>Inventario de administración de acceso
* ¿Cómo administra actualmente tooapplications de acceso de usuario? ¿Necesita toochange?  ¿Ha tenido en cuenta otras formas de acceso de toomanage, como con [RBAC](role-based-access-control-configure.md) por ejemplo?
* ¿Quién tiene acceso toowhat?

Puede que no tenga hello tooall de respuestas de estas preguntas por adelantado pero no importa.  Esta guía puede ayudarle a responder a algunas de esas preguntas y a tomar algunas decisiones informadas.

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure y un directorio de Azure Active Directory.  Si todavía no dispone de una suscripción a Azure, puede probar Azure de forma gratuita durante 30 días. [pruébelo.](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Integración de aplicaciones con Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Búsqueda de aplicaciones de nube no sancionadas con Cloud App Discovery
Como se mencionó anteriormente, puede haber aplicaciones que no han sido administradas por su organización hasta ahora.  Como parte del proceso de inventario de hello, es posible toofind autorización aplicaciones en la nube. Consulte [Búsqueda de aplicaciones de nube no sancionadas con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Tipos de autenticación
Cada una de las aplicaciones puede tener requisitos de autenticación diferentes. Con Azure AD, pueden usar certificados de firma con aplicaciones que usan SAML 2.0, WS-Federation o protocolos de conexión OpenID, así como inicio de sesión único con contraseña. Para más información sobre los tipos de autenticación de aplicaciones para su uso con Azure AD, consulte [Administración de certificados para federada el inicio de sesión único federado en Azure Active Directory](active-directory-sso-certs.md) e [Inicio de sesión único basado en contraseña](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Habilitación de SSO con el proxy de la aplicación de Azure AD
Con el Proxy de aplicación de Microsoft Azure AD, puede proporcionar tooapplications de acceso que se encuentra dentro de la red privada de forma segura, desde cualquier lugar y en cualquier dispositivo. Cuando haya instalado un conector de proxy de aplicación dentro de su entorno, se podrá configurar con facilidad con Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Integración de aplicaciones con Azure AD
Hello siguientes artículos describen maneras diferentes de hello aplicaciones integran con Azure AD y ofrecen pautas.

* [Determinar qué toouse de Active Directory](active-directory-administer.md)
* [Uso de aplicaciones en la Galería de la aplicación de Azure de Hola](active-directory-appssoaccess-whatis.md)
* [Lista de tutoriales sobre integración de aplicaciones SaaS](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Administrar acceso tooapplications
Hello artículos siguientes describen maneras de administrar acceso tooapplications una vez que se han integrado con Azure AD al uso de conectores AD de Azure y Azure AD.

* [Administración de acceso tooapps con Azure AD](active-directory-managing-access-to-apps.md)
* [Automatización con conectores de Azure AD](active-directory-saas-app-provisioning.md)
* [Asignación de usuarios tooan aplicación](active-directory-applications-guiding-developers-assigning-users.md)
* [Asignar grupos de aplicación de tooan](active-directory-applications-guiding-developers-assigning-groups.md)
* [Uso compartido de cuentas](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Integración de aplicaciones personalizadas
Si está escribiendo una aplicación nueva y desea que los desarrolladores de tooassist de aprovechar la potencia de hello Azure AD, consulte [directrices a los desarrolladores](active-directory-applications-guiding-developers-for-lob-applications.md).

Si desea tooadd su toohello de aplicación personalizada Galería de aplicaciones de Azure, consulte ["Traiga su propia aplicación" con la configuración de SAML de autoservicio de Azure AD](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Otras referencias
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

