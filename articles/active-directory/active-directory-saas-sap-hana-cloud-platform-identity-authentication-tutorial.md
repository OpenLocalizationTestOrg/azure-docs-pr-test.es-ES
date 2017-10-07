---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform Identity Authentication | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SAP HANA autenticación de la identidad de plataforma de nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform Identity Authentication

En este tutorial, aprenderá cómo toointegrate SAP HANA autenticación de identidades de plataforma de nube con Azure Active Directory (Azure AD). Autenticación de la identidad de plataforma de nube de SAP HANA se utiliza como un proxy IdP tooaccess las aplicaciones SAP con Azure AD como Hola IdP principal.

Integración de autenticación de la identidad de plataforma de nube de SAP HANA con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSAP aplicación
- Puede habilitar los usuarios tooautomatically get tooSAP ha iniciado sesión con las aplicaciones inicio de sesión único (SSO) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con autenticación de la identidad de plataforma de nube de SAP HANA, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción de **SAP HANA Cloud Platform Identity Authentication** con el inicio de sesión único habilitado


>[!NOTE] 
>Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
>

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar la autenticación de la identidad de plataforma de nube de SAP HANA desde la Galería de Hola
2. Configuración y prueba del inicio de sesión único de Azure AD

Antes de entrar en detalles técnicos de hello, resulta vital toounderstand conceptos de hello en que va toolook. Hola federación de Active Directory de Azure y autenticación de la identidad de plataforma de nube de SAP HANA permite tooimplement SSO a través de aplicaciones o servicios protegidos por AAD (como un IdP) con aplicaciones de SAP y servicios protegidos por identidad de plataforma de nube de SAP HANA Autenticación.

Actualmente, autenticación de la identidad de plataforma de nube de SAP HANA actúa como un proveedor de identidades de Proxy tooSAP-aplicaciones. A su vez, Azure Active Directory actúa como Hola iniciales de proveedor de identidades en este programa de instalación. 

Hola siguiente diagrama muestra cómo hacerlo:    

![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

Con esta configuración, su inquilino de SAP HANA Cloud Platform Identity Authentication se configurará como una aplicación de confianza en Azure Active Directory. 

Todas las aplicaciones de SAP y los servicios que desee tooprotect a través de esta manera se configuran posteriormente en la consola de administración de autenticación de la identidad de plataforma de nube de SAP HANA Hola!

Esto significa que esa autorización para conceder acceso tooSAP aplicaciones y servicios necesidades tootake lugar en la autenticación de la identidad de plataforma de nube de SAP HANA para dicha configuración (como autorización tooconfiguring lugar en Azure Active Directory).

Mediante la configuración de autenticación de la identidad de plataforma de nube de SAP HANA como una aplicación a través de hello Azure Active Directory Marketplace, no es necesario tootake atención configurar notificaciones individuales necesarios y las aserciones de SAML y transformaciones necesitan tooproduce un token de autenticación válido para las aplicaciones de SAP.

>[!NOTE] 
>Actualmente, el SSO web solo se ha probado en ambas soluciones. Aunque los flujos necesarios para establecer comunicación de aplicación a API o de API a API deberían funcionar, todavía no se han probado. Sin embargo, sí que se hará en actividades posteriores.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Agregar autenticación de la identidad de plataforma de nube de SAP HANA desde la Galería de Hola
integración de hello tooconfigure de autenticación de la identidad de plataforma de nube de SAP HANA en Azure AD, deberá tooadd autenticación de la identidad de plataforma de nube de SAP HANA en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd autenticación de identidad de SAP HANA en la nube plataforma desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola [ **portal de administración de Azure**](https://portal.azure.com), en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **autenticación de la identidad de plataforma de nube de SAP HANA**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. En el panel de resultados de hello, seleccione **autenticación de la identidad de plataforma de nube de SAP HANA**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, se configura y prueba el inicio de sesión único de Azure AD con SAP HANA Cloud Platform Identity Authentication con un usuario de prueba llamado "Britta Simon".

Para toowork SSO, Azure AD necesita tooknow qué usuario equivalente de hello en autenticación de la identidad de plataforma de nube de SAP HANA es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en autenticación de la identidad de plataforma de nube de SAP HANA debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de autenticación de la identidad de plataforma de nube de SAP HANA.

tooconfigure y prueba de Azure AD SSO con la autenticación de la identidad de plataforma de nube de SAP HANA, deberá hello toocomplete después de bloques de creación:

1. **[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de autenticación de la identidad de plataforma de nube de SAP HANA](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave un equivalente de Britta Simon en la plataforma de identidad autenticación SAP HANA en la nube es representación toohello vinculado Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilita el SSO de Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de autenticación de la identidad de plataforma de nube de SAP HANA.

Aplicación de autenticación de la identidad de plataforma de nube de SAP HANA espera las aserciones de SAML de hello en un formato concreto. Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto.

![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure SSO de AD de Azure con la autenticación de identidades de plataforma de nube de SAP HANA, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **autenticación de la identidad de plataforma de nube de SAP HANA** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único][5]

3. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, si la aplicación SAP espera un atributo, por ejemplo "firstName". En el cuadro de diálogo de atributos de token de SAML de hello, Agregar atributo de "firstName" Hola.
 1. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.
 
    ![Configurar inicio de sesión único][6]

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello "firstName".
 3. De hello **valor del atributo** lista, el valor del atributo Hola seleccione "user.givenname".
 4. Haga clic en **Aceptar**.

4. En hello **dominio de autenticación de la identidad de plataforma de SAP HANA en la nube y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba el inicio de sesión de Hola en dirección URL para la aplicación de SAP de hello.
 2. Hola **identificador** cuadro de texto, valor de Hola de tipo siguiente patrón:`<entity-id>.accounts.ondemand.com` 
    * Si no sabe este valor, siga documentación de autenticación de la identidad de plataforma de nube de SAP HANA hello en [inquilino SAML 2.0 configuración](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. En hello **configuración de autenticación de identidad de SAP HANA Cloud plataforma** sección, haga clic en **configurar autenticación de identidad de plataforma de SAP HANA en la nube** tooopen **configurardeiniciodesesión** cuadro de diálogo. A continuación, haga clic en **metadatos XML de SAML** y guarde el archivo hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget SSO configurado para la aplicación, vaya tooSAP consola de administración de la autenticación de identidad de HANA nube plataforma. dirección URL de Hello tiene Hola siguiente patrón:`https://<tenant-id>.accounts.ondemand.com/admin`
 * A continuación, siga documentación hello en autenticación de la identidad de plataforma de nube de SAP HANA demasiado[configurar Microsoft Azure AD como proveedor de identidad corporativa en autenticación de la identidad de plataforma de nube de SAP HANA](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. En el portal de administración de Azure de hello, haga clic en **guardar** botón.
8. Continuar Hola siguientes pasos únicamente si desea tooadd y habilitar SSO para otra aplicación de SAP. Repita los pasos en hello sección "Agregar SAP HANA nube plataforma autenticación de la identidad de la Galería de Hola" tooadd otra instancia de la autenticación de la identidad de plataforma de nube de SAP HANA.
9. En el portal de administración de Azure de hello, en hello **autenticación de la identidad de plataforma de nube de SAP HANA** página de integración de aplicaciones, haga clic en **en el inicio de sesión vinculado**.

    ![Configuración del inicio de sesión vinculado](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. A continuación, guarde la configuración de Hola.

>[!NOTE] 
>nueva aplicación de Hello aprovecharán la configuración de SSO de hello para la aplicación de SAP de hello anterior. Asegúrese de que se use Hola mismo proveedores de identidad corporativa en hello consola de administración de autenticación de SAP HANA nube plataforma de identidad.
>

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es toocreate un usuario de prueba en el nuevo portal de hello llamado a Britta Simon.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.
  2. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.
  3. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.
  4. Haga clic en **Crear**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Creación de un usuario de prueba de SAP HANA Cloud Platform Identity Authentication

No es necesario toocreate un usuario en la autenticación de la identidad de plataforma de nube de SAP HANA. Los usuarios que están en el almacén del usuario de hello Azure AD pueden usar la funcionalidad SSO de Hola.

Autenticación de la identidad de plataforma de nube de SAP HANA es compatible con la opción de federación de identidades de Hola. Esta opción permite Hola aplicación toocheck si los usuarios de hello autenticados por el proveedor de identidad corporativa Hola existen en hello almacén de SAP HANA en la nube plataforma de identidad de autenticación de usuario. 

En la configuración predeterminada de hello, opción de federación de identidades de hello está deshabilitada. Si se habilita la federación de identidades, solo los usuarios de Hola que se importan de autenticación de la identidad de plataforma de nube de SAP HANA son tooaccess capaz de aplicación de hello. 

Para obtener más información sobre cómo tooenable o deshabilitar la federación de identidades con autenticación de identidades de plataforma de nube de SAP HANA, vea Habilitar la federación de identidades con autenticación de identidades de plataforma de nube de SAP HANA en [Configurar federación de identidades con hello almacén de SAP HANA nube plataforma de identidad de autenticación de usuario. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSAP acceso HANA autenticación de la identidad de plataforma de nube.

![Asignar usuario][200] 

**tooassign Britta Simon tooSAP autenticación de identidades de plataforma de nube de HANA, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **autenticación de la identidad de plataforma de nube de SAP HANA**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    

### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de autenticación de la identidad de plataforma de nube de SAP HANA Hola Hola Panel de acceso, deberá obtener la aplicación de autenticación de la identidad de plataforma de nube de SAP HANA tooyour automáticamente ha iniciado sesión.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png