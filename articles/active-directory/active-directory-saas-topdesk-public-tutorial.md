---
title: "Tutorial: integración de Azure Active Directory con TOPdesk - Public | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Active Directory de Azure y TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Tutorial: Integración de Azure Active Directory con TOPdesk - Public

En este tutorial, aprenderá cómo toointegrate TOPdesk - Public con Azure Active Directory (Azure AD).

Integración de TOPdesk - Public con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTOPdesk - público.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTOPdesk - Public (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con TOPdesk - Public, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en TOPdesk - Public

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar TOPdesk - Public de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-topdesk---public-from-hello-gallery"></a>Agregar TOPdesk - Public de galería de Hola
integración de hello tooconfigure de TOPdesk - Public en Azure AD, deberá tooadd TOPdesk - Public de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd TOPdesk - Public de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **TOPdesk - Public**, seleccione **TOPdesk - Public** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Lista de resultados de TOPdesk - Public Hola](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TOPdesk - Public con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TOPdesk - Public es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TOPdesk - Public debe toobe establecido.

En TOPdesk - Public, asignar Hola valo hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y probar el inicio de sesión único en Azure AD con TOPdesk - Public, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba pública de TOPdesk -](#create-a-topdesk---public-test-user)**  - toohave un equivalente de Britta Simon en TOPdesk - Public que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación TOPdesk - Public.

**tooconfigure inicio de sesión único en Azure AD con TOPdesk - Public, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **TOPdesk - Public** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. En hello **TOPdesk - dominio público y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.topdesk.net`
    
    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. La dirección URL de respuesta se explica más adelante en el tutorial. Póngase en contacto con [TOPdesk - equipo de soporte técnico de cliente público](https://help.topdesk.com/saas/enterprise/user/) tooget estos valores.  

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. En hello **TOPdesk - Public Configuration** sección, haga clic en **configurar TOPdesk - Public** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Inicio de sesión tooyour **TOPdesk - Public** sitio de la empresa como administrador.

8. Hola **TOPdesk** menú, haga clic en **configuración**.
   
    ![Configuración](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configuración")

9. Haga clic en **Login Settings**(Configuración de inicio de sesión).
   
    ![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configuración de inicio de sesión")

10. Expanda hello **configuración de inicio de sesión** menú y, a continuación, haga clic en **General**.
   
    ![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")

11. Hola **público** sección de hello **inicio de sesión SAML** configuración sección, lleve a cabo Hola pasos:
   
    ![Configuración técnica](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configuración técnica")
   
    a. Haga clic en **descargar** toodownload Hola archivo de metadatos públicos y, a continuación, guardarlo localmente en el equipo.
   
    b. Abrir archivo de metadatos de hello descargado y, a continuación, busque hello **AssertionConsumerService** nodo.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Hola copia **AssertionConsumerService** valor, pegue este valor en hello **dirección URL de respuesta** en el cuadro de texto **TOPdesk - dominio público y las direcciones URL** sección.      
   
12. toocreate un archivo de certificado, lleve a cabo Hola pasos:
    
    ![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")
    
    a. Abra Hola descarga archivo de metadatos desde el portal de Azure.
    
    b. Expanda hello **RoleDescriptor** nodo que tenga un **xsi: Type** de **fed: ApplicationServiceType**.
    
    c. Copiar valor de Hola de hello **X509Certificate** nodo.
    
    d. Hola Guardar copia **X509Certificate** valor localmente en el equipo en un archivo.

13. Hola **público** sección, haga clic en **agregar**.
    
    ![Inicio de sesión SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Inicio de sesión SAML")

14. En hello **Asistente de configuración de SAML** cuadro de diálogo, siga los pasos de hello:
    
    ![Asistente para configuración de SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Asistente de configuración de SAML")
    
    a. tooupload los metadatos descargados de archivos desde el portal de Azure, en **metadatos de federación**, haga clic en **examinar**.

    b. tooupload archivo su certificado, en **certificado (RSA)**, haga clic en **examinar**.

    c. que se obtuvo al equipo de soporte técnico de TOPdesk hello, en el archivo de logotipo de hello tooupload **icono del logotipo de**, haga clic en **examinar**.

    d. Hola **atributo de nombre de usuario** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. Hola **nombre para mostrar** cuadro de texto, escriba un nombre para la configuración.

    f. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-a-topdesk---public-test-user"></a>Creación de un usuario de prueba de TOPdesk - Public

En orden tooenable Azure AD a los usuarios toolog en TOPdesk - Public, se les deben aprovisionar en TOPdesk - Public.  
En caso de hello de TOPdesk - Public, el aprovisionamiento es una tarea manual.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamiento de usuario, realizar Hola pasos:
1. Inicio de sesión tooyour **TOPdesk - Public** como administrador.

2. En el menú de hello en la parte superior de hello, haga clic en **TOPdesk \> New \> archivos auxiliares \> persona**.
   
    ![Persona](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Persona")

3. En el cuadro de diálogo de hello nueva persona, realice Hola pasos:
   
    ![Nueva persona](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nueva persona")
   
    a. Haga clic en la ficha General de Hola.

    b. Hola **apellido** cuadro de texto, escriba el apellido del usuario de hello como Simon
 
    c. Seleccione un **sitio** de cuenta de hello.
 
    d. Haga clic en **Guardar**.

> [!NOTE]
> Puede usar cualquier otra TOPdesk - herramienta de creación de cuentas de usuario público o las API proporcionadas por TOPdesk - cuentas de usuario de tooprovision pública de Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTOPdesk - público.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooTOPdesk - Public, realizar Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **TOPdesk - Public**.

    ![Hello TOPdesk - Public vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello TOPdesk - Public disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour TOPdesk - Public aplicación.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

