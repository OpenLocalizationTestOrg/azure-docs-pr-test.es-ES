---
title: aaaMonitor y administrar las canalizaciones mediante hello portal de Azure y PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola portal de Azure y Azure PowerShell toomonitor y administrar factorías de datos de Azure de Hola y las canalizaciones que haya creado."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Supervisar y administrar las canalizaciones de factoría de datos de Azure mediante Hola portal de Azure y PowerShell
> [!div class="op_single_selector"]
> * [Uso de Azure Portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Uso de la aplicación de supervisión y administración](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> aplicación de administración y supervisión de Hello proporciona una mejor compatibilidad para supervisar y administrar sus canalizaciones de datos y solucionar los problemas. Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md). 


Este artículo describe cómo administrar toomonitor y depurar las canalizaciones mediante el portal de Azure y PowerShell. Hello artículo también proporciona información acerca de cómo toocreate alertas y obtener notificaciones acerca de los errores.

## <a name="understand-pipelines-and-activity-states"></a>Descripción de las canalizaciones y los estados de actividad
Mediante el uso de hello portal de Azure, hacer lo siguiente:

* Ver una factoría de datos como un diagrama.
* Ver las actividades en una canalización.
* Ver conjuntos de datos de entrada y salida.

Esta sección también describe cómo un segmento del conjunto de datos realiza la transición de estado de un estado tooanother.   

### <a name="navigate-tooyour-data-factory"></a>Navegue tooyour factoría de datos
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **factorías de datos** en menú Hola Hola izquierda. Si no lo ve, haga clic en **más servicios >**y, a continuación, haga clic en **factorías de datos** en hello **INTELLIGENCE + análisis** categoría.

   ![Examinar todo -> Factorías de datos](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. En hello **factorías de datos** hoja, factoría de datos seleccione Hola que le interesa.

    ![Selección de la factoría de datos](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Debería ver la página principal de Hola de factoría de datos de Hola.

   ![Hoja Factoría de datos](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Vista de diagrama de la factoría de datos
Hola **diagrama** vista de una factoría de datos proporciona un único panel de vidrio toomonitor y administrar la factoría de datos de Hola y de sus activos. Hola toosee **diagrama** ver de la factoría de datos, haga clic en **diagrama** en la portada de Hola de factoría de datos de Hola.

![Vista de diagrama](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

Puede acercar, alejar, zoom toofit, zoom too100%, diseño de Hola de bloqueo del diagrama de Hola y automáticamente Posicione canalizaciones y los conjuntos de datos. También puede ver información de linaje de datos de hello (es decir, mostrar los elementos que preceden y siguen en la cadena de los elementos seleccionados).

### <a name="activities-inside-a-pipeline"></a>Actividades en una canalización
1. Haga clic en canalización hello y, a continuación, haga clic en **canalización abierto** toosee todas las actividades de Hola de canalización, junto con los conjuntos de datos de entrada y salida para las actividades de Hola. Esta característica es útil cuando la canalización incluye más de una actividad y desea toounderstand Hola operativa acerca del linaje de una sola canalización.

    ![Menú Abrir canalización](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. En el siguiente ejemplo de Hola, verá una actividad de copia de canalización de hello con una entrada y salida. 

    ![Actividades en una canalización](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Puede navegar toohello atrás portada Hola factoría de datos haciendo clic en hello **factoría de datos** vínculo en la ruta de navegación de hello en la esquina superior izquierda de Hola.

    ![Navegue generador toodata atrás](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Estado de cada actividad dentro de una canalización de hello de vista
Puede ver estado actual de Hola de una actividad por ver el estado de Hola de cualquiera de los conjuntos de datos de hello producidos por actividad hello.

Haga doble clic en hello **OutputBlobTable** en hello **diagrama**, puede ver todos los sectores de Hola que se producen en ejecuciones de actividad diferente dentro de una canalización. Puede ver que actividad de copia de Hola se ejecutó correctamente para hello últimas ocho horas y genera sectores Hola Hola **listo** estado.  

![Estado de canalización de Hola](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

segmentos de conjunto de datos de Hola de factoría de datos de hello pueden tener uno de hello siguientes estados:

<table>
<tr>
    <th align="left">Estado</th><th align="left">Subestado</th><th align="left">Description</th>
</tr>
<tr>
    <td rowspan="8">En espera</td><td>ScheduleTime</td><td>no se ha llegado el momento de Hola para hello toorun de segmento.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>dependencias de nivel superior de Hello no están preparadas.</td>
</tr>
<tr>
<td>ComputeResources</td><td>recursos de proceso de Hello no están disponibles.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Todas las instancias de actividad de hello están ocupadas ejecutando otros segmentos.</td>
</tr>
<tr>
<td>ActivityResume</td><td>actividad Hello está en pausa y no puede ejecutar sectores Hola hasta que se reanude la actividad Hola.</td>
</tr>
<tr>
<td>Retry</td><td>Se está volviendo a intentar la ejecución de la actividad.</td>
</tr>
<tr>
<td>Validación</td><td>Aún no ha iniciado la validación.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>La validación es toobe espera vuelve a intentar.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>Validación en curso.</td>
</tr>
<td>-</td>
<td>segmento de saludo se está procesando.</td>
</tr>
<tr>
<td rowspan="4">Con error</td><td>TimedOut</td><td>ejecución de la actividad de Hello ha tardado más de las permitidas por actividad hello.</td>
</tr>
<tr>
<td>Canceled</td><td>segmento de Hello fue cancelada por acción del usuario.</td>
</tr>
<tr>
<td>Validación</td><td>Error de validación.</td>
</tr>
<tr>
<td>-</td><td>segmento de Hello no pudo toobe generado o validar.</td>
</tr>
<td>Ready</td><td>-</td><td>segmento de Hello está listo para su uso.</td>
</tr>
<tr>
<td>Skipped</td><td>None</td><td>segmento de Hello no está procesando.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>Un segmento utiliza tooexist con un estado diferente, pero se ha restablecido.</td>
</tr>
</table>



Puede ver detalles de hello sobre un segmento, haga clic en una entrada de segmento en hello **sectores actualizado recientemente** hoja.

![Detalles de segmento](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Si el segmento de Hola se ha ejecutado varias veces, verá varias filas en hello **se ejecuta la actividad** lista. Puede ver detalles sobre la actividad ejecutar haciendo clic en la entrada de hello ejecutar Hola **se ejecuta la actividad** lista. lista de Hello muestra todos los archivos de registro de hello, junto con un mensaje de error si hay alguno. Esta característica es útiles registros de tooview y de depuración sin tener tooleave su factoría de datos.

![Detalles de ejecución de actividad](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Si no está segmento Hola Hola **listo** estado, puede ver segmentos ascendentes de Hola que no están preparados y están bloqueando el intervalo actual de Hola de ejecutarse en hello **segmentos ascendentes que no están listos** lista. Esta característica es útil cuando el segmento está en **espera** estado y desea que está esperando dependencias ascendentes de toounderstand Hola que Hola segmento.

![Segmentos ascendentes que no están listos](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Diagrama de estado del conjunto de datos
Después de implementar una factoría de datos y las canalizaciones de hello tienen un período activo válido, el conjunto de datos de hello segmentos de transición de un estado tooanother. Actualmente, el estado del sector de hello sigue Hola después de diagrama de estado:

![Diagrama de estado](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

flujo de transición de estado del conjunto de datos en la factoría de datos Hello es siguiente de hello: espera -> en curso o en curso (Validating) -> Listo/fallido.

segmento de Hola se inicia en un **espera** estado, esperando toobe las condiciones previas cumplido antes de su ejecución. A continuación, actividad de hello empieza a ejecutarse y segmento Hola entra en un **en curso** estado. ejecución de la actividad de Hello podría succeed o fail. segmento de Hello está marcada como **listo** o **error**, según el resultado de hello de ejecución de Hola.

Puede restablecer Hola segmento toogo de hello **listo** o **error** estado toohello **espera** estado. También puede marcar el estado del segmento de hello**omitir**, lo que evita la actividad de hello de ejecución y no procesa el segmento de Hola.

## <a name="pause-and-resume-pipelines"></a>Pausa y reanudación de canalizaciones
Puede administrar las canalizaciones usando Azure PowerShell. Por ejemplo, puede pausar y reanudar canalizaciones ejecutando cmdlets de Azure PowerShell. 

> [!NOTE] 
> vista de diagrama de Hello no admite pausar y reanudar las canalizaciones. Si desea que toouse una interfaz de usuario, utilice Hola de supervisión y administración de aplicaciones. Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md) artículo. 

Puede pausar/suspender canalizaciones mediante el uso de hello **AzureRmDataFactoryPipeline Suspend** cmdlet de PowerShell. Este cmdlet es útil cuando no desee que toorun sus canalizaciones hasta que se solucione un problema. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Por ejemplo:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Una vez resuelto el problema de Hola con canalización de hello, puede reanudar canalización Hola suspendido ejecutando el siguiente comando de PowerShell de hello:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Por ejemplo:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Depuración de canalizaciones
Factoría de datos de Azure proporciona amplias funciones de toodebug y solucionar problemas de canalizaciones mediante Hola portal de Azure y Azure PowerShell.

> [! Tenga en cuenta} es mucho más fácil tootroubleshot errores con Hola supervisión & aplicación de administración. Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md) artículo. 

### <a name="find-errors-in-a-pipeline"></a>Búsqueda de errores en una canalización
Si se produce un error en la ejecución de la actividad de hello en una canalización, conjunto de datos de hello generado por la canalización de hello es en un estado de error debido a un error de Hola. Puede depurar y solucionar los errores en Data Factory de Azure mediante el uso de hello siguiendo métodos.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Usar hello toodebug portal Azure un error
1. En hello **tabla** hoja, haga clic en el sector de problema de Hola que tiene hello **estado** establecido demasiado**error**.

   ![Hoja Tabla con segmentos con problemas](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. En hello **el segmento de datos** hoja, haga clic en la actividad de hello que no se pudo ejecutar.

   ![Segmento de datos con un error](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. En hello **detalles de ejecución de la actividad** hoja, puede descargar archivos Hola que están asociados con el procesamiento de HDInsight de Hola. Haga clic en **descargar** estado/stderr toodownload Hola error archivo de registro que contiene detalles sobre el error de Hola.

   ![Hoja Detalles de ejecución de actividad con errores](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Usar PowerShell toodebug un error
1. Inicie **PowerShell**.
2. Ejecute hello **Get AzureRmDataFactorySlice** comandos toosee sectores de Hola y sus Estados. Debería ver un segmento con el estado de Hola de **error**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Por ejemplo:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Reemplace **StartDateTime** por la hora de inicio de la canalización. 
3. Ahora, ejecute hello **AzureRmDataFactoryRun Get** ejecutaron cmdlet tooget detalles acerca de la actividad de hello para el segmento de Hola.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Por ejemplo:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    valor de Hola de StartDateTime es hora de inicio de Hola de segmento de error o problema de Hola que anotó en el paso anterior de Hola. Hola de fecha y hora debe ir entre comillas dobles.
4. Debería ver resultados con detalles sobre los errores Hola similar siguiente toohello:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Puede ejecutar hello **guardar AzureRmDataFactoryLog** cmdlet con el valor de identificador que se produzcan de salida de hello y descargar archivos de registro de hello mediante Hola Hola **- DownloadLogsoption** Hola cmdlet.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Repetición de la ejecución de errores en una canalización

> [!IMPORTANT]
> Es más fácil de errores de tootroubleshoot y vuelva a ejecutar sectores errores mediante el uso de Hola supervisión y administración de aplicaciones. Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Usar hello portal de Azure
Después de solucionar problemas y depurar los errores en una canalización, puede volver a ejecutar errores navegar por segmento de error toohello y haciendo clic en hello **ejecutar** botón de barra de comandos de Hola.

![Repetición de ejecución de un segmento con errores](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

En caso de segmento de hello no pudo validar debido a un error de directiva (por ejemplo, si datos no están disponibles), puede corregir el error de Hola y validar de nuevo haciendo clic en hello **validar** botón de barra de comandos de Hola.

![Corrección de errores y validación](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Uso de Azure PowerShell
Puede volver a ejecutar errores mediante el uso de hello **AzureRmDataFactorySliceStatus conjunto** cmdlet. Vea hello [AzureRmDataFactorySliceStatus conjunto](https://msdn.microsoft.com/library/mt603522.aspx) tema para la sintaxis y otros detalles acerca del cmdlet Hola.

**Ejemplo:**

Hello en el ejemplo siguiente se establece estado Hola de todos los sectores de hello tabla 'DAWikiAggregatedData' too'Waiting' en el generador de datos de Azure de hello 'WikiADF'.

Hola 'tipo ' de actualización se establece too'UpstreamInPipeline ', lo que significa que los Estados de cada sector para la tabla de Hola y todas las tablas (ascendente) dependiente de Hola se establecen too'Waiting'. Hola otro valor posible para este parámetro es "Individual".

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Creación de alertas
Azure registra eventos del usuario cuando se crea, actualiza o elimina un recurso de Azure (por ejemplo, una factoría de datos). Puede crear alertas en estos eventos. Puede utilizar toocapture de factoría de datos diferentes métricas y crear alertas para las métricas. Se recomienda que use los eventos con fines de supervisión en tiempo real y las métricas con fines históricos.

### <a name="alerts-on-events"></a>Alertas en eventos
Los eventos de Azure proporcionan información útil sobre lo que sucede en los recursos de Azure. Al usar Azure Data Factory, se generan eventos cuando:

* Se crea, actualiza o elimina una factoría de datos.
* Se inicia o finaliza el procesamiento de datos (su "ejecución").
* Se crea o se elimina un clúster de HDInsight a petición.

Puede crear alertas para estos eventos de usuario y configurarlos en el Administrador de toohello de notificaciones de correo electrónico de toosend y coadministrators de suscripción de Hola. Además, puede especificar direcciones de correo electrónico adicionales de los usuarios que necesitan tooreceive notificaciones de correo electrónico cuando se cumplen las condiciones de Hola. Esta característica es útil cuando desea tooget una notificación cuando se produzcan errores y no desea que el monitor de toocontinuously su factoría de datos.

> [!NOTE]
> Actualmente, portal de hello no mostrar alertas de eventos. Hola de uso [aplicación de supervisión y administración](data-factory-monitor-manage-app.md) toosee todas las alertas.


#### <a name="specify-an-alert-definition"></a>Especificación de una definición de alerta
toospecify una definición de alerta, cree un archivo JSON que describe las operaciones de Hola que desee toobe alerta en. En el siguiente ejemplo de Hola, alerta de hello envía una notificación de correo electrónico para hello RunFinished operación. toobe específico, se envía una notificación de correo electrónico cuando se ha completado una ejecución de factoría de datos de Hola y Hola ejecutar ha fallado (estado = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

Puede quitar **subestado** de hello definición de JSON si no desea toobe alerta en un error específico.

Este ejemplo se configura la alerta de Hola para todos los generadores de datos en su suscripción. Si desea hello toobe alerta configurada para una factoría de datos determinado, puede especificar la factoría de datos **resourceUri** en hello **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Hello tabla siguiente proporciona Hola lista de operaciones disponibles y Estados (y sub-estados).

| Nombre de la operación | Estado | Subestado |
| --- | --- | --- |
| RunStarted |Started |Iniciando |
| RunFinished |Failed / Succeeded |FailedResourceAllocation<br/><br/>Succeeded<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><Canceled<br/><br/>FailedValidation<br/><br/>Abandoned |
| OnDemandClusterCreateStarted |Started | |
| OnDemandClusterCreateSuccessful |Correcto | |
| OnDemandClusterDeleted |Correcto | |

Vea [crear regla de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) para obtener más información acerca de los elementos JSON de Hola que se usan en el ejemplo de Hola.

#### <a name="deploy-hello-alert"></a>Implementar alerta Hola
alerta de hello toodeploy, use el cmdlet de PowerShell de Azure hello **AzureRmResourceGroupDeployment nuevo**, tal y como se muestra en el siguiente ejemplo de Hola:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Una vez que haya terminado correctamente la implementación de grupo de recursos de hello, verá Hola siguientes mensajes:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> Puede usar hello [crear regla de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) API de REST toocreate una regla de alerta. carga JSON de Hello es ejemplo JSON toohello similar.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Recuperar la lista de Hola de implementaciones de grupos de recursos de Azure
lista de hello tooretrieve de implementa las implementaciones de grupo de recursos de Azure, use el cmdlet hello **AzureRmResourceGroupDeployment Get**, tal y como se muestra en el siguiente ejemplo de Hola:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Solución de problemas de eventos del usuario
1. Puede ver todos los eventos de Hola que se generan después de hacer clic hello **métricas y las operaciones** icono.

    ![Icono Métricas y operaciones](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Haga clic en hello **eventos** eventos de hello toosee en mosaico.

    ![Icono de eventos](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. En hello **eventos** hoja, puede ver detalles sobre eventos, eventos filtrados y así sucesivamente.

    ![Hoja Eventos](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Haga clic en un **operación** en lista de operaciones de Hola que se produzca un error.

    ![Seleccionar una operación](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Haga clic en un **Error** toosee detalles del evento sobre error Hola.

    ![Evento de error](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Vea [una visión general de Azure cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) para cmdlets de PowerShell que puede usar tooadd, obtener o quitar alertas. Estos son algunos ejemplos del uso de hello **AlertRule Get** cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Ejecute hello después de get-help comandos toosee detalles y ejemplos relacionados con el cmdlet Get-AlertRule de Hola.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Si ve eventos de generación de alertas de hello en hello hoja portal pero no recibe notificaciones de correo electrónico, compruebe si dirección de correo electrónico de hello especificado se ha establecido tooreceive los correos electrónicos de remitentes externos. los mensajes de alerta de Hola se podrían haber bloqueado por la configuración de correo electrónico.

### <a name="alerts-on-metrics"></a>Alertas en métricas
Puede usar Data Factory para capturar diversas métricas y crear alertas sobre las métricas. Puede supervisar y crear alertas para hello siguiendo las métricas para intervalos de saludo de la factoría de datos:

* **Ejecuciones con error**
* **Ejecuciones correctas**

Estas métricas son útiles y le ayudarán a tooget que una visión general de global correctos y erróneos se ejecuta en la factoría de datos de Hola. Las métricas se emiten cada vez que hay una ejecución del segmento. En principio Hola de hora de hello, estas métricas se agregan e insertan tooyour cuenta de almacenamiento. las métricas de tooenable, configure una cuenta de almacenamiento.

#### <a name="enable-metrics"></a>Habilitación de métricas
las métricas de tooenable, haga clic en siguiente Hola de hello **factoría de datos** hoja:

**Supervisión** > **Métrica** > **Configuración de diagnóstico** > **Diagnóstico**

![Vínculo a Diagnóstico](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

En hello **diagnósticos** hoja, haga clic en **en**, seleccione la cuenta de almacenamiento de Hola y haga clic en **guardar**.

![Hoja Diagnósticos](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Podría tardar hasta hora tooone Hola métricas toobe visible en hello **supervisión** hoja como agregación de métricas se realiza cada hora.

### <a name="set-up-an-alert-on-metrics"></a>Configuración de alertas en métricas
Haga clic en hello **las métricas de la factoría de datos** icono:

![Icono Métricas de la factoría de datos](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

En hello **métrica** hoja, haga clic en **+ Agregar alerta** en la barra de herramientas de Hola.
![Hoja Métrica de la factoría de datos &gt; Agregar alerta](./media/data-factory-monitor-manage-pipelines/add-alert.png)

En hello **agregar una regla de alerta** página, Hola pasos y haga clic en **Aceptar**.

* Escriba un nombre para la alerta de hello (ejemplo: "alerta de error de").
* Escriba una descripción de alerta de hello (ejemplo: "enviar un correo electrónico cuando se produce un error").
* Seleccione una métrica ("ejecuciones con error" frente a "ejecuciones correctas").
* Especifique una condición y el valor del umbral.   
* Especificar el período de Hola de tiempo.
* Especifica si se debe enviar un correo electrónico tooowners, contributors y readers.

![Hoja Métrica de la factoría de datos > Agregar regla de alerta](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Después de regla de alerta de Hola se agrega correctamente, se cierra la hoja de Hola y verá la nueva alerta de hello en hello **métrica** hoja.

![Hoja Métrica de la factoría de datos > Nueva alerta agregada](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

También debería ver el número de Hola de alertas en hello **reglas de alerta** icono. Haga clic en hello **reglas de alerta** icono.

![Hoja Métrica de la factoría de datos: Reglas de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

En hello **reglas de alertas** hoja, vea las alertas existentes. tooadd una alerta, haga clic en **Agregar alerta** en la barra de herramientas de Hola.

![Hoja Reglas de alertas](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Notificaciones de alerta
Después de regla de alerta de hello coincide con la condición de hello, debería obtener un correo electrónico que indica que se activa la alerta de Hola. Después de que se resuelve el problema de Hola y condición de alerta de hello no coincide con ya, obtendrá un correo electrónico que dice Hola alerta se resuelve.

Este comportamiento es diferente al de eventos en los que se envía una notificación en todos los errores en los que la regla de alerta se cumple.

### <a name="deploy-alerts-by-using-powershell"></a>Establecimiento de alertas mediante PowerShell
Puede implementar las alertas para métricas Hola misma forma que para los eventos.

**Definición de la alerta**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Reemplace *subscriptionId*, *resourceGroupName*, y *dataFactoryName* en el ejemplo de Hola con los valores adecuados.

*metricName* admite actualmente dos valores:

* FailedRuns
* SuccessfulRuns

**Implementar alerta Hola**

alerta de hello toodeploy, use el cmdlet de PowerShell de Azure hello **AzureRmResourceGroupDeployment nuevo**, tal y como se muestra en el siguiente ejemplo de Hola:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Debería ver el siguiente mensaje después de una correcta implementación:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

También puede usar hello **AlertRule agregar** cmdlet toodeploy una regla de alerta. Vea hello [AlertRule agregar](https://msdn.microsoft.com/library/mt282468.aspx) tema para obtener información detallada y ejemplos.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Mover un grupo de recursos distinto de tooa de factoría de datos o una suscripción
Puede mover un grupo de recursos diferente de tooa de generador de datos o una suscripción diferente mediante hello **mover** botón en la página principal de saludo de la factoría de datos de la barra de comandos.

![Mover factoría de datos](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

También puede mover cualquier recurso relacionado (por ejemplo, las alertas que están asociadas a la factoría de datos de hello), junto con la factoría de datos de Hola.

![Cuadro de diálogo Mover recursos](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
