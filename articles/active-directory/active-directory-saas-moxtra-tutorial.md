---
title: "Tutorial: Integración de Azure Active Directory con Moxtra | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Tutorial: Integración de Azure Active Directory con Moxtra

En este tutorial, aprenderá cómo toointegrate Moxtra con Azure Active Directory (Azure AD).

Integración Moxtra con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooMoxtra
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMoxtra (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Moxtra tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Moxtra

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Moxtra desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-moxtra-from-hello-gallery"></a>Agregar Moxtra desde la Galería de Hola
integración de hello tooconfigure de Moxtra en Azure AD, deberá tooadd Moxtra de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Moxtra de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Moxtra**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. En el panel de resultados de hello, seleccione **Moxtra**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Moxtra con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Moxtra es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Moxtra debe toobe establecido.

En Moxtra, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Moxtra, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Moxtra](#creating-a-moxtra-test-user)**  -toohave un equivalente de Britta Simon en Moxtra que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Moxtra.

**inicio de sesión único en Azure AD tooconfigure con Moxtra, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Moxtra** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. En hello **Moxtra dominio y las direcciones URL** sección, lleve a cabo Hola siguiendo el paso:

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://www.moxtra.com/service/#login`

4. Aplicación de Moxtra espera las aserciones de SAML de hello en un formato concreto. Configurar Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones. Hola siguiente captura de pantalla muestra un ejemplo de esta configuración. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos:
    
    | Nombre del atributo | Valor de atributo |
    | ------------------- | -------------------- |    
    | firstname | user.givenname |
    | lastname | user.surname |
    | idpid    | < SAML Entity ID > 

    > [!Note]
    > Hola valo **idpid** atributo no es real. Puede obtener valor real de Hola de **referencia rápida** sección bajo **Moxtra configuración**.
    
    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.

    d. Haga clic en **Aceptar**.
    
5. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. En hello **Moxtra configuración** sección, haga clic en **configurar Moxtra** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour Moxtra como administrador.

9. En la barra de herramientas de Hola Hola izquierda, haga clic en **consola de administración > SAML Single Sign-on**y, a continuación, haga clic en **nuevo**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. En hello **SAML** , siga los pasos de hello:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: *SAML*). 
  
    b. Hola **Id. de entidad IdP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure. 
 
    c. En **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure. 
 
    d. Hola **AuthnContextClassRef** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:ac:classes:Password**. 
 
    e. Hola **NameID Format** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**. 
 
    f. Abrir el certificado que ha descargado desde el portal de Azure en el Bloc de notas, copie el contenido de hello y, a continuación, péguelo en hello **certificado** cuadro de texto.    
 
    g. En el cuadro de dominio de correo electrónico SAML de hello, escriba el dominio de correo electrónico SAML.    
  
    >[!NOTE]
    >dominio de toosee Hola pasos tooverify hello, haga clic en hello "****" a continuación.

    h. Haga clic en **Update**(Actualizar).

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-moxtra-test-user"></a>Creación de un usuario de prueba de Moxtra

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Moxtra toocreate.

**toocreate un usuario llamado Britta Simon en Moxtra, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour Moxtra sitio de su compañía como administrador.

2. En la barra de herramientas de Hola Hola izquierda, haga clic en **consola de administración > Administración de usuarios**y, a continuación, **Agregar usuario**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. En hello **Agregar usuario** cuadro de diálogo, realizar Hola pasos:
  
    a. Hola **nombre** cuadro de texto, tipo **Bárbara**.
  
    b. Hola **Last Name** cuadro de texto, tipo **Simon**.
  
    c. Hola **correo electrónico** cuadro de texto, tipo de Bárbara dirección de correo electrónico igual que en el portal de Azure.
  
    d. Hola **división** cuadro de texto, tipo **desarrollo**.
  
    e. Hola **departamento** cuadro de texto, tipo **TI**.
  
    f. Seleccione **Administrator** (Administrador).
  
    g. Haga clic en **Agregar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMoxtra.

![Asignar usuario][200] 

**tooassign Britta Simon tooMoxtra, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Moxtra**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Moxtra Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Moxtra aplicación.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

