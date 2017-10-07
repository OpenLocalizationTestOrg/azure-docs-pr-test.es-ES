---
title: aaaOverview de hello Azure Activity Log | Documentos de Microsoft
description: "Obtenga información acerca de qué hello es el registro de actividad de Azure y cómo puede utilizarlo toounderstand los eventos que se producen en su suscripción de Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Supervisar la actividad de suscripción con hello Azure Activity Log
Hola **Azure Activity Log** es un registro de suscripción que proporciona una visión general de los eventos de nivel de suscripción que se han producido en Azure. Esto incluye una amplia variedad de datos de Azure Resource Manager tooupdates de datos operativos en los eventos de estado del servicio. Hola registro de actividad se conocía anteriormente como "Registros de auditoría" o "Registros operativos," desde eventos de plano de control de informes de hello categoría administrativa para las suscripciones. Gracias a Hola registro de actividad, puede determinar hello ' qué, quién y cuándo ' para las operaciones (PUT, POST, DELETE) realizadas en los recursos de hello en su suscripción de escritura. También puede entender el estado Hola de operación de Hola y otras propiedades relevantes. Hola registro de actividad no incluye las operaciones de lectura (GET) o las operaciones de recursos que utilizan Hola clásico / modelo de "RDFE".

![Comparación de los registros de actividad y otros tipos de registros ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Ilustración 1: Comparación de los registros de actividad y otros tipos de registros

Hello registro de actividad difiere de [registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md). Registros de actividad proporcionan datos sobre las operaciones de hello en un recurso de hello fuera (Hola "plano de control"). Registros de diagnóstico se emiten por un recurso y proporcionan información acerca de la operación de Hola de ese recurso (Hola "plano de datos").

Puede recuperar eventos desde el registro de actividad mediante Hola portal de Azure, CLI, cmdlets de PowerShell y API de REST de Monitor de Azure.


> [!WARNING]
> Hello Azure Activity Log es principalmente para las actividades que se producen en el Administrador de recursos de Azure. No realiza un seguimiento de recursos usando el modelo clásico/RDFE de Hola. Algunos tipos de recursos clásicos tienen un proveedor de recursos de servidor proxy en Azure Resource Manager (por ejemplo, Microsoft.ClassicCompute). Si interactúa con un tipo de recurso de clásico a través de Azure Resource Manager con estos proveedores de recursos de servidor proxy, las operaciones de hello aparecen en hello registro de actividad. Si interactúa con un recurso clásico escriba en el portal clásico de Hola o en caso contrario, fuera de servidores proxy de hello Azure Resource Manager, las acciones sólo se graban en el registro de operaciones de Hola. es accesible sólo en el portal clásico de Hola Hola registro de operaciones.
>
>

Hola de vista siguientes Hola de presentación de vídeo registro de actividad.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Categorías de registro de actividad de Hola
Hola registro de actividad contiene varias categorías de datos. Para obtener detalles completos sobre esquemas de Hola de estas categorías, [consulte este artículo](monitoring-activity-log-schema.md). Entre ellos se incluyen los siguientes:
* **Administrativas** -esta categoría contiene el registro de hello de todos los cree, las operaciones update, delete y acción se realizan a través del Administrador de recursos. Ejemplos de hello tipos de eventos que aparecen en esta categoría se incluyen "creación la máquina virtual" y "eliminación grupo de seguridad de red" cada acción realizada por un usuario o aplicación con el Administrador de recursos se modela como una operación en un tipo de recurso determinado. Si el tipo de operación de hello es escribir, eliminar o acción, registros de Hola de inicio de Hola y el éxito o por error de esa operación se registran en la categoría administrativa Hola. categoría administrativa de Hello también incluye cualquier control de acceso basado en toorole cambios en una suscripción.
* **Estado del servicio** -esta categoría contiene el registro de hello de los incidentes de mantenimiento de servicio que se han producido en Azure. Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "SQL Azure en este de EE. está experimentando tiempos de inactividad". Eventos de estado de servicio vienen en cinco variedades: acción requerida, recuperación asistida, incidente, mantenimiento, información o seguridad y sólo aparece si tiene un recurso de suscripción de Hola que podría verse afectada por los eventos de Hola.
* **Alerta** -esta categoría contiene el registro de hello de todas las activaciones de alertas de Azure. Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "% de CPU en myVM ha sido por encima del 80 para hello últimos 5 minutos". Varios sistemas de Azure tienen un concepto de alerta: puede definir una regla de algún tipo y recibir una notificación cuando las condiciones coincidan con esa regla. Cada vez que un tipo de alerta de Azure compatible "se activa,' o hello las condiciones son toogenerate cumpla una notificación, un registro de la activación de hello también se inserta toothis categoría de hello registro de actividad.
* **Escalado automático** -esta categoría contiene el registro de hello de cualquier operación de toohello relacionados de eventos del motor de escalado automático de hello en función de cualquier configuración de escalado automático que ha definido en su suscripción. Un ejemplo de Hola tipo de evento que aparecen en esta categoría es "Escalado automático ampliación vertical error en la acción". Usar el escalado automático, automáticamente puede escalar horizontalmente o escalar en hello número de instancias de un tipo de recurso compatible se basa en la hora del día y carga datos (métricas) con una configuración de escalado automático. Cuando se cumplen las condiciones de hello tooscale hacia arriba o hacia abajo, inicio de Hola y eventos se ha realizado correctamente o con errores se registran en esta categoría.
* **Recomendación**: esta categoría contiene eventos de recomendación de determinados tipos de recursos, como sitios web y servidores SQL Server. Estos eventos ofrecen recomendaciones para cómo toobetter utilizar los recursos. Solo recibirá eventos de este tipo si dispone de recursos que emitan recomendaciones.
* **Directiva, Seguridad y Estado de los recursos**: estas categorías no contienen ningún evento; están reservadas para un uso futuro.

## <a name="event-schema-per-category"></a>Esquema de eventos por categoría
[Vea este esquema de eventos de registro de actividad de artículo toounderstand Hola por categoría.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>¿Qué puede hacer con hello registro de actividad
Estas son algunas cosas de Hola que puede hacer con hello registro de actividad:

![Registro de actividad de Azure](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Consultar y ver en hello **portal de Azure**.
* [Crear una alerta basada en un evento de Activity Log.](monitoring-activity-log-alerts.md)
* [Transmitir tooan **concentrador de eventos** ](monitoring-stream-activity-logs-event-hubs.md) para ingesta por un servicio de otro fabricante o una solución de análisis personalizada como Power BI.
* Analizar en Power BI con hello [ **paquete de contenido de Power BI**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Guardar tooa **cuenta de almacenamiento** para la inspección de archivado o manual](monitoring-archive-activity-log.md). Puede especificar el tiempo de retención de hello (en días) con hello **perfil del registro**.
* Consultarlo mediante un cmdlet de PowerShell, la CLI o la API de REST.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Consultar el registro de actividad de Hola Hola portal de Azure
Dentro de hello portal de Azure puede ver el registro de actividad en varios lugares:
* Hola **hoja de registro de actividad**, que se puede acceder mediante la búsqueda de hello registro de actividad en "Más Services" en el panel de navegación izquierdo de Hola.
* Hola **hoja Monitor**, que aparece de forma predeterminada en el panel de navegación izquierdo de Hola. Hola registro de actividad es una sección de esta hoja de Monitor de Azure.
* Cualquier recurso **hoja de recursos**, por ejemplo, hoja de configuración de Hola para una máquina Virtual. Hola registro de actividad es sea una de las secciones de hello en la mayoría de estos módulos de recursos, y haga clic en ella automáticamente filtra los eventos de hello toothose relacionados con los recursos específicos de toothat.

Hola portal de Azure, puede filtrar el registro de actividad por estos campos:
* TimeSpan - Hola inicio y finalización de tiempo para los eventos.
* Categoría - categoría de eventos de hello como se describió anteriormente.
* Suscripción: uno o más nombres de suscripción de Azure.
* Grupo de recursos: uno o más grupos de recursos dentro de esas suscripciones.
* Resource (name): nombre del saludo de un recurso específico.
* Tipo de recurso - tipo de Hola de recurso, por ejemplo, Microsoft.Compute/virtualmachines.
* Nombre de operación: nombre de Hola de una operación de Azure Resource Manager, por ejemplo, Microsoft.SQL/servers/Write.
* Gravedad: nivel de gravedad de Hola de evento hello (informativo, advertencia, Error, crítico).
* Evento iniciado por - llamador' hello' o el usuario que realizó la operación de Hola.
* Abrir búsqueda: se trata de un cuadro de búsqueda de texto abierto que busca esa cadena en todos los campos de todos los eventos.

Una vez haya definido un conjunto de filtros, puede guardarlo como una consulta que se conserva entre sesiones, si alguna vez necesitas tooperform Hola misma consulta con los filtros aplicados nuevo en hello futuras. También puede anclar mantener la consulta tooyour panel Azure tooalways un ojo según determinados eventos.

Al hacer clic en "Aplicar" se ejecuta la consulta y se muestran todos los eventos que coinciden. Al hacer clic en cualquier evento de muestra de lista Hola Hola resumen de ese evento, así como Hola completa sin formato JSON de ese evento.

Incluso más energía, puede hacer clic en hello **Log Search** icono, que muestra los datos de registro de actividad de hello [soluciones de análisis de registro de actividad de análisis de registros](../log-analytics/log-analytics-activity.md). hoja de registro de actividad de Hola ofrece una experiencia de exploración/filtro básico en registros, pero habilita el análisis de registros toopivot, consultar y visualizar los datos de las maneras más eficaces.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Exportar registro de actividad con un perfil de registro de hello
Un **perfil de registro** controla cómo se exporta el registro de actividad. Con un perfil de registro, puede configurar:

* Dónde se debería enviar Hola registro de actividad (cuenta de almacenamiento o concentradores de eventos)
* Qué categorías de eventos (Escritura, Eliminación, Acción) se deberían enviar. *Hola significado de "categoría" en los perfiles de registro y eventos del registro de actividad es diferente. En el perfil de registro de hello, "Categoría" representa el tipo de operación de hello (acción de escritura, eliminación,). En un evento de registro de actividad, propiedad de "categoría" hello representa el origen de Hola o tipo de evento (por ejemplo, administración, ServiceHealth, alerta etc.).*
* Qué regiones (ubicaciones) se deben exportar. Asegúrese de tooinclude seguro "global", ya que muchos eventos en el registro de actividad de Hola son los eventos globales.
* ¿Durante cuánto tiempo se debe conservar Hola registro de actividad en una cuenta de almacenamiento.
    - Una retención de cero días significa que los registros se conservan de forma indefinida. En caso contrario, valor de hello puede ser cualquier número de días comprendido entre 1 y 2147483647.
    - Si se han establecido directivas de retención pero almacenar los registros en una cuenta de almacenamiento está deshabilitada (por ejemplo, si solo se seleccionan las opciones de los centros de eventos o OMS), las directivas de retención de hello no tienen ningún efecto.
    - Las directivas de retención aplicada por día, por lo que en hello final de un día (UTC), los registros de día de Hola que es ahora más allá de la directiva de retención de Hola se eliminan. Por ejemplo, si tuviera una directiva de retención de un día, en principio de Hola de hoy día de Hola Hola registros de hello anteayer se eliminarán.

Puede usar una cuenta de almacenamiento o espacio de nombres de concentrador de eventos que no esté en Hola misma suscripción como Hola una emisión de registros. usuario de Hola que configura los valores de hello debe tener las suscripciones tooboth de acceso correspondientes RBAC Hola.

Estas opciones se pueden configurar a través de la opción de "Exportación" hello en la hoja de registro de actividad de hello en el portal de Hola. También se puede configurar mediante programación [utilizando Hola API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931927.aspx), cmdlets de PowerShell o CLI. Una suscripción solo puede tener un perfil de registro.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Configurar perfiles de registro mediante Hola portal de Azure
Puede transmitir por secuencias tooan de registro de actividad de hello concentrador de eventos o almacenarlas en una cuenta de almacenamiento mediante el uso de opción de "Exportación" Hola Hola portal de Azure.

1. Navegue toohello **registro de actividad** hoja con menú de hello en hello izquierda del portal de Hola.

    ![Navegue tooActivity registro en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Haga clic en hello **exportar** situado en la parte superior de Hola de hoja de Hola.

    ![Botón Exportar en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. En la hoja de Hola que aparece, puede seleccionar:  
  * regiones que le gustaría tooexport eventos
  * Hola toowhich cuenta de almacenamiento que le gustaría toosave eventos
  * número de Hola de días que desea tooretain estos eventos en el almacenamiento. Un valor de 0 días conserva los registros de Hola para siempre.
  * Namespace de Bus de servicio de Hello en el que desea una toobe de concentrador de eventos creado para la transmisión por secuencias estos eventos.

     ![Exportar en hoja de registro de actividad](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Haga clic en **guardar** toosave esta configuración. configuración de Hello inmediatamente se pueden suscripción tooyour aplicada.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Configurar perfiles de registro mediante Hola Cmdlets de PowerShell de Azure
#### <a name="get-existing-log-profile"></a>Obtención del perfil de registro existente
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Incorporación de un perfil de registro
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Propiedad | Obligatorio | Description |
| --- | --- | --- |
| Nombre |Sí |Nombre de su perfil de registro. |
| StorageAccountId |No |Se debe guardar el Id. de recurso de hello toowhich de cuenta de almacenamiento Hola registro de actividad. |
| serviceBusRuleId |No |Id. de regla de Bus de servicio para el espacio de nombres de Bus de servicio de hello le gustaría creados en los centros de eventos toohave. Es una cadena con este formato: `{service bus resource ID}/authorizationrules/{key name}`. |
| Ubicaciones |Sí |Lista separada por comas de regiones que le gustaría toocollect eventos de registro de actividad. |
| RetentionInDays |Sí |Número de días que deben retenerse los eventos, entre 1 y 2147483647. Un valor de cero almacena los registros de hello indefinidamente (indefinidamente). |
| Categorías |No |Lista separada por comas de las categorías de eventos que deben recopilarse. Los valores posibles son Write, Delete y Action. |

#### <a name="remove-a-log-profile"></a>Eliminación de un perfil de registro
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Configurar perfiles de registro mediante hello Azure multiplataforma CLI
#### <a name="get-existing-log-profile"></a>Obtención del perfil de registro existente
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Hola `name` propiedad debe ser el nombre de Hola de su perfil de registro.

#### <a name="add-a-log-profile"></a>Incorporación de un perfil de registro
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Propiedad | Obligatorio | Description |
| --- | --- | --- |
| name |Sí |Nombre de su perfil de registro. |
| storageId |No |Se debe guardar el Id. de recurso de hello toowhich de cuenta de almacenamiento Hola registro de actividad. |
| serviceBusRuleId |No |Id. de regla de Bus de servicio para el espacio de nombres de Bus de servicio de hello le gustaría creados en los centros de eventos toohave. Es una cadena con este formato: `{service bus resource ID}/authorizationrules/{key name}`. |
| Ubicaciones |Sí |Lista separada por comas de regiones que le gustaría toocollect eventos de registro de actividad. |
| RetentionInDays |Sí |Número de días que deben retenerse los eventos, entre 1 y 2147483647. Un valor de cero almacena los registros de hello indefinidamente (indefinidamente). |
| Categorías |No |Lista separada por comas de las categorías de eventos que deben recopilarse. Los valores posibles son Write, Delete y Action. |

#### <a name="remove-a-log-profile"></a>Eliminación de perfil de registro
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola registro de actividad (anteriormente registros de auditoría)](../azure-resource-manager/resource-group-audit.md)
* [Transmitir hello Azure Activity Log tooEvent centros](monitoring-stream-activity-logs-event-hubs.md)
