---
title: "Azure AD Connect: actualización automática | Microsoft Docs"
description: "Este tema describe Hola integrados característica de actualización automática en la sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: actualización automática
Esta característica se introdujo con la compilación 1.1.105.0 (publicada en febrero de 2016).

## <a name="overview"></a>Información general
Nunca ha sido tan fácil con hello asegurándose de que la instalación de Azure AD Connect siempre está en funcionamiento toodate **la actualización automática** característica. Esta característica está habilitada de forma predeterminada para realizar instalaciones rápidas y actualizaciones de DirSync. Cuando se publica una nueva versión, se actualiza automáticamente la instalación.

Actualización automática está habilitada de forma predeterminada para siguiente hello:

* Instalación de la configuración rápida y actualizaciones de sincronización de directorios.
* Uso de SQL Express LocalDB, que es el modo de ejecución que siempre se utiliza en la configuración rápida. DirSync con SQL Express LocalDB también utiliza LocalDB.
* Hola cuenta de AD es cuenta de hello predeterminada MSOL_ creado por la configuración de Express y sincronización de directorios.
* Tiene menos de 100.000 objetos de metaverso Hola.

Hola estado actual de la actualización automática se puede ver con el cmdlet de PowerShell de hello `Get-ADSyncAutoUpgrade`. Tiene Hola siguientes estados:

| Estado | Comentario |
| --- | --- |
| Enabled |La actualización automática está habilitada. |
| Suspended |Hola sistema solo establece. sistema de Hello es ya no las actualizaciones automáticas de tooreceive elegibles. |
| Disabled |La actualización automática está deshabilitada. |

Puede cambiar entre **Habilitado** y **Deshabilitado** con `Set-ADSyncAutoUpgrade`. Solo sistema Hola debería establecer estado de hello **Suspended**.

La actualización automática está usando Azure AD Connect Health para la infraestructura de actualización de Hola. Para toowork de actualización automática, asegúrese de que ha abierto hello las direcciones URL en el servidor proxy para **Azure AD Connect Health** como se documenta en [intervalos de direcciones IP y las direcciones URL de Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Si hello **Synchronization Service Manager** interfaz de usuario está ejecutando en el servidor de hello, entonces hello actualización se suspende hasta que se cierre la interfaz de usuario de Hola.

## <a name="troubleshooting"></a>Solución de problemas
Si la instalación de Connect no actualizarse según lo esperado, a continuación, siga estos toofind pasos cuál podría ser incorrecto.

En primer lugar, no debería esperar Hola toobe actualización automática intentada Hola primer día que se lance una nueva versión. Hay una aleatoriedad intencional antes intentar una actualización, por lo que no se alarme si la instalación no se actualiza inmediatamente.

Si cree que algo no es el adecuado, a continuación, primero ejecute `Get-ADSyncAutoUpgrade` tooensure la actualización automática está habilitada.

A continuación, asegúrese de que ha abierto Hola requiere las direcciones URL en el servidor proxy o firewall. Actualización automática está usando Azure AD Connect Health tal y como se describe en hello [Introducción](#overview). Si usa un proxy, asegúrese de mantenimiento ha sido configurado toouse una [servidor proxy](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Probar hello [conectividad de mantenimiento](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

Con hello conectividad tooAzure AD comprobado, es hora toolook en registros de eventos de Hola. Iniciar el Visor de eventos de Hola y mire en hello **aplicación** registro de eventos. Agregar un filtro de registro de eventos para el origen de hello **actualizar conectarse de Azure AD** y el intervalo de Id. de evento de hello **300-399**.  
![Filtro de registro de eventos para la actualización automática](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

Ahora puede ver los registros de eventos de hello asociados con el estado de hello para la actualización automática.  
![Filtro de registro de eventos para la actualización automática](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

código de resultado de Hello tiene un prefijo con una visión general del estado de Hola.

| Prefijo del código de resultado | Description |
| --- | --- |
| Correcto |instalación de Hola se actualizó correctamente. |
| UpgradeAborted |Una condición temporal Detener actualización Hola. Se volverá a y expectativa de hello es que funciona correctamente más tarde. |
| UpgradeNotSupported |sistema de Hello tiene una configuración que está bloqueando el sistema de Hola desde que se actualiza automáticamente. Será toosee volverá a intentar si está cambiando el estado de hello, pero expectativa de hello es que el sistema de hello debe actualizarse manualmente. |

Esta es una lista de mensajes de Hola más comunes que encuentre. No muestra todos los, pero debe ser mensaje de resultado de hello despejado, con qué problema hello es.

| Mensaje de resultado | Description |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |No se pudo escribir el registro de toohello. |
| UpgradeAbortedInsufficientDatabasePermissions |grupo de administradores integrados de Hello no tiene la base de datos de toohello de permisos. Actualizar manualmente la versión más reciente de toohello de Azure AD Connect tooaddress este problema. |
| UpgradeAbortedInsufficientDiskSpace |Hay no hay suficientes toosupport de espacio en disco de una actualización. |
| UpgradeAbortedSecurityGroupsNotPresent |No se pudo encontrar y resolver todos los grupos de seguridad utilizados por el motor de sincronización de Hola. |
| UpgradeAbortedServiceCanNotBeStarted |Hola servicio NT **Microsoft Azure AD Sync** no se pudo toostart. |
| UpgradeAbortedServiceCanNotBeStopped |Hola servicio NT **Microsoft Azure AD Sync** no se pudo toostop. |
| UpgradeAbortedServiceIsNotRunning |Hola servicio NT **Microsoft Azure AD Sync** no se está ejecutando. |
| UpgradeAbortedSyncCycleDisabled |Hola SyncCycle opción Hola [programador](active-directory-aadconnectsync-feature-scheduler.md) se ha deshabilitado. |
| UpgradeAbortedSyncExeInUse |Hola [el administrador del servicio de sincronización UI](active-directory-aadconnectsync-service-manager-ui.md) está abierto en servidores de Hola. |
| UpgradeAbortedSyncOrConfigurationInProgress |se ejecuta el Asistente para la instalación de Hola o se programó una sincronización fuera de programador de Hola. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |Ha agregado su propia configuración de toohello de reglas personalizadas. |
| UpgradeNotSupportedDeviceWritebackEnabled |Se ha habilitado hello [reescritura de dispositivos](active-directory-aadconnect-feature-device-writeback.md) característica. |
| UpgradeNotSupportedGroupWritebackEnabled |Se ha habilitado hello [reescritura de grupos](active-directory-aadconnect-feature-preview.md#group-writeback) característica. |
| UpgradeNotSupportedInvalidPersistedState |instalación de Hello no es una configuración rápida o una actualización de la sincronización de directorios. |
| UpgradeNotSupportedMetaverseSizeExceeeded |Tiene más de 100.000 objetos en el metaverso Hola. |
| UpgradeNotSupportedMultiForestSetup |Se está conectando toomore a un único bosque. El programa de instalación rápida sólo conecta tooone bosque. |
| UpgradeNotSupportedNonLocalDbInstall |No se está utilizando una base de datos de SQL Server Express LocalDB. |
| UpgradeNotSupportedNonMsolAccount |Hola [cuenta de conector AD](active-directory-aadconnect-accounts-permissions.md#active-directory-account) ya no está cuenta de hello predeterminada MSOL_. |
| UpgradeNotSupportedStagingModeEnabled |configuración del servidor de Hello toobe [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |Se ha habilitado hello [reescritura de usuarios](active-directory-aadconnect-feature-preview.md#user-writeback) característica. |

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
