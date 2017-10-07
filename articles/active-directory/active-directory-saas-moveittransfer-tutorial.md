---
title: "Tutorial: Integración de Azure Active Directory con MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y transferencia de MOVEit - integración de Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Tutorial: Integración de Azure Active Directory con MOVEit Transfer - Azure AD integration

En este tutorial, aprenderá cómo toointegrate MOVEit transferencia: integración de Azure AD con Azure Active Directory (Azure AD).

Integración de transferencia de MOVEit - integración de Azure AD con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooMOVEit transferencia: integración de Azure AD.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMOVEit transferencia: integración de Azure AD (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con la transferencia de MOVEit - integración de Azure AD, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en MOVEit Transfer - Azure AD integration

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar MOVEit transferencia: integración de Azure AD desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Agregar MOVEit transferencia: integración de Azure AD desde la Galería de Hola
integración de hello tooconfigure de transferencia de MOVEit - integración de Azure AD en Azure AD, deberá tooadd MOVEit transferencia: integración de Azure AD de lista tooyour de hello Galería de aplicaciones administradas de SaaS.

**tooadd MOVEit transferencia: integración de Azure AD desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **MOVEit transferencia: integración de Azure AD**, seleccione **MOVEit transferencia: integración de Azure AD** desde el panel de resultados, a continuación, haga clic en **agregar** hello tooadd de botón aplicación.

    ![Transferencia de MOVEit - integración de Azure AD en la lista de resultados de Hola](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, configurará y probará el inicio de sesión único de Azure AD con MOVEit Transfer - Azure AD integration con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en transferencia de MOVEit - integración de Azure AD es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en transferencia de MOVEit - integración de Azure AD necesita toobe establecido.

En transferencia de MOVEit - integración de Azure AD, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con transferencia MOVEit - integración de Azure AD, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear una transferencia de MOVEit - usuario de prueba de integración de Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user) ** - toohave un equivalente de Britta Simon en transferencia de MOVEit - integración de Azure AD que está vinculado toohello Azure AD representación del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la transferencia de MOVEit - aplicación de integración de Azure AD.

**inicio de sesión único en tooconfigure Azure AD con la transferencia de MOVEit - integración de Azure AD, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **MOVEit transferencia: integración de Azure AD** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. En hello **MOVEit transferencia: integración de Azure AD dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://contoso.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://contoso.com/<tenatid>`

    c. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Puede hacer referencia a estos valores más tarde en **dirección URL de metadatos del proveedor de servicio** sección o póngase en contacto con [MOVEit transferencia: equipo de soporte técnico de cliente de integración de Azure AD](https://community.ipswitch.com/s/support) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Inicie sesión en tooyour MOVEit transferencia inquilino como administrador.

7. En el panel de navegación izquierdo de hello, haga clic en **configuración**.

    ![Sección Configuración en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Haga clic en el vínculo **Single Signon** (Inicio de sesión único) que se encuentra en **Security Policies -> User Auth** (Directivas de seguridad -> Autenticación de usuario).

    ![Directivas de seguridad en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Haga clic en el documento de metadatos de Hola de toodownload vínculo de dirección URL de metadatos de Hola.

    ![Dirección URL de metadatos del proveedor de servicios](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Comprobar **entityID** coincide con **identificador** en hello **MOVEit transferencia: integración de Azure AD dominio y las direcciones URL** sección.
    * Comprobar **AssertionConsumerService** coincide con la dirección URL de ubicación **dirección URL de respuesta** en hello **MOVEit transferencia: integración de Azure AD dominio y las direcciones URL** sección.
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Haga clic en **Agregar proveedor de identidades** botón tooadd un nuevo proveedor de identidad federada.

    ![Agregación del proveedor de identidades](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Haga clic en **Examinar... ** tooselect Hola archivo de metadatos que descargó desde el portal de Azure, a continuación, haga clic en **Agregar proveedor de identidades** hello tooupload el archivo descargado.

    ![Proveedor de identidades de SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Seleccione "**Sí**" como **habilitado** en hello **modificar configuración del proveedor de identidad federado... ** página y haga clic en **guardar**.

    ![Configuración del proveedor de identidades federadas](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. Hola **editar federado identidad del proveedor de configuración de usuario** página, lleve a cabo Hola siguientes acciones:
    
    ![Edición de la configuración del proveedor de identidades federadas](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Seleccione **SAML NameID** en **Login name** (Nombre de inicio de sesión).
    
    b. Seleccione **otros** como **nombre completo** y Hola **nombre del atributo** cuadro de texto establecer valor de hello: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Seleccione **otros** como **correo electrónico** y Hola **nombre del atributo** cuadro de texto establecer valor de hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Seleccione **Yes** (Sí) en **Auto-create account on signon** (Crear automáticamente cuenta al iniciar sesión).
    
    e. Haga clic en el botón **Guardar** .

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Creación de un usuario de prueba de MOVEit Transfer - Azure AD integration

objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en transferencia de MOVEit - integración de Azure AD. MOVEit Transfer - Azure AD integration admite el aprovisionamiento Just-In-Time que ha habilitado. No hay ningún elemento de acción para usted en esta sección. Se crea un nuevo usuario durante una tooaccess de intento de transferencia de MOVEit - integración de Azure AD si no existe todavía.

>[!NOTE]
>Si necesita un usuario toocreate manualmente, necesita hello toocontact [MOVEit transferencia: equipo de soporte técnico de cliente de integración de Azure AD](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMOVEit transferencia: integración de Azure AD.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooMOVEit transferencia: integración de Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **MOVEit transferencia: integración de Azure AD**.

    ![Transferencia Hello MOVEit - integración de Azure AD vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.

Al hacer clic en hello MOVEit transferencia - icono de integración de Azure AD en el Panel de acceso de hello, obtendrá automáticamente ha iniciado sesión tooyour MOVEit transferencia: aplicación de integración de Azure AD. 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

