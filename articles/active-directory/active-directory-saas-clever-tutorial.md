---
title: "Tutorial: integración de Azure Active Directory con Clever | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a>Tutorial: integración de Azure Active Directory con Clever

En este tutorial, aprenderá cómo toointegrate Clever con Azure Active Directory (Azure AD).

Integración Clever con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooClever.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooClever (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Clever tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Clever

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Clever desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-clever-from-hello-gallery"></a>Agregar Clever desde la Galería de Hola
integración de hello tooconfigure de Clever en Azure AD, deberá tooadd Clever de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Clever de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **Clever**, seleccione **Clever** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Inteligente en la lista de resultados de Hola](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, configurará y probará el inicio de sesión único de Azure AD con Clever con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Clever es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Clever debe toobe establecido.

En Clever, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Clever, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba inteligente](#create-a-clever-test-user)**  -toohave un equivalente de Britta Simon en Clever que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación inteligente.

**inicio de sesión único en Azure AD tooconfigure con Clever, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Clever** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. En hello **tanto de esos dominios y direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://clever.com/in/<companyname>`

    b. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://clever.com/<companyname>`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente inteligente](https://clever.com/about/contact/) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. Hola aplicación inteligente espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de Token SAML** configuración.

    Hola siguiente captura de pantalla muestra un ejemplo de esto.

    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:
    
    | Nombre del atributo  | Valor de atributo |
    | --------------- | -------------------- |    
    | clever.student.credentials.district\_username  | user.userprincipalname |
    | Firstname  | user.givenname |
    | Lastname  | user.surname |    

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.

    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.

    d. Deje hello **Namespace** cuadro de texto en blanco.
    
    d. Haga clic en **Aceptar**.     

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. Hola toogenerate **metadatos** dirección url, realizar Hola pasos:

    a. Haga clic en **Registros de aplicaciones**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    b. Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    c. Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    d. Ahora vaya toohello página de propiedades de **Clever** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    e. Generar hello **dirección URL de metadatos** con hello sigue el patrón:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`   

9. En una ventana del explorador web diferente, inicie sesión en el sitio de su compañía tanto de esos tooyour como administrador.

10. En la barra de herramientas de hello, haga clic en **inicio de sesión instantáneo**.

    ![Inicio de sesión instantáneo](./media/active-directory-saas-clever-tutorial/ic798984.png "Inicio de sesión instantáneo")

11. En hello **inicio de sesión instantáneo** , siga los pasos de hello:
      
      ![Inicio de sesión instantáneo](./media/active-directory-saas-clever-tutorial/ic798985.png "Inicio de sesión instantáneo")
      
      a. Hola de tipo **dirección URL de inicio de sesión**.
      
      >[!NOTE]
      >Hola **dirección URL de inicio de sesión** es un valor personalizado. Póngase en contacto con [equipo de soporte técnico de cliente inteligente](https://clever.com/about/contact/) tooget este valor.
      
      b. En **Identity System** (Sistema de identidades), seleccione **ADFS**.

      c. Hola de tipo **dirección URL de metadatos** en hello **dirección URL de metadatos** cuadro de texto.
      
      d. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-a-clever-test-user"></a>Creación de un usuario de prueba de Clever

toolog de los usuarios de Azure AD tooenable en tooClever, se les deben aprovisionar en Clever.

En el caso de Clever, trabajar con [equipo de soporte técnico de cliente inteligente](https://clever.com/about/contact/) para agregar usuarios de Hola de plataforma inteligente Hola. Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único. 

>[!NOTE]
>Puede usar cualquier otra herramienta de creación de cuentas de usuario tanto de esos o las API proporcionadas por tooprovision inteligente cuentas de usuario de Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooClever.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooClever, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Clever**.

    ![Hola Clever vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono inteligente hello en Hola Panel de acceso, deberá obtener aplicaciones tanto de esos tooyour automáticamente ha iniciado sesión.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

