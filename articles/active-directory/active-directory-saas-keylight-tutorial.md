---
title: "Tutorial: Integración de Azure Active Directory con LockPath Keylight | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Tutorial: Integración de Azure Active Directory con LockPath Keylight

En este tutorial, aprenderá cómo toointegrate LockPath Keylight con Azure Active Directory (Azure AD).

Integración LockPath Keylight con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooLockPath luz clave
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLockPath luz clave (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con LockPath Keylight tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en LockPath Keylight

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar LockPath Keylight desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Agregar LockPath Keylight desde la Galería de Hola
integración de hello tooconfigure de LockPath Keylight en Azure AD, deberá tooadd LockPath Keylight de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd LockPath Keylight desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **LockPath Keylight**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. En el panel de resultados de hello, seleccione **LockPath Keylight**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con LockPath Keylight con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LockPath Keylight es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LockPath Keylight debe toobe establecido.

En LockPath Keylight, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con LockPath Keylight, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba LockPath Keylight](#creating-a-lockpath-keylight-test-user) ** -toohave un equivalente de Britta Simon en LockPath Keylight que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación LockPath Keylight.

**inicio de sesión único en Azure AD tooconfigure con LockPath Keylight, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **LockPath Keylight** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. En hello **LockPath luz clave dominio y las direcciones URL** sección, lleve a cabo pasos de hello::

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.keylightgrc.com/`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.keylightgrc.com`

    c. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Póngase en contacto con [equipo de soporte técnico de cliente de luz clave LockPath](https://www.lockpath.com/contact/) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. En hello **LockPath luz clave configuración** sección, haga clic en **configurar luz de clave de LockPath** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable SSO en LockPath Keylight, lleve a cabo Hola pasos:
   
    a. Inicio de sesión tooyour LockPath Keylight cuenta como administrador.
    
    b. En el menú de hello en la parte superior de hello, haga clic en **persona**y seleccione **el programa de instalación de luz clave**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. En vista de árbol de Hola Hola izquierda, haga clic en **SAML**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. En hello **configuración SAML** cuadro de diálogo, haga clic en **editar**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/404.png) 

8. En hello **modificar configuración de SAML** cuadro de diálogo, siga los pasos de hello:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Establecer **autenticación SAML** demasiado**Active**.

    b. Hola pegar **SAML Single Sign-On dirección URL del servicio** valor que haya copiado desde Hola portal de Azure en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.

    c. Hola pegar **dirección URL del servicio de cierre de sesión único** valor que haya copiado desde Hola portal de Azure en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.

    d. Haga clic en **Elegir archivo** tooselect su LockPath Keylight descargado de certificado y, a continuación, haga clic en **abiertos** certificado de hello tooupload.

    e. Establecer **ubicación de Id. de usuario de SAML** demasiado**elemento NameIdentifier de instrucción de sujeto de hello**.
    
    f. Proporcionar hello **proveedor de servicios de luz clave** con hello sigue el patrón: **https://&lt;CompanyName&gt;. keylightgrc.com**.
    
    g. Establecer **a los usuarios de aprovisionamiento automático** demasiado**Active**.

    h. Establecer **tipo de cuenta de aprovisionamiento automático** demasiado**usuario completo**.

    i. Establezca **Auto-provision security role** (Rol de seguridad de aprovisionamiento automático) y seleccione **Standard User with SAML** (Usuario estándar con SAML).
    
    j. Establezca **Auto-provision security config** (Configuración de seguridad de aprovisionamiento automático) y seleccione **Standard User Configuration** (Configuración de usuario estándar).
     
    k. Hola **atributo de correo electrónico** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. Hola **atributo de nombre** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. Hola **último atributo de nombre** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Creación de un usuario de prueba de LockPath Keylight

En esta sección, creará un usuario llamado Britta Simon en LockPath Keylight. LockPath Keylight admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

No hay ningún elemento de acción para usted en esta sección. Se crea un nuevo usuario al tener acceso a LockPath Keylight si el usuario de hello no existe todavía. 

>[!NOTE]
>Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de cliente de luz clave LockPath](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLockPath luz clave.

![Asignar usuario][200] 

**tooassign Britta Simon tooLockPath luz clave, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **LockPath Keylight**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello LockPath Keylight el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour LockPath Keylight aplicación. 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

