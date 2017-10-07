---
title: "toochoose aaaHow qué aplicación escriba toouse al agregar una aplicación | Documentos de Microsoft"
description: "Entender Hola admitida tipos de aplicaciones se puede integrar con Azure AD y sus opciones de configuración relacionados"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>¿Cómo toochoose qué aplicación escriba toouse al agregar una aplicación

Este artículo le ayudará toounderstand Hola cuatro tipos principales de las aplicaciones que se puede integrar con Azure AD:

* Qué es compatible en cada una de ellas
* Por qué elegir una determinada aplicación
* ¿Cómo tooconfigure propiedades básicas de los de la aplicación, que cómo los usuarios son **aprovisionado**, o lo **inicio de sesión único** toouse de tecnología.

## <a name="supported-application-types-in-azure-ad"></a>Tipos de aplicaciones compatibles en Azure AD

Hola de Azure AD admite cuatro principales tipos de aplicaciones que se pueden agregar mediante **agregar** característica se encuentra en **aplicaciones empresariales**. Entre ellos se incluyen los siguientes:

-   **Aplicaciones de la Galería de Azure AD**: una aplicación que se ha integrado previamente para el inicio de sesión único con Azure AD.

-   **Las aplicaciones de Proxy de aplicación** : una aplicación que se ejecuta en su entorno local que desea que tooprovide segura inicio de sesión único en tooexternally.

-   **Aplicaciones personalizadas** : una aplicación que su organización desea toodevelop en Hola plataforma de desarrollo de aplicaciones de Windows Azure AD, pero que no exista todavía.

-   **Aplicaciones que no son de la Galería**: ¡traiga sus propias aplicaciones! Cualquier vínculo web que desee, cualquier aplicación que representa un campo de nombre de usuario y contraseña, admite los protocolos de SAML u OpenID Connect o admite SCIM que desea toointegrate para el inicio de sesión único con Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Características y funcionalidades compatibles con todos los Hola por encima de los tipos de aplicación

Hello siguientes características son compatibles con cualquiera de Hola por encima de los 4 tipos de aplicación en Azure AD:

-   **Inicio rápido**: comience a trabajar con una aplicación rápidamente siguiendo [sencillos pasos de implementación](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started).

-   **Administración de las propiedades generales** : obtener un [vínculo profundo directa](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) aplicación tooan, [personalizar la personalización de marca de hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) de una aplicación, o [deshabilitar aplicación hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) para todos los usuarios.

-   **Administración de grupos y usuarios** : [asignar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) o [quitar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) aplicación tooan usuarios y grupos y, opcionalmente, asignar Hola determinados roles de aplicación estos usuarios y grupos tienen acceso a

-   **Acceso a la aplicación de autoservicio** : habilitar su toorequest usuarios [acceso a la aplicación de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan aplicación desde su acceso a la aplicación paneles mediante la adición de una aplicación directamente o [ unirse a un grupo habilitado autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), puede requerir la aprobación de negocio a lo largo de hello forma

-   **Registros de inicio de sesión** : vea [todos Hola aplicación de inicios de sesión tooan](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), o todas las aplicaciones

-   **Registros de auditoría** : vea [detallada de los registros de auditoría sobre la aplicación de modificaciones tooan](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), o tooall las aplicaciones

-   **Acceso condicional basado en riesgo y** : establezca eficaz [reglas de acceso basada en condiciones](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) que se aplican cuando los usuarios intentan toosign en tooa de aplicación específica

-   **Vista permisos** – ver ninguno de hello [OAuth2 permisos](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) una aplicación tiene acceso tooin su directorio desde un solo lugar

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modos de inicio de sesión único y de aprovisionamiento admitidos por tipos de aplicaciones específicas

Hola tabla siguiente describen Hola otro inicio de sesión único y el aprovisionamiento de modos admitidos por cada uno de Hola por encima de los tipos de aplicación. Puede usar esta tabla toohelp toounderstand qué aplicación debe tooadd toosupport un objetivo específico.

  ![Tabla de tipos de aplicaciones](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>¿Cómo toochoose un modo de inicio de sesión único

Hola admitida **inicio de sesión único** modos para aplicaciones de Azure AD se enumeran a continuación.

-   **Azure AD inicio de sesión único deshabilitado** : elija Azure AD inicio de sesión único deshabilitado **modo de inicio de sesión único** si aún no está listo toointegrate esta aplicación con el inicio de sesión único con Azure AD, o simplemente está probando horizontal

-   **Vinculados de inicio de sesión** : elija hello [en el inicio de sesión vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de inicio de sesión único** si tiene una aplicación que ya está conectada con una única inicio de sesión solución existente, o si su intención es toopublish una sencilla de vínculos para los usuarios en sus [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) o [iniciador de la aplicación de Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Sesión basado en contraseña** : elija hello [sesión basado en contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de inicio de sesión único** si la aplicación representa un campo de nombre de usuario y contraseña HTML y desea que toostore que nombre de usuario y una contraseña segura toobe reproducir toohello aplicación más tarde

-   **Sesión basado en SAML** : elija hello [sesión basado en SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) toospecific las funciones de aplicación en función de inicio de sesión único en modo si la aplicación es compatible con los protocolos SAML u OpenID Connect de Hola o desea que los usuarios pueden toomap de toobe en reglas que se definan en su SAML notificaciones *

   >[!NOTE]
   >Esta opción no está disponible cuando se configura el proxy de aplicación Hola para una aplicación.
   >
   >

-   **Basado en el encabezado de inicio de sesión** : elija esta opción [sesión basada en encabezado](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) inicio de sesión en modo de inicio único si tiene una aplicación que use PingAccess que admite el encabezado HTTP en función de autenticación que desee tooperform-inicio de sesión único en demasiado

   >[!NOTE]
   >Esta opción solo está disponible cuando se configura el proxy de aplicación de Hola y PingAccess para una aplicación.
   >
   >

-   **Autenticación de Windows integrada** : elija hello [autenticación integrada de Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) el inicio de sesión único en modo al exponer una aplicación de WIA local que desee tooperform-inicio de sesión único en demasiado

   >[!NOTE]
   >Esta opción solo está disponible cuando se configura el proxy de aplicación Hola para una aplicación.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Modos de inicio de sesión únicos para aplicaciones personalizadas

Las aplicaciones que ha personalizado desarrollado mediante hello [aplicación desarrollados de forma personalizada](#_Custom-Developed_Applications) experiencia también admiten únicos inicio de sesión modos adicionales no enumeradas anteriormente. Entre ellos se incluyen los siguientes:

-   Inicio de sesión basado en [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)

-   Inicio de sesión basado en [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)

-   Inicio de sesión basado en [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)

-   Inicio de sesión basado en [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)

Hola de lectura [Guía del desarrollador de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn más información acerca de cómo la aplicación toocreate desarrollados personalizada que admite estos único modos de inicio de sesión.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>¿Cómo tooset una aplicación del único modo de inicio de sesión

tooset una aplicación **inicio de sesión único** modo, siga las instrucciones de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccione la aplicación hello para el que desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

## <a name="how-toochoose-a-provisioning-mode"></a>¿Cómo toochoose un modo de aprovisionamiento

-   **Aprovisionamiento manual** : elija hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) modo de aprovisionamiento si dispone de las cuentas existentes o desea toomanage cuentas para esta aplicación fuera de Azure AD.

-   **Aprovisionamiento automático** : elija hello [automática](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **modo de aprovisionamiento** si desea tooenable basadas en la API el aprovisionamiento automático o la cancelación del aprovisionamiento de cuentas de usuario toothis aplicación 

   >[!NOTE]
   >Esta opción solo está disponible para las aplicaciones dentro de hello **tasky** categoría de hello [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **El aprovisionamiento automático basado en SCIM** : usar [el aprovisionamiento automático basado en SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) si la aplicación es compatible con protocolo de hello SCIM para detectar cambios toousers y los grupos, que se genera automáticamente para los cambios aplicación de tooany integrada con Azure AD 

   >[!NOTE]
   >Esta opción no aparece como un modo de aprovisionamiento específico, pero está habilitada de forma predeterminada para todas las aplicaciones que se integran con Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>¿Cómo tooset una aplicación del modo de aprovisionamiento

tooset una aplicación **aprovisionamiento** modo, siga las instrucciones de Hola a continuación:

tooset una aplicación **inicio de sesión único** modo, siga las instrucciones de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello para el que desea tooconfigure de aprovisionamiento.

7.  Una vez que se carga la aplicación hello, haga clic en **Provisioning** del menú de navegación izquierdo de la aplicación hello.

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)
