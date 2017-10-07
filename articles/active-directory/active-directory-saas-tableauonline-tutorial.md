---
title: "Tutorial: Integración de Azure Active Directory con Tableau Online | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y una plantilla en línea."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Tutorial: Integración de Azure Active Directory con Tableau Online

En este tutorial, aprenderá cómo toointegrate Tableau Online con Azure Active Directory (Azure AD).

Integración Tableau Online con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTableau en línea
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTableau en línea (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con una plantilla en línea, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Tableau Online

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar una plantilla en línea desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-tableau-online-from-hello-gallery"></a>Agregar una plantilla en línea desde la Galería de Hola
integración de hello tooconfigure de Tableau en línea en Azure AD, deberá tooadd Tableau en pantalla de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Tableau en línea desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Tableau en línea**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. En el panel de resultados de hello, seleccione **Tableau en línea**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Tableau Online con un usuario de prueba llamado Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en una plantilla en línea es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en una plantilla en línea debe toobe establecido.

En línea Tableau, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con una plantilla en línea, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Tableau en línea](#creating-a-tableau-online-test-user)**  -toohave un equivalente de Britta Simon en una plantilla en línea que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de una plantilla en línea.

**inicio de sesión único en tooconfigure Azure AD con una plantilla en línea realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Tableau en línea** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. En hello **Tableau en pantalla de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://sso.online.tableau.com`

    b. Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://sso.online.tableau.com/public/sp/<instancename>`

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. En otra ventana del explorador, inicio de sesión tooyour aplicación Tableau en línea. Vaya demasiado**configuración** y, a continuación, **autenticación**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML, en **tipos de autenticación** sección. Comprobar hello **inicio de sesión único con SAML** casilla de verificación.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Desplácese hacia abajo hasta la sección **Importar archivo de metadatos en Tableau Online** .  Haga clic en Examinar e importar el archivo de metadatos de Hola que ha descargado de Azure AD. A continuación, haga clic en **Aplicar**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. Hola **coincide con las aserciones** sección, inserte el nombre de aserción de proveedor de identidades correspondiente de Hola para **dirección de correo electrónico**, **nombre**, y **apellidos** . tooget esta información de Azure AD: 
  
    a. En Hola portal de Azure, vaya hello **Tableau en línea** página de integración de aplicaciones.
    
    b. En la sección de atributos hello, seleccione hello **"ver y editar todos los demás atributos de usuario"** casilla de verificación. 
    
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Copiar valor de espacio de nombres de Hola para estos atributos: Hola givenname, correo electrónico y surname utilizando lo siguiente:

   ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. Haga clic en el valor **user.givenname** 
    
    e. Copiar valor de Hola de hello **espacio de nombres** cuadro de texto.

   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. valores de espacio de nombres de hello toocopy para correo electrónico de Hola y surname siguen Hola pasos anteriores.

    g. Cambiar de aplicación de una plantilla en línea toohello, a continuación, establecer hello **Tableau en línea atributos** sección como sigue:
     * Correo electrónico: **mail** o **userprincipalname**
     * Nombre: **givenname**
     * Apellidos: **surname**
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-tableau-online-test-user"></a>Crear un usuario de prueba de Tableau Online

En esta sección, creará una usuaria llamada Britta Simon en Tableau Online.

1. En **Tableau Online**, haga clic en **Settings** (Configuración) y en la sección **Authentication** (Autenticación). Desplácese hacia abajo demasiado**Seleccionar usuarios** sección. Haga clic en **Add users** (Agregar usuarios) y en **Enter Email Addresses** (Especificar direcciones de correo electrónico).
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Seleccione **Add users for single sign-on (SSO) authentication**[Agregar usuarios para la autenticación mediante inicio de sesión único (SSO)]. Hola **escribir direcciones de correo electrónico** Agregar cuadro de textobritta.simon@contoso.com
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. Haga clic en **Crear**.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTableau en línea.

![Asignar usuario][200] 

**tooassign Britta Simon tooTableau en línea, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Tableau en línea**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono Tableau en línea Hola Hola Panel de acceso, deberá obtener la aplicación Tableau en línea tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

