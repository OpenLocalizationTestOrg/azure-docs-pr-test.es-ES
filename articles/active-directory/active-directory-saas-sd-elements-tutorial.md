---
title: "Tutorial: Integración de Azure Active Directory con SD Elements | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y los elementos de SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a>Tutorial: Integración de Azure Active Directory con SD Elements

En este tutorial, aprenderá cómo toointegrate elementos SD con Azure Active Directory (Azure AD).

Integrar los elementos de SD con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSD elementos
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión con tooSD elementos (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con elementos de SD tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en SD Elements

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de SD de elementos de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sd-elements-from-hello-gallery"></a>Adición de SD de elementos de galería de Hola
integración de hello tooconfigure de elementos de SD en Azure AD, deberá tooadd SD elementos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SD elementos de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **SD elementos**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. En el panel de resultados de hello, seleccione **SD elementos**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SD Elements con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en elementos de SD es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en elementos de SD debe toobe establecido.

SD de elementos, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con elementos de SD, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de elementos de SD](#creating-a-sd-elements-test-user)**  -toohave un equivalente de Britta Simon en elementos de SD es representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de elementos de SD.

**inicio de sesión único en tooconfigure Azure AD con elementos de SD, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **SD elementos** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. En hello **SD elementos dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.sdelements.com/sso/saml2/metadata`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenantname>.sdelements.com/sso/saml2/acs/`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico de los elementos de SD](mailto:support@sdelements.com) tooget estos valores.

4. Aplicación de elementos de SD espera las aserciones de SAML de hello en un formato concreto. Configurar Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de hello **"Atributo de usuario"** pestaña de aplicación hello. Hola siguiente captura de pantalla muestra un ejemplo de esto.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de Hola y realizar Hola pasos: 

    | Nombre del atributo | Valor de atributo |
    | --- | --- |
    | email |user.mail |
    | firstname |user.givenname |
    | lastname |user.surname |

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.

    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.

    d. Haga clic en **Aceptar**.
 
6. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. En hello **SD elementos de configuración** sección, haga clic en **configurar elementos de SD** tooopen **configurar inicio de sesión** ventana. Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. tooget inicio de sesión único habilitado, póngase en contacto con su [equipo de soporte técnico SD elementos](mailto:support@sdelements.com) y proporcióneles con archivo de certificado descargado hello. 

10. En otra ventana del explorador, inquilino de SD elementos tooyour inicio de sesión como administrador.

11. En el menú de hello en la parte superior de hello, haga clic en **System**y, a continuación, **Single Sign-on**. 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. En hello **configuración de inicio de sesión único** cuadro de diálogo, realizar Hola pasos:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    a. Como **Tipo de inicio de sesión único**, seleccione **SAML**.
   
    b. Hola **Id. de entidad de proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure. 
   
    c. Hola **servicio proveedor de identidad Single Sign-On** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure. 
   
    d. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-sd-elements-test-user"></a>Creación de un usuario de prueba de SD Elements

objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en elementos de SD. En caso de hello de SD elementos, la creación de elementos de SD usuarios es una tarea manual.

**toocreate Britta Simon SD de elementos, lleve a cabo Hola pasos:**

1. En una ventana del explorador web, sitio de la empresa de inicio de sesión tooyour SD elementos como administrador.

2. En el menú de hello en la parte superior de hello, haga clic en **administración de usuarios**y, a continuación, **usuarios**.
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. Haga clic en **Add New User**(Agregar nuevo usuario).
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. En hello **Agregar nuevo usuario** cuadro de diálogo, realizar Hola pasos:
   
    ![Creación de un usuario de prueba de SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    a. Hola **correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .
   
    b. Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **Bárbara**.
   
    c. Hola **Last Name** cuadro de texto, escriba Hola último nombre de usuario como **Simon**.
   
    d. Como **Rol**, seleccione **Usuario**. 
   
    e. Haga clic en **Crear usuario**.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSD elementos.

![Asignar usuario][200] 

**tooassign Britta Simon tooSD elementos, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **SD elementos**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.
  
Al hacer clic en hello SD elementos disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación SD elementos.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

