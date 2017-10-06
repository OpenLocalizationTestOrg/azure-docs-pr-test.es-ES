---
title: "Tutorial: Integración de Azure Active Directory con ServiceNow | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ServiceNow y ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Tutorial: Integración de Azure Active Directory con ServiceNow
En este tutorial, aprenderá cómo toointegrate ServiceNow y ServiceNow Express con Azure Active Directory (Azure AD).

Integración de ServiceNow y ServiceNow Express con Azure AD proporciona Hola siguientes ventajas:

* Puede controlar en Azure AD que tenga acceso tooServiceNow y ServiceNow Express
* Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooServiceNow y ServiceNow Express (Single Sign-On) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con ServiceNow y ServiceNow Express tooconfigure, necesita Hola siguientes elementos:

* Una suscripción de Azure AD
* Para ServiceNow, una instancia o inquilino de ServiceNow, versión Calgary o superior
* Para ServiceNow Express, una instancia de ServiceNow Express, versión Helsinki o superior
* inquilino de ServiceNow Hola debe tener hello [varios único inicio de sesión de complemento de proveedor de](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) habilitado. Esto puede hacerse [enviando una solicitud de servicio](https://hi.service-now.com). 

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
> 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar ServiceNow desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD en ServiceNow o ServiceNow Express

## <a name="adding-servicenow-from-hello-gallery"></a>Agregar ServiceNow desde la Galería de Hola
integración de hello tooconfigure de ServiceNow o ServiceNow Express en Azure AD, deberá tooadd ServiceNow de lista de tooyour Hola Galería de aplicaciones administradas de SaaS. 

**tooadd ServiceNow de galería de hello, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**. 
   
    ![Active Directory][1]
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones][2]
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Aplicaciones][4]
6. En el cuadro de búsqueda de hello, escriba **ServiceNow**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. En el panel de resultados de hello, seleccione **ServiceNow**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ServiceNow o ServiceNow con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ServiceNow es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ServiceNow debe toobe establecido.
Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en ServiceNow. tooconfigure y prueba de inicio de sesión único en Azure AD con ServiceNow, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable la toouse usuarios esta característica.
2. **[Configurar Azure AD Single Sign-On para ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable la toouse usuarios esta característica.
3. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
4. **[Crear un usuario de prueba de ServiceNow](#creating-a-servicenow-test-user)**  -toohave un equivalente de Britta Simon en ServiceNow que está vinculado toohello Azure AD representación de ella.
5. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
6. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

> [!NOTE]
> Si desea que tooconfigure ServiceNow omite el paso 2. Del mismo modo, si desea tooconfigure ServiceNow Express, que omite el paso 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Configuración del inicio de sesión único de Azure AD para ServiceNow
1. En portal clásico de hello Azure AD, en hello **ServiceNow** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo .
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar inicio de sesión único")

2. En hello **¿cómo desea que los usuarios toosign en tooServiceNow** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar inicio de sesión único")

3. En hello **configurar opciones de aplicación** , siga los pasos de hello:
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar dirección URL de la aplicación")
   
    a. Hola **ServiceNow inicio de sesión en la URL** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello: `https://<instance-name>.service-now.com`.
   
    b. Hola **identificador** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello: `https://<instance-name>.service-now.com`.
   
    c. Haga clic en **Siguiente**

4. toohave Azure AD automáticamente configurar ServiceNow para la autenticación de SAML, escriba el nombre de instancia de ServiceNow, nombre de usuario y contraseña de administrador en hello **configuración automática de inicio de sesión único** formulario y haga clic en  *Configurar*. Tenga en cuenta ese nombre de usuario de administrador Hola proporcionado debe tener hello **security_admin** rol asignado en ServiceNow para este toowork. En caso contrario, toomanually configurar ServiceNow toouse Azure AD como proveedor de identidades SAML, haga clic en **configurar manualmente la aplicación hello para el inicio de sesión único**, a continuación, haga clic en **siguiente** hello completa y pasos siguientes.
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar dirección URL de la aplicación")

5. En hello **configurar inicio de sesión único en ServiceNow** página, haga clic en **Descargar certificado**, guardar el archivo de certificado de hello localmente en el equipo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar inicio de sesión único")

6. Inicio de sesión tooyour ServiceNow aplicación como administrador.

7. Activar hello *integración - varios Single Sign-On instalador de proveedor* complemento siguiendo Hola pasos siguientes:
   
    a. En el panel de navegación de hello en el lado izquierdo de hello, vaya demasiado**definición del sistema** sección y, a continuación, haga clic en **complementos**.
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")(Activar complemento)
   
    b. Busque *Integration - Multiple Provider Single Sign-On Installer*.
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")(Activar complemento)
   
    c. Seleccione el complemento de Hola. Haga clic con el botón derecho y seleccione **Activate/Upgrade** (Activar o actualizar).
   
    d. Haga clic en hello **activar** botón.

8. En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **propiedades**.  
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurar dirección URL de la aplicación")

9. En hello **varias propiedades de proveedor de SSO** cuadro de diálogo, realizar Hola pasos:
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurar dirección URL de la aplicación")
   
    a. En **Enable multiple provider SSO** (Habilitar SSO de varios proveedores), seleccione **Yes** (Sí).
   
    b. Como **habilitar el registro de depuración se obtuvo Hola proveedor múltiples integración de SSO**, seleccione **Sí**.
   
    c. En **campo hello en usuario Hola de tabla que...**  cuadro de texto, tipo **nombre_usuario**.
   
    d. Haga clic en **Guardar**.

10. En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **x509 certificados**.
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurar inicio de sesión único")

11. En hello **certificados X.509** cuadro de diálogo, haga clic en **nuevo**.
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurar inicio de sesión único")

12. En hello **certificados X.509** cuadro de diálogo, realizar Hola pasos:
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar inicio de sesión único")
    
     a. Haga clic en **Nuevo**.
    
     b. Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **TestSAML2.0**).
    
     c. Seleccione **Active**(Activo).
    
     d. En **Format** (Formato), seleccione **PEM**.
    
     e. En **Type** (Tipo), seleccione **Trust Store Cert** (Confiar en certificados de almacén).
    
     f. Abra el certificado codificado en Base64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado PEM** cuadro de texto.
    
     g. Haga clic en **Update**(Actualizar).

13. En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **proveedores de identidades**.
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurar inicio de sesión único")

14. En hello **proveedores de identidades** cuadro de diálogo, haga clic en **New**:
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurar inicio de sesión único")

15. En hello **proveedores de identidades** cuadro de diálogo, haga clic en **SAML2 Update1?**:
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurar inicio de sesión único")

16. En el cuadro de diálogo de propiedades de la actualización 1 de SAML2 hello, realizar Hola pasos:
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurar inicio de sesión único")

    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **SAML 2.0**).

    b. Hola **campo usuario** cuadro de texto, tipo **correo electrónico** o **nombre_usuario**, dependiendo de qué campo se usa toouniquely identificar a los usuarios en la implementación de ServiceNow. 

    > [!NOTE] 
    > Puede configue Azure AD tooemit cualquier Id. de usuario de hello Azure AD (nombre principal de usuario) u Hola dirección de correo electrónico como Hola identificador único en el token SAML de Hola por van toohello **ServiceNow > atributos > Single Sign-On** sección de Hola portal de Azure clásico y asignación Hola deseado campo toohello **nameidentifier** atributo. Hola valor almacenado para el atributo seleccionado hello en Azure AD (p. ej. nombre principal de usuario) debe coincidir con hello almacenados en ServiceNow para el campo de hello especificado (por ejemplo, user_name)

    c. En el portal clásico de hello Azure AD, copie hello **Id. de proveedor de identidad** valor y, a continuación, péguelo en hello **dirección URL del proveedor de identidad** cuadro de texto.

    d. En el portal clásico de hello Azure AD, copie hello **URL de solicitud de autenticación** valor y, a continuación, péguelo en hello **AuthnRequest del proveedor de identidades** cuadro de texto.

    e. En el portal clásico de hello Azure AD, copie hello **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **SingleLogoutRequest del proveedor de identidades** cuadro de texto.

    f. Hola **ServiceNow Homepage** cuadro de texto, escriba Hola la dirección URL de la página de inicio de la instancia de ServiceNow.

    > [!NOTE] 
    > página de inicio de instancia de ServiceNow de Hello es una concatenación de su **dirección URL del inquilino ServieNow** y **/navpage.DO** (p. ej.:`https://fabrikam.service-now.com/navpage.do`).

    g. Hola **Id. de entidad / emisor** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow.

    h. Hola **dirección URL de audiencia** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow. 

    i. Hola **protocolo de enlace de hello del IDP SingleLogoutRequest** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:bindings:HTTP-redirigir**.

    j. En el cuadro de texto de política de NameID hello, escriba **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: sin especificar**.

    k. Anule la selección de **Create an AuthnContextClass**(Crear AuthnContextClass).

    l. Hola **método AuthnContextClassRef**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Esto solo es preciso para las organizaciones que solo trabajan en la nube. Si se usa MFA o ADFS local para la autenticación, este valor no se debe configurar. 

    m. En el cuadro de diálogo **Clock Skew** (Desplazamiento del reloj), escriba **60**.

    n. En **Single Sign On Script** (Script de inicio de sesión único), seleccione **MultiSSO_SAML2_Update1**.

    o. Como **x509 certificado**, seleccione certificado Hola ha creado en el paso anterior de Hola.

    p. Haga clic en **Enviar**. 

1. En el portal clásico de hello Azure AD, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**. 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar inicio de sesión único")

2. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar inicio de sesión único")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Configuración del inicio de sesión único de Azure AD para ServiceNow Express
1. En portal clásico de hello Azure AD, en hello **ServiceNow** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo .
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar inicio de sesión único")

2. En hello **¿cómo desea que los usuarios toosign en tooServiceNow** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar inicio de sesión único")

3. En hello **configurar opciones de aplicación** , siga los pasos de hello:
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar dirección URL de la aplicación")
   
    a. Hola **ServiceNow inicio de sesión en la URL** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello: `https://<instance-name>.service-now.com`.
   
    b. Hola **dirección URL del emisor** cuadro de texto, escriba la dirección URL utilizado por la aplicación de ServiceNow de toosign en tooyour de los usuarios seguir el patrón de hello `https://<instance-name>.service-now.com`.
   
    c. Haga clic en **Siguiente**

4. Haga clic en **configurar manualmente la aplicación hello para el inicio de sesión único**, a continuación, haga clic en **siguiente** y Hola completa siguiendo los pasos indicados.
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar dirección URL de la aplicación")

5. En hello **configurar inicio de sesión único en ServiceNow** página, haga clic en **Descargar certificado**, guardar el archivo de certificado de hello localmente en el equipo y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar inicio de sesión único")

6. Inicio de sesión tooyour ServiceNow Express aplicación como administrador.

7. En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **Single Sign-On**.  
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurar dirección URL de la aplicación")

8. En hello **Single Sign-On** cuadro de diálogo, haga clic en el icono de configuración de hello en superior de hello derecho y establezca hello siguientes propiedades:
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurar dirección URL de la aplicación")
   
    a. Alternar **habilitar proveedor múltiples SSO** toohello derecha.
   
    b. Alternar **depuración Habilitar registro de hello proveedor múltiples integración de SSO** toohello derecha.
   
    c. En **campo hello en usuario Hola de tabla que...**  cuadro de texto, tipo **nombre_usuario**.
9. En hello **Single Sign-On** cuadro de diálogo, haga clic en **Agregar nuevo certificado**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurar inicio de sesión único")
10. En hello **certificados X.509** cuadro de diálogo, realizar Hola pasos:
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar inicio de sesión único")
    
    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **TestSAML2.0**).
    
    b. Seleccione **Active**(Activo).
    
    c. En **Format** (Formato), seleccione **PEM**.
    
    d. En **Type** (Tipo), seleccione **Trust Store Cert** (Confiar en certificados de almacén).
    
    e. Cree un archivo con codificación Base64 a partir del certificado descargado.
    
    > [!NOTE]
    > Para obtener más información, consulte [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Abra el certificado codificado en Base64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado PEM** cuadro de texto.
    
    g. Haga clic en **Update**(Actualizar).
11. En hello **Single Sign-On** cuadro de diálogo, haga clic en **agregar nueva IdP**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurar inicio de sesión único")
12. En hello **Agregar nuevo proveedor de identidades** cuadro de diálogo, en **configurar el proveedor de identidades**, realizar Hola pasos:
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurar inicio de sesión único")

    a. Hola **nombre** cuadro de texto, escriba un nombre para la configuración (p. ej.: **SAML 2.0**).

    b. En el portal clásico de hello Azure AD, copie hello **Id. de proveedor de identidad** valor y, a continuación, péguelo en hello **dirección URL del proveedor de identidad** cuadro de texto.

    c. En el portal clásico de hello Azure AD, copie hello **URL de solicitud de autenticación** valor y, a continuación, péguelo en hello **AuthnRequest del proveedor de identidades** cuadro de texto.

    d. En el portal clásico de hello Azure AD, copie hello **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **SingleLogoutRequest del proveedor de identidades** cuadro de texto.

    e. Como **certificado del proveedor de identidad**, seleccione certificado Hola ha creado en el paso anterior de Hola.


1. Haga clic en **configuración avanzada**y en **propiedades adicionales del proveedor de identidad**, realizar Hola pasos:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurar inicio de sesión único")
   
    a. Hola **protocolo de enlace de hello del IDP SingleLogoutRequest** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:2.0:bindings:HTTP-redirigir**.
   
    b. Hola **política de NameID** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: sin especificar**.    
   
    c. Hola **método AuthnContextClassRef**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Anule la selección de **Create an AuthnContextClass**(Crear AuthnContextClass).

2. En **propiedades adicionales del proveedor de servicio**, realizar Hola pasos:
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurar inicio de sesión único")
   
    a. Hola **ServiceNow Homepage** cuadro de texto, escriba Hola la dirección URL de la página de inicio de la instancia de ServiceNow.
   
    > [!NOTE]
    > página de inicio de instancia de ServiceNow de Hello es una concatenación de su **dirección URL del inquilino ServieNow** y **/navpage.DO** (p. ej.: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. Hola **Id. de entidad / emisor** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow.
   
    c. Hola **URI de audiencia** cuadro de texto, escriba la dirección URL Hola de su inquilino de ServiceNow. 
   
    d. En el cuadro de diálogo **Clock Skew** (Desplazamiento del reloj), escriba **60**.
   
    e. Hola **campo usuario** cuadro de texto, tipo **correo electrónico** o **nombre_usuario**, dependiendo de qué campo se usa toouniquely identificar a los usuarios en la implementación de ServiceNow.
   
    > [!NOTE]
    > Puede configue Azure AD tooemit cualquier Id. de usuario de hello Azure AD (nombre principal de usuario) u Hola dirección de correo electrónico como Hola identificador único en el token SAML de Hola por van toohello **ServiceNow > atributos > Single Sign-On** sección de Hola portal de Azure clásico y asignación Hola deseado campo toohello **nameidentifier** atributo. Hola valor almacenado para el atributo seleccionado hello en Azure AD (p. ej. nombre principal de usuario) debe coincidir con hello almacenados en ServiceNow para el campo de hello especificado (por ejemplo, user_name)
    > 
    > 
   
    f. Haga clic en **Guardar**. 

3. En el portal clásico de hello Azure AD, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**. 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar inicio de sesión único")

4. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar inicio de sesión único")

## <a name="configuring-user-provisioning"></a>Configuración del aprovisionamiento de usuario
objetivo de Hola de esta sección es toooutline cómo tooenable el aprovisionamiento de usuarios de usuario de Active Directory cuentas tooServiceNow.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure aprovisionamiento de usuario, realizar Hola pasos:
1. En hello Azure clásico portal de administración en hello **ServiceNow** página de integración de aplicaciones, haga clic en **configurar aprovisionamiento de usuario**. 
   
    ![Aprovisionamiento de usuarios](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Aprovisionamiento de usuarios")

2. En hello **escriba el aprovisionamiento automático de usuarios de ServiceNow credenciales tooenable** , proporcione Hola siguientes opciones de configuración:
   
     a. Hola **nombre de la instancia de ServiceNow** cuadro de texto, nombre de la instancia de tipo hello ServiceNow.
   
     b. Hola **nombre de usuario de administrador de ServiceNow** cuadro de texto, nombre de tipo hello de hello cuenta de administrador de ServiceNow.
   
     c. Hola **contraseña de administrador de ServiceNow** cuadro de texto, escriba la contraseña de Hola para esta cuenta.
   
     d. Haga clic en **validar** tooverify su configuración.
   
     e. Haga clic en hello **siguiente** Hola de botón tooopen **pasos siguientes** página.
   
     f. Si desea que todos los usuarios toothis application tooprovision, seleccione "**aprovisionar automáticamente todas las cuentas de usuario en la aplicación de hello directorio toothis**". 
   
    ![Pasos siguientes](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Pasos siguientes")
   
     g. En hello **pasos siguientes** página, haga clic en **completar** toosave su configuración.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, creará un usuario de prueba en el portal clásico de hello llamado a Britta Simon.

![Creación de un usuario de Azure AD][20]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.

3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. En Tipo de usuario, seleccione Nuevo usuario de la organización.
   
    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
   
    c. Haga clic en **Siguiente**.

6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:
   
   ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
   
   b. Hola **Last Name** cuadro de texto, tipo, **Simon**.
   
   c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
   
   d. Hola **rol** lista, seleccione **usuario**.
   
   e. Haga clic en **Siguiente**.

7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Anote el valor de Hola de hello **nueva contraseña**.
   
    b. Haga clic en **Completo**.   

### <a name="creating-a-servicenow-test-user"></a>Creación de un usuario de prueba de ServiceNow
En esta sección, creará un usuario llamado Britta Simon en ServiceNow. En esta sección, creará un usuario llamado Britta Simon en ServiceNow. Si no sabe cómo tooadd un usuario en su ServiceNow o ServiceNow Express cuenta, póngase en contacto con el equipo de soporte técnico de ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD
En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooServiceNow de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooServiceNow, lleve a cabo Hola pasos:**

1. En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ServiceNow**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Asignar usuario][203] 

4. En la lista de todos los usuarios de hello, seleccione **Britta Simon**.

5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Asignar usuario][205]

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 
objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de ServiceNow Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour ServiceNow aplicación.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
