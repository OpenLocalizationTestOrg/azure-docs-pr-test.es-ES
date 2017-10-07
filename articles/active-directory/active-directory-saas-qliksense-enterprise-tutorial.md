---
title: "Tutorial: Integración de Azure Active Directory con Qlik Sense Enterprise | Microsoft Doc"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Qlik sentido empresarial."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Tutorial: Integración de Azure Active Directory con Qlik Sense Enterprise

En este tutorial, aprenderá cómo toointegrate Qlik sentido empresarial con Azure Active Directory (Azure AD).

Integración Qlik sentido empresarial con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooQlik sentido empresarial.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooQlik sentido empresarial (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Qlik sentido Enterprise, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Qlik Sense Enterprise

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Qlik sentido empresarial desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Agregar Qlik sentido empresarial desde la Galería de Hola
integración de hello tooconfigure de Qlik sentido Enterprise en Azure AD, deberá tooadd Qlik sentido empresarial de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Qlik sentido empresarial desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **Qlik sentido Enterprise**, seleccione **Qlik sentido Enterprise** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Qlik sentido empresarial en la lista de resultados de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Qlik Sense Enterprise utilizando un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Qlik sentido empresarial es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Qlik sentido empresarial debe toobe establecido.

En las empresas de sentido Qlik, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Qlik sentido empresarial, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Enterprise de sentido Qlik](#create-a-qlik-sense-enterprise-test-user) ** -toohave un equivalente de Britta Simon en Qlik sentido empresarial que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación empresarial de sentido Qlik.

**tooconfigure inicio de sesión único en Azure AD con Qlik sentido Enterprise, lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Qlik sentido Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. En hello **Qlik sentido empresarial dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Tenga en cuenta Hola finales barra diagonal al final de Hola de este URI. ya que es obligatorio.
    
    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Estos valores no son reales. Actualización de estos valores con Hola real dirección URL de inicio de sesión y el identificador, que se explican más adelante en este tutorial o póngase en contacto con [equipo de soporte técnico de cliente de empresa de sentido Qlik](https://www.qlik.com/us/services/support) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Preparar el archivo XML de metadatos de federación de hello por lo que puede cargar ese servidor de sentido tooQlik.
   
    > [!NOTE]
    > Antes de cargar Hola IdP metadatos toohello server Qlik sentido, archivo hello necesita toobe editar tooremove información tooensure el funcionamiento correcto entre Azure AD y el servidor de Qlik sentido.
    
    ![QlikSense][qs24]
   
    a. Abra el archivo de FederationMetaData.xml de hello, que ha descargado desde el portal de Azure en un editor de texto.
   
    b. Busque el valor de hello **RoleDescriptor**.  Hay cuatro entradas (dos pares de etiquetas de elementos de apertura y cierre).
   
    c. Eliminar etiquetas de RoleDescriptor de Hola y toda la información en medio de archivo hello.
   
    d. Guarde el archivo de Hola y mantenerlo cercanas para utilizarlo más adelante en este documento.

7. Navegue toohello Qlik sentido Qlik Management Console (QMC) como un usuario que puede crear las configuraciones de proxy virtual.

8. Hola QMC, haga clic en hello **Proxies Virtual** elemento de menú.
   
    ![QlikSense][qs6] 

9. En la parte inferior de Hola de pantalla de bienvenida, haga clic en hello **crear nuevo** botón.
   
    ![QlikSense][qs7]

10. aparece la pantalla de edición de Hello Virtual proxy.  En hello lado derecho de la pantalla de bienvenida es un menú para hacer visible las opciones de configuración.
   
    ![QlikSense][qs9]

11. Con la opción de menú de identificación de hello comprueba, escribe la información de identificación de hello para la configuración de proxy de virtual de Azure Hola.
    
    ![QlikSense][qs8]  
    
    a. Hola **descripción** campo es un nombre descriptivo para la configuración de proxy virtual Hola.  Escriba un valor para este campo.
    
    b. Hola **prefijo** campo identifica de punto de conexión de hello proxy virtual para conectar tooQlik sentido con Azure AD Single Sign-On.  Escriba un nombre de prefijo único para este proxy virtual.
    
    c. **Tiempo de espera de inactividad de sesión (minutos)** Hola tiempo de espera para las conexiones a través de este proxy virtual.
    
    d. Hola **nombre de encabezado de cookie de sesión** es almacenar nombre de cookie de Hola Hola identificador de sesión de hello sesión Qlik sentido un usuario recibe tras la autenticación correcta.  Este nombre debe ser único.

12. Haga clic en hello autenticación menú opción toomake visible.  aparece la pantalla de bienvenida la autenticación.
    
    ![QlikSense][qs10]
    
    a. Hola **modo de acceso anónimo** desplegable determina si pueden tener acceso a los usuarios anónimos Qlik sentido a través de proxy virtual Hola.  opción predeterminada de Hello no es ningún usuario anónimo.
    
    b. Hola **método de autenticación** desplegable determina el esquema Hola Hola autenticación virtual proxy usará.  Seleccione SAML de lista desplegable de Hola.  Como resultado, aparecerán más opciones.
    
    c. Hola **el campo de identificador URI del host SAML**, los usuarios de nombre de host de entrada Hola escribir tooaccess Qlik sentido a través de este proxy virtual SAML.  nombre de host de Hello es uri Hola de hello server Qlik sentido.
    
    d. Hola **Id. de entidad SAML**, escriba Hola mismo valor especificado para el campo de identificador URI de host de hello SAML.
    
    e. Hola **metadatos SAML IdP** es archivo hello editado anteriormente en hello **editar los metadatos de federación de la configuración de AD Azure** sección.  **Antes de cargar los metadatos de IdP de hello, archivo hello necesita toobe editar** tooremove información tooensure el funcionamiento correcto entre Azure AD y el servidor de Qlik sentido.  **Consulte instrucciones toohello anteriores si tiene el archivo hello aún toobe editar.**  Si se ha editado el archivo hello haga clic en el botón de examinar hello y tooupload de archivo de metadatos editado Hola seleccione Configuración de proxy virtual toohello.
    
    f. Escriba la referencia de esquema o nombre de atributo de Hola para atributo SAML de Hola que representa hello **UserID** Azure AD envía toohello server Qlik sentido.  Información de referencia de esquema está disponible en hello Azure aplicación pantallas después de la configuración.  atributo de nombre de hello toouse, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Escriba el valor de Hola para hello **directorio usuario** que será toousers adjunto al realizar la autenticación tooQlik servidor de sentido a través de Azure AD.  Los valores codificados deben estar entre **corchetes**.  toouse un atributo que se envían en hello aserción de SAML de Azure AD, escriba el nombre de Hola de atributo hello en este cuadro de texto **sin** corchetes.
    
    h. Hola **algoritmo de firma de SAML** conjuntos hello para la configuración de proxy virtual Hola de firma de certificado de proveedor (en este servidor Qlik sentido mayúscula) de servicio.  Si servidor Qlik sentido utiliza un certificado de confianza que se genera mediante RSA mejorado de Microsoft y proveedor de servicios criptográficos de AES, cambie algoritmo de firma de SAML de hello demasiado**SHA-256**.
    
    i. Hola sección de asignación de atributo SAML permite atributos adicionales como grupos toobe enviado tooQlik sentido para su uso en las reglas de seguridad.

13. Haga clic en hello **equilibrio de carga** toomake de opción de menú que visible.  aparece la pantalla de bienvenida equilibrio de carga.
    
    ![QlikSense][qs11]

14. Haga clic en hello **Agregar nuevo nodo de servidor** botón nodo seleccione motor o nodos Qlik sentido se envíe con fines de equilibrio de carga de las sesiones toofor y haga clic en hello **agregar** botón.
    
    ![QlikSense][qs12]

15. Haga clic en toomake de opción de menú Opciones avanzadas de hello visible. aparece la pantalla avanzada de bienvenida.
    
    ![QlikSense][qs13]
    
    lista blanca de Hello Host identifica los nombres de host que se aceptan cuando se conecte toohello server Qlik sentido.  **Escriba el nombre de host de hello los usuarios especificarán al conectar el servidor de sentido tooQlik.** nombre de host de Hello es hello mismo valor que Hola SAML host uri sin Hola https://.

16. Haga clic en hello **aplicar** botón.
    
    ![QlikSense][qs14]

17. Haga clic en el mensaje de advertencia de hello Aceptar tooaccept que indica los servidores proxy se reiniciará proxy virtual toohello vinculado.
    
    ![QlikSense][qs15]

18. En el lado derecho de Hola de pantalla de bienvenida, aparece el menú de elementos de asociados de Hola.  Haga clic en hello **proxy** opción de menú.
    
    ![QlikSense][qs16]

19. aparece la pantalla de bienvenida proxy.  Haga clic en hello **vínculo** botón en hello inferior toolink proxy proxy toohello virtual.
    
    ![QlikSense][qs17]

20. Nodo de proxy de hello SELECT que admitirá esta conexión virtual proxy y haga clic en hello **vínculo** botón.  Después de vincular, proxy Hola se enumerará en servidores proxy asociados.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. Después de aproximadamente cinco segundos tooten, Hola mensaje Actualizar QMC aparecerá.  Haga clic en hello **QMC actualizar** botón.
    
    ![QlikSense][qs20]

22. Cuando actualiza hello QMC, haga clic en hello **Virtual proxy** elemento de menú. nueva entrada de proxy virtual SAML Hola se muestra en la tabla de hello en la pantalla de bienvenida.  Solo un clic en la entrada de proxy virtual Hola.
    
    ![QlikSense][qs51]

23. En la parte inferior de Hola de pantalla de bienvenida, se activará un botón de hello SP descargar metadatos.  Haga clic en hello **SP descargar metadatos** archivo tooa de botón toosave hello metadatos.
    
    ![QlikSense][qs52]

24. Archivo de metadatos de sp de hello abierto.  Observar hello **entityID** hello y entrada **AssertionConsumerService** entrada.  Estos valores son equivalente toohello **identificador** hello y **dirección URL de inicio de sesión** en configuración de la aplicación hello Azure AD. Pegue estos valores en hello **Qlik sentido empresarial dominio y las direcciones URL** sección de configuración de la aplicación hello Azure AD si no coinciden, a continuación, se debe reemplazar en el Asistente para configuración de aplicación de Azure AD Hola.
    
    ![QlikSense][qs53]

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

   ![botón de Hello Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

   ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

   ![botón de agregar Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

   ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. Hola **nombre** , escriba **BrittaSimon**.

   b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

   c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

   d. Haga clic en **Crear**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Creación de un usuario de prueba de Qlik Sense Enterprise

En esta sección, creará un usuario llamado "Britta Simon" en Qlik Sense Enterprise. Trabajar con [equipo de soporte técnico de cliente de empresa de sentido Qlik](https://www.qlik.com/us/services/support) para agregar usuarios de hello en plataforma de hello Qlik sentido empresarial. Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único. 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooQlik sentido empresarial.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooQlik sentido Enterprise, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Qlik sentido Enterprise**.

    ![vínculo de Hello Qlik sentido empresarial en la lista de aplicaciones de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Qlik sentido empresarial Hola Hola Panel de acceso, deberá obtener aplicaciones de Qlik sentido Enterprise tooyour automáticamente ha iniciado sesión. 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

