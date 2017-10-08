---
title: "Tutorial: Integración de Azure Active Directory con Sprinklr | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Tutorial: integración de Azure Active Directory con Sprinklr

En este tutorial, aprenderá cómo toointegrate Sprinklr con Azure Active Directory (Azure AD).

Integración Sprinklr con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSprinklr
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSprinklr (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Sprinklr tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Sprinklr

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Sprinklr desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sprinklr-from-hello-gallery"></a>Agregar Sprinklr desde la Galería de Hola
integración de hello tooconfigure de Sprinklr en Azure AD, deberá tooadd Sprinklr de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Sprinklr de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Sprinklr**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. En el panel de resultados de hello, seleccione **Sprinklr**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sprinklr con un usuario de prueba llamado Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Sprinklr es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Sprinklr debe toobe establecido.

En Sprinklr, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Sprinklr, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Sprinklr](#creating-a-sprinklr-test-user)**  -toohave un equivalente de Britta Simon en Sprinklr que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Sprinklr.

**inicio de sesión único en tooconfigure Azure AD con Sprinklr, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Sprinklr** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. En hello **Sprinklr dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sprinklr.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Estos valores no son reales. Actualice el valor de hello con hello real dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de Sprinklr](https://www.sprinklr.com/contact-us/) tooget estos valores. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. En hello **configuración de Sprinklr** sección, haga clic en **configurar Sprinklr** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

7. En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa Sprinklr tooyour como administrador.

8. Vaya demasiado**administración \> configuración**.
   
    ![Administración](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administración")

9. Vaya demasiado**administrar socios \> inicio de sesión único** en el panel izquierdo de Hola.
   
    ![Administración de asociado](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Administración de asociados")

10. Haga clic en **+Add Single Sign On**(+ Agregar inicios de sesión únicos).
   
    ![Inicios de sesión únicos](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Inicios de sesión únicos")

11. En hello **inicio de sesión único** , siga los pasos de hello:
   
    ![Inicios de sesión únicos](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Inicios de sesión únicos")

    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración (por ejemplo: *WAADSSOTest*).

    b. Seleccione **Habilitado**.

    c. Seleccione **Use new SSO Certificate**(Usar el nuevo certificado de SSO).
             
    e. Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidad** cuadro de texto.

    f. Hola pegar **Id. de entidad SAML** valor que ha copiado desde el Portal de Azure en hello **Id. de entidad** cuadro de texto.

    g. Hola pegar **SAML Single Sign-On dirección URL del servicio** valor que ha copiado desde el Portal de Azure en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.

    h. Hola pegar **dirección URL de cierre de sesión** valor que ha copiado desde el Portal de Azure en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.
     
    i. Como **Tipo de Id. de usuario de SAML**, seleccione **La aserción contiene el nombre de usuario de sprinklr.com del usuario**.

    j. Como **ubicación de Id. de usuario de SAML**, seleccione **Id. de usuario está en el elemento de identificador de nombre de Hola de hello instrucción Subject**.

    k. Haga clic en **Guardar**.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-sprinklr-test-user"></a>Creación de un usuario de prueba de Sprinklr

1. Inicie sesión en tooyour sitio de la empresa Sprinklr como administrador.

2. Vaya demasiado**administración \> configuración**.
   
    ![Administración](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administración")

3. Vaya demasiado**cliente administrar \> usuarios** en el panel izquierdo de Hola.
   
    ![Configuración](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Configuración")

4. Haga clic en **Agregar usuario**.
   
    ![Configuración](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Configuración")

5. En hello **Editar usuario** cuadro de diálogo, realizar Hola pasos:
   
    ![Edición de usuarios](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edición de usuarios") 

    a. Hola **correo electrónico**, **nombre** y **Last Name** cuadros de texto, información de tipo hello de una cuenta de usuario de Azure AD que desee tooprovision.

    b. Seleccione **Password Disabled**(Contraseña deshabilitada).

    c. Seleccione **Language** (Lenguaje).

    d. Seleccione **User Type**(Tipo de usuario).

    e. Haga clic en **Update**(Actualizar).
   
     >[!IMPORTANT]
     >**Contraseña deshabilitada** debe ser tooenable seleccionado un toolog de usuario en a través de un proveedor de identidades. 
     
6. Vaya demasiado**rol**y, a continuación, realizar Hola pasos:
   
    ![Roles de asociados](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Roles de asociados")

    a. De hello **Global** lista, seleccione **todos los\_permisos**.  

    b. Haga clic en **Update**(Actualizar).

>[!NOTE]
>Puede usar cualquier otra Sprinklr usuario cuenta herramienta de creación o las API proporcionadas por Sprinklr tooprovision cuentas de usuario de Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSprinklr.

![Asignar usuario][200] 

**tooassign Britta Simon tooSprinklr, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Sprinklr**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Sprinklr de Hola Hola Panel de acceso, debe obtener automáticamente ha iniciado sesión tooyour Sprinklr aplicación para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

