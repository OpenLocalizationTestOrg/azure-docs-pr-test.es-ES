---
title: "Tutorial: Integración de Azure Active Directory con RFPIO | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Tutorial: Integración de Azure Active Directory con RFPIO

En este tutorial, aprenderá cómo toointegrate RFPIO con Azure Active Directory (Azure AD).

Integración RFPIO con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar quién en Azure AD que tenga acceso tooRFPIO.
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooRFPIO (Single Sign-On) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con RFPIO tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD.
- Una suscripción habilitada para el inicio de sesión único en RFPIO

> [!NOTE]
> No se recomienda que utilice un pasos de hello tootest del entorno de producción en este tutorial.

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hola que se describe en este tutorial consta de dos bloques principales:

1. Agregar RFPIO desde la Galería de Hola.
2. Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-rfpio-from-hello-gallery"></a>Agregar RFPIO de galería de Hola
integración de hello tooconfigure de RFPIO en Azure AD, deberá tooadd RFPIO de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO de galería de Hola

1. Hola  **[portal de Azure](https://portal.azure.com)**, en Hola panel de navegación izquierdo, seleccione hello **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd una nueva aplicación, seleccione hello **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **RFPIO**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. En el panel de resultados de hello, seleccione **RFPIO**y, a continuación, seleccione hello **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con RFPIO con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow ¿qué relación hello es entre equivalente en RFPIO un usuario y en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en RFPIO debe toobe establecido.

En RFPIO, asigne el valor de Hola de **nombre de usuario** en Azure AD como valor de Hola de **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con RFPIO, deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable su toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**--tootest inicio de sesión único en Azure AD con Britta Simon.
3. **[Crear un usuario de prueba RFPIO](#creating-a-rfpio-test-user)**  --toohave un equivalente de Britta Simon en RFPIO que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**tooenable--Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#testing-single-sign-on)**  --tooverify si Hola configuración funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación RFPIO.

**inicio de sesión único en Azure AD tooconfigure con RFPIO, realizar Hola pasos:**

1. En el portal de Azure, en Hola Hola **RFPIO** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. En hello **RFPIO dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://www.rfpio.com`

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Active **Mostrar configuración avanzada de URL**.

    c. Hola **estado de retransmisión** cuadro de texto escriba un valor de cadena. Póngase en contacto con [equipo de soporte técnico RFPIO](https://www.rfpio.com/contact/) tooget este valor. 

4. Active **Mostrar configuración avanzada de URL**. Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:   

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://www.app.rfpio.com`

5. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. En una ventana del explorador web diferente, inicio de sesión toohello **RFPIO** sitio Web como administrador.

8. Haga clic en el desplegable de esquina izquierda inferior de Hola.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Haga clic en hello **configuración de la organización**. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Haga clic en hello **características e integración**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. Hola **configuración de SSO de SAML** haga clic en **editar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. En esta sección, realice las siguientes acciones:

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Copiar el contenido de Hola de hello **XML de metadatos descargado** y péguelo en hello **configuración de identidad** campo.

    > [!NOTE]
    >Hola toocopy contenido de descarga **Metadata XML** Use **el Bloc de notas ++** o adecuada **Editor XML**. 

    b. Haga clic en **Validar**.

    c. Después de hacer clic **validar**, voltear **SAML(Enabled)** tooon.

    d. Haga clic en **Enviar**.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="create-a-rfpio-test-user"></a>Creación de un usuario de prueba de RFPIO

toolog de los usuarios de Azure AD tooenable en tooRFPIO, se les deben aprovisionar en RFPIO.  
En caso de hello de RFPIO, el aprovisionamiento es una tarea manual.

**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour sitio RFPIO de su compañía como administrador.

2. Haga clic en el desplegable de esquina izquierda inferior de Hola.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Haga clic en hello **configuración de la organización**. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Haga clic en **TEAM MEMBERS** (MIEMBROS DE EQUIPO).

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Haga clic en **ADD MEMBERS** (AGREGAR MIEMBROS).

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. Hola **agregar nuevos miembros** sección. Realice las siguientes acciones:

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. ENTRAR **dirección de correo electrónico** en hello **escriba una dirección de correo por línea** campo.

    b. Seleccione **Role** (Role) de acuerdo con sus requisitos.

    c. Haga clic en **ADD MEMBERS** (AGREGAR MIEMBROS).
        
    > [!NOTE]
    > titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooRFPIO.

![Asignar usuario][200] 

**tooassign Britta Simon tooRFPIO, lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **RFPIO**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el uso de hello Panel de acceso.

Al hacer clic en hello RFPIO el icono Panel de acceso de hello, deberá obtener la aplicación de RFPIO tooyour automáticamente ha iniciado sesión.
Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

