---
title: "Tutorial: Integración de Azure Active Directory con Rightscale | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Tutorial: Integración de Azure Active Directory con Rightscale

En este tutorial, aprenderá cómo toointegrate Rightscale con Azure Active Directory (Azure AD).

Integración Rightscale con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooRightscale
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRightscale (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Rightscale tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Rightscale

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Rightscale desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-rightscale-from-hello-gallery"></a>Agregar Rightscale desde la Galería de Hola
integración de hello tooconfigure de Rightscale en Azure AD, deberá tooadd Rightscale de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Rightscale de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Rightscale**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. En el panel de resultados de hello, seleccione **Rightscale**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Rightscale con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Rightscale es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Rightscale debe toobe establecido.

En Rightscale, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Rightscale, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Rightscale](#creating-a-rightscale-test-user)**  -toohave un equivalente de Britta Simon en Rightscale que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Rightscale.

**inicio de sesión único en Azure AD tooconfigure con Rightscale, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Rightscale** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. En hello **Rightscale dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP** no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. En hello **Rightscale dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Haga clic en hello **mostrar avanzadas de configuración de la URL**.

    b. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://login.rightscale.com/`

5. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. En hello **Rightscale configuración** sección, haga clic en **configurar Rightscale** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración del inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. tooget configurado para la aplicación de SSO, debe a toosign en tooyour RightScale inquilino como administrador.

    a. En el menú de hello en la parte superior de hello, haga clic en hello **configuración** pestaña y seleccione **Single Sign-On**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Haga clic en hello "**nueva**" botón tooadd **los proveedores de identidad SAML**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. En el cuadro de texto hello de **nombre para mostrar**, el nombre de la compañía de entrada.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Seleccione **SSO iniciado por el RightScale permite usar una sugerencia de detección** y entrada su **nombre de dominio** Hola por debajo del cuadro de texto.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Pegue el valor de Hola de **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure en **punto de conexión de SSO de SAML** en RightScale.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Pegue el valor de Hola de **Id. de entidad SAML** que haya copiado desde el portal de Azure en **SAML EntityID** en RightScale.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Haga clic en **explorador** certificado de hello tooupload de botón que descargó desde el portal de Azure.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Haga clic en **Guardar**.
<CE>
> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-rightscale-test-user"></a>Creación de un usuario de prueba de Rightscale

En esta sección, creará un usuario denominado Britta Simon en RightScale. Trabajar con [equipo de soporte técnico de Rightscale cliente](mailto:support@rightscale.com) a los usuarios de tooadd hello en la plataforma de RightScale Hola.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRightscale.

![Asignar usuario][200] 

**tooassign Britta Simon tooRightscale, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Rightscale**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.  

Al hacer clic en icono de RightScale Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour RightScale aplicación.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

