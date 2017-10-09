---
title: "Tutorial: Integración de Azure Active Directory con Workstars | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a>Tutorial: integración de Azure Active Directory con Workstars

En este tutorial, aprenderá cómo toointegrate Workstars con Azure Active Directory (Azure AD).

Integración Workstars con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooWorkstars.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkstars (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Workstars tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Workstars

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Workstars desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-workstars-from-hello-gallery"></a>Agregar Workstars desde la Galería de Hola
integración de hello tooconfigure de Workstars en Azure AD, deberá tooadd Workstars de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Workstars de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **Workstars**, seleccione **Workstars** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Workstars en la lista de resultados de Hola](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workstars con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workstars es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workstars debe toobe establecido.

En Workstars, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Workstars, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Workstars](#create-a-workstars-test-user)**  -toohave un equivalente de Britta Simon en Workstars que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Workstars.

**inicio de sesión único en Azure AD tooconfigure con Workstars, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Workstars** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. En hello **Workstars dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    a. Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://workstars.com`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.workstars.com/saml/login_check`

    > [!NOTE] 
    > valor de Hello no es real. Valor de Hola de actualización con Hola dirección URL de respuesta real. Póngase en contacto con [equipo de soporte técnico Workstars](https://support.workstars.com) valor de hello tooget.
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. En hello **Workstars configuración** sección, haga clic en **configurar Workstars** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour Workstars como administrador.

8. En la barra de herramientas principal de hello, haga clic en **configuración**.

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. Vaya demasiado**inicio de sesión** > **configuración**.

    ![Inicio de sesión de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. En hello **único inicio de sesión en (SAML) - configuración** , siga los pasos de hello:
    
    ![SAML de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    a. En el cuadro de texto **Nombre del proveedor de identidad**, escriba **Office 365**.

    b. Hola **Id. de entidad de proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.

    c. Copie el contenido de Hola Hola descargado del archivo de certificado en el Bloc de notas y, a continuación, péguelo en hello **x509 certificado** cuadro de texto. 

    d. Hola **dirección URL SSO SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.
    
    e. Hola **dirección URL de cierre de sesión remoto** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure. 

    f. Seleccione **Id. de nombre** como **Correo electrónico (predeterminado)**.

    g. Haga clic en **Confirmar**.
    
> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
  
### <a name="create-a-workstars-test-user"></a>Creación de un usuario de prueba de Workstars

En esta sección, se crea un usuario denominado Britta Simon en Workstars. Trabajar con [equipo de soporte técnico Workstars](https://support.workstars.com) a los usuarios de tooadd hello en la plataforma de Workstars Hola.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkstars.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooWorkstars, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Workstars**.

    ![vínculo de Workstars Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Workstars el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Workstars aplicación.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

