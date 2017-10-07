---
title: "Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el servicio de seguridad de Web (WSS) de Symantec."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS)

En este tutorial, aprenderá cómo toointegrate Symantec Web seguridad Service (WSS) con Azure Active Directory (Azure AD).

Integración de servicios de seguridad Web de Symantec (WSS) con Azure AD proporciona Hola siguientes ventajas:

- Puede controlar en Azure AD que tenga acceso tooSymantec Web seguridad Service (WSS)
- Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSymantec Web seguridad Service (WSS) (Single Sign-On) con sus cuentas de Azure AD
- Puede administrar las cuentas en una ubicación central: Hola portal de Azure

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con el servicio de seguridad Web de Symantec (WSS), necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción de Symantec Web Security Service (WSS) con inicio de sesión único habilitado

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar servicio de seguridad de Web de Symantec (WSS) desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Agregar servicio de seguridad de Web de Symantec (WSS) desde la Galería de Hola
integración de hello tooconfigure de Symantec Web seguridad Service (WSS) en Azure AD, deberá tooadd Symantec Web seguridad Service (WSS) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Symantec Web seguridad Service (WSS) de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![Aplicaciones][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![Aplicaciones][3]

4. En el cuadro de búsqueda de hello, escriba **Symantec Web seguridad Service (WSS)**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. En el panel de resultados de hello, seleccione **Symantec Web seguridad Service (WSS)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS) con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el servicio de seguridad Web de Symantec (WSS) es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el servicio de seguridad Web de Symantec (WSS) debe toobe establecido.

En el servicio de seguridad de Web de Symantec (WSS), asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con el servicio de seguridad Web de Symantec (WSS), deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de servicio de seguridad de Web (WSS) de Symantec](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente de Britta Simon en Symantec Web seguridad Service (WSS) que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de servicio de seguridad de Web (WSS) de Symantec.

**tooconfigure inicio de sesión único en Azure AD con el servicio de seguridad de Web de Symantec (WSS), lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Symantec Web seguridad Service (WSS)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. En hello **dominio del servicio (WSS) de seguridad de Web de Symantec y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. Hola **dirección URL de inicio de sesión** cuadro de texto dirección url de hello mención, que desee tooblock según la directiva de bloqueo de toohello de hello Symantec Web seguridad Service (WSS).  
    
    b. Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`

    > [!NOTE] 
    > Estos valores no son reales. Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador. Póngase en contacto con [equipo de soporte técnico de cliente de servicio de seguridad de Web (WSS) de Symantec](https://www.symantec.com/contact-us) tooget estos valores. 

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. tooconfigure inicio de sesión único en **Symantec Web seguridad Service (WSS)** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipodesoportetécnicodeSymantecWebseguridadService(WSS)](https://www.symantec.com/contact-us).

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

![Creación de un usuario de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. En hello **usuario** cuadro de diálogo, siga los pasos de hello:
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    a. Hola **nombre** cuadro de texto, tipo **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.

    c. Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.

    d. Haga clic en **Crear**.
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a>Crear un usuario de prueba de Symantec Web Security Service (WSS)

En esta sección, creará un usuario llamado Britta Simon en Symantec Web Security Service (WSS). Trabajar con [equipo de soporte técnico de Symantec Web seguridad Service (WSS)](https://www.symantec.com/contact-us) para agregar usuarios de hello en plataforma de hello Symantec Web seguridad Service (WSS). Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único. También junto con hello usuario informa necesita toosend Hola dirección IP pública de máquina de Hola desde el que está tratando de aplicación de hello tooaccess.

> [!NOTE]
> Por favor, [haga clic aquí](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget su equipo público de dirección IP.

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSymantec Web seguridad Service (WSS).

![Asignar usuario][200] 

**tooassign Britta Simon tooSymantec Web seguridad Service (WSS), lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Symantec Web seguridad Service (WSS)**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![Asignar usuario][202] 

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.

Al hacer clic en hello Symantec Web seguridad Service (WSS) el icono Hola Panel de acceso, obtendrá redirigida toohello bloqueo de página para el que se ha configurado la directiva de bloqueo de Hola.
Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

