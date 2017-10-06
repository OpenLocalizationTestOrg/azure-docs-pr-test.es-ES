---
title: "Tutorial: integración de Azure Active Directory con Egnyte | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Tutorial: integración de Azure Active Directory con Egnyte

En este tutorial, aprenderá cómo toointegrate Egnyte con Azure Active Directory (Azure AD).

Integración de Egnyte con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooEgnyte
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEgnyte (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Egnyte tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Egnyte

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Egnyte desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-egnyte-from-hello-gallery"></a>Agregar Egnyte desde la Galería de Hola
integración de hello tooconfigure de Egnyte en Azure AD, deberá tooadd Egnyte de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Egnyte de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Egnyte**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. En el panel de resultados de hello, seleccione **Egnyte**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Egnyte con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Egnyte es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Egnyte debe toobe establecido.

En Egnyte, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Egnyte, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Creación de un usuario de prueba de Egnyte](#creating-an-egnyte-test-user)**  -toohave un equivalente de Britta Simon en Egnyte que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Egnyte.

**inicio de sesión único en Azure AD tooconfigure con Egnyte, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Egnyte** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. En hello **Egnyte dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Este valor no es real. Actualice este valor con hello dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de cliente de Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget este valor. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. En hello **configuración de Egnyte** sección, haga clic en **configurar Egnyte** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa tooyour como administrador.

8. Haga clic en **Configuración**.
   
   ![Configuración](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Configuración")

9. En el menú de hello, haga clic en **configuración**.

   ![Configuración](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Configuración")

10. Haga clic en hello **configuración** ficha y, a continuación, haga clic en **seguridad**.

    ![Seguridad](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Seguridad")

11. Hola **autenticación de inicio de sesión único** sección, lleve a cabo Hola pasos:

    ![Autenticación de inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Autenticación de inicio de sesión único")   
    
    a. En **Autenticación de inicio de sesión único**, seleccione **SAML 2.0**.
   
    b. En **Proveedor de identidades**, seleccione **AzureAD**.
   
    c. Pegar **SAML Single Sign-On dirección URL del servicio** copiados desde el portal de Azure en hello **URL de inicio de sesión del proveedor de identidades** cuadro de texto.
   
    d. Pegar **Id. de entidad SAML** que haya copiado desde el portal de Azure en hello **Id. de entidad de proveedor de identidad** cuadro de texto.
      
    e. Abra el certificado codificado en base 64 en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado del proveedor de identidad** cuadro de texto.
   
    f. En **Asignación de usuario predeterminada**, seleccione **Dirección de correo electrónico**.
   
    g. En **Usar valor de emisor específico del dominio**, seleccione **Deshabilitado**.
   
    h. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-an-egnyte-test-user"></a>Creación de un usuario de prueba de Egnyte

toolog de los usuarios de Azure AD tooenable en tooEgnyte, se les deben aprovisionar en Egnyte. En caso de hello de Egnyte, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**

1. Inicie sesión en tooyour **Egnyte** como administrador.

2. Vaya demasiado**configuración \> usuarios y grupos**.

3. Haga clic en **Agregar nuevo usuario**y, a continuación, seleccione el tipo de saludo del usuario que desea tooadd.
   
   ![Usuarios](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Usuarios")

4. Hola **nuevo usuario estándar** sección, lleve a cabo Hola pasos:
   
   ![Nuevo usuario estándar](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Nuevo usuario estándar")   

   a. Hola de tipo **correo electrónico**, **nombre de usuario**y otros detalles de una cuenta válida de Azure Active Directory que desee tooprovision.
   
   b. Haga clic en **Guardar**.
    
    >[!NOTE]
    >titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico de notificación.
    >

>[!NOTE]
>Puede usar cualquier otra Egnyte usuario cuenta herramienta de creación o las API proporcionadas por Egnyte tooprovision cuentas de usuario AAD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEgnyte.

![Asignar usuario][200] 

**tooassign Britta Simon tooEgnyte, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Egnyte**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Egnyte Hola Hola Panel de acceso, deberá obtener aplicaciones de Egnyte tooyour automáticamente ha iniciado sesión.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

