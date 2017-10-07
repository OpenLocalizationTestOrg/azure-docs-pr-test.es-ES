---
title: "Tutorial: Integración de Azure Active Directory con xMatters OnDemand | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Tutorial: Integración de Azure Active Directory con xMatters OnDemand

En este tutorial, aprenderá cómo toointegrate xMatters OnDemand con Azure Active Directory (Azure AD).

Integración xMatters OnDemand con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooxMatters OnDemand
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooxMatters OnDemand (inicio de sesión único) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con xMatters OnDemand, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en xMatters OnDemand

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar xMatters OnDemand desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a>Agregar xMatters OnDemand desde la Galería de Hola
integración de hello tooconfigure de xMatters OnDemand en Azure AD, deberá tooadd xMatters OnDemand de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd xMatters OnDemand de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **xMatters OnDemand**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. En el panel de resultados de hello, seleccione **xMatters OnDemand**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con xMatters OnDemand con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué Hola usuario equivalente en xMatters OnDemand es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en xMatters OnDemand debe toobe establecido.

En xMatters OnDemand, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con xMatters OnDemand, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave un equivalente de Britta Simon en xMatters OnDemand que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en su xMatters OnDemand aplicación.

**inicio de sesión único en tooconfigure Azure AD con xMatters OnDemand, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **xMatters OnDemand** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. En hello **xMatters OnDemand dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde Hola archivo del certificado localmente como **c:\\XMatters OnDemand.cer**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > Necesita tooforward Hola certificado toohello [equipo de soporte técnico de xMatters OnDemand](https://www.xmatters.com/company/contact-us/). certificado de Hello debe toobe cargada por el equipo de soporte técnico de xMatters Hola antes de finalizar la configuración de inicio de sesión único de Hola. 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. En hello **xMatters OnDemand configuración** sección, haga clic en **configurar xMatters OnDemand** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en tooyour sitio de la compañía de XMatters OnDemand como administrador.

8. En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**y, a continuación, haga clic en **detalles de la compañía** en la barra de navegación de hello en el lado izquierdo de Hola.
   
    ![Administración](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Administración")

9. En hello **configuración de SAML** , siga los pasos de hello:
   
    ![Configuración de SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuración de SAML")
   
    a. Seleccione **Habilitar SAML**.
   
    b. Pegar **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure en hello **Id. de proveedor de identidad** cuadro de texto.
   
    c. Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **inicio de sesión único en URL** cuadro de texto.
   
    d. Pegar **dirección URL de cierre de sesión**, que haya copiado desde Hola portal de Azure en hello **dirección URL de cierre de sesión único** cuadro de texto.
   
    e. En la página de detalles de la compañía de hello, en la parte superior de hello, haga clic en **guardar cambios**.
    
    ![Detalles de la compañía](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Detalles de la compañía")

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-xmatters-ondemand-test-user"></a>Creación de un usuario de prueba de xMatters OnDemand

En orden tooenable toolog de los usuarios de Azure AD en tooXMatters OnDemand, les deben aprovisionar en XMatters OnDemand. En caso de hello de XMatters OnDemand, el aprovisionamiento es una tarea manual.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>tooprovision una cuenta de usuario, realizar Hola lo siguiente:
1. Inicie sesión en tooyour **XMatters OnDemand** inquilino.

2.  Haga clic en **usuarios** ficha y, a continuación, haga clic en **Agregar usuario**.
  
    ![Usuarios](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Usuarios")

3. Hola **agregar un usuario** sección, lleve a cabo Hola pasos:
   
    ![Agregar un usuario](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Agregar un usuario")

    a. Seleccione **Active**(Activo).

    b. Hola **Id. de usuario** cuadro de texto, Id. de usuario de tipo hello del usuario como Brittasimon@contoso.com.
   
    c. Hola **nombre** cuadro de texto Nombre de usuario de hello como Bárbara tipo.

    d. Hola **Last Name** cuadro de texto, escriba Apellidos del usuario de hello como Simon.
    
    e. Hola **sitio** cuadro de texto, sitio válido de hello entrar un Azure válida que desee tooprovision de cuenta de AD.
    
    f. Haga clic en **Guardar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooxMatters a petición.

![Asignar usuario][200] 

**tooassign Britta Simon tooxMatters OnDemand, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **xMatters OnDemand**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello xMatters OnDemand icono en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour xMatters OnDemand aplicación.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

