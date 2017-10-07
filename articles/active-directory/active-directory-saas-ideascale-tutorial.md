---
title: "Tutorial: integración de Azure Active Directory con IdeaScale | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Tutorial: integración de Azure Active Directory con IdeaScale

En este tutorial, aprenderá cómo toointegrate IdeaScale con Azure Active Directory (Azure AD).

Integración de IdeaScale con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooIdeaScale
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooIdeaScale (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con IdeaScale tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en IdeaScale

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar IdeaScale desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-ideascale-from-hello-gallery"></a>Agregar IdeaScale desde la Galería de Hola
integración de hello tooconfigure de IdeaScale en Azure AD, deberá tooadd IdeaScale de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd IdeaScale de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **IdeaScale**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. En el panel de resultados de hello, seleccione **IdeaScale**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con IdeaScale con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en IdeaScale es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en IdeaScale debe toobe establecido.

En IdeaScale, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con IdeaScale, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Creación de un usuario de prueba de IdeaScale](#creating-an-ideascale-test-user)**  -toohave un equivalente de Britta Simon en IdeaScale que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de IdeaScale.

**inicio de sesión único en Azure AD tooconfigure con IdeaScale, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **IdeaScale** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. En hello **IdeaScale dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.ideascale.com`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de IdeaScale](http://support.ideascale.com/) tooget estos valores. 
 
4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. En hello **configuración de IdeaScale** sección, haga clic en **configurar IdeaScale** tooopen **configurar inicio de sesión** ventana. Hola copia **dirección URL de cierre de sesión y el Id. de entidad SAML** de hello **sección de referencia rápida**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía IdeaScale tooyour como administrador.

8. Vaya demasiado**configuración de la Comunidad**.
   
    ![Configuración de la Comunidad](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configuración de la Comunidad")

9. Vaya demasiado**seguridad \> configuración de inicio de sesión único**.
   
    ![Configuración de inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Configuración de inicio de sesión único")

10. En **Single-Signon Type** (Tipo de inicio de sesión único), seleccione **SAML 2.0**.
   
    ![Tipo de inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Tipo de inicio de sesión único")

11. En hello **configuración de inicio de sesión único** cuadro de diálogo, realizar Hola pasos:
   
    ![Configuración de inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Configuración de inicio de sesión único")
   
    a. En **Id. de entidad de SAML IdP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.

    b. Copie el contenido de hello del archivo de metadatos descargado desde el portal de Azure y péguelo en hello **metadatos SAML IdP** cuadro de texto.

    c. En **URL de cierre de sesión** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.

    d. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-an-ideascale-test-user"></a>Creación de un usuario de prueba de IdeaScale

toolog de los usuarios de Azure AD tooenable en IdeaScale, se les deben aprovisionar en tooIdeaScale. En caso de hello de IdeaScale, el aprovisionamiento es una tarea manual.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicie sesión en tooyour **IdeaScale** como administrador.

2. Vaya demasiado**configuración de la Comunidad**.
   
    ![Configuración de la Comunidad](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configuración de la Comunidad")

3. Vaya demasiado**configuración básica \> miembro administración**.

4. Haga clic en **Agregar miembro**.
   
    ![Administración de miembros](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Administración de miembros")

5. En la sección Agregar nuevo miembro hello, realizar Hola pasos:
   
    ![Agregar nuevo miembro](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Agregar nuevo miembro")
   
    a. Hola **direcciones de correo electrónico** cuadro de texto, dirección de correo electrónico de tipo hello de una cuenta válida de AAD que desee tooprovision.
   
    b. Haga clic en **Guardar cambios**. 
   
    >[!NOTE]
    >titular de la cuenta de Hello Azure Active Directory Obtiene un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.
      
>[!NOTE]
>Puede usar cualquier otra IdeaScale usuario cuenta herramienta de creación o las API proporcionadas por IdeaScale tooprovision cuentas de usuario AAD.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooIdeaScale.

![Asignar usuario][200] 

**tooassign Britta Simon tooIdeaScale, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **IdeaScale**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 


objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.

Al hacer clic en icono de IdeaScale Hola Hola Panel de acceso, deberá obtener la aplicación de IdeaScale tooyour automáticamente ha iniciado sesión.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

