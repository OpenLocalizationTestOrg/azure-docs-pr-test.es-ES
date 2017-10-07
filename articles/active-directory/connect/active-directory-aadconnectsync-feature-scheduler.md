---
title: "Sincronización de Azure AD Connect: Scheduler | Microsoft Docs"
description: "Este tema describe la característica de programador integrado hello en la sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Sincronización de Azure AD Connect: Programador
Este tema describe a programador integrado de hello en la sincronización de Azure AD Connect (conocido como) motor de sincronización).

Esta característica se introdujo con la compilación 1.1.105.0 (publicada en febrero de 2016).

## <a name="overview"></a>Información general
Azure AD Connect Sync sincronizará los cambios que se producen en su directorio local mediante un programador. Hay dos procesos de programador, uno para la sincronización de contraseñas y otro para la sincronización de objetos o atributos y tareas de mantenimiento. Este tema tratan Hola este último.

En versiones anteriores, programador de Hola para objetos y atributos era motor de sincronización de toohello externo. Utiliza el programador de tareas de Windows o un proceso de sincronización de Windows servicio tootrigger Hola independiente. Programador de Hello es con Hola motor de sincronización de toohello integrados de las versiones 1.1 y permitir alguna personalización. frecuencia de sincronización de Hello nuevo valor predeterminado es 30 minutos.

Programador de Hello es responsable de dos tareas:

* **Ciclo de sincronización**. Hola proceso tooimport, sincronización y los cambios de exportación.
* **Tareas de mantenimiento**. Renueve las claves y certificados para el restablecimiento de contraseña y el servicio de registro de dispositivos (DRS). Purgar las entradas más antiguas en el registro de operaciones de Hola.

Programador de Hello propio siempre se está ejecutando, pero puede ser configurado tooonly ejecutar una o ninguna de estas tareas. Por ejemplo, si necesita toohave su propio proceso de ciclo de sincronización, puede deshabilitar esta tarea en el programador de hello pero la tarea de mantenimiento de hello sigue en ejecución.

## <a name="scheduler-configuration"></a>Configuración del programador
toosee las opciones de configuración actual, vaya tooPowerShell y ejecute `Get-ADSyncScheduler`. Muestra algo parecido a esta imagen:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Si ve **no está disponible el comando de sincronización de Hola o cmdlet** cuando se ejecuta este cmdlet, a continuación, módulo de PowerShell de hello no está cargado. Este problema puede ocurrir si ejecutar Azure AD Connect en un controlador de dominio o en un servidor con mayores niveles de restricción de PowerShell que la configuración predeterminada de Hola. Si ve este error, a continuación, ejecute `Import-Module ADSync` toomake Hola cmdlet disponible.

* **AllowedSyncCycleInterval**. Intervalo tiempo más corto de Hello entre los ciclos de sincronización permitida por Azure AD. No se puede sincronizar con más frecuencia que esta configuración y mantener la compatibilidad.
* **CurrentlyEffectiveSyncCycleInterval**. Hola programación actualmente en vigor. Tiene Hola mismo valor que CustomizedSyncInterval (Si establecer) si no es más frecuente que AllowedSyncInterval. Si usa una compilación anterior a 1.1.281 y cambia CustomizedSyncCycleInterval, esto surte efecto tras el próximo ciclo de sincronización. De compilación 1.1.281 cambio Hola surte efecto inmediatamente.
* **CustomizedSyncCycleInterval**. Si desea Hola programador toorun con cualquier otra frecuencia predeterminado de Hola 30 minutos, configure esta opción. En la imagen anterior de hello, programador de Hola se estableció toorun cada hora en su lugar. Si establece este valor tooa inferior a AllowedSyncInterval, se utiliza este último Hola.
* **NextSyncCyclePolicyType**. Diferencial o inicial. Define si Hola a continuación ejecute debe procesar solo los cambios de delta, o si hello siguiente ejecución debería hacer una completa importar y sincronizar. Hola este último también podría volver a procesar las reglas nuevas o modificadas.
* **NextSyncCycleStartTimeInUTC**. Próxima vez que inicie el programador de Hola Hola siguiente ciclo de sincronización.
* **PurgeRunHistoryInterval**. Hola operación tiempo deben mantenerse los registros. Estos registros se pueden revisar en el Administrador de servicio de sincronización de Hola. Hola predeterminada es tookeep estos registros durante 7 días.
* **SyncCycleEnabled**. Indica si el programador de hello está ejecutando importación hello, sincronización y los procesos de exportación como parte de su funcionamiento.
* **MaintenanceEnabled**. Muestra si se habilita el proceso de mantenimiento de Hola. Actualiza certificados o claves de Hola y Hola de purga de registro de operaciones.
* **StagingModeEnabled**. Muestra si el [modo provisional](active-directory-aadconnectsync-operations.md#staging-mode) está habilitado. Sin embargo si esta opción está habilitada, a continuación, se suprimen Hola exportaciones de ejecución, Ejecutar importación y sincronización.
* **SchedulerSuspended**. Establecidas por conectar durante un programador de hello tootemporarily actualización bloque de ejecución.

Puede cambiar algunos de estos valores con `Set-ADSyncScheduler`. se puede modificar Hola parámetros siguientes:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

En compilaciones anteriores de Azure AD Connect, **isStagingModeEnabled** se expuso en Set-ADSyncScheduler. Es **no compatible** tooset esta propiedad. Hola propiedad **SchedulerSuspended** solo debe modificarse, Connect. Es **no compatible** tooset esto con PowerShell directamente.

configuración del programador Hola se almacena en Azure AD. Si tiene un servidor de ensayo, cualquier cambio en el servidor principal de hello también afecta al servidor (excepto IsStagingModeEnabled) de almacenamiento provisional de Hola.

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Sintaxis: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
 d: días; HH: horas; mm: minutos; ss: segundos

Ejemplo: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Cambios Hola programador toorun cada tres horas.

Ejemplo: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Los cambios realizados Hola programador toorun diariamente.

### <a name="disable-hello-scheduler"></a>Deshabilite al programador de Hola  
Si necesita cambios de configuración de toomake, a continuación, deberá a Programador de hello toodisable. Por ejemplo, cuando se [configurar el filtrado de](active-directory-aadconnectsync-configure-filtering.md) o [realizar cambios en las reglas de toosynchronization](active-directory-aadconnectsync-change-the-configuration.md).

Programador de hello toodisable, ejecute `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Deshabilite al programador de Hola](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Una vez realizados los cambios, no olvide programador de hello tooenable nuevo con `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Inicie el programador de Hola
Programador de Hello es ejecutar cada 30 minutos de forma predeterminada. En algunos casos, quizás desee toorun ciclo de una sincronización entre Hola programado ciclos o necesita toorun un tipo diferente.

**Ciclo de sincronización diferencial**  
Un ciclo de sincronización delta incluye Hola pasos:

* Importación diferencial en todos los conectores
* Sincronización diferencial en todos los conectores
* Exportación en todos los conectores

Es posible que haya una urgencia cambio que se debe sincronizar inmediatamente, motivo por el cual debe toomanually ejecutar un ciclo. Si necesita toomanually ejecutar un ciclo, a continuación, de ejecución de PowerShell `Start-ADSyncSyncCycle -PolicyType Delta`.

**Ciclo de sincronización completo**  
Si ha realizado una Hola después de los cambios de configuración, deberá toorun un ciclo de sincronización completa (conocido como) sincronización inicial):

* Agregar más toobe atributos u objetos importado desde un directorio de origen
* Realizó cambios en las reglas de sincronización de toohello
* Cambió el [filtrado](active-directory-aadconnectsync-configure-filtering.md) para que se incluya un número diferente de objetos

Si ha realizado alguno de estos cambios, debe toorun ciclo de una sincronización completa para que el motor de sincronización de hello tiene espacios conectores de hello oportunidad tooreconsolidate Hola. Un ciclo de sincronización completa incluye Hola pasos:

* Importación completa en todos los conectores
* Sincronización completa en todos los conectores
* Exportación en todos los conectores

tooinitiate un ciclo de sincronización completa, ejecute `Start-ADSyncSyncCycle -PolicyType Initial` desde un símbolo del sistema de PowerShell. Este comando inicia un ciclo de sincronización completo.

## <a name="stop-hello-scheduler"></a>Detener el programador de Hola
Si el programador de saludo se está ejecutando un ciclo de sincronización, puede que tenga toostop. Por ejemplo, si inicia el Asistente para la instalación de Hola y recibirá este error:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Cuando se está ejecutando un ciclo de sincronización, no puede realizar cambios de configuración. Se podría esperar hasta que el programador de hello ha finalizado el proceso de hello, pero también puede detener por lo que puede hacer los cambios inmediatamente. Detener Hola ciclo actual no es dañino y los cambios pendientes se procesan con ejecutar a continuación.

1. Inicio indicándole Hola programador toostop con su actual ciclo con el cmdlet de PowerShell de hello `Stop-ADSyncSyncCycle`.
2. Si usas una compilación antes de 1.1.281 y, después, deteniendo el programador de hello no Hola actual conector de su tarea actual. tooforce Hola conector toostop, tomar Hola siguientes acciones: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Iniciar **servicio de sincronización de** desde el menú de inicio de Hola. Vaya demasiado**conectores**, resalte Hola conector con el estado de hello **ejecutando**y seleccione **detener** de hello acciones.

Programador de Hello aún está activo y se inicia de nuevo en la siguiente oportunidad.

## <a name="custom-scheduler"></a>Programador personalizado
Hello cmdlets documentadas en esta sección solo están disponibles en la compilación [1.1.130.0](active-directory-aadconnect-version-history.md#111300) y versiones posteriores.

Si el programador integrado hello no satisface sus requisitos, puede programar conectores hello mediante PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
Puede iniciar un perfil para un conector de esta manera:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Hola nombres toouse para [nombres de conectores](active-directory-aadconnectsync-service-manager-ui-connectors.md) y [nombres de perfil de ejecución](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) puede encontrarse en hello [UI Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

![Invocar el perfil de ejecución](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Hola `Invoke-ADSyncRunProfile` cmdlet es sincrónico, es decir, no devuelve el control hasta Hola conector ha completado la operación de hello, ya sea correctamente o con error.

Cuando se programan sus conectores, recomendación de hello es tooschedule ellas en hello siguiendo el orden:

1. (Diferencial y completo) Importar desde directorios locales, como Active Directory
2. (Diferencial y completo) Importar desde Azure AD
3. (Diferencial y completo) Sincronización desde directorios locales, como Active Directory
4. (Diferencial y completo) Sincronización desde Azure AD
5. Exportar tooAzure AD
6. Exportar directorios de tooon locales, como Active Directory

Este orden es cómo programador integrado Hola ejecuta Hola conectores.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
También puede supervisar toosee de motor de sincronización de hello si está ocupado o inactivo. Este cmdlet devuelve un resultado vacío si el motor de sincronización de hello está inactivo y no está ejecutando un conector. Si está ejecutando un conector, devuelve el nombre de Hola de hello conector.

```
Get-ADSyncConnectorRunStatus
```

![Estado de la ejecución de conector](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
En la imagen anterior de hello, primera línea de hello es desde un estado donde el motor de sincronización de hello está inactivo. segunda línea de Hola de cuando se está ejecutando Hola conector de Azure AD.

## <a name="scheduler-and-installation-wizard"></a>Programador y Asistente para instalación
Si inicia el Asistente para la instalación de hello, programador de Hola se suspende temporalmente. Este comportamiento es como se supone realizar cambios de configuración y no se puede aplicar esta configuración si el motor de sincronización de saludo se está ejecutando activamente. Por esta razón, no deje a Asistente para la instalación de hello abierto desde que se detiene el motor de sincronización de Hola de realizar ninguna acción de sincronización.

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
