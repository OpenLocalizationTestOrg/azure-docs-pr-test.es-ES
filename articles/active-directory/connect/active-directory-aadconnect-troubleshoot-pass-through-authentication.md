---
title: "Azure AD Connect: Solucionar problemas de autenticación de paso a través | Documentos de Microsoft"
description: "Este artículo se describe cómo tootroubleshoot autenticación de paso a través de Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Solucionar problemas de autenticación de paso a través de Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Solución de problemas de autenticación de paso a través de Azure Active Directory

Este artículo sirve de ayuda para encontrar información acerca de cómo solucionar los problemas comunes relativos a la autenticación de paso a través de Azure AD.

>[!IMPORTANT]
>Si se enfrentan a problemas de inicio de sesión de usuario con la autenticación de paso a través, no deshabilite la característica de Hola o desinstalar los agentes de autenticación de paso a través sin tener un toofall de cuenta de administrador Global solo en la nube en. Información acerca de la [incorporación de una cuenta de administrador global que está solo en la nube](../active-directory-users-create-azure-portal.md). Este paso es esencial y se asegura de no quedar bloqueado fuera de su inquilino.

## <a name="general-issues"></a>Problemas generales

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Comprobar el estado de la característica de Hola y agentes de autenticación

Asegúrese de que esa característica de autenticación de paso a través de hello sigue siendo **habilitado** sobre el estado del inquilino y Hola de agentes de autenticación muestra **Active**y no **inactivo**. Puede comprobar el estado por van toohello **Azure AD Connect** hoja en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com/).

![Centro de administración de Azure Active Directory: hoja de Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centro de administración de Azure Active Directory: hoja de Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Mensajes de error de inicio de sesión para el usuario

Si el usuario de hello es no se puede toosign en mediante la autenticación de paso a través, puede ver uno de los siguientes errores de cara al usuario en la pantalla de inicio de sesión de bienvenida Azure AD de hello: 

|Error|Description|Resolución
| --- | --- | ---
|AADSTS80001|No se puede tooconnect tooActive Directory|Asegúrese de que los servidores de agente son miembros del bosque de hello misma instancia de AD como usuarios de hello cuyas contraseñas necesitan toobe validado y son tooActive tooconnect capaz de directorio.  
|AADSTS8002|Tiempo de espera agotado conexión tooActive Directory|Compruebe tooensure que Active Directory está disponible y responde toorequests de agentes de Hola.
|AADSTS80004|nombre de usuario de Hello pasado a toohello agente no era válida|Asegúrese de usuario de hello está intentando toosign con hello nombre de usuario.
|AADSTS80005|La validación encontró una excepción WebException impredecible|Se trata de un error transitorio. Vuelva a intentar la solicitud de saludo. Si continúa toofail, póngase en contacto con el soporte técnico de Microsoft.
|AADSTS80007|Error al establecer comunicación con Active Directory.|Compruebe los registros del agente de Hola para obtener más información y comprobar que Active Directory está funcionando según lo previsto.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Motivos del error de inicio de sesión en el centro de administración de Azure Active Directory Hola

Iniciar solución de problemas de inicio de sesión de usuario examinando hello [informe actividad de inicio de sesión](../active-directory-reporting-activity-sign-ins.md) en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com/).

![Centro de administración de Azure Active Directory: informe de inicios de sesión](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Navegue demasiado**Azure Active Directory** -> **inicios de sesión** en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com/) y haga clic en la actividad de inicio de sesión de un usuario específico. Busque hello **código de ERROR de inicio de sesión** campo. Valor de Hola de asignación de ese motivo del error tooa campo y la resolución mediante hello en la tabla siguiente:

|Código de error de inicio de sesión|Motivo del error de inicio de sesión|Resolución
| --- | --- | ---
| 50144 | Ha expirado la contraseña de Active Directory del usuario. | Restablecer la contraseña de usuario de hello en su Active Directory local.
| 80001 | No hay ningún agente de autenticación disponible. | Instale y registre un agente de autenticación.
| 80002 | El tiempo de espera se agotó para la solicitud de validación de contraseña del agente de autenticación. | Compruebe si su Active Directory es accesible desde Hola agente de autenticación.
| 80003 | El agente de autenticación recibió una respuesta no válida. | Si el problema de hello es reproducible coherentemente a través de varios usuarios, compruebe la configuración de Active Directory.
| 80004 | Se usó un nombre principal de usuario (UPN) incorrecto en una solicitud de inicio de sesión. | Pida hello toosign de usuario con el nombre de usuario correcto de Hola.
| 80005 | Error del agente de autenticación. | Se trata de un error transitorio. Inténtelo de nuevo más tarde.
| 80007 | Autenticación agente no se puede tooconnect tooActive Directory. | Compruebe si su Active Directory es accesible desde Hola agente de autenticación.
| 80010 | Contraseña de no se puede toodecrypt de agente de autenticación. | Si el problema de hello es reproducible coherentemente, instalar y registrar a un nuevo agente de autenticación. Y desinstalar Hola actual. 
| 80011 | Clave de descifrado de no se puede tooretrieve de agente de autenticación. | Si el problema de hello es reproducible coherentemente, instalar y registrar a un nuevo agente de autenticación. Y desinstalar Hola actual.

## <a name="authentication-agent-installation-issues"></a>Problemas de instalación del agente de autenticación

### <a name="an-unexpected-error-occurred"></a>Se ha producido un error inesperado

[Recopilar registros del agente](#collecting-pass-through-authentication-agent-logs) de servidor hello y póngase en contacto con Microsoft Support con su problema.

## <a name="authentication-agent-registration-issues"></a>Problemas de registro del agente de autenticación

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Error en el registro de hello agente de autenticación debido a los puertos tooblocked

Asegúrese de ese servidor hello en qué Hola se ha instalado el agente de autenticación puede comunicarse con nuestro servicio de las direcciones URL y los puertos enumerados [aquí](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Error en el registro de hello agente de autenticación debido a errores de autorización de cuenta o tootoken

Asegúrese de que usa una cuenta de administrador global solo en la nube para todas las operaciones de instalación y registro del agente de autenticación independiente o de Azure AD Connect. Hay un problema conocido con cuentas de administrador Global habilitado MFA; desactivar temporalmente MFA (solo las operaciones de Hola de toocomplete) para solucionar este problema.

### <a name="an-unexpected-error-occurred"></a>Se ha producido un error inesperado

[Recopilar registros del agente](#collecting-pass-through-authentication-agent-logs) de servidor hello y póngase en contacto con Microsoft Support con su problema.

## <a name="authentication-agent-uninstallation-issues"></a>Problemas de desinstalación del agente de autenticación

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Mensaje de advertencia al desinstalar Azure AD Connect

Si tiene habilitada en su inquilino de la autenticación de paso a través e intenta toouninstall Azure AD Connect, muestra Hola siguiente mensaje de advertencia: "los usuarios no será capaz de toosign tooAzure AD a menos que tenga otros agentes de autenticación de paso a través instalar en otros servidores."

Asegúrese de que el programa de instalación es [alto disponible](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) antes de desinstalar tooavoid de Azure AD Connect importantes en el inicio de sesión de usuario.

## <a name="issues-with-enabling-hello-feature"></a>Problemas con la habilitación de la característica de Hola

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>No se pudo habilitar la característica de hello porque no había disponible ningún agente de autenticación

Necesita toohave tooenable de agente de autenticación activa al menos una autenticación de paso a través en su inquilino. Puede instalar un agente de autenticación instalando Azure AD Connect o un agente de autenticación independiente.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Error en la habilitación de la característica Hola debido tooblocked puertos

Asegúrese de ese servidor hello en el que se instala Azure AD Connect puede comunicarse con nuestro servicio de las direcciones URL y los puertos enumerados [aquí](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Error en la habilitación de la característica Hola debido a errores de autorización de cuenta o tootoken

Asegúrese de que usa una cuenta de administrador Global solo en la nube al habilitar la característica de Hola. Hay un problema conocido con la autenticación multifactor (MFA)-habilitado las cuentas de administrador Global; desactivar temporalmente MFA (sólo en el funcionamiento de toocomplete Hola) para solucionar este problema.

## <a name="exchange-activesync-configuration-issues"></a>Problemas de configuración de Exchange ActiveSync

Se trata de problemas comunes de hello al configurar la compatibilidad de Exchange ActiveSync para la autenticación de paso a través.

### <a name="exchange-powershell-issue"></a>Problema de Exchange PowerShell

Si ve Hola "**no se encuentra un parámetro que coincida con el nombre de parámetro 'PerTenantSwitchToESTSEnabled'\.**" Error al ejecutar hello `Set-OrganizationConfig` Exchange PowerShell command, póngase en contacto con Microsoft Support.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync no funciona

configuración de Hola aplica algún tiempo tootake: Hola período de tiempo depende del entorno. Si la situación de hello persiste durante mucho tiempo, póngase en contacto con Microsoft Support.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Recopilación de registros del agente de autenticación de autenticación de paso a través

Según el tipo de saludo de problema, es posible que tenga, necesita toolook en distintos lugares de registros del agente de autenticación de paso a través.

### <a name="authentication-agent-event-logs"></a>Registros de eventos del agente de autenticación

Para ver errores relacionados con toohello agente de autenticación, abra una aplicación de Visor de eventos en el servidor de Hola Hola y compruebe en **aplicación y servicio Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Para realizar análisis detallado, habilitar Hola "" de la sesión. No se ejecutan Hola agente de autenticación con este registro habilitado durante las operaciones normales; usar solo para solucionar problemas. contenido del registro de Hello solo está visible cuando se deshabilita registro Hola de nuevo.

### <a name="detailed-trace-logs"></a>Registros de seguimiento detallados

tootroubleshoot inicio de sesión de errores de usuarios, busque los registros de seguimiento en **%programdata%\Microsoft\Azure AD conectarse autenticación Agent\Trace\\**. Estos registros son razones un inicio de sesión de usuario específico usando la característica de autenticación de paso a través de Hola. Estos errores son también motivos del error de inicio de sesión de toohello asignado se muestra en hello anterior [tabla](#sign-in-failure-reasons-on-the-Azure-portal). La siguiente es una entrada del registro de ejemplo:

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

Puede obtener detalles descriptivos de error de hello ('1328' en el anterior ejemplo de Hola) abriendo el símbolo del sistema de Hola y Hola ejecución siguiente comando (Nota: reemplace '1328' con el número de error real de Hola que se ve en los registros):

`Net helpmsg 1328`

![Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Registros de controlador de dominio

Si está habilitado el registro de auditoría, encontrará información adicional en los registros de seguridad de Hola de los controladores de dominio. Una manera sencilla tooquery inicio de sesión en las solicitudes enviadas por los agentes de autenticación de paso a través es como sigue:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Contadores de Performance Monitor

Otra manera toomonitor agentes de autenticación es tootrack contadores del Monitor de rendimiento específicos en cada servidor donde está instalado el agente de autenticación de Hola. Hola de uso después de contadores globales (**autenticaciones # PTA**, **#PTA no se pudo autenticaciones** y **las autenticaciones correctas de #PTA**) y contadores de errores (**Errores de autenticación de # PTA**):

![Contadores de Performance Monitor de la Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>La Autenticación de paso a través ofrece alta disponibilidad mediante la utilización de varios agentes de autenticación, pero _no_ usa el equilibrio de carga. Según la configuración, _no_ todos los agentes de autenticación reciben aproximadamente el _mismo_ número de solicitudes. Es posible que un agente de autenticación específico no reciba ningún tráfico.
