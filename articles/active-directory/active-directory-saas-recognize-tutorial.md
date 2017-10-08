---
title: "Tutorial: integración de Azure Active Directory con Recognize | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y reconocer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a>Tutorial: Integración de Azure Active Directory con Recognize

En este tutorial, aprenderá cómo reconocer toointegrate con Azure Active Directory (Azure AD).

Reconocer la integración con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooRecognize
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRecognize (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD tooconfigure con reconocer, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Recognize

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar reconocer desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-recognize-from-hello-gallery"></a>Agregar reconocer desde la Galería de Hola
integración de hello tooconfigure de reconocer en Azure AD, deberá tooadd reconocer de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd reconocer desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **reconocer**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. En el panel de resultados de hello, seleccione **reconocer**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Recognize con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en reconocer es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en reconocer debe toobe establecido.

En reconocer, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

prueba Azure AD y tooconfigure inicio de sesión único con reconocer, necesita hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de reconocer](#creating-a-recognize-test-user)**  -toohave un equivalente de Britta Simon en reconocer que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de reconocer.

**inicio de sesión único en Azure AD tooconfigure con reconocer, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **reconocer** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. En hello **reconocer dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://recognizeapp.com/<your-domain>/saml/sso`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://recognizeapp.com/<your-domain>`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente reconoce](mailto:support@recognizeapp.com) obtener la dirección URL de inicio de sesión y puede obtener el valor de identificador abriendo Hola dirección URL de metadatos del proveedor de servicio de la sección de configuración de SSO que se explica más adelante en el tutorial Hola Hola. . 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. En hello **reconocer configuración** sección, haga clic en **configurar reconocer** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. En una ventana del explorador web diferente, inicio de sesión tooyour reconocer inquilino como administrador.

8. En hello esquina superior derecha, haga clic en **menú**. Vaya demasiado**Administrador de la compañía**.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. En el panel de navegación izquierdo de hello, haga clic en **configuración**.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. Realizar Hola seguir pasos de **configuración de SSO** sección.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    a. En **Enable SSO** (Habilitar SSO), seleccione **ON** (Activado).

    b. Hola **Id. de entidad IDP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.
    
    c. Hola **dirección url de destino de Sso** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.
    
    d. Hola **dirección url de destino de Slo** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure. 
    
    e. Abra su descargado **certificado (Base64)** un archivo en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado** cuadro de texto.
    
    f. Haga clic en hello **Guardar configuración** botón. 

11. Al lado de hello **configuración de SSO** sección, copie la dirección URL de hello en **dirección url de metadatos del proveedor de servicio**.
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. Abra hello **vínculo de dirección URL de metadatos** en un documento de metadatos en blanco del explorador toodownload Hola. A continuación, copie Hola EntityDescriptor value(entityID) archivo hello y péguelo en **identificador** en el cuadro de texto **sección reconocer dominio y las direcciones URL** en el portal de Azure.
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-recognize-test-user"></a>Creación de un usuario de prueba de Recognize

En orden tooenable toolog de los usuarios de Azure AD en reconocer, se les deben aprovisionar en reconocer. En caso de hello de reconocer, el aprovisionamiento es una tarea manual.

Esta aplicación no admite el aprovisionamiento SCIM, pero tiene una sincronización de usuario alternativa que aprovisiona a los usuarios. 

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en su sitio de la compañía de Recognize como administrador.

2. En hello esquina superior derecha, haga clic en **menú**. Vaya demasiado**Administrador de la compañía**.

3. En el panel de navegación izquierdo de hello, haga clic en **configuración**.

4. Realizar Hola seguir pasos de **usuario sincronización** sección.
   
   ![Nuevo usuario](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Nuevo usuario")
   
   a. En **Sync Enabled** (Sincronización habilitada), seleccione **ON** (Activado).
   
   b. En **Choose sync provider** (Elegir proveedor de sincronización), seleccione **Microsoft/Office 365**.
   
   c. Haga clic en **Run User Sync** (Ejecutar sincronización de usuario).

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRecognize.

![Asignar usuario][200] 

**tooassign Britta Simon tooRecognize, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **reconocer**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de reconocer Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour reconocer aplicación. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

