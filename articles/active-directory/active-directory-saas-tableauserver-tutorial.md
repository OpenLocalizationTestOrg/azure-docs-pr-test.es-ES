---
title: "Tutorial: Integración de Azure Active Directory con Tableau Server | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el servidor de una plantilla."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>Tutorial: Integración de Azure Active Directory con Tableau Server

En este tutorial, aprenderá cómo toointegrate Server Tableau con Azure Active Directory (Azure AD).

Integración Tableau servidor con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTableau Server
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTableau Server (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con el servidor de Tableau, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Tableau Server

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar servidor de una plantilla de la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-tableau-server-from-hello-gallery"></a>Agregar servidor de una plantilla de la Galería de Hola
integración de hello tooconfigure de Tableau Server en Azure AD, deberá tooadd Server de una plantilla de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Tableau Server desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Tableau Server**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. En el panel de resultados de hello, seleccione **Tableau Server**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Tableau Server con un usuario de prueba llamado Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el servidor de Tableau es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Tableau Server necesita toobe establecido.

En el servidor de Tableau, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con el servidor de una plantilla, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de servidor Tableau](#creating-a-tableau-server-test-user)**  -toohave un equivalente de Britta Simon en servidor Tableau representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de servidor de una plantilla.

**inicio de sesión único en tooconfigure Azure AD con el servidor de Tableau, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Tableau Server** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. En hello **Tableau dominio del servidor y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://azure.<domain name>.link`
    
    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://azure.<domain name>.link`

    c. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > Hello valores anteriores no son valores reales. Posteriormente, actualizar valores de hello con dirección URL real de Hola y el identificador de página de configuración del servidor de una plantilla de Hola. 

4. Aplicación de servidor tableau espera las aserciones de SAML de hello en un formato concreto. Configurar Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de hello **"Atributos de usuario"** sección en la página de integración de aplicaciones. Hello captura de pantalla siguiente muestra un ejemplo de Hola mismo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:
    
    | Nombre del atributo | Valor de atributo |
    | ---------------| --------------- |    
    | nombre de usuario | *user.displayname* |

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.
    
    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.
    
    d. Haga clic en **Aceptar**.


6. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. Haga clic en el botón **Guardar**.

    ![Configuración del inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget configurado para la aplicación de SSO, debe a inquilino de Tableau Server tooyour toosign la sesión como administrador.
   
   a. En configuración del servidor de una plantilla de hello, haga clic en hello **SAML** ficha.
  
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. Casilla de Hola de **Use SAML para inicio de sesión único**.
   
   c. Dirección URL de retorno de servidor tableau: Hola dirección URL que accederá los usuarios del servidor de una plantilla, por ejemplo, http://tableau_server. No se recomienda usar http://localhost. No se permite usar una dirección URL con una barra diagonal final (por ejemplo, http://servidor_de_tableau/). Copia **Tableau servidor la dirección URL de retorno** y péguelo tooAzure AD **dirección URL de inicio de sesión** en el cuadro de texto **Tableau dominio del servidor y las direcciones URL** sección.
   
   d. Id. de entidad SAML: Id. de entidad de hello identifica de forma única el toohello de instalación de servidor Tableau IdP. Aquí puede especificar la dirección URL del servidor Tableau nuevo, si lo desea, pero no tiene toobe la dirección URL del servidor Tableau. Copia **Id. de entidad SAML** y péguelo tooAzure AD **identificador** en el cuadro de texto **Tableau dominio del servidor y las direcciones URL** sección.
     
   e. Haga clic en hello **Exportar archivo de metadatos** y ábralo en la aplicación de editor de texto hello. Busque la dirección URL del servicio de consumidor de aserción con Http Post y el índice 0 y copiar dirección URL de Hola. Ahora pega tooAzure AD **dirección URL de respuesta** en el cuadro de texto **Tableau dominio del servidor y las direcciones URL** sección.
   
   f. Busque el archivo de metadatos de federación descargado del portal de Azure y, a continuación, cargarlo en hello **archivo de metadatos de SAML Idp**.
   
   g. Haga clic en hello **Aceptar** botón en la página de configuración del servidor de una plantilla de Hola.
   
    >[!NOTE] 
    >Cliente tener tooupload cualquier certificado en la configuración de SSO de SAML del servidor de una plantilla de Hola y obtener omitirán Hola flujo SSO.
    >Si necesita ayuda para la configuración de SAML en el servidor de una plantilla, consulte el artículo de toothis [configurar SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).
    >
<CE>

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-tableau-server-test-user"></a>Crear un usuario de prueba de Tableau Server

objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Tableau Server. Debe tooprovision todos los usuarios de hello en el servidor de una plantilla de Hola. 

Ese nombre de usuario del usuario de hello debe coincidir con el valor de Hola que ha configurado en el atributo personalizado de hello Azure AD de **nombre de usuario**. Con hello correcto de asignación de integración de hello debería funcionar [configurar Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).

>[!NOTE]
>Si necesita un usuario toocreate manualmente, debe toocontact hello Tableau Administrador de su organización.
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTableau Server.

![Asignar usuario][200] 

**tooassign Britta Simon tooTableau servidor, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Tableau Server**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de servidor de una plantilla de Hola Hola Panel de acceso, deberá obtener la aplicación de servidor de una plantilla de tooyour automáticamente ha iniciado sesión.
Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

