---
title: "Tutorial: integración de Azure Active Directory con Soonr Workplace | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Soonr al área de trabajo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Tutorial: integración de Azure Active Directory con Soonr Workplace

objetivo de Hola de este tutorial es tooshow, cómo toointegrate Soonr al área de trabajo con Azure Active Directory (Azure AD).  
Integración Soonr al área de trabajo con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSoonr al área de trabajo
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSoonr al área de trabajo (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con un área de trabajo de Soonr tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Soonr Workplace


> [!NOTE] 
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.  
escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar un área de trabajo Soonr de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Agregar un área de trabajo Soonr de galería de Hola
integración de hello tooconfigure Soonr área de trabajo en Azure AD, deberá tooadd Soonr al área de trabajo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Soonr al área de trabajo desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 

    ![Active Directory][1]

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.

    ![Aplicaciones][2]

4. Haga clic en **agregar** final Hola de página Hola.

    ![Aplicaciones][3]

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
 
    ![Aplicaciones][4]

6. En el cuadro de búsqueda de hello, escriba **al área de trabajo de Soonr**.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. En el panel de resultados de hello, seleccione **al área de trabajo de Soonr**y, a continuación, haga clic en **completar** aplicación de hello tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con Soonr al área de trabajo a partir de un usuario de prueba denominado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en usuario de un área de trabajo de Soonr tooan en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el área de trabajo de Soonr debe toobe establecido.  

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en lugar de trabajo Soonr.

tooconfigure y prueba de inicio de sesión único en Azure AD con Soonr al área de trabajo, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba al área de trabajo de Soonr](#creating-a-soonr-workplace-test-user)**  -toohave un equivalente de Britta Simon en lugar de trabajo de Soonr es representación toohello vinculado Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación de área de trabajo de Soonr.


**inicio de sesión único en tooconfigure Azure AD con Soonr al área de trabajo, realizar Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **al área de trabajo de Soonr** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.

    ![Configurar inicio de sesión único][6] 

2. En hello **¿cómo desea que los usuarios toosign en tooSoonr al área de trabajo** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:.

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Haga clic en **Siguiente**.

    > [!NOTE] 
    > Tenga en cuenta que esto no es un valor real Hola. Tendrá que tooupdate este valor con hello real iniciar sesión en la dirección URL. Póngase en contacto con tooget de equipo de soporte técnico al área de trabajo de Soonr este valor.

4. En hello **configurar inicio de sesión único en el área de trabajo de Soonr** página, haga clic en **descargar metadatos** y, a continuación, guarde el archivo hello en el equipo:

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget SSO configurado para la aplicación, póngase en contacto con el equipo de soporte técnico al área de trabajo Soonr y proporcionarles siguiente hello: 

    Hola • descargado **metadatos** archivo

    • hello **dirección URL del emisor**

    • hello **dirección URL SSO SAML**

    • hello **dirección URL del servicio de cierre de sesión único**

    >[!NOTE]
    >Esta aplicación es sustituida por <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">al área de trabajo de Autotask</a> y hacer referencia <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">esto</a> tutorial para configurar la aplicación hello con Azure AD.
   
6. Hola portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.

    ![Inicio de sesión único de Azure AD ][10]

7. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
  
    ![Inicio de sesión único de Azure AD ][11]



### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.  

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. En Tipo de usuario, seleccione Nuevo usuario de la organización.

    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.

    c. Haga clic en **Siguiente**.

6.  En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. Hola **nombre** cuadro de texto, tipo **Bárbara**.  

    b. Hola **Last Name** cuadro de texto, tipo, **Simon**.

    c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.

    d. Hola **rol** lista, seleccione **usuario**.

    e. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Anote el valor de Hola de hello **nueva contraseña**.

    b. Haga clic en **Completo**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Creación de un usuario de prueba de Soonr Workplace

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en lugar de trabajo de Soonr toocreate. Trabaje con toocreate de equipo de soporte técnico al área de trabajo de Soonr un usuario en la plataforma de Hola. Puede generar incidencia de soporte técnico de hello con Soonr de <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">aquí</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSoonr de acceso al área de trabajo.

![Asignar usuario][200] 

**tooassign Britta Simon tooSoonr al área de trabajo, lleve a cabo Hola pasos:**

1. En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **al área de trabajo de Soonr**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.

    ![Asignar usuario][203] 

1. En la lista de usuarios de hello, seleccione **Britta Simon**.

2. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.

    ![Asignar usuario][205]



### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.  
Al hacer clic en hello al área de trabajo Soonr el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Soonr al área de trabajo.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
