---
title: "Azure AD Connect: solución de problemas de conectividad | Microsoft Docs"
description: "Explica cómo problemas de conectividad de tootroubleshoot con Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Solución de problemas de conectividad con Azure AD Connect
Este artículo explica cómo funciona la conectividad entre Azure AD Connect y Azure AD y cómo emite tootroubleshoot conectividad. Estos problemas son probablemente toobe visto en un entorno con un servidor proxy.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Solucionar problemas de conectividad en el Asistente para la instalación de Hola
Azure AD Connect usa autenticación moderna (mediante la biblioteca ADAL Hola) para la autenticación. Asistente para la instalación de Hola y el motor de sincronización de hello apropiado requieren toobe machine.config configurado correctamente debido a que estos dos son las aplicaciones .NET.

En este artículo, le mostramos cómo Fabrikam se conecta tooAzure AD a través de su servidor proxy. servidor proxy de Hola se denomina fabrikamproxy y está usando el puerto 8080.

Primero necesitamos toomake seguro [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) está configurado correctamente.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> En algunos blogs de Microsoft no está documentado que se deben realizar cambios toomiiserver.exe.config en su lugar. Sin embargo, este archivo se sobrescribe en cada actualización por lo que incluso si funciona durante la instalación inicial, el sistema de Hola deja de funcionar al actualizar primero. Por esta razón, recomendación de hello es tooupdate machine.config en su lugar.
>
>

servidor proxy de Hello también debe tener abiertas de las direcciones URL de hello necesario. lista oficial de Hola se documenta en [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

De estas direcciones URL, hello en la tabla siguiente es Hola absoluta toobe mínimo tooconnect puede tooAzure AD en absoluto. Esta lista no incluye características opcionales, como la escritura diferida de contraseñas ni Azure AD Connect Health. Es toohelp aquí documentado en la solución de problemas de configuración inicial de Hola.

| URL | Port | Description |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Enumera toodownload usado CRL. |
| \*.verisign.com |HTTP/80 |Enumera toodownload usado CRL. |
| \*.entrust.com |HTTP/80 |Toodownload usado CRL se enumera para MFA. |
| \*.windows.net |HTTPS/443 |Toosign utilizado en tooAzure AD. |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |Se utiliza para MFA. |
| \*.microsoftonline.com |HTTPS/443 |Usar tooconfigure los datos de directorio y de importación y exportación de Azure AD. |

## <a name="errors-in-hello-wizard"></a>Errores en el Asistente de Hola
Asistente para la instalación de Hello usa dos contextos de seguridad diferentes. En la página de hello **conectar tooAzure AD**, que está usando Hola usuario inició sesión. En la página de hello **configurar**, está cambiando toohello [cuenta de servicio de hello para el motor de sincronización de hello](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Si hay un problema, aparecerá más probable es que ya se encuentra hello **conectar tooAzure AD** página Hola Asistente puesto que la configuración de proxy de hello es global.

Hola problemas siguientes es los errores más comunes de Hola que se producen en el Asistente para la instalación de Hola.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>Asistente para la instalación de Hello no se ha configurado correctamente
Este error aparece cuando el propio asistente hello no puede llegar al proxy de Hola.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Si ve este error, compruebe hello [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) se ha configurado correctamente.
* Si se ve correcta, siga los pasos de hello en [Compruebe la conectividad de proxy](#verify-proxy-connectivity) toosee si Hola problema está presente fuera así el Asistente de Hola.

### <a name="a-microsoft-account-is-used"></a>Se usa una cuenta Microsoft
Si utiliza una **cuenta Microsoft** en lugar de una cuenta **educativa o profesional**, aparece un error genérico.  
![Se usa una cuenta Microsoft](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>no se puede alcanzar el punto de conexión de Hello MFA
Este error aparece si hello extremo **https://secure.aadcdn.microsoftonline-p.com** no se puede alcanzar y el administrador global tiene MFA habilitado.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Si ve este error, compruebe ese punto de conexión de hello **secure.aadcdn.microsoftonline p.com** se ha agregado toohello proxy.

### <a name="hello-password-cannot-be-verified"></a>no se puede comprobar la contraseña de Hola
No se puede comprobar si se realiza correctamente en conexión tooAzure AD, pero la propia contraseña Hola Asistente para la instalación de hello que verá este error:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* ¿Es una contraseña temporal de contraseña de Hola y debe cambiarse? ¿Es lo que realmente Hola contraseña correcta? Intente toosign en toohttps://login.microsoftonline.com (en otro equipo que el servidor de Azure AD Connect Hola) y compruebe la cuenta de hello es utilizable.

### <a name="verify-proxy-connectivity"></a>Comprobación de la conectividad de proxy
tooverify si el servidor de Azure AD Connect hello tiene conectividad real con hello Proxy e Internet, utilice algunos toosee PowerShell si las solicitudes web está permitiendo el proxy de Hola o no. En un símbolo del sistema de PowerShell, ejecute `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc` (Técnicamente hello primera llamada es toohttps://login.microsoftonline.com y este URI también funciona, pero otro URI hello es más rápido toorespond).

PowerShell utiliza la configuración de hello en el proxy de hello toocontact de machine.config. configuración de Hello en winhttp/netsh no debería afectar estos cmdlets.

Si el proxy de hello está configurado correctamente, debería obtener un estado correcto: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Si recibes **servidor remoto de no se puede tooconnect toohello**, PowerShell está tratando de toomake una llamada directa sin usar el proxy de Hola o DNS no está configurado correctamente. Asegúrese de hello seguro **machine.config** archivo está configurado correctamente.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Si el proxy de hello no está configurado correctamente, recibirá un error: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Error | Texto del error | Comentario |
| --- | --- | --- |
| 403 |Prohibido |no se ha abierto el proxy de Hola para hello la dirección URL solicitada. Revisar configuración de proxy de Hola y asegúrese de hello seguro [direcciones URL](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) se han abierto. |
| 407 |Se requiere autenticación del proxy |servidor proxy de Hello necesarios en un inicio de sesión y se proporciona ninguno. Si el servidor proxy requiere autenticación, asegúrese de toohave seguro esta opción configurada en el archivo machine.config de Hola. Además, asegúrese de que se utilizan cuentas de dominio para ejecutar el Asistente de Hola de usuario de Hola y para la cuenta de servicio de Hola. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>patrón de comunicación de Hello entre Azure AD Connect y Azure AD
Si ha seguido todos los pasos anteriores y aún no se puede conectar, en este momento puede comenzar a examinar los registros de red. En esta sección se documenta un patrón de conectividad normal y correcta. También lo es enumerar falsas rojo comunes que puede hacer caso omiso al leer registros de red de Hola.

* No hay llamadas toohttps://dc.services.visualstudio.com. No es necesario toohave que puede hacer caso omiso de esta dirección URL abierta en el proxy de Hola para toosucceed de instalación de Hola y estas llamadas.
* Verá que la resolución de dns muestra hello hosts real toobe en nsatc.net de espacio de nombre DNS de Hola y de otros espacios de nombres no se admite con microsoftonline.com. Sin embargo, no hay las solicitudes de servicio web en los nombres de servidor real de hello y no tiene tooadd estos proxy toohello de direcciones URL.
* provisioningapi y adminwebservice de puntos de conexión de hello son puntos de conexión de detección y utilizar toofind Hola extremo real toouse. Estos puntos de conexión difieren en función de la región.

### <a name="reference-proxy-logs"></a>Registros de proxy de referencia
Este es un volcado de memoria de un proxy real hello y registro de instalación página del asistente desde el que se tomó (mismo punto de conexión se han quitado de toohello entradas duplicadas). Esta sección se puede usar como referencia para su propio proxy y los registros de red. los puntos de conexión Hola real puede variar en su entorno (en concreto las direcciones URL en *cursiva*).

**Conectar tooAzure AD**

| Hora | URL |
| --- | --- |
| 11/1/2016 8:31 |connect://login.microsoftonline.com:443 |
| 11/1/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 11/1/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/1/2016 8:32 |connect://login.microsoftonline.com:443 |
| 11/1/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 11/1/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Configuración**

| Hora | URL |
| --- | --- |
| 11/1/2016 8:43 |connect://login.microsoftonline.com:443 |
| 11/1/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/1/2016 8:43 |connect://login.microsoftonline.com:443 |
| 11/1/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 11/1/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 11/1/2016 8:44 |connect://login.microsoftonline.com:443 |
| 11/1/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 11/1/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/1/2016 8:44 |connect://login.microsoftonline.com:443 |
| 11/1/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 11/1/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Sincronización inicial**

| Hora | URL |
| --- | --- |
| 11/1/2016 8:48 |connect://login.windows.net:443 |
| 11/1/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 11/1/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 11/1/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>Errores de autenticación
Esta sección tratan los errores que pueden devolverse desde AAL (biblioteca de autenticación hello usa Azure AD Connect) y PowerShell. error de Hello explicada en ayudar a comprender los pasos siguientes.

### <a name="invalid-grant"></a>Concesión no válida
Nombre de usuario o contraseña no válidos. Para obtener más información, consulte [no se puede comprobar la contraseña de hello](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Tipo de usuario desconocido
El directorio de Azure AD no se encuentra o no se ha resuelto. ¿Quizá intente toologin con un nombre de usuario en un dominio no comprobado?

### <a name="user-realm-discovery-failed"></a>Error de detección de dominio de usuario
Problemas de configuración de red o proxy. no se puede alcanzar la red de Hola. Vea [solucionar problemas de conectividad en el Asistente para la instalación de hello](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Contraseña de usuario expirada
Las credenciales han expirado. Cambie la contraseña.

### <a name="authorizationfailure"></a>AuthorizationFailure
Problema desconocido.

### <a name="authentication-cancelled"></a>Autenticación cancelada
se canceló la comprobación de la autenticación multifactor (MFA) de Hola.

### <a name="connecttomsonline"></a>ConnectToMSOnline
La autenticación fue correcta, pero Azure AD PowerShell tiene un problema de autenticación.

### <a name="azurerolemissing"></a>AzureRoleMissing
Autenticación realizada correctamente. Usted no es un administrador global.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
Autenticación realizada correctamente. Se ha habilitado la administración de identidades con privilegios y en la actualidad usted no es un administrador global. Para más información, vea [Introducción a Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
Autenticación realizada correctamente. No se pudo recuperar la información de la empresa de Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
Autenticación realizada correctamente. No se pudo recuperar la información de domino de Azure AD.

### <a name="unexpected-exception"></a>Excepción inesperada
Se muestra como error inesperado en el Asistente para la instalación de Hola. Puede ocurrir si intenta toouse un **Account Microsoft** en lugar de un **school u organización cuenta**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Pasos para solucionar problemas de versiones anteriores.
Con las versiones a partir de número de compilación 1.1.105.0 (publicada en febrero de 2016), se retiró el Ayudante para el inicio de sesión de Hola. Esta configuración de hello y sección ya no es necesaria, pero se conserva como referencia.

Para hello inicio de sesión único en toowork del asistente, debe configurarse winhttp. Esta configuración puede realizarse con [**netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Ayudante para el inicio de sesión de Hello no se ha configurado correctamente
Este error aparece cuando el Ayudante para el inicio de sesión de hello no puede llegar al proxy de Hola u Hola proxy no permita solicitud Hola.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Si ve este error, busque en configuración de proxy de hello en [netsh](active-directory-aadconnect-prerequisites.md#connectivity) y compruebe que es correcta.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Si se ve correcta, siga los pasos de hello en [Compruebe la conectividad de proxy](#verify-proxy-connectivity) toosee si Hola problema está presente fuera así el Asistente de Hola.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
