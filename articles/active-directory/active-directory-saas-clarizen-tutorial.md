---
title: "Tutorial: integración de Azure Active Directory con Clarizen | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Clarizen."
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
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Tutorial: integración de Azure Active Directory con Clarizen

En este tutorial, aprenderá cómo toointegrate Azure Active Directory (Azure AD) con Clarizen. Esto proporciona integración Hola siguientes ventajas:

- Puede controlar, en Azure AD, que tiene acceso tooClarizen.
- Puede habilitar la toobe usuarios tooClarizen (inicio de sesión único) con sus cuentas de Azure AD inicia sesión automáticamente.
- Puede administrar las cuentas en una ubicación central, Hola portal de Azure.

escenario de Hello en este tutorial consta de dos tareas principales:

1. Agregar Clarizen de hello Galería.
2. Configuración y prueba del inicio de sesión único en Azure AD.

Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con Clarizen tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción de Clarizen con inicio de sesión único habilitado

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- Pruebe el inicio de sesión único de Azure AD en un entorno de prueba. No use su entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Agregar Clarizen de galería de Hola
integración de hello tooconfigure de Clarizen en Azure AD, agregue Clarizen de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, haga clic en hello **Azure Active Directory** icono.

    ![Icono de Azure Active Directory][1]

2. Haga clic en **Aplicaciones empresariales**. A continuación, haga clic en **Todas las aplicaciones**.

    ![Clic en "Aplicaciones empresariales" y "Todas las aplicaciones"][2]

3. Haga clic en hello **agregar** situado en la parte superior de Hola Hola del cuadro de diálogo.

    ![botón de "Agregar" Hello][3]

4. En el cuadro de búsqueda de hello, escriba **Clarizen**.

    ![Escriba "Clarizen" en el cuadro de búsqueda de Hola](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. En el panel de resultados de hello, seleccione **Clarizen**y, a continuación, haga clic en **agregar** aplicación de hello tooadd.

    ![Seleccionar Clarizen en el panel de resultados de Hola](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En las secciones siguientes de hello, configurar y probar el inicio de sesión único en Azure AD con Clarizen en función de usuario de prueba de hello Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Clarizen es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Clarizen debe toobe establecido. Establecer esta relación de vínculo asignando el valor de Hola de **nombre de usuario** en Azure AD como valor de Hola de **nombre de usuario** en Clarizen.

tooconfigure y prueba de inicio de sesión único en Azure AD con Clarizen, Hola completa después de bloques de creación:

1. **[Configurar inicio de sesión único en Azure AD](#configure-azure-ad-single-sign-on)**  tooenable su toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  tootest inicio de sesión único en Azure AD con Britta Simon.
3. **[Crear un usuario de prueba de Clarizen](#create-a-clarizen-test-user)**  toohave un equivalente de Britta Simon en Clarizen que está vinculado toohello Azure AD representación de ella.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD
Habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Clarizen.

1. En el portal de Azure, en Hola Hola **Clarizen** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Clic en "Inicio de sesión único"][4]

2. Hola **inicio de sesión único** cuadro de diálogo para **modo**, seleccione **sesión basado en SAML** tooenable inicio de sesión único.

    ![Selección de "Inicio de sesión basado en SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. Hola **Clarizen dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Cuadros de identificador y dirección URL de respuesta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. Hola **identificador** cuadro de valor de tipo hello como: **Clarizen**

    b. Hola **dirección URL de respuesta** , escriba una dirección URL mediante el uso de hello siguiente patrón: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Estas no son valores reales de Hola. Ha identificador real de toouse hello y dirección URL de respuesta. Aquí se recomienda usar valor de una cadena única de hello como Hola identificador. tooget Hola valores reales, póngase en contacto con hello [equipo de soporte técnico de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).

4. En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.

    ![Clic en "Crear un nuevo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. Hola **crear nuevo certificado** diálogo cuadro, haga clic en el icono del calendario de Hola y seleccione una fecha de expiración. A continuación, haga clic en **Guardar**.

    ![Seleccionar y guardar una fecha de expiración](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. Hola **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado**y, a continuación, haga clic en **guardar**.

    ![Activar casilla de verificación de Hola para hacer que el nuevo certificado de hello active](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. Hola **el certificado de sustitución** cuadro de diálogo, haga clic en **Aceptar**.

    ![Al hacer clic en "Aceptar" tooconfirm que desea toomake Hola certificado activo](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. Hola **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Haga clic en descarga de hello toostart "Certificado (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. Hola **configuración de Clarizen** sección, haga clic en **configurar Clarizen** tooopen hello **configurar inicio de sesión** ventana.

    ![Clic en "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Ventana "Configurar inicio de sesión", incluidos los archivos y las direcciones URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía Clarizen tooyour como administrador.

11. Haga clic en el nombre de usuario y luego haga clic en **Settings** (Configuración).

    ![Clic en "Settings" (Configuración) debajo del nombre de usuario](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Configuración")

12. Haga clic en hello **configuración Global** ficha. A continuación, siguiente demasiado**autenticación federada**, haga clic en **editar**.

    ![Pestaña "Global Settings"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")

13. Hola **autenticación federada** diálogo cuadro, lleve a cabo Hola pasos:

    ![Cuadro de diálogo "Federated Authentication"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")

    a. Seleccione **Habilitar autenticación federada**.

    b. Haga clic en **cargar** tooupload el certificado descargado.

    c. Hola **dirección URL de inicio de sesión** cuadro, escriba el valor de Hola de **SAML Single Sign-On dirección URL del servicio** desde la ventana de configuración de aplicación hello Azure AD.

    d. Hola **dirección URL de cierre de sesión** cuadro, escriba el valor de Hola de **dirección URL de cierre de sesión** desde la ventana de configuración de aplicación hello Azure AD.

    e. Seleccione **Usar POST**.

    f. Haga clic en **Guardar**.

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
Hola portal de Azure, cree un usuario de prueba llamado a Britta Simon.

![Nombre y direcciones de correo del usuario de prueba de hello Azure AD][100]

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** icono.

    ![Icono de Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Haga clic en **usuarios y grupos**y, a continuación, haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.

    ![Clic en "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. En la parte superior de Hola Hola del cuadro de diálogo, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.

    ![botón de "Agregar" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![Cuadro de diálogo "Usuario" con los campos nombre, dirección de correo electrónico y contraseña cumplimentados](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello de hello cuenta Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de **contraseña**.

    d. Haga clic en **Create**(Crear).

### <a name="create-a-clarizen-test-user"></a>Creación de un usuario de prueba de Clarizen
tooenable toosign de los usuarios de Azure AD en tooClarizen, debe aprovisionar las cuentas de usuario. En caso de hello de Clarizen, el aprovisionamiento es una tarea manual.

1. Inicie sesión en tooyour Clarizen sitio de su compañía como administrador.

2. Haga clic en **Contactos**.

    ![Clic en "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")

3. Haga clic en **Invitar a usuario**.

    ![Botón "Invite User"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")

4. Hola **invitar personas** diálogo cuadro, lleve a cabo Hola pasos:

    ![Cuadro de diálogo "Invite People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")

    a. Hola **correo electrónico** cuadro de dirección de correo electrónico de tipo hello de hello cuenta Britta Simon.

    b. Haga clic en **Invitar**.

    > [!NOTE]
    > titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD
Habilitar Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooClarizen de acceso.

![Usuario de prueba asignado][200]

1. Hola portal de Azure, abrir vista de aplicaciones de hello, examinar vista del directorio toohello, haga clic en **aplicaciones empresariales**y, a continuación, haga clic en **todas las aplicaciones**.

    ![Clic en "Aplicaciones empresariales" y "Todas las aplicaciones"][201]

2. En la lista de aplicaciones de hello, seleccione **Clarizen**.

    ![Al seleccionar Clarizen en lista de Hola](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. En el panel izquierdo de hello, haga clic en **usuarios y grupos**.

    ![Clic en "Usuarios y grupos"][202]

4. Haga clic en hello **agregar** botón. A continuación, en hello **Agregar asignación** cuadro de diálogo, seleccione **usuarios y grupos**.

    ![botón de "Agregar" Hello y cuadro de diálogo "Agregar asignación" hello][203]

5. Hola **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en lista de Hola de usuarios.

6. Hola **usuarios y grupos** diálogo cuadro, haga clic en hello **seleccione** botón.

7. Hola **Agregar asignación** diálogo cuadro, haga clic en hello **asignar** botón.

### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único
Probar la configuración de inicio de sesión única de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de Clarizen Hola Hola Panel de acceso, debería firmar automáticamente en tooyour aplicación Clarizen.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
