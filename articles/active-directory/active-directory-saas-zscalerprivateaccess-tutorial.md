---
title: "Tutorial: Integración de Azure Active Directory con Zscaler Private Access (ZPA) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y acceso privado de Zscaler (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a>Tutorial: Integración de Azure Active Directory con Zscaler Private Access (ZPA)

En este tutorial, aprenderá cómo toointegrate acceso privado de Zscaler (ZPA) con Azure Active Directory (Azure AD).

Integración de acceso privada de Zscaler (ZPA) con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooZscaler acceso privado (ZPA)
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooZscaler acceso privado (ZPA) (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con Zscaler privada acceso (ZPA), necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único de Zscaler Private Access (ZPA)


> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.


pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar acceso privado de Zscaler (ZPA) desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a>Agregar acceso privado de Zscaler (ZPA) desde la Galería de Hola
integración de hello tooconfigure de acceso privada de Zscaler (ZPA) en Azure AD, deberá tooadd acceso privado de Zscaler (ZPA) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd acceso privado de Zscaler (ZPA) desde la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **acceso privado de Zscaler (ZPA)**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. En el panel de resultados de hello, seleccione **acceso privado de Zscaler (ZPA)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler Private Access (ZPA) con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el acceso privado de Zscaler (ZPA) es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el acceso privado de Zscaler (ZPA) debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de acceso privada de Zscaler (ZPA).

tooconfigure y prueba de inicio de sesión único en Azure AD con Zscaler privada acceso (ZPA), deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de Zscaler privada acceso (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave un equivalente de Britta Simon en Zscaler privada acceso (ZPA) que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de Zscaler privada acceso (ZPA).

**tooconfigure inicio de sesión único en Azure AD con acceso privado de Zscaler (ZPA), lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, en hello **acceso privado de Zscaler (ZPA)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. En hello **dominio Zscaler privada acceso (ZPA) y las direcciones URL** sección, lleve a cabo Hola pasos:
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`

    b. Hola **identificador** cuadro de texto, tipo:`https://samlsp.private.zscaler.com/auth/metadata`

    > [!NOTE] 
    > Tenga en cuenta que estos no son los valores reales de Hola. Tendrá que tooupdate estos valores con hello real iniciar sesión en la dirección URL y el identificador. Aquí le sugerimos toouse Hola valor único de dirección URL en hello identificador. Póngase en contacto con [equipo de soporte técnico de Zscaler privada acceso (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget estos valores.

4. En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. En hello **crear nuevo certificado** cuadro de diálogo, haga clic en el icono del calendario de Hola y seleccione un **fecha de expiración**. Luego haga clic en el botón **Guardar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. En hello **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado** y haga clic en **guardar** botón.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. En la ventana emergente de hello **el certificado de sustitución** ventana, haga clic en **Aceptar**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Zscaler Private Access (ZPA) como administrador.

10. Navegue demasiado**administrador** y, a continuación, haga clic en **configuración de Idp**.

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. Hola **configuración de Idp** sección, haga clic en **agregar nueva configuración de IDP**.

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. Hola **nueva configuración de IDP** sección, lleve a cabo Hola pasos:

    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    a. Haga clic en **Select File** (Seleccionar archivo) y cargue su archivo de metadatos descargado.

    b. Haga clic en el botón **Guardar** .
    


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**. 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a>Creación de un usuario de prueba de Zscaler Private Access (ZPA)

En esta sección, creará un usuario llamado Britta Simon en Zscaler Private Access (ZPA). Trabaje con [equipo de soporte técnico de Zscaler privada acceso (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooadd los usuarios de hello en la plataforma de hello Zscaler privada acceso (ZPA).


### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooZscaler acceso acceso privado (ZPA).

![Asignar usuario][200] 

**tooassign Britta Simon tooZscaler acceso privado (ZPA), lleve a cabo Hola pasos:**

1. En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **acceso privado de Zscaler (ZPA)**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    


### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en icono de Zscaler privada acceso (ZPA) Hola Hola Panel de acceso, deberá obtener la aplicación de Zscaler privada acceso (ZPA) tooyour automáticamente ha iniciado sesión.


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png