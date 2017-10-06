---
title: "aaaAzure factoría de datos: ejemplos"
description: Proporciona detalles acerca de los ejemplos que se incluyen con hello servicio Data Factory de Azure.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Factoría de datos de Azure: ejemplos
## <a name="samples-on-github"></a>Ejemplos en GitHub
Hola [repositorio de GitHub Azure-DataFactory](https://github.com/azure/azure-datafactory) contiene varios ejemplos que le ayudarán a rápidamente aumento con el servicio Data Factory de Azure (o) modifique los scripts de Hola y utilizarlo en la propia aplicación. carpeta de Hello Samples\JSON contiene fragmentos JSON para los escenarios comunes.

| Muestra | Description |
|:--- |:--- |
| [Tutorial de ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |Este ejemplo proporciona un tutorial to-end para el procesamiento de archivos de registro mediante datos de Data Factory de Azure tooturn de archivos de registro en tooinsights. <br/><br/>En este tutorial, canalización de factoría de datos de hello recopila registros de ejemplo, procesos y enriquece datos Hola de registros con datos de referencia y transforma Hola datos tooevaluate Hola la eficacia de una campaña de marketing que recientemente se ha iniciado. |
| [Muestras de JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |Esta muestra ofrece ejemplos de JSON para escenarios comunes. |
| [Muestra de descargador de datos HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Este ejemplo exhibe descarga de datos de un tooAzure de extremo HTTP almacenamiento de blobs mediante la actividad personalizada. NET. |
| [Muestra de CrossAppDomainDotNetActivity](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Este ejemplo permite tooauthor una actividad personalizada de .NET que no está restringida versiones tooassembly utilizadas por el selector ADF hello (por ejemplo, WindowsAzure.Storage v4.3.0, v6.0.x Newtonsoft.Json, etcetera). |
| [Ejecutar script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Este ejemplo incluye la actividad personalizada de hello factoría de datos que puede ser utilizado tooinvoke RScript.exe. Esta muestra solo funciona con su propio clúster de HDInsight (no a petición) que ya tiene R instalado. |
| [Invocar trabajos de Spark en clústeres de Hadoop de HDInsight](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |Este ejemplo se muestra cómo toouse MapReduce actividad tooinvoke un programa de Spark. programa de spark Hola solo copia datos de una tooanother de contenedor de blobs de Azure. |
| [Análisis de Twitter mediante actividad de puntuación de lotes de Aprendizaje automático de Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |Este ejemplo muestra cómo toouse AzureMLBatchScoringActivity tooinvoke un aprendizaje automático de Azure de modelo que lleva a cabo análisis de opinión de twitter, puntuación, predicción etcetera. |
| [Análisis de Twitter mediante actividad personalizada](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Este ejemplo muestra cómo toouse una tooinvoke de actividad de .NET personalizado un modelo de aprendizaje automático de Azure que realiza análisis de opiniones, puntuación, predicción etcetera de twitter. |
| [Canalizaciones con parámetros para el Aprendizaje automático de Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |ejemplo de Hola proporciona un extremo a C# código toodeploy N canalizaciones para puntuar y reciclaje cada uno con un parámetro de otra región donde lista Hola de regiones provienen de un archivo parameters.txt, que se incluye con este ejemplo. |
| [Actualización de datos de referencia para los trabajos de Análisis de transmisiones de Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |Este ejemplo muestra cómo actualizan toouse Data Factory de Azure y Azure Stream Analytics toorun juntos Hola consultas con hello de instalación y de datos de referencia para los datos de referencia según una programación. |
| [Canalización híbrida con Hadoop Hortonworks local](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |ejemplo de Hola utiliza un clúster de Hadoop local como un destino de proceso para ejecutar trabajos de factoría de datos tal como se agregaría otros destinos de proceso como un HDInsight en función de clúster de Hadoop en la nube. |
| [Herramienta de conversión de JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Esta herramienta le permite tooconvert JSON de toolatest too2015-07-01-versión preliminar anterior de versión o 2015-07-01-preview (valor predeterminado). |
| [Archivo de entrada de ejemplo de U-SQL](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Se trata de un archivo de ejemplo que utiliza una actividad U-SQL. |
| [Eliminar archivo de blob](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Este ejemplo muestra un archivo de C# que se puede usar como parte de ADF personalizada .net actividad toodelete archivos de origen de hello ubicación del Blob de Azure, una vez que se han copiado archivos Hola.|

## <a name="azure-resource-manager-templates"></a>Plantillas de Azure Resource Manager
Puede encontrar Hola siguiente plantillas del Administrador de recursos de Azure de factoría de datos de GitHub.

| Plantilla | Descripción |
| --- | --- |
| [Copiar desde el almacenamiento de blobs de Azure tooAzure base de datos SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |La implementación de esta plantilla crea un generador de datos de Azure con una canalización que copia datos de hello especifican la base de datos SQL de Azure toohello de almacenamiento de blobs de Azure |
| [Copiar desde Salesforce tooAzure almacenamiento de blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |La implementación de esta plantilla crea un generador de datos de Azure con una canalización que copia datos de hello especifican almacenamiento de blobs de Azure de toohello de cuenta de Salesforce. |
| [Transformación de los datos mediante la ejecución de un script de Hive en un clúster de Azure HDInsight](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |La implementación de esta plantilla crea un generador de datos de Azure con una canalización que transforma los datos mediante la ejecución de script de Hive de ejemplo de Hola en un clúster de Hadoop de HDInsight de Azure. |

## <a name="samples-in-azure-portal"></a>Ejemplos en Azure Portal
Puede usar hello **ejemplo canalizaciones** factoría de datos de tooyour el icono en la página principal de Hola de sus canalizaciones de ejemplo de toodeploy de generador de datos y sus entidades asociadas (conjuntos de datos y servicios vinculados).

1. Cree una factoría de datos o abra una. Vea [copiar los datos de almacenamiento de blobs tooSQL con factoría de datos de la base de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para pasos toocreate una factoría de datos.
2. Hola **factoría de datos** hoja de factoría de datos de hello, haga clic en hello **ejemplo canalizaciones** icono.

    ![Icono Canalizaciones de ejemplo](./media/data-factory-samples/SamplePipelinesTile.png)
3. Hola **ejemplo canalizaciones** hoja, haga clic en hello **ejemplo** que desea toodeploy.

    ![Hoja Canalizaciones de ejemplo](./media/data-factory-samples/SampleTile.png)
4. Especificar opciones de configuración de ejemplo de Hola. Por ejemplo, el nombre de la cuenta de almacenamiento de Azure y la clave de la cuenta, el nombre del servidor de SQL Azure, la base de datos, el identificador de usuario y la contraseña, etc.

    ![Hoja de ejemplo](./media/data-factory-samples/SampleBlade.png)
5. Una vez que haya en la especificación de opciones de configuración de hello, haga clic en **crear** toocreate/implementar Hola canalizaciones de ejemplo y utilizadas por las canalizaciones de hello services/tablas vinculadas.
6. Ver el estado de Hola de implementación en mosaico de ejemplo de Hola que hizo clic anteriormente hello **ejemplo canalizaciones** hoja.

    ![Estado de implementación](./media/data-factory-samples/DeploymentStatus.png)
7. Cuando vea hello **implementación se realizó correctamente** mensaje en mosaico Hola de ejemplo de Hola, cerrar hello **ejemplo canalizaciones** hoja.  
8. En **factoría de datos** hoja, verá que se agregan los servicios vinculados, conjuntos de datos y las canalizaciones tooyour factoría de datos.  

    ![Hoja de la Factoría de datos](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Ejemplos en Visual Studio
### <a name="prerequisites"></a>Requisitos previos
Debe tener instalado en el equipo siguiente de hello:

* Visual Studio 2013 o Visual Studio 2015.
* Descargue el SDK de Azure para Visual Studio 2013 o Visual Studio 2015. Navegue demasiado[página de descargas de Azure](https://azure.microsoft.com/downloads/) y haga clic en **VS 2013** o **VS 2015** en hello **.NET** sección.
* Descargue el complemento de Data Factory de Azure más reciente de Hola para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) o [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Si usa Visual Studio 2013, también puede actualizar complemento Hola haciendo Hola pasos: en el menú de hello, haga clic en **herramientas** -> **extensiones y actualizaciones**  ->  **En línea** -> **Galería de Visual Studio** -> **herramientas de generador de datos de Microsoft Azure para Visual Studio**  ->  **Actualización**.

### <a name="use-data-factory-templates"></a>Uso de plantillas de Data Factory
1. Haga clic en **archivo** en el menú de hello, seleccione demasiado**New**y haga clic en **proyecto**.
2. Hola **nuevo proyecto** diálogo cuadro, Hola lo siguiente:

   1. Seleccione **DataFactory** en **Plantillas**.
   2. Seleccione **plantillas de factoría de datos** en el panel derecho de Hola.
   3. Escriba un **nombre** proyecto Hola.
   4. Seleccione un **ubicación** proyecto Hola.
   5. Haga clic en **Aceptar**.

      ![Cuadro de diálogo Nuevo proyecto](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. Hola **plantillas de factoría de datos** cuadro de diálogo, la plantilla de ejemplo de Hola select de hello **plantillas de casos de uso** sección y haga clic en **siguiente**. Hello pasos siguientes le guían a través mediante hello **del cliente de generación de perfiles** plantilla. Pasos son similares para Hola otros ejemplos.

    ![Cuadro de diálogo Plantillas de Data Factory](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. Hola **configuración del generador de datos** cuadro de diálogo, haga clic en **siguiente** en hello **Fundamentos de la factoría de datos** página.
5. En hello **factoría de datos de configuración** página, Hola lo siguiente:
   1. Seleccione la opción **Crear la nueva factoría de datos**. También puede seleccionar **Use existing data factory**(Usar factoría de datos existente).
   2. Escriba un **nombre** de factoría de datos de Hola.
   3. Seleccione hello **suscripción de Azure** en que se desea Hola datos generador toobe creado.
   4. Seleccione hello **grupo de recursos** de factoría de datos de Hola.
   5. Seleccione hello **oeste de EE.**, **UU**, o **Europa del Norte** para hello **región**.
   6. Haga clic en **Siguiente**.
6. Hola **configurar almacenes de datos** página, especifique un existente **base de datos SQL de Azure** y **cuenta de almacenamiento de Azure** (o) crear base de datos y el almacenamiento y haga clic en siguiente.
7. Hola **configurar proceso** página, seleccione los valores predeterminados y haga clic en **siguiente**.
8. Hola **resumen** página, revise todas las opciones y haga clic en **siguiente**.
9. Hola **estado de implementación** página, espere hasta que finalice la implementación de Hola y haga clic en **finalizar**.
10. Haga clic en el proyecto en el Explorador de soluciones de Hola y haga clic en **publicar**.
11. Si ve **iniciar sesión en la cuenta de Microsoft tooyour** cuadro de diálogo, escriba sus credenciales de cuenta de hello que tenga la suscripción de Azure y haga clic en **iniciar sesión en**.
12. Debería ver Hola después el cuadro de diálogo:

    ![Cuadro de diálogo Publicar](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. Hola **factoría de datos de configuración** página, Hola lo siguiente:

    1. Confirme la opción **Use existing data factory** (Usar factoría de datos existente).
    2. Seleccione hello **factoría de datos** tenía select cuando se usa la plantilla de Hola.
    3. Haga clic en **siguiente** tooswitch toohello **publicar elementos** página. (Presione **ficha** toomove fuera Hola de hello nombre campo tooif **siguiente** botón está deshabilitado.)
14. Hola **publicar elementos** página, asegúrese de que todas las factorías de datos de entidades están seleccionadas y haga clic en Hola **siguiente** tooswitch toohello **resumen** página.     
15. Revise el resumen de Hola y haga clic en **siguiente** Hola de proceso y la vista de la implementación del hello toostart **estado de implementación**.
16. Hola **estado de implementación** página, debería ver estado de Hola Hola del proceso de implementación. Después de que se realice la implementación de hello, haga clic en Finalizar.

Vea [crear su primer factoría de datos (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) para obtener más información acerca del uso de entidades de factoría de datos de Visual Studio tooauthor y publicarlas tooAzure.          
