---
title: "Tutorial: Integración de Azure Active Directory con PolicyStat | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Tutorial: Integración de Azure Active Directory con PolicyStat

En este tutorial, aprenderá cómo toointegrate PolicyStat con Azure Active Directory (Azure AD).

Integración PolicyStat con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooPolicyStat
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPolicyStat (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con PolicyStat tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en PolicyStat

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar PolicyStat desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-policystat-from-hello-gallery"></a>Agregar PolicyStat desde la Galería de Hola
integración de hello tooconfigure de PolicyStat en Azure AD, deberá tooadd PolicyStat de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd PolicyStat de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **PolicyStat**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. En el panel de resultados de hello, seleccione **PolicyStat**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con PolicyStat con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PolicyStat es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PolicyStat debe toobe establecido.

En PolicyStat, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con PolicyStat, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba PolicyStat](#creating-a-policystat-test-user)**  -toohave un equivalente de Britta Simon en PolicyStat que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación PolicyStat.

**inicio de sesión único en Azure AD tooconfigure con PolicyStat, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **PolicyStat** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. En hello **PolicyStat dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.policystat.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de PolicyStat](http://www.policystat.com/support/) tooget estos valores. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooPolicyStat con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

    Hola PolicyStat aplicación espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de Token SAML** configuración.  

     Hola siguiente captura de pantalla muestra un ejemplo de esto.

     ![Atributos](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Atributos")

6. asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:

    | Nombre del atributo    |   Valor de atributo |
    |------------------- | -------------------- |
    | uid | ExtractMailPrefix([mail]) |
    
    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. Hola **nombre del atributo** cuadro de texto, tipo **uid**.

    c. Hola **valor del atributo** cuadro de texto, seleccione **ExtractMailPrefix()**.    
   
    d. De hello **correo** lista, seleccione **User.mail**.
    
    e. Haga clic en **Aceptar**.

7. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. En otra ventana del explorador web, inicie sesión en el sitio de la compañía PolicyStat como administrador.

9. Haga clic en hello **administración** ficha y, a continuación, haga clic en **configuración de inicio de sesión único** en el panel de navegación izquierdo.
   
    ![Menú Administrator](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menú Administrator")

10. Hola **el programa de instalación** sección, seleccione **integración de inicio de sesión único habilitar**.
   
    ![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuración de inicio de sesión único")

11. Haga clic en **configurar los atributos de**y, a continuación, en hello **configurar los atributos** sección, lleve a cabo Hola pasos:
   
    ![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuración de inicio de sesión único")
   
    a. Hola **atributo Username** cuadro de texto, tipo **uid**.

    b. Hola **atributo de nombre** cuadro de texto, tipo **firstname** del usuario **Bárbara**.

    c. Hola **último atributo de nombre** cuadro de texto, tipo **lastname** del usuario **Simon**.

    d. Hola **atributo de correo electrónico** cuadro de texto, tipo **emailaddress** del usuario  **BrittaSimon@contoso.com** .

    e. Haga clic en **Guardar cambios**.

12. Haga clic en **los metadatos de IDP**y, a continuación, en hello **los metadatos de IDP** sección, lleve a cabo Hola pasos:
   
    ![Configuración de inicio de sesión único](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuración de inicio de sesión único")
   
    a. Abra el archivo de metadatos descargado, Hola copia contenido y, a continuación, péguelo en hello **los metadatos del proveedor de identidad** cuadro de texto.

    b. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-policystat-test-user"></a>Creación de un usuario de prueba de PolicyStat

En orden tooenable toolog de los usuarios de Azure AD en PolicyStat, se les deben aprovisionar en PolicyStat.  

PolicyStat admite aprovisionamiento de usuarios justo a tiempo. Esto significa, no es necesario a los usuarios de tooadd Hola manualmente tooPolicyStat. los usuarios de Hola se agregarán automáticamente su primer inicio de sesión a través de SSO.

>[!NOTE]
>Puede usar cualquier otra PolicyStat usuario cuenta herramienta de creación o las API proporcionadas por PolicyStat tooprovision cuentas de usuario de Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPolicyStat.

![Asignar usuario][200] 

**tooassign Britta Simon tooPolicyStat, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **PolicyStat**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de PolicyStat Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour PolicyStat aplicación.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

