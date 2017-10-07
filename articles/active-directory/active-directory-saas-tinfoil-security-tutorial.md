---
title: "Tutorial: Integración de Azure Active Directory con TINFOIL SECURITY | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Tutorial: Integración de Azure Active Directory con TINFOIL SECURITY

En este tutorial, aprenderá cómo toointegrate TINFOIL SECURITY con Azure Active Directory (Azure AD).

Integración de TINFOIL SECURITY con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooTINFOIL seguridad
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTINFOIL seguridad (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con TINFOIL SECURITY tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en TINFOIL SECURITY

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar TINFOIL SECURITY de galería de Hola
2. Configuración y prueba del inicio de sesión único en Azure AD

## <a name="add-tinfoil-security-from-hello-gallery"></a>Agregar TINFOIL SECURITY de galería de Hola
integración de hello tooconfigure de TINFOIL SECURITY en Azure AD, deberá tooadd TINFOIL SECURITY de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd TINFOIL SECURITY de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **TINFOIL SECURITY**, seleccione **TINFOIL SECURITY** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![TINFOIL SECURITY desde la galería](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con TINFOIL SECURITY con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en TINFOIL SECURITY es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en TINFOIL SECURITY debe toobe establecido.

En TINFOIL SECURITY, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con TINFOIL SECURITY, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave un equivalente de Britta Simon en TINFOIL SECURITY que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de TINFOIL SECURITY.

**inicio de sesión único en tooconfigure AD de Azure con TINFOIL SECURITY, siga Hola pasos:**

1. En el portal de Azure, en Hola Hola **TINFOIL SECURITY** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Inicio de sesión basado en SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. En hello **TINFOIL SECURITY dominio y las direcciones URL** sección, hello usuario no tiene tooperform todos los pasos tal y como aplicación hello ya está integrado previamente con Azure.

    ![Configurar inicio de sesión único](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** valor.

    ![Sección Certificado de firma SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:
    
    ![Atributos](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Atributos")
    
    | Nombre del atributo    |   Valor de atributo |
    | ------------------- | -------------------- |
    | accountid | UXXXXXXXXXXXXX |
    
    a. Haga clic en **agregar atributo de usuario**.
    
    ![AGREGAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")
    
    ![AGREGAR atributo](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")
    
    b. Hola **nombre del atributo** cuadro de texto, tipo **accountid**.
    
    c. Hola **valor del atributo** cuadro de texto, valor de identificador de cuenta de hello de pegar que obtendrá más adelante en el tutorial de Hola.
    
    d. Haga clic en **Aceptar**.    

6. Haga clic en el botón **Guardar** .

    ![Botón Guardar](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. En hello **configuración de seguridad de TINFOIL** sección, haga clic en **configurar TINFOIL SECURITY** tooopen **configurar inicio de sesión** ventana. Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**

    ![Configuración de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de TINFOIL SECURITY.

9. En la barra de herramientas de hello en la parte superior de hello, haga clic en **mi cuenta**.
   
    ![Panel](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Panel")

10. Haga clic en **Seguridad**.
   
    ![Seguridad](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Seguridad")

11. En hello **Single Sign-On** configuración, siga los pasos de hello:
   
    ![Inicio de sesión único](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Inicio de sesión único")
   
    a. Seleccione **Habilitar SAML**.
   
    b. Haga clic en **Configuración manual**.
   
    c. En **dirección URL de Post SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure
   
    d. En **huella digital de certificado SAML** cuadro de texto, pegue Hola valo **huella digital** que haya copiado desde **el certificado de firma de SAML** sección.
  
    e. Copia **su Id. de cuenta** valor y pegue el valor de hello en **valor del atributo** en el cuadro de texto **Agregar atributo** sección en el portal de Azure.
   
    f. Haga clic en **Guardar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Usuarios y grupos -> Todos los usuarios ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Usuario](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Creación de un usuario de prueba de TINFOIL SECURITY

En orden tooenable toolog de los usuarios de Azure AD en TINFOIL SECURITY, se les deben aprovisionar en TINFOIL SECURITY. En caso de hello de TINFOIL SECURITY, el aprovisionamiento es una tarea manual.

**tooget un usuario aprovisionado, lleve a cabo Hola pasos:**

1. Si el usuario de hello forma parte de una cuenta de empresa, deberá demasiado[póngase en contacto con el equipo de soporte técnico de TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) cuenta de usuario de hello tooget creada.

2. Si hello es un usuario de TINFOIL SECURITY SaaS regular, usuario Hola puede agregar un tooany de colaborador de sitios del usuario de Hola. Este desencadena un toosend de proceso especificado un toohello de invitación de correo electrónico toocreate una nueva cuenta de usuario de TINFOIL SECURITY.

> [!NOTE]
> Puede usar cualquier otra TINFOIL SECURITY usuario cuenta herramienta de creación o las API proporcionadas por TINFOIL SECURITY tooprovision cuentas de usuario de Azure AD.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTINFOIL seguridad.

![Asignar usuario][200] 

**tooassign Britta Simon tooTINFOIL seguridad, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **TINFOIL SECURITY**.

    ![Selección de TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de TINFOIL SECURITY Hola Hola Panel de acceso, deberá obtener la aplicación de TINFOIL SECURITY tooyour automáticamente ha iniciado sesión. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

