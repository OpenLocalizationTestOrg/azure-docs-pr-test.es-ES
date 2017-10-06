---
title: "Tutorial: Integración de Azure Active Directory con vxMaintain | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Tutorial: Integración de Azure Active Directory con vxMaintain

En este tutorial, aprenderá cómo toointegrate vxMaintain con Azure Active Directory (Azure AD).

Esta integración proporciona varias ventajas importantes. Puede:

- Control de Azure AD que tenga acceso a toovxMaintain.
- Habilitar el inicio de sesión de los usuarios tooautomatically en toovxMaintain con inicio de sesión único (SSO) con sus cuentas de Azure AD.
- Administrar las cuentas en una ubicación central: Hola portal de Azure.

toolearn más información acerca de la integración de aplicaciones de SaaS con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

integración de Azure AD con vxMaintain tooconfigure, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción de inicio de sesión único de vxMaintain habilitada

> [!NOTE]
> Cuando se prueba pasos hello en este tutorial, se recomienda que no use un entorno de producción.

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. 

escenario de Hola que se describe en este tutorial consta de dos bloques principales:

* Agregar vxMaintain desde la Galería de Hola
* Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="add-vxmaintain-from-hello-gallery"></a>Agregar vxMaintain de galería de Hola
integración de hello tooconfigure de vxMaintain con Azure AD, deberá tooadd vxMaintain de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

tooadd vxMaintain de galería de hello, Hola siguientes:

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón. 

    ![botón de Hello Azure Active Directory][1]

2. Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.

    ![panel de "Aplicaciones empresariales" Hello][2]
    
3. una aplicación Hola tooadd **todas las aplicaciones** cuadro de diálogo, seleccione **nueva aplicación**.

    ![Hola "Nueva aplicación" botón][3]

4. En el cuadro de búsqueda de hello, escriba **vxMaintain**.

    ![lista de desplegable de "Inicio de sesión en modo simple" Hola](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. En la lista de resultados de hello, seleccione **vxMaintain**y, a continuación, seleccione **agregar**.

    ![vínculo de Hello vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con vxMaintain con un usuario de prueba llamado "Britta Simon".

Para toowork SSO, Azure AD necesita usuario de Azure AD tooknow hello vxMaintain homólogo toohello. Es decir, debe establecer una relación de vínculo entre el usuario vxMaintain correspondiente de Hola y Hola Azure AD.

relación de vínculo de tooestablish hello, asignar Hola vxMaintain **nombre de usuario** valor como hello Azure AD **nombre de usuario** valor.

tooconfigure y SSO de Azure AD mediante el uso de vxMaintain, Hola completa después de bloques de creación de la prueba.

### <a name="configure-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, puede habilitar el SSO de AD de Azure en hello portal de Azure y configurar SSO en la aplicación vxMaintain haciendo Hola siguiente:

1. En el portal de Azure, en Hola Hola **vxMaintain** página de integración de aplicaciones, seleccione **inicio de sesión único**.

    ![Hola "Inicio de sesión único" comando][4]

2. tooenable SSO, Hola **modo de inicio de sesión único** lista desplegable, seleccione **sesión basado en SAML**.
 
    ![Hola "basado en SAML Sign-on" comando](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. En **vxMaintain dominio y las direcciones URL**, Hola siguientes:

    ![Hola vxMaintain sección de dominio y las direcciones URL](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. Hola **identificador** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://<company name>.verisae.com`

    b. Hola **dirección URL de respuesta** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Hello valores anteriores no son reales. Actualizarlas con el identificador real de Hola o dirección URL de respuesta. valores de hello tooobtain, Hola contacto [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).
 
4. En **el certificado de firma de SAML**, seleccione **Metadata XML**y, a continuación, guarde el equipo de tooyour de archivo de metadatos de Hola.

    ![Hola sección "Certificado de firma de SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Seleccione **Guardar**.

    ![botón Guardar de Hola](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO, Hola envío descargado **Metadata XML** archivo toohello [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).

> [!TIP]
> Como configurar la aplicación hello, puede leer una versión concisa de hello precede a instrucciones de hello [portal de Azure](https://portal.azure.com). Después de Agregar aplicación hello de hello **Active Directory** > **aplicaciones empresariales** sección, seleccione hello **Single Sign-On** ficha y, a continuación, Hola de acceso incrusta la documentación de hello **configuración** sección. 
>
>toolearn más información acerca de la característica de documentación de embedded hello, consulte [administración de inicio de sesión único para aplicaciones empresariales](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, para crear el usuario de prueba Britta Simon Hola portal de Azure, llevando a cabo Hola siguiente:

![usuario de prueba de Hello Azure AD][100]

1. Hola **portal de Azure**, en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón.

    ![botón de "Azure Active Directory" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay una lista de usuarios, vaya demasiado**usuarios y grupos** > **todos los usuarios**.
    
    ![vínculo de Hello "Todos los usuarios"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Hola **todos los usuarios** abre el cuadro de diálogo. 

3. Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.
 
    ![botón de agregar Hola](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. Hola **usuario** diálogo cuadro, Hola siguientes:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de Hola de tipo de usuario de prueba Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, valor de hello tenga en cuenta que se generó en hello **contraseña** cuadro.

    d. Seleccione **Crear**.
 
### <a name="create-a-vxmaintain-test-user"></a>Creación de un usuario de prueba de vxMaintain

En esta sección, creará una usuaria de prueba llamada Britta Simon en vxMaintain. los usuarios de tooadd en la plataforma de vxMaintain hello, trabajar con el [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us). Antes de usar SSO, crear y activar los usuarios de Hola.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita el usuario de prueba Britta Simon toouse Azure SSO concediendo acceso toovxMaintain. por lo tanto, toodo Hola siguientes:

![Usuario de prueba en la lista de nombre para mostrar de Hola][200] 

1. En el portal de Azure hello **aplicaciones** ver, vaya demasiado**directorio** Vista > **aplicaciones empresariales** > **detodaslasaplicaciones**.

    ![vínculo de Hello "Todas las aplicaciones"][201] 

2. Hola **aplicaciones** lista, seleccione **vxMaintain**.

    ![vínculo de Hello vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. En el panel izquierdo de hello, seleccione **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. Seleccione **agregar** y, a continuación, en hello **Agregar asignación** panel, seleccione **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][203]

5. Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**y, a continuación, seleccione hello **seleccione** botón.

7. Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Prueba del inicio de sesión único de Azure AD

En esta sección, probará la configuración de SSO de Azure AD mediante el uso de hello Panel de acceso.

Seleccionar hello **vxMaintain** icono en el Panel de acceso de hello debe iniciar sesión en tooyour vxMaintain aplicación automáticamente.

Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Pasos siguientes

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

