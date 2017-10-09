---
title: "Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el servicio de seguridad de Web (WSS) de Symantec."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS)

En este tutorial, obtendrá información sobre cómo toointegrate su servicio de seguridad de Web de Symantec (WSS) cuenta con su cuenta de Azure Active Directory (Azure AD) para que WSS puede autenticar un usuario final que se aprovisiona en hello Azure AD mediante la autenticación de SAML y aplicar el usuario o reglas de nivel de directiva de grupo.

Integración de servicios de seguridad Web de Symantec (WSS) con Azure AD proporciona Hola siguientes ventajas:

- Administre todos los usuarios finales de Hola y grupos usados por su cuenta WSS desde el portal de Azure AD. 

- Permitir tooauthenticate de los usuarios finales de Hola a sí mismos en WSS con sus credenciales de Azure AD.

- Activar aplicación Hola a nivel de usuario y grupo de reglas de nivel de directiva definidas en su cuenta WSS.

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooconfigure integración de Azure AD con el servicio de seguridad Web de Symantec (WSS), necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una cuenta de Symantec Web Security Service (WSS)

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda con una cuenta WSS que se está usando actualmente para el propósito de producción.

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

- No use una cuenta de WSS que se esté usando actualmente en producción para esta prueba a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, va a configurar su Azure AD tooenable único inicio de sesión tooWSS con credenciales de usuario final de hello definidas en su cuenta de Azure AD.
escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar aplicación de servicio de seguridad de Web (WSS) de Symantec hello desde galería Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Agregar servicio de seguridad de Web de Symantec (WSS) desde la Galería de Hola
integración de hello tooconfigure de Symantec Web seguridad Service (WSS) en Azure AD, deberá tooadd Symantec Web seguridad Service (WSS) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd Symantec Web seguridad Service (WSS) de la Galería de hello, lleve a cabo Hola pasos:**

1. Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono. 

    ![botón de Hello Azure Active Directory][1]

2. Navegue demasiado**aplicaciones empresariales**. A continuación, vaya demasiado**todas las aplicaciones**.

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **Symantec Web seguridad Service (WSS)**, seleccione **Symantec Web seguridad Service (WSS)** desde el panel de resultados, a continuación, haga clic en **agregar** hello tooadd de botón aplicación.

    ![Servicio de seguridad Web de Symantec (WSS) en la lista de resultados de Hola](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS) con un usuario de prueba llamado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el servicio de seguridad Web de Symantec (WSS) es tooa usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el servicio de seguridad Web de Symantec (WSS) debe toobe establecido.

En el servicio de seguridad de Web de Symantec (WSS), asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.

tooconfigure y prueba de inicio de sesión único en Azure AD con el servicio de seguridad Web de Symantec (WSS), deberá hello toocomplete después de bloques de creación:

1. **[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de servicio de seguridad de Web (WSS) de Symantec](#create-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente de Britta Simon en Symantec Web seguridad Service (WSS) que es la representación toohello vinculado Azure AD del usuario.
4. **[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de servicio de seguridad de Web (WSS) de Symantec.

**tooconfigure inicio de sesión único en Azure AD con el servicio de seguridad de Web de Symantec (WSS), lleve a cabo Hola pasos:**

1. En el portal de Azure, en Hola Hola **Symantec Web seguridad Service (WSS)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

2. En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. En hello **dominio del servicio (WSS) de seguridad de Web de Symantec y las direcciones URL** sección, lleve a cabo Hola pasos:

    ![Información de dominio y direcciones URL de inicio de sesión único de Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. Hola **dirección URL de respuesta** cuadro de texto, escriba la dirección URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Póngase en contacto con hello [equipo de soporte técnico de cliente de servicio de seguridad de Web (WSS) de Symantec](https://www.symantec.com/contact-us) si Hola valores de hello **identificador** y **dirección URL de respuesta** por algún motivo no funcionan.

4. En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Haga clic en el botón **Guardar** .

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure inicio de sesión único en hello lado de servicio de seguridad de Web (WSS) de Symantec, consulte la documentación en línea del toohello WSS. Hola descargado **Metadata XML** archivo deberá toobe importado en el portal WSS Hola. Póngase en contacto con hello [equipo de soporte técnico de Symantec Web seguridad Service (WSS)](https://www.symantec.com/contact-us) si necesita ayuda con la configuración de hello en el portal WSS Hola.

> [!TIP]
> Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!  Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola. Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.

   ![Creación de un usuario de prueba de Azure AD][100]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.

    ![botón de agregar Hola](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. Hola **nombre** , escriba **BrittaSimon**.

    b. Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.

    c. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    d. Haga clic en **Crear**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Creación de un usuario de prueba de Symantec Web Security Service (WSS)

En esta sección, creará un usuario llamado Britta Simon en Symantec Web Security Service (WSS). el nombre de usuario de Hello correspondiente final puede crearse manualmente en el portal WSS de Hola o puede esperar a que los usuarios o grupos de hello aprovisionados en hello Azure AD toobe sincronizado toohello WSS portal después de unos minutos (unos 15 minutos). Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único. dirección IP pública de Hello del equipo del usuario final de hello, que será sitios Web toobrowse usado también necesita toobe aprovisionado en el portal de servicio de seguridad de Web (WSS) de Symantec Hola.

> [!NOTE]
> Por favor, [haga clic aquí](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget su equipo público de dirección IP.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSymantec Web seguridad Service (WSS).

![Asigne el rol de usuario de Hola][200] 

**tooassign Britta Simon tooSymantec Web seguridad Service (WSS), lleve a cabo Hola pasos:**

1. Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **Symantec Web seguridad Service (WSS)**.

    ![vínculo de servicio de seguridad de Web (WSS) de Symantec Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.

    ![vínculo de "Usuarios y grupos" Hello][202]

4. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![panel de agregar asignación de Hola][203]

5. En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.

6. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

7. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará funcionalidad de inicio de sesión único de hello ahora que ha configurado su toouse de cuenta WSS Azure AD para la autenticación de SAML.

Después de haber configurado el tráfico de tooproxy de explorador web tooWSS, cuando abra el explorador web e intente toobrowse tooa sitio, a continuación, se va a ser redirigido toohello el inicio de sesión Azure página. Especifique credenciales Hola Hola prueba final del usuario de que se ha aprovisionado en hello Azure AD (es decir, BrittaSimon) y los asociados de contraseña. Una vez autenticado, podrá toobrowse capaz de sitio Web de toohello que eligió. Debe crear una regla de directiva en hello WSS lado tooblock BrittaSimon del examen tooa sitio en particular, a continuación, debería ver Hola WSS bloquear página cuando intente toobrowse toothat sitio como usuario BrittaSimon.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

