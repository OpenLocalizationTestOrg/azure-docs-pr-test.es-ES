---
title: "un inicio de sesión único para una aplicación de la Galería de Azure AD federado aaaHow tooconfigure | Documentos de Microsoft"
description: "Un inicio de sesión único para una existente Galería de Azure AD aplicación y utilice tutoriales tooget a trabajar rápidamente cómo federado tooconfigure"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD

Todas las aplicaciones en la Galería de hello Azure AD habilitado con capacidad de inicio de sesión único de empresa tiene un tutorial paso a paso disponible. Puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones detalladas paso a paso.

## <a name="overview-of-steps-required"></a>Introducción a los pasos necesarios
una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Agregar una aplicación de la Galería de Azure AD Hola](#add-an-application-from-the-azure-ad-gallery)

-   [Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperación de los metadatos y el certificado de Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Asignar a usuarios de aplicación toohello](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Agregar una aplicación de la Galería de Azure AD Hola

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.

6.  Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.

7.  Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.

8.  Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.

9.  Haga clic en **agregar** button, aplicación de hello tooadd.

Tras un breve período de tiempo, es que la hoja de configuración de la aplicación pueda toosee Hola.

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurar inicio de sesión único para una aplicación desde la Galería de Azure AD Hola

tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Coadministrador**.

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Seleccione **sesión basado en SAML** de hello **modo** lista desplegable.

9.  Especifique los valores de hello necesario en **dominio y las direcciones URL.** Deberá obtener estos valores del proveedor de la aplicación hello.

   1. aplicación de hello tooconfigure como SSO iniciado por el SP, Hola inicio de sesión en la dirección URL es un valor necesario. En algunas aplicaciones, Hola identificador también es un valor obligatorio.

   2. aplicación de hello tooconfigure como SSO iniciado por IdP, Hola dirección URL de respuesta es un valor necesario. En algunas aplicaciones, Hola identificador también es un valor obligatorio.

10. **Opcional:** haga clic en **mostrar avanzadas de configuración de direcciones URL** si desea que los valores no sean necesarios de hello toosee.

11. Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.

12. **Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.

  tooadd un atributo:
   
   1. Haga clic en **Agregar atributo**. Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.

   1. Haga clic en **Guardar**. Verá el nuevo atributo de hello en la tabla de Hola.

13. Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello. Además, tendrá las direcciones URL de metadatos de Hola y requiere un certificado toosetup SSO con la aplicación hello.

14. Haga clic en **guardar** configuración de toosave Hola.

15. Asignar a usuarios de aplicación de toohello.

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación

tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello ha configurado el inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable. Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.

  >[!NOTE] 
  >Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML. Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.
  >
  >

9.  atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.

   tooadd un atributo:
  
   1. Haga clic en **Agregar atributo**. Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.

   2. Haga clic en **Guardar**. Verá el nuevo atributo de hello en la tabla de Hola.

## <a name="download-hello-azure-ad-metadata-or-certificate"></a>Descargar los metadatos de Azure AD de Hola o certificado

metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  *  Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones**.

6.  Seleccionar aplicación hello ha configurado el inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna. Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.

Azure AD no proporciona la dirección URL tooget Hola metadatos. solo se pueden recuperar metadatos de Hola como un archivo XML.

## <a name="assign-users-toohello-application"></a>Asignar a usuarios de aplicación toohello

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

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a>Personalizar las notificaciones SAML de hello envía tooan aplicación

toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)



