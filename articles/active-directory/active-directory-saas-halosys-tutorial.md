---
title: "Tutorial: Integración de Azure Active Directory con Halosys | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Halosys con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Tutorial: Integración de Azure Active Directory con Halosys

En este tutorial, aprenderá cómo toointegrate Halosys con Azure Active Directory (Azure AD).

Integración Halosys con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooHalosys
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHalosys (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Halosys tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Halosys.


> [!NOTE] 
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Halosys desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-halosys-from-hello-gallery"></a>Agregar Halosys desde la Galería de Hola
integración de hello tooconfigure de Halosys en Azure AD, deberá tooadd Halosys de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Halosys de galería de hello, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.

    ![Active Directory][1]
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.

    ![Aplicaciones][2]

4. Haga clic en **agregar** final Hola de página Hola.

    ![Aplicaciones][3]

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.

    ![Aplicaciones][4]

6. En el cuadro de búsqueda de hello, escriba **Halosys**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. En el panel de resultados de hello, seleccione **Halosys**y, a continuación, haga clic en **completar** aplicación de hello tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Halosys con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Halosys es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Halosys debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Halosys.

tooconfigure y prueba de inicio de sesión único en Azure AD con Halosys, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Halosys](#creating-a-halosys-test-user)**  -toohave un equivalente de Britta Simon en Halosys que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación Halosys.


**inicio de sesión único en Azure AD tooconfigure con Halosys, realizar Hola pasos:**

1. En portal clásico de hello, en hello **Halosys** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On** cuadro de diálogo.
     
    ![Configurar inicio de sesión único][6] 

2. En hello **¿cómo desea que los usuarios toosign en tooHalosys** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por la aplicación de Halosys de tooyour toosign en los usuarios con hello sigue el patrón: `https://<company-name>.Halosys.com/client-api/api`.

    Hola b.In **dirección URL de identificación** cuadro de texto, escriba la dirección URL Hola Hola siguiente patrón: `https://<company-name>.Halosys.com`. 
         
4. En hello **configurar inicio de sesión único en Halosys** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo:

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO configurado para la aplicación, póngase en contacto con el equipo de soporte técnico de Halosys y proporcionarles siguiente hello:

    Hola • descargado **archivo de metadatos**
    
    • hello **dirección URL SSO SAML**
    

6. En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.
    
    ![Inicio de sesión único de Azure AD ][10]

7. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
 
    ![Inicio de sesión único de Azure AD ][11]


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, creará un usuario de prueba en el portal clásico de hello llamado a Britta Simon.


![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello: ![crear un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. En Tipo de usuario, seleccione Nuevo usuario de la organización.

    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.

    c. Haga clic en **Siguiente**.

6.  En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello: ![crear un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. Hola **nombre** cuadro de texto, tipo **Bárbara**.  

    b. Hola **Last Name** cuadro de texto, tipo, **Simon**.

    c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.

    d. Hola **rol** lista, seleccione **usuario**.

    e. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Anote el valor de Hola de hello **nueva contraseña**.

    b. Haga clic en **Completo**.   



### <a name="creating-a-halosys-test-user"></a>Creación de un usuario de prueba de Halosys

En esta sección, creará un usuario llamado Britta Simon en Halosys. Trabaje con Halosys usuarios de soporte técnico team tooadd hello en la plataforma de Halosys Hola.


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooHalosys de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooHalosys, lleve a cabo Hola pasos:**

1. En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Halosys**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.

    ![Asignar usuario][203]

4. En la lista de usuarios de hello, seleccione **Britta Simon**.

5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.

    ![Asignar usuario][205]


### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Halosys el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Halosys aplicación.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
