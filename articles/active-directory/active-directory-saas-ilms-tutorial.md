---
title: "Tutorial: Integración de Azure Active Directory con iLMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Tutorial: Integración de Azure Active Directory con iLMS

En este tutorial, aprenderá cómo toointegrate iLMS con Azure Active Directory (Azure AD).

Integración iLMS con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooiLMS
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooiLMS (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con iLMS tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en iLMS

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar iLMS desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-ilms-from-hello-gallery"></a>Agregar iLMS desde la Galería de Hola
integración de hello tooconfigure de iLMS en Azure AD, deberá tooadd iLMS de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd iLMS de galería de hello, lleve a cabo Hola pasos:**

1. Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **iLMS**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. En el panel de resultados de hello, seleccione **iLMS**, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con iLMS con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en iLMS es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en iLMS debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en iLMS.

tooconfigure y prueba de inicio de sesión único en Azure AD con iLMS, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Creación de un usuario de prueba iLMS](#creating-an-ilms-test-user) ** -toohave un equivalente de Britta Simon en iLMS que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación iLMS.

**inicio de sesión único en Azure AD tooconfigure con iLMS, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **iLMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. En hello **iLMS dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. Hola **identificador** cuadro de texto, pegue hello **identificador** valor copiar de **proveedor de servicios** sección de configuración de SAML en el portal de administración de iLMS.

    b. Hola **dirección URL de respuesta** cuadro de texto, pegue hello **(dirección URL del extremo)** valor copiar de **proveedor de servicios** sección de configuración de SAML en el portal de administración de iLMS tener siguiente Hola patrón`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >"123456" es un valor de ejemplo del identificador.

4. Comprobar **mostrar avanzadas de configuración de direcciones URL**, si lo desea tooconfigure aplicación de hello en **SP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, pegue hello **(dirección URL del extremo)** valor copiar de **proveedor de servicios** sección de configuración de SAML en el portal de administración de iLMS como`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT aprovisionamiento, iLMS aplicación espera las aserciones de SAML de hello en un formato concreto. Configurar Hola después de notificaciones para esta aplicación. Puede administrar valores de hello de estos atributos de hello **atributos de usuario** sección en la página de integración de aplicaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Crear **departamento, región** y **división** atributos y agregue el nombre de Hola de estos atributos en iLMS. Todos estos atributos mostrados anteriormente son obligatorios.    

    > [!NOTE] 
    > Tiene tooenable **crear cuenta de usuario de Un-recognized** en iLMS toomap estos atributos. Siga las instrucciones de hello [aquí](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget una idea en la configuración de atributos de Hola.

6. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:
    
    | Nombre del atributo | Valor de atributo |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.
    
    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.
    
    d. Haga clic en **Aceptar**.

7. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. En una ventana del explorador web diferente, inicie sesión en tooyour **portal de administración de iLMS** como administrador.

10. Haga clic en **SSO:SAML** en **configuración** ficha Configuración de SAML tooopen y realizar Hola pasos:
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Expanda hello **proveedor de servicios** sección y copia hello **identificador** y **(dirección URL del extremo)** valor.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. En la sección **Identity Provider** (Proveedor de identidades), haga clic en **Import Metadata** (Importar metadatos).
    
    c. Seleccione hello **metadatos** archivo descargado desde el Portal de Azure desde **el certificado de firma de SAML** sección.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Si desea que tooenable JIT aprovisionamiento toocreate iLMS de cuentas para anular-reconocer a los usuarios, siga los pasos siguientes:
        
       - Active **Create Un-recognized User Account** (Crear cuenta de usuario no reconocido).
       
       ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Asignar atributos de hello en Azure AD con atributos de hello en iLMS. En la columna de atributos de hello, especifique el valor de predeterminada de nombre o hello de atributos de Hola.

    e. Vaya demasiado**reglas de negocios** pestaña y realizar Hola pasos: 
        
       ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/5.png)

       - Comprobar **crear Un-recognized regiones, divisiones y departamentos** toocreate regiones, divisiones y departamentos que ya no existen en tiempo de Hola de inicio de sesión único.
        
       - Comprobar **actualizar el perfil de usuario durante inicio de sesión de** toospecify si se actualiza el perfil de usuario de hello con cada inicio de sesión único. 
        
       - Si hello **"Actualización en blanco valores para no campos en el perfil de usuario obligatorio"** opción está activada, campos de perfil opcional que están en blanco al inicio de sesión será también provocar hello iLMS perfil usuario toocontain valores en blanco para esos campos.
        
       - Comprobar **enviar correo electrónico de notificación de Error** y escriba correo electrónico de saludo del usuario de Hola donde desea que el correo electrónico de notificación de error de tooreceive Hola.

11. Haga clic en **guardar** botón Configuración de hello toosave.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-an-ilms-test-user"></a>Creación de un usuario de prueba de iLMS

Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de autenticar usuarios se crean automáticamente en la aplicación hello. JIT funcionará, si ha seleccionado hello **crear cuenta de usuario de Un-recognized** casilla durante la configuración de SAML en el portal de administración de iLMS.

Si necesita un usuario toocreate manualmente, siga pasos siguientes:

1. Inicie sesión en el sitio de la empresa iLMS tooyour como administrador.

2. Haga clic en **"Registrar usuario"** en **usuarios** ficha tooopen **Registrar usuario** página. 
   
   ![Agregar empleado](./media/active-directory-saas-ilms-tutorial/3.png)

3. En hello **"Registrar usuario"** , siga los pasos de Hola.

    ![Agregar empleado](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. Hola **nombre** cuadro de texto, tipo hello nombre Bárbara.
   
    b. Hola **Last Name** cuadro de texto, hello tipo apellidos Simon.

    c. Hola **Id. de correo electrónico** cuadro de texto, dirección de correo electrónico de Hola de tipo de cuenta de Britta Simon.

    d. Hola **región** lista desplegable valor seleccione Hola de región.

    e. Hola **división** lista desplegable, valor de hello select para la división.

    f. Hola **departamento** lista desplegable valor seleccione Hola de departamento.

    g. Haga clic en **Guardar**.

    > [!NOTE] 
    > Puede enviar toouser de correo electrónico de registro seleccionando **enviar correo de registro** casilla de verificación.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooiLMS de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooiLMS, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **iLMS**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello iLMS el icono Panel de acceso de hello, deberá obtener automáticamente ha iniciado sesión tooyour iLMS aplicación.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

