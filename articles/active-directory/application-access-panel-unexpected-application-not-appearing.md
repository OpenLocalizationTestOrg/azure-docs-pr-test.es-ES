---
title: "aplicación aaaAn asignado no aparece en el panel de acceso de hello | Documentos de Microsoft"
description: "Solucionar problemas de por qué una aplicación no aparece en el Panel de acceso de Hola"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a>Una aplicación asignada no aparece en el panel de acceso de Hola

Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a. Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola. aplicación Hello debe configurarse correctamente y asignado toohello usuario o un grupo de usuario de hello es miembro de la aplicación de hello toosee Hola Panel de acceso.

tipo Hello de aplicaciones posible que un usuario esté viendo se dividen en hello siguientes categorías:

-   Aplicaciones de Office 365

-   Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación

-   Aplicaciones de SSO basado en contraseña

-   Aplicaciones con soluciones SSO existentes

## <a name="general-issues-toocheck-first"></a>General emite toocheck primero

-   Si una aplicación se acaba de agregar usuario tooa, toosign de entrada y salida vuelva a intentarlo en el Panel de acceso del usuario de hello después de unos toosee minutos si se agrega la aplicación hello.

-   Si se acaba de quitar una licencia a un usuario o grupo de usuario de hello es que un miembro de este puede tardar mucho tiempo, según el tamaño de Hola y la complejidad del grupo de Hola para toobe cambios realizado. Permitir un tiempo adicional antes de iniciar sesión en el Panel de acceso de Hola.

## <a name="problems-related-tooapplication-configuration"></a>Configuración de tooapplication relacionados de problemas

Puede que una aplicación no aparezca en el panel de acceso de un usuario porque no está configurada correctamente. A continuación se muestran algunas maneras que se puede solucionar problemas de configuración de tooapplication relacionados de problemas:

-   [¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [¿Cómo tooconfigure federado inicio de sesión único para una aplicación no Galería](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [¿Cómo tooconfigure una contraseña única aplicación de inicio de sesión para una aplicación de la Galería de Azure AD](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [¿Cómo tooconfigure una contraseña única aplicación de inicio de sesión para una aplicación no Galería](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD

Todas las aplicaciones de la Galería de Azure AD Hola habilitado con capacidad de Enterprise Single Sign-On tiene un tutorial paso a paso disponible. Puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones paso a paso detallados.

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Agregar una aplicación de la Galería de Azure AD Hola](#add-an-application-from-the-azure-ad-gallery)

-   [Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperación de los metadatos y el certificado de Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Agregar una aplicación de la Galería de Azure AD Hola

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

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a>Configurar inicio de sesión único para una aplicación desde la Galería de Azure AD Hola

tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

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

   2. Haga clic en **Guardar**. Verá el nuevo atributo de hello en la tabla de Hola.

13. Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello. Además, tendrá las direcciones URL de metadatos de Hola y requiere un certificado toosetup SSO con la aplicación hello.

14. Haga clic en **guardar** configuración de toosave Hola.

15. Asignar a usuarios de aplicación de toohello.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación

tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello desea tooshow aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

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

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Descargar los metadatos de Azure AD de Hola o certificado

metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello ha configurado el inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna. Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.

    Azure AD no proporciona la dirección URL tooget Hola metadatos. solo se pueden recuperar metadatos de Hola como un archivo XML.

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a>¿Cómo tooconfigure federado inicio de sesión único para una aplicación no Galería

una aplicación no Galería tooconfigure, necesita toohave Azure AD premium y aplicación hello es compatible con SAML 2.0. Para más información acerca de las versiones de Azure AD, visite [Precios de Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).

-   [Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)](#configuring-single-sign-on)

-   [Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [Recuperación de los metadatos y el certificado de Azure AD](#download-the-azure-ad-metadata-or-certificate)

-   [Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a>Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)

tooconfigure inicio de sesión único para una aplicación que no está en la Galería de Azure AD de hello, siga Hola pasos siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.

6.  Haga clic en **aplicación gallery no** en hello **agregar su propia aplicación** sección.

7.  Escriba el nombre de Hola de aplicación Hola Hola **nombre** cuadro de texto.

8.  Haga clic en **agregar** button, aplicación de hello tooadd.

9.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

10. Seleccione **sesión basado en SAML** en hello **modo** lista desplegable.

11. Especifique los valores de hello necesario en **dominio y las direcciones URL.** Deberá obtener estos valores del proveedor de la aplicación hello.

   1. aplicación de hello tooconfigure como SSO iniciado por IdP, escriba Hola dirección URL de respuesta y Hola identificador.

   2.  **Opcional:** Hola de aplicación de hello tooconfigure como SSO iniciado por el SP, inicio de sesión en la dirección URL es un valor necesario.

12. Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.

13. **Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.

   tooadd un atributo:

   1. Haga clic en **Agregar atributo**. Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.

   2. Haga clic en **Guardar**. Verá el nuevo atributo de hello en la tabla de Hola.

14. Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello. Además, tiene las direcciones URL de Azure AD y certificados necesarios para la aplicación hello.

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a>Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación

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

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a>Descargar los metadatos de Azure AD de Hola o certificado

metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello ha configurado el inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna. Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.

Azure AD no proporciona la dirección URL tooget Hola metadatos. solo se pueden recuperar metadatos de Hola como un archivo XML.

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Agregar una aplicación de la Galería de Azure AD Hola](#add-an-application-from-the-azure-ad-gallery)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Agregar una aplicación de la Galería de Azure AD Hola

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

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar la aplicación hello para el inicio de sesión único en la contraseña

tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  [Asignar usuarios de aplicación de toohello](#how-to-assign-a-user-to-an-application-directly).

10. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Incorporación de una aplicación ajena a la galería](#add-a-non-gallery-application)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a>Incorporación de una aplicación ajena a la galería

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**.

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.

6.  Haga clic en **Aplicación situada fuera de la galería**.

7.  Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto. Seleccione **Agregar**.

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

#### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar la aplicación hello para el inicio de sesión único en la contraseña

tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

    1.  Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  Escriba hello **dirección URL de inicio de sesión**. Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a. Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.

10. [Asignar usuarios de aplicación de toohello](#how-to-assign-a-user-to-an-application-directly).

11. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemas relacionados tooassigning aplicaciones toousers

Un usuario puede no esté viendo una aplicación en su Panel de acceso porque no se les asignan toohello aplicación. A continuación se muestran algunas maneras toocheck:

-   [Comprobar si un usuario se ha asignado toohello aplicación](#check-if-a-user-is-assigned-to-the-application)

-   [¿Cómo tooassign directamente una aplicación de tooan de usuario](#how-to-assign-a-user-to-an-application-directly)

-   [Compruebe si un usuario se haya asignado tooa licencia relacionados con la aplicación toohello](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [¿Cómo tooassign un usuario de tooa de licencia](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a>Comprobar si un usuario se ha asignado toohello aplicación

toocheck si se asigna a un usuario toohello aplicación, siga Hola pasos siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

6.  **Búsqueda** como nombre de Hola de aplicación hello en cuestión.

7.  Haga clic en **Usuarios y grupos**.

8.  Compruebe toosee si el usuario se le asigna la aplicación toohello.

   * Si no siga los pasos de hello en "cómo tooassign una aplicación de usuario tooan directamente" toodo para.

### <a name="how-tooassign-a-user-tooan-application-directly"></a>¿Cómo tooassign directamente una aplicación de tooan de usuario

tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global**.

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

Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Comprobar si un usuario está sometido a una licencia relacionados con la aplicación toohello

toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

  * Si se asigna la licencia de Office tooan Esto activar tooappear de las aplicaciones de Office de primera entidad de usuario de Hola Hola Panel de acceso del usuario.

### <a name="how-tooassign-a-user-a-license"></a>¿Cómo tooassign un usuario una licencia 

tooassign un usuario tooa de licencias, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

8.  Haga clic en hello **asignar** botón.

9.  Seleccione **uno o más productos** en lista de Hola de productos disponibles.

10. **Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos. Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.

11. Haga clic en hello **asignar** botón tooassign estos usuario toothis de licencias.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemas relacionados tooassigning aplicaciones toogroups

Un usuario puede estar viendo una aplicación en su Panel de acceso ya que forman parte de un grupo que se ha asignado la aplicación hello. A continuación se muestran algunas maneras toocheck:

-   [Comprobar la pertenencia a grupos de un usuario](#check-a-users-group-memberships)

-   [¿Cómo tooassign una tooa de aplicación de grupo directamente](#how-to-assign-an-application-to-a-group-directly)

-   [Comprobar si un usuario forma parte del grupo asignado licencias tooa](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [¿Cómo tooassign un grupo de tooa de licencias](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a>Comprobar la pertenencia a grupos de un usuario

toocheck pertenencia de un grupo, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Grupos**.

8.  Compruebe toosee si el usuario es parte de una aplicación de toohello de grupo asignado.

  * Si desea que tooremove Hola usuario del grupo de hello, **haga clic en la fila de hello** del grupo de Hola y seleccione Eliminar.

### <a name="how-tooassign-an-application-tooa-group-directly"></a>¿Cómo tooassign una tooa de aplicación de grupo directamente

tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global**.

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.

7.  Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.

9.  Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.

10. Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.

11. Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**. Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.

12. **Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.

13. Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.

14. **Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.

15. Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.

Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a>Comprobar si un usuario forma parte del grupo asignado licencias tooa

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Grupos**.

8.  Haga clic en la fila de Hola de un grupo específico.

9.  Haga clic en **licencias** toosee qué grupo de licencias Hola asignó tooit.

   * Si se asigna el grupo de hello licencia de Office tooan en que esto, puede habilitar determinada tooappear de las aplicaciones de Office de primera entidad Hola Panel de acceso del usuario.

### <a name="how-tooassign-a-license-tooa-group"></a>¿Cómo tooassign un grupo de tooa de licencias

tooassign un grupo de tooa licencias, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los grupos**.

6.  **Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.

8.  Haga clic en hello **asignar** botón.

9.  Seleccione **uno o más productos** en lista de Hola de productos disponibles.

10. **Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos. Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.

11. Haga clic en hello **asignar** botón tooassign estos toothis de grupo de licencias. Esto puede tardar mucho tiempo, en función de hello tamaño y la complejidad del grupo de Hola.

>[!NOTE]
>toodo esto con mayor rapidez, considere la posibilidad de temporalmente asignar una licencia toohello usuario directamente. 
>
>

## <a name="next-steps"></a>Pasos siguientes
[Agregar nuevos usuarios tooAzure Active Directory](active-directory-users-create-azure-portal.md)

