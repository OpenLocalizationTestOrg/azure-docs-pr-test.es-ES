---
title: "Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Splunk Enterprise y Splunk en la nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Tutorial: Integración de Azure Active Directory con Splunk Enterprise y Splunk Cloud

En este tutorial, aprenderá cómo toointegrate Splunk Enterprise y Splunk en la nube con Azure Active Directory (Azure AD).

Integración de Splunk Enterprise y Splunk en la nube con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSplunk Enterprise y Splunk en la nube
- Puede habilitar la get ha iniciado sesión tooSplunk de usuarios tooautomatically grandes empresas y nube Splunk inicio de sesión único (SSO) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Splunk Enterprise y Splunk en la nube, debe Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el SSO en Splunk Enterprise o Splunk Cloud.


>[!NOTE]
>Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
>

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Splunk Enterprise y Splunk en la nube de la Galería de Hola
2. Configuración y prueba del inicio de sesión único de Azure AD


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Agregar Splunk empresarial y en la nube Splunk de galería de Hola
integración de hello tooconfigure de empresa de Splunk y Splunk en la nube en Azure AD, necesita tooadd Splunk Enterprise y Splunk en la nube de lista de tooyour Hola Galería de las aplicaciones de SaaS administradas.

**tooadd Splunk Enterprise y Splunk en la nube de la Galería de hello, realizar Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.

    ![Active Directory][1]

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.

    ![Aplicaciones][2]

4. Haga clic en **agregar** final Hola de página Hola.

    ![Aplicaciones][3]

5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.

    ![Aplicaciones][4]

6. En el cuadro de búsqueda de hello, escriba **Splunk Enterprise o nube Splunk**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. En el panel de resultados de hello, seleccione **Splunk empresarial y en la nube Splunk**y, a continuación, haga clic en **completar** aplicación de hello tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Splunk Enterprise y Splunk Cloud mediante un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Splunk Enterprise y Splunk en la nube es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Splunk Enterprise y Splunk en la nube debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Splunk Enterprise y Splunk en la nube.

tooconfigure y prueba de inicio de sesión único en Azure AD con Splunk Enterprise y Splunk en la nube, deberá hello toocomplete después de bloques de creación:

1. **[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Splunk empresarial y en la nube Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user) ** -toohave un equivalente de Britta Simon de empresa de Splunk y Splunk en la nube que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, se habilita el SSO de Azure AD en el portal clásico de Hola y configura SSO en la aplicación empresarial de Splunk y Splunk en la nube.


**tooconfigure inicio de sesión único en Azure AD con Splunk Enterprise y Splunk en la nube, lleve a cabo Hola pasos:**

1. En portal clásico de hello, en hello **Splunk empresarial y en la nube Splunk** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On** cuadro de diálogo.
     
    ![Configurar inicio de sesión único][6] 

2. En hello **cómo le gustaría toosign a los usuarios en tooSplunk empresarial y en la nube Splunk** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada los usuarios toosign en tooyour Splunk Enterprise y aplicación de nube de Splunk mediante Hola sigue el patrón:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. Hola **identificador** cuadro de texto, escriba Hola la dirección URL del servidor Splunk.
  3. Hola **dirección URL de respuesta** cuadro de texto, escriba la dirección URL Hola con hello sigue el patrón:`https://<splunkserver>/saml/acs`
  4. Haga clic en **Siguiente**.
 
4. En hello **configurar inicio de sesión único en Splunk empresarial y en la nube Splunk** , siga los pasos de hello:

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo.
  2. Haga clic en **Siguiente**.

5. tooget SSO configurado para la aplicación, póngase en contacto con Splunk empresarial y el equipo de soporte técnico de Splunk en la nube y proporcionarles siguiente hello:

    * Hola descargado **federaton metadatos**
6. En el portal clásico de hello, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.
    
    ![Inicio de sesión único de Azure AD ][10]

7. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.  
 
    ![Inicio de sesión único de Azure AD ][11]

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, creará un usuario de prueba en el portal clásico de hello llamado a Britta Simon.

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. En Tipo de usuario, seleccione Nuevo usuario de la organización.
  2. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
  3. Haga clic en **Siguiente**.

6.  En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:
  
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
  2. Hola **Last Name** cuadro de texto, tipo, **Simon**.
  3. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
  4. Hola **rol** lista, seleccione **usuario**.
  5. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Anote el valor de Hola de hello **nueva contraseña**.
  2. Haga clic en **Completo**.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Creación de un usuario de prueba de Splunk Enterprise y Splunk Cloud

En esta sección, creará un usuario llamado Britta Simon en Splunk Enterprise y Splunk Cloud. Trabaje con Splunk empresarial y en la nube Splunk usuarios de soporte técnico team tooadd hello en hello Splunk Enterprise y plataforma de nube Splunk.


### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse SSOy Azure conceder su acceso tooSplunk Enterprise y Splunk en la nube.

![Asignar usuario][200] 

**tooassign Britta Simon tooSplunk Enterprise y Splunk en la nube, realizar Hola pasos:**

1. En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Splunk empresarial y en la nube Splunk**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.

    ![Asignar usuario][203]

4. En la lista de usuarios de hello, seleccione **Britta Simon**.

5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.

    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la AD SSOonfiguration de Azure con hello Panel de acceso.

Al hacer clic en hello Splunk empresarial y el icono de nube Splunk Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación empresarial de Splunk y Splunk en la nube.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
