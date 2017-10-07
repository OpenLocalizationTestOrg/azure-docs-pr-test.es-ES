---
title: "Tutorial: Integración de Azure Active Directory con Sugar CRM | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a>Tutorial: Integración de Azure Active Directory con Sugar CRM

En este tutorial, aprenderá cómo toointegrate Sugar CRM con Azure Active Directory (Azure AD).

Integración de Sugar CRM con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSugar CRM
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSugar CRM (inicio de sesión único) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Sugar CRM, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Un suscripción habilitada para el inicio de sesión único en SugarCRM

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Sugar CRM desde galería Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-sugar-crm-from-hello-gallery"></a>Agregar Sugar CRM desde galería Hola
integración de hello tooconfigure de Sugar CRM en Azure AD, deberá tooadd Sugar CRM de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Sugar CRM de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Sugar CRM**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. En el panel de resultados de hello, seleccione **Sugar CRM**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Sugar CRM con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Sugar CRM es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Sugar CRM debe toobe establecido.

En Sugar CRM, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Sugar CRM, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave un equivalente de Britta Simon en Sugar CRM que está vinculado toohello Azure AD representación del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Sugar CRM.

**inicio de sesión único en Azure AD tooconfigure con Sugar CRM, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Sugar CRM** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. En hello **Sugar CRM dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > valor de Hello no es real. Valor de Hola de actualización con Hola dirección URL de inicio de sesión real. Póngase en contacto con [equipo de soporte técnico de Sugar CRM cliente](https://support.sugarcrm.com/) valor de hello tooget. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. En hello **Sugar CRM configuración** sección, haga clic en **configurar Sugar CRM** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de Sugar CRM tooyour como administrador.

8. Vaya demasiado**administración**.
   
    ![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administración")

9. Hola **administración** sección, haga clic en **administración de contraseñas**.
   
    ![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administración")

10. Seleccione **Habilitar autenticación SAML**.
   
    ![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administración")

11. Hola **autenticación SAML** sección, lleve a cabo Hola pasos:
   
    ![Autenticación SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Autenticación SAML")  
 
    a. Hola **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.
  
    b. Hola **dirección URL de SLO** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.
  
    c. Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, pegue Hola certificado completo en **certificado X.509** cuadro de texto.
  
    d. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-sugar-crm-test-user"></a>Creación de un usuario de prueba de Sugar CRM

En orden tooenable toolog de los usuarios de Azure AD en tooSugar CRM, deben ser aprovisionado tooSugar CRM.

En caso de hello de Sugar CRM, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **Sugar CRM** como administrador.

2. Vaya demasiado**administración**.
   
    ![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administración")

3. Hola **administración** sección, haga clic en **administración de usuarios**.
   
    ![Administración](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administración")

4. Vaya demasiado**usuarios \> crear nuevo usuario**.
   
    ![Creación de nuevos usuarios](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Creación de nuevos usuarios")

5. En hello **perfil de usuario** , realice los pasos de hello:
   
    ![Nuevo usuario](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Nuevo usuario")

    a. Hola de tipo **nombre de usuario**, **apellidos**, y **dirección de correo electrónico** de un usuario de Azure Active Directory válido en hello relacionados con cuadros de texto.
  
6. Como **Estado**, seleccione **Activo**.

7. En la ficha contraseña de hello, realizar Hola pasos:
   
    ![Nuevo usuario](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Nuevo usuario")

    a. Escriba la contraseña de hello en hello relacionado con cuadro de texto.

    b. Haga clic en **Guardar**.

>[!NOTE]
>Puede usar cualquier otra Sugar CRM usuario cuenta herramienta de creación o las API proporcionadas por Sugar CRM tooprovision cuentas de usuario AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSugar CRM.

![Asignar usuario][200] 

**tooassign Britta Simon tooSugar CRM, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Sugar CRM**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de Sugar CRM Hola Hola Panel de acceso, deberá obtener la aplicación de Sugar CRM tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

