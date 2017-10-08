---
title: "Tutorial: integración de Azure Active Directory con SuccessFactors | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse SuccessFactors con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Tutorial: integración de Azure Active Directory con SuccessFactors
objetivo de Hola de este tutorial es tooshow, cómo toointegrate SuccessFactors con Azure Active Directory (Azure AD).

Integración de SuccessFactors con Azure AD proporciona Hola siguientes ventajas:

* Puede controlar en Azure AD que tenga acceso tooSuccessFactors
* Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSuccessFactors (Single Sign-On) con sus cuentas de Azure AD
* Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico

Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Requisitos previos
integración de Azure AD con SuccessFactors tooconfigure, necesita Hola siguientes elementos:

* Una suscripción de Azure válida
* Un inquilino en SuccessFactors

> [!NOTE]
> Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.
> 
> 

pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:

* No debe usar el entorno de producción, a menos que sea necesario.
* Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.

escenario de Hello descrito en este tutorial consta de dos bloques principales:

1. Agregar SuccessFactors desde la Galería de Hola
2. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-successfactors-from-hello-gallery"></a>Agregar SuccessFactors desde la Galería de Hola
integración de hello tooconfigure de SuccessFactors en Azure AD, deberá tooadd SuccessFactors de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.

**tooadd SuccessFactors de galería de hello, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo hello, haga clic en **Active Directory**.
   
    ![Configuración del inicio de sesión único][1]
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Configuración del inicio de sesión único][2]
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Aplicaciones][3]
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Configuración del inicio de sesión único][4]
6. Hola **cuadro de búsqueda**, tipo **SuccessFactors**.
   
    ![Configuración del inicio de sesión único][5]
7. En el panel de resultados de hello, seleccione **SuccessFactors**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Configuración del inicio de sesión único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con SuccessFactors a partir de un usuario de prueba denominado "Britta Simon".

Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SuccessFactors tooan usuario en Azure AD. En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SuccessFactors debe toobe establecido.

Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SuccessFactors.

tooconfigure y prueba de inicio de sesión único en Azure AD con SuccessFactors, deberá hello toocomplete después de bloques de creación:

1. **[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.
2. **[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.
3. **[Crear un usuario de prueba de SuccessFactors](#creating-a-successfactors-test-user)**  -toohave un equivalente de Britta Simon en SuccessFactors que está vinculado toohello Azure AD representación de ella.
4. **[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.
5. **[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD
En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación de SuccessFactors.

**inicio de sesión único en Azure AD tooconfigure con SuccessFactors, siga Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **SuccessFactors** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
    ![Configuración del inicio de sesión único][7]
2. En hello **¿cómo desea que los usuarios toosign en tooSuccessFactors** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configuración del inicio de sesión único][8]
3. En hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**.
   
    ![Configuración del inicio de sesión único][9]
   
    a. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando uno de hello siguiendo patrones: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando uno de hello siguiendo patrones: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Haga clic en **Siguiente**. 

    > [!NOTE]
    > Tenga en cuenta que estos no son los valores reales de Hola. Tener tooupdate estos valores con hello URL de dirección URL de inicio de sesión y de respuesta real. tooget estos valores, póngase en contacto con [equipo de soporte técnico de SuccessFactors](https://www.successfactors.com/en_us/support.html).

1. En hello **configurar inicio de sesión único en SuccessFactors** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello localmente en el equipo.
   
    ![Configuración del inicio de sesión único][10]

2. En otra ventana del explorador web, inicie sesión en el **Portal de administración de SuccessFactors** como administrador.

3. Visite **seguridad de la aplicación** y nativo demasiado**inicio de sesión único en la característica**. 

4. Colocar cualquier valor en hello **restablecer Token** y haga clic en **guardar Token** tooenable SSO de SAML.
   
    ![Configuración del inicio de sesión único en la aplicación][11]

    > [!NOTE] 
    > Este valor solo se utiliza como Hola interruptor de encendido/apagado. Si se guarda ningún valor, Hola SSO de SAML es ON. Si se guarda un valor en blanco Hola SSO de SAML es OFF.

1. Captura de pantalla de toobelow nativo y realizar las siguientes acciones de Hola.
   
    ![Configuración del inicio de sesión único en la aplicación][12]
   
    a. Seleccione hello **SSO de SAML v2** botón de Radio
   
    b. Establecer Hola SAML imponer entidad Name(e.g. SAml issuer + company name).
   
    c. Hola **emisor SAML** textbox coloca el valor de Hola de **dirección URL del emisor** desde el Asistente para configuración de aplicaciones de Azure AD.
   
    d. Seleccione **Response(Customer Generated/IdP/AP)** [Respuesta (cliente generado/IdP/AP)] como **Require Mandatory Signature** (Requerir firma obligatoria).
   
    e. Seleccione **Enabled** (Habilitado) como **Enable SAML Flag** (Habilitar marca SAML).
   
    f. Seleccione **No** como **Login Request Signature(SF Generated/SP/RP)** [Firma de solicitud de inicio de sesión (SF generado/SP/RP)].
   
    g. Seleccione **Browser/Post Profile** (Perfil de explorador/envío) como **SAML Profile** (Perfil SAML).
   
    h. Seleccione **No** como **Enforce Certificate Valid Period** (Aplicar período válido de certificado).
   
    i. Copiar el contenido de Hola Hola descargado del archivo de certificado y, a continuación, péguelo en hello **el certificado de comprobación SAML** cuadro de texto.

    > [!NOTE] 
    > contenido del certificado Hola se debe comenzar etiquetas de certificado de certificado y de cierre.

1. Navegue tooSAML V2 y, a continuación, realizar Hola pasos:
   
    ![Configuración del inicio de sesión único en la aplicación][13]
   
    a. Seleccione **Yes** (Sí) como **Support SP-initiated Global Logout** (Permitir cierre de sesión global iniciado por SP).
   
    b. Hola **URL del servicio de cierre de sesión Global (destino de LogoutRequest)** textbox coloca el valor de Hola de **dirección URL de cierre de sesión remoto** desde el Asistente para configuración de aplicaciones de Azure AD.
   
    c. Seleccione **No** en **Require sp must encrypt all NameID element** (Requerir que sp cifre todos los elementos NameID).
   
    d. Seleccione **Unspecified** (Sin especificar) como **NameID Format** (Formato de NameID).
   
    e. Seleccione **Yes** (Sí) como **Enable sp initiated login (AuthnRequest)** [Permitir inicio de sesión iniciado por sp (AuthnRequest)].
   
    f. Hola **solicitud de envío como emisor de toda la empresa** textbox coloca el valor de Hola de **dirección URL de inicio de sesión remoto** desde el Asistente para configuración de aplicaciones de Azure AD.
2. Siga estos pasos si desea que los nombres de usuario de inicio de sesión de toomake Hola distingue entre mayúsculas y minúsculas,.
   
    a. Visite **configuración de la empresa**(cerca de la parte inferior de hello).
   
    b. Seleccione la casilla junto a **Enable Non-Case-Sensitive Username**(Habilitar nombre de usuario sin distinción de mayúsculas y minúsculas).
   
    Haga clic en **Save**(Guardar).
   
    ![Configurar inicio de sesión único][29]

    > [!NOTE] 
    > Si intentas tooenable esto, sistema de hello comprueba si se creará un nombre de inicio de sesión SAML duplicado. Por ejemplo, si el cliente de hello tiene nombres de usuario User1 y user1. Al no distinguir mayúsculas de minúsculas, estos nombres pasan a ser duplicados. sistema de Hello le proporcionará un mensaje de error y no habilitará la característica de Hola. Hola cliente deberá toochange uno de los nombres de usuario de Hola por lo que se ha escrito realmente diferentes. 

1. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
   
    ![Aplicaciones][14]
2. En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.
   
    ![Aplicaciones][15]

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
objetivo de Hola de esta sección es toocreate un usuario de prueba en el portal clásico de hello llamado a Britta Simon.

![Creación de un usuario de Azure AD][16]

**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**

1. Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.
   
    ![Creación de un usuario de prueba de Azure AD][17]
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.
   
    ![Creación de un usuario de prueba de Azure AD][18]
4. Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.
   
    ![Creación de un usuario de prueba de Azure AD][19]
5. En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD][20]
   
    a. En Tipo de usuario, seleccione Nuevo usuario de la organización.
   
    b. En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.
   
    c. Haga clic en **Siguiente**.
6. En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD][21]
   
    a. Hola **nombre** cuadro de texto, tipo **Bárbara**.  
   
    b. Hola **Last Name** cuadro de texto, tipo, **Simon**.
   
    c. Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.
   
    d. Hola **rol** lista, seleccione **usuario**.
   
    e. Haga clic en **Siguiente**.
7. En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.
   
    ![Creación de un usuario de prueba de Azure AD][22]
8. En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:
   
    ![Creación de un usuario de prueba de Azure AD][23]
   
    a. Anote el valor de Hola de hello **nueva contraseña**.
   
    b. Haga clic en **Complete**.  

### <a name="creating-a-successfactors-test-user"></a>Creación de un usuario de prueba de SuccessFactors
En orden tooenable toolog de los usuarios de Azure AD en SuccessFactors, se les deben aprovisionar en SuccessFactors.  
En caso de hello de SuccessFactors, el aprovisionamiento es una tarea manual.

tooget los usuarios creados en SuccessFactors, necesita hello toocontact [equipo de soporte técnico de SuccessFactors](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Asignación de usuario de prueba de hello Azure AD
objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSuccessFactors de acceso.

![Asignar usuario][24]

**tooassign Britta Simon tooSuccessFactors, lleve a cabo Hola pasos:**

1. En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Asignar usuario][25]
2. En la lista de aplicaciones de hello, seleccione **SuccessFactors**.
   
    ![Configurar inicio de sesión único][26]
3. En el menú de hello en la parte superior de hello, haga clic en **usuarios**.
   
    ![Asignar usuario][27]
4. En la lista de usuarios de hello, seleccione **Britta Simon**.
5. En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.
   
    ![Asignar usuario][28]

### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 
objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.

Al hacer clic en hello SuccessFactors disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación de SuccessFactors.

## <a name="additional-resources"></a>Recursos adicionales
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
