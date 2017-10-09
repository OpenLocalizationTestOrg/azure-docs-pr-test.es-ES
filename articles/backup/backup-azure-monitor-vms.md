---
title: "las copias de seguridad implementado por el Administrador de recursos de máquina virtual de aaaMonitor | Documentos de Microsoft"
description: "Supervise eventos y alertas de copias de seguridad de máquinas virtuales implementadas por Resource Manager. Envíe correo electrónico basado en alertas."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Supervisión de alertas de copias de seguridad de máquinas virtuales de Azure
Las alertas son las respuestas del servicio de Hola que se alcanza o superado un umbral de evento. Saber cuándo problemas inicio puede tookeeping crítico costos empresariales hacia abajo. Normalmente no se produzcan alertas según una programación y, por lo que resulta útil tooknow tan pronto como sea posible después de que se produzcan alertas. Por ejemplo, cuando se produce un error en un trabajo de copia de seguridad o restauración, se produce una alerta con cinco minutos de error de Hola. En el panel de almacén de hello, Hola icono de alertas de copia de seguridad muestra eventos críticos y de nivel de advertencia. En configuración de alertas de copia de seguridad de hello, puede ver todos los eventos. Pero, ¿qué hacer si se produce una alerta cuando está trabajando en otro asunto? Si no sabe cuando se produce la alerta de hello, podría ser una molestias secundarias o pudieron poner en peligro datos. Cuando esto ocurre, toomake seguro personas adecuadas de hello están al corriente de una alerta - configurar Hola servicio toosend las notificaciones de alerta por correo electrónico. Para más información acerca de cómo configurar las notificaciones por correo electrónico, consulte [Configuración de notificaciones](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>¿Cómo se puede encontrar información acerca de las alertas de hello?
tooview información sobre eventos de Hola que generó una alerta, debe abrir la hoja de alertas de copia de seguridad de Hola. Hay dos hoja de alertas de copia de seguridad de Hola de tooopen maneras: desde Hola icono Alerts de copia de seguridad en el panel del almacén de Hola o de hoja de alertas y eventos de Hola.

icono hoja de alertas de copia de seguridad de hello tooopen de alertas de copia de seguridad:

* En hello **alertas de copia de seguridad** icono Panel de almacén de hello, haga clic en **crítico** o **advertencia** tooview Hola eventos operativos para ese nivel de gravedad.

    ![Icono Alertas de copias de seguridad](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

hoja de alertas de copia de seguridad de hello tooopen de hoja de alertas y eventos de hello:

1. En el panel de almacén de hello, haga clic en **toda la configuración de**. ![Botón Toda la configuración](./media/backup-azure-monitor-vms/all-settings-button.png)
2. En hello **configuración** hoja, haga clic en **alertas y eventos**. ![Botón Alertas y eventos](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. En hello **alertas y eventos** hoja, haga clic en **alertas de copia de seguridad**. ![Botón Alertas de copias de seguridad](./media/backup-azure-monitor-vms/backup-alerts.png)

    Hola **alertas de copia de seguridad** hoja se abre y muestra Hola alertas filtradas.

    ![Icono Alertas de copias de seguridad](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview obtener información detallada sobre una alerta determinada, en lista de Hola de eventos, haga clic en hello alerta tooopen su **detalles** hoja.

    ![Detalle de evento](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    atributos de hello toocustomize mostrados en la lista hello, consulte [ver atributos de evento adicionales](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Configuración de notificaciones
 Puede configurar notificaciones de correo electrónico toosend Hola de servicio para las alertas de hello ocurrido a lo largo hello más allá de la hora, o cuando se producen determinados tipos de eventos.

tooset configurar notificaciones de correo electrónico para alertas

1. En el menú de las alertas de copia de seguridad de hello, haga clic en **configurar notificaciones**

    ![Menú Alertas de copias de seguridad](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    se abre la hoja de Hello configurar notificaciones.

    ![Hoja Configurar notificaciones](./media/backup-azure-monitor-vms/configure-notifications.png)
2. En la hoja de notificaciones configurar hello, para las notificaciones de correo electrónico, haga clic en **en**.

    Hola destinatarios y cuadros de diálogo de gravedad tienen una estrella toothem siguiente porque se necesita esa información. Proporcione al menos una dirección de correo electrónico y seleccione al menos un nivel de gravedad.
3. Hola **destinatarios (correo electrónico)** cuadro de diálogo, tipo hello direcciones de correo electrónico que reciba notificaciones de Hola. Usar el formato de hello: username@domainname.com. Separe varias direcciones de correo electrónico con un signo de punto y coma (;).
4. Hola **notificar** área, elija **por alerta** toosend notificación cuando hello especificado se produzca la alerta, o **implícita por hora** toosend un resumen de hello última hora.
5. Hola **gravedad** cuadro de diálogo, elija uno o más niveles que desea tootrigger notificación por correo electrónico.
6. Haga clic en **Guardar**.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Tipos de alerta disponibles para la copia de seguridad de máquinas virtuales de IaaS de Azure
   | Nivel de alerta | Alertas enviadas |
   | --- | --- |
   | Crítico |Error de copia de seguridad, error de recuperación |
   | Advertencia |None |
   | Informativo |None |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>¿Existen situaciones en las que no se envía ningún correo electrónico incluso si las notificaciones se configuran?
Hay situaciones donde no se envía una alerta, incluso aunque las notificaciones de Hola se han configurado correctamente. Hola notificaciones de correo electrónico de las situaciones siguientes no se envían tooavoid alerta ruido:

* Si las notificaciones están configurada tooHourly implícita, y una alerta se genera y resuelto durante la hora de Hola.
* Hola trabajos se cancelan.
* Se desencadena un trabajo de copia de seguridad y, a continuación, se produce un error y otro trabajo de copia de seguridad está en curso.
* Inicia un trabajo de copia de seguridad programado para una máquina virtual habilitada para el Administrador de recursos, pero Hola VM ya no existe.

## <a name="customize-your-view-of-events"></a>Personalización de la vista de eventos
Hola **registros de auditoría** configuración incluye un conjunto predefinido de filtros y las columnas que muestra información de eventos operativos. Puede personalizar la vista de Hola para que cuando Hola **eventos** hoja se abre, muestra Hola información que desee.

1. Hola [panel almacén](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), haga clic en tooand de examinar **los registros de auditoría** tooopen Hola **eventos** hoja.

    ![Registros de auditoría](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hola **eventos** hoja abre toohello eventos operativos filtrados solo para el almacén actual Hola.

    ![Filtro Registros de auditoría](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    hoja de Hello muestra la lista de Hola de crítico, Error, advertencia e informativos eventos ocurridos en hello semana pasada. intervalo de tiempo Hello es un valor predeterminado establecido en hello **filtro**. Hola **eventos** hoja también muestra un gráfico de barra de seguimiento cuando se han producido eventos de Hola. Si no desea toosee Hola gráfico de barras, hello **eventos** menú, haga clic en **Ocultar gráfico** tootoggle desactivar gráfico Hola. vista predeterminada de Hola de eventos muestra información de operación, nivel, estado, recursos y tiempo. Para obtener información acerca de cómo exponer atributos de evento adicionales, consulte la sección hello [expandiendo la información del evento](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Para obtener información adicional sobre un evento operativo, Hola **operación** columna, haga clic en un evento operativo tooopen su hoja. hoja de Hello contiene información detallada acerca de los eventos de Hola. Eventos se agrupan por su identificador de correlación y una lista de eventos de Hola que se produjeron en el intervalo de tiempo de Hola.

    ![Detalles de la operación](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview obtener información detallada acerca de un evento concreto, desde la lista de Hola de eventos, haga clic en hello eventos tooopen su **detalles** hoja.

    ![Detalle de evento](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    información de nivel de evento de Hello es tan detallada como Hola obtiene información. Si prefiere ver este proporciona mucha información sobre cada evento y desea que tooadd esto mucho detalle toohello **eventos** hoja, consulte la sección de hello [expandiendo la información del evento](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Personalizar el filtro de eventos de Hola
Hola de uso **filtro** tooadjust o elija la información de Hola que aparece en un módulo determinado. información de eventos de Hola toofilter:

1. Hola [panel almacén](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), haga clic en tooand de examinar **los registros de auditoría** tooopen Hola **eventos** hoja.

    ![Registros de auditoría](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Hola **eventos** hoja abre toohello eventos operativos filtrados solo para el almacén actual Hola.

    ![Filtro Registros de auditoría](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. En hello **eventos** menú, haga clic en **filtro** tooopen esa hoja.

    ![Hoja de filtro abierta](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. En hello **filtro** hoja, ajustar hello **nivel**, **intervalo de tiempo**, y **llamador** filtros. Hello otros filtros no están disponibles desde que se establecieron información actual de tooprovide hello para el almacén de servicios de recuperación de Hola.

    ![Registros de auditoria: detalles de la consulta](./media/backup-azure-monitor-vms/filter-blade.png)

    Puede especificar hello **nivel** de evento: crítico, Error, advertencia o informativa. Puede elegir cualquier combinación de niveles de evento, pero debe tener al menos uno seleccionado. Hola nivel activar o desactivar. Hola **intervalo de tiempo** filtro le permite toospecify Hola período de tiempo para capturar eventos. Si utiliza un intervalo de tiempo personalizado, puede establecer Hola inicio y finalización.
4. Una vez que esté listo tooquery Hola operaciones registros con el filtro, haga clic en **actualización**. mostrarán resultados de Hola Hola **eventos** hoja.

    ![Detalles de la operación](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Visualización de atributos adicionales de eventos
Con hello **columnas** botón, puede habilitar eventos adicionales atributos tooappear en lista Hola Hola **eventos** hoja. lista predeterminada de Hola de eventos muestra información de operación, nivel, estado, recursos y tiempo. tooenable atributos adicionales:

1. En hello **eventos** hoja, haga clic en **columnas**.

    ![Abrir columnas](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Hola **Elegir columnas** abre la hoja.

    ![Hoja Columnas](./media/backup-azure-monitor-vms/columns-blade.png)
2. Hola tooselect atributo, haga clic en la casilla de verificación de Hola. Hola atributo casilla se activa y desactiva.
3. Haga clic en **restablecer** tooreset lista de Hola de atributos en hello **eventos** hoja. Después de agregar o quitar atributos de lista de hello, utilice **restablecer** nueva lista de atributos de evento de Hola de tooview.
4. Haga clic en **actualización** tooupdate datos de hello en los atributos de evento de Hola. Hello en la tabla siguiente proporciona información acerca de cada atributo.

| Nombre de la columna | Description |
| --- | --- |
| Operación |nombre de Hola de operación de Hola |
| Nivel |Hola a nivel de operación de hello, los valores pueden ser: informativo, advertencia, Error o crítico |
| Estado |Descriptivo estado de operación de Hola |
| Recurso |Dirección URL que identifica el recurso de hello; también conocido como Id. de recurso de Hola |
| Hora |Tiempo, medido desde Hola hora actual, cuando se produjo el evento de Hola |
| Autor de llamada |Quién o qué llama o desencadenó el evento de hello; puede ser sistema hello, o un usuario |
| Timestamp |tiempo de Hello cuando se activó el evento de Hola |
| Grupo de recursos |grupo de recursos asociado de Hola |
| Tipo de recurso |tipo de recurso interno de Hello utilizada por el Administrador de recursos |
| Id. de suscripción |Hola asociación del Id. de suscripción |
| Categoría |Categoría de evento de Hola |
| Id. de correlación |Identificador común para eventos relacionados |

## <a name="use-powershell-toocustomize-alerts"></a>Usar PowerShell toocustomize alertas
Puede obtener las notificaciones de alerta personalizadas para los trabajos de hello en el portal de Hola. tooget estos trabajos, definir reglas en hello operativa registra eventos de alerta basada en PowerShell. Use *PowerShell versión 1.3.0 o posterior*.

toodefine un tooalert de notificación personalizada para errores de copia de seguridad, use un comando como Hola siguiente secuencia de comandos:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** : puede obtener ResourceId de hello los registros de auditoría. Hola ResourceId es una dirección URL proporcionada en la columna de recurso de Hola de registros de operaciones de Hola.

**OperationName** : OperationName está en formato de Hola "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" donde *EventName* puede ser:<br/>

* Registro <br/>
* Unregister  <br/>
* ConfigureProtection  <br/>
* Backup  <br/>
* Restore  <br/>
* StopProtection  <br/>
* DeleteBackupData  <br/>
* CreateProtectionPolicy  <br/>
* DeleteProtectionPolicy  <br/>
* UpdateProtectionPolicy  <br/>

**Status** : los valores admitidos son: Started, Succeeded o Failed.

**ResourceGroup** : se trata de hello pertenece toowhich Hola recurso de grupo de recursos. Puede agregar la columna toohello genera registros de hello grupo de recursos. Grupo de recursos es uno de los tipos disponibles de Hola de información de eventos.

**Nombre** : nombre de regla de alerta de Hola.

**CustomEmail** : especificar toowhich de dirección de correo electrónico personalizada hello desea toosend una notificación de alerta

**SendToServiceOwners** : esta opción envía los administradores de tooall de notificaciones de alerta y los coadministradores tienen permisos de suscripción de Hola. Se puede utilizar en el cmdlet **New-AzureRmAlertRuleEmail** .

### <a name="limitations-on-alerts"></a>Limitaciones de las alertas
Alertas basadas en eventos son toohello asunto siguientes limitaciones:

1. Las alertas se activan en todas las máquinas virtuales en hello que del almacén de servicios de recuperación. No se puede personalizar la alerta de Hola para un subconjunto de máquinas virtuales en un almacén de servicios de recuperación.
2. Esta característica se encuentra en versión preliminar. [Más información](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Las alertas se envían desde "alerts-noreply@mail.windowsazure.com". Actualmente no se puede modificar el remitente del correo electrónico de Hola.

## <a name="next-steps"></a>Pasos siguientes
Registros de eventos Habilitar evaluación excelente y compatibilidad para las operaciones de copia de seguridad de Hola de auditoría. se registra Hello las siguientes operaciones:

* Registro
* Unregister 
* Configuración de protección
* Copia de seguridad (tanto programada como a petición)
* Restore 
* Detener protección
* Eliminación de datos de copia de seguridad
* Add policy
* Eliminación de directiva
* Actualización de directiva
* Cancelar trabajo

Para obtener una explicación amplia de eventos, las operaciones y los registros de auditoría a través de hello servicios de Azure, vea el artículo de hello [ver eventos y registros de auditoría](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Para información sobre cómo volver a crear una máquina virtual a partir de un punto de recuperación, consulte [Restauración de máquinas virtuales en Azure](backup-azure-restore-vms.md). Si necesita información sobre la protección de las máquinas virtuales, consulte [primer vistazo: copia de seguridad del almacén de servicios de recuperación de tooa de máquinas virtuales](backup-azure-vms-first-look-arm.md). Obtenga información acerca de las tareas de administración de Hola para copias de seguridad de máquina virtual en el artículo de hello, [copias de seguridad de máquina virtual de Azure administrar](backup-azure-manage-vms.md).
