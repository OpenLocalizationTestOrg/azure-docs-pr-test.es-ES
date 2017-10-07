---
title: "Tutorial: integración de Azure Active Directory con ClickTime | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Tutorial: integración de Azure Active Directory con ClickTime

En este tutorial, aprenderá cómo toointegrate ClickTime con Azure Active Directory (Azure AD).

Integración de ClickTime con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooClickTime
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooClickTime (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con ClickTime tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en ClickTime

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar ClickTime desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-clicktime-from-hello-gallery"></a>Agregar ClickTime desde la Galería de Hola
integración de hello tooconfigure de ClickTime en Azure AD, deberá tooadd ClickTime de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd ClickTime de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **ClickTime**, seleccione **ClickTime** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Lista de resultados de ClickTime Hola](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ClickTime con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ClickTime es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ClickTime debe toobe establecido.

En ClickTime, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con ClickTime, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de ClickTime](#create-a-clicktime-test-user)**  -toohave un equivalente de Britta Simon en ClickTime que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de ClickTime.

**inicio de sesión único en tooconfigure Azure AD con ClickTime, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **ClickTime** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. En hello **ClickTime dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información sobre dominio y direcciones URL de inicio de sesión único de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL como:`https://app.clicktime.com/sp/`
    
    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello siguiendo patrones: 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. En hello **configuración de ClickTime** sección, haga clic en **configurar ClickTime** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de ClickTime como administrador.

8. En la barra de herramientas de hello en la parte superior de hello, haga clic en **preferencias**y, a continuación, haga clic en **configuración de seguridad**.

9. Hola **preferencias de inicio de sesión único** configuración sección, lleve a cabo Hola pasos:
   
    ![Configuración de seguridad](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Configuración de seguridad")
   
    a.  Seleccione **Allow** sign-in using Single Sign-On (SSO) with **Azure AD** [Permitir inicio de sesión mediante inicio de sesión único (SSO) con Azure AD].
   
    b. Hola **extremo del proveedor de identidad** cuadro de texto, pegue **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.
   
    c.  Abra hello **certificado codificado en base 64** descargado desde el portal de Azure en **el Bloc de notas**, copiar el contenido de hello y, a continuación, péguelo en hello **certificado X.509** cuadro de texto.
   
    d.  Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.
 
    ![botón de agregar Hola](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="create-a-clicktime-test-user"></a>Creación de un usuario de prueba de ClickTime

En orden tooenable toolog de los usuarios de Azure AD en ClickTime, se les deben aprovisionar en ClickTime.  
En caso de hello de ClickTime, el aprovisionamiento es una tarea manual.

> [!NOTE]
> Puede usar cualquier otra ClickTime usuario cuenta herramienta de creación o las API proporcionadas por ClickTime tooprovision cuentas de usuario de Azure AD.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**
1. Inicie sesión en tooyour **ClickTime** inquilino.
2. En la barra de herramientas de hello en la parte superior de hello, haga clic en **empresa**y, a continuación, haga clic en **personas**.
   
    ![Personas](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Personas")
3. Haga clic en **Add Person**(Agregar persona).
   
    ![Agregar persona](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Agregar persona")
4. Hola sección nueva persona, realice Hola pasos:
   
    ![Personas](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Personas")
   
    a.  Hola **nombre completo** cuadro de texto, tipo de nombre completo del usuario como **Britta Simon**. 
  
    b.  Hola **dirección de correo electrónico** Hola de tipo de correo electrónico del usuario, cuadro de texto, como  **brittasimon@contoso.com** .
       
    > [!NOTE]
    > Si desea, puede establecer propiedades adicionales del objeto de hello nueva persona.
   
    c.  Haga clic en **Guardar**.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooClickTime.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooClickTime, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ClickTime**.

    ![Vínculo de ClickTimne en la lista de aplicaciones de Hola](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de ClickTime Hola Hola Panel de acceso, deberá obtener aplicaciones de ClickTime tooyour automáticamente ha iniciado sesión.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

