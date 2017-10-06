---
title: "Tutorial: Integración de Azure Active Directory con Autotask Workplace | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Autotask al área de trabajo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a>Tutorial: Integración de Azure Active Directory con Autotask Workplace

En este tutorial, aprenderá cómo toointegrate Autotask al área de trabajo con Azure Active Directory (Azure AD).

Integración Autotask al área de trabajo con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooAutotask al área de trabajo
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAutotask al área de trabajo (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con un área de trabajo de Autotask tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Autotask Workplace
- Es necesario que sea administrador o superadministrador en Workplace.
- Debe tener una cuenta de administrador en hello Azure AD.
- los usuarios de Hola que vaya a usar esta característica deben tener cuentas dentro de un área de trabajo y hello Azure AD y deben coincidir con sus direcciones de correo electrónico para ambos.

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar un área de trabajo Autotask de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-autotask-workplace-from-hello-gallery"></a>Agregar un área de trabajo Autotask de galería de Hola
integración de hello tooconfigure Autotask área de trabajo en Azure AD, deberá tooadd Autotask al área de trabajo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Autotask al área de trabajo desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **al área de trabajo de Autotask**, seleccione **al área de trabajo de Autotask** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Lista de resultados de un área de trabajo Autotask Hola](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Autotask Workplace con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el área de trabajo de Autotask es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el área de trabajo de Autotask debe toobe establecido.

En lugar de trabajo Autotask, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Autotask al área de trabajo, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba al área de trabajo de Autotask](#create-an-autotask-workplace-test-user)**  -toohave un equivalente de Britta Simon en lugar de trabajo de Autotask es representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de área de trabajo de Autotask.

**inicio de sesión único en tooconfigure Azure AD con Autotask al área de trabajo, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **al área de trabajo de Autotask** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. Si desea que aplicación de hello tooconfigure en **IDP** inicia el modo, realizar Hola seguir pasos de hello **Autotask al área de trabajo dominio y las direcciones URL** sección:

    ![Información de dominio y direcciones URL de inicio de sesión único de Autotask Workplace para IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`

4. Si desea tooconfigure aplicación de hello en **SP** modo iniciado, comprobación de **mostrar avanzadas de configuración de la URL** y realizar Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Autotask Workplace para SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awp.autotask.net/loginsso`
     
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Póngase en contacto con [equipo de soporte técnico de cliente al área de trabajo de Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget estos valores. 

5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. En una ventana del explorador web diferente, inicio de sesión tooWorkplace Online mediante Hola credenciales de administrador.

    >[!Note]
    >Al configurar Hola IdP, un subdominio deberá toobe especificado. tooconfirm Hola correcto subdominio, tooWorkplace de inicio de sesión en línea. Una vez iniciada la sesión, asegúrese de subdominio de toohello nota en la dirección URL de Hola.
    >subdominio Hola forma parte de hello entre Hola "https://" y ".awp.autotask.net/" y debe ser nos, Europa, Canadá o Australia.

8. Vaya demasiado**configuración** > **Single Sign-On** y realizar Hola pasos:

    ![Configuración de inicio de sesión único de Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    a. Seleccione hello **archivo de metadatos XML** opción y, a continuación, cargar hello **Metadata XML** descargado del portal de Azure.

    b. Haga clic en **Enable SSO** (Habilitar SSO).
    
    ![Aprobación de configuración de inicio de sesión único de Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    c. Seleccione hello **puedo confirmar esta información es correcta y confianza este IdP** casilla de verificación.

    d. Haga clic en **Approve** (Aprobar).
     
>[!Note]
>Si necesita ayuda con la configuración de área de trabajo de Autotask, consulte la sección [esta página](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget asistencia con la cuenta de empresa.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.

### <a name="create-an-autotask-workplace-test-user"></a>Creación de un usuario de prueba de Autotask Workplace

En esta sección, creará un usuario llamado Britta Simon en Autotask. Trabaje con [equipo de soporte técnico al área de trabajo de Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) a los usuarios de tooadd Hola Hola plataforma Autotask al área de trabajo.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAutotask al área de trabajo.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooAutotask al área de trabajo, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **al área de trabajo de Autotask**.

    ![vínculo al área de trabajo de Autotask en la lista de aplicaciones de Hola Hola](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello al área de trabajo Autotask el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Autotask al área de trabajo.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

