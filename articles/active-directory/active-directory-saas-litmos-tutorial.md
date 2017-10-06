---
title: "Tutorial: integración de Azure Active Directory con Litmos | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a>Tutorial: Integración de Azure Active Directory con Litmos

En este tutorial, aprenderá cómo toointegrate Litmos con Azure Active Directory (Azure AD).

Integración Litmos con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooLitmos.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLitmos (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con Litmos tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Litmos

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar Litmos desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-litmos-from-hello-gallery"></a>Agregar Litmos desde la Galería de Hola
integración de hello tooconfigure de Litmos en Azure AD, deberá tooadd Litmos de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Litmos de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **Litmos**, seleccione **Litmos** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Litmos en la lista de resultados de Hola](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Litmos con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Litmos es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Litmos debe toobe establecido.

En Litmos, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con Litmos, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba Litmos](#create-a-litmos-test-user)**  -toohave un equivalente de Britta Simon en Litmos que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Litmos.

**inicio de sesión único en Azure AD tooconfigure con Litmos, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **Litmos** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. En hello **Litmos dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.litmos.com/account/Login`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.litmos.com/integration/samllogin`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con URL real de identificador y la respuesta de hello, que se explican más adelante en el tutorial o póngase en contacto con [equipo de soporte técnico Litmos](https://www.litmos.com/contact-us/) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. Como parte de la configuración de hello, necesita hello toocustomize **atributos de Token SAML** para la aplicación Litmos.

    ![Sección atributos](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | Nombre del atributo   | Valor de atributo |   
    | ---------------  | ----------------|
    | Nombre |user.givenname |
    | Apellidos  |user.surname |
    | Email |user.mail |

    a. Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.

    ![Agregar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Cuadro de diálogo Agregar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    b. Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.

    c. De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.
    
    d. Haga clic en **Aceptar**.     

6. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. En otra ventana del explorador, inicio de sesión tooyour Litmos el sitio de la empresa como administrador.

8. En la barra de navegación de hello en el lado izquierdo de hello, haga clic en **cuentas**.
   
    ![Sección Cuentas en la aplicación][22] 

9. Haga clic en hello **integraciones** ficha.
   
    ![Pestaña Integración][23] 

10. En hello **integraciones** ficha, desplácese hacia abajo demasiado**3rd integraciones de entidad**y, a continuación, haga clic en **SAML 2.0** ficha.
   
    ![Sección SAML 2.0][24] 

11. Copiar valor de hello en **Hola extremo de SAML para litmos es:** y péguelo en hello **dirección URL de respuesta** cuadro de texto en hello **Litmos dominio y las direcciones URL** sección en el portal de Azure. 
   
    ![Punto de conexión de SAML][26] 

12. En su **Litmos** aplicación, realizar Hola pasos:
    
     ![Aplicación Litmos][25] 
     
     a. Haga clic en **Enable SAML**(Habilitar SAML).
    
     b. Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509 de SAML** cuadro de texto.
     
     c. Haga clic en **Guardar cambios**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
  
### <a name="create-a-litmos-test-user"></a>Creación de un usuario de prueba en Litmos

objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Litmos toocreate.  
Hola Litmos aplicación admite Just-in-Time de aprovisionamiento. Esto significa que, una cuenta de usuario se crea automáticamente si es necesario durante una aplicación de Hola de tooaccess intento con hello Panel de acceso.

**toocreate un usuario llamado Britta Simon en Litmos, lleve a cabo Hola pasos:**

1. En otra ventana del explorador, inicio de sesión tooyour Litmos el sitio de la empresa como administrador.

2. En la barra de navegación de hello en el lado izquierdo de hello, haga clic en **cuentas**.
   
    ![Sección Cuentas en la aplicación][22] 

3. Haga clic en hello **integraciones** ficha.
   
    ![Pestaña Integraciones][23] 

4. En hello **integraciones** ficha, desplácese hacia abajo demasiado**3rd integraciones de entidad**y, a continuación, haga clic en **SAML 2.0** ficha.
   
    ![SAML 2.0][24] 
    
5. Seleccione **Autogenerate Users**(Generar usuarios automáticamente)
   
    ![Generar usuarios automáticamente][27] 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLitmos.

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooLitmos, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Litmos**.

    ![vínculo de Litmos Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.  

Al hacer clic en hello Litmos el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Litmos aplicación. 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

