---
title: "Tutorial: integración de Azure Active Directory con Qualtrics | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Qualtrics con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Tutorial: Integración de Azure Active Directory con Qualtrics
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Qualtrics.  

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una suscripción habilitada para el inicio de sesión único (SSO) en Qualtrics

Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooQualtrics será toosingle capaz de inicio de sesión en la aplicación hello en el sitio de empresa de Qualtrics (servicio iniciado por el proveedor inicio de sesión), o mediante hello [toohello de introducción Obtener acceso al Panel](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para Qualtrics
2. Configuración del inicio de sesión único (SSO)
3. Configuración del aprovisionamiento de usuario
4. Asignación de usuarios

![Escenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Escenario")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Habilitar la integración de aplicación Hola para Qualtrics
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Qualtrics.

**integración de aplicaciones de hello tooenable para Qualtrics, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
   ![Aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
   ![Agregar aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
   ![Agregar una aplicación de la galería](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **Qualtrics**.
   
   ![Galería de aplicaciones](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **Qualtrics**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooQualtrics con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Qualtrics** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en tooQualtrics** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurar inicio de sesión único")
3. En hello **configurar URL de aplicación** página Hola **Qualtrics inicio de sesión en la URL** cuadro de texto, escriba la dirección URL (p. ej.: "*https://ssotest2ut1.qualtrics.com*") y, a continuación, haga clic en **Siguiente**.
   
   ![Configurar dirección URL de la aplicación](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurar dirección URL de la aplicación")
4. En hello **configurar inicio de sesión único en Qualtrics** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos de hello en el equipo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurar inicio de sesión único")
5. Enviar Hola metadatos archivo toohello equipo de soporte técnico de Qualtrics.
   
   >[!NOTE]
   >configuración de SSO de Hello tiene toobe realizada por el equipo de soporte técnico de Qualtrics Hola. Recibirá una notificación en cuanto se ha completado la configuración de Hola.
   > 
   > 
6. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurar inicio de sesión único")
   
## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios

No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooQualtrics. Cuando un usuario asignado intenta toolog en Qualtrics a través de panel de acceso de hello, Qualtrics comprueba si existe el usuario de Hola.  

Si no hay cuentas de usuario disponibles, Qualtrics crea una automáticamente.

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign tooQualtrics de los usuarios, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En hello **Qualtrics** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sí")

Si desea tootest la configuración de SSO, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

