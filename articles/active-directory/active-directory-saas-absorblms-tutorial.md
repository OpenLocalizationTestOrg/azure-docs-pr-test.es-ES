---
title: "Tutorial: Integración de Azure Active Directory con Absorb LMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y absorber LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Tutorial: Integración de Azure Active Directory con Absorb LMS

En este tutorial, aprenderá cómo toointegrate absorber LMS con Azure Active Directory (Azure AD).

Integración absorber LMS con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooAbsorb LMS
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAbsorb LMS (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte. [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con LMS absorber tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Absorb LMS

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar absorber LMS desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-absorb-lms-from-hello-gallery"></a>Agregar absorber LMS desde la Galería de Hola
integración de hello tooconfigure de absorber LMS en tooAzure AD, deberá tooadd absorber LMS de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd absorber LMS de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **absorber LMS**, seleccione **absorber LMS** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Absorber LMS en la lista de resultados de Hola](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Absorb LMS con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LMS absorber es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LMS absorber debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en absorber LMS.

tooconfigure y prueba de inicio de sesión único en Azure AD con LMS absorber, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de absorber LMS](#create-an-absorb-lms-test-user)**  -toohave un equivalente de Britta Simon en LMS absorber que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de absorber LMS.

**inicio de sesión único en tooconfigure Azure AD con LMS absorber, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **absorber LMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. En hello **absorber LMS dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Estos valores no son Hola real. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico de absorber LMS cliente](https://www.absorblms.com/support) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. En hello **absorber la configuración de LMS** sección, haga clic en **configurar LMS absorber** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía absorber LMS tooyour como administrador.

9. Haga clic en hello **icono de cuenta** en la interfaz de administración de Hola. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Haga clic en **Portal Settings** (Configuración del portal).

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Haga clic en hello **usuarios** ficha.

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Lleve a cabo Hola siguiendo los pasos tooaccess Hola Single Sign-On campos de la configuración:

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Seleccione Hola adecuado **modo**.

    b. Hola abierto certificado que ha descargado de hello portal de Azure en el Bloc de notas, quite hello **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---** etiqueta y, a continuación, pegue Hola restantes contenido en Hola **clave** cuadro de texto.
    
    c. Hola **propiedad Id**, seleccione Hola atributo apropiado de que ha configurado como Hola identificador de usuario en hello Azure AD (por ejemplo, si se selecciona userprinciplename hello en Azure AD, nombre de usuario se seleccionará aquí.)

    d. Hola **dirección URL de inicio de sesión**, pegue hello **"SAML Single Sign-On dirección URL del servicio"** valor haya copiado desde hello **configurar inicio de sesión** ventana de hello portal de Azure.

    e. Hola **Logout URL**, pegue hello **"URL de cierre de sesión"** valor haya copiado desde hello **configurar inicio de sesión** ventana de hello portal de Azure.

13. Habilite **"Only Allow SSO Login"** (Solo permitir inicio de sesión SSO).

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Haga clic en **"Save"** (Guardar).

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![botón de agregar Hola](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.

### <a name="create-an-absorb-lms-test-user"></a>Creación de un usuario de prueba de Absorb LMS

toolog de los usuarios de Azure AD tooenable en tooAbsorb LMS, se les deben aprovisionar en tooAbsorb LMS.  
En el caso de Absorb LMS, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour sitio absorber LMS de su compañía como administrador.

2. Haga clic en la pestaña **Users** (Usuarios).

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Haga clic en **usuarios** en hello **usuarios** ficha.

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Seleccione **User** (Usuario) de la lista desplegable **Add New** (Agregar nuevo).

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. En hello **Agregar usuario** , siga los pasos de hello:

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. Hola **nombre** cuadro de texto Nombre tipo hello como Bárbara.

    b. Hola **Last Name** cuadro de texto, escriba Hola apellidos como Simon.
    
    c. Hola **nombre de usuario** cuadro de texto, escriba el nombre de usuario de hello como Britta Simon.

    d. Hola **contraseña** cuadro de texto, escriba la contraseña de Britta Simon Hola.

    e. Hola **Confirmar contraseña** cuadro de texto, hello tipo misma contraseña.
    
    f. Establézcalo en **ACTIVE** (ACTIVO).   

6. Haga clic en **"Save"** (Guardar).
 
### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAbsorb LMS.

![Asigne el rol de usuario de Hola][200]

**tooassign Britta Simon tooAbsorb LMS, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **absorber LMS**.

    ![Hola absorber LMS vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Haga clic en hello absorber LMS disponer en mosaico en hello Panel de acceso, obtendrá una aplicación de absorber LMS tooyour automáticamente ha iniciado sesión. Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

