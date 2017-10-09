---
title: "Tutorial: Integración de Azure Active Directory con NetSuite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a>Tutorial: Integración de Azure Active Directory con NetSuite

En este tutorial, aprenderá cómo toointegrate Netsuite con Azure Active Directory (Azure AD).

Integración Netsuite con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooNetsuite
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNetsuite (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Netsuite tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en NetSuite

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Netsuite desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-netsuite-from-hello-gallery"></a>Agregar Netsuite desde la Galería de Hola
integración de hello tooconfigure de Netsuite en Azure AD, deberá tooadd Netsuite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Netsuite de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Netsuite**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. En el panel de resultados de hello, seleccione **Netsuite**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con NetSuite con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Netsuite es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Netsuite debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Netsuite.

tooconfigure y prueba de inicio de sesión único en Azure AD con Netsuite, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Netsuite](#creating-a-netsuite-test-user)**  -toohave un equivalente de Britta Simon en Netsuite que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Netsuite.

**inicio de sesión único en Azure AD tooconfigure con Netsuite, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **Netsuite** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. En hello **Netsuite dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`

    > [!NOTE] 
    > Este valor no es real. Valor de Hola de actualización con Hola dirección URL de respuesta real. Póngase en contacto con [equipo de soporte técnico de Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget este valor.
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. En hello **configuración de Netsuite** sección, haga clic en **configurar Netsuite** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. Abra una nueva pestaña en el explorador e inicie sesión en el sitio de la empresa Netsuite como administrador.

8. En la barra de herramientas de hello al principio de Hola de página de hello, haga clic en **el programa de instalación**, a continuación, haga clic en **el Administrador de instalación**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. De hello **tareas de configuración** lista, seleccione **integración**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. Hola **administrar autenticación** sección, haga clic en **SAML Single Sign-on**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. En hello **configuración de SAML** , siga los pasos de hello:
   
    a. Hola copia **SAML Single Sign-On dirección URL del servicio** valor de **referencia rápida** sección de **configurar inicio de sesión** y péguelo en hello **proveedor de identidades Página de inicio de sesión** campo en Netsuite.

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    b. En NetSuite, seleccione **Primary Authentication Method** (Método de autenticación principal).

    c. Para la etiqueta de campo de hello **metadatos del proveedor de identidad de SAMLV2**, seleccione **cargar archivo de metadatos de IDP**. A continuación, haga clic en **examinar** archivo de metadatos de hello tooupload que descargó del portal de Azure.

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    d. Haga clic en **Enviar**.

12. En Azure AD, haga clic en la casilla **Ver y editar todos los atributos de usuario** y agregue el atributo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. Para hello **nombre del atributo** , escriba en `account`. Para hello **valor del atributo** , escriba en el identificador de cuenta de Netsuite. Este valor es constante y cambiar con la cuenta. Instrucciones sobre cómo toofind tu identificador de cuenta se incluyen a continuación:

      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    a. En Netsuite, haga clic en **el programa de instalación** desde el menú de navegación superior de Hola.

    b. A continuación, haga clic en hello **tareas de configuración** sección del menú de navegación izquierdo de hello, seleccione hello **integración** sección y haga clic en **preferencias de servicios Web**.

    c. Copie su ID de cuenta de Netsuite y pegarlos en hello **valor del atributo** campo en Azure AD.

    ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. Antes de que los usuarios pueden realizar un inicio de sesión único en Netsuite, que deben asignarse en primer lugar los permisos adecuados de hello en Netsuite. Siga instrucciones hello tooassign estos permisos.

    a. En el menú de navegación superior de hello, haga clic en **el programa de instalación**, a continuación, haga clic en **el Administrador de instalación**.
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    b. En el menú de navegación izquierdo de hello, seleccione **usuarios/Roles**, a continuación, haga clic en **administrar funciones**.
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    c. Haga clic en **Nuevo rol**.

    d. Escriba un **nombre** para el nuevo rol, seleccione hello y **Single Sign-On solo** casilla de verificación.
      
      ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    e. Haga clic en **Guardar**.

    f. En el menú de hello en la parte superior de hello, haga clic en **permisos**. A continuación, haga clic en **Configuración**.
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    g. Seleccione **Configurar inicio de sesión único de SAM** y haga clic en **Agregar**.

    h. Haga clic en **Guardar**.

    i. En el menú de navegación superior de hello, haga clic en **el programa de instalación**, a continuación, haga clic en **el Administrador de instalación**.
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    j. En el menú de navegación izquierdo de hello, seleccione **usuarios/Roles**, a continuación, haga clic en **administrar usuarios**.
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    k. Seleccione un usuario de prueba. A continuación, haga clic en **Editar**.
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    l. En el cuadro de diálogo de Roles de hello, seleccione el rol de Hola que ha creado y haga clic en **agregar**.
      
       ![Configurar inicio de sesión único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    m. Haga clic en **Guardar**.
    
> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 

### <a name="creating-a-netsuite-test-user"></a>Creación de un usuario de prueba de NetSuite

En esta sección se creará un usuario llamado Britta Simon en NetSuite. NetSuite admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.
No hay ningún elemento de acción para usted en esta sección. Si un usuario ya no existe en Netsuite, se crea uno nuevo cuando intente tooaccess Netsuite.


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNetsuite.

![Asignar usuario][200] 

**tooassign Britta Simon tooNetsuite, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Netsuite**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

tootest Hola de su inicio de sesión configuración de inicio único, abra Panel de acceso en [https://myapps.microsoft.com](https://myapps.microsoft.com/), inicie sesión en la cuenta de prueba de Hola y haga clic en **Netsuite**.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configuración del aprovisionamiento de usuarios](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

