---
title: "Tutorial: Integración de Azure Active Directory con ServiceChannel | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a>Tutorial: Integración de Azure Active Directory con ServiceChannel

En este tutorial, aprenderá cómo toointegrate ServiceChannel con Azure Active Directory (Azure AD).

Integración de ServiceChannel con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooServiceChannel
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooServiceChannel (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con ServiceChannel tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en ServiceChannel

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar ServiceChannel desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-servicechannel-from-hello-gallery"></a>Agregar ServiceChannel desde la Galería de Hola
integración de hello tooconfigure de ServiceChannel en Azure AD, deberá tooadd ServiceChannel de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd ServiceChannel de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **ServiceChannel**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. En el panel de resultados de hello, seleccione **ServiceChannel**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con ServiceChannel con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ServiceChannel es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ServiceChannel debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de ServiceChannel.

tooconfigure y prueba de inicio de sesión único en Azure AD con ServiceChannel, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de ServiceChannel](#creating-a-servicechannel-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de ServiceChannel.

**inicio de sesión único en Azure AD tooconfigure con ServiceChannel, realizar Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **ServiceChannel** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. En hello **ServiceChannel dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    a. Hola **identificador** cuadro de texto, valor de tipo hello como:`http://adfs.<domain>.com/adfs/service/trust`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<customer domain>.servicechannel.com/saml/acs`

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tener tooupdate estos valores con hello URL de identificador y la respuesta real. Aquí le sugerimos toouse Hola único valor de cadena en hello identificador. Póngase en contacto con [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) tooget estos valores.

4. La aplicación de ServiceChannel espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones. Hola siguiente captura de pantalla muestra un ejemplo de esto. **NameIdentifier (identificador de usuario)** es Hola solo notificación obligatoria y es el valor predeterminado de hello **user.userprincipalname** pero ServiceChannel espera este toobe asignado con **user.mail**. Si tiene previsto aprovisionamiento de usuarios solo en tiempo de tooenable, debe agregar Hola después notificaciones tal y como se muestra a continuación. **Rol** notificación necesita toobe asignado demasiado**user.assignedroles** que contiene la función de saludo del usuario de Hola.  

    Puede consultar la guía de ServiceChannel [aquí](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) para obtener más información sobre las notificaciones.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > Haga clic en [aquí](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow cómo tooconfigure **rol** en Azure AD

5. En **atributos de usuario** sección, haga clic en **ver y editar todos los demás atributos de usuario** y establezca los atributos de Hola.

    | Nombre del atributo | Valor de atributo |
    | --- | --- |    
    | Rol| user.assignedroles |

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.
    
    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.
    
    d. Haga clic en **Aceptar**.
    
6. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. Haga clic en **Guardar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. En hello **configuración de ServiceChannel** sección, haga clic en **configurar ServiceChannel** tooopen **configurar inicio de sesión** ventana. Tenga en cuenta que hello **SAML Entity ID** de hello **referencia rápida** sección.

9. tooconfigure inicio de sesión único en **ServiceChannel** lado, necesita hello toosend descargado **certificado (Base64)** y **Id. de entidad SAML** demasiado[ Equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us). Configurará esto Hola de toohave orden configurada correctamente en ambos lados de la conexión de SSO de SAML.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 

### <a name="creating-a-servicechannel-test-user"></a>Crear un usuario de prueba de ServiceChannel

Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de que los usuarios de autenticación se creará en la aplicación hello automáticamente. Para el aprovisionamiento de usuario completo, póngase en contacto con el [equipo de soporte técnico de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooServiceChannel de acceso.

![Asignar usuario][200] 

**tooassign Britta Simon tooServiceChannel, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ServiceChannel**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de ServiceChannel Hola Hola Panel de acceso, deberá obtener aplicaciones de ServiceChannel tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png