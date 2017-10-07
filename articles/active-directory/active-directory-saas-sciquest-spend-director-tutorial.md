---
title: "Tutorial: Integración de Azure Active Directory con SciQuest Spend Director | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SciQuest dedicar Director."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Tutorial: Integración de Azure Active Directory con SciQuest Spend Director
objetivo de Hola de este tutorial es tooshow, cómo toointegrate SciQuest dedicar Director con Azure Active Directory (Azure AD).  
Integración SciQuest dedicar Director con Azure AD proporciona Hola siguientes ventajas: 

* Puede controlar en Azure AD que tenga acceso tooSciQuest Director de gastos 
* Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSciQuest Director de gastos (Single Sign-On) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
tooconfigure integración de Azure AD con SciQuest dedicar Director, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Una suscripción de SciQuest Spend Director habilitada para el inicio de sesión único

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
> 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.  
escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar SciQuest dedicar Director de galería de Hola 
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Agregar SciQuest dedicar Director de galería de Hola
integración de hello tooconfigure de Director de dedicar SciQuest en Azure AD, deberá tooadd SciQuest dedicar Director de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SciQuest dedicar Director de galería de hello, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1]

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2]

4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4]

6. En el cuadro de búsqueda de hello, escriba **sciQuest dedicar director**.
   
    ![Aplicaciones][5]

7. En el panel de resultados de hello, seleccione **SciQuest dedicar Director**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Aplicaciones][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con SciQuest dedicar Director a partir de un usuario de prueba denominado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en Director de gasto de SciQuest tooan usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SciQuest dedicar Director debe toobe establecido.  
Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SciQuest dedicar Director.

tooconfigure y prueba de inicio de sesión único en Azure AD con SciQuest dedicar Director, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD único Single Sign-On](#configuring-azure-ad-single-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Director de gasto de SciQuest](#creating-a-halogen-software-test-user) ** -toohave un equivalente de Britta Simon en SciQuest dedicar Director es representación toohello vinculado Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooenable Azure AD single sign-on Hola portal de Azure clásico y tooconfigure inicio de sesión único en la aplicación SciQuest dedicar Director.

**tooconfigure inicio de sesión único en Azure AD con SciQuest dedicar Director, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **SciQuest dedicar Director** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**cuadro de diálogo.
   
    ![Configurar inicio de sesión único][8]

2. En hello **¿cómo desea que los usuarios toosign en tooSciQuest Director de gastos** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Inicio de sesión único de Azure AD ][9]

3. En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello: 
   
    ![Configurar las opciones de la aplicación][10]
   
     a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL que utilizan su toosign a los usuarios de aplicación de Director de gasto de SciQuest de tooyour utiliza Hola siguiente patrón: *https://.* SciQuest.com/.**
   
     b. Hola **dirección URL de respuesta** cuadro de texto, hello tipo mismo valor ha escrito en hello **dirección URL de inicio de sesión** cuadro de texto. 
   
     c. Haga clic en **Siguiente**.

4. En hello **configurar inicio de sesión único en el Director de dedicar SciQuest** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos de hello localmente en el equipo.
   
    ![Qué es Azure AD Connect][11]

5. Póngase en contacto con SciQuest tooenable de compatibilidad con este método de autenticación mediante metadatos de hello anterior descargado.

6. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo. 
   
    ![Qué es Azure AD Connect][15]

7. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Qué es Azure AD Connect][100] 

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Qué es Azure AD Connect][101] 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**. 
   
    ![Qué es Azure AD Connect][102] 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Qué es Azure AD Connect][103] 
   
    a. En **Tipo de usuario**, seleccione **Nuevo usuario de la organización**.
   
    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
   
    c. Haga clic en **Siguiente**.

6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello: 
   
    ![Qué es Azure AD Connect][104] 
   
    a. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
   
    b. Hola **Last Name** txtbox, tipo, **Simon**.
   
    c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
   
    d. Hola **rol** lista, seleccione **usuario**.
   
    e. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Qué es Azure AD Connect][105]  

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Qué es Azure AD Connect][106]   
   
    a. Anote el valor de Hola de hello **nueva contraseña**.
   
    b. Haga clic en **Completo**.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Creación de un usuario de prueba de SciQuest Spend Director
objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en SciQuest dedicar Director.

El equipo de soporte de SciQuest dedicar Director es necesario toocontact y proporcionarles detalles Hola sobre su tooget de cuenta de prueba que creó.

Como alternativa, también puede aprovechar el aprovisionamiento Just-In-Time, una característica de inicio de sesión único que es compatible con SciQuest Spend Director.  
Si el aprovisionamiento Just-In-Time está habilitado, los usuarios se crean automáticamente en SciQuest Spend Director durante un intento de inicio de sesión único, si no existen. Esta característica elimina la necesidad de hello toomanually crear equivalente de inicio de sesión único a los usuarios.

el aprovisionamiento de just-in-time de tooget habilitado, debe toocontact está el equipo de soporte de SciQuest dedicar Director.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSciQuest acceso Director de gastos.

![Qué es Azure AD Connect][200]

**tooassign Britta Simon tooSciQuest Director de gasto, lleve a cabo Hola pasos:**

1. En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.
   
    ![Qué es Azure AD Connect][201]

2. En la lista de aplicaciones de hello, seleccione **SciQuest dedicar Director**.
   
    ![Qué es Azure AD Connect][202]

3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Qué es Azure AD Connect][203]

4. En la lista de usuarios de hello, seleccione **Britta Simon**.
   
    ![Qué es Azure AD Connect][204]

5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Qué es Azure AD Connect][205]

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 
objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.  
Al hacer clic en icono de Director de dedicar SciQuest Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour SciQuest dedicar Director aplicación.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

