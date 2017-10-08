---
title: "Tutorial: Integración de Azure Active Directory con Workday | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y los días laborables."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Tutorial: Integración de Azure Active Directory con Workday

En este tutorial, aprenderá cómo toointegrate Workday con Azure Active Directory (Azure AD).

Integración de Workday con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooWorkday
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkday (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Workday tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Workday

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Adición de jornada laboral de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-workday-from-hello-gallery"></a>Adición de jornada laboral de galería de Hola
integración de hello tooconfigure de jornada laboral en Azure AD, deberá tooadd Workday de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Workday de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Workday**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. En el panel de resultados de hello, seleccione **Workday**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con Workday con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workday es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workday debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en jornada laboral.

tooconfigure y prueba de inicio de sesión único en Azure AD con Workday, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de jornada laboral](#creating-a-workday-test-user)**  -toohave un equivalente de Britta Simon en jornada laboral que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de jornada laboral.

**inicio de sesión único en tooconfigure Azure AD con Workday, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Workday** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. En hello **Workday dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello como:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Estos valores no son Hola real. Actualizar estos valores con la URL de inicio de sesión real de Hola y la dirección URL de respuesta. La URL de respuesta debe tener un subdominio (por ejemplo, www, wd2, wd3, wd3-impl, wd5 y wd5-impl). Usar algo como "*http://www.myworkday.com*" funciona, pero "*http://myworkday.com*" no funciona. Póngase en contacto con [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget estos valores. 
 

4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. En hello **configuración de Workday** sección, haga clic en **configurar Workday** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración del inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía Workday tooyour como administrador.

8. Vaya demasiado**menú \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Vaya demasiado**administración de cuentas**.
   
    ![Administración de cuentas](./media/active-directory-saas-workday-tutorial/IC782924.png "Administración de cuentas")

10. Vaya demasiado**Editar configuración de inquilino – seguridad**.
   
    ![Edición de seguridad del inquilino](./media/active-directory-saas-workday-tutorial/IC782925.png "Edición de seguridad del inquilino")

11. Hola **direcciones URL de redirección** sección, lleve a cabo Hola pasos:
   
    ![Direcciones URL de redirección](./media/active-directory-saas-workday-tutorial/IC7829581.png "Direcciones URL de redirección")
   
    a. Haga clic en **Add Row**(Agregar fila).
   
    b. Hola **dirección URL de redireccionamiento de inicio de sesión** cuadro de texto hello y **dirección URL de redireccionamiento de Mobile** cuadro de texto, hello tipo **dirección URL de inicio de sesión** que ha escrito en hello **Workday dominio y Las direcciones URL** sección de hello portal de Azure.
   
    c. En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **dirección URL de cierre de sesión**y, a continuación, péguelo en hello **dirección URL de redireccionamiento de cierre de sesión** cuadro de texto.
   
    d.  En **entorno** cuadro de texto, el nombre del entorno de tipo hello.  

    >[!NOTE]
    > Hello valor del atributo de entorno Hola está ligado toohello valor de dirección URL del inquilino hello:  
    >-Si nombre de dominio de Hola de URL de inquilino de Workday Hola comienza con impl por ejemplo: *https://impl.workday.com/\<inquilino\>/login-saml2.htmld*), hello **entorno** debe establecer el atributo tooImplementation.  
    >-Si el nombre de dominio de hello empieza por algo más, necesita toocontact [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget Hola coincidencia **entorno** valor.

12. Hola **configuración de SAML** sección, lleve a cabo Hola pasos:
   
    ![Configuración de SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configuración de SAML")
   
    a.  Seleccione **Enable SAML Authentication**(Habilitar autenticación SAML).
   
    b.  Haga clic en **Add Row**(Agregar fila).

13. Hola sección proveedores de identidades SAML, siga Hola siguiendo los pasos:
   
    ![Proveedores de identidades SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Proveedores de identidades SAML")
   
    a. En el cuadro de texto de nombre de proveedor de identidad de hello, escriba un nombre de proveedor (por ejemplo: *SPInitiatedSSO*).
   
    b. En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **Id. de entidad SAML** valor y, a continuación, péguelo en hello **emisor** cuadro de texto.
   
    c. Seleccione **Enable Workday Initiated Logout** (Habilitar el cierre de sesión iniciado de Workday).
   
    d. En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **dirección URL de cierre de sesión** valor y, a continuación, péguelo en hello **URL de solicitud de cierre de sesión** cuadro de texto.

    e. Haga clic en **Identity Provider Public Key Certificate** (Certificado de clave pública de proveedor de identidades) y, después, en **Crear**. 

    ![Crear](./media/active-directory-saas-workday-tutorial/IC782928.png "Crear")

    f. Haga clic en **Create x509 Public Key**(Crear clave pública x509). 

    ![Crear](./media/active-directory-saas-workday-tutorial/IC782929.png "Crear")


14. Hola **x509 ver clave pública** sección, lleve a cabo Hola pasos: 
   
    ![Visualización de clave pública x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Visualización de clave pública x509") 
   
    a. Hola **nombre** cuadro de texto, escriba un nombre para el certificado (por ejemplo: *PPE\_SP*).
   
    b. Hola **válido desde** cuadro de texto, hello de tipo válido de valor de atributo de su certificado.
   
    c.  Hola **válido hasta** cuadro de texto, valor de tipo hello tooattribute válida de su certificado.
   
    > [!NOTE]
    > Puede obtener Hola válido de fecha y Hola toodate válida de hello Descargar certificado haciendo doble clic en él.  aparecen las fechas de Hello en hello **detalles** ficha.
    > 
    >
   
    d.  Abra el certificado codificado en base 64 en el Bloc de notas y, a continuación, Hola copia contenido del mismo.
   
    e.  Hola **certificado** cuadro de texto, contenido de hello Pegar del Portapapeles.
   
    f.  Haga clic en **Aceptar**.

15. Lleve a cabo Hola pasos: 
   
    ![Configuración de SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuración de SSO")
   
    a.  Habilitar hello **x509 par de claves privada**.
   
    b.  Hola **Id. de proveedor de servicio** cuadro de texto, tipo **http://www.workday.com**.
   
    c.  Seleccione **Habilitar autenticación SAML iniciada por el proveedor de servicios**.
   
    d.  En el portal de Azure, en Hola Hola **configurar inicio de sesión** ventana, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **dirección URL de servicio de SSO IdP** cuadro de texto.
   
    e. Seleccione **No desinflar la solicitud de autenticación iniciada por el SP**.
   
    f. Como **Método de firma de solicitud de autenticación**, seleccione **SHA256**. 
   
    ![Método de firma de solicitud de autenticación](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Método de firma de solicitud de autenticación") 
   
    g. Haga clic en **Aceptar**. 
   
    ![ACEPTAR](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-workday-test-user"></a>Creación de un usuario de prueba de Workday

tooget un usuario de prueba aprovisionado en Workday, deberá hello toocontact [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html).
Hola [equipo de soporte técnico de Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) crea usuario Hola para usted.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkday.

![Asignar usuario][200] 

**tooassign Britta Simon tooWorkday, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Workday**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

