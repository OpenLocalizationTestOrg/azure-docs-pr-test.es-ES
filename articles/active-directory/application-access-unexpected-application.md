---
title: "aplicación de aaaUnexpected en la lista de aplicaciones | Documentos de Microsoft"
description: "¿Cómo toosee todas las aplicaciones en su inquilino y entender cómo las aplicaciones aparecen en la lista de todas las aplicaciones en las aplicaciones empresariales"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Aplicación inesperada en mi lista de aplicaciones

En este artículo le ayudarán a toounderstand cómo aparecen las aplicaciones en su **todas las aplicaciones** lista en **aplicaciones empresariales**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>¿Cómo toosee todas las aplicaciones en el inquilino

toosee todos Hola aplicaciones en su inquilino, deberá hello toouse **filtro** control tooshow **todas las aplicaciones** en hello **todas las aplicaciones** lista. toodo, a continuación siga los pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

6.  Haga clic en uso de Hola Hola **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones**.

7.  En hello **filtro** hoja, conjunto hello **mostrar** opción demasiado**todas las aplicaciones.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>¿Por qué aparece una aplicación específica en mi lista de todas las aplicaciones?

Cuando filtra demasiado**todas las aplicaciones**, hello **todas las aplicaciones** **lista** muestra todos los objetos de entidad de servicio en el inquilino. Los objetos de entidad de servicio pueden aparecer en esta lista de varias formas:

1.  Cuando se agrega cualquier aplicación desde la Galería de aplicaciones de hello, incluidos:

   1. **Aplicaciones de la Galería de Azure AD**: una aplicación que se ha integrado previamente para el inicio de sesión único con Azure AD.

   2. **Las aplicaciones de Proxy de aplicación** : una aplicación que se ejecuta en su entorno local que desea que tooprovide segura inicio de sesión único en tooexternally.

   3. **Aplicaciones personalizadas** : una aplicación que su organización desea toodevelop en Hola plataforma de desarrollo de aplicaciones de Windows Azure AD, pero que no exista todavía.

   4. **Aplicaciones que no son de la Galería**: ¡traiga sus propias aplicaciones! Cualquier vínculo web que desee, cualquier aplicación que representa un campo de nombre de usuario y contraseña, admite los protocolos de SAML u OpenID Connect o admite SCIM que desea toointegrate para el inicio de sesión único con Azure AD.

2.  Al registrarse o iniciar sesión en una aplicación de <sup>terceros</sup> integrada con Azure Active Directory. Un ejemplo de esto es [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  Al registrarse, o agregar un usuario de tooa de licencia o una aplicación de usuario primer grupo tooa, al igual que [Microsoft Office 365](http://products.office.com/).

4.  Cuando se agrega un nuevo registro de aplicación mediante la creación de una aplicación desarrollados de forma personalizada con hello [registro de aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Cuando se agrega un nuevo registro de aplicación mediante la creación de una aplicación desarrollados de forma personalizada con hello [Portal de registro de aplicación de V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Al agregar una aplicación que está desarrollando con los [métodos de autenticación de ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) o los [servicios conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) de Visual Studio.

7.  Cuando se crea un objeto de entidad de servicio con hello [módulo de PowerShell de Azure AD](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Cuando se [tooan aplicación de consentimiento](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) como un administrador toouse los datos en el inquilino.

9.  Cuando un [tooan aplicación consentimiento del usuario](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse datos en el inquilino.

10. Al habilitar determinados servicios que almacenan datos en el inquilino. Un ejemplo de esto es de restablecimiento de contraseña, que se modela como un toostore de entidad de seguridad de servicio la contraseña de directiva de restablecimiento de forma segura.

tooget obtener más información sobre cómo las aplicaciones se agregan directorio tooyour, leer [cómo y por qué aplicaciones se agregan tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Deseo tooremove aplicación de tooan de asignación de un usuario específico o un grupo

tooremove una aplicación tooan de asignación de usuario o grupo, siga los pasos de hello indicados en hello [quitar una asignación de usuario o grupo de una aplicación de empresa en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artículo.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Deseo toodisable todas las aplicaciones de tooan de acceso para cada usuario

toodisable todos los inicios de sesión tooan aplicación de usuario, siga los pasos de hello enumerados en hello [deshabilitar inicios de sesión de usuario para una aplicación de empresa en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artículo.

## <a name="i-want-toodelete-an-application-entirely"></a>Deseo toodelete una aplicación completamente

demasiado**eliminar una aplicación**, siga estas instrucciones hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccione la aplicación hello desea toodelete.

7.  Una vez que se carga la aplicación hello, haga clic en **eliminar** icono de la aplicación de hello superior **Introducción** hoja.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Deseo toodisable todas las aplicaciones de tooany de operaciones de consentimiento de usuario futuras

Deshabilitando el consentimiento del usuario para todo el directorio impedir que los usuarios finales consentimiento tooany aplicación. A pesar de ello, los administradores podrán seguir dando el consentimiento en nombre de los usuarios. toolearn más información acerca de la aplicación de consentimiento y por qué puede o no ser conveniente toodo, lea [usuario conocimiento y consentimiento del administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

demasiado**deshabilitar todas las operaciones de consentimiento de usuario futuras en todo el directorio**, siga estas instrucciones hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Configuración de usuario**.

6.  Deshabilitar todas las operaciones de consentimiento de usuario futuras establecer hello **a los usuarios pueden permitir aplicaciones tooaccess sus datos** alternar demasiado**No** y haga clic en hello **guardar** botón.

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)
