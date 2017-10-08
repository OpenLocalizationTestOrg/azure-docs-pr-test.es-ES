---
title: "Tutorial: Integración de Azure Active Directory con Replicon | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Replicon con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Tutorial: Integración de Azure Active Directory con Replicon
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Replicon. escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Un inquilino de Replicon

Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooReplicon será toosingle capaz de inicio de sesión en la aplicación hello en el sitio de empresa de Replicon (servicio iniciado por el proveedor inicio de sesión), o mediante hello [Introducción toohello acceso Panel](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para Replicon
2. Configuración del inicio de sesión único (SSO)
3. Configuración del aprovisionamiento de usuario
4. Asignación de usuarios

![Escenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Escenario")

## <a name="enable-hello-application-integration-for-replicon"></a>Habilitar la integración de aplicación Hola para Replicon
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Replicon.

**integración de aplicaciones de hello tooenable para Replicon, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones](./media/active-directory-saas-replicon-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Agregar aplicaciones](./media/active-directory-saas-replicon-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Agregar una aplicación de la galería](./media/active-directory-saas-replicon-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **Replicon**.
   
    ![Galería de aplicaciones](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **Replicon**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooReplicon con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Replicon** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en tooReplicon** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurar inicio de sesión único")
3. En hello **configurar URL de aplicación** , siga los pasos de hello:
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurar dirección URL de la aplicación")
  1. Hola **Replicon inicio de sesión en la URL** cuadro de texto, escriba la dirección URL de inquilino de Replicon (p. ej.: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. Hola **dirección URL de respuesta de Replicon** cuadro de texto, escriba su Replicon **AssertionConsumerService** dirección URL (p. ej.: *https://global.replicon.com/! / saml2/empresa/sso/post*).  
      
     >[!NOTE]
     >Puede obtener dirección URL de Hola de hello metadatos de Replicon en: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Haga clic en **Siguiente**.

4. En hello **configurar inicio de sesión único en Replicon** page, toodownload sus metadatos, haga clic en **descargar metadatos**y, a continuación, guarde los metadatos de hello en el equipo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurar inicio de sesión único")
5. En otra ventana del explorador web, inicie sesión en como administrador en el sitio de Replicon de la compañía.

6. tooconfigure SAML 2.0, lleve a cabo Hola pasos:
   
    ![Habilitar la autenticación SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Habilitar la autenticación SAML")
  
  1. Hola toodisplay **EnableSAML Authentication2** cuadro de diálogo, anexar Hola después de dirección URL de tooyour, después de la clave de su empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * siguiente Hello muestra esquema Hola de dirección URL completa de hello:  
   **https://na2.replicon.com/\<SuClaveCompañía\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Haga clic en hello  **+**  tooexpand hello **v20Configuration** sección.
   3. Haga clic en hello  **+**  tooexpand hello **metaDataConfiguration** sección.
   4. Haga clic en **Elegir archivo**, tooselect su archivo XML de metadatos de proveedor de identidad y haga clic en **enviar**.

7. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurar inicio de sesión único")
   
## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios

En orden tooenable toolog de los usuarios de Azure AD en Replicon, se les deben aprovisionar en Replicon.  

En caso de hello de Replicon, el aprovisionamiento es una tarea manual.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. En una ventana del explorador web, inicie sesión en como administrador en el sitio de Replicon de la compañía.
2. Vaya demasiado**administración \> usuarios**.
   
    ![Usuarios](./media/active-directory-saas-replicon-tutorial/IC777806.png "Usuarios")
3. Haga clic en **+Agregar usuario**.
   
    ![Agregar usuario](./media/active-directory-saas-replicon-tutorial/IC777807.png "Agregar usuario")
4. Hola **perfil de usuario** sección, lleve a cabo Hola pasos:
   
    ![Perfil de usuario](./media/active-directory-saas-replicon-tutorial/IC777808.png "Perfil de usuario")
   
  1. Hola **nombre de inicio de sesión** cuadro de texto, hello Azure AD de tipo dirección de correo electrónico del usuario de hello Azure AD que desee tooprovision.
  2. En **Tipo de autenticación,** seleccione **SSO**.
  3. Hola **departamento** cuadro de texto, escriba el departamento del usuario de Hola.
  4. En **Tipo de empleado**, seleccione **Administrador**.
  5. Haga clic en **Guardar perfil de usuario**.

>[!NOTE]
>Puede usar cualquier otra Replicon usuario cuenta herramienta de creación o las API proporcionadas por Replicon tooprovision cuentas de usuario AAD.
> 
> 

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign tooReplicon de los usuarios, realizar Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.

2. En hello **Replicon** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
    ![Asignar usuarios](./media/active-directory-saas-replicon-tutorial/IC777809.png "Asignar usuarios")

3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
    ![Sí](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sí")

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

