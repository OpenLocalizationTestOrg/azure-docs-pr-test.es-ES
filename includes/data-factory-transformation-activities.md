Factoría de datos de Azure admite Hola siguiendo las actividades de transformación que pueden ser agregado toopipelines individualmente o se encadenan con otra actividad.

| Actividad de transformación de datos | Entorno de procesos |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Streaming](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Actividades de Machine Learning: ejecución de Batch y recurso de actualización](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |MV de Azure |
| [Procedimiento almacenado](../articles/data-factory/data-factory-stored-proc-activity.md) |SQL Azure, Almacenamiento de datos SQL de Azure o SQL Server |
| [U-SQL de análisis con Data Lake](../articles/data-factory/data-factory-usql-activity.md) |Análisis con Azure Data Lake |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] o Lote de Azure |

> [!NOTE]
> Puede usar programas de MapReduce actividad toorun Spark en el clúster de HDInsight Spark. Consulte [Invoke Spark programs from Azure Data Factory](../articles/data-factory/data-factory-spark.md) (Invocar programas Spark desde Data Factory de Azure) para obtener información detallada.
> Puede crear una actividad personalizada toorun R scripts en el clúster de HDInsight con R instalado. Consulte [Run R Script using Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Ejecutar script de R con Data Factory de Azure).
> 
> 

