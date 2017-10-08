---
title: "Tutorial: Integración de Azure Active Directory con SCC LifeCycle | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse SCC LifeCycle con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Tutorial: Integración de Azure Active Directory con SCC LifeCycle
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y SCC LifeCycle.  

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una suscripción habilitada para el inicio de sesión único (SSO) en SCC LifeCycle

Después de completar este tutorial, Hola usuarios de Azure AD que haya asignado será el ciclo de vida de tooSCC toosingle capaz de inicio de sesión en la aplicación hello en el sitio de SCC LifeCycle (servicio iniciado por el proveedor inicio de sesión), o mediante hello [Introducción Panel de acceso de toohello](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para SCC LifeCycle
2. Configuración del inicio de sesión único (SSO)
3. Configuración del aprovisionamiento de usuario
4. Asignación de usuarios

![Escenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Escenario")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Habilitar la integración de aplicación Hola para SCC LifeCycle
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para SCC LifeCycle.

**integración de aplicaciones de hello tooenable para SCC LifeCycle, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Agregar aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Agregar una aplicación de la galería](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **SCC LifeCycle**.
   
    ![Galería de aplicaciones](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **SCC LifeCycle**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![Ciclo de vida de SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "Ciclo de vida de SCC")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooauthenticate tooSCC del ciclo de vida de tooenable a los usuarios con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **SCC LifeCycle** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen Hola ** configurar inicio de sesión único ** cuadro de diálogo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en tooSCC ciclo de vida de** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurar inicio de sesión único")
3. En hello **configurar URL de aplicación** página Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL Hola utilizado por su toosign a los usuarios en tooyour aplicación de SCC LifeCycle mediante Hola sigue el patrón "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*"y, a continuación, haga clic en **siguiente**.
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurar dirección URL de la aplicación")
4. En hello **configurar inicio de sesión único en SCC LifeCycle** página, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos localmente en el equipo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurar inicio de sesión único")
5. Reenviar ese tooSCC del archivo de metadatos equipo de soporte técnico de ciclo de vida.
   
   >[!NOTE]
   >Inicio de sesión único tiene toobe habilitada por Hola, equipo de soporte técnico de SCC LifeCycle.
   > 
   > 

6. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurar inicio de sesión único")
   
## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios

En orden tooenable toolog de los usuarios de Azure AD en SCC LifeCycle, se les deben aprovisionar en SCC LifeCycle. No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooSCC del ciclo de vida.

Cuando un toolog de intentos de usuario asignado en SCC LifeCycle, automáticamente se crea una cuenta de SCC LifeCycle si es necesario.

>[!NOTE]
>Puede usar cualquier otra SCC LifeCycle usuario cuenta herramienta de creación o las API proporcionadas por tooprovision de SCC LifeCycle cuentas de usuario AAD.
> 
> 

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign usuarios tooSCC ciclo de vida, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En Hola ** SCC LifeCycle ** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
    ![Asignar usuarios](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
    ![Sí](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sí")

Si desea tootest la configuración de SSO, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

