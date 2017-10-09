---
title: "Tutorial: Integración de Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FirmPlay - apoyo de empleado de contratación."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>Tutorial: Integración de Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting

En este tutorial, aprenderá cómo toointegrate FirmPlay - apoyo de empleado de contratación con Azure Active Directory (Azure AD).

Integrar FirmPlay - apoyo de empleado de contratación con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooFirmPlay - apoyo de empleado de contratación
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFirmPlay - apoyo de empleado de contratación (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con FirmPlay - apoyo de empleado de contratación, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión única de FirmPlay - Employee Advocacy for Recruiting


> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar FirmPlay - apoyo de empleado de contratación de galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>Agregar FirmPlay - apoyo de empleado de contratación de galería de Hola
integración de hello tooconfigure de FirmPlay - Propugnación de empleado de contratación en Azure AD, deberá tooadd FirmPlay - apoyo de empleado de contratación de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd FirmPlay - apoyo de empleado de contratación de galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **FirmPlay - apoyo de empleado de contratación**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. En el panel de resultados de hello, seleccione **FirmPlay - apoyo de empleado de contratación**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con FirmPlay - Employee Advocacy for Recruiting utilizando usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FirmPlay - apoyo de empleado de contratación es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FirmPlay - apoyo de empleado de contratación debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en FirmPlay - apoyo de empleado de contratación.

tooconfigure y prueba de inicio de sesión único en Azure AD con FirmPlay - apoyo de empleado de contratación, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un FirmPlay - Propugnación empleado para el usuario de prueba de contratación](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave un equivalente de Britta Simon en FirmPlay: Propugnación empleado para aplicaciones de contratación es decir vinculado representación toohello Azure AD de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en su FirmPlay - Propugnación empleado para la aplicación de contratación.

**tooconfigure inicio de sesión único en Azure AD con FirmPlay - apoyo de empleado de contratación, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **FirmPlay - apoyo de empleado de contratación** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. En hello **FirmPlay - Propugnación empleado para aplicaciones de contratación de dominio y las direcciones URL** sección en hello **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<your-subdomain>.firmplay.com/`

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Tenga en cuenta que esto no es un valor real Hola. Tendrá que tooupdate este valor con hello real iniciar sesión en la dirección URL. Póngase en contacto con [FirmPlay - Propugnación empleado para el equipo de soporte técnico de contratación](mailto:engineering@firmplay.com) tooget este valor. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**. Luego haga clic en el botón **Guardar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. En hello **el certificado de firma de SAML** sección, haga clic en **certificado (base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo. 

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. En hello **FirmPlay - Propugnación empleado para la configuración de aplicaciones de contratación** sección, haga clic en **FirmPlay configurar - apoyo de empleado de contratación** tooopen **configurar inicio de sesión en**cuadro de diálogo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget SSO configurado para la aplicación, póngase en contacto con [FirmPlay - Propugnación empleado para el equipo de soporte técnico de contratación](mailto:engineering@firmplay.com) y proporcionarles siguiente hello: 

    Hola • descargado **archivo de certificado**

    • hello **SAML Single Sign-On dirección URL del servicio**

    • hello **Id. de entidad de SAML**

    • hello **dirección URL de cierre de sesión**
  

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>Creación de un usuario de prueba de FirmPlay - Employee Advocacy for Recruiting

En esta sección, creará un usuario llamado a Britta Simon en FirmPlay - Employee Advocacy for Recruiting. Trabaje con [FirmPlay - Propugnación empleado para el equipo de soporte técnico de contratación](mailto:engineering@firmplay.com) a los usuarios de tooadd Hola Hola FirmPlay - Propugnación empleado para la plataforma de contratación.


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooFirmPlay de acceso - apoyo de empleado de contratación.

![Asignar usuario][200] 

**tooassign Britta Simon tooFirmPlay - apoyo de empleado de contratación, lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **FirmPlay - apoyo de empleado de contratación**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    


### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello FirmPlay - apoyo de empleado de icono de contratación Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour FirmPlay - Propugnación empleado para la aplicación de contratación.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png