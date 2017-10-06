---
title: "Tutorial: Integración de Azure Active Directory con TeamSeer | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a>Tutorial: integración de Azure Active Directory con TeamSeer

En este tutorial, aprenderá cómo toointegrate TeamSeer con Azure Active Directory (Azure AD).

Integración TeamSeer con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTeamSeer
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTeamSeer (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con TeamSeer tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en TeamSeer

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar TeamSeer desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-teamseer-from-hello-gallery"></a>Agregar TeamSeer desde la Galería de Hola
integración de hello tooconfigure de TeamSeer en tooAzure AD, deberá tooadd TeamSeer de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd TeamSeer de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **TeamSeer**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. En el panel de resultados de hello, seleccione **TeamSeer**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TeamSeer con un usuario de prueba llamado Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TeamSeer es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TeamSeer debe toobe establecido.

En TeamSeer, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con TeamSeer, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de TeamSeer](#creating-a-teamseer-test-user)**  -toohave un equivalente de Britta Simon en TeamSeer que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TeamSeer.

**inicio de sesión único en Azure AD tooconfigure con TeamSeer, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **TeamSeer** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. En hello **TeamSeer dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.teamseer.com/<companyid>`

    > [!NOTE] 
    > valor de Hello no es real. Valor de Hola de actualización con Hola dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de TeamSeer cliente](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) valor de hello tooget. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. En hello **configuración de TeamSeer** sección, haga clic en **configurar TeamSeer** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía TeamSeer tooyour como administrador.

8. Vaya demasiado**administración de recursos humanos**.
   
    ![Administración de RR. HH.](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Administración de RR. HH.")

9. Haga clic en **Configuración**.
   
    ![Instalación](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Instalación")

10. Haga clic en **Configurar detalles del proveedor SAML**.
   
    ![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Configuración de SAML")

11. En la sección de detalles del proveedor SAML hello, realizar Hola pasos:
   
    ![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Configuración de SAML")   

    a. Hola pegar **URL de servicio de inicio de sesión único** valor en toohello **URL** cuadro de texto.
          
    b. Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles de tooyour y, a continuación, péguelo toohello **certificado público IdP** cuadro de texto.

12. Hola toocomplete configuración del proveedor SAML, lleve a cabo Hola pasos:
    
    ![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Configuración de SAML") 

    a. Hola **direcciones de correo electrónico de prueba**, escriba la dirección de correo electrónico del usuario de prueba de Hola. 
  
    b. Hola **emisor** cuadro de texto, hello de tipo dirección URL del emisor del proveedor de servicios de Hola. 
  
    c. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-teamseer-test-user"></a>Creación de un usuario de prueba de TeamSeer

toolog de los usuarios de Azure AD tooenable en tooTeamSeer, se les deben aprovisionar en tooShiftPlanning. En caso de hello de TeamSeer, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **TeamSeer** sitio de la empresa como administrador.

2. Lleve a cabo Hola pasos:
   
    ![Administración de RR. HH.](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Administración de RR. HH.")  
 
    a. Vaya demasiado**administración de recursos humanos \> usuarios**.
  
    b. Haga clic en **ejecutar el Asistente para nuevo usuario de hello**.

3. Hola **detalles del usuario** sección, lleve a cabo Hola pasos:
   
    ![Detalles del usuario](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Detalles del usuario")

    a. Hola de tipo **nombre**, **apellido**, **nombre de usuario (dirección de correo electrónico)** de una cuenta válida de AAD que desee tooprovision en toohello relacionados con cuadros de texto.
  
    b. Haga clic en **Siguiente**.

4. Siga hello en pantalla instrucciones para agregar un nuevo usuario y haga clic en **finalizar**.

>[!NOTE]
>Puede usar cualquier otra TeamSeer usuario cuenta herramienta de creación o las API proporcionadas por TeamSeer tooprovision cuentas de usuario de Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTeamSeer.

![Asignar usuario][200] 

**tooassign Britta Simon tooTeamSeer, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **TeamSeer**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

