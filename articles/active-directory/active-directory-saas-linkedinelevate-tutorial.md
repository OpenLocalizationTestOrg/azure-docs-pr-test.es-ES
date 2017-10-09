---
title: "Tutorial: Integración de Azure Active Directory con LinkedIn Elevate | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y elevar LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Tutorial: Integración de Azure Active Directory con LinkedIn Elevate

En este tutorial, aprenderá cómo elevar los toointegrate LinkedIn con Azure Active Directory (Azure AD).

Integración elevar LinkedIn con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooLinkedIn elevar
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLinkedIn elevar (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con elevar LinkedIn, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en LinkedIn Elevate

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar LinkedIn elevar desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>Agregar LinkedIn elevar desde la Galería de Hola
integración de hello tooconfigure de LinkedIn elevar en Azure AD, deberá tooadd LinkedIn elevar de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd LinkedIn elevar el nivel de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **LinkedIn elevar**. En el panel de resultados, haga clic en **LinkedIn elevar** aplicación de hello tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con LinkedIn Elevate utilizando usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en elevar LinkedIn es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LinkedIn elevar debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en LinkedIn elevar sus privilegios.

tooconfigure y prueba de inicio de sesión único en Azure AD con elevar LinkedIn, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba LinkedIn elevar](#creating-a-linkedin-elevate-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación LinkedIn elevar sus privilegios.

**inicio de sesión único en tooconfigure Azure AD con elevar LinkedIn, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **LinkedIn elevar** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. En una ventana del explorador web diferente, inicio de sesión tooyour LinkedIn elevar inquilino como administrador.

4. En **Account Center** (Centro de cuentas), haga clic en **Global Settings** (Configuración global) en **Settings** (Configuración). Además, seleccione **elevar - elevar prueba de AAD** de lista desplegable de Hola.

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Haga clic en **o haga clic aquí tooload y copie los campos individuales de formulario de hello** y copie **Id. de entidad** y **dirección Url de acceso de consumidor de aserción (ACS)**

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. En el Portal de Azure, en **LinkedIn elevar dominio y las direcciones URL**, realizar Hola siguientes pasos si desea tooconfigure SSO en **iniciado por IdP** modo

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. Hola **identificador** cuadro de texto, escriba Hola **Id. de entidad** copiados desde el LinkedIn Portal 

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba Hola **dirección Url de acceso de consumidor de aserción (ACS)** copiados desde el LinkedIn Portal

7. Si desea que tooconfigure SSO en **iniciado en SP**, a continuación, haga clic en la opción Mostrar URL avanzada en la sección de configuración de Hola y configurar inicio de sesión de hello en dirección URL con hello siguiente patrón:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. La aplicación LinkedIn elevar espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto. Hola valor predeterminado de **identificador de usuario** es **user.userprincipalname** pero LinkedIn elevar espera este toobe asignado con la dirección de correo electrónico del usuario de Hola. Para que puede usar **user.mail** de atributo de la lista de Hola o usar el valor de atributo apropiado de hello según la configuración de la organización. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola. Necesita tooadd otra notificación denominado **departamento** y valor de hello debe toobe asignado demasiado**user.department**.

    | Nombre del atributo | Valor de atributo |
    | --- | --- |    
    | department| user.department |

      ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. Haga clic en la página de detalles de atributo de Agregar atributo tooopen Hola Agregar atributo de departamento Hola tal como se muestra a continuación:

      ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Haga clic en **Aceptar** atributo de hello toosave.

      c. Cambiar el nombre del atributo de Hola Hola **emailaddress** demasiado**correo electrónico**.


10. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. Haga clic en **Guardar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Vaya demasiado**configuración de administración de LinkedIn** sección. Cargar archivo XML de Hola que acaba de descargar de hello portal de Azure haciendo clic en hello opción de archivo de cargar XML.

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Haga clic en **en** tooenable SSO. Estado SSO cambiará de **no conectado** demasiado**conectado**

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Creación de un usuario de prueba de LinkedIn Elevate

Aplicación de elevar vinculado admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente. Página de configuración de administración de hello en el conmutador de hello LinkedIn elevar Hola voltear portal **asignar automáticamente licencias** tooactive tooenable sólo en tiempo de aprovisionamiento y esto también asignarán a un usuario de toohello licencia.

   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooLinkedIn acceso elevar.

![Asignar usuario][200] 

**tooassign Britta Simon tooLinkedIn elevar, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **LinkedIn elevar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de LinkedIn elevar Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión Azure hello y en después de la sesión correctamente, deberá obtener en la aplicación LinkedIn elevar sus privilegios.

## <a name="additional-resources"></a>Recursos adicionales

* [Tutorial: configuración de LinkedIn Elevate para el aprovisionamiento automático de usuarios con Azure Active Directory](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
