---
title: "Tutorial: integración de Azure Active Directory con Wdesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a>Tutorial: integración de Azure Active Directory con Wdesk

En este tutorial, aprenderá cómo toointegrate Wdesk con Azure Active Directory (Azure AD).

Integración Wdesk con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooWdesk
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWdesk (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte. [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Wdesk tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Wdesk

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Wdesk desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-wdesk-from-hello-gallery"></a>Agregar Wdesk desde la Galería de Hola
integración de hello tooconfigure de Wdesk en Azure AD, deberá tooadd Wdesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Wdesk de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Wdesk**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. En el panel de resultados de hello, seleccione **Wdesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Wdesk con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Wdesk es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Wdesk debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Wdesk.

tooconfigure y prueba de inicio de sesión único en Azure AD con Wdesk, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Wdesk](#creating-a-wdesk-test-user) ** -toohave un equivalente de Britta Simon en Wdesk que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Wdesk.

**inicio de sesión único en Azure AD tooconfigure con Wdesk, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Wdesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. En hello **Wdesk dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado realiza Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`

4. Active **Mostrar configuración avanzada de URL**. Si desea que aplicación de hello tooconfigure en **SP** inicia el modo, realizar Hola siguiendo el paso:

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`
     
    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. Estos valores se obtienen de portal WDesk al configurar Hola SSO. 
  
5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. En una ventana del explorador web diferente, tooWdesk de inicio de sesión como un administrador de seguridad.

8. En hello parte inferior izquierda, haga clic en **administración** y elija **Administrador de la cuenta**:
 
     ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. En Wdesk administrador, navegue demasiado**seguridad**, a continuación, **SAML** > **configuración SAML**:

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. En **configuración General**, comprobar hello **habilitar SAML Single Sign On**:

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. En **detalles del proveedor de servicio**, realizar Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      a. Hola copia **dirección URL de inicio de sesión** y péguelo en **dirección Url de inicio de sesión** cuadro de texto en el portal de Azure.
   
      b. Hola copia **dirección Url de metadatos** y péguelo en **identificador** cuadro de texto en el portal de Azure.
       
      c. Hola copia **dirección url de consumidor** y péguelo en **dirección Url de respuesta** cuadro de texto en el portal de Azure.
   
      d. Haga clic en **guardar** sobre los cambios de hello toosave de portal de Azure.      

12. Haga clic en **configurar opciones de IdP** tooopen **modificar configuración de IdP** cuadro de diálogo. Haga clic en **Elegir archivo** toolocate hello **Metadata.xml** archivo que guardó en el portal de Azure, a continuación, cargarlo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. Haga clic en **Guardar cambios**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-wdesk-test-user"></a>Creación de usuario de prueba de Wdesk

toolog de los usuarios de Azure AD tooenable en tooWdesk, se les deben aprovisionar en Wdesk. En el caso de Wdesk, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooWdesk como un administrador de seguridad.
2. Navegue demasiado**administración** > **Administrador de la cuenta**.

     ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. Haga clic en **Members** (Miembros) en **People** (Contactos).

4. Ahora haga clic en **Agregar miembro** tooopen **Agregar miembro** cuadro de diálogo. 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. En **usuario** texto cuadro, escriba el nombre de usuario de saludo del usuario como ** brittasimon@contoso.com ** y haga clic en **continuar** botón.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  Especifique los detalles de hello tal y como se muestra a continuación:
  
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    a. En **correo electrónico** texto cuadro, escriba el correo electrónico de saludo del usuario como ** brittasimon@contoso.com **.

    b. En **nombre** texto cuadro, escriba Hola nombre de usuario como **Bárbara**.

    c. En **Last Name** texto cuadro, escriba Hola último nombre de usuario como **Simon**.

7. Haga clic en el botón **Save Member** (Guardar miembro).  

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWdesk.

![Asignar usuario][200] 

**tooassign Britta Simon tooWdesk, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Wdesk**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Wdesk Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Wdesk aplicación.
Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

