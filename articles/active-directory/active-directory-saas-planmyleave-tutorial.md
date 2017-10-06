---
title: "Tutorial: integración de Azure Active Directory con PlanMyLeave | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Tutorial: Integración de Azure Active Directory con PlanMyLeave

En este tutorial, aprenderá cómo toointegrate PlanMyLeave con Azure Active Directory (Azure AD).

Integración PlanMyLeave con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooPlanMyLeave
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPlanMyLeave (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con PlanMyLeave tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en PlanMyLeave


> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar PlanMyLeave desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-planmyleave-from-hello-gallery"></a>Agregar PlanMyLeave desde la Galería de Hola
integración de hello tooconfigure de PlanMyLeave en Azure AD, deberá tooadd PlanMyLeave de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd PlanMyLeave de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **PlanMyLeave**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. En el panel de resultados de hello, seleccione **PlanMyLeave**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PlanMyLeave con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PlanMyLeave es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PlanMyLeave debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en PlanMyLeave.

tooconfigure y prueba de inicio de sesión único en Azure AD con PlanMyLeave, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave un equivalente de Britta Simon en PlanMyLeave que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación PlanMyLeave.

**inicio de sesión único en Azure AD tooconfigure con PlanMyLeave, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **PlanMyLeave** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** página del cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. En hello **PlanMyLeave dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tendrá que tooupdate estos valores con hello real iniciar sesión en la dirección URL y el identificador. Póngase en contacto con [equipo de soporte técnico de PlanMyLeave](mailto:support@planmyleave.com) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**. Luego haga clic en el botón **Guardar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. En hello **PlanMyLeave configuración** sección, haga clic en **configurar PlanMyLeave** tooopen **configurar inicio de sesión** ventana.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. En otra ventana del explorador web, inicie sesión en como administrador en el inquilino de PlanMyLeave.

11. Vaya demasiado**el programa de instalación de sistema**. A continuación, en hello **administración de seguridad** sección, haga clic **configuración de SAML de la empresa** .

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. En hello **configuración SAML** sección, haga clic en el icono de editor.

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. En hello **configuración de SAML de actualización** sección, lleve a cabo Hola pasos:

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  Hola **dirección URL de inicio de sesión** cuadro de texto, coloque valor Hola de **SAML Single Sign-On dirección URL del servicio** desde la ventana de configuración de aplicación de Azure AD.

    b.  Abra el archivo de certificado descargado en el Bloc de notas, copie solo Hola contenido entre Hola---Begin Certificate---y---End certificate---del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado** cuadro de texto.

    c. Establecer"**está habilitado**"demasiado"**Sí**".

    d. Haga clic en **Guardar**.



### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 



### <a name="creating-a-planmyleave-test-user"></a>Crear un usuario de prueba de PlanMyLeave

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en PlanMyLeave toocreate. PlanMyLeave admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

No hay ningún elemento de acción para usted en esta sección. Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento PlanMyLeave.

> [!NOTE]
> Si necesita un usuario toocreate manualmente, necesita toocontact [equipo de soporte técnico de PlanMyLeave](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooPlanMyLeave de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooPlanMyLeave, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **PlanMyLeave**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    


### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de PlanMyLeave Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour PlanMyLeave aplicación.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png