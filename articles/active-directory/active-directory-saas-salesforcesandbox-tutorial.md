---
title: "Tutorial: Integración de Azure Active Directory con Salesforce Sandbox | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el espacio aislado de Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Tutorial: Integración de Azure Active Directory con Salesforce Sandbox

En este tutorial, aprenderá cómo toointegrate espacio aislado de Salesforce con Azure Active Directory (Azure AD).

Integración de Salesforce Sandbox con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSalesforce espacio aislado
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSalesforce espacio aislado (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Salesforce Sandbox tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Salesforce Sandbox

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar espacio aislado de Salesforce desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Agregar espacio aislado de Salesforce desde la Galería de Hola
integración de hello tooconfigure de espacio aislado de Salesforce en Azure AD, necesita tooadd espacio aislado de Salesforce en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Salesforce Sandbox de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Salesforce Sandbox**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. En el panel de resultados de hello, seleccione **Salesforce Sandbox**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Salesforce Sandbox con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en espacio aislado de Salesforce es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en espacio aislado de Salesforce debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en espacio aislado de Salesforce.

tooconfigure y prueba de inicio de sesión único en Azure AD con Salesforce Sandbox, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave un equivalente de Britta Simon en espacio aislado de Salesforce es representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de espacio aislado de Salesforce.

**inicio de sesión único en tooconfigure Azure AD con Salesforce Sandbox, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Salesforce Sandbox** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. En hello **dominio de espacio aislado de Salesforce y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Este valor no es hello real. Actualizar este valor con la URL de inicio de sesión real de Hola. Póngase en contacto con [equipo de soporte técnico de cliente de espacio aislado de Salesforce](https://help.salesforce.com/support) tooget este valor.


4. Si ya ha configurado un inicio de sesión único para otra instancia de Salesforce Sandbox de su directorio, también debe configurar hello **identificador** toohave Hola el mismo valor que hello **dirección URL de inicio de sesión**. 
    
    >[!Note]
    >Hola **identificador** campo puede encontrarse mediante la comprobación de hello **Mostrar configuración avanzada** casilla de verificación de hello **configurar URL de aplicación** página del cuadro de diálogo de Hola 


5. En hello **el certificado de firma de SAML** sección, haga clic en **certificado** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. En hello **configuración de espacio aislado de Salesforce** sección, haga clic en **configurar Salesforce Sandbox** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración del inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Abra una nueva pestaña en el explorador e inicie sesión tooyour cuenta de administrador de espacio aislado de Salesforce.

9. En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. En el panel de navegación de Hola Hola izquierda, haga clic en **controles de seguridad**y, a continuación, haga clic en **configuración de inicio de sesión único**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. En la sección de configuración de inicio de sesión único de hello, realizar Hola siguiendo los pasos: ![configurar Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Seleccione **SAML habilitado**. 

     b.  Haga clic en **Nuevo**.

12. En la sección de configuración de inicio de sesión único de SAML de hello, realizar Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    el cuadro de texto de a.In Hola nombre, escriba un nombre Hola de configuración de hello (p. ej.: *SPSSOWAAD\_prueba*). 

    b. Pegar **Id. de entidad Small** valor en hello **emisor** cuadro de texto.

    c. Hola **Id. de entidad** cuadro de texto, tipo **https://test.salesforce.com** si es Hola la primera instancia de Salesforce Sandbox que va a Agregar directorio tooyour. Si ya ha agregado una instancia de Salesforce Sandbox, después de hello **Id. de entidad** tipo Hola **dirección URL de inicio de sesión**, que debe tener este formato:`http://company.my.salesforce.com`  
 
    d. Haga clic en **examinar** hello tooupload descargado el certificado.  

    e. Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**.
 
    f. Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.

    g. Pegar **URL de servicio de inicio de sesión único** en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto. 

    h. SFDC no admite el cierre de sesión SAML.  Como alternativa, pegue 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' en hello **URL de cierre de sesión del proveedor de identidades** cuadro de texto.

    i. Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP POST** (Método HTTP POST). 

    j. Haga clic en **Guardar**.

### <a name="enable-your-domain"></a>Habilitación del dominio
En esta sección se supone que ya ha creado un dominio.  Para más información, consulte [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US) (Definición del nombre de dominio).

**tooenable su dominio, realizar Hola pasos:**

1. En el panel de navegación izquierdo de hello, haga clic en **Domain Management**y, a continuación, haga clic en **mi dominio.**
   
     ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Asegúrese de que su dominio se ha configurado correctamente. 

2. Hola **configuración de la página de inicio de sesión** sección, haga clic en **editar**, a continuación, como **servicio de autenticación**, seleccione nombre de Hola de hello configuración de inicio de sesión único de SAML de hello anterior sección y, por último, haga clic en **guardar**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Tan pronto como tiene configurado un dominio, los usuarios deben usar toohello Salesforce sandbox de hello dominio URL toologin.  

valor de hello tooget de dirección URL de hello, haga clic en perfil SSO de Hola que haya creado en la sección anterior de Hola.    

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Creación de un usuario de prueba de Salesforce Sandbox

En esta sección, creará un usuario llamado a Britta Simon en Salesforce Sandbox. Salesforce Sandbox admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.
No hay ningún elemento de acción para usted en esta sección. Si un usuario ya no existe en el espacio aislado de Salesforce, se crea uno nuevo si intentas tooaccess espacio aislado de Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSalesforce espacio aislado.

![Asignar usuario][200] 

**tooassign Britta Simon tooSalesforce de espacio aislado, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Salesforce Sandbox**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Si desea tootest la configuración de SSO, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

