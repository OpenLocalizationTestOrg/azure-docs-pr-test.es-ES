---
title: "Solución de problemas de la configuración de Enterprise State Roaming en Azure Active Directory | Microsoft Docs"
description: "Proporciona respuestas toosome preguntas los administradores de TI podrían tener sobre la configuración y sincronización de datos de aplicaciones."
services: active-directory
keywords: "configuración de enterprise state roaming, nube de windows, preguntas más frecuentes sobre enterprise state roaming"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Solución de problemas de la configuración de Enterprise State Roaming en Azure Active Directory

Este tema proporciona información acerca de cómo tootroubleshoot y diagnosticar problemas con la itinerancia de estado de empresa y proporciona una lista de problemas conocidos.

## <a name="preliminary-steps-for-troubleshooting"></a>Pasos preliminares para solucionar problemas 
Antes de comenzar la solución de problemas, compruebe que los usuarios de Hola y de dispositivos se hayan configurado correctamente y que se cumplen todos los requisitos de Hola de itinerancia de estado de empresa por usuarios de Hola y de dispositivos de Hola. 

1. Windows 10, con las actualizaciones más recientes de hello y un mínimo versión 1511 (compilación del sistema operativo 10586 o posterior) está instalado en el dispositivo de Hola. 
2. dispositivo de Hello es Azure AD Unidos, o Unidos a un dominio y registrado con Azure AD.
3. En el portal de Azure Active Directory de hello, **itinerancia de estado de Enterprise** está habilitada para directorio de hello en **configurar** > **dispositivos**  >  **a los usuarios pueden sincronizar la configuración y datos de aplicaciones empresariales**. Todos los usuarios seleccionados, o bien usuario hello es habilitado para la sincronización a través de la opción seleccionada de Hola e incluido en el grupo de seguridad de Hola.
4. usuario de Hello tiene una suscripción de Azure Active Directory Premium asignada toothem.  
5. se ha reiniciado el dispositivo de Hola y Hola usuario ha iniciado la sesión después de que se ha habilitado la itinerancia de estado de Enterprise.

## <a name="information-tooinclude-when-you-need-help"></a>Información tooinclude cuando necesite ayuda
Si no puede resolver el problema con las guías de Hola a continuación, póngase en contacto con nuestros ingenieros de soporte técnico. Cuando se comunique con ellos, se recomienda hello tooinclude siguiente información:

- **Descripción general del error de Hola** : ¿hay mensajes de error que ve Hola usuario? Si no apareció ningún mensaje de error, describa Hola comportamiento inesperado que observó en detalle. ¿Qué características están habilitadas para la sincronización y qué es usuario de hello espera toosync? ¿Son varias características no está sincronizando o está aislada de TI tooone?
- **Usuarios afectados**: el funcionamiento o error de la sincronización afecta a uno o a varios usuarios. ¿Cuántos dispositivos están implicados por usuario? ¿No se está sincronizando ninguno de ellos o algunos se están sincronizando y otros no?
- **¿Información acerca del usuario de Hola** : qué identidad es usuario de hello en toolog toohello dispositivo? ¿Cómo se registro de usuarios de hello en dispositivo toohello? ¿Son parte de un grupo de seguridad seleccionado permitido toosync? 
- **¿Obtener información acerca del dispositivo de Hola** : este dispositivo Unidos a Azure AD o Unidos a un dominio? ¿Qué compilación es dispositivo hello en? ¿Cuáles son las actualizaciones más recientes de hello?
- **Fecha / hora / zona horaria** : ¿cuál era Hola fecha y hora precisa vio el error hello (incluya la zona horaria de hello)?
- Incluir esta información nos ayudará a solucionar su problema lo antes posible.

## <a name="troubleshooting-and-diagnosing-issues"></a>Solución de problemas y diagnóstico de problemas
Esta sección proporciona sugerencias sobre cómo tootroubleshoot y diagnosticar problemas tooEnterprise relacionados itinerancia de estado.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Comprobar la sincronización y Hola "Sincronizar la configuración" página de configuración 

1. Después de unirse a los equipos que ejecutan Windows 10 tooa dominio que está configurado tooallow itinerancia de estado de Enterprise, inicio de sesión con su cuenta profesional. Vaya demasiado**configuración** > **cuentas** > **la configuración de sincronización** y confirmar que hello y sincronización de configuración individuales y ese top Hola de página de configuración de Hello indica que están sincronizando con su cuenta profesional. Confirmar Hola cuenta también se usa como la cuenta de inicio de sesión en **configuración** > **cuentas** > **su información**. 
2. Compruebe que funciona la sincronización en varios equipos mediante la realización de algunos cambios en la máquina original de hello, como mover Hola barra de tareas toohello parte derecha o superior de la pantalla de bienvenida. Ver el cambio de hello propagar toohello segunda máquina dentro de cinco minutos. 
 - Pantalla de bienvenida de bloqueo y desbloqueo (Win + L) puede ayudar a desencadenar una sincronización.
 - Debe contar con Hola misma cuenta de inicio de sesión en ambos equipos para sincronización toowork – como itinerancia de estado de empresa es no cuenta de equipo de Hola y la cuenta de usuario de toohello relacionados.

**Problema potencial**: página de configuración de Hola se alterna de hello en gris y, en lugar de ver una cuenta, verá texto hello "algunas características de Windows sólo están disponibles si usa una cuenta de Microsoft o cuenta profesional". Este problema puede producirse para dispositivos que se han configurado toobe Unidos a un dominio y registrado tooAzure AD, pero el dispositivo de hello no ha autenticado correctamente tooAzure AD. Una posible causa es que se debe aplicar la directiva de dispositivo de hello, pero esta aplicación realiza de forma asincrónica y puede retrasarse por unas pocas horas. tooverify compruebe este problema, siga los pasos de hello en Hola toocheck de estado de registro de dispositivo si éste es el caso de hello.

### <a name="verify-hello-device-registration-status"></a>Compruebe el estado de registro del dispositivo Hola
Itinerancia de estado de empresa requiere Hola dispositivo toobe registrado con Azure AD. Aunque tooEnterprise no específico del estado de movilidad, Hola instrucciones siguientes puede ayudarle a confirmar que Hola cliente de Windows 10 está registrado y confirmar huella digital, dirección URL de la configuración de Azure AD, NGC o estado y otra información.

1.  Hola abrir símbolo reducido. toodo esto en Windows, abra Hola selector de ejecución (Win + R) y escriba "cmd" tooopen.
2.  Una vez abierto Hola símbolo del sistema, escriba "*/Status dsregcmd.exe*".
3.  Para la salida esperada, Hola **AzureAdJoined** valor del campo debe ser "YES", **WamDefaultSet** valor del campo debe ser "YES" y Hola **WamDefaultGUID** valor de campo debe ser un GUID con "(organización)" al final de Hola.

**Problema potencial**: **WamDefaultSet** y **AzureAdJoined** tanto tienen "N" en el valor del campo de hello, dispositivo Hola era Unidos a un dominio y registrado con Azure AD y dispositivo hello no se sincroniza. Si se muestra esto, dispositivo Hola puede necesita toowait para toobe de directiva aplicada u Hola autenticación para error al conectar tooAzure AD del dispositivo de Hola. usuario de Hello habrá toowait unas pocas horas para hello toobe de directiva aplicada. Otros pasos de solución de problemas pueden incluir volver a intentar el registro automático de firma y vuelve o iniciar tarea hello en el programador de tareas. En algunos casos, puede ayudar a resolver este problema ejecutar "*dsregcmd.exe /leave*" en una ventana del símbolo del sistema con privilegios elevados, reiniciar y volver a intentar el registro.


**Problema potencial**: campo de Hola para **AzureAdSettingsUrl** está vacía y hello dispositivo no sync. Hola usuario puede haber inició la última toohello dispositivo antes de habilitar la itinerancia de estado de empresa en hello Azure Active Portal de directorio. Reiniciar el dispositivo de Hola y tener inicio de sesión de usuario de Hola. Si lo desea, en el portal de hello, intente tener Hola, Administrador de TI deshabilitar y volver a habilitar la configuración de sincronización de los usuarios pueden y datos de aplicaciones empresariales. Una vez que vuelve a habilitar, reiniciar el dispositivo de Hola y tener inicio de sesión de usuario de Hola. Si no se soluciona el problema de hello, **AzureAdSettingsUrl** puede estar vacío en caso de hello de un certificado de dispositivo defectuoso. En este caso, puede ayudar a resolver este problema ejecutar "*dsregcmd.exe /leave*" en una ventana del símbolo del sistema con privilegios elevados, reiniciar y volver a intentar el registro.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Enterprise State Roaming y Multi-Factor Authentication 
Bajo ciertas condiciones, la itinerancia de estado de empresa puede producir un error toosync datos si se configura la autenticación multifactor de Azure. Para obtener más detalles sobre estos síntomas, consulte el documento de soporte técnico de hello [KB3193683](https://support.microsoft.com/kb/3193683). 

**Problema potencial**: si el dispositivo está configurado toorequire la autenticación multifactor en el portal de Azure Active Directory de hello, pueden producirse errores toosync configuración al iniciar sesión en el dispositivo tooa Windows 10 con una contraseña. Este tipo de configuración de la autenticación multifactor está previsto tooprotect una cuenta de administrador de Azure. Los usuarios administradores todavía pueden ser capaz de toosync debe iniciar sesión en dispositivos Windows 10 tootheir con su Microsoft Passport para el PIN de trabajo o realizando la autenticación multifactor al tener acceso a otros servicios de Azure como Office 365.

**Problema potencial**: sincronización puede producir un error si Hola, administrador configura la directiva de acceso condicional de Active Directory Federation Services la autenticación multifactor de Hola y el token de acceso de hello en dispositivo Hola expira. Asegúrese de que iniciar sesión y cierre la sesión usando Hola Microsoft Passport para el PIN de trabajo o completar la autenticación multifactor al tener acceso a otros servicios de Azure como Office 365.

###<a name="event-viewer"></a>Visor de eventos
Para la solución avanzada, Visor de eventos puede ser errores específicos de toofind usado. Éstos aparecen documentados en la siguiente tabla se Hola. Hola eventos pueden encontrarse en el Visor de eventos > registros de aplicaciones y servicios > **Microsoft** > **Windows** > **SettingSync** y para problemas relacionados con la identidad con la sincronización de **Microsoft** > **Windows** > **Azure AD**.


## <a name="known-issues"></a>Problemas conocidos

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>La sincronización no funciona en los dispositivos que tienen aplicaciones que se hayan cargado con software MDM

Afecta a dispositivos que ejecutan Hola actualización de aniversario de Windows 10 (versión 1607). En el Visor de eventos en registros de Azure SettingSync hello, con frecuencia se ve hello 6013 de Id. de evento con el error 80070259.

**Acción recomendada**  
Asegúrese de que cliente v1607 de hello Windows 10 tiene Hola 23 de agosto de 2016 actualización acumulativa ([KB3176934](https://support.microsoft.com/kb/3176934) 14393.82 de compilación del sistema operativo). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Los favoritos de Internet Explorer no se sincronizan

Afecta a dispositivos que ejecutan Hola actualización de noviembre de Windows 10 (versión 1511).

**Acción recomendada**  
Asegúrese de que cliente v1511 de hello Windows 10 tiene Hola julio de 2016 actualización acumulativa ([KB3172985](https://support.microsoft.com/kb/3172985) 10586.494 de compilación del sistema operativo).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>El tema no se está sincronizando, así como los datos protegidos Windows Information Protection 

tooprevent pérdida de datos, los datos que está protegidos con [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) no se sincronizarán a través de itinerancia de estado de empresa para dispositivos con Hola actualización de aniversario de Windows 10.



**Acción recomendada**  
Ninguno. Las actualizaciones futuras tooWindows puede resolver este problema.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>La configuración de fecha, hora y región no se sincroniza en dispositivos unidos a un dominio 
  
Dispositivos que están unidos a un dominio no experimentarán la sincronización de hello establecer fecha, hora y región: hora automática. Mediante la hora automática puede override Hola otros valores de fecha, hora y región y hacer que esas configuraciones no toosync. 

**Acción recomendada**  
Ninguno. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>UAC avisa al sincronizar las contraseñas

Dispositivos de afecta a ejecutando Hola actualización de noviembre de 10 (versión 1511) de Windows con una NIC inalámbrica que se configuran toosync contraseñas.

**Acción recomendada**  
Asegúrese de que cliente v1511 de hello Windows 10 tiene la actualización acumulativa de hello ([KB3140743](https://support.microsoft.com/kb/3140743) 10586.494 de compilación del sistema operativo).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>La sincronización no funciona en dispositivos que usan tarjetas inteligentes para el inicio de sesión
Si intentas toosign en el dispositivo de Windows de tooyour mediante una tarjeta inteligente o tarjeta inteligente virtual, sincronización de configuración dejará de funcionar.     

**Acción recomendada**  
Ninguno. Las actualizaciones futuras tooWindows puede resolver este problema.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>El dispositivo unidos a un dominio no se sincroniza después de salir de la red corporativa     
Dispositivos Unidos a un dominio registrado tooAzure que AD puede experimentar errores de sincronización si Hola dispositivo está fuera del sitio durante largos períodos de tiempo, no se puede completar la autenticación de dominio.

**Acción recomendada**  
Conectar red corporativa de hello dispositivo tooa de modo que puede reanudar la sincronización.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>No se está sincronizando los dispositivos de Azure AD combinada y usuario de hello tiene un nombre Principal de usuario en grafía mixta.
 Si el usuario de hello tiene un mayúsculas y minúsculas mezcladas UPN (p. ej. nombre de usuario en lugar del nombre de usuario) y hello es en un dispositivo Unidos a Azure AD que ha actualizado desde Windows 10 de compilación 10586 too14393, dispositivo del usuario de hello puede producir un error toosync. 

**Acción recomendada**  
usuario de Hello necesitará toounjoin y volver a unir el dispositivo de la nube toohello Hola. toodo, inicie sesión como usuario de administrador Local de Hola y separación de dispositivo de hello yendo demasiado**configuración** > **System** > **sobre** y seleccione " Administrar o desconectarse de la empresa o centro educativo". Limpiar los archivos de hello y, a continuación, Azure AD Join Hola dispositivo nuevo en **configuración** > **System** > **sobre** y seleccionando "conectar tooWork o la escuela". Continuar toojoin Hola dispositivo tooAzure Active Directory y el flujo de hello completa.

En el paso de limpieza de hello, Hola de limpieza siguientes archivos:
- Settings.dat en `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Todos los archivos de Hola Hola carpeta`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>Id. de evento 6065: 80070533 Este usuario no puede iniciar sesión porque esta cuenta está deshabilitada  
Este error puede verse en el Visor de eventos en registros de hello SettingSync/Debug, cuando las credenciales del usuario de hello expiraron. Además, puede producirse cuando el inquilino de hello no tenía automáticamente AzureRMS aprovisionado. 

**Acción recomendada**  
En el primer caso de hello, tener usuario Hola actualizar sus credenciales y el dispositivo de inicio de sesión toohello con nuevas credenciales de Hola. Hola toosolve AzureRMS problema, continúe con pasos de hello enumerados en [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>Id. de evento 1098: Error: error en la operación del agente de token de 0xCAA5001C  
En el Visor de eventos en registros AAD/Operational hello, este error puede aparecer con el evento 1104: punto de acceso de AAD en la nube complemento llamada Get símbolo (token) devolvió el error: 0xC000005F. Este problema se produce si faltan permisos o atributos de propiedad.    

**Acción recomendada**  
Continúe con los pasos de hello aparecen [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Pasos siguientes

- Hola de uso [foro de User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) sugerencias de comentarios y asegúrese de tooprovide en cómo Enterprise tooimprove estado de movilidad.

- Para obtener más información, vea hello [Introducción a la itinerancia de estado de Enterprise](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Temas relacionados
* [Información general de Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitación de Enterprise State Roaming en Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Preguntas más frecuentes sobre itinerancia de datos y configuración](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Configuración de MDM y directivas de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referencia de la configuración de movilidad de Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
