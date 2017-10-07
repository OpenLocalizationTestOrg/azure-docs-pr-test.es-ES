---
title: "datos de aaaCopy de Blobs de almacenamiento de Azure en el almacén de Data Lake | Documentos de Microsoft"
description: "Usar datos de la herramienta toocopy AdlCopy almacenamiento de Blobs tooData Lake del almacén de Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData
> [!div class="op_single_selector"]
> * [Uso de DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Uso de AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Almacén de Data Lake de Azure proporciona una herramienta de línea de comandos, [AdlCopy](http://aka.ms/downloadadlcopy), datos de toocopy de hello siguientes orígenes:

* Desde los blobs de Almacenamiento de Azure en Data Lake Store. No se puede usar datos de toocopy de AdlCopy de blobs de almacenamiento de almacén de Data Lake tooAzure.
* Entre dos cuentas de Azure Data Lake Store.

Además, puede utilizar la herramienta de AdlCopy de hello en dos modos diferentes:

* **Independiente**, donde herramienta Hola utiliza la tarea de almacén de Data Lake recursos tooperform Hola.
* **Con una cuenta de análisis de Data Lake**, donde unidades Hola asignadas la cuenta de análisis de Data Lake tooyour son operación de copia de hello tooperform usado. Conviene toouse esta opción cuando las tareas de copia de hello tooperform se trata de una manera predecible.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **blobs de almacenamiento de Azure** con algunos datos.
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)
* **(Opcional) de la cuenta de análisis de Azure Data Lake** -vea [empezar a trabajar con análisis de Azure Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md) para obtener instrucciones sobre cómo toocreate un Data Lake almacenar la cuenta.
* **Herramienta AdlCopy**. Instalar la herramienta de hello AdlCopy de [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Sintaxis de hello AdlCopy herramienta
Usar hello siguiendo la sintaxis toowork con la herramienta de hello AdlCopy

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

a continuación se describen los parámetros de Hello en sintaxis de hello:

| Opción | Description |
| --- | --- |
| Origen |Especifica la ubicación de Hola Hola de datos de origen en el blob de almacenamiento de Azure Hola. Hola origen puede ser un contenedor de blobs, un blob u otra cuenta de almacén de Data Lake. |
| Dest |Especifica toocopy de destino de almacén de Data Lake Hola a. |
| SourceKey |Especifica la clave de acceso de almacenamiento de hello para el origen de blob de almacenamiento de Azure Hola. Esto es necesario sólo si el origen de hello es un contenedor de blobs o un blob. |
| Cuenta |**Opcional**. Utilícelo si desea que el trabajo de copia de toouse análisis de Azure Data Lake cuenta toorun Hola. Si usa la opción de hello AccountType en sintaxis de Hola pero no especifica una cuenta de análisis de Data Lake, AdlCopy utiliza un trabajo de Hola de toorun de cuenta predeterminada. Además, si utiliza esta opción, debe agregar origen de hello (Blob de almacenamiento de Azure) y de destino (almacén de Azure Data Lake) como orígenes de datos para su cuenta de análisis de Data Lake. |
| Unidades |Especifica el número de Hola de unidades de análisis de Data Lake que se usará para el trabajo de copia de Hola. Esta opción es obligatoria si utiliza hello **/cuenta** opción cuenta de análisis de Data Lake hello toospecify. |
| Patrón |Especifica un patrón de expresión regular que indica qué toocopy blobs o archivos. AdlCopy usa una coincidencia que distingue mayúsculas de minúsculas. patrón predeterminado que Hello usa cuando no se especifica ningún patrón es toocopy todos los elementos. No se admite la especificación de varios patrones de archivos. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Usar datos de toocopy de AdlCopy (como independiente) de un blob de almacenamiento de Azure
1. Abra un símbolo del sistema y desplácese directorio toohello AdlCopy está instalado, por lo general `%HOMEPATH%\Documents\adlcopy`.
2. Ejecute hello después comando toocopy un blob en cuestión desde Hola origen contenedor tooa almacén de Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Por ejemplo:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] sintaxis de Hello anterior especifica hello toobe tooa copiada cajón de cuenta de almacén de Data Lake Hola. Herramienta de AdlCopy crea una carpeta si no existe el nombre de la carpeta especificada de Hola.

    Podrá tooenter solicitada credenciales Hola para Hola suscripción de Azure en la que dispone de su cuenta de almacén de Data Lake. Verá un siguiente toohello similar de salida:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. También puede copiar todos los blobs de Hola de cuenta de almacén de Data Lake toohello un contenedor mediante el siguiente comando de hello:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Por ejemplo:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Consideraciones sobre rendimiento

Si va a copiar de una cuenta de almacenamiento de blobs de Azure, puede limitar durante la copia en el lado de almacenamiento de blobs de Hola. Esto disminuirá el rendimiento de Hola de su trabajo de copia. toolearn más información acerca de los límites de Hola de almacenamiento de blobs de Azure, consulte los límites de almacenamiento de Azure en [suscripción de Azure y límites de servicio](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>Usar datos de toocopy AdlCopy (como independiente) desde otra cuenta de almacén de Data Lake
También puede usar AdlCopy toocopy datos entre las dos cuentas de almacén de Data Lake.

1. Abra un símbolo del sistema y desplácese directorio toohello AdlCopy está instalado, por lo general `%HOMEPATH%\Documents\adlcopy`.
2. Ejecutar Hola después comando toocopy un archivo específico desde un almacén de Data Lake cuenta tooanother.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Por ejemplo:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > sintaxis de Hello anterior especifica toobe tooa copiada carpeta de archivos de hello en la cuenta de almacén de Data Lake de destino de Hola. Herramienta de AdlCopy crea una carpeta si no existe el nombre de la carpeta especificada de Hola.
   >
   >

    Podrá tooenter solicitada credenciales Hola para Hola suscripción de Azure en la que dispone de su cuenta de almacén de Data Lake. Verá un siguiente toohello similar de salida:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Hello siguiente comando copia todos los archivos de una carpeta específica en hello origen almacén de Data Lake cuenta tooa carpeta de destino de hello cuenta de almacén de Data Lake.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Consideraciones sobre rendimiento

Cuando se usa AdlCopy como una herramienta independiente, copia Hola se ejecuta en compartido, Azure los recursos administrados. rendimiento de Hello es posible que obtenga en este entorno depende de la carga del sistema y los recursos disponibles. Este modo se usa preferiblemente en el caso de pequeñas transferencias de manera ad hoc. Ningún parámetro necesario toobe optimizan cuando se usa AdlCopy como una herramienta independiente.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Usar datos de toocopy AdlCopy (con la cuenta de análisis de Data Lake)
También puede usar el análisis de Data Lake cuenta tooData Lake almacén de blobs de hello toorun AdlCopy datos de toocopy de trabajo del almacenamiento de Azure. Esta opción se utiliza normalmente cuando Hola datos toobe movido esté dentro del alcance de Hola de gigabytes y terabytes, y desea que el rendimiento de predicción y un mejor rendimiento.

toouse que su cuenta de análisis de Data Lake con AdlCopy toocopy de un Blob de almacenamiento de Azure, el origen de hello (Blob de almacenamiento de Azure) debe agregarse como un origen de datos para su cuenta de análisis de Data Lake. Para obtener instrucciones sobre cómo agregar la cuenta de análisis de Data Lake tooyour de orígenes de datos adicionales, consulte [orígenes de datos de la cuenta de administración de análisis de Data Lake](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> Si va a copiar de una cuenta de almacén de Azure Data Lake como origen de hello con una cuenta de análisis de Data Lake, no es necesario tooassociate Hola cuenta de almacén de Data Lake con hello cuenta de análisis de Data Lake. Hello requisito tooassociate Hola origen almacén con hello cuenta de análisis de Data Lake es solo cuando el origen de hello es una cuenta de almacenamiento de Azure.
>
>

Ejecute hello siguientes toocopy de comando de una cuenta de almacén de Data Lake tooa de blob de almacenamiento de Azure con cuenta de análisis de Data Lake:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Por ejemplo:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Del mismo modo, ejecute hello siguientes toocopy de comando de una cuenta de almacén de Data Lake tooa de blob de almacenamiento de Azure con cuenta de análisis de Data Lake:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Consideraciones sobre rendimiento

Cuando se copian datos en el intervalo de Hola de terabytes, usar AdlCopy con su propia cuenta de análisis de Data Lake de Azure proporciona un rendimiento mejor y más predecible. parámetro de Hola que debe optimizarse es número de Hola de Azure datos Lake Analytics unidades toouse Hola trabajo de copia. Aumentar el número de Hola de unidades aumentarán el rendimiento de Hola de su trabajo de copia. Cada toobe de archivo copiado puede usar una unidad de máxima. Especificar más unidades que Hola número de archivos que se copió no aumentará el rendimiento.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Usar AdlCopy toocopy datos mediante la coincidencia de patrones
En esta sección, aprenderá cómo toouse AdlCopy toocopy datos de un origen (en el ejemplo siguiente se utiliza Blob de almacenamiento de Azure) tooa de la cuenta de almacén de Data Lake de destino mediante la coincidencia de patrones. Por ejemplo, puede utilizar estos pasos hello toocopy todos los archivos con extensión .csv de hello origen blob toohello el destino.

1. Abra un símbolo del sistema y desplácese directorio toohello AdlCopy está instalado, por lo general `%HOMEPATH%\Documents\adlcopy`.
2. Ejecutar todos los archivos de hello después toocopy de comandos con la extensión de tipo *.csv de un blob en cuestión de hello origen contenedor tooa almacén de Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Por ejemplo:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Facturación
* Si usa hello AdlCopy herramienta como independiente que se le facturará de costos de salida para mover datos, si no está en la cuenta de almacenamiento de Azure de origen de Hola Hola misma región como Hola almacén de Data Lake.
* Si usa hello AdlCopy herramienta con el análisis de Data Lake cuenta estándar [las tasas de facturación del análisis de Data Lake](https://azure.microsoft.com/pricing/details/data-lake-analytics/) se aplicará.

## <a name="considerations-for-using-adlcopy"></a>Consideraciones para usar AdlCopy
* AdlCopy (para la versión 1.0.5) admite la copia de datos desde orígenes que en conjunto tienen más de miles de archivos y carpetas. Sin embargo, si encuentra problemas al copiar un conjunto de datos grande, puede distribuir archivos o carpetas de hello en subcarpetas diferentes y utilice en su lugar las subcarpetas de toothose de ruta de acceso de hello como origen de Hola.

## <a name="performance-considerations-for-using-adlcopy"></a>Consideraciones de rendimiento sobre el uso de AdlCopy

AdlCopy admite la copia de datos que contienen miles de archivos y carpetas. Sin embargo, si encuentra problemas al copiar un conjunto de datos grande, puede distribuir archivos o carpetas de hello en subcarpetas más pequeñas. AdlCopy se creó para copias ad hoc. Si está tratando de toocopy datos de forma periódica, considere la posibilidad de usar [Data Factory de Azure](../data-factory/data-factory-azure-datalake-connector.md) que proporciona una administración completa alrededor de las operaciones de copia de Hola.

## <a name="release-notes"></a>Notas de la versión
* 1.0.13 - si va a copiar datos toohello misma cuenta de almacén de Azure Data Lake a través de adlcopy varios comandos, no es necesario tooreenter sus credenciales para cada uno de ellos dejan de ejecutarse. Ahora, Adlcopy almacena en caché esa información entre varias ejecuciones.

## <a name="next-steps"></a>Pasos siguientes
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
