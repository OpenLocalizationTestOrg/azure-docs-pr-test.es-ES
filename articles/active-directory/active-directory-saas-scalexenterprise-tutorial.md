---
title: "Tutorial: Integración de Azure Active Directory con ScaleX Enterprise | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Tutorial: Integración de Azure Active Directory con ScaleX Enterprise

En este tutorial, aprenderá cómo toointegrate ScaleX Enterprise con Azure Active Directory (Azure AD).

Integración ScaleX Enterprise con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooScaleX Enterprise
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooScaleX Enterprise (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte. ¿Qué es el acceso a aplicaciones y el inicio de sesión único con [Azure Active Directory](active-directory-appssoaccess-whatis.md)?

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con ScaleX Enterprise tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en ScaleX Enterprise

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use su entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar ScaleX Enterprise desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Agregar ScaleX Enterprise desde la Galería de Hola
integración de hello tooconfigure de ScaleX Enterprise en tooAzure AD, deberá tooadd ScaleX Enterprise de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd ScaleX Enterprise de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **ScaleX Enterprise**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. En el panel de resultados de hello, seleccione **ScaleX Enterprise**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ScaleX Enterprise utilizando un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ScaleX Enterprise es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ScaleX empresa necesita toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en ScaleX Enterprise.

tooconfigure y prueba de inicio de sesión único en Azure AD con ScaleX Enterprise, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave un equivalente de Britta Simon en ScaleX Enterprise que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación empresarial de ScaleX.

**inicio de sesión único en tooconfigure AD de Azure con ScaleX Enterprise, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **ScaleX Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. En hello **ScaleX Enterprise dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. Hola **identificador** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://platform.rescale.com/saml2/<company id>/`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Estas no son valores reales de Hola. Actualizar estos valores con hello identificador real, la dirección URL de respuesta o la dirección URL de inicio de sesión. Póngase en contacto con [equipo de soporte técnico de cliente de empresa ScaleX](http://info.rescale.com/contact_sales) tooget estos valores. 

5. La aplicación ScaleX espera las aserciones de SAML de hello en un formato específico, lo que requiere toomodify atributo personalizado tooyour SAML atributos de token configuración de asignaciones. Haga clic en **ver y editar todos los demás atributos de usuario** casilla tooopen Hola personalizado atributos de configuración.

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Haga clic con el atributo de hello **nombre** y haga clic en eliminar.

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Haga clic en **emailaddress** ventana Editar atributo de atributo tooopen hello. Cambie el valor de **user.mail** demasiado**user.userprincipalname** y haga clic en Aceptar.

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. En hello **configuración de la empresa ScaleX** sección, haga clic en **configurar ScaleX Enterprise** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. inicio de sesión único en tooconfigure en **ScaleX Enterprise** lado, el sitio Web de Enterprise ScaleX empresa toohello de inicio de sesión como administrador.

9. Haga clic en menú Hola Hola superior derecha y seleccione **Contoso administración**.

    > [!NOTE] 
    > Contoso solo es un ejemplo. Debería tratarse del nombre real de la empresa. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Seleccione **integraciones** desde el menú superior de Hola y seleccione **Single Sign-On**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Complete el formulario de hello como se indica a continuación:

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Seleccione **"Create any user who can authenticate with SSO"** (Crear cualquier usuario que se pueda autenticar con SSO).

    b. **Proveedor de servicios saml**: pegue el valor de hello ***urn: oasis: nombres: tc: SAML:2.0:nameid-formato: persistente***

    c. **Nombre del campo de correo electrónico del proveedor de identidades en la respuesta de ACS**: pegue el valor de Hola`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **Id. de entidad EntityDescriptor de proveedor de identidad:** Hola pegar **Id. de entidad SAML** valor copiados de hello portal de Azure.

    e. **URL de SingleSignOnService del proveedor de identidades:** Hola pegar **SAML Single Sign-On dirección URL del servicio** de hello portal de Azure.

    f. **Certificado público X509 del proveedor de identidades:** descargar el certificado de hello abierto X509 de hello Azure en el Bloc de notas y pegue contenido de hello en este cuadro. Asegúrese de que no haya que ningún saltos de línea hello intermedia del contenido del certificado de Hola.
    
    g. Comprobar Hola siguiendo las casillas de verificación: **habilitado, cifrar NameID y AuthnRequests de inicio de sesión.**

    h. Haga clic en **configuración de SSO de actualización** configuración de toosave Hola.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Creación de un usuario de prueba de ScaleX Enterprise

toolog de los usuarios de Azure AD tooenable en tooScaleX Enterprise, se les deben aprovisionar en tooScaleX Enterprise. En caso de hello de ScaleX Enterprise, el aprovisionamiento es una tarea automática y no se requiere ningún paso manual. Todos los usuarios que pueden autenticar correctamente con las credenciales SSO se aprovisionará automáticamente en hello ScaleX lado.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de empresa de tooScaleX de acceso de usuarios.

![Asignar usuario][200] 

**tooassign Britta Simon tooScaleX Enterprise, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ScaleX Enterprise**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Haga clic en hello ScaleX Enterprise disponer en mosaico en hello Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour aplicación ScaleX empresarial. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

