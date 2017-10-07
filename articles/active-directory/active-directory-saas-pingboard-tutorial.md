---
title: "Tutorial: Integración de Azure Active Directory con Pingboard | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Tutorial: Integración de Azure Active Directory con Pingboard

En este tutorial, aprenderá cómo toointegrate Pingboard con Azure Active Directory (Azure AD).

Integración Pingboard con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooPingboard
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPingboard (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Pingboard tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción a Pingboard habilitada para inicio de sesión único

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Pingboard desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-pingboard-from-hello-gallery"></a>Agregar Pingboard desde la Galería de Hola
integración de hello tooconfigure de Pingboard en Azure AD, deberá tooadd Pingboard de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Pingboard de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Pingboard**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. En el panel de resultados de hello, seleccione **Pingboard**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pingboard con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Pingboard es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Pingboard debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Pingboard.

tooconfigure y prueba de inicio de sesión único en Azure AD con Pingboard, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Pingboard](#creating-a-pingboard-test-user) ** -toohave un equivalente de Britta Simon en Pingboard que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Pingboard.

**inicio de sesión único en Azure AD tooconfigure con Pingboard, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **Pingboard** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. En hello **Pingboard dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. Hola **identificador** cuadro de texto, valor de tipo hello como:`http://<entity-id>.pingboard.com/sp`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tener tooupdate estos valores con hello URL de identificador y la respuesta real. Aquí le sugerimos toouse Hola único valor de cadena en hello identificador. Póngase en contacto con [equipo de soporte técnico de cliente de Pingboard](https://support.pingboard.com/) tooget estos valores. 

4. Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`http://<sub-domain>.pingboard.com/sign_in`
     
5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure SSO en el lado de Pingboard, abra una nueva ventana del explorador e inicie sesión tooyour Pingboard cuenta. Debe ser un tooset de administración de Pingboard seguridad de inicio de sesión único en.

8. En el menú superior Hola seleccione **aplicaciones > integraciones**

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  En hello **integraciones** página, busque hello **"Azure Active Directory"** icono y haga clic en él.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. Hola modal que sigue a haga clic en **"Configurar"**

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. En hello después de la página, observará que "integración de Azure SSO está habilitada.". Abra Hola descargado el archivo de Metadata XML en un Hola el Bloc de notas y pegar contenido en **metadatos de IDP**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. se validará el archivo Hello y, si todo es correcto, ahora se habilitará el inicio de sesión único

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-pingboard-test-user"></a>Creación de un usuario de prueba de Pingboard

En orden tooenable toolog de los usuarios de Azure AD en Pingboard, se les deben aprovisionar en Pingboard.  
En caso de hello de Pingboard, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour Pingboard sitio de su compañía como administrador.

2. Haga clic en el botón **“Add Employee”** (Agregar empleado) en la página **Directory** (Directorio).

    ![Agregar empleado](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. En hello **"Agregar empleado"** cuadro de diálogo, siga los pasos de Hola.

    ![Invitar a contactos](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. Hola **nombre completo** cuadro de texto, nombre completo de tipo hello de Britta Simon.

    b. Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.

    c. Hola **puesto** cuadro de texto, puesto de trabajo de tipo hello de Britta Simon.

    d. Hola **ubicación** ubicación seleccione Hola de Britta Simon de lista desplegable.
    
    e. Haga clic en **Agregar**.   

4. Adición de hello tooconfirm de usuario aparecerá una pantalla de confirmación.
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooPingboard de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooPingboard, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Pingboard**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Pingboard Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Pingboard aplicación.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
