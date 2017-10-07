---
title: "Tutorial: Integración de Azure Active Directory con Boomi | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Tutorial: Integración de Azure Active Directory con Boomi

En este tutorial, aprenderá cómo toointegrate Boomi con Azure Active Directory (Azure AD).

Integración de Boomi con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooBoomi
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBoomi (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Boomi tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Boomi

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de Boomi de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-boomi-from-hello-gallery"></a>Adición de Boomi de galería de Hola
integración de hello tooconfigure de Boomi en Azure AD, deberá tooadd Boomi de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Boomi de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Boomi**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. En el panel de resultados de hello, seleccione **Boomi**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Boomi con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Boomi es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Boomi debe toobe establecido.

En Boomi, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Boomi, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Boomi](#creating-a-boomi-test-user)**  -toohave un equivalente de Britta Simon en Boomi que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Boomi.

**inicio de sesión único en Azure AD tooconfigure con Boomi, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Boomi** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. En hello **Boomi dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://platform.boomi.com/sso/<accountname>/saml`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico de Boomi](https://boomi.com/company/contact/) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Aplicación de Boomi espera las aserciones de SAML de hello en un formato concreto. Configure Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, para cada fila se muestra en la tabla de Hola a continuación, realizar Hola pasos:

    | Nombre del atributo | Valor de atributo |
    | -------------- | --------------- |
    | FEDERATION_ID | user.mail |
    
    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.
    
    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.
    
    d. Haga clic en **Aceptar**.

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. En hello **configuración de Boomi** sección, haga clic en **configurar Boomi** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Boomi. 

9. Navegue demasiado**nombre de la compañía** y vaya demasiado**configurar**.

10. Haga clic en hello **opciones SSO** ficha y realice los pasos siguientes.

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Marque la casilla **Enable SAML Single Sign-On** (Habilitar el inicio de sesión único de SAML).

    b. Haga clic en **importación** hello tooupload descarga certificado de Azure AD demasiado**certificado del proveedor de identidad**.
    
    c. Hola **URL de inicio de sesión del proveedor de identidades** cuadro de texto, coloque valor Hola de **SAML Single Sign-On dirección URL del servicio** desde la ventana de configuración de aplicación de Azure AD.

    d. Como **ubicación del identificador de federación**, seleccione el botón de radio **Federation Id is in FEDERATION_ID Attribute element** (El id. de federación está en el elemento de atributo FEDERATION_ID). 

    e. Haga clic en el botón **Guardar** .

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-boomi-test-user"></a>Creación de un usuario de prueba de Boomi

En orden tooenable toolog de los usuarios de Azure AD en tooBoomi, se les deben aprovisionar en Boomi. En caso de hello de Boomi, el aprovisionamiento es una tarea manual.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision una cuenta de usuario, lleve a cabo Hola pasos:

1. Inicie sesión en tooyour sitio Boomi de su compañía como administrador.

2. Después de iniciar sesión, navegar demasiado**administración de usuarios** y vaya demasiado**usuarios**.

    ![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuarios")

3. Haga clic en  **+**  hello e icono **agregar y mantener los Roles de usuario** abre el cuadro de diálogo.

    ![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuarios")

    ![Usuarios](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuarios")

    a. Hola **dirección de correo electrónico del usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como BrittaSimon@contoso.com.
    
    b. Hola **nombre** cuadro de texto, tipo hello nombre de usuario como Bárbara.

    c. Hola **apellidos** cuadro de texto, escriba Hola apellidos del usuario como Simon.
    
    d. Escriba del usuario de hello **identificador de federación**. Cada usuario debe tener un identificador de federación que identifica de forma única usuario Hola dentro de la cuenta de hello.
    
    e. Asignar Hola **usuario estándar** usuario toohello de rol. No se debe asignar el rol de administrador de hello porque dispondría de invertir el acceso normal de ambiente, así como acceso de inicio de sesión único.
    
    f. Haga clic en **Aceptar**.
    
    > [!NOTE]
    > usuario de Hello no recibirá un correo electrónico de bienvenida de notificación que contiene una contraseña que puede ser utilizado toolog en toohello AtomSphere cuenta porque su contraseña se administra a través del proveedor de identidades de Hola. Puede usar cualquier otra Boomi usuario cuenta herramienta de creación o las API proporcionadas por Boomi tooprovision cuentas de usuario AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBoomi.

![Asignar usuario][200] 

**tooassign Britta Simon tooBoomi, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Boomi**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Boomi de Hola Hola Panel de acceso, deberá obtener aplicaciones de Boomi de tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

