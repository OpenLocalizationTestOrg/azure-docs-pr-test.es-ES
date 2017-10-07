---
title: "Tutorial: Integración de Azure Active Directory con Work.com | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Tutorial: Integración de Azure Active Directory con Work.com

En este tutorial, aprenderá cómo toointegrate Work.com con Azure Active Directory (Azure AD).

Integración Work.com con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooWork.com
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWork.com (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Work.com tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Work.com

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Work.com de galería de Hola
2. Configuración y prueba del inicio de sesión único en Azure AD

## <a name="add-workcom-from-hello-gallery"></a>Agregar Work.com de galería de Hola
integración de hello tooconfigure de Work.com en Azure AD, deberá tooadd Work.com de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Work.com de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Work.com**, seleccione **Work.com** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Incorporación desde la galería](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Work.com con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Work.com es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Work.com debe toobe establecido.

En Work.com, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Work.com, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Work.com](#create-a-workcom-test-user)**  -toohave un equivalente de Britta Simon en Work.com que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Work.com.

>[!NOTE]
>tooconfigure inicio de sesión único, es necesario un nombre de dominio personalizado de Work.com toosetup aún. Necesita toodefine al menos un dominio nombre, el nombre de dominio de prueba e impleméntelo tooyour toda la organización.

**inicio de sesión único en Azure AD tooconfigure con Work.com, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Work.com** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. En hello **Work.com dominio y las direcciones URL** sección, realice Hola siguiente:

    ![Sección Dominio y direcciones URL de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<companyname>.my.salesforce.com`

    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de cliente de Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget este valor. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Sección Certificado de firma SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. En hello **configuración de Work.com** sección, haga clic en **configurar Work.com** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Sección de configuración de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. Inicie sesión en tooyour inquilino de Work.com como administrador.

8. Vaya demasiado**el programa de instalación**.
   
    ![Instalación](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalación")

9. En el panel de navegación izquierdo de hello, Hola **administrar** sección, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello  **Mi dominio** página. 
   
    ![Mi dominio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Mi dominio")

10. tooverify que el dominio se ha configurado correctamente, asegúrese de que se encuentra en "**paso 4 implementado tooUsers**" y revise el "**mi configuración de dominio**".
   
    ![Dominio implementado tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser implementadas de dominio")

11. Inicie sesión en tooyour inquilino de Work.com.

12. Vaya demasiado**el programa de instalación**.
    
    ![Instalación](./media/active-directory-saas-work-com-tutorial/ic794108.png "Instalación")

13. Expanda hello **controles de seguridad** menú y, a continuación, haga clic en **configuración de inicio de sesión único**.
    
    ![Configuración de inicio de sesión único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configuración de inicio de sesión único")

14. En hello **configuración de inicio de sesión único** cuadro de diálogo, siga los pasos de hello:
    
    ![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")
    
    a. Seleccione **SAML habilitado**.
    
    b. Haga clic en **Nuevo**.

15. Hola **configuración de inicio de sesión único de SAML** sección, lleve a cabo Hola pasos:
    
    ![Inicio de sesión único SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Inicio de sesión único SAML")
    
    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración.  
       
    > [!NOTE]
    > Proporciona un valor para **nombre** rellenar automáticamente hello **nombre de la API** cuadro de texto.
    
    b. En **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.
    
    c. tooupload Hola Descargar certificado desde el portal de Azure, haga clic en **examinar**.
    
    d. Hola **Id. de entidad** cuadro de texto, tipo `https://salesforce-work.com`.
    
    e. Como **tipo de identidad SAML**, seleccione **la aserción contiene Hola Id. de federación del objeto de usuario de hello**.
    
    f. Como **ubicación de identidad SAML**, seleccione **identidad está en el elemento NameIdentifier de Hola de hello instrucción Subject**.
    
    g. En **URL de inicio de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.

    h. En **URL de cierre de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.
    
    i. Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP Post** (Método HTTP Post).
    
    j. Haga clic en **Guardar**.

16. En el portal clásico de Work.com, en el panel de navegación izquierdo de hello, haga clic en **Domain Management** tooexpand Hola sección relacionada y, a continuación, haga clic en **mi dominio** tooopen hello **mi dominio**página. 
    
    ![Mi dominio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Mi dominio")

17. En hello **mi dominio** página Hola **personalización de la página de inicio de sesión** sección, haga clic en **editar**.
    
    ![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-work-com-tutorial/ic767826.png "Personalización de marca de página de inicio de sesión")

14. En hello **personalización de la página de inicio de sesión** página Hola **servicio de autenticación** sección, el nombre de Hola de su **configuración de SSO de SAML** se muestra. Selecciónelo y luego haga clic en **Save**(Guardar).
    
    ![Personalización de marca de página de inicio de sesión](./media/active-directory-saas-work-com-tutorial/ic784366.png "Personalización de marca de página de inicio de sesión")

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Usuarios y grupos -> Todos los usuarios](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Sumar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="create-a-workcom-test-user"></a>Creación de un usuario de prueba de Work.com
Para Azure Active Directory a los usuarios toobe puede toosign en, deben ser tooWork.com aprovisionado. En caso de hello de Work.com, el aprovisionamiento es una tarea manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamiento de usuario, realizar Hola pasos:
1. Inicie sesión en tooyour sitio de empresa de Work.com como administrador.

2. Vaya demasiado**el programa de instalación**.
   
    ![Instalación](./media/active-directory-saas-work-com-tutorial/IC794108.png "Instalación")
3. Vaya demasiado**administrar usuarios \> usuarios**.
   
    ![Administración de usuarios](./media/active-directory-saas-work-com-tutorial/IC784369.png "Administración de usuarios")

4. Haga clic en **Nuevo usuario**.
   
    ![Todos los usuarios](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos los usuarios")

5. En la sección Editar usuarios hello, realizar Hola siguiendo los pasos, en los atributos de un Azure válida cuadros de texto relacionados con la cuenta de AD que quiera tooprovision en hello:
   
    ![Edición de usuario](./media/active-directory-saas-work-com-tutorial/ic794118.png "Edición de usuario")
   
    a. Hola **nombre** cuadro de texto, hello tipo **nombre** del usuario de hello **Bárbara**.
    
    b. Hola **Last Name** cuadro de texto, hello tipo **apellidos** del usuario de hello **Simon**.
    
    c. Hola **Alias** cuadro de texto, hello tipo **nombre** del usuario de hello **BrittaS**.
    
    d. Hola **correo electrónico** cuadro de texto, hello tipo **dirección de correo electrónico** del usuario  **Brittasimon@contoso.com** .
    
    e. Hola **nombre de usuario** cuadro de texto, escriba un nombre de usuario del usuario como  **Brittasimon@contoso.com** .
    
    f. Hola **nombre Nick** cuadro de texto, escriba un **nombre nick** del usuario **Simon**.
    
    g. Seleccione **Role** (Rol), **User License** (Licencia de usuario) y **Profile** (Perfil).
    
    h. Haga clic en **Guardar**.  
      
    > [!NOTE]
    > titular de cuenta de Hello Azure AD recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWork.com.

![Asignar usuario][200] 

**tooassign Britta Simon tooWork.com, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Work.com**.

    ![Work.com en la lista de la aplicación](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Work.com Hola Hola Panel de acceso, deberá obtener aplicaciones de Work.com tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

