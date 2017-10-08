---
title: "Tutorial: Integración de Azure Active Directory con Marketo | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Tutorial: integración de Azure Active Directory con Marketo

En este tutorial, aprenderá cómo toointegrate Marketo con Azure Active Directory (Azure AD).

Integración de Marketo con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooMarketo
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMarketo (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Marketo tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Marketo

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Marketo desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-marketo-from-hello-gallery"></a>Agregar Marketo desde la Galería de Hola
integración de hello tooconfigure de Marketo en Azure AD, deberá tooadd Marketo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Marketo desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Marketo**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. En el panel de resultados de hello, seleccione **Marketo**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Marketo con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Marketo es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Marketo debe toobe establecido.

En Marketo, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Marketo, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Marketo](#creating-a-marketo-test-user)**  -toohave un equivalente de Britta Simon en Marketo que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Marketo.

**inicio de sesión único en Azure AD tooconfigure con Marketo, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Marketo** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. En hello **Marketo dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://saml.marketo.com/sp`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico de Marketo](http://investors.marketo.com/contactus.cfm) tooget estos valores.
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. En hello **configuración de Marketo** sección, haga clic en **configurar Marketo** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. tooget Munchkin identificador de la aplicación, inicie sesión en tooMarketo usando credenciales de administrador y realizar las siguientes acciones:
   
    a. Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.
   
    b. Haga clic en hello **administración** botón en el panel de navegación superior de Hola.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegar por el menú de la integración de toohello y haga clic en hello **vínculo Munchkin**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    d. Copie Hola Id. de Munchkin mostrado en pantalla de bienvenida y completar la dirección URL de respuesta en el Asistente para configuración de hello Azure AD.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. Hola tooconfigure SSO en la aplicación hello, siga Hola pasos siguientes:
   
    a. Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.
   
    b. Haga clic en hello **administración** botón en el panel de navegación superior de Hola.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegar por el menú de la integración de toohello y haga clic en **Single Sign On**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    d. Hola tooenable configuración de SAML, haga clic en **editar** botón.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    e. Ya está la configuración de inicio de sesión único **habilitada**.
   
    f. Hola pegar **Id. de entidad SAML**, Hola **Id. del emisor** cuadro de texto.
   
    g. Hola **Id. de entidad** cuadro de texto, escriba la dirección URL de hello como `http://saml.marketo.com/sp`.
   
    h. Hola seleccione ubicación del identificador de usuario como **elemento de identificador de nombre**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Si el identificador de usuario no es el valor UPN, a continuación, cambiar el valor de hello en la pestaña del atributo Hola.
   
    i. Cargar certificado de hello, que ha descargado desde el Asistente para configuración de Azure AD. **Guardar** Hola configuración.
   
    j. Editar la configuración de redirección de páginas de Hola.
   
    k. Hola pegar **SAML Single Sign-On dirección URL del servicio** en hello **dirección URL de inicio de sesión** cuadro de texto.
   
    l. Hola pegar **dirección URL de cierre de sesión** en hello **Logout URL** cuadro de texto.
   
    m. Hola **URL del Error**, copia el **URL de la instancia de Marketo** y haga clic en **guardar** botón toosave configuración.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. tooenable Hola SSO para los usuarios, Hola completa siguientes acciones:
   
    a. Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.
   
    b. Haga clic en hello **administración** botón en el panel de navegación superior de Hola.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue toohello **seguridad** menú y haga clic en **configuración de inicio de sesión**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    d. Comprobar hello **requieren SSO** opción y **guardar** Hola configuración.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-marketo-test-user"></a>Creación de un usuario de prueba de Marketo

En esta sección, creará un usuario llamado Britta Simon en Marketo. Siga estos toocreate pasos un usuario en la plataforma de Marketo.

1. Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.

2. Haga clic en hello **administración** botón en el panel de navegación superior de Hola.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. Navegue toohello **seguridad** menú y haga clic en **a los usuarios y Roles**
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. Haga clic en hello **invitar a un nuevo usuario** vínculo en la ficha de usuarios de Hola
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. Hola Hola del relleno del Asistente de invitar a un nuevo usuario después de información
   
    a. Escriba Hola usuario **correo electrónico** dirección en el cuadro de texto de Hola
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    b. Escriba hello **nombre** en el cuadro de texto de Hola
   
    c. Escriba hello **Last Name** en el cuadro de texto de Hola
   
    d. Haga clic en **Siguiente**

6. Hola **permisos** ficha, seleccione hello **userRoles** y haga clic en **siguiente**
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. Haga clic en hello **enviar** botón invitación de usuario de hello toosend
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. Usuario recibe la notificación de correo electrónico de Hola y tiene tooclick Hola vincular y cambiar la cuenta de hello contraseña tooactivate Hola. 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMarketo.

![Asignar usuario][200] 

**tooassign Britta Simon tooMarketo, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Marketo**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Marketo Hola Hola Panel de acceso, deberá obtener aplicaciones de Marketo tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

