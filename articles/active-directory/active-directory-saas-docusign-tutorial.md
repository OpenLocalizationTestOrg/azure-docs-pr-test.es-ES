---
title: "Tutorial: integración de Azure Active Directory con DocuSign | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>Tutorial: Integración de Azure Active Directory con DocuSign

En este tutorial, aprenderá cómo toointegrate DocuSign con Azure Active Directory (Azure AD).

Integración de DocuSign con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooDocuSign
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDocuSign (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con DocuSign tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en DocuSign

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar DocuSign desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-docusign-from-hello-gallery"></a>Agregar DocuSign desde la Galería de Hola
integración de hello tooconfigure de DocuSign en Azure AD, deberá tooadd DocuSign de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd DocuSign de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **DocuSign**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. En el panel de resultados de hello, seleccione **DocuSign**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con DocuSign con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en DocuSign es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en DocuSign debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en DocuSign.

tooconfigure y prueba de inicio de sesión único en Azure AD con DocuSign, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de DocuSign](#creating-a-docusign-test-user) ** -toohave un equivalente de Britta Simon en DocuSign que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de DocuSign.

**inicio de sesión único en tooconfigure Azure AD con DocuSign, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **DocuSign** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base 64)** y, a continuación, guarde el archivo de certificado en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. En hello **configuración de DocuSign** sección del portal de Azure, haga clic en **DocuSign configurar** ventana tooopen configurar inicio de sesión. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. En una ventana del explorador web diferente, inicio de sesión tooyour **portal de administración de DocuSign** como administrador.

6. En el menú de navegación de Hola Hola izquierda, haga clic en **dominios**.
   
    ![Configuración del inicio de sesión único][51]

7. En el panel derecho de hello, haga clic en **notificación dominio**.
   
    ![Configuración del inicio de sesión único][52]

8. En hello **de notificación de un dominio** cuadro de diálogo, en hello **nombre de dominio** cuadro de texto, escriba el dominio de su empresa y, a continuación, haga clic en **notificación**. Asegúrese de comprobar el dominio de Hola y Hola estado está activo.
   
    ![Configuración del inicio de sesión único][53]

9. En el menú en el lado izquierdo de hello, haga clic en **proveedores de identidades**  
   
    ![Configuración del inicio de sesión único][54]
10. En el panel derecho de hello, haga clic en **Agregar proveedor de identidades**. 
   
    ![Configuración del inicio de sesión único][55]

11. En hello **configuración del proveedor de identidad** , siga los pasos de hello:
   
    ![Configuración del inicio de sesión único][56]

    a. Hola **nombre** cuadro de texto, escriba un nombre único para la configuración. No utilice espacios.

    b. Pegar **Id. de entidad SAML** en hello **emisor del proveedor de identidades** cuadro de texto.

    c. Pegar **SAML Single Sign-On dirección URL del servicio** en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.

    d. Pegar **dirección URL de cierre de sesión** en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.

    e. Seleccione **Sign AuthN Request**(Firmar solicitud de autenticación).

    f. En **Send AuthN request by** (Enviar solicitud de autorización por), seleccione **POST**.

    g. En **Send logout request by** (Enviar solicitud de cierre de sesión por), seleccione **GET**.

12. Hola **asignación de atributo personalizado** sección, elija el campo de Hola que desee toomap con notificación de AD de Azure. En este ejemplo, Hola **emailaddress** notificación se asigna su valor hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**. Es nombre de notificación predeterminado de Hola de Azure AD para notificación de correo electrónico. 
   
    > [!NOTE]
    > Hola de uso adecuado **identificador de usuario** toomap usuario de saludo de la asignación de usuario de Azure AD tooDocuSign. Seleccione Hola campo apropiado y escriba el valor adecuado de hello según la configuración de la organización.
          
    ![Configuración del inicio de sesión único][57]

13. Hola **certificado del proveedor de identidad** sección, haga clic en **agregar certificado**y, a continuación, cargar el certificado de Hola que ha descargado desde el portal de Azure AD.   
   
    ![Configuración del inicio de sesión único][58]

14. Haga clic en **Guardar**.

15. Hola **proveedores de identidades** sección, haga clic en **acciones**y, a continuación, haga clic en **extremos**.   
   
    ![Configuración del inicio de sesión único][59]
 
16. Hola **ver SAML 2.0 extremos** sección **portal de administración de DocuSign**, realizar Hola pasos:
   
    ![Configuración del inicio de sesión único][60]
   
    a. Hola copia **dirección URL del emisor de proveedor de servicio**y, a continuación, pegue en hello **identificador** en el cuadro de texto **DocuSign dominio y las direcciones URL** sección de hello Azure Hola siguiente portal patrón: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.
   
    b. Hola copia **dirección URL de inicio de sesión del proveedor de servicio**y, a continuación, pegue en hello **dirección URL de inicio de sesión** en el cuadro de texto **DocuSign dominio y las direcciones URL** sección de hello Azure Hola siguiente portal patrón: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  Haga clic en **Close**
    
17. En el portal de Azure hello, haga clic en **guardar**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-docusign-test-user"></a>Creación de un usuario de prueba de DocuSign

Admite la aplicación **sólo en el aprovisionamiento de usuarios de tiempo** y después de autenticar usuarios se crean automáticamente en la aplicación hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooDocuSign de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooDocuSign, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **DocuSign**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de DocuSign Hola Hola Panel de acceso, deberá obtener aplicaciones de DocuSign tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

