---
title: "Tutorial: integración de Azure Active Directory con ThousandEyes | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Tutorial: integración de Azure Active Directory con ThousandEyes

En este tutorial, aprenderá cómo toointegrate ThousandEyes con Azure Active Directory (Azure AD).

Integración ThousandEyes con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooThousandEyes
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooThousandEyes (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con ThousandEyes tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en ThousandEyes

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar ThousandEyes desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-thousandeyes-from-hello-gallery"></a>Agregar ThousandEyes desde la Galería de Hola
integración de hello tooconfigure de ThousandEyes en Azure AD, deberá tooadd ThousandEyes de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd ThousandEyes de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **ThousandEyes**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. En el panel de resultados de hello, seleccione **ThousandEyes**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con ThousandEyes con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ThousandEyes es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ThousandEyes debe toobe establecido.

En ThousandEyes, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con ThousandEyes, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de ThousandEyes](#creating-a-thousandeyes-test-user) ** -toohave un equivalente de Britta Simon en ThousandEyes que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación ThousandEyes.

**inicio de sesión único en Azure AD tooconfigure con ThousandEyes, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **ThousandEyes** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. En hello **ThousandEyes dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://app.thousandeyes.com/login/sso`

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. En hello **configuración de ThousandEyes** sección, haga clic en **configurar ThousandEyes** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en tooyour **ThousandEyes** sitio de la empresa como administrador.

8. En el menú de hello en la parte superior de hello, haga clic en **configuración**.
   
    ![Configuración](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Configuración")

9. Haga clic en **Cuenta**
   
    ![Cuenta](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Cuenta")

10. Haga clic en hello **seguridad y autenticación** ficha.
   
    ![Seguridad y autenticación](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Seguridad y autenticación")

11. Hola **el programa de instalación Single Sign-On** sección, lleve a cabo Hola pasos:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Configurar inicio de sesión único")
  
    a. Seleccione **Enable Single Sign-On**(Habilitar inicio de sesión único).
  
    b. En el cuadro de texto **IDP Login URL** (Dirección URL de inicio de sesión de IDP), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal.
  
    c. Copie el valor de **Sign-out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal en el cuadro de texto **Logout page URL** (Dirección URL de la página de cierre de sesión).
  
    d. En el cuadro de texto **Emisor de proveedor de identidades**, pegue el valor de **id. de entidad de SAML** que ha copiado de Azure Portal.
  
    e. En **certificado de comprobación**, haga clic en **Elegir archivo**y, a continuación, cargar el certificado de Hola que ha descargado desde el portal de Azure.
  
    f. Haga clic en **Guardar**.
 
> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-thousandeyes-test-user"></a>Creación de un usuario de prueba de ThousandEyes

En orden tooenable toolog de los usuarios de Azure AD en ThousandEyes, se les deben aprovisionar en ThousandEyes.  
En caso de hello de ThousandEyes, el aprovisionamiento es una tarea manual.

>[!NOTE]
>Puede usar cualquier otra ThousandEyes usuario cuenta herramienta de creación o las API proporcionadas por ThousandEyes tooprovision Azure Active Directory las cuentas de usuario.

**tooprovision un tooThousandEyes de cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en su sitio de la compañía de ThousandEyes como administrador.

2. Haga clic en **Configuración**.
   
    ![Configuración](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Configuración")

3. Haga clic en **Cuenta**.
   
    ![Cuenta](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Cuenta")

4. Haga clic en hello **cuentas y usuarios** ficha.
   
    ![Cuentas y usuarios](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Cuentas y usuarios")

5. Hola **agregar usuarios y cuentas** sección, lleve a cabo Hola pasos:
   
    ![Agregar cuentas de usuario](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Agregar cuentas de usuario")   
  
    a. En **nombre** cuadro de texto Nombre de usuario como Hola de tipo **Britta Simon**.

    b. En **correo electrónico** Hola de tipo de correo electrónico del usuario, cuadro de texto, como ** brittasimon@contoso.com **.
   
    b. Haga clic en **tooAccount Agregar nuevo usuario**.
      
     >[!NOTE]
     >obtendrá un correo electrónico con un vínculo tooconfirm y activar la cuenta de hello titular de la cuenta de Hello Azure Active Directory.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooThousandEyes.

![Asignar usuario][200] 

**tooassign Britta Simon tooThousandEyes, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ThousandEyes**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello ThousandEyes disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación ThousandEyes.

Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

