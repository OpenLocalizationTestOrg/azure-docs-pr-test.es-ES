---
title: "Tutorial: Integración de Azure Active Directory con Huddle | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a>Tutorial: integración de Azure Active Directory con Huddle

En este tutorial, aprenderá cómo toointegrate Huddle con Azure Active Directory (Azure AD).

Integración de Huddle con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooHuddle
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHuddle (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD tooconfigure con Huddle, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Huddle

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario

En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Huddle desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-huddle-from-hello-gallery"></a>Agregar Huddle desde la Galería de Hola
integración de hello tooconfigure de Huddle en Azure AD, deberá tooadd Huddle de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Huddle de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Huddle**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. En el panel de resultados de hello, seleccione **Huddle**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Huddle con un usuario de prueba llamado "Britta Simon"

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Huddle es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Huddle necesidades toobe establecido.

En Huddle, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Huddle, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.

2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.

3. **[Crear un usuario de prueba de Huddle](#creating-a-huddle-test-user)**  -toohave un equivalente de Britta Simon en Huddle que es la representación toohello vinculado Azure AD del usuario.

4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.

5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Huddle.

**tooconfigure inicio de sesión único en Azure AD con Huddle, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Huddle** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. En hello **Huddle dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<company name>.huddle.com`

    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de Huddle cliente](https://huddle.zendesk.com) tooget este valor. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. En hello **Huddle configuración** sección, haga clic en **configurar Huddle** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.** 

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. tooconfigure inicio de sesión único en el lado de Huddle, necesita hello toosend descargado **certificado**, **SAML Single Sign-On dirección URL del servicio**, y **Id. de entidad SAML** demasiado[Equipo de soporte técnico de huddle cliente](https://huddle.zendesk.com). Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.  
   
    >[!NOTE]
    > Inicio de sesión único debe toobe habilitada por el equipo de soporte técnico de Huddle Hola. Recibirá una notificación cuando se haya completado la configuración de Hola. 
    > 

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 
   
### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-huddle-test-user"></a>Creación de un usuario de prueba de Huddle

toolog de los usuarios de Azure AD tooenable en tooHuddle, se les deben aprovisionar en Huddle. En caso de hello de Huddle, el aprovisionamiento es una tarea manual.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicie sesión en tooyour **Huddle** como administrador.
2. Haga clic en **Área de trabajo**.
3. Haga clic en **Contactos\>Invitar a contactos**.
   
   ![Personas](./media/active-directory-saas-huddle-tutorial/IC787838.png "Personas")

4. Hola **crear una nueva invitación** sección, lleve a cabo Hola pasos:
   
   ![Nueva invitación](./media/active-directory-saas-huddle-tutorial/IC787839.png "Nueva invitación")
   
   a. Hola **elegir un toojoin de personas de equipo tooinvite** lista, seleccione **equipo**.

   b. Hola de tipo **dirección de correo electrónico** de un anuncio de Azure válido de la cuenta que desee tooprovision en demasiado**escriba la dirección de correo electrónico para las personas que desea que tooinvite** cuadro de texto.

   c. Haga clic en **Invitar**.   
   
    >[!NOTE]
    > Hola cuenta de Azure AD titular recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla. 
    > 

>[!NOTE]
>Puede usar cualquier otra Huddle usuario cuenta herramienta de creación o las API proporcionadas por Huddle tooprovision cuentas de usuario de Azure AD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHuddle.

![Asignar usuario][200] 

**tooassign Britta Simon tooHuddle, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Huddle**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Huddle Hola Hola Panel de acceso, deberá obtener automáticamente la página de inicio de sesión de aplicación de Huddle.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
