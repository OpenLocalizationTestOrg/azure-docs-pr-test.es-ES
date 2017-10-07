---
title: "Tutorial: Integración de Azure Active Directory con Teamphoria | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Tutorial: Integración de Azure Active Directory con Teamphoria

En este tutorial, aprenderá cómo toointegrate Teamphoria con Azure Active Directory (Azure AD).

Integración Teamphoria con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTeamphoria
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTeamphoria (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Teamphoria tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Teamphoria

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Teamphoria desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-teamphoria-from-hello-gallery"></a>Agregar Teamphoria desde la Galería de Hola
integración de hello tooconfigure de Teamphoria en Azure AD, deberá tooadd Teamphoria de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Teamphoria de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Teamphoria**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. En el panel de resultados de hello, seleccione **Teamphoria**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Teamphoria con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Teamphoria es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Teamphoria debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Teamphoria.

tooconfigure y prueba de inicio de sesión único en Azure AD con Teamphoria, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Teamphoria](#creating-a-teamphoria-test-user) ** -toohave un equivalente de Britta Simon en Teamphoria que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación Teamphoria.

**inicio de sesión único en Azure AD tooconfigure con Teamphoria, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **Teamphoria** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. En hello **Teamphoria dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL con hello sigue el patrón:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tiene estos valores con hello tooupdate dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de cliente de Teamphoria](https://www.teamphoria.com/) tooget Hola sesión URL. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. En hello **Teamphoria configuración** sección, haga clic en **configurar Teamphoria** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. inicio de sesión único en tooconfigure en **Teamphoria** lado, la aplicación de Teamphoria tooyour de inicio de sesión como administrador.

8. Vaya demasiado**configuración de administración** opción en la barra de herramientas izquierda hello y en Hola Hola ficha configurar, haga clic en **inicio de sesión único** ventana de configuración de SSO de hello tooopen.

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Haga clic en **Agregar nuevo proveedor de IDENTIDADES** opción en forma de Hola de tooopen Hola esquina superior derecha para agregar una configuración de Hola para SSO.

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Escriba los detalles de hello en campos de hello tal como se describe a continuación:

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **NOMBRE para mostrar** : escriba el nombre para mostrar hello de complemento de hello en la página de administración Hola.

    b. **NOMBRE del botón** : nombre de Hola de pestaña de Hola que se mostrará en la página de inicio de sesión de hello para el inicio de sesión mediante SSO.

    c. **CERTIFICADO** : Hola abierto certificado descargó anteriormente desde el portal de Azure en el Bloc de notas, copie el contenido de Hola Hola Hola igual y péguelo aquí en el cuadro de Hola.

    d. **PUNTO de entrada** : Hola pegar **SAML Single Sign-On dirección URL del servicio** copian Hola de formulario anterior portal de Azure.

    e. Cambiar la opción de hello demasiado**ON** y haga clic en **guardar**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-teamphoria-test-user"></a>Crear un usuario de prueba Teamphoria

En orden tooenable toolog de los usuarios de Azure AD en Teamphoria, se les deben aprovisionar en Teamphoria. En caso de hello de Teamphoria, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour Teamphoria sitio de su compañía como administrador.

2. Haga clic en **administración** parámetros en la barra de herramientas izquierda hello y en hello **administrar** pestaña haga clic en **usuarios** tooopen página de administración de Hola para los usuarios.

    ![Agregar empleado](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Haga clic en hello **invitar a MANUAL** opción.

    ![Invitar a contactos](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. En esta página, realizar las acciones siguientes. 
    
    ![Invitar a contactos](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. Hola **dirección de correo electrónico** cuadro de texto, hello **dirección de correo electrónico** de BrittaSimon.

    b. Hola **nombre** cuadro de texto, tipo **Bárbara**.

    c. Hola **LAST NAME** cuadro de texto, tipo **Simon**.

    d. Haga clic en **INVITE 1 USER**. El usuario necesita tooaccept Hola invitación tooget creado en el sistema de Hola.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooTeamphoria de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooTeamphoria, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Teamphoria**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso. Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

