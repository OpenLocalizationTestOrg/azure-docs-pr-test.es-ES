---
title: "Tutorial: Integración de Azure Active Directory con Dropbox for Business | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Dropbox para empresas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Tutorial: Integración de Azure Active Directory con Dropbox para Empresas

En este tutorial, aprenderá cómo toointegrate Dropbox para empresas con Azure Active Directory (Azure AD).

Integración de Dropbox para empresas con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooDropbox para la empresa
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooDropbox para la empresa (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Dropbox para empresas, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción a Dropbox for Business con inicio de sesión único habilitado.

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de Dropbox para empresas de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Adición de Dropbox para empresas de galería de Hola
integración de hello tooconfigure de Dropbox para empresas en Azure AD, necesita tooadd Dropbox para empresas de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Dropbox para empresas de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Dropbox para empresas**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. En el panel de resultados de hello, seleccione **Dropbox para empresas**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con Dropbox for Business con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Dropbox para empresas es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Dropbox para empresas necesita toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Dropbox para empresas.

tooconfigure y prueba de inicio de sesión único en Azure AD con Dropbox para empresas, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear una lista desplegable para el usuario de prueba empresarial](#creating-a-dropbox-for-business-test-user)**  -toohave un equivalente de Britta Simon en Dropbox para empresas que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en Dropbox para aplicaciones de negocios.

**inicio de sesión único en tooconfigure Azure AD con Dropbox para empresas, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Dropbox para empresas** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. En hello **Dropbox para el dominio de negocio y las direcciones URL** sección, lleve a cabo Hola pasos:

    a. Inicie sesión en tooyour Dropbox para el inquilino de negocios. 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurar inicio de sesión único")
   
    b. En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **consola de administración de**. 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurar inicio de sesión único")
   
    c. En hello **consola de administración de**, haga clic en **autenticación** en el panel de navegación izquierdo de Hola. 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurar inicio de sesión único")
   
    d. Hola **inicio de sesión único** sección, seleccione **habilitar inicio de sesión único**y, a continuación, haga clic en **más** tooexpand en esta sección.  
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurar inicio de sesión único")
   
    e. Copiar dirección URL de Hola a continuación demasiado**a los usuarios pueden iniciar sesión escribiendo su dirección de correo electrónico o pueden ir directamente a**. 
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. En el portal de Azure, en Hola Hola **dirección URL de inicio de sesión** cuadro de texto dirección URL de Hola de pegar.

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Este valor no es real. Actualice el valor de hello con hello sesión URL real se obtiene de su sección de inicio de sesión único. Póngase en contacto con [Dropbox para el equipo de soporte técnico de cliente empresarial](https://www.dropbox.com/business/contact) tooget este valor. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. En hello **Dropbox para configuración de negocios** sección, haga clic en **configurar Dropbox para empresas** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure inicio de sesión único en **Dropbox para empresas** en paralelo, vaya el inquilino Dropbox para empresas, Hola **inicio de sesión único** sección de hello **autenticación** página, lleve a cabo Hola pasos: 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurar inicio de sesión único")
   
    a. Haga clic en **Required**(Obligatorio).
   
    b. En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **dirección URL de inicio de sesión** cuadro de texto.

    c. Haga clic en **Seleccionar certificado**y, a continuación, busque tooyour **archivo de certificado codificado en Base64**.

    d. Haga clic en **guardar cambios** toocomplete configuración de hello en el inquilino DropBox para empresas.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Creación de un usuario de prueba de Dropbox for Business

En esta sección, creará un usuario llamado a Britta Simon en Dropbox for Business. Dropbox for Business admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

No hay ningún elemento de acción para usted en esta sección. Si un usuario ya no existe en Dropbox para empresas, se crea uno nuevo cuando intente tooaccess Dropbox para empresas.

>[!Note]
>Si necesita toocreate manualmente, póngase en contacto con en un usuario [Dropbox para el equipo de soporte técnico de cliente empresarial](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooDropbox para la empresa.

![Asignar usuario][200] 

**tooassign Britta Simon tooDropbox para la empresa, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Dropbox para empresas**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Dropbox de icono de negocios en el Panel de acceso de hello, obtendrá la página de inicio de sesión de la lista desplegable para aplicaciones de negocios.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

