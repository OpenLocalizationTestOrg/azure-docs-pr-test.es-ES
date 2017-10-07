---
title: "Tutorial: Integración de Azure Active Directory con ScreenSteps | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Tutorial: Integración de Azure Active Directory con ScreenSteps

En este tutorial, aprenderá cómo toointegrate ScreenSteps con Azure Active Directory (Azure AD).

Integración ScreenSteps con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooScreenSteps.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooScreenSteps (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con ScreenSteps tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en ScreenSteps

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar ScreenSteps desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-screensteps-from-hello-gallery"></a>Agregar ScreenSteps desde la Galería de Hola
integración de hello tooconfigure de ScreenSteps en Azure AD, deberá tooadd ScreenSteps de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd ScreenSteps de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **ScreenSteps**, seleccione **ScreenSteps** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Lista de resultados de ScreenSteps Hola](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ScreenSteps con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ScreenSteps es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ScreenSteps debe toobe establecido.

En ScreenSteps, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con ScreenSteps, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de ScreenSteps](#create-a-screensteps-test-user)**  -toohave un equivalente de Britta Simon en ScreenSteps que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de ScreenSteps.

**inicio de sesión único en tooconfigure Azure AD con ScreenSteps, realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **ScreenSteps** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. En hello **ScreenSteps dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello Sign On URL real, que se explica más adelante en este tutorial. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. En hello **configuración de ScreenSteps** sección, haga clic en **configurar ScreenSteps** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. En otra ventana del explorador web, inicie sesión en su sitio de la compañía de ScreenSteps como administrador.

8. Haga clic en **Configuración de la cuenta**.

    ![Administración de cuentas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Administración de cuentas")

9. Haga clic en **Inicio de sesión único**.

    ![Autenticación remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticación remota")

10. Haga clic en **Crear punto de conexión de inicio de sesión único**.

    ![Autenticación remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticación remota")

11. Hola **extremo de inicio de sesión único crear** sección, lleve a cabo Hola pasos:

    ![Creación de un punto de conexión de autenticación](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Creación de un punto de conexión de autenticación")
    
    a. Hola **título** cuadro de texto, escriba un título.
    
    b. De hello **modo** lista, seleccione **SAML**.
    
    c. Haga clic en **Crear**.

12. **Editar** Hola nuevo punto de conexión.

    ![Editar punto de conexión](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Editar punto de conexión")

13. Hola **extremo de inicio de sesión único editar** sección, lleve a cabo Hola pasos:

    ![Punto de conexión de autenticación remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Punto de conexión de autenticación remota")

    a. Haga clic en **carga de nuevo el archivo de certificado SAML**y, a continuación, carga Hola certificado en el que ha descargado desde el portal de Azure.
    
    b. Pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión remoto** cuadro de texto.
    
    c. Pegar **dirección URL de cierre de sesión** valor, que haya copiado desde Hola portal de Azure en hello **Log out URL** cuadro de texto.
    
    d. Seleccione un **grupo** tooassign toowhen de los usuarios que los haya aprovisionado.
    
    e. Haga clic en **Update**(Actualizar).

    f. Hola copia **dirección URL del consumidor SAML** toohello Portapapeles y pegar en toohello **dirección URL de inicio de sesión** en el cuadro de texto **ScreenSteps dominio y las direcciones URL** sección.
    
    g. Devolver toohello **extremo de inicio de sesión único editar**.
    
    h. Haga clic en hello **Predeterminar para cuenta** botón toouse este punto de conexión para todos los usuarios que inician sesión en ScreenSteps. Como alternativa, puede hacer clic en hello **agregar tooSite** botón toouse este punto de conexión para sitios específicos de **ScreenSteps**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-a-screensteps-test-user"></a>Creación de un usuario de prueba de ScreenSteps

En esta sección, creará un usuario llamado Britta Simon en ScreenSteps. Trabajar con [equipo de soporte técnico de ScreenSteps cliente](https://www.screensteps.com/contact) para agregar usuarios de hello en la plataforma de ScreenSteps Hola. Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único. 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooScreenSteps.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooScreenSteps, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ScreenSteps**.

    ![vínculo de ScreenSteps Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello ScreenSteps disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour ScreenSteps aplicación.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

