---
title: "Tutorial: integración de Azure Active Directory con ZScaler ZSCloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>Tutorial: integración de Azure Active Directory con ZScaler ZSCloud

En este tutorial, aprenderá cómo toointegrate Zscaler ZSCloud con Azure Active Directory (Azure AD).

Integración de Zscaler ZSCloud con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooZscaler ZSCloud
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler ZSCloud (inicio de sesión único) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Zscaler ZSCloud tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en ZScaler ZSCloud

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Zscaler ZSCloud desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>Agregar Zscaler ZSCloud desde la Galería de Hola
integración de hello tooconfigure de Zscaler ZSCloud en Azure AD, deberá tooadd Zscaler ZSCloud de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Zscaler ZSCloud de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Zscaler ZSCloud**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. En el panel de resultados de hello, seleccione **Zscaler ZSCloud**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler ZSCloud con un usuario de prueba llamado Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Zscaler ZSCloud es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Zscaler ZSCloud debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Zscaler ZSCloud.

tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler ZSCloud, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Configuración de proxy](#configuring-proxy-settings)**  -configuración de proxy de hello tooconfigure en Internet Explorer
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave un equivalente de Britta Simon en Zscaler ZSCloud que está vinculado toohello Azure AD representación del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Zscaler ZSCloud.

**inicio de sesión único en tooconfigure Azure AD con Zscaler ZSCloud, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Zscaler ZSCloud** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. En hello **Zscaler ZSCloud dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por los usuarios en toosign tooyour aplicación de ZScaler ZSCloud.
    
    > [!NOTE] 
    > Tiene este valor con hello tooupdate dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de Zscaler ZSCloud cliente](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget este valor. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. En hello **configuración de Zscaler ZSCloud** sección, haga clic en **configurar Zscaler ZSCloud** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en tooyour sitio de empresa de ZScaler ZSCloud como administrador.

8. En el menú de hello en la parte superior de hello, haga clic en **administración**.
   
    ![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administración")

9. En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.   
            
    ![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Administración de usuarios y autenticación")

10. Hola **elegir opciones de autenticación para su organización** sección, lleve a cabo Hola pasos:   
                
    ![Autenticación](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticación")
   
    a. Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).

    b. Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).

11. En hello **configurar SAML Single Sign-On parámetros** página del cuadro de diálogo, realizar pasos de hello y, a continuación, haga clic en **realiza**

    ![Inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Inicio de sesión único")
    
    a. Hola pegar **SAML Single Sign-On dirección URL del servicio** valor en hello **dirección URL de los usuarios de toowhich del Portal de SAML de Hola se envía para autenticación** cuadro de texto.
    
    b. Hola **atributo que contiene el nombre de inicio de sesión** cuadro de texto, tipo **NameID**.
    
    c. tooupload el certificado descargado, haga clic en **Zscaler pem**.
    
    d. Seleccione **Habilitar aprovisionamiento automático de SAML**.

12. En hello **configurar la autenticación de usuario** cuadro de diálogo, siga los pasos de hello:

    ![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administración")
    
    a. Haga clic en **Guardar**.

    b. Haga clic en **Activar ahora**.

## <a name="configuring-proxy-settings"></a>Configuración de los valores de proxy
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>configuración de proxy de hello tooconfigure en Internet Explorer

1. Inicie **Internet Explorer**.

2. Seleccione **opciones de Internet** de hello **herramientas** menú Abrir hello **opciones de Internet** cuadro de diálogo.   
    
     ![Opciones de Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opciones de Internet")

3. Haga clic en hello **conexiones** ficha.   
  
     ![Conexiones](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Conexiones")

4. Haga clic en **configuración de LAN** tooopen hello **configuración de LAN** cuadro de diálogo.

5. En la sección servidor Proxy hello, realizar Hola pasos:   
   
    ![Servidor proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Servidor proxy")

    a. Seleccione **Usar un servidor proxy para la LAN**.

    b. En el cuadro de texto de dirección de hello, escriba **gateway.zscalerone.net**.

    c. En el cuadro de texto de puerto de hello, escriba **80**.

    d. Seleccione **No usar servidor proxy para direcciones locales**.

    e. Haga clic en **Aceptar** tooclose hello **configuración de red de área Local (LAN)** cuadro de diálogo.

6. Haga clic en **Aceptar** tooclose hello **opciones de Internet** cuadro de diálogo.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.

### <a name="creating-a-zscaler-zscloud-test-user"></a>Creación de un usuario de prueba de ZScaler ZSCloud

toolog de los usuarios de Azure AD tooenable en tooZScaler ZSCloud, deben ser aprovisionado tooZScaler ZSCloud.  
En caso de hello de ZScaler ZSCloud, el aprovisionamiento es una tarea manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamiento de usuario, realizar Hola pasos:

1. Inicie sesión en tooyour **Zscaler** inquilino.

2. Haga clic en **Administración**.   
   
    ![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administración")

3. Haga clic en **User Management**(Administración de usuarios).   
        
     ![Agregar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Agregar")

4. Hola **usuarios** , haga clic en **agregar**.
      
    ![Agregar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Agregar")

5. En la sección Agregar usuario hello, realizar Hola pasos:
        
    ![Agregar usuario](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Agregar usuario")
   
    a. Hola de tipo **UserID**, **usuario DisplayName**, **contraseña**, **Confirmar contraseña**y, a continuación, seleccione **grupos**hello y **departamento** de una cuenta válida de AAD que desee tooprovision.

    b. Haga clic en **Guardar**.

> [!NOTE]
> Puede usar cualquier otra ZScaler ZSCloud usuario cuenta herramienta de creación o las API proporcionadas por ZScaler ZSCloud tooprovision cuentas de usuario AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooZscaler ZSCloud.

![Asignar usuario][200] 

**tooassign tooZscaler Britta Simon ZSCloud, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Zscaler ZSCloud**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.

Al hacer clic en hello Zscaler ZSCloud disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación de Zscaler ZSCloud.

Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

