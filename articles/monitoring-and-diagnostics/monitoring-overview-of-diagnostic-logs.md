---
title: "aaaOverview de registros de diagnóstico de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué son los registros de diagnóstico de Azure y cómo puede usarlos toounderstand los eventos que se producen en un recurso de Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Recopile y use los datos de registro provenientes de los recursos de Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>Qué son los registros de diagnóstico de Azure
**Registros de diagnóstico de nivel de recurso de Azure** son registros emitidos por un recurso que proporcionan datos enriquecidos y frecuentes acerca de la operación de Hola de ese recurso. contenido de Hola de estos registros varía según el tipo de recurso. Por ejemplo, los contadores de regla de grupo de seguridad de red y las auditorías de Key Vault son dos categorías de registros de recursos.

Registros de diagnóstico de nivel de recursos se diferencian hello [registro de actividad](monitoring-overview-activity-logs.md). Hola registro de actividad proporciona una visión general de las operaciones de Hola que se realizaron en los recursos de la suscripción con el Administrador de recursos, por ejemplo, crear una máquina virtual o eliminar una aplicación de lógica. Hola registro de actividad es un registro de nivel de suscripción. Los registros de diagnóstico de nivel de recursos proporcionan una visión general de las operaciones realizadas dentro del mismo recurso, por ejemplo, obtener un secreto de un almacén de claves.

Los registros de diagnóstico de nivel de recursos también difieren de los registros de diagnóstico de nivel de sistema operativo invitado. Estos son los recopilados por un agente que se ejecuta dentro de una máquina virtual u otro tipo de recurso admitido. Registros de diagnóstico de nivel de recursos no requieren ningún dato específico del recurso de agente y capturar de hello plataforma Windows Azure, mientras que los registros de diagnóstico de nivel de sistema operativo invitado capturan datos de sistema operativo de Hola y aplicaciones que se ejecutan en una máquina virtual.

No todos los recursos admiten Hola nuevo tipo de registros de diagnóstico de recursos que se describen aquí. Este artículo contiene una lista de la sección Qué tipos de recursos admiten registros de diagnóstico de nivel de recurso nuevo Hola.

![Comparación de los registros de diagnóstico de recursos y otros tipos de registros ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Qué se puede hacer con los registros de diagnóstico de nivel de recursos
Estas son algunas cosas de Hola que puede hacer con los registros de diagnóstico de recursos:

![Ubicación lógica de los registros de diagnóstico de recursos](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Guardarlos tooa [ **cuenta de almacenamiento** ](monitoring-archive-diagnostic-logs.md) para la inspección de auditoría o manual. Puede especificar el tiempo (en días) de retención de hello mediante **configuración de diagnóstico de recurso**.
* [Transmitirlos demasiado**centros de eventos** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) para ingesta por un servicio de otro fabricante o una solución de análisis personalizada como Power BI.
* Analizarlos con [Log Analytics de OMS](../log-analytics/log-analytics-azure-storage.md)

Puede usar una cuenta de almacenamiento o espacio de nombres de los centros de eventos que no esté en Hola misma suscripción como Hola una emisión de registros. usuario de Hola que configura los valores de hello debe tener las suscripciones tooboth de acceso correspondientes RBAC Hola.

## <a name="resource-diagnostic-settings"></a>Configuración de diagnóstico de recursos
Los registros de diagnóstico de recursos para recursos que no son de proceso se configuran mediante la configuración de diagnóstico de recursos. **Configuración de diagnóstico de recursos** para un control de recursos:

* Dónde se envían los registros de diagnóstico y las métricas (cuenta de almacenamiento, Event Hubs o Log Analytics de OMS).
* Qué categorías de registro se envían y si se envían también datos de métrica.
* Cuánto tiempo se debe conservar cada categoría de registro en una cuenta de almacenamiento
    - Una retención de cero días significa que los registros se conservan de forma indefinida. En caso contrario, valor de hello puede ser cualquier número de días comprendido entre 1 y 2147483647.
    - Si se han establecido directivas de retención pero almacenar los registros en una cuenta de almacenamiento está deshabilitada (por ejemplo, si solo se seleccionan las opciones de los centros de eventos o OMS), las directivas de retención de hello no tienen ningún efecto.
    - Las directivas de retención aplicada por día, por lo que en hello final de un día (UTC), los registros de día de Hola que es ahora más allá de la directiva de retención de Hola se eliminan. Por ejemplo, si tuviera una directiva de retención de un día, en principio de Hola de hoy día de Hola Hola registros de hello anteayer se eliminarán.

Estas opciones se configuran fácilmente a través de la configuración de diagnóstico de Hola para un recurso en hello portal de Azure, a través de los comandos de PowerShell de Azure y la CLI o hello [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Registros de diagnóstico y las métricas para de capa de SO invitado de Hola de uso de recursos (por ejemplo, las máquinas virtuales o Service Fabric) de proceso [un mecanismo independiente para la configuración y selección de salidas](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>¿Cómo tooenable colección de registros de diagnóstico de recursos
Recopilación de registros de diagnóstico de recursos se puede habilitar [como parte de la creación de un recurso en una plantilla de administrador de recursos](./monitoring-enable-diagnostic-logs-using-template.md) o después de que se crea un recurso de página de ese recurso en el portal de Hola. También puede habilitar la recopilación en cualquier momento mediante comandos de Azure PowerShell o CLI o con hello API de REST de Monitor de Azure.

> [!TIP]
> Estas instrucciones no pueden aplicar directamente tooevery recurso. Vea los vínculos de esquema de hello en parte inferior de Hola de este paso especial de toounderstand de página que se pueden aplicar a tipos de recursos de toocertain.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Habilitar la recopilación de registros de diagnóstico de recursos en el portal de Hola
Puede habilitar la recopilación de registros de diagnóstico de recursos de hello Azure portal después de que se ha creado un recurso por recurso específico tooa va o navegando tooAzure Monitor. tooenable esto a través del Monitor de Azure:

1. Hola [portal de Azure](http://portal.azure.com), desplácese tooAzure Monitor y haga clic en **configuración de diagnóstico**

    ![Sección de supervisión de Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Si lo desea Hola lista Filtrar por tipo de recurso o grupo de recursos, a continuación, haga clic en el recurso de hello para el que le gustaría tooset una configuración de diagnóstico.

3. Si ninguna configuración existe en el recurso de Hola que ha seleccionado, son toocreate solicitada una configuración. Haga clic en "Activar diagnóstico".

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   Si hay una configuración existente en el recurso de hello, verá una lista de configuraciones ya configurado en este recurso. Haga clic en "Agregar configuración de diagnóstico".

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Asigne un nombre de su configuración, Hola casillas para cada toowhich de destino que desee toosend datos y configurar el recurso que se utiliza para cada destino. También puede establecer un número de días tooretain estos registros mediante el uso de hello **retención (días)** controles deslizantes (sólo aplicable toohello almacenamiento cuenta de destino). Una retención de cero días almacena los registros de hello indefinidamente.
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Haga clic en **Guardar**.

Transcurridos unos instantes, Hola nueva opción aparece en la lista de valores para este recurso, y registros de diagnóstico se envían toohello especifica destinos tan pronto como los nuevos datos de evento se generan.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Habilitación de la recopilación de registros de diagnóstico de recursos mediante PowerShell
colección de tooenable de registros de diagnóstico de recursos a través de PowerShell de Azure, Hola de uso siguientes comandos:

tooenable almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

identificador de cuenta de almacenamiento de Hola Hola Id. de recurso para los registros de hello almacenamiento cuenta toowhich desea toosend Hola de.

tooenable transmisión por secuencias de concentrador de eventos de registros de diagnóstico tooan, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

Identificador de regla de bus de servicio de Hello es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

enviar tooenable del área de trabajo de análisis de registros de tooa registros de diagnóstico, use este comando:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Puede obtener Id. de recurso de Hola de su área de trabajo de análisis de registros mediante Hola siguiente comando:

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Puede combinar estos parámetros tooenable varias opciones de salida.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Habilitación de la recopilación de registros de diagnóstico de recursos mediante la CLI
tooenable colección de registros de diagnóstico de recursos a través de hello CLI de Azure, use Hola siguientes comandos:

tooenable almacenamiento de registros de diagnóstico en una cuenta de almacenamiento, use este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

identificador de cuenta de almacenamiento de Hola Hola Id. de recurso para los registros de hello almacenamiento cuenta toowhich desea toosend Hola de.

tooenable transmisión por secuencias de concentrador de eventos de registros de diagnóstico tooan, use este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

Identificador de regla de bus de servicio de Hello es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.

enviar tooenable del área de trabajo de análisis de registros de tooa registros de diagnóstico, use este comando:

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Puede combinar estos parámetros tooenable varias opciones de salida.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Habilitación de la recopilación de registros de diagnóstico de recursos mediante la API de REST
configuración de diagnóstico de toochange con hello API de REST de Monitor de Azure, consulte [este documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Administrar la configuración de diagnóstico de recursos en el portal de Hola
Asegúrese de que todos los recursos estén instalados con la configuración de diagnóstico. Navegue demasiado**Monitor** Hola portal y abra **configuración de diagnóstico**.

![Hoja de registros de diagnóstico en el portal de Hola](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Puede que tenga tooclick "más sección"servicios de toofind Hola Monitor.

Aquí puede ver y filtrar todos los recursos que admiten la configuración de diagnóstico toosee si tienen los diagnósticos están habilitados. También puede explorar en profundidad toosee si se establecen varias opciones de configuración en un recurso y compruebe qué cuenta de almacenamiento, el espacio de nombres de los centros de eventos o el área de trabajo de análisis de registros que se transmiten datos a.

![Resultados de los registros de diagnóstico en el portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Agregar que una configuración de diagnóstico, se abrirá Hola vista de configuración de diagnóstico, donde puede habilitar, deshabilitar o modificar la configuración de diagnóstico para hello recurso seleccionado.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Servicios admitidos, categorías y esquemas para los registros de diagnóstico de recursos
[Consulte este artículo](monitoring-diagnostic-logs-schema.md) para obtener una lista completa de los esquemas utilizados por los servicios y las categorías de registro de hello y servicios compatibles.

## <a name="next-steps"></a>Pasos siguientes

* [Registros de diagnóstico de recursos de secuencia demasiado**centros de eventos**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Cambiar la configuración de diagnóstico de recursos mediante Hola API de REST de Monitor de Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Análisis de registros desde Azure Storage con Log Analytics](../log-analytics/log-analytics-azure-storage.md)
