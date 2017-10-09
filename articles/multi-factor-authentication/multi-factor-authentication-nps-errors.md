---
title: "códigos de error de aaaTroubleshoot para hello extensión de NPS de MFA de Azure | Documentos de Microsoft"
description: "Obtener ayuda para solucionar problemas relacionados con hello extensión NPS para la autenticación multifactor de Azure con soluciones específicas para mensajes de error comunes"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Resolver mensajes de error de hello extensión NPS para la autenticación multifactor de Azure

Si se producen errores con hello extensión NPS para la autenticación multifactor de Azure, use este tooreach una resolución de artículo con mayor rapidez. 

## <a name="troubleshooting-steps-for-common-errors"></a>Pasos para la solución de errores comunes

| Código de error | Pasos para solucionar problemas |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Póngase en contacto con soporte técnico](#contact-microsoft-support)e indique el lista Hola de pasos para recopilar registros. Proporcione toda la información posible acerca de qué sucedió antes del error de hello, incluidos el identificador del inquilino y nombre principal de usuario (UPN). |
| **CLIENT_CERT_INSTALL_ERROR** | Puede haber un problema con cómo el certificado de cliente de Hola se instaló o asociada con su inquilino. Siga las instrucciones de hello en [Hola de solución de problemas extensión MFA NPS](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate problemas de certificados de cliente. |
| **ESTS_TOKEN_ERROR** | Siga las instrucciones de hello en [Hola de solución de problemas extensión MFA NPS](multi-factor-authentication-nps-extension.md#troubleshooting) AAL y el certificado de cliente de tooinvestigate problemas de token. |
| **HTTPS_COMMUNICATION_ERROR** | servidor NPS Hello es respuestas no se puede tooreceive de MFA de Azure. Compruebe que los firewalls están abierto bidireccional para tráfico tooand de https://adnotifications.windowsazure.com |
| **HTTP_CONNECT_ERROR** | En el servidor de Hola que se ejecuta la extensión NPS hello, compruebe que puede comunicarse con https://adnotifications.windowsazure.com y https://login.microsoftonline.com/. Si esos sitios no cargan, solucione los problemas de conectividad que tenga ese servidor. |
| **REGISTRY_CONFIG_ERROR** | Una clave no está presente en el registro de hello para la aplicación hello, que puede deberse a que hello [script de PowerShell](multi-factor-authentication-nps-extension.md#install-the-nps-extension) no se haya ejecutado después de la instalación. mensaje de error de Hello debe incluir clave ausente Hola. Asegúrese de que tiene la clave de hello en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa. |
| **REQUEST_FORMAT_ERROR** <br> Falta el atributo nombreUsuario\Identificador obligatorio en la solicitud de RADIUS. Compruebe que NPS recibe las solicitudes de RADIUS | Este error refleja habitualmente un problema de instalación. Hola extensión NPS debe instalarse en servidores NPS que pueden recibir solicitudes RADIUS. Los servidores de NPS que están instalados como dependencias para servicios como RDG y RRAS no reciben solicitudes de RADIUS. Extensión de NPS no funciona cuando se instala sobre estas instalaciones y errores porque no puede leer los detalles de saludo de solicitud de autenticación de Hola. |
| **REQUEST_MISSING_CODE** | Asegúrese de que Protocolo de cifrado de contraseña de hello entre servidores NAS y NPS hello es compatible con el método de autenticación secundario Hola que esté usando. **PAP** admite todos los métodos de autenticación de Hola de MFA de Azure en la nube de hello: llamada de teléfono, mensaje de texto unidireccional, notificación de aplicación móvil y código de comprobación de la aplicación móvil. **CHAPV2** y **EAP** admiten llamadas de teléfono y notificaciones de aplicación móvil. |
| **USERNAME_CANONICALIZATION_ERROR** | Compruebe que Hola usuario esté presente en la instancia local de Active Directory, y ese servicio NPS hello tiene directorio de hello tooaccess de permisos. Si usa confianzas entre bosques, [póngase en contacto con el servicio de soporte técnico](#contact-microsoft-support) para más ayuda. |


   

### <a name="alternate-login-id-errors"></a>Errores de identificador de inicio de sesión alternativo

| Código de error | Mensaje de error | Pasos para solucionar problemas |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Error: error de búsqueda de userObjectSid | Compruebe que el usuario Hola existe en la instancia local de Active Directory. Si usa confianzas entre bosques, [póngase en contacto con el servicio de soporte técnico](#contact-microsoft-support) para más ayuda. |
| **ALTERNATE_LOGIN_ID_ERROR** | Error: error en la búsqueda de LoginId alternativo | Compruebe que LDAP_ALTERNATE_LOGINID_ATTRIBUTE esté establecido tooa [atributos de active directory válido](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> Si LDAP_FORCE_GLOBAL_CATALOG se establece tooTrue o LDAP_LOOKUP_FORESTS está configurado con un valor no vacío, compruebe que ha configurado un catálogo Global y se agrega a ese atributo de AlternateLoginId de hello tooit. <br><br> Si LDAP_LOOKUP_FORESTS está configurado con un valor no vacío, compruebe que el valor de hello es correcto. Si hay más de un nombre de bosque, nombres de hello deben separarse con punto y coma, no espacios. <br><br> Si estos pasos no soluciona el problema de hello, [póngase en contacto con soporte técnico](#contact-microsoft-support) para obtener más ayuda. |
| **ALTERNATE_LOGIN_ID_ERROR** | Error: el valor de LoginId alternativo está vacío | Compruebe que ese atributo de AlternateLoginId Hola está configurado para el usuario de Hola. |


## <a name="errors-your-users-may-encounter"></a>Errores que pueden encontrar los usuarios

| Código de error | Mensaje de error | Pasos para solucionar problemas |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Inquilino de autor de llamada no tiene autenticación de toodo de permisos de acceso para el usuario de Hola | Compruebe si hello dominio del inquilino y el dominio de Hola Hola nombre principal de usuario (UPN) se Hola igual. Por ejemplo, asegúrese de que user@contoso.com está tratando de tooauthenticate toohello Contoso inquilino. Hola UPN representa un usuario válido para el inquilino de hello en Azure. |
| **AuthenticationMethodNotConfigured** | Hola especifica el método de autenticación no se configuró para el usuario de Hola | Tener usuario Hola agregar o comprobar sus métodos de verificación según las instrucciones de toohello en [administrar la configuración de verificación en dos pasos](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | No se admite el método de autenticación especificado. | Recopile todos los registros que incluyen este error y [póngase en contacto con el servicio de soporte técnico](#contact-microsoft-support). Cuando póngase en contacto con el soporte técnico, proporcione el nombre de usuario de Hola y método de verificación secundaria hello que desencadenó el error Hola. |
| **BecAccessDenied** | MSODS Bec llamada devuelve acceso denegado, probablemente Hola username no está definido en el inquilino de Hola | usuario de Hola está presente en el Active Directory local pero no se ha sincronizado en Azure AD mediante AD Connect. O bien, usuario hello no está presente para el inquilino de Hola. Agregar usuario de hello tooAzure AD y pídale que le agregue sus métodos de verificación según las instrucciones de toohello en [administrar la configuración de verificación en dos pasos](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** o **StrongAuthenticationServiceInvalidParameter** | número de teléfono de Hello tiene un formato irreconocible | Haga que el usuario de hello corregir sus números de teléfono de comprobación. |
| **InvalidSession** | Hola especificado sesión no es válida o haber expirado | sesión de Hello ha tardado más de tres minutos toocomplete. Compruebe ese usuario hello es escribir el código de comprobación de Hola o se responde toohello notificación de la aplicación, en los tres minutos de iniciar la solicitud de autenticación de Hola. Si no se soluciona el problema de hello, compruebe que no haya ningún latencias de red entre el cliente, servidor NAS, servidor NPS y el punto de conexión de hello Azure MFA.  |
| **NoDefaultAuthenticationMethodIsConfigured** | No se configuró ningún método de autenticación predeterminado para el usuario de Hola | Tener usuario Hola agregar o comprobar sus métodos de verificación según las instrucciones de toohello en [administrar la configuración de verificación en dos pasos](./end-user/multi-factor-authentication-end-user-manage-settings.md). Compruebe ese usuario Hola ha elegido un método de autenticación predeterminado y configurado ese método para su cuenta. |
| **OathCodePinIncorrect** | Se escribió un PIN y un código de error incorrectos. | Este error no se espera en hello extensión NPS. Si el usuario encuentra este error, [póngase en contacto con el servicio de soporte técnico](#contact-microsoft-support) para ayuda en la solución de problemas. |
| **ProofDataNotFound** | Datos de prueba no se configuró para hello especificada método de autenticación. | Tener usuario Hola pruebe un método de verificación diferente o agregue un nuevos métodos de comprobación según las instrucciones de toohello en [administrar la configuración de verificación en dos pasos](./end-user/multi-factor-authentication-end-user-manage-settings.md). Si el usuario de hello continúa toosee este error después de confirma que su método de comprobación se ha configurado correctamente, [póngase en contacto con soporte técnico](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Se escribió un PIN y un código de error incorrectos. (OneWaySMS) | Este error no se espera en hello extensión NPS. Si el usuario encuentra este error, [póngase en contacto con el servicio de soporte técnico](#contact-microsoft-support) para ayuda en la solución de problemas. |
| **TenantIsBlocked** | El inquilino está bloqueado | [Póngase en contacto con soporte técnico](#contact-microsoft-support) con Id. de directorio de la página de propiedades de hello Azure AD en hello portal de Azure. |
| **UserNotFound** | no se encontró el usuario especificado de Hola | Hola inquilino ya no es visible como activa en Azure AD. Compruebe que la suscripción está activa y tiene Hola necesario en primer lugar las aplicaciones de terceros. También asegúrese de inquilino de hello en el asunto del certificado de hello es como se esperaba y cert Hola sigue siendo válido y registrado en la entidad de servicio de Hola. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Mensajes que pueden encontrar los usuarios que no son errores

A veces, los usuarios pueden recibir mensajes de Multi-Factor Authentication debido a un error de la solicitud de autenticación. Estos no son errores de producto de Hola de configuración, pero son advertencias intencionales que explique por qué se denegó una solicitud de autenticación.

| Código de error | Mensaje de error | Pasos recomendados | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Se escribió un código incorrecto\Código OATH incorrecto | No es un error, el usuario escribió un código incorrecto. | usuario de Hello escrito código incorrecto Hola. Pídale que solicite un código nuevo o que vuelva a iniciar sesión para intentarlo nuevamente. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Se alcanzó el número máximo de reintentos de código | usuario de Hello error en la comprobación de la comprobación de hello demasiadas veces. Dependiendo de su configuración, puede que necesiten toobe desbloqueado por un administrador ahora.  |
| **SMSAuthFailedWrongCodeEntered** | Se escribió un código incorrecto/OTP de mensaje de texto incorrecto | usuario de Hello escrito código incorrecto Hola. Pídale que solicite un código nuevo o que vuelva a iniciar sesión para intentarlo nuevamente. |

## <a name="errors-that-require-support"></a>Errores que requieren soporte técnico

Si encuentra uno de estos errores, se recomienda [ponerse en contacto con el servicio de soporte técnico](#contact-microsoft-support) para obtener ayuda en el diagnóstico. No hay un conjunto estándar de pasos para abordar estos errores. Al ponerse en contacto con soporte técnico, ser seguro tooinclude como la cantidad de información posible acerca de los pasos de Hola que ha provocado el error tooan y la información del inquilino.

| Código de error | Mensaje de error |
| ---------- | ------------- |
| **InvalidParameter** | La solicitud no debe ser nula |
| **InvalidParameter** | El valor ObjectId no debe estar vacío ni ser un valor nulo para ReplicationScope:{0} |
| **InvalidParameter** | Hola longitud de CompanyName \{0} \ tiene más de {1} de longitud máxima permitida de Hola |
| **InvalidParameter** | El valor UserPrincipalName no debe estar vacío ni ser un valor nulo |
| **InvalidParameter** | Hola proporciona que tenantid no tiene formato correcto |
| **InvalidParameter** | El valor SessionId no debe estar vacío ni ser un valor nulo |
| **InvalidParameter** | No se pudo resolver ningún valor ProofData desde la solicitud o Msods. Hola ProofData es desconocido |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Pasos siguientes

### <a name="troubleshoot-user-accounts"></a>Solución de problemas de cuentas de usuario

Si los usuarios [tienen problemas con la verificación en dos pasos](./end-user/multi-factor-authentication-end-user-troubleshoot.md), ayúdelos a autodiagnosticar problemas. 

### <a name="contact-microsoft-support"></a>Consultar al soporte técnico de Microsoft

Si necesita ayuda adicional, póngase en contacto con un profesional de soporte técnico a través de [Soporte técnico del servidor Azure Multi-Factor Authentication](https://support.microsoft.com/oas/default.aspx?prid=14947). Al ponerse en contacto con nosotros, nos resultará de gran utilidad que incluya tanta información sobre su problema como sea posible. Información que puede proporcionar incluye página Hola donde vio error hello, Hola Id. de Hola de código, Id. de sesión específico de hello, de error específico del usuario de Hola que vio el error de Hola y registros de depuración.

toocollect registros de depuración para el diagnóstico de soporte técnico, use Hola pasos: 

1. Abra un símbolo del sistema de administrador y ejecute estos comandos:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Reproduzca el problema de Hola

3. Para detener la traza de hello con estos comandos:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Comprima el contenido de Hola de carpeta C:\NPS de Hola y adjunte el caso de soporte técnico de hello zip archivo toohello.


