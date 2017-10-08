---
title: "Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Enterprise de encuesta de Kenexa de IBM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise

En este tutorial, aprenderá cómo toointegrate IBM Kenexa encuesta Enterprise con Azure Active Directory (Azure AD).

Integración de IBM Kenexa encuesta Enterprise con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooIBM Kenexa encuesta Enterprise.
- Puede habilitar el inicio de sesión de los usuarios tooautomatically en tooIBM Kenexa encuesta Enterprise mediante el inicio de sesión único (SSO) con sus cuentas de Azure AD.
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure.

Si desea más información acerca del software tooknow como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con IBM Kenexa encuesta Enterprise, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en IBM Kenexa Survey Enterprise

> [!NOTE]
> Cuando se prueba pasos hello en este tutorial, se recomienda que no use un entorno de producción.

pasos de hello tootest en este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba. escenario de Hello descrito en hello tutorial consta de dos bloques principales:

* Agregar IBM Kenexa encuesta Enterprise desde la Galería de Hola
* Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Agregar IBM Kenexa encuesta Enterprise de galería de Hola
integración de hello tooconfigure de IBM Kenexa encuesta Enterprise en Azure AD, agregue IBM Kenexa encuesta Enterprise de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

tooadd IBM Kenexa encuesta Enterprise desde la Galería de Hola Hola siguientes:

1. Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, haga clic en hello **Azure Active Directory** botón. 

    ![botón de Hello Azure Active Directory][1]

2. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd una aplicación, haga clic en hello **nueva aplicación** botón.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **IBM Kenexa encuesta Enterprise**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. En la lista de resultados de hello, seleccione **IBM Kenexa encuesta Enterprise**y, a continuación, haga clic en hello **agregar** botón aplicación hello de tooadd.

    ![Lista de resultados de la empresa de encuesta de Kenexa de IBM en hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con IBM Kenexa Survey Enterprise con un usuario de prueba llamado "Britta Simon".

Para toowork SSO, Azure AD necesita a equivalente de usuario de tooidentify Hola IBM Kenexa encuesta Enterprise en Azure AD. Es decir, Azure AD debe establecer una relación de vínculo entre un usuario de Azure AD y un usuario relacionado de IBM Kenexa Survey Enterprise.

relación de vínculo de tooestablish hello, asignar Hola valo hello **nombre de usuario** de empresa de encuesta de IBM Kenexa como valor de Hola de hello **nombre de usuario** en Azure AD.

prueba SSO de Azure AD con IBM Kenexa encuesta Enterprise, completa y tooconfigure Hola bloques de creación de hello las dos secciones siguientes.

### <a name="configure-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar SSO de Azure AD en hello portal de Azure y configurar SSO en la aplicación empresarial de IBM Kenexa encuesta haciendo Hola siguiente:

1. En el portal de Azure, en Hola Hola **IBM Kenexa encuesta Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo de inicio de sesión único de IBM Kenexa Survey Enterprise][4]

2. Hola **inicio de sesión único** cuadro de diálogo hello **modo** cuadro, seleccione **sesión basado en SAML** tooenable SSO.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. Hola **IBM Kenexa encuesta Enterprise dominio y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. Hola **identificador** cuadro de texto, escriba una dirección URL con hello sigue el patrón:`https://surveys.kenexa.com/<companycode>`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello sigue el patrón:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Hello valores anteriores no son reales. Actualizarlas con el identificador real de Hola o dirección URL de respuesta. tooobtain Hola valores reales, póngase en contacto con hello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw).

4. En **el certificado de firma de SAML**, haga clic en **certificado (Base64)**y, a continuación, guarde el equipo de tooyour de archivo de certificado de Hola.

    ![vínculo de descarga del certificado (Base64) Hola](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Hola aplicación empresarial de encuesta de IBM Kenexa espera las aserciones de lenguaje de marcado de aserciones de seguridad (SAML) de hello tooreceive en un formato específico, lo que requiere tooadd atributo personalizado toohello configuración de asignaciones de los atributos de token de SAML. Hello valor de notificación de identificador de usuario de Hola en respuesta Hola debe coincidir con Id. de SSO configurado en el sistema de Kenexa Hola Hola. toomap Hola identificador de usuario correspondiente en su organización como protocolo de datagramas de Internet SSO (IDP), trabajar con hello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw). 

    De forma predeterminada, AD de Azure establece el identificador de usuario de hello como valor de nombre principal (UPN) del usuario de Hola. Puede cambiar este valor en hello **atributo** ficha, tal y como se muestra en la siguiente captura de pantalla de Hola. integración de Hello funciona sólo después de haber completado correctamente la asignación de Hola.
    
    ![cuadro de diálogo de atributos de usuario de Hola](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Haga clic en **Guardar**.

    ![Hola configurar inicio de sesión único botón Guardar](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. Hola tooopen **configurar inicio de sesión** ventana, en **configuración de la empresa de encuesta de IBM Kenexa**, haga clic en **configurar IBM Kenexa encuesta Enterprise**. 
 
    ![vínculo de Hello configurar IBM Kenexa encuesta Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Hola copia **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML single sign-on dirección URL del servicio** valores de hello **referencia rápida** sección.

8. Hola **configurar inicio de sesión** ventana, en **referencia rápida**, Hola copia **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y  **SAML single sign-on dirección URL del servicio** valores.

9. tooconfigure SSO en hello **IBM Kenexa encuesta Enterprise** cara, enviar Hola descargado **certificado (Base64)**, **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML single sign-on dirección URL del servicio** valores toohello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Se puede hacer referencia tooa versión concisa de estas instrucciones en hello [portal de Azure](https://portal.azure.com) mientras está configurando la aplicación hello. Después de Agregar aplicación hello de hello **Active Directory** > **aplicaciones empresariales** sección, simplemente haga clic en hello **inicio de sesión único** ficha y, a continuación, obtener acceso a Hola incrustado documentación a través de hello **configuración** sección Hola final. toolearn más información acerca de la característica de documentación de embedded hello, consulte [Azure AD incrustado documentación](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, para crear el usuario de prueba Britta Simon Hola portal de Azure, llevando a cabo Hola siguiente:

![Creación de un usuario de prueba de Azure AD][100]

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.
 
    ![botón de agregar Hola](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Creación de un usuario de prueba de IBM Kenexa Survey Enterprise

En esta sección, creará un usuario llamado Britta Simon en IBM Kenexa Survey Enterprise. 

los usuarios de toocreate en Hola sistema IBM Kenexa encuesta Enterprise y mapa Hola Id. de SSO para ellos, puede trabajar con hello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw). Este valor de Id. de SSO también debe estar asignado el valor de identificador de usuario toohello de Azure AD. Puede cambiar esta configuración predeterminada en hello **atributo** ficha.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita a usuario Britta Simon toouse Azure SSO concediendo acceso tooIBM Kenexa encuesta Enterprise.

![Asigne el rol de usuario de Hola][200] 

usuario tooassign Britta Simon tooIBM Kenexa encuesta Enterprise, Hola siguientes:

1. Hola portal de Azure, abra hello **aplicaciones** ver, vaya toohello **directorio** visualizarla, seleccione **aplicaciones empresariales**y, a continuación, haga clic en **todos los aplicaciones**.

    ![Hola "Aplicaciones empresariales" y los vínculos de "Todas las aplicaciones"][201] 

2. Hola **aplicaciones** lista, seleccione **IBM Kenexa encuesta Enterprise**.

    ![vínculo de IBM Kenexa encuesta Enterprise Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. En el panel izquierdo de hello, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. Haga clic en hello **agregar** botón y, a continuación, en hello **Agregar asignación** panel, seleccione **usuarios y grupos**.

    ![panel de agregar asignación de Hola][203]

5. Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**.

6. Hola **usuarios y grupos** diálogo cuadro, haga clic en hello **seleccione** botón.

7. Hola **Agregar asignación** diálogo cuadro, haga clic en hello **asignar** botón.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de SSO de Azure AD mediante el uso de hello Panel de acceso.

Al hacer clic en hello **IBM Kenexa encuesta Enterprise** Hola de mosaico en el Panel de acceso, debe iniciar sesión automáticamente en tooyour aplicación empresarial de encuesta de Kenexa de IBM.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
