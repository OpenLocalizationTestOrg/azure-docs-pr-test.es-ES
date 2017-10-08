---
title: "Tutorial: Integración de Azure Active Directory con Coupa | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Coupa con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Tutorial: Integración de Azure Active Directory con Coupa
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Coupa.  
escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una suscripción habilitada para el inicio de sesión único (SSO) en Coupa

Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooCoupa será capaz de toosingle inicio de sesión en la aplicación hello mediante hello [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

* Habilitar la integración de aplicación Hola para Coupa
* Configuración del inicio de sesión único
* Configuración del aprovisionamiento de usuario
* Asignación de usuarios

![Escenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Escenario")

## <a name="enable-hello-application-integration-for-coupa"></a>Habilitar la integración de aplicación Hola para Coupa
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Coupa.

**integración de aplicaciones de hello tooenable para Coupa, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
   ![Aplicaciones](./media/active-directory-saas-coupa-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
   ![Agregar aplicaciones](./media/active-directory-saas-coupa-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
   ![Agregar una aplicación de la galería](./media/active-directory-saas-coupa-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **Coupa**.
   
   ![Galería de aplicaciones](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **Coupa**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooCoupa con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.  

Configurar el inicio de sesión único para Coupa necesario tooretrieve un valor de huella digital de un certificado. Si no está familiarizado con este procedimiento, consulte [cómo tooretrieve valor de huella digital del certificado](http://youtu.be/YKQF266SAxI).

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour sitio de Coupa como administrador.
2. Vaya demasiado**el programa de instalación \> Control de seguridad**.
   
   ![Controles de seguridad](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de seguridad")
3. toodownload hello Coupa metadatos archivo tooyour equipo, haga clic en **descargar e importar metadatos de SP**.
   
   ![Metadatos SP de Coupa](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadatos SP de Coupa")
4. En otra ventana del explorador, inicie sesión en toohello portal de Azure clásico.
5. En hello **Coupa** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurar inicio de sesión único")
6. En hello **¿cómo desea que los usuarios toosign en tooCoupa** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurar inicio de sesión único")
7. En hello **configurar URL de aplicación** , siga los pasos de hello:
   
   ![Configurar dirección URL de la aplicación](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurar dirección URL de la aplicación")   
   1. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL utilizada por su toosign a los usuarios en la aplicación de Coupa tooyour (p. ej.: "*http://company.Coupa.com*").
   2. Abra el archivo de metadatos de Coupa descargado y, a continuación, copie hello **AssertionConsumerService índice/URL**.
   3. Hola **Coupa Reply URL** cuadro de texto, pegue hello **AssertionConsumerService índice/URL** valor.
   4. Haga clic en **Siguiente**.
8. En hello **configurar inicio de sesión único en Coupa** page, toodownload el archivo de metadatos, haga clic en **descargar metadatos**y, a continuación, guardar archivo hello localmente en el equipo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurar inicio de sesión único")
9. En el sitio de Coupa hello, vaya demasiado**el programa de instalación \> Control de seguridad**.
   
   ![Controles de seguridad](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de seguridad")
10. Hola **inicie sesión con credenciales de Coupa** sección, lleve a cabo Hola pasos:  

   ![Inicio de sesión con credenciales de Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Inicio de sesión con credenciales de Coupa") 
   1. Seleccione **Iniciar sesión con SAML**.
   2. Haga clic en **examinar** tooupload el archivo de metadatos de Azure Active descargado.
   3. Haga clic en **Guardar**.
11. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
    
   ![Configurar inicio de sesión único](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurar inicio de sesión único")
    
## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios

En orden tooenable toolog de los usuarios de Azure AD en Coupa, se les deben aprovisionar en Coupa.  

* En caso de hello de Coupa, el aprovisionamiento es una tarea manual.

**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**

1. Inicie sesión en tooyour **Coupa** como administrador.
2. En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**y, a continuación, haga clic en **usuarios**.
   
   ![Usuarios](./media/active-directory-saas-coupa-tutorial/IC791908.png "Usuarios")
3. Haga clic en **Create**(Crear).
   
   ![Creación de usuarios](./media/active-directory-saas-coupa-tutorial/IC791909.png "Creación de usuarios")
4. Hola **crear usuario** sección, lleve a cabo Hola pasos:
   
   ![Detalles del usuario](./media/active-directory-saas-coupa-tutorial/IC791910.png "Detalles del usuario")
   
   1. Hola de tipo **inicio de sesión**, **nombre**, **Last Name**, **Id. de inicio de sesión único**, **correo electrónico** atributos de un cuenta válida de Azure Active Directory que quiera tooprovision en hello relacionados con cuadros de texto.
   2. Haga clic en **Crear**.   
   >[!NOTE]
   >titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla. 
   > 

>[!NOTE]
>Puede usar cualquier otra Coupa usuario cuenta herramienta de creación o las API proporcionadas por Coupa tooprovision cuentas de usuario AAD. 
> 

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign tooCoupa de los usuarios, realizar Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En Hola ** Coupa ** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-coupa-tutorial/IC791911.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sí")

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

