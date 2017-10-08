---
title: "Tutorial: Integración de Azure Active Directory con Bynder | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Tutorial: Integración de Azure Active Directory con Bynder
objetivo de Hola de este tutorial es tooshow, cómo toointegrate Bynder con Azure Active Directory (Azure AD).

Integración Bynder con Azure AD proporciona Hola siguientes ventajas:

* Puede controlar en Azure AD que tenga acceso tooBynder
* Puede habilitar los usuarios tooautomatically get tooBynder ha iniciado sesión con inicio de sesión único (SSO) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con Bynder tooconfigure, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Una suscripción habilitada para el inicio de sesión único en Bynder

>[!NOTE]
>Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción. 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest Microsoft Azure AD SSO en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Bynder desde la Galería de Hola
2. Configuración y prueba del inicio de sesión único de Microsoft Azure AD

## <a name="add-bynder-from-hello-gallery"></a>Agregar Bynder de galería de Hola
integración de hello tooconfigure de Bynder en Azure AD, deberá tooadd Bynder de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Bynder de galería de hello, lleve a cabo Hola pasos:**

1. Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1]
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2]
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4]
6. En el cuadro de búsqueda de hello, escriba **Bynder**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. En el panel de resultados de hello, seleccione **Bynder**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Seleccionar aplicación hello en la Galería de Hola](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configuración y prueba del inicio de sesión único de Microsoft Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y probar Microsoft Azure AD SSO con Bynder a partir de un usuario de prueba denominado "Britta Simon".

Para toowork SSO, Azure AD necesita tooknow es qué usuario equivalente de hello en Bynder tooan usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Bynder debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Bynder.

tooconfigure y prueba de Microsoft Azure AD SSO con Bynder, deberá hello toocomplete después de bloques de creación:

1. **[Configuración del inicio de sesión único en Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On con Britta Simon.
3. **[Crear un usuario de prueba Bynder](#creating-a-bynder-test-user)**  -toohave un equivalente de Britta Simon en Bynder que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.
5. **[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configuración del inicio de sesión único de Microsoft Azure AD
En esta sección, habilita el SSO de Microsoft Azure AD en el portal clásico de Hola y configurar SSO en la aplicación Bynder.

**tooconfigure Microsoft Azure AD SSO con Bynder, lleve a cabo Hola pasos:**

1. En portal clásico de hello, en hello **Bynder** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On** cuadro de diálogo.
   
    ![Configurar inicio de sesión único][6] 
2. En hello **¿cómo desea que los usuarios toosign en tooBynder** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. En hello **configurar opciones de aplicación** página de diálogo, si lo desea tooconfigure aplicación de hello en **modo iniciado por IDP**, realizar pasos de Hola y haga clic en **siguiente**:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Haga clic en **Siguiente**.
4. Si desea que aplicación de hello tooconfigure en **modo iniciado en SP** en hello **configurar opciones de aplicación** página de diálogo y, a continuación, haga clic en hello **"Show advanced configuración (opcional)"**y, a continuación, escriba Hola **dirección URL de inicio de sesión** y haga clic en **siguiente**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.getbynder.com/login/`
  2. Haga clic en **Siguiente**.
  
   >[!NOTE]
   >valor Hola Hola dirección URL de inicio de sesión en este tutorial es simplemente un placeholfer. valor real de hello tooget para su entorno, póngase en contacto con Bynder.
   >

5. En hello **configurar inicio de sesión único en Bynder** página, realizar pasos de Hola y haga clic en **siguiente**:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo.
  2. Haga clic en **Siguiente**.
6. tooget SSO configurado para la aplicación, póngase en contacto con el equipo de soporte de Bynder. Adjuntar el archivo de metadatos descargado de Hola y compartirlo con Bynder equipo tooset seguridad SSO en uno de su lados.
7. En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.
   
    ![Inicio de sesión único de Azure AD ][10]
8. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
   
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es toocreate un usuario de prueba en el portal clásico de hello llamado a Britta Simon.

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. En Tipo de usuario, seleccione Nuevo usuario de la organización.
  2. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
  3. Haga clic en **Siguiente**.
6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
  2. Hola **Last Name** cuadro de texto, tipo, **Simon**. 
  3. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
  4. Hola **rol** lista, seleccione **usuario**.
  5. Haga clic en **Siguiente**.
7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Anote el valor de Hola de hello **nueva contraseña**.
   2. Haga clic en **Completo**.   

### <a name="create-a-bynder-test-user"></a>Creación de un usuario de prueba de Bynder
objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Bynder toocreate. Bynder admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

No hay ningún elemento de acción para usted en esta sección. Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento Bynder.

>[!NOTE]
>Si necesita un usuario toocreate manualmente, debe equipo de soporte técnico de toocontact hello Bynder. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure SSO mediante la concesión de su tooBynder de acceso.

   ![Asignar usuario][200]

**tooassign Britta Simon tooBynder, lleve a cabo Hola pasos:**

1. En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Asignar usuario][201]
2. En la lista de aplicaciones de hello, seleccione **Bynder**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Asignar usuario][203]
4. En la lista de usuarios de hello, seleccione **Britta Simon**.
5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único
objetivo de Hola de esta sección es tootest la configuración de SSO de Microsoft Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de Bynder Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Bynder aplicación.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
