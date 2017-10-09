---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO para FishEye/Crucible | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kantega SSO para FishEye/placa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a>Tutorial: Integración de Azure Active Directory con Kantega SSO para FishEye/Crucible

En este tutorial, aprenderá cómo toointegrate Kantega SSO para FishEye/placa con Azure Active Directory (Azure AD).

Integración Kantega SSO para FishEye/placa con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooKantega SSO para FishEye/placa
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKantega SSO para FishEye/placa (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Kantega SSO para FishEye/placa tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único de Kantega SSO para FishEye/Crucible

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Kantega SSO para FishEye/placa de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a>Agregar Kantega SSO para FishEye/placa de galería de Hola
integración de hello tooconfigure de Kantega SSO para FishEye/placa en Azure AD, necesitará tooadd Kantega SSO para FishEye/placa de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Kantega SSO para FishEye/placa de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Kantega SSO para FishEye/placa**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. En el panel de resultados de hello, seleccione **Kantega SSO para FishEye/placa**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO para FishEye/Crucible con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kantega SSO para FishEye/placa es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kantega SSO para FishEye/placa debe toobe establecido.

En Kantega SSO para FishEye/placa, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Kantega SSO para FishEye/placa, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un SSO Kantega de usuario de prueba de FishEye/placa](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave un equivalente de Britta Simon en Kantega SSO para FishEye/placa es representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO Kantega para aplicaciones de FishEye/placa.

**tooconfigure inicio de sesión único en Azure AD con Kantega SSO para FishEye/placa, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Kantega SSO para FishEye/placa** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. En **IDP** inicia el modo, hello **Kantega SSO de dominio FishEye/placa y direcciones URL** sección realizar Hola siguiendo el paso:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. En **SP** modo iniciado, verificación **mostrar avanzadas de configuración de la URL** y realizar Hola siguiendo el paso:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Estos valores se reciben durante la configuración de Hola de complemento FishEye/placa que se explica más adelante en el tutorial Hola.

5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. En una ventana del explorador web diferente, inicie sesión en tooyour FishEye/placa en el servidor local como administrador.

8. Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. En la sección Configuración del sistema, haga clic en **Find new add-ons** (Buscar nuevos complementos). 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. Búsqueda **Kantega SSO para placa** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. se inicia la instalación del complemento Hola. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. Una vez completada la instalación de Hola. Haga clic en **Cerrar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. Haga clic en **Administrar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. Haga clic en **configurar** tooconfigure Hola nuevo complemento.  

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. Hola **SAML** sección. Seleccione **Azure Active Directory (Azure AD)** de hello **Agregar proveedor de identidades** lista desplegable.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. Seleccione el nivel de suscripción **Básica**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. En hello **propiedades de la aplicación** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    a. Hola copia **App ID URI** valor y utilizarlo como **identificador, dirección URL de respuesta y dirección URL de inicio de sesión** en hello **Kantega SSO de dominio FishEye/placa y direcciones URL** sección en el portal de Azure.

    b. Haga clic en **Siguiente**.

18. En hello **importación de metadatos** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    a. Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.

    b. Haga clic en **Siguiente**.

19. En hello **nombre y SSO ubicación** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    a. Agregar nombre de proveedor de identidades de hello en **el nombre del proveedor de identidad** cuadro de texto (por ejemplo, Azure AD).

    b. Haga clic en **Siguiente**.

20. Comprobar el certificado de firma de Hola y haga clic en **siguiente**.    

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. En hello **cuentas de usuario de ojo de pez** sección, realice los siguientes pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    a. Seleccione **crear usuarios en el directorio interno del FishEye si es necesario** y escriba nombre adecuado Hola del grupo de Hola para los usuarios (puede ser no varios. de grupos separados por coma).

    b. Haga clic en **Siguiente**.

22. Haga clic en **Finalizar**

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. En hello **conoce dominios para Azure AD** sección, realice los siguientes pasos:   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    a. Seleccione **conoce dominios** desde el panel izquierdo de Hola de página Hola.

    b. Escriba el nombre de dominio en hello **conoce dominios** cuadro de texto.

    c. Haga clic en **Guardar**.  

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a>Creación de un usuario de prueba de Kantega SSO para FishEye/Crucible

toolog de los usuarios de Azure AD tooenable en tooFishEye/placa, se les deben aprovisionar en FishEye/placa. En Kantega SSO para FishEye/Crucible, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour placa en el servidor local como administrador.

2. Mantenga el mouse sobre el icono de engranaje y haga clic en hello **usuarios**.

    ![Agregar empleado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. En la sección de la pestaña **Usuarios**, haga clic en **Agregar usuario**.

    ![Agregar empleado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. En hello **Agregar nuevo usuario** cuadro de diálogo, siga los pasos de hello:

    ![Agregar empleado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    a. Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.
    
    b. Hola **nombre para mostrar** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.
    
    c. Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.

    d. Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.  

    e. Hola **Confirmar contraseña** cuadro de texto, volver a entrar Hola contraseña del usuario.

    f. Haga clic en **Agregar**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKantega SSO para FishEye/placa.

![Asignar usuario][200] 

**tooassign Britta Simon tooKantega SSO para FishEye/placa, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Kantega SSO para FishEye/placa**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Kantega SSO de icono FishEye/placa Hola Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour Kantega SSO para aplicaciones de FishEye/placa.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

