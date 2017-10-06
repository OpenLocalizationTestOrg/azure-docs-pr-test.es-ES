---
title: "Tutorial: Integración de Azure Active Directory con Adobe Creative Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Adobe creativa en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Tutorial: Integración de Azure Active Directory con Adobe Creative Cloud

En este tutorial, aprenderá cómo toointegrate Adobe Creative en la nube con Azure Active Directory (Azure AD).

Integración de Adobe creativa en la nube con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooAdobe creativa en la nube
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAdobe creativa en la nube (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Adobe creativa en la nube, debe Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Adobe Creative Cloud

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Adobe creativa en la nube desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Agregar Adobe creativa en la nube desde la Galería de Hola
integración de hello tooconfigure de Adobe creativa en la nube en Azure AD, deberá tooadd Adobe creativa en la nube de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Adobe creativa en la nube de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Adobe Creative nube**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. En el panel de resultados de hello, seleccione **Adobe Creative nube**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Adobe Creative Cloud utilizando usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Adobe creativa en la nube es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Adobe creativa en la nube debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Adobe creativa en la nube.

tooconfigure y prueba de inicio de sesión único en Azure AD con Adobe creativa en la nube, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Creación de un usuario de prueba en la nube Adobe Creative](#creating-an-adobe-creative-cloud-test-user)**  -toohave un equivalente de Britta Simon en Adobe creativa en la nube que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Adobe creativa en la nube.

**tooconfigure inicio de sesión único en Azure AD con Adobe creativa en la nube, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **Adobe Creative nube** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. En hello **Adobe Creative nube dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. Hola **identificador** cuadro de texto, valor de tipo hello como:`https://www.okta.com/saml2/service-provider/<token>`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tener tooupdate estos valores con hello URL de identificador y la respuesta real. Aquí le sugerimos toouse Hola único valor de cadena en hello identificador. Si necesita un usuario toocreate manualmente, debe equipo de soporte técnico de toocontact hello Adobe creativa en la nube.

4. En hello **Adobe Creative nube dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **SP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Haga clic en hello **mostrar avanzadas de configuración de direcciones URL** opción

    b. Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://adobe.com`

5. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. En hello **configuración de nube de Adobe Creative** sección, haga clic en **configurar Adobe creativa en la nube** tooopen **configurar inicio de sesión** ventana. Copie hello **Id. de entidad SAML** y **dirección URL del servicio de SSO de SAML** desde la sección de referencia rápida.

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. En una ventana del explorador web diferente, inquilinos de nube creativa de Adobe tooyour inicio de sesión como administrador.

8.  Vaya demasiado**identidad** Hola panel de navegación izquierdo y haga clic en el dominio. A continuación, realizar Hola seguir pasos de **inicio de sesión único en requiere una configuración** sección.

    ![Configuración](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Configuración")

9. Haga clic en **examinar** hello tooupload descarga certificado de Azure AD demasiado**certificado IDP**.

10. Hola **emisor IDP** cuadro de texto, coloque valor Hola de **Id. de entidad SAML** que copió de **configurar inicio de sesión** sección en el portal de Azure.

11. Hola **dirección URL de inicio de sesión IDP** cuadro de texto, coloque valor Hola de **dirección URL del servicio de SSO de SAML** que copió de **configurar inicio de sesión** sección en el portal de Azure.

12. Seleccione **HTTP - Redirect** (HTTP - Redireccionamiento) como **IDP Binding** (Enlace IDP).

13. Seleccione **Email Address** (Dirección de correo electrónico) como **User Login Setting** (Configuración de inicio de sesión de usuario).
 
14. Haga clic en el botón **Guardar** .

15. panel de Hello presentará ahora Hola XML **"Descargar los metadatos"** archivo. Contiene la URL de EntityDescriptor y la URL de AssertionConsumerService de Adobe. Por favor, abra el archivo hello y configurarlos en hello aplicación de Azure AD.

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Hola uso EntityDescriptor valor Adobe proporcionado para **identificador** en hello **configurar opciones de aplicación** cuadro de diálogo.

    b. Hola de uso AssertionConsumerService valor Adobe proporcionado para **dirección URL de respuesta** en hello **configurar opciones de aplicación** cuadro de diálogo.
 
### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Creación de un usuario de prueba de Adobe Creative Cloud

En orden tooenable toolog de los usuarios de Azure AD en Adobe creativa en la nube, se les deben aprovisionar en Adobe creativa en la nube.  
En caso de hello de Adobe creativa en la nube, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour sitio de la compañía de Adobe creativa en la nube como administrador.

2. Haga clic en **Contactos**.

    ![Personas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Personas")

3. Haga clic en **Invitar a usuario**.

    ![Invitación de usuarios](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invitación de usuarios")

4. En hello **invitar personas** cuadro de diálogo, siga los pasos de hello:

    ![Invitar a personas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invitar a personas")

    a. Hola **correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.
    
    b. Haga clic en **Invitar**.

    > [!NOTE]
    > titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooAdobe acceso creativa en la nube.

![Asignar usuario][200] 

**tooassign Britta Simon tooAdobe creativa en la nube, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Adobe Creative nube**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Adobe creativa en la nube de Hola Hola Panel de acceso, deberá obtener la aplicación en la nube creativa de Adobe tooyour automáticamente ha iniciado sesión.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png