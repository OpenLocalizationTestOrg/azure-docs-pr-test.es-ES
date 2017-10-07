---
title: "Tutorial: integración de Azure Active Directory con Zscaler | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2894534f5d6711fd6af618cd699fa5837b5bf26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a>Tutorial: Integración de Azure Active Directory con Zscaler

En este tutorial, aprenderá cómo toointegrate Zscaler con Azure Active Directory (Azure AD).

Integración Zscaler con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooZscaler
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Zscaler tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Zscaler

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Zscaler desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-zscaler-from-hello-gallery"></a>Agregar Zscaler desde la Galería de Hola
integración de hello tooconfigure de Zscaler en Azure AD, deberá tooadd Zscaler de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Zscaler de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Zscaler**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. En el panel de resultados de hello, seleccione **Zscaler**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zscaler es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zscaler debe toobe establecido.

En Zscaler, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Configuración de proxy](#configuring-proxy-settings)**  -configuración de proxy de hello tooconfigure en Internet Explorer
3. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
4. **[Crear un usuario de prueba de Zscaler](#creating-a-zscaler-test-user)**  -toohave un equivalente de Britta Simon en Zscaler que es la representación toohello vinculado Azure AD del usuario.
5. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
6. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zscaler.

**inicio de sesión único en tooconfigure Azure AD con Zscaler, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Zscaler** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. En hello **Zscaler dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.zsclaer.net`

    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de Zscaler cliente](https://www.zscaler.com/company/contact) tooget este valor. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. En hello **configuración de Zscaler** sección, haga clic en **configurar Zscaler** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de ZScaler tooyour como administrador.

8. En el menú de hello en la parte superior de hello, haga clic en **administración**.
   
    ![Administración](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administración")

9. En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.   
            
    ![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Administración de usuarios y autenticación")

10. Hola **elegir opciones de autenticación para su organización** sección, lleve a cabo Hola pasos:   
                
    ![Autenticación](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Autenticación")
   
    a. Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).

    b. Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).

11. En hello **configurar SAML Single Sign-On parámetros** página del cuadro de diálogo, realizar pasos de hello y, a continuación, haga clic en **realiza**

    ![Inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Inicio de sesión único")
    
    a. Hola pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de los usuarios de toowhich del Portal de SAML de Hola se envía para autenticación** cuadro de texto.
    
    b. Hola **atributo que contiene el nombre de inicio de sesión** cuadro de texto, tipo **NameID**.
    
    c. tooupload el certificado descargado, haga clic en **Zscaler pem**.
    
    d. Seleccione **Habilitar aprovisionamiento automático de SAML**.

12. En hello **configurar la autenticación de usuario** cuadro de diálogo, siga los pasos de hello:

    ![Administración](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administración")
    
    a. Haga clic en **Guardar**.

    b. Haga clic en **Activar ahora**.

## <a name="configuring-proxy-settings"></a>Configuración de los valores de proxy
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>configuración de proxy de hello tooconfigure en Internet Explorer

1. Inicie **Internet Explorer**.

2. Seleccione **opciones de Internet** de hello **herramientas** menú Abrir hello **opciones de Internet** cuadro de diálogo.   
    
     ![Opciones de Internet](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Opciones de Internet")

3. Haga clic en hello **conexiones** ficha.   
  
     ![Conexiones](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Conexiones")

4. Haga clic en **configuración de LAN** tooopen hello **configuración de LAN** cuadro de diálogo.

5. En la sección servidor Proxy hello, realizar Hola pasos:   
   
    ![Servidor proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Servidor proxy")

    a. Seleccione **Usar un servidor proxy para la LAN**.

    b. En el cuadro de texto de dirección de hello, escriba **gateway.zscaler.net**.

    c. En el cuadro de texto de puerto de hello, escriba **80**.

    d. Seleccione **No usar servidor proxy para direcciones locales**.

    e. Haga clic en **Aceptar** tooclose hello **configuración de red de área Local (LAN)** cuadro de diálogo.

6. Haga clic en **Aceptar** tooclose hello **opciones de Internet** cuadro de diálogo.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-zscaler-test-user"></a>Creación de un usuario de prueba de Zscaler

toolog de los usuarios de Azure AD tooenable en tooZScaler, deben ser tooZScaler aprovisionado.  
En caso de hello de ZScaler, el aprovisionamiento es una tarea manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamiento de usuario, realizar Hola pasos:

1. Inicie sesión en tooyour **Zscaler** inquilino.

2. Haga clic en **Administración**.   
   
    ![Administración](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administración")

3. Haga clic en **User Management**(Administración de usuarios).   
        
     ![Agregar](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Agregar")

4. Hola **usuarios** , haga clic en **agregar**.
      
    ![Agregar](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Agregar")

5. En la sección Agregar usuario hello, realizar Hola pasos:
        
    ![Agregar usuario](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Agregar usuario")
   
    a. Hola de tipo **UserID**, **usuario DisplayName**, **contraseña**, **Confirmar contraseña**y, a continuación, seleccione **grupos**hello y **departamento** de una cuenta válida de AAD que desee tooprovision.

    b. Haga clic en **Guardar**.

> [!NOTE]
> Puede usar cualquier otra ZScaler usuario cuenta herramienta de creación o las API proporcionadas por ZScaler tooprovision cuentas de usuario AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZscaler.

![Asignar usuario][200] 

**tooassign Britta Simon tooZscaler, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Zscaler**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Zscaler Hola Hola Panel de acceso, deberá obtener la aplicación de Zscaler tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

