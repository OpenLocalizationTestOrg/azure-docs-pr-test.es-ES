---
title: "Tutorial: Integración de Azure Active Directory con myPolicies | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a>Tutorial: Integración de Azure Active Directory con myPolicies

En este tutorial, aprenderá cómo toointegrate myPolicies con Azure Active Directory (Azure AD).

Integración myPolicies con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso toomyPolicies
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión toomyPolicies (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con myPolicies tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en myPolicies

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar myPolicies desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-mypolicies-from-hello-gallery"></a>Agregar myPolicies desde la Galería de Hola
integración de hello tooconfigure de myPolicies en Azure AD, deberá tooadd myPolicies de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd myPolicies de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **myPolicies**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. En el panel de resultados de hello, seleccione **myPolicies**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con myPolicies con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en myPolicies es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en myPolicies debe toobe establecido.

En myPolicies, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con myPolicies, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba myPolicies](#creating-a-mypolicies-test-user)**  -toohave un equivalente de Britta Simon en myPolicies que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación myPolicies.

**inicio de sesión único en Azure AD tooconfigure con myPolicies, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **myPolicies** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. En hello **myPolicies dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.mypolicies.com/`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico myPolicies](mailto:support@mypolicies.com) tooget estos valores.

4. aplicación de Hello myPolicies espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones. Configurar Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. Haga clic en **ver y editar todos los demás atributos de usuario** checkbox en hello **atributos de usuario** sección atributos de hello tooexpand. Realizar Hola siguiendo los pasos en cada uno de los atributos de muestra de Hola-

    | Nombre del atributo | Valor de atributo |
    | ------------------- | ---------- |
    | givenname | user.givenname |
    | surname | user.surname |
    | emailaddress | user.mail |
    | name | user.userprincipalname |
    
    a. Haga clic en Hola de hello atributo tooopen **Editar atributo** cuadro de diálogo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    b. Eliminar el valor de dirección URL de Hola de hello **Namespace**.
    
    c. Haga clic en **Aceptar** configuración de toosave Hola.
    
6. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. En hello **myPolicies configuración** sección, haga clic en **configurar myPolicies** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. inicio de sesión único en tooconfigure en **myPolicies** lado, necesita hello toosend descargado **Certificate(Base64)** y **SAML Single Sign-On dirección URL del servicio** demasiado[equipo de soporte técnico myPolicies](mailto:support@mypolicies.com). 

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-mypolicies-test-user"></a>Creación de un usuario de prueba de myPolicies

En esta sección, se crea un usuario denominado Britta Simon en myPolicies. Trabajar con [equipo de soporte técnico myPolicies](mailto:support@mypolicies.com) para agregar usuarios de hello en la plataforma de myPolicies Hola. Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso toomyPolicies.

![Asignar usuario][200] 

**tooassign Britta Simon toomyPolicies, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **myPolicies**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello myPolicies el icono Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour myPolicies aplicación.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

