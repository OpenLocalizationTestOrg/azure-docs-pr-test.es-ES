---
title: "Tutorial: Integración de Azure Active Directory con Wizergos Productivity Software | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el Software de productividad de Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Tutorial: integración de Azure Active Directory con Wizergos Productivity Software
objetivo de Hola de este tutorial es tooshow, cómo toointegrate Wizergos Software de productividad con Azure Active Directory (Azure AD).

La integración del Software de productividad Wizergos con Azure AD proporciona Hola siguientes ventajas:

* Puede controlar en Azure AD que tenga acceso tooWizergos Software de productividad
* Puede habilitar la get ha iniciado sesión tooWizergos de usuarios tooautomatically Software de productividad inicio de sesión único (SSO) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con el Software de productividad de Wizergos tooconfigure, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Un suscripción habilitada para el inicio de sesión único en Wizergos Productivity Software

>[!NOTE]
>Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción. 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest Azure AD SSO en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Software de productividad Wizergos desde galería Hola
2. Configuración y prueba del inicio de sesión único de Azure AD

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Agregar Software de productividad Wizergos desde galería Hola
integración de hello tooconfigure Wizergos de Software de productividad en Azure AD, deberá tooadd Wizergos Software de productividad de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Wizergos Software de productividad de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1]
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2]
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4]
6. En el cuadro de búsqueda de hello, escriba **Software de productividad de Wizergos**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. En el panel de resultados de hello, seleccione **Software de productividad de Wizergos**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Seleccionar aplicación hello en la Galería de Hola](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configuración y prueba del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de Azure AD SSO con el Software de productividad de Wizergos a partir de un usuario de prueba denominado "Britta Simon".

Para toowork SSO, Azure AD necesita tooknow qué usuario equivalente de hello en usuario de Software de productividad de Wizergos tooan en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el Software de productividad Wizergos debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** Wizergos software de productividad.

tooconfigure y prueba de inicio de sesión único en Azure AD con BynWizergos productividad Softwareder, deberá hello toocomplete después de bloques de creación:

1. **[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Software de productividad de Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave un equivalente de Britta Simon Wizergos software de productividad que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD
En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación de Software de productividad de Wizergos.

**tooconfigure inicio de sesión único en Azure AD con el Software de productividad Wizergos, lleve a cabo Hola pasos:**

1. En portal clásico de hello, en hello **Software de productividad de Wizergos** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**cuadro de diálogo.
   
    ![Configurar inicio de sesión único][6] 
2. En hello **¿cómo desea que los usuarios toosign en tooWizergos Software de productividad** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. En hello **configurar opciones de aplicación** página del cuadro de diálogo, haga clic en **siguiente**:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. En hello **configurar inicio de sesión único en Software de productividad de Wizergos** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo hello en el equipo:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. En una ventana del explorador web diferente, inquilino de Software de productividad de Wizergos tooyour de inicio de sesión como administrador.
6. En hello hamburguesa menú, seleccione **administración**.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. En el menú de la izquierda de la página Admin, seleccione **AUTHENTICACIÓN** y haga clic en **Azure AD**.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Realizar Hola seguir pasos de **autenticación** sección.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Haga clic en **cargar** Hola de tooupload botón descarga certificado de Azure AD. 
  2. Hola **dirección URL del emisor** textbox coloca el valor de Hola de **dirección URL del emisor** desde el Asistente para configuración de aplicaciones de Azure AD.
  3. Hola **dirección URL de inicio de sesión único** textbox coloca el valor de Hola de **URL de servicio de inicio de sesión único** desde el Asistente para configuración de aplicaciones de Azure AD.
  4. Hola **dirección URL de cierre de sesión único** textbox coloca el valor de Hola de **dirección URL del servicio de cierre de sesión único** desde el Asistente para configuración de aplicaciones de Azure AD.
  5. Haga clic en el botón **Guardar** .
9. En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.
   
    ![Inicio de sesión único de Azure AD ][10]
10. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
    
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es toocreate un usuario de prueba en el portal clásico de hello llamado a Britta Simon.

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. En Tipo de usuario, seleccione Nuevo usuario de la organización.
  2. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
  3. Haga clic en **Siguiente**.
6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
  2. Hola **Last Name** cuadro de texto, tipo, **Simon**.
  3. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
  4. Hola **rol** lista, seleccione **usuario**.
  5. Haga clic en **Siguiente**.
7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Anote el valor de Hola de hello **nueva contraseña**.
  2. Haga clic en **Completo**.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Creación de un usuario de prueba de Wizergos Productivity Software
En esta sección, creará un usuario llamado Britta Simon en Wizergos Productivity Software. Trabaje con el equipo de soporte técnico de Software de productividad Wizergos a través de [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd los usuarios de hello en la plataforma de Software de productividad Wizergos Hola.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure SSO mediante la concesión de su Software de productividad de tooWizergos de acceso.

  ![Asignar usuario][200]

**tooassign Britta Simon tooWizergos Software de productividad, lleve a cabo Hola pasos:**

1. En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Asignar usuario][201]
2. En la lista de aplicaciones de hello, seleccione **Software de productividad de Wizergos**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Asignar usuario][203]
4. En la lista de usuarios de hello, seleccione **Britta Simon**.
5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único
objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de Software de productividad Wizergos Hola Hola Panel de acceso, deberá obtener la aplicación de Software de productividad Wizergos tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
