---
title: "Tutorial: integración de Azure Active Directory con Samanage | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Tutorial: integración de Azure Active Directory con Samanage

En este tutorial, aprenderá cómo toointegrate Samanage con Azure Active Directory (Azure AD).

Integración de Samanage con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSamanage
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSamanage (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Samanage tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Samanage

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Samanage desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-samanage-from-hello-gallery"></a>Agregar Samanage desde la Galería de Hola
integración de hello tooconfigure de Samanage en Azure AD, deberá tooadd Samanage de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Samanage de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Samanage**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. En el panel de resultados de hello, seleccione **Samanage**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Samanage con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Samanage es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Samanage debe toobe establecido.

En Samanage, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Samanage, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Samanage](#creating-a-samanage-test-user)**  -toohave un equivalente de Britta Simon en Samanage que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Samanage.

**inicio de sesión único en tooconfigure Azure AD con Samanage, realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **Samanage** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. En hello **Samanage dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador, que se explica más adelante en el tutorial Hola. Para más información, póngase en contacto con [equipo de soporte al cliente de Samanage](https://www.samanage.com/support).    
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. En hello **configuración de Samanage** sección, haga clic en **configurar Samanage** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y el Id. de entidad SAML** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Samanage como administrador.

8. Haga clic en **Dashboard** (Panel) y seleccione **Setup** (Configuración) en el panel de navegación izquierdo.
   
    ![Panel](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Panel")

9. Haga clic en **Inicio de sesión único**.
   
    ![Inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Inicio de sesión único")

10. Navegue demasiado**inicio de sesión con SAML** sección, lleve a cabo Hola pasos:
   
    ![Inicio de sesión con SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Inicio de sesión con SAML")
 
    a. Haga clic en **Enable Single Sign-On with SAML**(Habilitar inicio de sesión único con SAML).  
 
    b. Hola **dirección URL del proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.    
 
    c. Confirmar hello **dirección URL de inicio de sesión** coincidencias hello **dirección URL de inicio de sesión** de **Samanage dominio y las direcciones URL** sección en el portal de Azure.
 
    d. Hola **Logout URL** cuadro de texto, escriba el valor de Hola de **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.
 
    e. Hola **emisor SAML** textbox, identificador de aplicación de tipo Hola URI establecido en el proveedor de identidad.
 
    f. Abra el certificado codificado en base 64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **pegar su certificado a continuación de proveedor de identidades x.509** cuadro de texto.
 
    g. Haga clic en **Create users if they do not exist in Samanage**(Crear usuarios si no existen en Samanage).
 
    h. Haga clic en **Update**(Actualizar).

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-samanage-test-user"></a>Creación de un usuario de prueba en Samanage

toolog de los usuarios de Azure AD tooenable en tooSamanage, se les deben aprovisionar en Samanage.  
En caso de hello de Samanage, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en su sitio de la compañía de Samanage como administrador.

2. Haga clic en **Dashboard** (Panel) y seleccione **Setup** (Configuración) en el panel de navegación izquierdo.
   
    ![Instalación](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Instalación")

3. Haga clic en hello **usuarios** ficha
   
    ![Usuarios](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Usuarios")

4. Haga clic en **Nuevo usuario**.
   
    ![Nuevo usuario](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nuevo usuario")

5. Hola de tipo **nombre** hello y **dirección de correo electrónico** de una cuenta de Azure Active Directory que desee tooprovision y haga clic en **crear usuario**.
   
    ![Creación de usuarios](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Creación de usuarios")
   
   >[!NOTE]
   >titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla. Puede usar cualquier otra Samanage usuario cuenta herramienta de creación o las API proporcionadas por Samanage tooprovision Azure Active Directory las cuentas de usuario.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSamanage.

![Asignar usuario][200] 

**tooassign Britta Simon tooSamanage, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Samanage**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Samanage Hola Hola Panel de acceso, deberá obtener aplicaciones de Samanage tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

