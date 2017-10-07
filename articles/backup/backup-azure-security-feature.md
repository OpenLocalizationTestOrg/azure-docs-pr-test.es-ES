---
title: "aaaSecurity características toohelp proteger las copias de seguridad híbrido que utilice la copia de seguridad de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las características toouse seguridad en copia de seguridad de Azure toomake las copias de seguridad más seguras"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Toohelp de características de seguridad proteger las copias de seguridad híbrido que utilice la copia de seguridad de Azure
Cada vez es mayor la preocupación que generan problemas de seguridad como malware, ransomware e intrusión. Estos problemas de seguridad pueden ser costosos, en términos de dinero y datos. tooguard contra estos ataques, la copia de seguridad de Azure ahora proporciona seguridad características toohelp proteger las copias de seguridad híbrido. Este artículo trata cómo tooenable y usar estas características, mediante el uso de un agente de servicios de recuperación de Azure y un servidor de copia de seguridad de Azure. Estas características son:

- **Prevención**. Se agrega una capa adicional de autenticación cada vez que se realiza una operación crítica, como cambiar la frase de contraseña. Esta validación es tooensure que estas operaciones se pueden realizar solamente los usuarios que tienen credenciales válidas de Azure.
- **Alertas**. Se envía una notificación de correo electrónico se lleva a cabo toohello suscripción administrador cada vez que una operación crítica como la eliminación de los datos de copia de seguridad. Este correo electrónico garantiza que el usuario Hola se notifique rápidamente acerca de estas acciones.
- **Recuperación**. Datos de copia de seguridad eliminados se conservan durante más 14 días desde la fecha de Hola de eliminación de Hola. Esto garantiza la recuperación de datos de hello dentro de un período de tiempo determinado, así que no hay ninguna pérdida de datos, incluso si se produce un ataque. Además, un mayor número de puntos de recuperación mínimo se mantiene tooguard con datos dañados.

> [!NOTE]
> Las características de seguridad no se deben habilitar si usa la copia de seguridad de VM de infraestructura como servicio (IaaS). Estas características no están aún disponibles para la copia de seguridad de VM de IaaS, por lo que su habilitación no tendrá ningún impacto. Las características de seguridad solo se deben habilitar si se usa: <br/>
>  * **Agente de Azure Backup**. La versión mínima del agente es la 2.0.9052. Después de haber habilitado estas características, debe actualizar operaciones críticas de toothis agente versión tooperform. <br/>
>  * **Azure Backup Server**. La versión mínima del agente de Azure Backup es la 2.0.9052 con Update 1 de Azure Backup Server. <br/>
>  * **System Center Data Protection Manager**. La versión mínima del agente de Azure Backup es la 2.0.9052 con Data Protection Manager 2012 R2 UR12 o Data Protection Manager 2016 UR2. <br/> 


> [!NOTE]
> Estas características solo están disponibles para el almacén de Recovery Services. Hola todos los que acaba de crear almacenes de servicios de recuperación con las siguientes características habilitadas de forma predeterminada. Para almacenes de servicios de recuperación existentes, los usuarios habilitar estas características mediante el uso de pasos de hello mencionados en hello pasos de la sección. Después de hello características están habilitadas, se aplican equipos de agente de servicios de recuperación de tooall hello, instancias de servidor de copia de seguridad de Azure y servidores de Data Protection Manager registrados con el almacén de Hola. La habilitación a esta configuración es una acción única, por lo que una vez que se habiliten estas características no será posible deshabilitarlas.
>

## <a name="enable-security-features"></a>Habilitar características de seguridad
Si va a crear un almacén de servicios de recuperación, puede usar todas las características de seguridad de Hola. Si trabaja con un almacén existente, habilite las características de seguridad siguiendo estos pasos:

1. Inicie sesión en toohello portal de Azure mediante sus credenciales de Azure.
2. Seleccione **Examinar** y escriba **Recovery Services**.

    ![Captura de pantalla de opción Examinar de Azure Portal](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    aparece en la lista de Hola de almacenes de servicios de recuperación. Seleccione un almacén en ella. de este modo se abrirá el panel de Hello almacén seleccionado.
3. En lista de Hola de elementos que aparece en el almacén de hello, en **configuración**, haga clic en **propiedades**.

    ![Captura de pantalla de opciones del almacén de Recovery Services](./media/backup-azure-security-feature/vault-list-properties.png)
4. En **Configuración de seguridad**, haga clic en **Actualizar**.

    ![Captura de pantalla de propiedades del almacén de Recovery Services](./media/backup-azure-security-feature/security-settings-update.png)

    vínculo de actualización Hello abre Hola **configuración de seguridad** hoja, que proporciona un resumen de las características de Hola y que permite habilitarlos.
5. Desde la lista desplegable de hello **ha configurado la autenticación multifactor Azure?**, seleccione un valor tooconfirm si ha habilitado la [la autenticación multifactor Azure](../multi-factor-authentication/multi-factor-authentication.md). Si está habilitado, se le preguntará tooauthenticate desde otro dispositivo (por ejemplo, un teléfono móvil) al iniciar sesión en toohello portal de Azure.

   Al realizar operaciones críticas en copia de seguridad, tiene tooenter un PIN, disponible en el portal de Azure Hola de seguridad. Al habilitar Azure Multi-Factor Authentication, se agrega una capa de seguridad. Sólo los usuarios con credenciales válidas de Azure autorizados y autenticó desde otro dispositivo, puede tener acceso a Hola portal de Azure.
6. Seleccione la configuración de seguridad de toosave, **habilitar** y haga clic en **guardar**. Puede seleccionar **habilitar** sólo después de seleccionar un valor de hello **ha configurado la autenticación multifactor Azure?** lista en el paso anterior de Hola.

    ![Captura de pantalla de configuración de seguridad](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Recuperar datos de copia de seguridad eliminados
Copia de seguridad conserva los datos de copia de seguridad se eliminó durante 14 días más y no se elimina inmediatamente si hello **Detener copia de seguridad con los datos de copia de seguridad de delete** se realiza la operación. toorestore estos datos en el período de 14 días de hello, tomar Hola siguiendo los pasos, dependiendo de lo que está usando:

En el caso de los usuarios del **agente de Azure Recovery Services**:

1. Si el equipo de Hola donde se sucede las copias de seguridad sigue estando disponible, utilice [recuperar datos toohello mismo equipo](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) en servicios de recuperación de Azure, toorecover de todos los puntos de recuperación antiguos de Hola.
2. Si este equipo no está disponible, utilice [recuperar tooan alternativo máquina](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse otro tooget del equipo de servicios de recuperación de Azure estos datos.

Para los usuarios de **Azure Backup Server**:

1. Si servidor hello donde se sucede las copias de seguridad sigue estando disponible, volver a proteger Hola eliminar orígenes de datos así como usar hello **recuperar datos** toorecover de todos los puntos de recuperación antiguos de Hola de características.
2. Si este servidor no está disponible, utilice [recuperar datos desde otro servidor de copia de seguridad de Azure](backup-azure-alternate-dpm-server.md) toouse tooget la instancia del servidor de copia de seguridad de Azure otro estos datos.

En el caso de los usuarios de **Data Protection Manager**:

1. Si servidor hello donde se sucede las copias de seguridad sigue estando disponible, volver a proteger Hola eliminar orígenes de datos así como usar hello **recuperar datos** toorecover de todos los puntos de recuperación antiguos de Hola de características.
2. Si este servidor no está disponible, utilice [agregar DPM externo](backup-azure-alternate-dpm-server.md) toouse otro tooget de servidor de Data Protection Manager estos datos.

## <a name="prevent-attacks"></a>Prevenir ataques
Se han agregado comprobaciones toomake seguro solo los usuarios válidos pueden realizar varias operaciones. Entre estas se incluyen la adición de una capa de autenticación adicional y el mantenimiento de una duración de retención mínima con fines de recuperación.

### <a name="authentication-tooperform-critical-operations"></a>Operaciones críticas de autenticación tooperform
Como parte de agregar una capa adicional de autenticación para las operaciones críticas, se le tooenter solicitada un PIN de seguridad al realizar **detener la protección con datos de eliminación** y **frase de contraseña de cambio** operaciones .

tooreceive este PIN:

1. Inicie sesión en toohello portal de Azure.
2. Examinar demasiado**del almacén de servicios de recuperación** > **configuración** > **propiedades**.
3. En **PIN de seguridad**, haga clic en **Generar**. Se abrirá una hoja que contiene Hola PIN toobe especificado en la interfaz de usuario de agente de servicios de recuperación de Azure Hola.
    Este PIN solo es válido durante cinco minutos y se genera automáticamente después de ese período.

### <a name="maintain-a-minimum-retention-range"></a>Mantener una duración de retención mínima
tooensure que siempre hay un número válido de la recuperación de puntos disponibles, se han agregado Hola siguientes comprobaciones:

- Para la retención diaria, se deben realizar un mínimo de **siete** días de retención.
- Para la retención semanal, se deben realizar un mínimo de **cuatro** semanas de retención.
- Para la retención mensual, se deben realizar un mínimo de **tres** meses de retención.
- Para la retención anual, se debe realizar un mínimo de **un** año de retención.

## <a name="notifications-for-critical-operations"></a>Notificaciones de operaciones críticas
Normalmente, cuando se realiza una operación crítica, Hola, Administrador de suscripción se envía una notificación por correo electrónico con detalles sobre la operación de Hola. Puede configurar a los destinatarios de correo electrónico adicionales para estas notificaciones mediante Hola portal de Azure.

características de seguridad de Hola se mencionan en este artículo proporcionan los mecanismos de defensa contra ataques dirigidos. Lo que es más importante, si se produce un ataque, estas características ofrecen Hola toorecover de capacidad de los datos.

## <a name="troubleshooting-errors"></a>Solución de errores
| Operación | Detalles del error | Resolución |
| --- | --- | --- |
| Cambio de directiva |no se pudo modificar la directiva de copia de seguridad de Hola. Error: error en la operación actual de hello debido a error de servicio interno tooan [0x29834]. Vuelva a intentar operación hello más tarde. Si persiste el problema de hello, póngase en contacto con el soporte técnico de Microsoft. |**Causa:**<br/>Este error se genera cuando está habilitada la configuración de seguridad, intente tooreduce duración de retención por debajo de valores mínimos Hola especificada anteriormente y se encuentra en la versión no admitida (versiones compatibles se especifican en la primera nota de este artículo). <br/>**Acción recomendada:**<br/> En este caso, debe establecer el período de retención por encima de hello mínimo de retención período especificado (siete días para todos los días, cuatro semanas para todas las semanas, tres semanas para mensual o un año para copia anual) tooproceed con directivas relacionadas con las actualizaciones. Si lo desea, método preferente sería el agente de copia de seguridad de tooupdate, servidor de copia de seguridad de Azure o DPM UR tooleverage todas Hola actualizaciones de seguridad. |
| Cambiar la frase de contraseña |El PIN de seguridad escrito no es correcto. (ID.: 100130) Proporcionar toocomplete de PIN de seguridad correcta de hello esta operación. |**Causa:**<br/> Este error se genera cuando se escribe un PIN de seguridad no válido o caducado mientras se realiza una operación crítica (por ejemplo, cambiar la frase de contraseña). <br/>**Acción recomendada:**<br/> operación de hello toocomplete, debe escribir el PIN de seguridad válido. tooget Hola PIN, inicie sesión en el portal de tooAzure y navegar por el almacén de servicios de tooRecovery > Configuración > Propiedades > generar el PIN de seguridad. Use esta frase de contraseña de toochange PIN. |
| Cambiar la frase de contraseña |Error en la operación ID: 120002 |**Causa:**<br/>Este error se genera cuando está habilitada la configuración de seguridad, intente toochange frase de contraseña y se encuentra en la versión no admitida (válidas versiones especificadas en la primera nota de este artículo).<br/>**Acción recomendada:**<br/> frase de contraseña toochange, debe actualizar primero versión del agente de copia de seguridad de toominimum 2.0.9052 mínimo, copia de seguridad de Azure server toominimum, actualización 1 o toominimum DPM, DPM 2012 R2 UR12 o UR2 de 2016 de DPM (vínculos de descarga a continuación), a continuación, escriba el PIN de seguridad válida. tooget Hola PIN, inicie sesión en el portal de tooAzure y navegar por el almacén de servicios de tooRecovery > Configuración > Propiedades > generar el PIN de seguridad. Use esta frase de contraseña de toochange PIN. |

## <a name="next-steps"></a>Pasos siguientes
* [Introducción al almacén de servicios de recuperación de Azure de](backup-azure-vms-first-look-arm.md) tooenable estas características.
* [Descargar agente de servicios de recuperación de Azure más reciente de hello](http://aka.ms/azurebackup_agent) toohelp proteger los equipos de Windows y proteger los datos de copia de seguridad frente a ataques.
* [Descarga Hola servidor más reciente de copia de seguridad de Azure](https://aka.ms/latest_azurebackupserver) toohelp proteger las cargas de trabajo y proteger los datos de copia de seguridad frente a ataques.
* [Descargar UR12 para System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) o [descargar UR2 para System Center 2016 Data Protection Manager](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp proteger las cargas de trabajo y proteger los datos de copia de seguridad frente a ataques.
