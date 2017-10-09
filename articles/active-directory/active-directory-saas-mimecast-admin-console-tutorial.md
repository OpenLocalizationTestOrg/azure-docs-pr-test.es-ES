---
title: "Tutorial: Integración de Azure Active Directory con Mimecast Admin Console | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la consola de administración de Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Tutorial: Integración de Azure Active Directory con Mimecast Admin Console

En este tutorial, aprenderá cómo la consola de administración de Mimecast toointegrate con Azure Active Directory (Azure AD).

Integración de la consola de administración de Mimecast con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooMimecast consola de administración.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMimecast consola de administración (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con la consola de administración de Mimecast tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Un suscripción habilitada para inicio de sesión único en Mimecast Admin Console

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar la consola de administración de Mimecast de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a>Agregar la consola de administración de Mimecast de galería de Hola
integración de hello tooconfigure de consola de administración de Mimecast en Azure AD, deberá tooadd consola de administración de Mimecast de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd consola de administración de Mimecast de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **consola de administración de Mimecast**, seleccione **consola de administración de Mimecast** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Lista de resultados de la consola de administración de Mimecast Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mimecast Admin Console con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en la consola de administración de Mimecast es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la consola de administración de Mimecast debe toobe establecido.

En la consola de administración de Mimecast, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con la consola de administración de Mimecast, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de la consola de administración de Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave un equivalente de Britta Simon en la consola de administración de Mimecast es representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de consola de administración de Mimecast.

**tooconfigure inicio de sesión único en Azure AD con la consola de administración de Mimecast, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **consola de administración de Mimecast** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. En hello **Mimecast dominio de la consola de administración y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > dirección URL de inicio de sesión Hello es específica de la región.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. En hello **configuración de consola de administración de Mimecast** sección, haga clic en **configurar la consola de administración de Mimecast** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mimecast Admin Console.

8. Vaya demasiado**servicios \> aplicación**.

    ![Servicios](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Servicios")

9. Haga clic en **Authentication Profiles**(Perfiles de autenticación).

    ![Authentication Profiles (Perfiles de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles (Perfiles de autenticación)")
    
10. Haga clic en **New Authentication Profile**(Nuevo perfil de autenticación).

    ![New Authentication Profiles (Nuevos perfiles de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Authentication Profiles (Nuevos perfiles de autenticación)")

11. Hola **perfil de autenticación** sección, lleve a cabo Hola pasos:

    ![Authentication Profile (Perfil de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile (Perfil de autenticación)")
    
    a. Hola **descripción** cuadro de texto, escriba un nombre para la configuración.
    
    b. Seleccione **Enforce SAML Authentication for Mimecast Admin Console**(Aplicar la autenticación SAML a Mimecast Admin Console).
    
    c. Como **Provider** (Proveedor), seleccione **Azure Active Directory**.
    
    d. Pegar **Id. de entidad SAML**, que haya copiado desde Hola portal de Azure en hello **dirección URL del emisor** cuadro de texto.
    
    e. Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión** cuadro de texto.

    f. Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **Logout URL** cuadro de texto.
    
    >[!NOTE]
    >Hello valor de dirección URL de inicio de sesión y el valor de dirección URL de cierre de sesión de hello son para hello consola de administración de Mimecast Hola igual.
    
    g. Abrir el certificado en base 64 se descarga desde el portal de Azure en el Bloc de notas, quitar la primera línea de hello ("*--*") y la última línea de hello ("*--*"), Hola copia restantes contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidades (metadatos)** cuadro de texto.
    
    h. Seleccione **Permitir inicio de sesión único**.
    
    i. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-a-mimecast-admin-console-test-user"></a>Creación de un usuario de prueba de Mimecast Admin Console

En orden tooenable toolog de los usuarios de Azure AD en la consola de administración de Mimecast, se les deben aprovisionar en la consola de administración de Mimecast. En caso de hello de la consola de administración de Mimecast, el aprovisionamiento es una tarea manual.

* Deberá tooregister un dominio para poder crear los usuarios.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicio de sesión tooyour **consola de administración de Mimecast** como administrador.
2. Vaya demasiado**directorios \> interno**.
   
   ![Directories (Directorios)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories (Directorios)")
3. Haga clic en **Register New Domain**(Registrar nuevo dominio).
   
   ![Register New Domain (Registrar nuevo dominio)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain (Registrar nuevo dominio)")
4. Una vez creado el nuevo dominio, haga clic en **New Address**(Nueva dirección).
   
   ![New Address (Nueva dirección)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address (Nueva dirección)")
5. Hola dirección cuadro de diálogo nuevo, siga Hola pasos:
   
   ![Guardar](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Guardar")
   
   a. Hola de tipo **dirección de correo electrónico**, **nombre Global**, **contraseña**, y **Confirmar contraseña** atributos de un anuncio de Azure válido de la cuenta desea tooprovision en hello relacionados con cuadros de texto.

   b. Haga clic en **Guardar**.

>[!NOTE]
>Puede usar cualquier otra herramienta de creación de cuentas de usuario de consola de administración de Mimecast o las API proporcionadas por las cuentas de usuario de consola de administración de Mimecast tooprovision Azure AD. 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMimecast consola de administración.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooMimecast consola de administración, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **consola de administración de Mimecast**.

    ![vínculo de la consola de administración de Mimecast de Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de la consola de administración de Mimecast de Hola Hola Panel de acceso, deberá obtener la aplicación de consola de administración de Mimecast tooyour automáticamente ha iniciado sesión.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

