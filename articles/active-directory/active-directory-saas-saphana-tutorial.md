---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA| Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Tutorial: Integración de Azure Active Directory con SAP HANA

En este tutorial, aprenderá cómo toointegrate SAP HANA con Azure Active Directory (Azure AD).

Integración de SAP HANA con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSAP HANA
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAP HANA (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con SAP HANA, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en SAP HANA
- Instancia HANA en ejecución en cualquier IaaS pública, instancias locales, VM de Azure o instancias grandes de SAP en Azure
- Hola XSA administración Web Interface, así como Studio HANA instalado en la instancia HANA Hola.

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción de SAP HANA. Probar la integración de Hola primero en el desarrollo o el entorno de aplicación hello y, a continuación, entorno de producción de hello de uso de almacenamiento provisional.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de SAP HANA desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sap-hana-from-hello-gallery"></a>Adición de SAP HANA desde la Galería de Hola
integración de hello tooconfigure de SAP HANA en Azure AD, deberá tooadd SAP HANA en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SAP HANA desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **SAP HANA**, seleccione **SAP HANA** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd. 

    ![Hola nueva aplicación](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SAP HANA con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SAP HANA es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SAP HANA debe toobe establecido.

En SAP HANA, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con SAP HANA, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de SAP HANA](#creating-a-sap-hana-test-user) ** -toohave un equivalente de Britta Simon en SAP HANA que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SAP HANA.

**inicio de sesión único en Azure AD tooconfigure con SAP HANA, realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **SAP HANA** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. En hello **SAP HANA dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información sobre dominio y direcciones URL de inicio de sesión único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. Hola **identificador** cuadro de texto, tipo como:`HA100` 

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello URL de identificador y la respuesta real. Póngase en contacto con [equipo de soporte técnico de SAP HANA cliente](https://cloudplatform.sap.com/contact.html) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Si el certificado no está activo, después, actívelo haciendo clic en hello "hacer nueva certificado active" la casilla de verificación en hello Azure AD. 

5. Aplicación de SAP HANA espera las aserciones de SAML de hello en un formato concreto. Hola siguiente captura de pantalla muestra un ejemplo de esto. Aquí hemos asignamos hello **identificador de usuario** con **ExtractMailPrefix()** función de **user.mail**. Esto proporciona el valor de prefijo de saludo de correo electrónico del usuario de Hola que es Hola ID de usuario único. Toohello aplicación de SAP HANA, se envía cada respuesta correcta.

    ![Configurar inicio de sesión único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo:

    a. Hola **identificador de usuario** lista desplegable, seleccione **ExtractMailPrefix**.
    
    b. Hola **correo** lista desplegable, seleccione **user.mail**.

7. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure inicio de sesión único en **SAP HANA** lado, inicio de sesión tooyour **consola Web de HANA XSA** examinando toohello respectivo extremo de HTTPS.

    > [!Note]
    > En la configuración predeterminada de hello, dirección URL de hello redirige pantalla Inicio de sesión de bienvenida solicitud tooa, lo que requiere credenciales de hello autenticado SAP HANA base de datos usuario toocomplete Hola inicio de sesión del proceso de una. usuario de Hola que inicie sesión debe tener tareas de administración de hello privilegios necesarios tooperform SAML.

9. Hola XSA Web Interface, navegue demasiado**proveedor de identidad SAML** y desde allí, haga clic en hello **"+"** -situado en la parte inferior de Hola Hola pantalla toodisplay Hola Agregar identidad proveedor del panel de información y realizar Hola pasos:

    ![Agregación del proveedor de identidades](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. Hola **agregar información de proveedor de identidad** panel, pegar Hola contenido de hello Metadata XML, que ha descargado desde el portal de Azure en hello **metadatos** cuadro de texto.

    ![Adición de la configuración del proveedor de identidades](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Si contenido de hello del documento XML de hello es válido, Hola proceso de análisis extrae tooinsert de la información necesaria de hello en hello **asunto, Id. de entidad y emisor** campos de datos generales de hello área de pantalla y Hola campos de dirección URL de Hola Área de pantalla de destino, por ejemplo, * *dirección URL Base y la dirección URL de SingleSignOn (*)**.

    ![Adición de la configuración del proveedor de identidades](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. Área de pantalla en el cuadro de nombre de Hola de hello datos generales, escriba un nombre para el nuevo proveedor de identidades de SSO de SAML Hola.

    > [!Note]
    > nombre de Hola de hello SAML IDP es obligatorio y debe ser única; aparece en la lista Hola de IDPs SAML disponibles que se muestra, si selecciona SAML como método de autenticación de Hola para toouse de las aplicaciones de SAP HANA extra, por ejemplo, en área de pantalla de autenticación de Hola de herramienta de administración de artefactos de extra de Hola.

10. Guardar detalles de Hola de nuevo proveedor de identidades SAML Hola. Elija **guardar** toosave Hola detalles del proveedor de identidad SAML hello y agregue Hola nueva SAML IDP toohello lista de conocidos IDPs de SAML.

    ![Botón Guardar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. En Studio HANA dentro de las propiedades de sistema de Hola de hello **configuración** ficha, simplemente filtre la configuración por **saml** y ajustar hello **assertion_timeout** de **10 seg.** demasiado**120 segundo**.

    ![assertion_timeout setting](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![botón de agregar Hola](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-sap-hana-test-user"></a>Creación de un usuario de prueba en SAP HANA

toolog de los usuarios de Azure AD tooenable en tooSAP HANA, se les deben aprovisionar en SAP HANA.
SAP HANA admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

Si necesita un usuario toocreate manualmente, siga Hola pasos:

>[!Note]
>Puede cambiar autenticación externa Hola utilizada por el usuario de Hola.
Los usuarios externos se autentican utilizando un sistema externo, por ejemplo un sistema de Kerberos. Para obtener información detallada acerca de las identidades externas, póngase en contacto con su [administrador de dominio](https://cloudplatform.sap.com/contact.html).

1. Abra hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como administrador y habilitar Hola usuario de base de datos de SSO de SAML.

    ![crear usuario](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Graduación Hola casilla invisible toohello a la izquierda de **SAML** y siga el vínculo Configurar el saludo.

3. Haga clic en **agregar** tooadd Hola IDP SAML y haga clic en **Aceptar** seleccionar Hola IDP SAML adecuado.

4. Agregar hello **identidad externa** (p. ej. BrittaSimon aquí) o elija **"Cualquiera"** y haga clic en **Aceptar**.

    >[!Note]
    >Si "Cualquiera" casilla no está activada, el nombre de usuario de hello en HANA requiere nombre de Hola de coincidencia de tooexactly del usuario de Hola Hola UPN antes de sufijo de dominio de hello (es decir, BrittaSimon@contoso.com se convertiría en BrittaSimon en HANA).

5. Para realizar pruebas, asigne todos **"XS"** usuario toohello de roles.

    ![Asignación de roles](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Debe conceder solo los permisos adecuados para los casos de uso.

6. Guardar usuario Hola.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAP HANA.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooSAP HANA, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **SAP HANA**.

    ![Asignar usuario](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de SAP HANA Hola Hola Panel de acceso, deberá obtener la aplicación de SAP HANA tooyour automáticamente ha iniciado sesión.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

