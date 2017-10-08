---
title: "Tutorial: Integración de Azure Active Directory con TimeOffManager | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Tutorial: Integración de Azure Active Directory con TimeOffManager

En este tutorial, aprenderá cómo toointegrate TimeOffManager con Azure Active Directory (Azure AD).

Integración de TimeOffManager con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTimeOffManager
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTimeOffManager (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con TimeOffManager tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en TimeOffManager

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar TimeOffManager de galería de Hola
2. Configuración y prueba del inicio de sesión único en Azure AD

## <a name="add-timeoffmanager-from-hello-gallery"></a>Agregar TimeOffManager de galería de Hola
integración de hello tooconfigure de TimeOffManager en Azure AD, deberá tooadd TimeOffManager de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd TimeOffManager de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **TimeOffManager**, seleccione **TimeOffManager** desde el panel de resultados y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Incorporación desde la galería](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TimeOffManager utilizando un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TimeOffManager es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TimeOffManager debe toobe establecido.

En TimeOffManager, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con TimeOffManager, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave un equivalente de Britta Simon en TimeOffManager que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TimeOffManager.

**inicio de sesión único en Azure AD tooconfigure con TimeOffManager, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **TimeOffManager** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. En hello **TimeOffManager dominio y las direcciones URL** sección, realice Hola siguiente:

     ![Sección Dominio y direcciones URL de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Este valor no es real. Actualizar este valor con la dirección URL de respuesta real Hola. Puede obtener este valor de **inicio de sesión único en la página de configuración de** que se explica más adelante en el tutorial de Hola o póngase en contacto con [equipo de soporte técnico de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Sección Certificado de firma SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooTimeOffManger con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.
    
    La aplicación TimeOffManger espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto.

    ![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Atributos de token de SAML")
    
    | Nombre del atributo | Valor de atributo |
    | --- | --- |
    | Firstname |User.givenname |
    | Lastname |User.surname |
    | Email |User.mail |
    
    a.  Para cada fila de datos de tabla de hello anterior, haga clic en **Agregar atributo de usuario**.
    
    ![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Atributos de token de SAML")
    
    ![Atributos de token de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Atributos de token de SAML")
    
    b.  Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.
    
    c.  Hola **valor del atributo** cuadro de texto, valor de atributo seleccione Hola se muestra para esa fila.
    
    d.  Haga clic en **Aceptar**.
    
6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. En hello **configuración de TimeOffManager** sección, haga clic en **configurar TimeOffManager** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Sección Configuración de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de TimeOffManager.

9. Vaya demasiado**cuenta \> opciones de cuenta \> configuración de inicio de sesión único**.
   
   ![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Configuración de inicio de sesión único")
7. Hola **configuración de inicio de sesión único** sección, lleve a cabo Hola pasos:
   
   ![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Configuración de inicio de sesión único")
   
   a. Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, pegue Hola certificado completo en **certificado X.509** cuadro de texto.
   
   b. En **emisor Idp** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.
   
   c. En **dirección URL del extremo IdP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.
   
   d. En **Aplicar SAML**, seleccione **No**.
   
   e. En **Crear usuarios automáticamente**, seleccione **Sí**.
   
   f. En **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.
   
   g. Haga clic en **Guardar cambios**.

11. En **configuración de inicio de sesión único** Hola de copiar valor de la página **dirección URL del servicio de consumidor de aserción** y péguelo en hello **dirección URL de respuesta** cuadro de texto bajo **TimeOffManager Dominio y las direcciones URL** sección en el portal de Azure. 

      ![Configuración de inicio de sesión único](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Configuración de inicio de sesión único")

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Usuarios y grupos --> Todos los usuarios](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Botón Agregar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Página del cuadro de diálogo Usuario](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Creación de un usuario de prueba de TimeOffManager

En orden tooenable toolog de los usuarios de Azure AD en TimeOffManager, deben ser tooTimeOffManager aprovisionado.  

TimeOffManager admite aprovisionamiento de usuarios justo a tiempo. No hay ningún elemento de acción para usted.  

los usuarios de Hola se agregan automáticamente durante el saludo primer inicio de sesión con el inicio de sesión único en.

>[!NOTE]
>Puede usar cualquier otra TimeOffManager usuario cuenta herramienta de creación o las API proporcionadas por TimeOffManager tooprovision cuentas de usuario de Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTimeOffManager.

![Asignar usuario][200] 

**tooassign Britta Simon tooTimeOffManager, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **TimeOffManager**.

    ![TimeOffManager en la lista de aplicaciones](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de TimeOffManager Hola Hola Panel de acceso, deberá obtener aplicaciones de TimeOffManager tooyour automáticamente ha iniciado sesión. Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

