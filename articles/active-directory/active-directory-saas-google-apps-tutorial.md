---
title: "Tutorial: Integración de Azure Active Directory con Google Apps en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Tutorial: Integración de Azure Active Directory con Google Apps

En este tutorial, aprenderá cómo toointegrate Google Apps con Azure Active Directory (Azure AD).

Integración de Google Apps con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooGoogle aplicaciones
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGoogle aplicaciones (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea tooknow obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Google Apps, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Google Apps

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Tutorial en vídeo
¿Cómo tooEnable Single Sign-On tooGoogle aplicaciones en 2 minutos:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Preguntas frecuentes
1. **P: ¿Son los Chromebooks y otros dispositivos Chrome compatibles con el inicio de sesión único de Azure AD?**
   
    R: Sí, los usuarios son pueda toosign en sus dispositivos Chromebook con sus credenciales de Azure AD. Consulte este [artículo de soporte técnico de Google Apps](https://support.google.com/chrome/a/answer/6060880) para información sobre por qué puede que se pidan las credenciales a los usuarios dos veces.

2. **P: ¿si se habilita el inicio de sesión único, volverá a los usuarios ser capaz de toouse su toosign de credenciales de Azure AD en cualquier producto de Google, como aula de Google, GMail, Google Drive, YouTube etc.?**
   
    R: Sí, dependiendo de [qué aplicaciones de Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) elige tooenable o deshabilitar para su organización.

3. **P: ¿Puedo habilitar el inicio de sesión único solo para un subconjunto de mis usuarios de Google Apps?**
   
    R: no, activar inmediatamente en el inicio de sesión único requiere que todos los tooauthenticate de los usuarios de Google Apps con sus credenciales de Azure AD. Dado que Google Apps no admite tener varios proveedores de identidad, proveedor de identidades de Hola para su entorno de Google Apps puede ser Azure AD o Google, pero no ambos al Hola mismo tiempo.

4. **P: ¿si un usuario ha iniciado sesión a través de Windows, son que se autentican automáticamente aplicaciones tooGoogle sin que se le pide una contraseña?**
   
    R: Hay dos opciones para habilitar este escenario. En primer lugar, los usuarios podrían iniciar sesión en dispositivos Windows 10 a través de [Azure Active Directory Join](active-directory-azureadjoin-overview.md). Como alternativa, podrían iniciar sesión a los usuarios en los dispositivos de Windows que usan tooan Unidos a un dominio de Active Directory que se ha habilitado para único inicio de sesión tooAzure AD a través de local a un [los servicios de federación de Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) implementación. Ambas opciones requieren pasos de hello tooperform Hola después tutorial tooenable inicio de sesión único entre Azure AD y Google Apps.

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar aplicaciones de Google de la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-google-apps-from-hello-gallery"></a>Agregar aplicaciones de Google de la Galería de Hola
integración de hello tooconfigure de Google Apps en Azure AD, deberá tooadd Google Apps en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Google Apps en Galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Google Apps**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. En el panel de resultados de hello, seleccione **Google Apps**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Google Apps con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Google Apps es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Google Apps debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Google Apps.

tooconfigure y prueba de inicio de sesión único en Azure AD con Google Apps, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Google Apps](#creating-a-google-apps-test-user) ** -toohave un equivalente de Britta Simon en Google Apps que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Google Apps.

**inicio de sesión único en tooconfigure Azure AD con Google Apps, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Google Apps** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. En hello **dominio de Google Apps y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Este valor no es real. Actualice el valor de hello con URL de inicio de sesión real de Hola. Póngase en contacto con hello [equipo de soporte técnico de Google](https://www.google.com/contact/).
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. En hello **configuración de aplicaciones de Google** sección, haga clic en **configurar Google Apps** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, SAML Single Sign-On dirección URL del servicio y cambio de dirección URL de contraseña** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Abra una nueva pestaña en el explorador e inicie sesión en hello [consola de administración de aplicaciones de Google](http://admin.google.com/) con su cuenta de administrador.

8. Haga clic en **Seguridad**. Si no ve el vínculo de hello, puede estar oculto bajo hello **más controles** menú situado en la parte inferior de Hola de pantalla de bienvenida.
   
    ![Haga clic en Seguridad.][10]

9. En hello **seguridad** página, haga clic en **configurar el inicio de sesión único (SSO).**
   
    ![Haga clic en SSO.][11]

10. Lleve a cabo Hola después de los cambios de configuración:
   
    ![Configuración de SSO][12]
   
    a. Seleccione **Configurar SSO con un proveedor de identidades de terceros**.

    b. En el **URL de la página de inicio de sesión** en Google Apps, a continuación, pegue el valor de Hola de **URL de servicio de inicio de sesión único**, que haya copiado desde el portal de Azure.

    c. Hola **URL de la página de cierre de sesión** en Google Apps, a continuación, pegue el valor de Hola de **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure. 

    d. Hola **cambiar dirección URL de contraseña** en Google Apps, a continuación, pegue el valor de Hola de **cambiar dirección URL de contraseña**, que haya copiado desde el portal de Azure. 

    e. En aplicaciones de Google, para hello **certificado de verificación**, certificado de Hola de carga que ha descargado desde el portal de Azure.

    f. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-google-apps-test-user"></a>Creación de un usuario de prueba de Google Apps

objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Software de aplicaciones de Google. Google Apps admite el aprovisionamiento automático, que está habilitado de manera predeterminada. El usuario no tiene que hacer nada en esta sección. Si un usuario ya no existe en el Software de aplicaciones de Google, se crea uno nuevo si intentas tooaccess Software de aplicaciones de Google.

>[!NOTE] 
>Si necesita un usuario toocreate manualmente, póngase en contacto con hello [equipo de soporte técnico de Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooGoogle aplicaciones.

![Asignar usuario][200] 

**tooassign Britta Simon tooGoogle aplicaciones, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Google Apps**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, tootest Hola de su inicio de sesión configuración de inicio único, abra Panel de acceso en [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), a continuación, inicie sesión en la cuenta de prueba de Hola y haga clic en **Google Apps** el icono Servicios Hola Panel de acceso.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png