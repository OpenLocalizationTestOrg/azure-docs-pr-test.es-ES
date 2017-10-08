---
title: "Tutorial: Integración de Azure Active Directory con @Task| Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Tutorial: integración de Azure Active Directory con @Task
objetivo de Hola de este tutorial es tooshow, cómo toointegrate @Task con Azure Active Directory (Azure AD).  
Integrar @Task con Azure AD proporciona Hola siguientes ventajas: 

* Puede controlar en Azure AD que tenga accesotoo@Task
* Se pueden permitir a los usuarios obtener tooautomatically ha iniciado sesión too@Task (Single Sign-On) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola Portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD tooconfigure con @Task, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Una suscripción habilitada para inicio de sesión único en @Task

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
> 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.  
escenario de Hello descrito en este tutorial consta de tres pilares principales:

1. Agregar @Task de galería de Hola 
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-task-from-hello-gallery"></a>Agregar @Task de galería de Hola
integración de hello tooconfigure de @Task en Azure AD, necesita tooadd @Task de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd @Task desde la Galería de hello, llevar a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1] 
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2] 
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3] 
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4] 
6. En el cuadro de búsqueda de hello, escriba  **@Task** .
   
    ![Aplicaciones][5] 
7. En el panel de resultados de hello, seleccione  **@Task** y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Aplicaciones][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
Hola objetivo de esta sección es tooshow, cómo tooconfigure y prueba de Azure AD único inicio de sesión con @Task en función de un usuario de prueba denominado "Bárbara Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en @Task tooan usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en @Task necesita toobe establecido.   
Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en @Task.

prueba Azure AD y tooconfigure inicio de sesión único con @Task, necesita hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un @Tasktest usuario](#creating-a-halogen-software-test-user)**  -toohave un equivalente de Britta Simon en @Taskthat es representación toohello vinculado Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooenable Azure AD single sign-on en hello portal de Azure clásico y tooconfigure inicio de sesión único en su @Task aplicación.

**tooconfigure inicio de sesión único en Azure AD con @Task, realizar Hola pasos:**

1. En el portal de Azure clásico en Hola Hola  **@Task**  página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.
   
    ![Configurar inicio de sesión único][6] 
2. En hello **¿cómo desea que los usuarios toosign en too@Task**  página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Inicio de sesión único de Azure AD ][7] 
3. En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:
   
    ![Configurar las opciones de la aplicación][8] 
   
     a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por los usuarios en toosign tooyour @Task aplicación (p. ej.:*https://<Tenant name>.attask ondemand.com*).
   
     b. Haga clic en **Siguiente**.
4. En hello **configurar inicio de sesión único en @Task**  página, haga clic en **descargar metadatos**, guarde el archivo de metadatos de hello localmente en el equipo y, a continuación, haga clic en **siguiente**.
   
    ![Qué es Azure AD Connect][9] 
5. Inicio de sesión tooyour @Task como administrador.
6. Vaya demasiado**inicio de sesión único en la configuración**.
7. En hello **Single Sign-On** cuadro de diálogo, realizar pasos de Hola
   
    ![Configurar inicio de sesión único][23]
   
    a. En **Tipo**, seleccione **SAML 2.0**.
   
    b. Seleccione **Service Provider ID** (Id. del proveedor de servicios).
   
    c. En el portal de Azure clásico hello, copie hello **dirección URL de inicio de sesión remoto**y, a continuación, péguelo en hello **dirección URL del Portal de inicio de sesión** cuadro de texto.
   
    d. En el portal de Azure clásico hello, copie Hola **dirección URL del servicio de cierre de sesión único**y, a continuación, péguelo en hello **dirección URL de cierre de sesión** cuadro de texto.
   
    e. En el portal de Azure clásico hello, copie hello **cambiar dirección URL de contraseña**y, a continuación, péguelo en hello **cambiar dirección URL de contraseña** cuadro de texto.
   
    f. Haga clic en **Guardar**.
8. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**. 
   
    ![Qué es Azure AD Connect][10]
9. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
   
    ![Qué es Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.  

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**. 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello: 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. En Tipo de usuario, seleccione Nuevo usuario de la organización.
   
    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
   
    c. Haga clic en **Siguiente**.
6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello: 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
   
    b. Hola **Last Name** cuadro de texto, tipo, **Simon**.
   
    c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
   
    d. Hola **rol** lista, seleccione **usuario**.

    e. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Anote el valor de Hola de hello **nueva contraseña**.
   
    b. Haga clic en **Completo**.   

### <a name="creating-an-task-test-user"></a>Creación de un usuario de prueba de @Task
objetivo de Hola de esta sección es un usuario llamado Britta Simon toocreate @Task.

**un usuario llamado Britta Simon toocreate @Task, realizar Hola pasos:**

1. Inicio de sesión tooyour @Task como administrador.
2. En el menú de hello en la parte superior de hello, haga clic en **personas**.
3. Haga clic en **New Person**(Nueva persona). 
4. En el cuadro de diálogo de hello nueva persona, realice Hola pasos:
   
    ![Creación de un usuario de prueba de @Task][21] 
   
    a. Hola **nombre** cuadro de texto, escriba "Bárbara".
   
    b. Hola **Last Name** cuadro de texto, escriba "Simon".
   
    c. Hola **dirección de correo electrónico** cuadro de texto, escriba la dirección de correo electrónico Britta Simon en Azure Active Directory.
   
    d. Haga clic en **Add Person**(Agregar persona).

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su acceso too@Task.

![Asignar usuario][200] 

**tooassign Britta Simon too@Task, realizar Hola pasos:**

1. En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.
   
    ![Asignar usuario][201] 
2. En la lista de aplicaciones de hello, seleccione  **@Task** .
   
    ![Asignar usuario][202] 
3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Asignar usuario][203] 
4. En la lista de usuarios de hello, seleccione **Britta Simon**.
5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Asignar usuario][205]

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 
objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.  
Al hacer clic en hello @Task Hola de mosaico en el Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour @Task aplicación.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






