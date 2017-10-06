---
title: "Azure AD Connect: introducción al uso de la configuración rápida | Microsoft Docs"
description: "Obtenga información acerca de cómo toodownload, instalar y ejecutar al Asistente para la instalación de Hola para Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Introducción a Azure AD Connect mediante la configuración rápida
Se utiliza la **Configuración rápida** de Azure AD Connect cuando se dispone de una topología de bosque único y de [sincronización de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) para la autenticación. **Configuración rápida** es la opción predeterminada de Hola y se usa para el escenario de hello normalmente implementada. Es solo, unos tooextend alejada de clics corto en la nube de toohello del directorio local.

Antes de empezar a instalar Azure AD Connect, asegúrese de que demasiado[descargar Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) y los pasos de requisitos previos de hello completa de [Azure AD Connect: Hardware y los requisitos previos](active-directory-aadconnect-prerequisites.md).

Si la configuración rápida no coincide con su topología, consulte la [documentación relacionada](#related-documentation) sobre otros escenarios.

## <a name="express-installation-of-azure-ad-connect"></a>Instalación rápida de Azure AD Connect
Puede ver estos pasos de acción en hello [vídeos](#videos) sección.

1. Inicie sesión como un servidor de toohello de administrador local que se va tooinstall Azure AD Connect en. Debe hacerlo en el servidor de hello desea que el servidor de sincronización de toobe Hola.
2. Navegue tooand haga doble clic en **AzureADConnect.msi**.
3. En la pantalla de bienvenida de bienvenida, seleccione Hola cuadro otorgar toohello términos de licencia y haga clic en **continuar**.  
4. En la pantalla de configuración de Express de bienvenida, haga clic en **usar configuración rápida**.  
   ![Página principal tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. En pantalla de bienvenida conectar tooAzure AD, escriba Hola nombre de usuario y la contraseña de administrador global para Azure AD. Haga clic en **Siguiente**.  
   ![Conectar tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) si recibe un error y tiene problemas con la conectividad, vea [solucionar problemas de conectividad](active-directory-aadconnect-troubleshoot-connectivity.md).
6. En la pantalla de bienvenida conectar tooAD DS, escriba Hola username y password para una cuenta de administrador de empresa. También puede especificar parte de dominio de hello en formato NetBios o FQDN, es decir, FABRIKAM\administrator o fabrikam.com\administrator. Haga clic en **Siguiente**.  
   ![Conectar tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Hola [ **configuración de inicio de sesión de Azure AD** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) página solo se muestran si no se completó [comprobar los dominios](../active-directory-add-domain.md) en hello [requisitos previos](active-directory-aadconnect-prerequisites.md).
   ![Dominios sin comprobar](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Si ve esta página, revise los dominios marcados como **Not Added** (Sin agregar) y **Not Verified** (Sin comprobar). Asegúrese de que los dominios que usa se han comprobado en Azure AD. Haga clic en símbolo de actualización de hello cuando haya comprobado los dominios.
8. En la pantalla de bienvenida tooconfigure listo, haga clic en **instalar**.
   * Si lo desea en página de hello tooconfigure listo, puede anular la selección hello **iniciar el proceso de sincronización de hello tan pronto como finalice la configuración** casilla de verificación. Debe desactivar esta casilla si desea toodo una configuración adicional, como [filtrado](active-directory-aadconnectsync-configure-filtering.md). Si anula la selección de esta opción, Asistente Hola configura la sincronización pero deja a programador Hola deshabilitado. No se ejecuta hasta que habilite manualmente por [al volver a ejecutar el Asistente para la instalación de hello](active-directory-aadconnectsync-installation-wizard.md).
   * Si tiene Exchange en su Active Directory local, también tiene una opción tooenable [ **implementación híbrida de Exchange**](https://technet.microsoft.com/library/jj200581.aspx). Habilite esta opción si planea toohave buzones de correo Exchange tanto en la nube de Hola y localmente en hello mismo tiempo.
     ![Listo tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Cuando se completa la instalación de hello, haga clic en **Exit**.
10. Una vez finalizada la instalación de hello, cierre la sesión e inicie sesión de nuevo antes de usar el administrador del servicio de sincronización o Editor de reglas de sincronización.

## <a name="videos"></a>Vídeos
Para ver un vídeo sobre el uso de instalación rápida de hello, vea:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene instalado de Azure AD Connect puede [comprobar la instalación de Hola y asignar licencias](active-directory-aadconnect-whats-next.md).

Obtener más información sobre estas características, que estaban habilitadas con la instalación de hello: [la actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md), [evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), y [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Más información acerca de estos temas comunes: [programador y cómo sincronizar tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

## <a name="related-documentation"></a>documentación relacionada
| Tema. |
| --- | --- |
| Información general de Azure AD Connect |
| Instalación mediante configuración personalizada |
| Actualización desde DirSync |
| Cuentas usadas para la instalación |

