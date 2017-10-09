---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO para Bitbucket | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kantega SSO para Bitbucket."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: e86a9a9a42f2f80fe83191f113f6bab46cc8a37d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a>Tutorial: Integración de Azure Active Directory con Kantega SSO para Bitbucket

En este tutorial, aprenderá cómo toointegrate Kantega SSO para Bitbucket con Azure Active Directory (Azure AD).

Integración Kantega SSO para Bitbucket con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooKantega SSO para Bitbucket
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKantega SSO para Bitbucket (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Kantega SSO para Bitbucket, necesitará Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único de Kantega SSO para Bitbucket

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Kantega SSO para Bitbucket desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-kantega-sso-for-bitbucket-from-hello-gallery"></a>Agregar Kantega SSO para Bitbucket desde la Galería de Hola
integración de hello tooconfigure de Kantega SSO para Bitbucket en Azure AD, necesitará tooadd Kantega SSO para Bitbucket de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Kantega SSO para Bitbucket desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Kantega SSO para Bitbucket**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. En el panel de resultados de hello, seleccione **Kantega SSO para Bitbucket**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO para Bitbucket con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kantega SSO para Bitbucket es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kantega SSO para Bitbucket debe toobe establecido.

En Kantega SSO para Bitbucket, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Kantega SSO para Bitbucket, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un SSO Kantega de usuario de prueba de Bitbucket](#creating-a-kantega-sso-for-bitbucket-test-user)**  -toohave un equivalente de Britta Simon en Kantega SSO para Bitbucket que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO Kantega para aplicación de Bitbucket.

**tooconfigure inicio de sesión único en Azure AD con Kantega SSO para Bitbucket, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Kantega SSO para Bitbucket** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. En **IDP** inicia el modo, hello **Kantega SSO de dominio Bitbucket y direcciones URL** sección realizar Hola siguiendo el paso:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. En **SP** modo iniciado, verificación **mostrar avanzadas de configuración de la URL** y realizar Hola siguiendo el paso:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Estos valores se reciben durante la configuración de Hola de Bitbucket complemento que se explica más adelante en el tutorial Hola.

5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. En una ventana del explorador web diferente, inicie sesión en el portal de administración de Bitbucket tooyour como administrador.

8. Haga clic en el icono de engranaje y haga clic en hello **buscar nuevos complementos**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. Búsqueda **Kantega SSO para Bitbucket SAML & Kerberos** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. se inicia la instalación del complemento Hola.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. Una vez completada la instalación de Hola. Haga clic en **Cerrar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. Haga clic en **Administrar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. Haga clic en **configurar** tooconfigure Hola nuevo complemento.  

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. Hola **SAML** sección. Seleccione **Azure Active Directory (Azure AD)** de hello **Agregar proveedor de identidades** lista desplegable.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. Seleccione el nivel de suscripción **Básica**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. En hello **propiedades de la aplicación** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    a. Hola copia **App ID URI** valor y utilizarlo como **identificador, dirección URL de respuesta y dirección URL de inicio de sesión** en hello **Kantega SSO de dominio Bitbucket y direcciones URL** sección en el portal de Azure.

    b. Haga clic en **Siguiente**.

17. En hello **importación de metadatos** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    a. Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.

    b. Haga clic en **Siguiente**.

18. En hello **nombre y SSO ubicación** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    a. Agregar nombre de proveedor de identidades de hello en **el nombre del proveedor de identidad** cuadro de texto (por ejemplo, Azure AD).

    b. Haga clic en **Siguiente**.

19. Comprobar el certificado de firma de Hola y haga clic en **siguiente**.    

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. En hello **cuentas de usuario de Bitbucket** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    a. Seleccione **crear usuarios en el directorio interno de Bitbucket si es necesario** y escriba nombre adecuado Hola del grupo de Hola para los usuarios (puede ser no varios. de grupos separados por coma).

    b. Haga clic en **Siguiente**.

21. Haga clic en **Finalizar**

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. En hello **conoce dominios para Azure AD** sección, realice los siguientes pasos:   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    a. Seleccione **conoce dominios** desde el panel izquierdo de Hola de página Hola.

    b. Escriba el nombre de dominio en hello **conoce dominios** cuadro de texto.

    c. Haga clic en **Guardar**.  

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a>Creación de un usuario de prueba de Kantega SSO para Bitbucket

toolog de los usuarios de Azure AD tooenable en tooBitbucket, se les deben aprovisionar en Bitbucket. En Kantega SSO para Bitbucket, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour Bitbucket sitio de su compañía como administrador.

2. Haga clic en el icono de configuración.

    ![Agregar empleado](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. En la sección de la pestaña **Administración**, haga clic en **Usuarios**.

    ![Agregar empleado](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. Haga clic en **Crear usuario**.

    ![Agregar empleado](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. En hello **Create User** cuadro de diálogo, siga los pasos de hello:

    ![Agregar empleado](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    a. Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.
    
    b. Hola **nombre completo** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.
    
    c. Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.

    d. Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.  

    e. Hola **Confirmar contraseña** cuadro de texto, volver a entrar Hola contraseña del usuario.

    f. Haga clic en **Crear usuario**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKantega SSO para Bitbucket.

![Asignar usuario][200] 

**tooassign Britta Simon tooKantega SSO para Bitbucket, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Kantega SSO para Bitbucket**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Kantega SSO para Bitbucket icono en el Panel de acceso de hello, obtendrá automáticamente ha iniciado sesión tooyour Kantega SSO para aplicaciones de Bitbucket.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

