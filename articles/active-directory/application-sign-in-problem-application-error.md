---
title: "aaaError en la página de la aplicación después de iniciar sesión | Documentos de Microsoft"
description: "Cómo tooresolve problemas con Azure AD iniciar sesión cuando la propia aplicación Hola emite un error"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Error en la página de aplicación después de iniciar sesión

En este escenario, Azure AD ha iniciado sesión el usuario de hello en pero aplicación hello muestra un error no permitir el inicio de sesión de hello usuario toosuccessfully finalizar hello en flujo. En este escenario, aplicación hello no acepta problema de respuesta de hello Azure AD.

Hay algunos motivos posibles por qué aplicación hello no aceptó la respuesta de Hola de Azure AD. Si el error de hello en la aplicación hello no es lo suficientemente claro tooknow ¿qué es, a continuación, falta de respuesta de hello:

-   Si aplicación hello Galería hello Azure AD, compruebe ha seguido todos los pasos de hello en el artículo hello [cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Utilice una herramienta como [Fiddler](http://www.telerik.com/fiddler) toocapture SAML solicitud, respuesta de SAML y el token SAML.

-   Compartir respuesta de SAML de hello con hello aplicación proveedor tooknow novedades que faltan.

## <a name="missing-attributes-in-hello-saml-response"></a>Atributos que faltan en hello respuesta de SAML

tooadd un atributo en toobe de configuración de Azure AD Hola enviado como respuesta de hello Azure AD, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en **ver y editar atributos de todos los demás usuarios en** hello **atributos de usuario** Hola de sección tooedit atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.

   tooadd un atributo:

   * Haga clic en **Agregar atributo**. Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.

   * Haga clic en **Guardar**. Verá el nuevo atributo de hello en la tabla de Hola.

9.  Guardar configuración de Hola.

Próxima vez Hola usuario inicia sesión en la aplicación toohello, Azure AD Enviar nuevo atributo de Hola Hola respuesta de SAML.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>aplicación Hello espera un valor de identificador de usuario diferente o un formato

Hello aplicación de inicio de sesión toohello error porque Hola respuesta de SAML no encuentra los atributos, como los roles o porque la aplicación hello espera un formato diferente para el atributo de EntityID Hola.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Agregue un atributo en la configuración de la aplicación hello Azure AD:

Hola toochange valor de identificador de usuario, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  En hello **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.

## <a name="change-entityid-user-identifier-format"></a>Cambiar el formato de EntityID (Identificador de usuario)

Si la aplicación hello espera otro formato para el atributo de EntityID Hola. A continuación, no será formato de tooselect capaz de hello EntityID (identificador de usuario) que Azure AD envía toohello aplicación en respuesta Hola después de la autenticación de usuario.

Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML. Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>aplicación Hello espera un método de firma diferente para hello respuesta de SAML

toochange ¿qué partes del token SAML de hello están firmados digitalmente por Azure Active Directory. Siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en **Mostrar configuración de firma de certificado avanzada** en hello **el certificado de firma de SAML** sección.

9.  Seleccione Hola adecuado **opción firma** esperado por la aplicación hello:

  * Firmar respuesta SAML

  * Firmar respuesta y aserción SAML

  * Firmar aserción SAML

Próxima vez Hola usuario inicia sesión en la aplicación toohello, inicio de sesión de Azure AD Hola parte de respuesta SAML de hello seleccionado.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>aplicación Hello espera Hola firma toobe algoritmo SHA-1

De forma predeterminada, Azure AD firma de token SAML de hello mediante Hola mayoría algoritmo de seguridad. No se recomienda cambiar el algoritmo de inicio de sesión de hello tooSHA-1, a menos que requiera la aplicación hello.

toochange Hola algoritmo de firma, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en **Mostrar configuración de firma de certificado avanzada** en hello **el certificado de firma de SAML** sección.

9.  Seleccione SHA-1, Hola **algoritmo de firma**.

Próxima vez Hola usuario inicia sesión en la aplicación toohello, inicio de sesión de Azure AD Hola token SAML utilizando el algoritmo SHA-1.

## <a name="next-steps"></a>Pasos siguientes
[¿Cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
