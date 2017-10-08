---
title: "Tutorial: Integración de Azure Active Directory con Jobscience | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Tutorial: Integración de Azure Active Directory con Jobscience

En este tutorial, aprenderá cómo toointegrate Jobscience con Azure Active Directory (Azure AD).

Integración Jobscience con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooJobscience
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJobscience (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Jobscience tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Jobscience

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Jobscience desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-jobscience-from-hello-gallery"></a>Agregar Jobscience desde la Galería de Hola
integración de hello tooconfigure de Jobscience en Azure AD, deberá tooadd Jobscience de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Jobscience de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Jobscience**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. En el panel de resultados de hello, seleccione **Jobscience**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jobscience con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Jobscience es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Jobscience debe toobe establecido.

En Jobscience, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Jobscience, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Jobscience](#creating-a-jobscience-test-user)**  -toohave un equivalente de Britta Simon en Jobscience que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Jobscience.

**inicio de sesión único en tooconfigure Azure AD con Jobscience, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Jobscience** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. En hello **Jobscience dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello dirección URL de inicio de sesión real. Obtener este valor [equipo de soporte técnico de Jobscience cliente](https://www.jobscience.com/support) o del perfil SSO de hello creará que se explica más adelante en el tutorial Hola. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. En hello **configuración de Jobscience** sección, haga clic en **configurar Jobscience** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Inicie sesión en tooyour sitio de la compañía Jobscience como administrador.

8. Vaya demasiado**el programa de instalación**.
   
   ![Instalación](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Instalación")

9. En el panel de navegación izquierdo de hello, Hola **administrar** sección, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello  **Mi dominio** página. 
   
   ![Mi dominio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Mi dominio")

10. tooverify que el dominio se ha configurado correctamente, asegúrese de que se encuentra en "**paso 4 implementado tooUsers**" y revise el "**mi configuración de dominio**".

    ![Dominio implementado tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser implementadas de dominio")

11. En el sitio de la compañía de Jobscience hello, haga clic en **controles de seguridad**y, a continuación, haga clic en **configuración de inicio de sesión único**.
    
    ![Controles de seguridad](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Controles de seguridad")

12. Hola **configuración de inicio de sesión único** sección, lleve a cabo Hola pasos:
    
    ![Configuración de inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Configuración de inicio de sesión único")
    
    a. Seleccione **SAML habilitado**.

    b. Haga clic en **Nuevo**.

13. En hello **SAML Single Sign-On editar la configuración de** cuadro de diálogo, realizar Hola pasos:
    
    ![Inicio de sesión único SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Inicio de sesión único SAML")
    
    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración.

    b. En **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.

    c. Hola **Id. de entidad** cuadro de texto, tipo`https://salesforce-jobscience.com`

    d. Haga clic en **examinar** tooupload su certificado de Azure AD.

    e. Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**.

    f. Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.

    g. En **URL de inicio de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.

    h. En **URL de cierre de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.

    i. Haga clic en **Guardar**.

14. En el panel de navegación izquierdo de hello, Hola **administrar** sección, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello  **Mi dominio** página. 
    
    ![Mi dominio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Mi dominio")

15. En hello **mi dominio** página Hola **personalización de la página de inicio de sesión** sección, haga clic en **editar**.
    
    ![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Personalización de marca de página de inicio de sesión")

16. En hello **personalización de la página de inicio de sesión** página Hola **servicio de autenticación** sección, el nombre de Hola de su **configuración de SSO de SAML** se muestra. Selecciónelo y luego haga clic en **Save**(Guardar).
    
    ![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Personalización de marca de página de inicio de sesión")

17. Hola tooget SP iniciado por el inicio de sesión único en la dirección URL de inicio de sesión, haga clic en hello **configuración de inicio de sesión único** en hello **controles de seguridad** sección de menú.

    ![Controles de seguridad](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Controles de seguridad")
    
    Haga clic en el perfil SSO de Hola que haya creado en el paso de hello anterior. Esta página muestra hello inicio de sesión único en la dirección URL de su empresa (por ejemplo, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-jobscience-test-user"></a>Creación de un usuario de prueba de Jobscience

En orden tooenable toolog de los usuarios de Azure AD en tooJobscience, se les deben aprovisionar en Jobscience. En caso de hello de Jobscience, el aprovisionamiento es una tarea manual.

>[!NOTE]
>Puede usar cualquier otra Jobscience usuario cuenta herramienta de creación o las API proporcionadas por Jobscience tooprovision Azure Active Directory las cuentas de usuario.
>  
        
**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicie sesión en tooyour **Jobscience** como administrador.

2. Vaya tooSetup.
   
   ![Instalación](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Instalación")
3. Vaya demasiado**administrar usuarios \> usuarios**.
   
   ![Usuarios](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Usuarios")
4. Haga clic en **Nuevo usuario**.
   
   ![Todos los usuarios](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Todos los usuarios")
5. En hello **Editar usuario** cuadro de diálogo, realizar Hola pasos:
   
   ![Edición de usuario](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Edición de usuario")
   
   a. Hola **nombre** cuadro de texto, escriba un nombre de usuario de hello como Bárbara.
   
   b. Hola **Last Name** cuadro de texto, escriba los apellidos del usuario de hello como Simon.
   
   c. Hola **Alias** cuadro de texto, escriba un nombre de alias de usuario de hello como brittas.

   d. Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.

   e. Hola **nombre de usuario** cuadro de texto, escriba un nombre de usuario del usuario como Brittasimon@contoso.com.

   f. Hola **nombre Nick** cuadro de texto, escriba un nombre de nick del usuario como Simon.

   g. Haga clic en **Guardar**.

    
> [!NOTE]
> titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJobscience.

![Asignar usuario][200] 

**tooassign Britta Simon tooJobscience, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Jobscience**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Jobscience Hola Hola Panel de acceso, deberá obtener aplicaciones de Jobscience tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

