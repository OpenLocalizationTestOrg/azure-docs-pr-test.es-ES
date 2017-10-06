---
title: "aaaProblems iniciar sesión en la aplicación de galería no tooa configurado para federado inicio de sesión único | Documentos de Microsoft"
description: "Guía para problemas específicos de Hola que pueden darse al iniciar sesión en la aplicación de tooan configurada para basado en SAML federado inicio de sesión único con Azure AD"
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a>Problemas para iniciar sesión en aplicación de la Galería no de tooa configurada para un inicio de sesión único federado

tootroubleshoot su problema, necesita tooverify configuración de la aplicación hello en Azure AD como sigue:

-   Ha seguido todos los pasos de configuración de Hola para hello aplicación de la Galería de Azure AD.

-   Identificador Hello y dirección URL de respuesta que se configura en AAD coinciden únicamente valores esperados en la aplicación hello

-   Que haya asignado a los usuarios de aplicación toohello

## <a name="application-not-found-in-directory"></a>No se encontró la aplicación en el directorio

*AADSTS70001 de error: No se encontró la aplicación con el identificador 'https://contoso.com' en el directorio de hello*.

**Causa posible**

atributo de emisor de Hola se envía desde Hola aplicación tooAzure AD en la solicitud SAML de hello no coincide con el valor de identificador hello configurado en la aplicación hello Azure AD.

**Resolución**

Asegúrese de que ese atributo de emisor de hello en solicitud SAML de Hola que coincidentes Hola valor de identificador configurado en Azure AD:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  <span id="_Hlk477190042" class="anchor"></span>Vaya demasiado**dominio y las direcciones URL** sección. Compruebe que Hola el valor en hello identificador cuadro de texto es que coincida con el valor de hello para el valor de identificador de hello muestra error Hola.

Después de que ha actualizado el valor de identificador hello en Azure AD y su valor de hello coincidente envía por la aplicación hello en solicitud SAML de hello, debe ser capaz de toosign en toohello aplicación.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>dirección de respuesta de Hello no coincide con direcciones de respuesta de hello configuradas para la aplicación hello. 

*Error AADSTS50011: dirección de respuesta de hello 'https://contoso.com' no coincide con direcciones de respuesta de hello configuradas para la aplicación hello* 

**Causa posible** 

Hola AssertionConsumerServiceURL valor en la solicitud SAML de hello no coincide con valor de dirección URL de respuesta de Hola o un modelo configurado en Azure AD. Hola AssertionConsumerServiceURL valor en la solicitud SAML de hello es dirección URL de hello consulte Error Hola. 

**Resolución** 

Asegúrese de ese valor de AssertionConsumerServiceURL hello en solicitud SAML de hello su coincidencia Hola valor de dirección URL de respuesta configurado en Azure AD. 
 
1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.** 

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola. 

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento. 

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory. 

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones. 

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**
  
6.  Seleccione la aplicación hello desea tooconfigure inicio de sesión único

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Vaya demasiado**dominio y las direcciones URL** sección. Compruebe o actualice el valor de Hola Hola valor AssertionConsumerServiceURL en la solicitud SAML de Hola de Hola de toomatch de cuadro de texto dirección URL de respuesta.

  * Si no ve el cuadro de texto de dirección URL de respuesta de hello, seleccione hello **mostrar avanzadas de configuración de direcciones URL** casilla de verificación. 

Una vez que ha actualizado el valor de dirección URL de respuesta de hello en Azure AD y tiene que coincide con el valor de hello envía por la aplicación hello en hello solicitud SAML, debe ser capaz de toosign en toohello aplicación.

## <a name="user-not-assigned-a-role"></a>Usuario no asignado a un rol

*Error AADSTS50105: Hola firmado en el usuario 'brian@contoso.com' no está asignado el rol de tooa para la aplicación hello*

**Causa posible**

usuario Hello no se ha concedido acceso toohello aplicación en Azure AD.

**Resolución**

tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.

7.  Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.

9.  Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.

10. Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.

11. Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**. Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.

12. **Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.

13. Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.

14. **Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.

15. Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.

Tras un breve período de tiempo, los usuarios de Hola que seleccionó ser capaz de toolaunch dichas aplicaciones usan Hola métodos descritos en la sección de descripción de solución de Hola.

## <a name="not-a-valid-saml-request"></a>No es una solicitud SAML válida

*Error AADSTS75005: solicitud de hello no es un mensaje de protocolo de Saml2 válido.*

**Causa posible**

Azure AD no es compatible con hello SAML enviado por la aplicación hello para el inicio de sesión único de la solicitud. Algunos de los problemas más comunes son:

-   Faltan campos obligatorios en la solicitud SAML de Hola

-   Método codificado de la solicitud SAML

**Resolución**

1.  Capture la solicitud SAML. Siga el tutorial de hello en [cómo toodebug basado en SAML single sign-on tooapplications en Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn cómo solicitar toocapture Hola SAML.

2.  Póngase en contacto con el proveedor de la aplicación hello y recurso compartido:

    -   La solicitud SAML

    -   [Los requisitos del protocolo SAML de inicio de sesión único de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Debe validar admiten la implementación de Azure AD SAML hello para el inicio de sesión único.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Ningún recurso en la lista requiredResourceAccess

*Error AADSTS65005: aplicación de cliente de hello ha solicitado acceso tooresource ' 00000002-0000-0000-c000-000000000000'. Error en esta solicitud porque Hola de cliente no especifica este recurso en su lista de requiredResourceAccess*.

**Causa posible**

objeto de la aplicación Hello está dañado.

**Resolución**

problema de hello toosolve, aplicación hello de quitar del directorio de Hola. A continuación, agregar y volver a configurar aplicación hello, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Haga clic en **eliminar** en hello superior izquierda de la aplicación hello **Introducción** hoja.

8.  Actualizar Azure AD y agregar la aplicación hello de galería de Azure AD de Hola. A continuación, Configure la aplicación hello nuevo.

Después de volver a configurar la aplicación hello, debe ser capaz de toosign en toohello aplicación.

## <a name="certificate-or-key-not-configured"></a>Certificado o clave no configurados

Error AADSTS50003: No hay configurada ninguna clave de firma.

**Causa posible**

objeto de aplicación Hola está dañado y Azure AD no reconoce el certificado de hello configurado para la aplicación hello.

**Resolución**

toodelete y cree un nuevo certificado, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en **crear un nuevo certificado** en hello **SAML certificado de firma** sección.

9.  Seleccione la fecha de expiración. A continuación, haga clic en **Guardar**.

10. Comprobar **activar el nuevo certificado** certificados de active toooverride Hola. A continuación, haga clic en **guardar** princip Hola de hoja de Hola y acepte el certificado de sustitución de tooactivate Hola.

11. En hello **el certificado de firma de SAML** sección, haga clic en **quitar** tooremove hello **Unused** certificado.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Problema al personalizar las notificaciones SAML de hello envía tooan aplicación

toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
[Los requisitos del protocolo SAML de inicio de sesión único de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
