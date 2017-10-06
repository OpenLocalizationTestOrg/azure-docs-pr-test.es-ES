---
title: "Tutorial: Integración de Azure Active Directory con SAP Cloud for Customer | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la nube de SAP para el cliente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Tutorial: Integración de Azure Active Directory con SAP Cloud for Customer

En este tutorial, aprenderá cómo toointegrate SAP en la nube para el cliente con Azure Active Directory (Azure AD).

Integración de SAP en la nube para el cliente con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tiene acceso tooSAP en la nube para cliente
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAP en la nube de cliente (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con SAP en la nube para el cliente, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción a SAP Cloud for Customer con inicio de sesión único habilitado

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar en la nube SAP de cliente desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Agregar en la nube SAP de cliente desde la Galería de Hola
integración de hello tooconfigure de SAP en la nube para el cliente en Azure AD, necesitará tooadd en la nube SAP para cliente de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd en la nube SAP para cliente de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **en la nube SAP para cliente**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. En el panel de resultados de hello, seleccione **en la nube SAP para cliente**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAP Cloud for Customer con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en la nube de SAP para el cliente es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la nube de SAP para el cliente debe toobe establecido.

En la nube de SAP para el cliente, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con SAP en la nube para el cliente, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear una nube de SAP de usuario de cliente de prueba](#creating-a-sap-cloud-for-customer-test-user)**  -toohave un equivalente de Britta Simon en nube de SAP para cliente que es la representación en forma de toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la nube de SAP para la aplicación de cliente.

**tooconfigure inicio de sesión único en Azure AD con SAP en la nube para el cliente, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **en la nube SAP para cliente** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. En hello **SAP en la nube para el dominio del cliente y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server name>.crm.ondemand.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [SAP en la nube para el equipo de soporte técnico al cliente cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget estos valores. 

4. En hello **atributos de usuario** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. En **identificador de usuario** lista, seleccione hello **ExtractMailPrefix()** (función).

    b. De hello **correo** lista, atributo de usuario de hello seleccione desea toouse para su implementación.
    Por ejemplo, si desea toouse Hola EmployeeID como identificador de usuario único y lo ha almacenado el valor del atributo de Hola Hola ExtensionAttribute2, a continuación, seleccione user.extensionattribute2.  

5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. En hello **en la nube para la configuración de cliente de SAP** sección, haga clic en **configurar la nube de SAP para cliente** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO configurado, lleve a cabo Hola pasos:
   
    a. Inicie sesión en el portal de SAP Cloud for Customer con derechos de administrador.
   
    b. Navegue toohello **aplicación y tareas comunes de administración de usuario** y haga clic en hello **proveedor de identidades** ficha.
   
    c. Haga clic en **nuevo proveedor de identidades** Hola seleccione metadatos del archivo XML y ha descargado desde Hola portal de Azure. Mediante la importación de metadatos de hello, sistema de Hola carga automáticamente el certificado de firma necesaria de Hola y el certificado de cifrado.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory requiere Hola elemento dirección URL del servicio de consumidor de aserción en la solicitud SAML de hello, así que seleccione hello **incluir dirección URL del servicio de consumidor de aserción** casilla de verificación.
   
    e. Haga clic en **Activate Single Sign-On**(Activar inicio de sesión único).
   
    f. Guarde los cambios.
   
    g. Haga clic en hello **mi sistema** ficha.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. En el cuadro de texto **Azure AD Sign On URL** (Dirección URL de inicio de sesión de Azure AD), pegue la **dirección URL del servicio de inicio de sesión único de SAML** que copió desde Azure Portal.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Especifique si empleado Hola manualmente puede elegir entre iniciar sesión con el Id. de usuario y una contraseña o SSO seleccionando hello **selección de proveedor de identidad Manual**.
   
    j. Hola **dirección URL SSO** sección, especificar dirección URL de Hola que debe usarse en su toosign empleados en toohello sistema. 
    Hola **tooEmployee envía la dirección URL** lista, puede elegir entre Hola siguientes opciones:
   
    **Non-SSO URL**
   
    sistema de Hello envía a empleado de toohello Hola solo dirección URL de la normal del sistema. empleado de Hola no se puede iniciar sesión con SSO y debe utilizar la contraseña o certificado en su lugar.
   
    **SSO URL** 
   
    sistema de Hello envía a solo empleado de toohello de hello dirección URL SSO. empleado de Hello puede iniciar sesión con SSO. Solicitud de autenticación se redirige a través de hello IdP.
   
    **Automatic Selection**
   
    Si SSO no está activo, el sistema de hello envía a empleado de toohello de dirección URL de hello normal del sistema. Si SSO está activo, el sistema de Hola comprueba si empleado hello tiene una contraseña. Si hay una contraseña, dirección URL de SSO y dirección URL de SSO no se envían a toohello empleado. Sin embargo, si Hola empleado no tiene ninguna contraseña, sólo Hola dirección URL de SSO se envía a toohello empleado.
   
    k. Guarde los cambios.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Creación de un usuario de prueba de SAP Cloud for Customer

En esta sección, creará un usuario llamado Britta Simon en SAP Cloud for Customer. Trabaje con [SAP en la nube para el equipo de soporte técnico al cliente](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) a los usuarios de tooadd Hola Hola SAP en la nube para la plataforma de cliente. 

> [!NOTE]
> Asegúrese de que NameID valor debe coincidir con el campo de nombre de usuario de Hola Hola SAP en la nube para la plataforma de cliente.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAP en la nube para el cliente.

![Asignar usuario][200] 

**tooassign Britta Simon tooSAP en la nube para el cliente, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **en la nube SAP para cliente**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello en la nube SAP de icono del cliente en el Panel de acceso de hello, obtendrá automáticamente ha iniciado sesión en la nube SAP tooyour para la aplicación de cliente.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

