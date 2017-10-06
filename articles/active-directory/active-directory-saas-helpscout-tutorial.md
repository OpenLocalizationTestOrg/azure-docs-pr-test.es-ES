---
title: "Tutorial: Integración de Azure Active Directory con Help Scout | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ayudar a Scout."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Tutorial: integración de Azure Active Directory con Help Scout

En este tutorial, aprenderá cómo toointegrate ayuda Asesor de destinos con Azure Active Directory (Azure AD).

Obtener Hola siguientes ventajas de integrar ayuda Scout con Azure AD:

- En Azure AD, puede controlar quién tiene acceso tooHelp Scout.
- Puede firmar automáticamente en su tooHelp usuarios Scout mediante el inicio de sesión único y una cuenta de usuario Azure AD.
- Puede administrar las cuentas en una ubicación central, Hola portal de Azure.

toolearn más información acerca del software como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos

tooset la integración de Azure AD con Scout ayuda, necesita Hola siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción de Help Scout, con inicio de sesión único activado 

> [!NOTE]
> Si prueba a pasos de hello en este tutorial, se recomienda que no probarlas en un entorno de producción.

Recomendaciones para probar los pasos de hello en este tutorial:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba gratuita durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. 

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar a ayuda Scout de hello Galería.
2. Configuración y prueba del inicio de sesión único en Azure AD.

## <a name="add-help-scout-from-hello-gallery"></a>Agregar a ayuda Scout de galería de Hola
tooset la integración de Hola de ayuda Scout con Azure AD, en la Galería de hello, agregue la lista de tooyour de ayuda Scout de aplicaciones administradas de SaaS.

tooadd ayuda Scout de galería de hello:

1. Hola [portal de Azure](https://portal.azure.com), en el menú de la izquierda de Hola, seleccione **Azure Active Directory**. 

    ![botón de Hello Azure Active Directory][1]

2. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![página de aplicaciones de empresa de Hola][2]
    
3. tooadd una nueva aplicación, seleccione **nueva aplicación**.

    ![botón de nueva aplicación Hola][3]

4. En el cuadro de búsqueda de hello, escriba **ayuda Scout**. En los resultados de la búsqueda de hello, seleccione **ayuda Scout**y, a continuación, seleccione **agregar**.

    ![Ayuda Scout en la lista de resultados de Hola](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, configurará y probará el inicio de sesión único de Azure AD con Help Scout mediante un usuario de prueba llamado *Britta Simon*.

Para toowork de inicio de sesión único, Azure AD necesita usuario de equivalente de Azure AD tooknow hello en Scout ayuda. Se debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Scout ayuda.

Hola tooestablish vincular relación en Scout ayuda, para **nombre de usuario**, asignar un valor de Hola de hello **nombre de usuario** en Azure AD.

tooconfigure y prueba de inicio de sesión único en Azure AD con Scout ayuda, Hola completa después de tareas:

1. [Configuración del inicio de sesión único de Azure AD](#set-up-azure-ad-single-sign-on). Configura un toouse de usuario de esta característica.
2. [Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user). Pruebas AD Azure inicio de sesión único con usuario hello Britta Simon.
3. [Creación de un usuario de prueba de Help Scout](#create-a-help-scout-test-user). Crea a un equivalente de Britta Simon en Scout ayuda que está vinculado toohello representación de Azure AD del usuario de Hola.
4. [Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user). Configura Britta Simon toouse inicio de sesión único en Azure AD.
5. [Prueba de inicio de sesión único](#test-single-sign-on). Comprueba que la configuración de hello funciona.

### <a name="set-up-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, configurar inicio de sesión único en Azure AD en hello portal de Azure. A continuación, configura el inicio de sesión único en la aplicación Help Scout.

tooset de inicio de sesión único en Azure AD con Scout ayuda:

1. En el portal de Azure, en Hola Hola **ayuda Scout** página de integración de aplicaciones, seleccione **inicio de sesión único**.
 
    ![Configuración de vínculo de inicio de sesión único][4]

2. En hello **inicio de sesión único** página, para **modo**, seleccione **sesión basado en SAML**.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. En **ayuda Scout dominio y las direcciones URL**si desea tooset una aplicación hello en el modo iniciado por IDP, Hola completa pasos:

    1. Hola **identificador** cuadro, escriba una dirección URL con hello siguiente patrón:`urn:auth0:helpscout:<instancename>`

    2. Hola **dirección URL de respuesta** cuadro, escriba una dirección URL con hello siguiente patrón:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Información de dominio y direcciones URL de inicio de sesión único de Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Si desea tooset una aplicación hello en modo iniciado en SP, seleccione hello **mostrar avanzadas de configuración de direcciones URL** casilla de verificación y, a continuación, Hola siguientes:

    * Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL con hello siguiendo el formato:`https://secure.helpscout.net/members/login/`

    ![Información de dominio y direcciones URL de inicio de sesión único de Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > los valores de Hello en estas direcciones URL son únicamente como demostración. Actualizar valores de hello con la dirección URL de identificación real de Hola y la dirección URL de respuesta. tooget estos valores, póngase en contacto con [equipo de soporte técnico de ayuda Scout](mailto:help@helpscout.com). 

5. En **el certificado de firma de SAML**, seleccione **Metadata XML**y, a continuación, guarde el archivo de metadatos de hello en el equipo.

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Seleccione **Guardar**.

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset una sola sesión en el lado de ayuda Scout hello, enviar Hola descargar metadatos XML archivo toohello [equipo de soporte técnico de ayuda Scout](mailto:help@helpscout.com). equipo de soporte técnico de Hello ayuda Scout aplica esta configuración Hola SAML único inicio de sesión de conexión se establece correctamente en ambos lados.

> [!TIP]
> Puede leer una versión concisa de estas instrucciones en hello [portal de Azure](https://portal.azure.com), mientras que va a configurar la aplicación. Después de agregar la aplicación hello seleccionando **Active Directory** > **aplicaciones empresariales**, seleccione hello **Single Sign-On** ficha. Puede tener acceso a la documentación de hello incrustado en hello **configuración** sección final Hola de página Hola. Para más información, consulte la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

En esta sección, en hello portal de Azure, cree un usuario de prueba denominado a Britta Simon.

![Creación de un usuario de prueba de Azure AD][100]

toocreate un usuario de prueba en Azure AD:

1. En el portal de Azure, en el menú de la izquierda, Hola Hola seleccione **Azure Active Directory**.

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. lista de hello toodisplay de usuarios, seleccionados **usuarios y grupos**y, a continuación, seleccione **todos los usuarios**.

    ![Seleccionar Usuarios y grupos y, luego, Todos los usuarios](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. Hola tooopen **usuario** cuadro de diálogo, en parte superior de Hola de hello **todos los usuarios** página, seleccione **agregar**.

    ![botón de agregar Hola](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. Hola **usuario** cuadro de diálogo, Hola completa pasos:

    1. Hola **nombre** cuadro, escriba **BrittaSimon**.

    2. Hola **nombre de usuario** cuadro, escriba la dirección de correo electrónico de saludo del usuario Britta Simon.

    3. Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.

    4. Seleccione **Crear**.

        ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Creación de un usuario de prueba de Help Scout

objeto de Hola de esta sección es toocreate un usuario denominado a Britta Simon en Scout ayuda. Help Scout admite el aprovisionamiento Just-In-Time (JIT), que está activado de forma predeterminada.

En esta sección, no hay ningún toocomplete acción o tarea. Si un usuario ya no existe en Scout ayuda, se crea uno nuevo si intentas tooaccess Scout ayuda.

### <a name="assign-hello-azure-ad-test-user"></a>Asignar el usuario de prueba de hello Azure AD

En esta sección, que permita que a Hola usuario Britta Simon toouse Azure AD inicio de sesión único mediante la concesión de tooHelp de acceso de cuenta de usuario de hello Scout.

![Asigne el rol de usuario de Hola][200] 

tooassign Britta Simon tooHelp Scout:

1. Hola portal de Azure, abrir vista de aplicaciones de hello y, haga clic en la vista de directorio toohello. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![Asignar usuario][201] 

2. En la lista de aplicaciones de hello, seleccione **ayuda Scout**.

    ![vínculo de ayuda Scout Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. En el menú de la izquierda hello, seleccione **usuarios y grupos**.

    ![Hola a los usuarios y grupos de vínculo][202]

4. Seleccione **Agregar**. A continuación, en hello **Agregar asignación** página, seleccione **usuarios y grupos**.

    ![panel de agregar asignación de Hola][203]

5. En hello **usuarios y grupos** página, en la lista de Hola de usuarios, seleccionados **Britta Simon**.

6. En hello **usuarios y grupos** página, seleccione **seleccione**.

7. En hello **Agregar asignación** página, seleccione **asignar**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el panel de acceso de Hola.

Cuando se selecciona icono de ayuda Scout hello en el panel de acceso hello, se debe sesión automáticamente en tooyour aplicación Scout ayuda.

Para obtener más información sobre el panel de acceso, consulte [panel de acceso de introducción toohello](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

