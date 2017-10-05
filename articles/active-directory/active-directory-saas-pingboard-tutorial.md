---
title: "Tutorial: Integración de Azure Active Directory con Pingboard | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Tutorial: Integración de Azure Active Directory con Pingboard

En este tutorial, aprenderá a integrar Pingboard con Azure Active Directory (Azure AD).

La integración de Pingboard con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Pingboard.
- Puede permitir que los usuarios inicien sesión automáticamente en Pingboard (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.

Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Pingboard, se necesitan los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción a Pingboard habilitada para inicio de sesión único

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. La situación descrita en este tutorial consta de dos bloques de creación principales:

1. Agregar Pingboard desde la galería
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-pingboard-from-the-gallery"></a>Agregar Pingboard desde la galería
Para configurar la integración de Pingboard en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Pingboard desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

2. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda, escriba En el cuadro de búsqueda, escriba **Pingboard**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. En el panel de resultados, seleccione **Pingboard** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pingboard con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Pingboard para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Pingboard.

Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Pingboard.

Para configurar y probar el inicio de sesión único de Azure AD con Pingboard, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
2. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
3. **[Creación de un usuario de prueba de Pingboard](#creating-a-pingboard-test-user)**: para tener un homólogo de Britta Simon en Pingboard que esté vinculado a la representación de ella en Azure AD.
4. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Pingboard.

**Para configurar el inicio de sesión único de Azure AD con Pingboard, realice los pasos siguientes:**

1. En el Portal de administración de Azure, en la página de integración de aplicaciones de **Pingboard**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. En la sección **Dominio y direcciones URL de Pingboard**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. En el cuadro de texto **Identificador**, escriba el valor como `http://<entity-id>.pingboard.com/sp`.

    b. En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<entity-id>.pingboard.com/auth/saml/consume`.

    > [!NOTE] 
    > Tenga en cuenta que estos no son valores reales. Estos valores se tienen que actualizar con los valores reales de Identificador y URL de respuesta. Aquí le recomendamos que utilice el valor de cadena único en el identificador. Póngase en contacto con el [equipo de soporte técnico de Pingboard](https://support.pingboard.com/) para obtener estos valores. 

4. Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. En el cuadro de texto **URL de inicio de sesión**, escriba el valor como: `http://<sub-domain>.pingboard.com/sign_in`
     
5. En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. Para configurar SSO en Pingboard, abra una nueva ventana del explorador e inicie sesión en su cuenta de Pingboard. Debe ser un administrador de Pingboard para configurar el inicio de sesión único.

8. En el menú superior, seleccione **Aplicaciones > Integraciones**

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  En la página **Integraciones**, busque el icono **"Azure Active Directory"** y haga clic en él.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. En el estado modal que sigue, haga clic en **"Configurar"**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. En la siguiente página, observará que la "integración de Azure SSO está habilitada". Abra el archivo XML de metadatos descargado en el Bloc de notas y pegue el contenido en **metadatos de IDP**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. El archivo se validará y, si todo está correcto, se habilitará el inicio de sesión único.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-pingboard-test-user"></a>Creación de un usuario de prueba de Pingboard

Para permitir que los usuarios de Azure AD inicien sesión en Pingboard, tienen que aprovisionarse en Pingboard.  
En el caso de Pingboard, el aprovisionamiento es una tarea manual.

**Para aprovisionar cuentas de usuario, realice estos pasos:**

1. Inicie sesión en el sitio de la compañía Pingboard como administrador.

2. Haga clic en el botón **“Add Employee”** (Agregar empleado) en la página **Directory** (Directorio).

    ![Agregar empleado](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. En la página del cuadro de diálogo **"Add Employee"** (Agregar empleado), realice los siguientes pasos.

    ![Invitar a contactos](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. En el cuadro de texto **Nombre completo**, escriba el nombre completo de Britta Simon.

    b. En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de la cuenta de Britta Simon.

    c. En el cuadro de texto **Puesto**, escriba el puesto de Britta Simon.

    d. En la lista desplegable **Ubicación**, seleccione la ubicación de Britta Simon.
    
    e. Haga clic en **Agregar**.   

4. Se muestra una pantalla de confirmación para confirmar la adición del usuario.
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Pingboard.

![Asignar usuario][200] 

**Para asignar a Britta Simon a Pingboard, realice los pasos siguientes:**

1. En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).

    ![Asignar usuario][201] 

2. En la lista de aplicaciones, seleccione **Pingboard**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de Pingboard en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Pingboard.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
