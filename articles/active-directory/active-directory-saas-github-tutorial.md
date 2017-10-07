---
title: "Tutorial: Integración de Azure Active Directory con GitHub | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Tutorial: Integración de Azure Active Directory con GitHub

En este tutorial, aprenderá cómo toointegrate GitHub con Azure Active Directory (Azure AD).

Integración de GitHub con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooGitHub
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooGitHub (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con GitHub tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en GitHub


> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de GitHub de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-github-from-hello-gallery"></a>Adición de GitHub de galería de Hola
integración de hello tooconfigure de GitHub en Azure AD, deberá tooadd GitHub de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd GitHub de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **GitHub.com**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. En el panel de resultados de hello, seleccione **GitHub**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con GitHub mediante un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en GitHub es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en GitHub debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en GitHub.

tooconfigure y prueba de inicio de sesión único en Azure AD con GitHub, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de GitHub](#creating-a-GitHub-test-user) ** -toohave un equivalente de Britta Simon en GitHub que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de GitHub.

**inicio de sesión único en Azure AD tooconfigure con GitHub, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **GitHub** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. En hello **GitHub dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://github.com/orgs/<entity-id>/sso`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tener tooupdate estos valores con hello Sign-on dirección URL real y el identificador. Aquí le sugerimos toouse Hola único valor de cadena en hello identificador. Vaya a tooGitHub administrador sección tooretrieve estos valores. 

4. En hello **atributos de usuario** sección, seleccione **identificador de usuario** como user.mail.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**. Luego haga clic en el botón **Guardar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. En hello **configuración de GitHub** sección, haga clic en **configurar GitHub** tooopen **configurar inicio de sesión** ventana.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. En otra ventana del navegador web, inicie sesión en el sitio de la organización de GitHub como administrador.

12. Navegue demasiado**configuración** y haga clic en **seguridad**

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Comprobar hello **Habilitar autenticación SAML** cuadro, revelar campos de hello el inicio de sesión único en la configuración. A continuación, utilice Hola único inicio de sesión valor tooupdate Hola único inicio de sesión en dirección URL en configuración de Azure AD.

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Configurar Hola siguientes campos:

    a. **Dirección URL de inicio de sesión**: escriba **el inicio de sesión único de SAML dirección URL del servicio** de hello **configurar GitHub** sección en Azure AD

    b. **Emisor**: escriba **Id. de entidad SAML** de hello **configurar GitHub** sección en Azure AD

    c. **Certificado público**: Hola abierto descarga certificado de Azure AD en un contenido de hello el Bloc de notas y copie incluidos "BEGIN CERTIFICATE" y "END CERTIFICATE"

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Haga clic en **configuración de SAML de prueba** tooconfirm que no hay errores de validación o errores durante el SSO.

    ![Settings](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Haga clic en **Guardar**

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 


### <a name="creating-a-github-test-user"></a>Creación de un usuario de prueba de GitHub

En orden tooenable toolog de los usuarios de Azure AD en GitHub, se les deben aprovisionar en GitHub.  
En caso de hello de GitHub, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour sitio de GitHub su compañía como administrador.

2. Haga clic en **Contactos**.

    ![Personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Personas")

3. Haga clic en **Invitar a miembros**.

    ![Invitación de usuarios](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invitación de usuarios")

4. En hello **invitar miembros** cuadro de diálogo, siga los pasos de hello:

    a. Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.

    ![Invitar a personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invitar a personas")
    
    b. Haga clic en **Enviar invitación**.

    ![Invitar a personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invitar a personas")

    > [!NOTE]
    > titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooGitHub de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooGitHub, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **GitHub.com**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    


### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de GitHub de Hola Hola Panel de acceso, deberá obtener tooyour iniciado sesión en aplicaciones de GitHub. Con su cuenta personal podrá iniciar la sesión como una cuenta de organización pero, a continuación, la necesidad toolog.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
