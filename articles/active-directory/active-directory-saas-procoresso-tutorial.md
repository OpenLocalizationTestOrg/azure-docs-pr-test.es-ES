---
title: "Tutorial: Integración de Azure Active Directory con Procore SSO | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO Procore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Tutorial: Integración de Azure Active Directory con Procore SSO

En este tutorial, aprenderá cómo toointegrate Procore SSO con Azure Active Directory (Azure AD).

Integración de SSO Procore con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooProcore SSO
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooProcore SSO (inicio de sesión único) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con SSO Procore tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Procore SSO

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar SSO Procore desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-procore-sso-from-hello-gallery"></a>Agregar SSO Procore desde la Galería de Hola
integración de hello tooconfigure de SSO Procore en Azure AD, deberá tooadd SSO Procore de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Procore SSO de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Procore SSO**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. En el panel de resultados de hello, seleccione **SSO Procore**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Procore SSO con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SSO Procore es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SSO Procore debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Procore SSO.

tooconfigure y prueba de inicio de sesión único en Azure AD con SSO Procore, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de SSO Procore](#creating-a-procore-sso-test-user)**  -toohave un equivalente de Britta Simon en Procore SSO que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación SSO Procore.

**inicio de sesión único en tooconfigure Azure AD con SSO Procore, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **SSO Procore** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. En hello **Procore de SSO de dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. En hello **Procore configuración de SSO** sección, haga clic en **configurar SSO Procore** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. inicio de sesión único en tooconfigure en **Procore SSO** lado, un sitio de empresa procore tooyour de inicio de sesión como administrador.

8. De colocación del cuadro de herramientas de hello hacia abajo, haga clic en **administración** página de configuración de SSO de tooopen Hola.

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Describen los valores de hello pegar Hola que en los cuadros siguientes:

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. Hola **único inicio de sesión en dirección URL del emisor** cuadro, pegue Hola Id. de entidad SAML copiado de hello portal de Azure.

    b. Hola **SAML inicio de sesión en dirección URL de destino** cuadro, pegue Hola SAML Single Sign-On dirección URL del servicio se copian de hello portal de Azure.

    c. Ahora, abra hello **Metadata XML** descargado anteriormente de hello portal de Azure y copia certificados de hello en etiqueta Hola denominado **X509Certificate**. Hola pegar copia valor en hello **Single Sign On x509 certificado** cuadro.

10. Haga clic en **Guardar cambios**.

11. Después de esta configuración, debe hello toosend **nombre de dominio** (por ejemplo **contoso.com**) a través de que está iniciando en toohello Procore [equipo de soporte técnico Procore](https://support.procore.com/) y Activar SSO federado para ese dominio.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-procore-sso-test-user"></a>Creación de un usuario de prueba de Procore SSO

Siga Hola por debajo de los pasos toocreate un usuario de prueba Procore en uno de su lados.

1. Sitio de empresa procore de tooyour de inicio de sesión como administrador.  

2. De colocación del cuadro de herramientas de hello hacia abajo, haga clic en **Directory** página del directorio de la compañía de tooopen Hola.

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Haga clic en **agregar una persona** opción tooopen formulario de Hola y escriba realizar las siguientes opciones:

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. Hola **nombre** cuadro de texto Nombre del usuario de tipo como **Bárbara**.

    b. Hola **apellidos** cuadro de texto, apellido del usuario de tipo como **Simon**.

    c. Hola **dirección de correo electrónico** como dirección de correo electrónico del usuario del tipo de cuadro de texto,  **BrittaSimon@contoso.com** .

    d. Seleccione **Permission Template** (Plantilla de permisos) como **Apply Permission Template Later** (Aplicar plantilla de permisos más tarde).

    e. Haga clic en **Crear**.

4. Comprobar y actualizar los detalles de Hola Hola recién agregado contacto.

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Haga clic en **guardar y Enviar invitación** (si se requiere una invitación por correo electrónico) o **guardar** (guardar directamente) registro de usuario de toocomplete Hola.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooProcore acceso SSO.

![Asignar usuario][200] 

**tooassign Britta Simon tooProcore SSO, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Procore SSO**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso. Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586). Al hacer clic en icono de SSO Procore Hola Hola Panel de acceso, deberá obtener la aplicación de SSO Procore tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

