---
title: "Tutorial: integración de Azure Active Directory con Jitbit Helpdesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>Tutorial: Integración de Azure Active Directory con Jitbit Helpdesk

En este tutorial, aprenderá cómo toointegrate Jitbit Helpdesk con Azure Active Directory (Azure AD).

Integración Jitbit Helpdesk con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooJitbit departamento de soporte técnico
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJitbit departamento de soporte técnico (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Jitbit Helpdesk, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Jitbit Helpdesk

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Jitbit Helpdesk desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a>Agregar Jitbit Helpdesk desde la Galería de Hola
integración de hello tooconfigure de Jitbit Helpdesk en Azure AD, deberá tooadd Jitbit Helpdesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Jitbit Helpdesk de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Jitbit Helpdesk**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. En el panel de resultados de hello, seleccione **Jitbit Helpdesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jitbit Helpdesk con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Jitbit Helpdesk es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Jitbit Helpdesk debe toobe establecido.

En Jitbit Helpdesk, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Jitbit Helpdesk, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user) ** -toohave un equivalente de Britta Simon en Jitbit Helpdesk que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Jitbit Helpdesk.

**inicio de sesión único en tooconfigure Azure AD con Jitbit Helpdesk, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Jitbit Helpdesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. En hello **Jitbit Helpdesk dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de Jitbit Helpdesk cliente](https://www.jitbit.com/support/) tooget este valor. 
    
    b.  Hola **identificador** cuadro de texto, escriba una dirección URL como sigue:`https://www.jitbit.com/web-helpdesk/`

    
 


4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. En hello **Jitbit Helpdesk configuración** sección, haga clic en **configurar Jitbit Helpdesk** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Jitbit Helpdesk.

8. En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**.
   
    ![Administración](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administración")

9. Haga clic en **Configuración general**.
   
    ![Usuarios, compañías y permisos](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Usuarios, compañías y permisos")

10. Hola **configuración de autenticación** configuración sección, lleve a cabo Hola pasos:
   
    ![Configuración de la autenticación](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Configuración de la autenticación")
    
    a. Seleccione **habilitar SAML 2.0 único inicio de sesión**, toosign sesión utilizando Single Sign-On (SSO), con **OneLogin**.

    b. Hola **dirección URL del extremo** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.

    c. Abra su **base-64** codificado certificado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto

    d. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, nombre de tipo como **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a>Creación de un usuario de prueba de Jitbit Helpdesk

En orden tooenable toolog de los usuarios de Azure AD en Jitbit Helpdesk, se les deben aprovisionar en Jitbit Helpdesk.  En caso de hello de Jitbit Helpdesk, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **Jitbit Helpdesk** inquilino.

2. En el menú de hello en la parte superior de hello, haga clic en **administración**.
   
    ![Administración](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administración")

3. Haga clic en **Usuarios, compañías y permisos**.
   
    ![Usuarios, compañías y permisos](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Usuarios, compañías y permisos")

4. Haga clic en **Agregar usuario**.
   
    ![Agregar usuario](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Agregar usuario")
   
5. En la sección Crear hello, escriba datos Hola de cuenta de Azure AD Hola que desea tooprovision como se indica a continuación:

    ![Crear](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Crear")
   
   a. Hola **nombre de usuario** cuadro de texto, tipo **BrittaSimon**, nombre de usuario de hello en hello portal de Azure.

   b. Hola **correo electrónico** cuadro de texto, como tipo de correo electrónico del usuario de hello ** BrittaSimon@contoso.com **.

   c. Hola **nombre** cuadro de texto Nombre de usuario de hello como tipo **Bárbara**.

   d. Hola **Last Name** cuadro de texto, escriba Apellidos del usuario de hello como **Simon**.
   
   e. Haga clic en **Crear**.

>[!NOTE]
>Puede usar cualquier otra Jitbit Helpdesk usuario cuenta herramienta de creación o las API proporcionadas por Jitbit Helpdesk tooprovision cuentas de usuario de Azure AD.
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJitbit departamento de soporte técnico.

![Asignar usuario][200] 

**tooassign Britta Simon tooJitbit departamento de soporte técnico, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Jitbit Helpdesk**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Jitbit Helpdesk disponer en mosaico en el Panel de acceso de hello, deberá obtener la página de inicio de sesión de aplicación de Jitbit Helpdesk.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

