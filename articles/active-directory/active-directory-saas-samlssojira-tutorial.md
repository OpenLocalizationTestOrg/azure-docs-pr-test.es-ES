---
title: "Tutorial: Integración de Azure Active Directory con SAML SSO for Jira by resolution GmbH | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO de SAML para Jira mediante la resolución GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Tutorial: Integración de Azure Active Directory con SAML SSO for Jira by resolution GmbH

En este tutorial, aprenderá cómo toointegrate SSO de SAML para Jira mediante la resolución GmbH con Azure Active Directory (Azure AD).

Integración de SSO de SAML para Jira mediante la resolución GmbH con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSAML SSO para Jira mediante la resolución GmbH
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAML SSO para Jira mediante la resolución GmbH (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con SSO de SAML para Jira mediante la resolución GmbH tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único de SAML SSO for Jira by resolution GmbH

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de SSO de SAML para Jira resolución GmbH desde galería Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a>Adición de SSO de SAML para Jira resolución GmbH desde galería Hola
tooconfigure Hola integración de SSO de SAML para Jira mediante la resolución GmbH en Azure AD, necesitará tooadd SSO de SAML para Jira mediante la resolución GmbH de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SSO de SAML para Jira mediante la resolución GmbH de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **SSO de SAML para Jira mediante la resolución GmbH**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. En el panel de resultados de hello, seleccione **SSO de SAML para Jira mediante la resolución GmbH**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAML SSO for Jira by resolution GmbH con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario homólogo hello en SSO de SAML para Jira resolución GmbH es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado hello en SSO de SAML para Jira mediante la resolución GmbH debe toobe establecido.

En SSO de SAML para Jira mediante la resolución GmbH, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con SSO de SAML para Jira mediante la resolución GmbH, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un SSO de SAML para Jira por usuario de prueba de resolución GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave un equivalente de Britta Simon en SSO de SAML para Jira mediante la resolución GmbH que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO de SAML para Jira mediante la resolución de aplicación GmbH.

**tooconfigure inicio de sesión único en Azure AD con SSO de SAML para Jira mediante la resolución GmbH, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **SSO de SAML para Jira mediante la resolución GmbH** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. En hello **SSO de SAML para las direcciones URL y Jira mediante la resolución de dominio GmbH** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/samlsso`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/samlsso`

4. Active **Mostrar configuración avanzada de URL**. Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Póngase en contacto con [equipo de soporte técnico de SSO de SAML para Jira mediante la resolución de cliente GmbH](https://www.resolution.de/go/support) tooget estos valores. 

5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. En una ventana del explorador web diferente, inicie sesión en tooyour **SSO de SAML para Jira mediante el portal de administración de resolución GmbH** como administrador.

8. Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. Está página de acceso a tooAdministrator redirigida. Escriba hello **contraseña** y haga clic en **confirmar** botón.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. En la sección de la pestaña Complementos, haga clic en **Find new add-ons** (Buscar nuevos complementos). Búsqueda **SAML único inicio de sesión (SSO) para JIRA** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. se iniciará la instalación del complemento Hola. Haga clic en **Cerrar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. Haga clic en **Administrar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Haga clic en **configurar** tooconfigure Hola nuevo complemento.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. En **configuración del complemento SAML SingleSignOn** página, haga clic en **Agregar proveedor de identidad adicional** botón Configuración de hello tooconfigure de proveedor de identidades.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. Siga los pasos indicados en esta página:

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. Agregar **nombre** de hello proveedor de identidades (por ejemplo, Azure AD).
    
    b. Agregar **descripción** de hello proveedor de identidades (por ejemplo, Azure AD).

    c. Haga clic en **XML** y seleccione hello **metadatos** archivo, que ha descargado desde el portal de Azure.

    d. Haga clic en el botón **Cargar**.

    e. Lee los metadatos de IdP de Hola y rellena los campos de hello como se resalta en la captura de pantalla de Hola.   

16. Haga clic en **Guardar configuración** botón Configuración de hello toosave.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>Creación del usuario de prueba de SAML SSO for Jira by resolution GmbH

toolog de los usuarios de Azure AD tooenable en tooSAML SSO para Jira mediante la resolución GmbH, se les deben aprovisionar en SSO de SAML para Jira mediante la resolución GmbH.  
En SAML SSO for Jira by resolution GmbH, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour SSO de SAML para Jira por sitio de la compañía de resolución GmbH como administrador.

2. Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. Son tooenter de página de acceso redirigida tooAdministrator **contraseña** y haga clic en **confirmar** botón.

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. En la sección de la pestaña **Administración de usuarios**, haga clic en **Crear usuario**.

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. En hello **"Crear nuevo usuario"** cuadro de diálogo, siga los pasos de hello:

    ![Agregar empleado](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.

    b. Hola **nombre completo** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.

    c. Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.

    d. Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.

    e. Haga clic en **Crear usuario**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAML SSO para Jira mediante la resolución GmbH.

![Asignar usuario][200] 

**tooassign Britta Simon tooSAML SSO para Jira mediante la resolución GmbH, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **SSO de SAML para Jira mediante la resolución GmbH**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello SSO de SAML para Jira por mosaico GmbH de resolución en el Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour SSO de SAML para Jira mediante la resolución de aplicación GmbH.
Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

