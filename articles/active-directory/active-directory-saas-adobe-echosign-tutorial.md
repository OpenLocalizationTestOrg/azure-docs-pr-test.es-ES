---
title: "Tutorial: Integración de Azure Active Directory con Adobe Sign | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el inicio de sesión de Adobe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Tutorial: integración de Azure Active Directory con Adobe Sign

En este tutorial, aprenderá cómo toointegrate Adobe iniciar sesión con Azure Active Directory (Azure AD).

Integración de inicio de sesión de Adobe con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooAdobe inicio de sesión
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAdobe inicio de sesión (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con inicio de sesión de Adobe, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Adobe Sign

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar el inicio de sesión de Adobe desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-adobe-sign-from-hello-gallery"></a>Agregar el inicio de sesión de Adobe desde la Galería de Hola
integración de hello tooconfigure de inicio de sesión de Adobe en Azure AD, deberá tooadd inicio de sesión de Adobe en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd inicio de sesión de Adobe desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **inicio de sesión de Adobe**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. En el panel de resultados de hello, seleccione **inicio de sesión de Adobe**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Adobe Sign con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el inicio de sesión de Adobe es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el inicio de sesión de Adobe debe toobe establecido.

En el inicio de sesión de Adobe, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con inicio de sesión de Adobe, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Creación de un usuario de prueba de inicio de sesión de Adobe](#creating-an-adobe-sign-test-user)**  -toohave un equivalente de Britta Simon en Inicio de sesión de Adobe es representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de inicio de sesión de Adobe.

**inicio de sesión único en Azure AD tooconfigure con inicio de sesión de Adobe, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **inicio de sesión de Adobe** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. En hello **direcciones URL y el dominio de inicio de sesión de Adobe** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.echosign.com/`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de inicio de sesión de Adobe](https://helpx.adobe.com/in/contact/support.html) tooget estos valores. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. En hello **configuración de inicio de sesión de Adobe** sección, haga clic en **configurar inicio de sesión de Adobe** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de inicio de sesión de Adobe tooyour como administrador.

8. En el menú de hello en la parte superior de hello, haga clic en **cuenta**y, a continuación, en panel de navegación de hello en el lado izquierdo de hello, haga clic en **configuración SAML** en **configuración de la cuenta**.
   
   ![Cuenta](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Cuenta")

9. En la sección Configuración de SAML de hello, realizar Hola pasos:
   
   ![Configuración de SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Configuración de SAML")
   
   a. En **SAML Mode** (Modo de SAML), seleccione **SAML Mandatory** (SAML obligatorio).
   
   b. Seleccione **toolog de permitir que los administradores de cuentas de EchoSign con las credenciales de EchoSign**.
   
   c. En **User Creation** (Creación de usuario), seleccione **Automatically add users authenticated through SAML** (Agregar automáticamente usuarios autenticados a través de SAML).

10. Desplazarse, realizar Hola siguiendo los pasos:

       ![Configuración de SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Configuración de SAML")

    a. Pegar **Id. de entidad SAML**, que han copiado desde el portal de Azure en hello **Id. de entidad IdP** cuadro de texto.
    
    b. Pegar **SAML Single Sign-On dirección URL del servicio**, que han copiado desde el portal de Azure en hello **dirección URL de inicio de sesión IdP** cuadro de texto.
   
    c. Pegar **dirección URL de cierre de sesión**, que han copiado desde el portal de Azure en hello **IdP Logout URL** cuadro de texto.

    d. Abra su descargado **Certificate(Base64)** un archivo en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado IdP** cuadro de texto

    e. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Creación de un usuario de prueba de Adobe Sign

toolog de los usuarios de Azure AD tooenable en tooAdobe inicio de sesión, se les deben aprovisionar en Inicio de sesión de Adobe. En caso de hello de inicio de sesión de Adobe, el aprovisionamiento es una tarea manual.

>[!NOTE]
>Puede usar cualquier otro inicio de sesión de Adobe herramienta cuentas de usuario creación o las API proporcionadas por el inicio de sesión de Adobe tooprovision cuentas de usuario AAD. 

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **inicio de sesión de Adobe** como administrador.

2. En el menú de hello en la parte superior de hello, haga clic en **cuenta**y, a continuación, en panel de navegación de hello en el lado izquierdo de hello, haga clic en **usuarios y grupos**y, a continuación, haga clic en **crear un nuevo usuario**.
   
   ![Cuenta](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Cuenta")
   
3. Hola **crear nuevo usuario** sección, lleve a cabo Hola pasos:
   
   ![Creación de usuarios](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Creación de usuarios")
   
   a. Hola de tipo **dirección de correo electrónico**, **nombre**, y **Last Name** de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.
   
   b. Haga clic en **Crear usuario**.

>[!NOTE]
>titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarla. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAdobe inicio de sesión.

![Asignar usuario][200] 

**tooassign Britta Simon tooAdobe inicio de sesión, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **inicio de sesión de Adobe**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Al hacer clic en hello Adobe signo disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación de inicio de sesión de Adobe.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

