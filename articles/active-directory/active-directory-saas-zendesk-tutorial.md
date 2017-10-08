---
title: "Tutorial: Integración de Azure Active Directory con Zendesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Tutorial: Integración de Azure Active Directory con Zendesk

En este tutorial, aprenderá cómo toointegrate Zendesk con Azure Active Directory (Azure AD).

Integración de Zendesk con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooZendesk
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZendesk (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Zendesk tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Zendesk


> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Zendesk desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-zendesk-from-hello-gallery"></a>Agregar Zendesk desde la Galería de Hola
integración de hello tooconfigure de Zendesk en Azure AD, deberá tooadd Zendesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Zendesk de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Zendesk**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. En el panel de resultados de hello, seleccione **Zendesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zendesk con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zendesk es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zendesk debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Zendesk.

tooconfigure y prueba de inicio de sesión único en Azure AD con Zendesk, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Zendesk](#creating-a-zendesk-test-user)**  -toohave un equivalente de Britta Simon en Zendesk que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zendesk.

**inicio de sesión único en tooconfigure Azure AD con Zendesk, realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **Zendesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. En hello **Zendesk dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<subdomain>.zendesk.com`

    b. Hola **identificador** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con la URL de inicio de sesión real de Hola y dirección URL de identificación. Póngase en contacto con [equipo de soporte técnico de Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget estos valores. 

4. Zendesk espera las aserciones de SAML de hello en un formato concreto. No hay ningún atributo SAML obligatorio, pero si lo desea puede agregar un atributo de **atributos de usuario** sección por hello siguiente pasos siguientes: 

     ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Haga clic en hello **ver y editar Hola otros atributos** casilla de verificación.
     
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Haga clic en hello **Agregar atributo** tooopen **Agregar atributo** cuadro de diálogo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. Hola **nombre** cuadro de texto, el nombre del atributo de tipo hello (por ejemplo **emailaddress**).
    
    d. De hello **valor** lista, el valor del atributo de hello seleccione (como **user.mail**).
    
    e. Haga clic en **Aceptar**.
 
    > [!NOTE] 
    > Usar atributos de tooadd de atributos de extensión que no están en Azure AD de forma predeterminada. Haga clic en [atributos de usuario que se pueden establecer en SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget Hola completa lista de SAML atributos que **Zendesk** acepta. 

5. En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. En hello **configuración de Zendesk** sección, haga clic en **configurar Zendesk** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zendesk como administrador.

8. Haga clic en **Administrador**.

9. En el panel de navegación izquierdo de hello, haga clic en **configuración**y, a continuación, haga clic en **seguridad**.

10. En hello **seguridad** , siga los pasos de hello: 
   
     ![Seguridad](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Seguridad")

    ![Inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Inicio de sesión único")

     a. Haga clic en hello **Admin & agentes** ficha.

     b. Seleccione **Single sign-on (SSO) and SAML** (Inicio de sesión único (SSO) y SAML) y, luego, seleccione **SAML**.

     c. En **dirección URL SSO SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure. 

     d. En **dirección URL de cierre de sesión remoto** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.
        
     e. En **huella digital de certificado** cuadro de texto, pegue hello **huella digital** el valor de certificado que haya copiado desde el portal de Azure.
     
     f. Haga clic en **Guardar**.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 

### <a name="creating-a-zendesk-test-user"></a>Creación de un usuario de prueba de Zendesk

toolog de los usuarios de Azure AD tooenable en **Zendesk**, se les deben aprovisionar en **Zendesk**.  
Según el rol de hello asignado en aplicaciones de hello, Hola su comportamiento esperado:

 1. Las cuentas de **usuario final** se aprovisionan automáticamente al iniciar sesión.
 2. **Agente** y **administración** las cuentas que necesitan toobe aprovisionado manualmente en **Zendesk** antes de iniciar sesión.
 
**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **Zendesk** inquilino.

2. Seleccione hello **lista de clientes** ficha.

3. Seleccione hello **usuario** ficha y haga clic en **agregar**.
   
    ![Agregar usuario](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Agregar usuario")
4. Escriba la dirección de correo electrónico de Hola de una cuenta de Azure AD existente que desee tooprovision y, a continuación, haga clic en **guardar**.
   
    ![Nuevo usuario](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nuevo usuario")

> [!NOTE]
> Puede usar cualquier otra Zendesk usuario cuenta herramienta de creación o las API proporcionadas por Zendesk tooprovision cuentas de usuario AAD.


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZendesk.

![Asignar usuario][200] 

**tooassign Britta Simon tooZendesk, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Zendesk**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Zendesk Hola Hola Panel de acceso, deberá obtener aplicaciones de Zendesk tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
