---
title: "Tutorial: Integración de Azure Active Directory con Picturepark | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Tutorial: Integración de Azure Active Directory con Picturepark

En este tutorial, aprenderá cómo toointegrate Picturepark con Azure Active Directory (Azure AD).

Integración de Picturepark con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooPicturepark
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPicturepark (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Picturepark tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Picturepark

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Picturepark desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-picturepark-from-hello-gallery"></a>Agregar Picturepark desde la Galería de Hola
integración de hello tooconfigure de Picturepark en Azure AD, deberá tooadd Picturepark de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Picturepark de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Picturepark**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. En el panel de resultados de hello, seleccione **Picturepark**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Picturepark con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Picturepark es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Picturepark debe toobe establecido.

En Picturepark, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Picturepark, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Picturepark](#creating-a-picturepark-test-user) ** -toohave un equivalente de Britta Simon en Picturepark que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Picturepark.

**inicio de sesión único en Azure AD tooconfigure con Picturepark, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Picturepark** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. En hello **Picturepark dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.picturepark.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de Picturepark](https://picturepark.com/about/contact/) tooget estos valores. 
 
4. En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. En hello **configuración de Picturepark** sección, haga clic en **configurar Picturepark** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. En otra ventana del explorador web, inicie sesión en el sitio de la compañía Picturepark como administrador.

8. En la barra de herramientas de hello en la parte superior de hello, haga clic en **herramientas administrativas**y, a continuación, haga clic en **consola de administración**.
   
    ![Consola de administración](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Consola de administración")

9. Haga clic en **Autenticación** y en **Proveedores de identidades**.
   
    ![Autenticación](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticación")

10. Hola **configuración del proveedor de identidades** sección, lleve a cabo Hola pasos:
   
    ![Configuración del proveedor de identidades](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuración del proveedor de identidades")
   
    a. Haga clic en **Agregar**.
  
    b. Escriba un nombre para su configuración.
   
    c. Seleccione **Establecer como predeterminado**.
   
    d. En **URI de emisor** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.
   
    e. En **huella digital de emisor de confianza** cuadro de texto, pegue Hola valo **huella digital** que haya copiado desde **el certificado de firma de SAML** sección. 

11. Haga clic en **JoinDefaultUsersGroup**.

12. Hola tooset **Emailaddress** atributo Hola **notificación** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` y haga clic en **guardar**.

      ![Configuración](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuración")

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-picturepark-test-user"></a>Creación de un usuario de prueba de Picturepark

En orden tooenable toolog de los usuarios de Azure AD en Picturepark, se les deben aprovisionar en Picturepark. En caso de hello de Picturepark, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **Picturepark** inquilino.

2. En la barra de herramientas de hello en la parte superior de hello, haga clic en **herramientas administrativas**y, a continuación, haga clic en **usuarios**.
   
    ![Usuarios](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Usuarios")

3. Hola **información general de los usuarios** , haga clic en **nuevo**.
   
    ![Administración de usuarios](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Administración de usuarios")

4. En hello **Create User** cuadro de diálogo, realizar Hola siguiendo los pasos de un usuario válido de Azure Active Directory que desee tooprovision:
   
    ![Creación de usuarios](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Creación de usuarios")
   
    a. Hola **dirección de correo electrónico** cuadro de texto, hello tipo **dirección de correo electrónico** del usuario de hello ** BrittaSimon@contoso.com **.  
   
    b. Hola **contraseña** y **Confirmar contraseña** cuadros de texto, hello tipo **contraseña** de BrittaSimon. 
   
    c. Hola **nombre** cuadro de texto, hello tipo **nombre** del usuario de hello **Bárbara**. 
   
    d. Hola **Last Name** cuadro de texto, hello tipo **Last Name** del usuario de hello **Simon**.
   
    e. Hola **empresa** cuadro de texto, hello tipo **nombre de la compañía** del usuario de Hola. 
   
    f. Hola **país** cuadro de texto, seleccione hello **país** del usuario de Hola.
  
    g. Hola **código postal** cuadro de texto, hello tipo **código postal** de ciudad Hola.
   
    h. Hola **City** cuadro de texto, hello tipo **nombre de la ciudad** del usuario de Hola.

    i. Seleccione un valor en **Language**(Idioma).
   
    j. Haga clic en **Crear**.

>[!NOTE]
>Puede usar cualquier otra Picturepark usuario cuenta herramienta de creación o las API proporcionadas por Picturepark tooprovision cuentas de usuario de Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPicturepark.

![Asignar usuario][200] 

**tooassign Britta Simon tooPicturepark, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Picturepark**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Picturepark Hola Hola Panel de acceso, deberá obtener aplicaciones de Picturepark tooyour automáticamente ha iniciado sesión. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

