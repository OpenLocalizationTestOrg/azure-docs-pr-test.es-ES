---
title: "Tutorial: Integración de Azure Active Directory con Pagerduty | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Tutorial: Integración de Azure Active Directory con Pagerduty

En este tutorial, aprenderá cómo toointegrate PagerDuty con Azure Active Directory (Azure AD).

Integración PagerDuty con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooPagerDuty
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPagerDuty (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con PagerDuty tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en PagerDuty

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar PagerDuty desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-pagerduty-from-hello-gallery"></a>Agregar PagerDuty desde la Galería de Hola
integración de hello tooconfigure de PagerDuty en Azure AD, deberá tooadd PagerDuty de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd PagerDuty de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **PagerDuty**, seleccione **PagerDuty** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PagerDuty con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PagerDuty es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PagerDuty debe toobe establecido.

En PagerDuty, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con PagerDuty, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de PagerDuty](#create-a-pagerduty-test-user)**  -toohave un equivalente de Britta Simon en PagerDuty que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de PagerDuty.

**inicio de sesión único en tooconfigure Azure AD con PagerDuty, realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **PagerDuty** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. En hello **PagerDuty dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.pagerduty.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de PagerDuty](https://www.pagerduty.com/support/) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. En hello **configuración de PagerDuty** sección, haga clic en **configurar PagerDuty** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. En otra ventana del explorador web, inicie sesión en el sitio de la compañía Pagerduty como administrador.

8. En el menú de hello en la parte superior de hello, haga clic en **configuración de la cuenta**.
   
    ![Configuración de la cuenta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "configuración de la cuenta")

9. Haga clic en **Inicio de sesión único**.
   
    ![Inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Inicio de sesión único")

10. En hello **habilitar inicio de sesión único (SSO)** , siga los pasos de hello:
   
    ![Habilitar inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Habilitar inicio de sesión único")
   
    a. Abra el certificado codificado en base 64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto
  
    b. Hola **dirección URL de inicio de sesión** cuadro de texto, pegue **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.
  
    c. Hola **Logout URL** cuadro de texto, pegue **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.
 
    d. Seleccione **Activar inicio de sesión único**.
 
    e. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![botón de agregar Hola](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="create-a-pagerduty-test-user"></a>Creación de un usuario de prueba de PagerDuty

toolog de los usuarios de Azure AD tooenable en tooPagerDuty, se les deben aprovisionar en PagerDuty.  
En caso de hello de PagerDuty, el aprovisionamiento es una tarea manual.

>[!NOTE]
>Puede usar cualquier otra Pagerduty usuario cuenta herramienta de creación o las API proporcionadas por Pagerduty tooprovision Azure Active Directory las cuentas de usuario.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **Pagerduty** inquilino.

2. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.

3. Haga clic en **Agregar usuarios**.
   
    ![Agregar usuarios](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Agregar usuarios")

4.  En hello **invite a su equipo** cuadro de diálogo, realizar Hola pasos:
   
    ![Invite your team (Invitar a su equipo)](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team (Invitar a su equipo)")

    a. Hola de tipo **nombre y apellido** del usuario como **Britta Simon**. 
   
    b. Escriba el **Email** (correo electrónico) del usuario, por ejemplo **brittasimon@contoso.com**.
   
    c. Haga clic en **Add** (Agregar) y después en **Send Invites** (Enviar invitaciones).
   
    >[!NOTE]
    >Todos los usuarios agregados recibirán una toocreate invitar a una cuenta de PagerDuty.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPagerDuty.

![Asigne el rol de usuario de Hola][200]

**tooassign Britta Simon tooPagerDuty, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **PagerDuty**.

    ![vínculo de PagerDuty Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de PagerDuty Hola Hola acceso Panelyou debería obtener automáticamente ha iniciado sesión tooyour PagerDuty aplicación.

Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

