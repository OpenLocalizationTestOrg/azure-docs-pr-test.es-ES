---
title: "Tutorial: Integración de Azure Active Directory con Confluence SAML SSO by Microsoft | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO de SAML confluencia por Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>Tutorial: Integración de Azure Active Directory con Confluence SAML SSO by Microsoft

En este tutorial, aprenderá cómo toointegrate SSO de SAML confluencia por Microsoft con Azure Active Directory (Azure AD).

Integración de SSO de SAML confluencia por Microsoft con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooConfluence SSO de SAML por Microsoft
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooConfluence SSO de SAML por Microsoft (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con SSO de SAML confluencia por Microsoft, deberá Hola siguientes elementos:

- Una suscripción de Azure AD
- Aplicación de servidor confluencia instalado en un servidor de Windows de 64 bits (local o en la infraestructura de IaaS en la nube hello)
- El servidor de Confluence es compatible con HTTPS
- Tenga en cuenta Hola admitida versiones de complemento de confluencia se mencionan en por debajo de la sección.
- Confluencia servidor es accesible en internet especialmente tooAzure página de inicio de sesión de AD para la autenticación y debe tooreceive capaz de Hola símbolo (token) de Azure AD
- Las credenciales de administrador se configuran en Confluence
- WebSudo está deshabilitado en Confluence
- Usuario creado en la aplicación de servidor confluencia Hola de prueba

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción de confluencia. Probar la integración de Hola primero en el desarrollo o el entorno de aplicación hello y, a continuación, entorno de producción de hello de uso de almacenamiento provisional.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de versión de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-confluence"></a>Versiones compatibles de Confluence 

En la actualidad se admiten las siguientes versiones de Confluence:

- Confluencia: too5.10 5.0

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar SSO de SAML confluencia por Microsoft de la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a>Agregar SSO de SAML confluencia por Microsoft de la Galería de Hola
integración de hello tooconfigure de SSO de SAML confluencia por Microsoft en Azure AD, deberá tooadd SSO de SAML confluencia por Microsoft de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SSO de SAML confluencia por Microsoft de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **SSO de SAML confluencia Microsoft**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. En el panel de resultados de hello, seleccione **SSO de SAML confluencia Microsoft**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección va a configurar y probar el inicio de sesión único de Azure AD con Confluence SAML SSO by Microsoft con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en confluencia SSO de SAML de Microsoft es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SSO de SAML confluencia Microsoft necesita toobe establecido.

En SSO de SAML confluencia por Microsoft, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con SSO de SAML confluencia por Microsoft, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un SSO de SAML confluencia por usuario de prueba de Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave un equivalente de Britta Simon en SSO de SAML confluencia por Microsoft que está vinculado toohello Azure AD representación del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO de SAML confluencia por aplicación de Microsoft.

**tooconfigure inicio de sesión único en Azure AD con SSO de SAML confluencia por Microsoft, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **SSO de SAML confluencia Microsoft** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. En hello **SSO de SAML confluencia Domain de Microsoft y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/plugins/servlet/saml/auth`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/`

    c. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión. En caso de que sea una dirección URL con nombre, el puerto es opcional. Estos valores se reciben durante la configuración de Hola de complemento de confluencia, que se explica más adelante en el tutorial Hola.
 

4. Hola toogenerate **metadatos** dirección url, realizar Hola pasos:

    a. Haga clic en **Registros de aplicaciones**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    b. Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    c. Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    d. Ahora vaya toohello página de propiedades de **SSO de SAML confluencia Microsoft** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    e. Generar hello **dirección URL de metadatos** con hello sigue el patrón: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` y copie este valor en el Bloc de notas como se utiliza para la configuración de Hola de complemento de hello más tarde.

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. Póngase en contacto con [Microsoft](mailto:waadpartners@microsoft.com) con hello siguiente información para hello confluencia complemento.
    
    *   Nombre del cliente:
    *   Nombre del dominio principal:
    *   Azure AD Premium: Sí/No (el complemento será de tooall disponible Hola cliente Free, Basic y Premium SKU)
    *   Número de usuarios que van a usar esta integración:
    *   Versión de Confluence:
    *   Comentarios:

7. En una ventana del explorador web diferente, inicie sesión en la instancia de confluencia tooyour como administrador.

8. Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. En la sección de la pestaña Complementos, haga clic en **Administrar complementos**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. Cargar manualmente el complemento de hello proporcionado por Microsoft. Una vez instalado el complemento de hello, aparece en **usuario instalado** sección de complementos de **administrar complemento** sección.

11. Haga clic en **configurar** tooconfigure Hola nuevo complemento.

12. Siga estos pasos en la página de configuración:

    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    a. En **dirección URL de metadatos** pegar hello **dirección URL de metadatos** generados a partir de Azure AD y haga clic en hello **resolver** botón. Lee la dirección URL de metadatos de IdP de Hola y rellena toda la información de campos Hola.

    > [!Note]
    > La ubicación del Id. de usuario de SAML predeterminada es el identificador de nombre. Puede cambiar esta opción de atributo tooan y escriba el nombre del atributo adecuado de Hola.

    > [!TIP]
    > Asegúrese de que hay un solo certificado asignado en la aplicación hello de forma que no hay ningún error en la resolución de metadatos de Hola. Si hay varios certificados, después de resolver los metadatos de Hola, administrador obtiene un error.
    
    b. Hola copia **identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión** valores y péguelos en **identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión** cuadros de texto respectivamente en **SSO de SAML confluencia Domain de Microsoft y las direcciones URL**  sección en el portal de Azure.

    c. En **el nombre del botón de inicio de sesión** nombre de tipo hello del botón de la organización quiere Hola usuarios toosee en pantalla de inicio de sesión.

    d. En **ubicaciones de Id. de usuario de SAML** seleccione **Id. de usuario está en elemento NameIdentifier de Hola de hello instrucción Subject** o **Id. de usuario está en un elemento Attribute**.  Este identificador tiene toobe Hola confluencia un identificador de usuario. Si no se encuentra el Id. de usuario de hello, sistema no permitirá que toolog a los usuarios en. 
    
    e. Si selecciona **Id. de usuario está en un elemento Attribute** opción, a continuación, en **nombre del atributo** cuadro de texto Nombre de Hola de tipo de atributo de Hola donde se esperaba el Id. de usuario. 

    f. Si usas el dominio federado de hello (por ejemplo, etc. ADFS) con Azure AD, a continuación, haga clic en hello **habilitar Home Realm Discovery** opción y configure hello **nombre de dominio**.
    
    g. En **nombre de dominio** escriba Hola dominio aquí el nombre en el caso de inicio de sesión de hello basada en AD FS.

    h. Comprobar **Habilitar cierre de sesión único** si desea toolog fuera de Azure AD cuando un usuario cierra la sesión de confluencia. 

    i. Haga clic en **guardar** botón Configuración de hello toosave.


> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a>Creación de un usuario de prueba de Confluence SAML SSO by Microsoft

toolog de los usuarios de Azure AD tooenable en tooConfluence en el servidor local, se les deben aprovisionar en SSO de SAML confluencia por Microsoft. Para Confluence SAML SSO by Microsoft, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour confluencia en servidor local como administrador.

2. Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.

    ![Agregar empleado](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. En la sección Usuarios, haga clic en la pestaña **Agregar usuarios**. En hello **"Agregar usuarios"** cuadro de diálogo, siga los pasos de hello:

    ![Agregar empleado](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    a. Hola **nombre de usuario** cuadro de texto, correo electrónico de Hola de tipo de usuario como Britta Simon.

    b. Hola **nombre completo** cuadro de texto, nombre completo de tipo hello del usuario como Britta Simon.

    c. Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.

    d. Hola **contraseña** cuadro de texto, escriba la contraseña para Britta Simon Hola.

    e. Haga clic en **Confirmar contraseña** introducir la contraseña de Hola.
    
    f. Haga clic en el botón **Agregar**.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooConfluence SSO de SAML por Microsoft.

![Asignar usuario][200] 

**tooassign Britta Simon tooConfluence SSO de SAML por Microsoft, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **SSO de SAML confluencia Microsoft**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello SSO de SAML confluencia por mosaico de Microsoft en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour SSO de SAML confluencia por aplicación de Microsoft.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

