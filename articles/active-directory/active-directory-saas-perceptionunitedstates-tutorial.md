---
title: "Tutorial: Integración de Azure Active Directory con Perception United States (no UltiPro) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y percepción United States (no-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Tutorial: Integración de Azure Active Directory con Perception United States (no UltiPro)

En este tutorial, aprenderá cómo toointegrate spain percepción (no-UltiPro) con Azure Active Directory (Azure AD).

Integración percepción United States (no-UltiPro) con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooPerception Estados Unidos (no-UltiPro).
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPerception Estados Unidos (no-UltiPro) (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con percepción United States (no-UltiPro), necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Perception United States (no UltiPro)

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar percepción United States (no-UltiPro) desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Agregar percepción United States (no-UltiPro) desde la Galería de Hola
integración de hello tooconfigure de percepción United States (no-UltiPro) en Azure AD, deberá tooadd percepción United States (no-UltiPro) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd spain percepción (no-UltiPro) de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **percepción United States (no-UltiPro)**, seleccione **percepción United States (no-UltiPro)** desde el panel de resultados, a continuación, haga clic en **agregar** tooadd de botón aplicación Hello.

    ![Estados Unidos de percepción (no-UltiPro) en la lista de resultados de Hola](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Perception United States (no UltiPro) con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en percepción de Estados Unidos (no-UltiPro) es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en percepción de Estados Unidos (no-UltiPro) debe toobe establecido.

En la percepción de Estados Unidos (no-UltiPro), asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con percepción United States (no-UltiPro), deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de percepción United States (no-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave un equivalente de Britta Simon en percepción de Estados Unidos (no-UltiPro) que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de percepción United States (no-UltiPro).

**Azure AD tooconfigure inicio de sesión único con percepción United States (no-UltiPro), realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **percepción United States (no-UltiPro)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. En hello **dominio UnitedStates percepción (no-UltiPro) y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Perception United States (no UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://perception.kanjoya.com/sp`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > valor de Hello no es real. Se actualizará el valor de hello con URL de respuesta real hello, que se explica más adelante en el tutorial de Hola.
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. En hello **configuración percepción United States (no-UltiPro)** sección, haga clic en **configurar percepción United States (no-UltiPro)** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad SAML** de hello **sección de referencia rápida.**

    a. Hola **percepción United States (no-UltiPro)** aplicación requiere hello **Id. de entidad SAML** valor, que ha copiado, toobe uri codificado. valor de uri codificado de hello tooget, siguiente Hola de uso vincula:**http://www.url-encode-decode.com/**.

    b. Después de obtener el uri de hello codificado valor combinarla con hello **dirección URL de respuesta** según se indica a continuación:

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Hola pegar por encima del valor de hello **dirección URL de respuesta** en el cuadro de texto **dominio UnitedStates percepción (no-UltiPro) y las direcciones URL** sección.

    ![Configuración de Perception United States (no UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour percepción United States (no-UltiPro) como administrador.

8. En la barra de herramientas principal de hello, haga clic en **configuración de la cuenta**.

    ![Usuario de Perception United States (no UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. En hello **configuración de la cuenta** , siga los pasos de hello:

    ![Usuario de Perception United States (no UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. Hola **nombre de la compañía** cuadro de texto, nombre de tipo hello de hello **empresa**.
    
    b. Hola **nombre de la cuenta** cuadro de texto, nombre de tipo hello de hello **cuenta**.

    c. En **predeterminado respuesta-tooEmail** cuadro de texto, hello de tipo válida **correo electrónico**.

    d. Seleccione **SSO Identity Provider** (Proveedor de identidades de SSO) como **SAML 2.0**.

10. En hello **configuración de SSO** , siga los pasos de hello:

    ![Configuración de SSO de Perception United States (no UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Seleccione **SAML NameID Type** (Tipo de identificador de nombre de SAML) como **EMAIL** (correo electrónico).

    b. Hola **nombre de configuración de SSO** cuadro de texto Nombre del tipo hello de su **configuración**.
    
    c. En **el nombre del proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure. 

    d. En **cuadro de texto dominio SAML**, escriba el dominio de hello como  **@contoso.com** .

    e. Haga clic en **cargar nuevo** hello tooupload **Metadata XML** archivo.

    f. Haga clic en **Update**(Actualizar).


> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Creación de un usuario de prueba de Perception United States (no UltiPro)

En esta sección, creará un usuario llamado Britta Simon en Perception United States (no UltiPro). Trabajar con [equipo de soporte técnico de percepción United States (no-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd los usuarios de hello en la plataforma de hello percepción United States (no-UltiPro).

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPerception spain (no-UltiPro).

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooPerception spain (no-UltiPro), lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **percepción United States (no-UltiPro)**.

    ![vínculo de Hello percepción United States (no-UltiPro) en la lista de aplicaciones de Hola](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de percepción United States (no-UltiPro) Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación percepción United States (no-UltiPro).
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

