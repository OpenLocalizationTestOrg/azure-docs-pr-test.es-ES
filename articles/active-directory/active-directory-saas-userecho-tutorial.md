---
title: "Tutorial: Integración de Azure Active Directory con UserEcho | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a>Tutorial: integración de Azure Active Directory con UserEcho

En este tutorial, aprenderá cómo toointegrate UserEcho con Azure Active Directory (Azure AD).

Integración UserEcho con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooUserEcho
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooUserEcho (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con UserEcho tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción a UserEcho habilitada para inicio de sesión único

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar UserEcho desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-userecho-from-hello-gallery"></a>Agregar UserEcho desde la Galería de Hola
integración de hello tooconfigure de UserEcho en Azure AD, deberá tooadd UserEcho de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd UserEcho de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **UserEcho**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. En el panel de resultados de hello, seleccione **UserEcho**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con UserEcho con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en UserEcho es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en UserEcho debe toobe establecido.

En UserEcho, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con UserEcho, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba UserEcho](#creating-a-userecho-test-user)**  -toohave un equivalente de Britta Simon en UserEcho que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación UserEcho.

**inicio de sesión único en Azure AD tooconfigure con UserEcho, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **UserEcho** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. En hello **UserEcho dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.userecho.com/`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.userecho.com/saml/metadata/`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de UserEcho](https://feedback.userecho.com/) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. En hello **UserEcho configuración** sección, haga clic en **configurar UserEcho** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour UserEcho como administrador.

8. En la barra de herramientas de hello en la parte superior de hello, haga clic en el menú de hello tooexpand del nombre de usuario y, a continuación, haga clic en **el programa de instalación**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. Haga clic en **Integraciones**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. Haga clic en **Sitio web** y, después, en **Inicio de sesión único (SAML2)**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. En hello **inicio de sesión único (SAML)** , siga los pasos de hello:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    a. En **Habilitado para SAML**, seleccione **Sí**.
    
    b. Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **dirección URL SSO SAML** cuadro de texto.
    
    c. Pegar **dirección URL de cierre de sesión**, que haya copiado desde Hola portal de Azure en hello **logoout remoto URL** cuadro de texto.
    
    d. Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **certificado X.509** cuadro de texto.
    
    e. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-userecho-test-user"></a>Creación de un usuario de prueba de UserEcho

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en UserEcho toocreate.

**toocreate un usuario llamado Britta Simon en UserEcho, lleve a cabo Hola pasos:**

1. Sitio de empresa de UserEcho tooyour de inicio de sesión como administrador.

2. En la barra de herramientas de hello en la parte superior de hello, haga clic en el menú de hello tooexpand del nombre de usuario y, a continuación, haga clic en **el programa de instalación**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. Haga clic en **usuarios**, hello tooexpand **usuarios** sección.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. Haga clic en **Usuarios**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. Haga clic en **Invitar a un nuevo usuario**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. En hello **invitar a un nuevo usuario** cuadro de diálogo, realizar Hola pasos:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    a. Hola **nombre** cuadro de texto, nombre de tipo de usuario de hello como Britta Simon.
    
    b.  Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.
    
    c. Haga clic en **Invitar**.

Se envía una invitación tooBritta, lo que permite su toostart con UserEcho. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooUserEcho.

![Asignar usuario][200] 

**tooassign Britta Simon tooUserEcho, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **UserEcho**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.  

Al hacer clic en icono de UserEcho Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour UserEcho aplicación.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

