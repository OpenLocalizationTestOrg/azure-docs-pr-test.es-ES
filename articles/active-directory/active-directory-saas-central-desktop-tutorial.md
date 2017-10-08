---
title: "Tutorial: Integración de Azure Active Directory con Central Desktop | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Central Desktop con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Tutorial: integración de Azure Active Directory con Central Desktop
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Central Desktop. escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una suscripción de Central Desktop con inicio de sesión único habilitado / Inquilino de Central Desktop

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

* Habilitar la integración de aplicación Hola para Central Desktop
* Configuración del inicio de sesión único (SSO)
* Configuración del aprovisionamiento de usuario
* Asignación de usuarios

![Escenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Escenario")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Habilitar la integración de aplicación Hola para Central Desktop
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Central Desktop.

**integración de aplicaciones de hello tooenable para Central Desktop, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
   ![Aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
   ![Agregar aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
   ![Agregar una aplicación de la galería](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **Central Desktop**.
   
   ![Galería de aplicaciones](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **Central Desktop**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
   ![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooCentral escritorio con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

Como parte de este procedimiento, es necesario tooupload un inquilino de Central Desktop tooyour certificado codificado en base 64.  
Si no está familiarizado con este procedimiento, consulte [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Central Desktop** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen Hola ** configurar inicio de sesión único ** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en tooCentral Desktop** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurar inicio de sesión único")
3. En hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**: 
   
   1. Hola **inicio de sesión en dirección URL Central Desktop** cuadro de texto, escriba la dirección URL Hola de su inquilino de Central Desktop (p. ej.: *http://contoso.centraldesktop.com*).
   2. En el cuadro de texto de dirección URL de respuesta de Central Desktop hello, escriba la dirección URL AssertionConsumerService de Central Desktop (p. ej.: https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Puede obtener valor de Hola desde metadatos de central desktop hello (p. ej.: *http://contoso.centraldesktop.com*).
   >  
   
   ![Configurar dirección URL de la aplicación](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurar dirección URL de la aplicación")
4. En hello **configurar inicio de sesión único en Central Desktop** page, toodownload su certificado, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello en el equipo.
   
  ![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurar inicio de sesión único")
5. Inicie sesión en tooyour **Central Desktop** inquilino.
6. Vaya demasiado**configuración**, haga clic en **avanzadas**y, a continuación, haga clic en **Single Sign On**.
   
  ![Programa de instalación: avanzado](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Programa de instalación: avanzado")
7. En hello **inicio de sesión único en la configuración** , siga los pasos de hello:
   
  ![Configuración de inicio de sesión único ](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Configuración de inicio de sesión único")
   
  1. Seleccione **Enable SAML v2 Single Sign On**(Habilitar inicio de sesión único de SAML).
  2. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Central Desktop** page, Hola copia **dirección URL del emisor** valor y, a continuación, péguelo en hello **dirección URL SSO** cuadro de texto.
  3. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Central Desktop** page, Hola copia **dirección URL de inicio de sesión remoto** valor y, a continuación, péguelo en hello **dirección URL de inicio de sesión SSO**cuadro de texto.
  4. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en Central Desktop** page, Hola copia **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **SSO Logout URL** cuadro de texto.
8. Hola **método de comprobación de firmas de mensajes** sección, lleve a cabo Hola pasos:
   
   ![Método de autenticación de firma de mensaje](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Método de autenticación de firma de mensaje")
   
  1. Seleccione **Certificado**.
  2. De hello **certificado SSO** lista, seleccione **RSH SHA256**.
  3. Crear un archivo de texto del certificado de hello descargado, Hola copia contenido del archivo de texto hello y, a continuación, péguelo en hello **certificado SSO** campo.  
     >[!TIP]
     >Para obtener más información, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Seleccione **mostrar una página de inicio de sesión de vínculo tooyour SAMLv2**.
9. Haga clic en **Update**(Actualizar).
10. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurar inicio de sesión único")
    
## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios

Para AAD a los usuarios toobe puede toosign en, deben ser aprovisionado toohello aplicación Central Desktop. Esta sección describe cómo las cuentas de usuario AAD de toocreate en Central Desktop.

**tooCentral de cuentas de usuario de tooprovision escritorio:**
1. Inicie sesión en tooyour inquilino de Central Desktop.
2. Vaya demasiado**personas \> miembros internos**.
3. Haga clic en **Agregar miembros internos**.
   
  ![Personas](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personas")
4. Hola **dirección de correo electrónico de nuevos miembros** cuadro de texto, escriba una cuenta AAD que desee tooprovision y, a continuación, haga clic en **siguiente**.
   
  ![Direcciones de correo electrónico de los nuevos miembros](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Direcciones de correo electrónico de los nuevos miembros")
5. Haga clic en **Agregar miembros internos**.
   
  ![Agregar miembros internos](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Agregar miembros internos")
   
   >[!NOTE]
   >los usuarios de Hello que ha agregado recibirán un correo electrónico que incluye un vínculo de confirmación que necesitan cuenta de hello tooactivate tooclick.
   > 

>[!NOTE]
>Puede usar cualquier otra Central Desktop usuario cuenta herramienta de creación o las API proporcionadas por Central Desktop tooprovision cuentas de usuario AAD
>  

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign usuarios tooCentral escritorio, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En hello **Central Desktop** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sí")

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

