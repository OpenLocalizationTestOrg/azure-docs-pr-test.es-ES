---
title: "aaaAzure factoría de datos: preguntas más frecuentes"
description: "Preguntas más frecuentes acerca de Azure Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure Data Factory: preguntas más frecuentes
## <a name="general-questions"></a>Preguntas generales
### <a name="what-is-azure-data-factory"></a>¿Qué es Azure Data Factory?
Factoría de datos está basado en una nube servicio de integración de datos **automatiza el movimiento de Hola y la transformación de datos**. Al igual que un generador que se ejecuta equipo materias primas de tootake y transformarlos en terminados, factoría de datos orquesta servicios existentes que recopilan datos sin procesar y transforman en información lista para su uso.

Factoría de datos permite los datos de toomove de flujos de trabajo de datos de toocreate entre tanto local y almacenes de datos en la nube, así como datos de proceso o transformar mediante servicios de proceso como HDInsight de Azure y análisis de Data Lake de Azure. Después de crear una canalización que realiza la acción de Hola que necesita, puede programarlo toorun periódicamente (cada hora, diariamente, semanalmente etcetera).   

Para más información, consulte [Información general y conceptos clave](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>¿Dónde puedo encontrar detalles de precios de Azure Data Factory?
Vea [página de detalles de precios de factoría de datos] [ adf-pricing-details] para hello detalles de precios de hello Data Factory de Azure.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>¿Cómo puedo comenzar con Azure Data Factory?
* Para obtener información general de la factoría de datos de Azure, consulte [tooAzure Introducción factoría de datos](data-factory-introduction.md).
* Para obtener un tutorial sobre cómo demasiado**copiar o mover datos** con actividad de copia, consulte [copiar los datos de base de datos SQL del almacenamiento de blobs de Azure tooAzure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Para obtener un tutorial sobre cómo demasiado**transformar datos** mediante la actividad de Hive de HDInsight. consulte [Procesamiento de datos mediante la ejecución de scripts de Hive en un clúster Hadoop](data-factory-build-your-first-pipeline.md).

### <a name="what-is-hello-data-factorys-region-availability"></a>¿Qué es la disponibilidad de región del generador de datos de hello?
Data Factory está disponible en las regiones **Oeste de EE. UU.** y **Europa del Norte**. Hola proceso y servicios de almacenamiento utilizados por los generadores de datos pueden estar en otras regiones. Consulte las [regiones admitidas](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>¿Cuáles son los límites de hello en número de generadores/canalizaciones/actividades/orígenes de datos?
Vea **límites de factoría de datos de Azure** sección de hello [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md#data-factory-limits) artículo.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>¿Qué es la experiencia de creación/desarrollador de hello con servicio de factoría de datos de Azure?
Puede crear/crear factorías de datos mediante uno de hello después herramientas/SDK:

* **Portal de Azure** hojas de factoría de datos de Hola Hola portal de Azure proporcionan interfaz de usuario enriquecida para usted toocreate datos generadores ad vinculado servicios. Hola **Editor de generador de datos**, que también forma parte del portal de hello, le permite tooeasily crear servicios vinculados, tablas, conjuntos de datos y las canalizaciones mediante la especificación de las definiciones de JSON para estos artefactos. Vea [crear su primera canalización de datos mediante el portal de Azure](data-factory-build-your-first-pipeline-using-editor.md) para un ejemplo del uso de Hola toocreate/editor del portal e implementar una factoría de datos.
* **Visual Studio** puede usar Visual Studio toocreate un generador de datos de Azure. Consulte [Compilación de la primera Data Factory de Azure mediante Microsoft Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) .
* **Azure PowerShell** : consulte el tutorial [Creación y supervisión de Azure Data Factory mediante Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) para crear una factoría de datos mediante PowerShell. Consulte el contenido de [Referencia de cmdlets de Data Factory][adf-powershell-reference] en MSDN Library para obtener documentación completa de los cmdlets de Factoría de datos.
* **Biblioteca de clases .NET** Se pueden crear factorías de datos mediante programación con el SDK de .NET de Data Factory. Consulte [Creación, supervisión y administración de las factorías de datos mediante el SDK de .NET](data-factory-create-data-factories-programmatically.md) para un ver tutorial sobre la creación de una factoría de datos con el SDK de .NET. Consulte [Referencia de biblioteca de clases de Data Factory][msdn-class-library-reference] para una amplia documentación sobre el SDK de .NET de Factoría de datos.
* **API de REST** también puede usar hello REST API expuestas por el servicio toocreate de hello Data Factory de Azure e implementar generadores de datos. Consulte [Referencia de la API de REST de Data Factory][msdn-rest-api-reference] para ver una amplia documentación sobre la API de REST de Data Factory.
* **Plantilla de Azure Resource Manager** Consulte [Tutorial: Compilación de la primera Data Factory de Azure con la plantilla de Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md) para obtener más información.

### <a name="can-i-rename-a-data-factory"></a>¿Se puede cambiar el nombre de una Factoría de datos?
No. Como los demás recursos de Azure, no se puede cambiar el nombre de Hola de un generador de datos de Azure.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>¿Puedo mover una factoría de datos de una tooanother de suscripción de Azure?
Sí. Hola de uso **mover** situado en la hoja de factoría de datos como se muestra en hello siguiente diagrama:

![Mover factoría de datos](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>¿Qué entornos de proceso de hello admitidos factoría de datos?
Hello tabla siguiente proporciona una lista de entornos de ejecución compatible con las actividades de hello y factoría de datos que se pueden ejecutar en ellos.

| Entorno de procesos | actividades |
| --- | --- |
| [Clúster de HDInsight a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) o [clúster HDInsight propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |
| [Azure Batch](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Aprendizaje automático de Azure](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Actividades de Machine Learning: ejecución de Batch y recurso de actualización](data-factory-azure-ml-batch-execution-activity.md) |
| [Análisis con Azure Data Lake](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[U-SQL de análisis con Data Lake](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Procedimiento almacenado](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>¿Cómo se compara Azure Data Factory con SQL Server Integration Services (SSIS)? 
Vea hello [frente a Data Factory de Azure. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) de uno de nuestros MVP (profesionales más valiosos): Reza Rad. Algunos de los cambios recientes de Hola de factoría de datos pueden no aparecer en la presentación de diapositivas de Hola. Vamos a agregar más capacidades tooAzure factoría de datos continuamente. Vamos a agregar más capacidades tooAzure factoría de datos continuamente. Se incorporará estas actualizaciones en la comparación de Hola de tecnologías de integración de datos de Microsoft en algún momento más adelante este año.   

## <a name="activities---faq"></a>Actividades: preguntas más frecuentes
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>¿Cuáles son los diferentes tipos de Hola de actividades que se puede utilizar en una canalización de factoría de datos?
* [Las actividades de movimiento de datos](data-factory-data-movement-activities.md) datos toomove.
* [Las actividades de transformación de datos](data-factory-data-transformation-activities.md) tooprocess o transformar datos.

### <a name="when-does-an-activity-run"></a>¿Cuándo se ejecuta una actividad?
Hola **disponibilidad** tabla de datos determina cuándo se ejecuta la actividad hello de salida de valor de configuración Hola. Si se especifican los conjuntos de datos, la actividad hello comprueba si se cumplen todas las dependencias de datos de entrada de hello (es decir, **listo** estado) antes de que comience la ejecución.

## <a name="copy-activity---faq"></a>Actividad de copia: preguntas más frecuentes
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>¿Es mejor toohave una canalización con varias actividades o una canalización separada para cada actividad?
Se supone que las canalizaciones toobundle actividades relacionadas. Si los conjuntos de datos de Hola que los conectan no son consumidos por cualquier otra actividad fuera de la canalización de hello, puede mantener las actividades de hello en una canalización. De este modo, no tendría períodos activos de canalización toochain para que se alineen entre sí. Además, Hola integridad de los datos en tablas de hello toohello interno canalización se conserva mejor al actualizar la canalización de Hola. Actualización de la canalización básicamente detiene todas las actividades de Hola de canalización de hello, elimina y crea de nuevo. Desde la perspectiva de edición, también podría ser más fácil de flujo de hello toosee de datos dentro de hello relacionados con actividades en JSON de un archivo de canalización de Hola.

### <a name="what-are-hello-supported-data-stores"></a>¿Qué Hola admite almacenes de datos?
Actividad de copia de factoría de datos copia datos de un almacén de datos de origen datos almacén tooa receptor. Factoría de datos admite Hola siguientes almacenes de datos. Se pueden escribir datos de cualquier origen tooany receptor. Haga clic en un toolearn de almacén de datos cómo toocopy tooand de datos de ese almacén.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Almacenes de datos con * puede ser local o en IaaS de Azure y requieren tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) en una máquina de IaaS en local o de Azure.

### <a name="what-are-hello-supported-file-formats"></a>¿Qué Hola formatos de archivo compatibles?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>¿Donde se realiza la operación de copia de hello?
Consulte la sección [Movimiento de datos disponible globalmente](data-factory-data-movement-activities.md#global) para obtener más información. En resumen, cuando se trate de un almacén de datos local, se realizarla en operación de copia de Hola Hola Data Management Gateway en su entorno local. Y, cuando el movimiento de datos de hello entre dos almacenes en la nube, se realiza la operación de copia de hello en lugar de receptor toohello más cercano de Hola de región de hello mismo geography.

## <a name="hdinsight-activity---faq"></a>Actividad de HDInsight: preguntas más frecuentes
### <a name="what-regions-are-supported-by-hdinsight"></a>¿Qué regiones admiten HDInsight?
Vea Hola sección disponibilidad geográfica en el artículo siguiente de hello: o [detalles de precios HDInsight][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>¿Qué región se usa con un clúster de HDInsight a petición?
Hello clúster de HDInsight a petición se crea en Hola misma región donde existe el almacenamiento de hello especificado toobe utilizado con clúster de Hola.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>¿Cómo el clúster de HDInsight de tooyour de cuentas de almacenamiento adicional de tooassociate?
Si está usando su propio HDInsight clúster (BYOC - Traer su propio clúster), vea Hola temas siguientes:

* [Uso de un clúster de HDInsight con cuentas de almacenamiento y tiendas de metadatos alternativas][hdinsight-alternate-storage]
* [Uso de cuentas de almacenamiento adicionales con HDInsight Hive][hdinsight-alternate-storage-2]

Si está usando un clúster a petición creado por el servicio Data Factory hello, especifique las cuentas de almacenamiento adicional para hello HDInsight el servicio vinculado para que el servicio de factoría de datos de hello puede registrar en su nombre. En la definición de JSON para el servicio vinculado de petición de Hola Hola, use **additionalLinkedServiceNames** cuentas de almacenamiento alternativo de propiedad toospecify tal y como se muestra en hello siguiente fragmento de JSON:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
En el ejemplo de Hola anterior, otherLinkedServiceName1 y otherLinkedServiceName2 representan servicios vinculados cuyas definiciones contienen las credenciales que Hola cuentas de almacenamiento alternativo de tooaccess de necesidades de clúster de HDInsight.

## <a name="slices---faq"></a>Segmentos: preguntas más frecuentes
### <a name="why-are-my-input-slices-not-in-ready-state"></a>¿Por qué mis segmentos de entrada no presentan el estado Listo?
Un error común no establece **externo** propiedad demasiado**true** en hello conjunto de datos de entrada cuando los datos de entrada hello es factoría de datos de toohello externo (no generada por factoría de datos de hello).

En el siguiente ejemplo de Hola, solo necesita tooset **externo** tootrue en **dataset1**.  

**DataFactory1** Pipeline 1: dataset1 -&gt; activity1 -&gt; dataset2 -&gt; activity2 -&gt; dataset3 Pipeline 2: dataset3-&gt; activity3 -&gt; dataset4

Si tiene otro generador de datos con una canalización que toma dataset4 (producidos por canalización 2 de la factoría de datos 1), marque dataset4 como un conjunto de datos externo porque el conjunto de datos de hello generado por un generador de datos diferentes (DataFactory1, no DataFactory2).  

**DataFactory2**    
Pipeline 1: dataset4->activity4->dataset5

Si correctamente se establece la propiedad external hello, compruebe si existen datos de entrada de hello en ubicación de hello especificada en definición de conjunto de datos de entrada de Hola.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>¿Cómo toorun un segmento en otro momento a la medianoche al segmento de Hola se está produciendo diariamente?
Hola de uso **desplazamiento** tiempo de hello toospecify de propiedad a la que desea Hola segmento toobe generado. Consulte la sección [Disponibilidad del conjunto de datos](data-factory-create-datasets.md#dataset-availability) para obtener más información sobre esta propiedad. Este es un ejemplo rápido:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Se inician los segmentos diarias en **6: 00** en lugar de la medianoche de Hola de forma predeterminada.     

### <a name="how-can-i-rerun-a-slice"></a>¿Cómo puedo volver a ejecutar un segmento?
Puede volver a ejecutar un segmento en uno de hello siguientes maneras:

* Utilice supervisar y administrar aplicaciones toorerun una ventana actividad o segmento. Consulte [Nueva ejecución de ventanas de actividad seleccionadas](data-factory-monitor-manage-app.md#perform-batch-actions) para ver instrucciones.   
* Haga clic en **ejecutar** en la barra de comandos de hello en hello **el segmento de datos** hoja de sector de Hola Hola portal de Azure.
* Ejecutar **conjunto AzureRmDataFactorySliceStatus** cmdlet con el estado se establece demasiado**espera** de sector de Hola.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Vea [conjunto AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] para obtener más información sobre el cmdlet de Hola.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>¿Durante cuánto tiempo se tarda tooprocess de un sector?
Utilice el Explorador de ventana de actividad en el Monitor de & aplicación administrar tooknow cuánto tiempo tardó tooprocess un segmento de datos. Consulte [Explorador de ventanas de actividad](data-factory-monitor-manage-app.md#activity-window-explorer) para obtener más información.

También puede hacer Hola sigue de hello portal de Azure:  

1. Haga clic en **conjuntos de datos** icono hello **factoría de datos** hoja de la factoría de datos.
2. Haga clic en un conjunto de datos específico de hello en hello **conjuntos de datos** hoja.
3. Sector Hola SELECT que le interesa de hello **sectores recientes** lista en hello **tabla** hoja.
4. Haga clic en ejecutar desde Hola de actividad de hello **ejecuciones de actividad** lista en hello **el segmento de datos** hoja.
5. Haga clic en **propiedades** icono hello **detalles de ejecución de la actividad** hoja.
6. Debería ver Hola **duración** campo con un valor. Este valor es el segmento de hello tooprocess tiempo Hola.   

### <a name="how-toostop-a-running-slice"></a>¿Cómo toostop un segmento de ejecución?
Si necesita la canalización de hello toostop de ejecutarse, puede usar [AzureRmDataFactoryPipeline Suspend](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet. Actualmente, suspender canalización hello no detiene las ejecuciones de segmento de Hola que están en curso. Una vez que termine de ejecuciones de hello en curso, no se selecciona ningún segmento adicional.

Si realmente desea toostop todas las ejecuciones de hello inmediatamente, Hola solo forma podría toodelete Hola canalización y crearla de nuevo. Si elige canalización de hello toodelete, no es necesario toodelete tablas y servicios vinculados Hola canalización usa.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
