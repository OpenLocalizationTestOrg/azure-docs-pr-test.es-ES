---
title: "Tutorial: Integración de Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el sistema de supervisión de temperatura de SensoScientific inalámbrica."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Tutorial: Integración de Azure Active Directory con SensoScientific Wireless Temperature Monitoring System

En este tutorial, aprenderá cómo toointegrate SensoScientific inalámbrica temperatura el sistema de supervisión con Azure Active Directory (Azure AD).

Integrar el sistema de supervisión de temperatura de SensoScientific inalámbrica con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSensoScientific el sistema de supervisión de temperatura de inalámbrica
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSensoScientific sistema de supervisión de temperatura de inalámbrica (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con el sistema de supervisión de temperatura de SensoScientific inalámbrica, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción que tenga habilitado el inicio de sesión único en SensoScientific Wireless Temperature Monitoring System.

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar el sistema de supervisión de temperatura de SensoScientific inalámbrica desde galería Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Agregar el sistema de supervisión de temperatura de SensoScientific inalámbrica desde galería Hola
integración de hello tooconfigure del sistema de supervisión de temperatura de SensoScientific inalámbrico en Azure AD, deberá tooadd el sistema de supervisión de temperatura de SensoScientific inalámbrico de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SensoScientific inalámbrica temperatura el sistema de supervisión de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **el sistema de supervisión de temperatura de SensoScientific inalámbrica**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. En el panel de resultados de hello, seleccione **el sistema de supervisión de temperatura de SensoScientific inalámbrica**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SensoScientific Wireless Temperature Monitoring System mediante un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el sistema de supervisión de temperatura de SensoScientific inalámbrica es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el sistema de supervisión de temperatura de SensoScientific inalámbrica debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en el sistema de supervisión de temperatura de SensoScientific inalámbrica.

tooconfigure y prueba de inicio de sesión único en Azure AD con el sistema de supervisión de temperatura de SensoScientific inalámbrica, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba del sistema de supervisión de temperatura de SensoScientific inalámbrica](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave un equivalente de Britta Simon en SensoScientific inalámbrica temperatura el sistema de supervisión que está vinculado representación toohello Azure AD de usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de sistema de supervisión de temperatura de SensoScientific inalámbrica.

**tooconfigure inicio de sesión único en Azure AD con el sistema de supervisión de una temperatura de Wireless SensoScientific, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **el sistema de supervisión de temperatura de SensoScientific inalámbrica** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. En hello **SensoScientific inalámbrica temperatura el dominio de sistema de supervisión y las direcciones URL** no sección ningún tooperform necesario ningún paso como aplicación hello ya está integrado previamente con Azure:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. En hello **configuración de sistema de supervisión de SensoScientific inalámbrica temperatura** sección, haga clic en **configurar sistema de supervisión de SensoScientific inalámbrica temperatura** tooopen  **Configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Inicie sesión en tooyour aplicación del sistema de supervisión de temperatura de SensoScientific inalámbrica como administrador.

8. En el menú de navegación de hello en la parte superior de hello, haga clic en **configuración** y goto **configurar** en **Single Sign On** tooopen Hola inicio de sesión único en la configuración.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. En **inicio de sesión único en la configuración** formulario realizar Hola pasos:
 
    a. Seleccione **Issuer Name** (Nombre del emisor) como Azure AD.
    
    b. Hola pegar **Id. de entidad SAML** que haya copiado desde el portal de Azure en el cuadro de texto de dirección URL del emisor.
    
    c. Hola pegar **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure en el cuadro de texto URL de servicio de inicio de sesión único.

    d. Hola pegar **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure en el cuadro de texto de dirección URL del servicio de cierre de sesión único.

    e. Examinar el certificado de Hola que ha descargado desde el portal de Azure y cargar aquí.
    
    f. Haga clic en **Guardar**.
  
> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Creación de un usuario de prueba de SensoScientific Wireless Temperature Monitoring System

toolog de los usuarios de Azure AD tooenable en tooSensoScientific el sistema de supervisión de temperatura de inalámbrica, se les debe aprovisionar en el sistema de supervisión de temperatura de SensoScientific inalámbrica. Trabajar con [equipo de soporte técnico del sistema de supervisión de temperatura de SensoScientific Wireless](https://www.sensoscientific.com/contact-us/) para agregar usuarios de hello en la plataforma del sistema de supervisión de temperatura de SensoScientific inalámbrica Hola. Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSensoScientific el sistema de supervisión de temperatura de inalámbrica.

![Asignar usuario][200] 

**tooassign Britta Simon tooSensoScientific sistema de supervisión de temperatura de inalámbrica, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **el sistema de supervisión de temperatura de SensoScientific inalámbrica**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso. Haga clic en icono de sistema de supervisión de temperatura de SensoScientific inalámbrica Hola Hola Panel de acceso, será la aplicación de sistema de supervisión de temperatura de SensoScientific inalámbrica tooyour automáticamente ha iniciado sesión. Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

