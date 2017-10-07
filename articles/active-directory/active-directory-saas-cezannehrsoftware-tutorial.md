---
title: "Tutorial: integración de Azure Active Directory con el software Cezanne HR | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el software de recursos humanos Cezanne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Tutorial: Integración de Azure Active Directory con el software Cezanne HR

En este tutorial, aprenderá cómo toointegrate software de recursos humanos Cezanne con Azure Active Directory (Azure AD).

La integración del software de recursos humanos Cezanne con Azure AD proporciona Hola siguientes ventajas. Puede:

- Controlar en Azure AD que tenga acceso tooCezanne el software de recursos humanos.
- Habilitar el inicio de sesión de los usuarios tooautomatically en software de recursos humanos tooCezanne con inicio de sesión único (SSO) con sus cuentas de Azure AD.
- Administrar las cuentas en una ubicación central: Hola portal de Azure.

toolearn más información acerca del software como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y SSO con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con el software de recursos humanos Cezanne tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en el software Cezanne HR

> [!NOTE]
> pasos de hello tootest en este tutorial, se recomienda que no use un entorno de producción.

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba. 

escenario de Hello descrito en este tutorial consta de dos bloques principales:

* Agregar software de recursos humanos Cezanne desde galería Hola
* Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Agregar software de recursos humanos Cezanne de galería de Hola
integración de hello tooconfigure del software de recursos humanos Cezanne en Azure AD, agregar software de recursos humanos Cezanne de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

tooadd software de recursos humanos Cezanne desde la Galería de hello, Hola siguientes:

1. Hola  **[portal de Azure](https://portal.azure.com)**, en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón. 

    ![botón de "Azure Active Directory" Hello][1]

2. Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.

    ![vínculo de Hello "Todas las aplicaciones"][2]
    
3. una nueva aplicación, en parte superior de Hola de hello tooadd **todas las aplicaciones** cuadro de diálogo, seleccione **nueva aplicación**.

    ![Hola "Nueva aplicación" botón][3]

4. En el cuadro de búsqueda de hello, escriba **Cezanne HR Software**.

    ![cuadro de búsqueda de Hola](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. En la lista de resultados de hello, seleccione **Software de recursos humanos Cezanne** y, a continuación, seleccione hello **agregar** botón aplicación hello de tooadd.

    ![lista de resultados de Hola](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con el software Cezanne HR con un usuario de prueba llamado "Britta Simon".

Para toowork SSO, Azure AD necesita usuario de Azure AD toohello de tooknow hello Cezanne HR software equivalente. En otras palabras, debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado Hola Hola software Cezanne HR.

relación de vínculo de tooestablish hello, asignar Hola software de recursos humanos Cezanne **nombre de usuario** valor como hello Azure AD **nombre de usuario** valor.

tooconfigure y SSO de Azure AD mediante software de recursos humanos Cezanne, Hola completa después de bloques de creación de la prueba.

### <a name="configure-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, puede habilitar SSO de Azure AD en hello portal de Azure y configurar SSO en la aplicación de software de recursos humanos Cezanne haciendo Hola siguiente:

1. En el portal de Azure, en Hola Hola **Software de recursos humanos Cezanne** página de integración de aplicaciones, seleccione **inicio de sesión único**.

    ![Hola "Inicio de sesión único" comando][4]

2. tooenable SSO, Hola **inicio de sesión único** cuadro de diálogo, seleccione hello **modo** como **sesión basado en SAML**.
 
    ![cuadro de "Modo de" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. En **Cezanne HR Software dominio y las direcciones URL**, Hola siguientes:

    ![Hola "Cezanne HR Software dominio y las direcciones URL" sección](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. Hola **dirección URL de respuesta** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Hello valores anteriores no son reales. Actualizarlas con la dirección URL de respuesta real de Hola y dirección URL de inicio de sesión de Hola. valores de hello tooobtain, Hola contacto [equipo de soporte técnico de recursos humanos Cezanne software cliente](mailto:info@cezannehr.com).

4. En **el certificado de firma de SAML**, seleccione **certificado (Base64)**y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Hola sección "Certificado de firma de SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Seleccione **Guardar**.

    ![botón de "Guardar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. En **configuración de Software de recursos humanos Cezanne**, seleccione **configurar Software de recursos humanos Cezanne** tooopen hello **configurar inicio de sesión** ventana. Hola copia **Id. de entidad SAML** y **SAML Single Sign-On Service** dirección URL de hello **referencia rápida** sección.

    ![sección "Configuración de Software de recursos humanos Cezanne" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en el inquilino de software de recursos humanos Cezanne tooyour como administrador.

8. En el panel izquierdo de hello, seleccione **el programa de instalación de sistema**. Seleccione **Configuración de seguridad** > **Configuración de inicio de sesión único**.

    ![vínculo de "Single Sign-On configuración" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. Hola **permitir que los usuarios toolog en uso Hola después de servicios de inicio de sesión único (SSO)** panel, seleccione hello **SAML 2.0** casilla de verificación y seleccione hello **configuración avanzada** opción.

    ![Opciones de inicio de sesión único](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Seleccione **Agregar nuevo**.

    ![botón "Agregar nuevo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. En **proveedores de identidad SAML 2.0**, Hola siguientes:

    ![Hola sección "Proveedores de identidad SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. Hola **nombre para mostrar** cuadro, escriba el nombre de Hola de su proveedor de identidades.

    b. Hola **identificador de entidad** cuadro, pegue hello **Id. de entidad SAML** que copió de hello portal de Azure. 

    c. Hola **enlace SAML** cuadro de lista, seleccione **POST**.

    d. Hola **extremo de servicio de Token de seguridad** cuadro, pegue hello **SAML Single Sign-On Service** dirección URL que copió de hello portal de Azure. 
    
    e. Hola **nombre de atributo de Id. de usuario** cuadro, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. Hola tooupload descarga certificado de Azure AD, seleccione hello **cargar** botón.
    
    g. Seleccione **Aceptar**. 

12. Seleccione **Guardar**.

    ![botón de "Guardar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Como configurar la aplicación hello, puede leer una versión concisa de hello precede a instrucciones de hello [portal de Azure](https://portal.azure.com). Después de Agregar aplicación hello de hello **Active Directory** > **aplicaciones empresariales** sección, seleccione hello **inicio de sesión único** ficha. Hola acceso incrusta documentación de hello **configuración** sección. 

toolearn más información acerca de la característica de documentación de embedded hello, consulte [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, creará el usuario de prueba Britta Simon Hola portal de Azure.

![usuario de prueba de Hello Britta Simon][100]

toocreate un usuario de prueba en Azure AD, Hola siguientes:

1. Hola **portal de Azure**, en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón.

    ![botón de "Azure Active Directory" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, seleccionados **usuarios y grupos** > **todos los usuarios**.
    
    ![vínculo de Hello "Todos los usuarios"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Hola **todos los usuarios** abre el cuadro de diálogo.

3. Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.
 
    ![botón de "Agregar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. Hola **usuario** diálogo cuadro, Hola siguientes:
 
    ![cuadro de diálogo de "Usuario" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro, escriba el usuario Britta Simon **dirección de correo electrónico**.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, valor de hello tenga en cuenta que se generó en hello **contraseña** cuadro.

    d. Seleccione **Crear**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Creación de un usuario de prueba del software Cezanne HR

toosign de usuarios tooenable Azure AD en el software de tooCezanne recursos humanos, se les debe aprovisionar en recursos humanos Cezanne software. En caso de hello de recursos humanos Cezanne software, el aprovisionamiento es una tarea manual.

El aprovisionamiento de una cuenta de usuario haciendo Hola siguiente:

1.  Inicie sesión en tooyour Cezanne HR sitio de la compañía de software como administrador.

2.  En el panel izquierdo de hello, seleccione **el programa de instalación de sistema** > **administrar usuarios** > **Agregar nuevo usuario**.

    ![vínculo de "Agregar nuevo usuario" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nuevo usuario")

3.  En **detalles de la persona**, Hola siguientes:

    ![sección "Detalles de la persona" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nuevo usuario")
    
    a. Establezca **Usuario interno** en **DESACTIVADO**.
    
    b. Hola **nombre** cuadro, tipo hello nombre del usuario, por ejemplo, **Bárbara**.  
 
    c. Hola **Last Name** cuadro, tipo hello apellidos del usuario, por ejemplo, **Simon**.
    
    d. Hola **correo electrónico** , escriba la dirección de correo electrónico del usuario de hello, por ejemplo, Brittasimon@contoso.com.

4.  En **información de la cuenta**, Hola siguientes:

    ![sección "Información de cuenta" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nuevo usuario")
    
    a. Hola **nombre de usuario** , escriba la dirección de correo electrónico del usuario de hello, por ejemplo, Brittasimon@contoso.com.
    
    b. Hola **contraseña** , escriba la contraseña del usuario de Hola.
    
    c. Hola **rol de seguridad** cuadro, seleccione **Professional de recursos humanos**.
    
    d. Seleccione **Aceptar**.

5. En hello **inicio de sesión único** ficha Hola **SAML 2.0 identificadores** sección, seleccione **Agregar nuevo**.

    ![botón "Agregar nuevo" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "usuario")

6. Hola **proveedor de identidades** cuadro de lista, seleccione el proveedor de identidad. Hola **identificador de usuario** cuadro, escriba la dirección de correo electrónico de hello para la cuenta de prueba usuario Britta Simon.

    ![Hola cuadros "Proveedor de identidades" y "Identificador de usuario"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "usuario")
    
7. Seleccione **Guardar**.

    ![botón de "Guardar" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "usuario")

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita el usuario de prueba Britta Simon toouse Azure SSO concediendo acceso tooCezanne HR software.

![Acceso de usuario de prueba][200] 

1. Hola portal de Azure, abrir vista de aplicaciones de hello y, a continuación, vaya toohello vista del directorio. Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.

    ![vínculo de Hello "Todas las aplicaciones"][201] 

2. En la lista de aplicaciones de hello, seleccione **Cezanne HR Software**.

    ![lista de "Aplicaciones" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. En el menú de Hola Hola izquierda, seleccione **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Seleccione **Agregar**. A continuación, en hello **Agregar asignación** cuadro de diálogo, seleccione **usuarios y grupos**.

    ![Vínculo "Usuarios y grupos"][203]

5. Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**.

6. Hola **usuarios y grupos** cuadro de diálogo, seleccione **seleccione**.

7. Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.
    
### <a name="test-sso"></a>Prueba de SSO

En esta sección, probará la configuración de SSO de Azure AD mediante el uso de hello Panel de acceso.

Cuando se selecciona el icono de software de recursos humanos Cezanne hello en Hola Panel de acceso, iniciar sesión en tooyour automáticamente aplicaciones de software de recursos humanos Cezanne.

## <a name="next-steps"></a>Pasos siguientes

* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el SSO con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

