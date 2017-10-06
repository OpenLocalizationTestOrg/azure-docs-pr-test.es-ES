---
title: "Tutorial: Integración de Azure Active Directory con AirWatch | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Tutorial: Integración de Azure Active Directory con AirWatch

En este tutorial, aprenderá cómo toointegrate AirWatch con Azure Active Directory (Azure AD).

Integración de AirWatch con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooAirWatch
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAirWatch (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con AirWatch tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en AirWatch

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar AirWatch desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-airwatch-from-hello-gallery"></a>Agregar AirWatch desde la Galería de Hola
integración de hello tooconfigure de AirWatch en Azure AD, deberá tooadd AirWatch de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd AirWatch de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **AirWatch**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. En el panel de resultados de hello, seleccione **AirWatch**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AirWatch con un usuario de prueba llamado Britta Simon.

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en AirWatch es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en AirWatch debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en AirWatch.

tooconfigure y prueba de inicio de sesión único en Azure AD con AirWatch, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de AirWatch](#creating-a-airwatch-test-user)**  -toohave un equivalente de Britta Simon en AirWatch que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación AirWatch.

**inicio de sesión único en Azure AD tooconfigure con AirWatch, realice Hola pasos:**

1. En el portal de Azure, en Hola Hola **AirWatch** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. En hello **AirWatch dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. Hola **identificador** cuadro de texto, valor de tipo hello como`AirWatch`

    > [!NOTE] 
    > Este valor no es hello real. Actualizar este valor con la URL de inicio de sesión real de Hola. Póngase en contacto con [equipo de soporte técnico de cliente de AirWatch](http://www.air-watch.com/company/contact-us/) tooget este valor. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. En hello **configuración de AirWatch** sección, haga clic en **configurar AirWatch** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Haga clic en el botón **Guardar**.

    ![Configuración del inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa tooyour AirWatch como administrador.

8. En el panel de navegación izquierdo de hello, haga clic en **cuentas**y, a continuación, haga clic en **administradores**.
   
   ![Administradores](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administradores")

9. Expanda hello **configuración** menú y, a continuación, haga clic en **servicios de directorio**.
   
   ![Configuración](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Configuración")

10. Haga clic en hello **usuario** ficha Hola **DN Base** cuadro de texto, escriba el nombre de dominio y, a continuación, haga clic en **guardar**.
   
   ![Usuario](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Usuario")

11. Haga clic en hello **Server** ficha.
   
   ![Servidor](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Servidor")

12. Lleve a cabo Hola pasos:
    
    ![Cargar](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Cargar")   
    
    a. En **Directory Type** (Tipo de directorio), seleccione **None** (Ninguno).

    b. Seleccione **Use SAML For Authentication**(Usar SAML para autenticación).

    c. tooupload Hola certificado descargado, haga clic en **cargar**.

13. Hola **solicitar** sección, lleve a cabo Hola pasos:
    
    ![Solicitud](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Solicitud")  

    a. En **Request Binding Type** (Tipo de enlace de solicitud), seleccione **POST**.

    b. En el portal de Azure, en Hola Hola **configurar inicio de sesión único en Airwatch** página de diálogo, Hola copia **SAML Single Sign-On dirección URL del servicio** valor y, a continuación, péguelo en hello **proveedor de identidades Solo la dirección URL de inicio de sesión** cuadro de texto.

    c. En la lista **NameID Format** (Formato de NameID), seleccione **Email address** (Dirección de correo electrónico).

    d. Haga clic en **Guardar**.

14. Haga clic en hello **usuario** ficha de nuevo.
    
    ![Usuario](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Usuario")

15. Hola **atributo** sección, lleve a cabo Hola pasos:
    
    ![Atributo](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Atributo")

    a. Hola **identificador de objeto** cuadro de texto, tipo **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. Hola **nombre de usuario** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. Hola **nombre para mostrar** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. Hola **nombre** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    e. Hola **Last Name** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. Hola **correo electrónico** cuadro de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    g. Haga clic en **Guardar**.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-airwatch-test-user"></a>Creación de un usuario de prueba de AirWatch

toolog de los usuarios de Azure AD tooenable en tooAirWatch, se les deben aprovisionar en tooAirWatch.

* En el caso de AirWatch, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **AirWatch** como administrador.
2. En el panel de navegación de hello en el lado izquierdo de hello, haga clic en **cuentas**y, a continuación, haga clic en **usuarios**.
   
   ![Usuarios](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Usuarios")
3. Hola **usuarios** menú, haga clic en **vista de lista**y, a continuación, haga clic en **agregar \> Agregar usuario**.
   
   ![Agregar usuario](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Agregar usuario")
4. En hello **Agregar / Editar usuario** cuadro de diálogo, realizar Hola pasos:

   ![Agregar usuario](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Agregar usuario")   
   1. Hola de tipo **nombre de usuario**, **contraseña**, **Confirmar contraseña**, **nombre**, **Last Name**,  **Dirección de correo electrónico** de un Azure válida cuadros de texto relacionadas con la cuenta de Active Directory que quiera tooprovision en Hola.
   2. Haga clic en **Guardar**.

>[!NOTE]
>Puede usar cualquier otra AirWatch usuario cuenta herramienta de creación o las API proporcionadas por AirWatch tooprovision cuentas de usuario AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAirWatch.

![Asignar usuario][200] 

**tooassign Britta Simon tooAirWatch, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **AirWatch**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

