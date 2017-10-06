---
title: "Tutorial: Integración de Azure Active Directory con RunMyProcess | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a>Tutorial: Integración de Azure Active Directory con RunMyProcess

En este tutorial, aprenderá cómo toointegrate RunMyProcess con Azure Active Directory (Azure AD).

Integración de RunMyProcess con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooRunMyProcess
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRunMyProcess (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con RunMyProcess tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en RunMyProcess

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar RunMyProcess desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-runmyprocess-from-hello-gallery"></a>Agregar RunMyProcess desde la Galería de Hola
integración de hello tooconfigure de RunMyProcess en Azure AD, deberá tooadd RunMyProcess de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd RunMyProcess de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **RunMyProcess**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. En el panel de resultados de hello, seleccione **RunMyProcess**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con RunMyProcess con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en RunMyProcess es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en RunMyProcess debe toobe establecido.

En RunMyProcess, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con RunMyProcess, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave un equivalente de Britta Simon en RunMyProcess que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de RunMyProcess.

**inicio de sesión único en Azure AD tooconfigure con RunMyProcess, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **RunMyProcess** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. En hello **RunMyProcess dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://live.runmyprocess.com/live/<tenant id>`

    > [!NOTE] 
    > valor de Hello no es real. Valor de Hola de actualización con Hola dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de RunMyProcess cliente](mailto:support@runmyprocess.com) valor de hello tooget. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. En hello **configuración de RunMyProcess** sección, haga clic en **configurar RunMyProcess** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. En una ventana del explorador web diferente, inquilino de RunMyProcess tooyour de inicio de sesión como administrador.

8. En el panel de navegación izquierdo, haga clic en **Account** (Cuenta) y seleccione **Configuration** (Configuración).
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. Vaya demasiado**método de autenticación** sección y realice los pasos siguientes:
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    a. En **Método**, seleccione **SSO con Samlv2**. 

    b. Hola **redireccionamiento SSO** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.

    c. Hola **redireccionamiento de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.

    d. Hola **formato de Id. de nombre** cuadro de texto, valor de tipo hello de **formato de nombre de identificador** como **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.

    e. Copiar el contenido de Hola Hola descargado del archivo de certificado y, a continuación, péguelo en hello **certificado** cuadro de texto. 
 
    f. Haga clic en el icono **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-runmyprocess-test-user"></a>Creación de un usuario de prueba de RunMyProcess

En orden tooenable toolog de los usuarios de Azure AD en tooRunMyProcess, se les deben aprovisionar en RunMyProcess. En caso de hello de RunMyProcess, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour sitio de empresa de RunMyProcess como administrador.

2. Haga clic en **Account** (Cuenta) y seleccione **Users** (Usuarios) en el panel de navegación izquierdo y, a continuación, haga clic en **New User** (Usuario nuevo).
   
    ![Nuevo usuario](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Nuevo usuario")

3. Hola **configuración de usuario** sección, lleve a cabo Hola pasos:
   
    ![Perfil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Perfil") 
  
    a. Hola de tipo **nombre** y **correo electrónico** de un Azure válida cuadros de texto relacionados con la cuenta de AD que quiera tooprovision en Hola. 

    b. Seleccione un **lenguaje IDE**, un **lenguaje** y un **perfil**. 

    c. Seleccione **toome de correo electrónico de creación de cuenta de envío**. 

    d. Haga clic en **Guardar**.
   
    >[!NOTE]
    >Puede usar cualquier otra RunMyProcess usuario cuenta herramienta de creación o las API proporcionadas por RunMyProcess tooprovision Azure Active Directory las cuentas de usuario. 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRunMyProcess.

![Asignar usuario][200] 

**tooassign Britta Simon tooRunMyProcess, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **RunMyProcess**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.

Al hacer clic en hello RunMyProcess disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour RunMyProcess aplicación.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

