---
title: "Tutorial: Integración de Azure Active Directory con Mimecast Personal Portal | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Portal Personal de Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>Tutorial: Integración de Azure Active Directory con Mimecast Personal Portal

En este tutorial, aprenderá cómo toointegrate Portal Personal de Mimecast con Azure Active Directory (Azure AD).

Integración de Portal Personal de Mimecast con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooMimecast Portal Personal
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMimecast Portal Personal (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con el Portal Personal de Mimecast tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Un suscripción habilitada para inicio de sesión único en Mimecast Personal Portal

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Portal Personal de Mimecast desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>Agregar Portal Personal de Mimecast desde la Galería de Hola
integración de hello tooconfigure del Portal Personal de Mimecast en Azure AD, deberá tooadd Portal Personal de Mimecast de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Portal Personal de Mimecast desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Portal Personal de Mimecast**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. En el panel de resultados de hello, seleccione **Portal Personal de Mimecast**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mimecast Personal Portal con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el Portal Personal de Mimecast es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el Portal Personal de Mimecast debe toobe establecido.

En el Portal Personal de Mimecast, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con el Portal Personal de Mimecast, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba del Portal Personal de Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave un equivalente de Britta Simon en el Portal Personal de Mimecast que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Portal Personal de Mimecast.

**tooconfigure inicio de sesión único en Azure AD con el Portal Personal de Mimecast, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Portal Personal de Mimecast** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. En hello **dominio Portal Personal de Mimecast y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de Portal Personal de Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget estos valores. 
 


4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. En hello **configuración del Portal Personal de Mimecast** sección, haga clic en **configurar el Portal Personal de Mimecast** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mimecast Personal Portal.

8. Vaya demasiado**servicios \> aplicaciones**.
   
    ![Aplicaciones](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Aplicaciones")

9. Haga clic en **Authentication Profiles**(Perfiles de autenticación).
   
    ![Authentication Profiles (Perfiles de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles (Perfiles de autenticación)")

10. Haga clic en **New Authentication Profile**(Nuevo perfil de autenticación).
   
    ![New Authentication Profile (Nuevo perfil de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile (Nuevo perfil de autenticación)")

11. Hola **perfil de autenticación** sección, lleve a cabo Hola pasos:
   
    ![Authentication Profile (Perfil de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile (Perfil de autenticación)")
   
    a. Hola **descripción** cuadro de texto, escriba un nombre para la configuración.
   
    b. Seleccione **Aplicar la autenticación SAML a Mimecast Personal Portal**.
   
    c. Como **Provider** (Proveedor), seleccione **Azure Active Directory**.
   
    d. En **dirección URL del emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.
   
    e. En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.
   
    f. En **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.

    g. Abra su **base-64** codificado certificado en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidades (metadatos)** cuadro de texto.

    h. Seleccione **Permitir inicio de sesión único**.
   
    i. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>Creación de un usuario de prueba de Mimecast Personal Portal

En orden tooenable toolog de los usuarios de Azure AD en el Portal Personal de Mimecast, se les deben aprovisionar en el Portal Personal de Mimecast. En caso de hello del Portal Personal de Mimecast, el aprovisionamiento es una tarea manual.

Deberá tooregister un dominio para poder crear los usuarios.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicio de sesión tooyour **Portal Personal de Mimecast** como administrador.

2. Vaya demasiado**directorios \> interno**.
   
    ![Directories (Directorios)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories (Directorios)")

3. Haga clic en **Register New Domain**(Registrar nuevo dominio).
   
    ![Register New Domain (Registrar nuevo dominio)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain (Registrar nuevo dominio)")

4. Una vez creado el nuevo dominio, haga clic en **New Address**(Nueva dirección).
   
    ![New Address (Nueva dirección)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address (Nueva dirección)")

5. Hola dirección cuadro de diálogo nuevo, realizar Hola siguiendo los pasos de un Azure válida que desee tooprovision de cuenta de AD:
   
    ![Guardar](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Guardar")
   
    a. Hola **dirección de correo electrónico** cuadro de texto, tipo **dirección de correo electrónico** del usuario de hello como  **BrittaSimon@contoso.com** .
    
    b. Hola **nombre Global** cuadro de texto, hello tipo **nombre de usuario** como **BrittaSimon**.

    c. Hola **contraseña**, y **Confirmar contraseña** cuadros de texto, hello tipo **contraseña** del usuario de Hola.
   
    b. Haga clic en **Guardar**.

>[!NOTE]
>Puede usar cualquier otra herramienta de creación de cuentas de usuario de Portal Personal de Mimecast o las API proporcionadas por las cuentas de usuario de Azure AD de Portal Personal de Mimecast tooprovision. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMimecast Portal Personal.

![Asignar usuario][200] 

**tooassign Britta Simon tooMimecast Portal Personal, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Portal Personal de Mimecast**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 
En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Portal Personal de Mimecast Hola Hola Panel de acceso, deberá obtener la aplicación de Portal Personal de Mimecast tooyour automáticamente ha iniciado sesión. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

