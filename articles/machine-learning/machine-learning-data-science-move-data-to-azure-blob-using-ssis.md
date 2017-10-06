---
title: aaaMove tooor de datos de uso de conectores SSIS de almacenamiento de blobs de Azure | Documentos de Microsoft
description: Mover datos tooor de almacenamiento de blobs de Azure al uso de conectores SSIS.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Mover datos tooor de almacenamiento de blobs de Azure al uso de conectores SSIS
Hola [SQL Server Integration Services Feature Pack para Azure](https://msdn.microsoft.com/library/mt146770.aspx) proporciona componentes tooconnect tooAzure, transferencia de datos entre orígenes de datos de Azure y local y procesar los datos almacenados en Azure.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Una vez que los clientes que movido datos locales en la nube hello, puede acceder desde cualquier servicio de Azure tooleverage Hola toda la potencia del conjunto de Hola de tecnologías de Azure. Por ejemplo, se pueden usar en Aprendizaje automático de Azure o en un clúster de HDInsight.

Esto suele ser el primer paso de Hola para hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) y [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) tutoriales.

Para obtener una explicación de los escenarios canónicas que utilizan business tooaccomplish SSIS debe comunes en escenarios de integración de datos híbridos, consulte [hacer más con SQL Server Integration Services Feature Pack para Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.

> [!NOTE]
> Para un almacenamiento de blobs de tooAzure introducción completa, consulte demasiado[conceptos básicos de Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) y demasiado[servicio Blob de Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
tareas de hello tooperform describen en este artículo, debe tener una suscripción de Azure y una cuenta de almacenamiento de Azure configurada. Debe saber el almacenamiento de Azure cuenta nombre y la cuenta clave tooupload o descargar datos.

* tooset seguridad un **suscripción de Azure**, consulte [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obtener instrucciones sobre cómo crear una **cuenta de almacenamiento** y cómo obtener información sobre la cuenta y la clave, consulte [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).

Hola toouse **conectores SSIS**, debe descargar:

* **SQL Server 2014 o 2016 Standard (o superior)**: la instalación incluye SQL Server Integration Services.
* **Microsoft SQL Server 2014 o 2016 Integration Services Feature Pack para Azure**: estos se pueden descargar, respectivamente, de hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) y [integración con SQL Server 2016 Servicios](https://www.microsoft.com/download/details.aspx?id=49492) páginas.

> [!NOTE]
> SSIS se instala con SQL Server, pero no se incluye en la versión Express de Hola. Para obtener información sobre qué aplicaciones se incluyen en las distintas versiones de SQL Server, consulte [Ediciones de SQL Server](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)
> 
> 

Para obtener materiales de aprendizaje sobre SSIS, consulte [Aprendizaje práctico para SSIS](http://www.microsoft.com/download/details.aspx?id=20766)

Para obtener información acerca de cómo tooget arriba y ejecución con SISS toobuild simple paquetes de extracción, transformación y carga (ETL), consulte [SSIS Tutorial: crear un paquete ETL sencillo](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Descargar el conjunto de datos de taxis de la ciudad de Nueva York
Hello ejemplo descrito aquí usa un conjunto de datos disponible públicamente--hello [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos. conjunto de datos de Hello consta de llevar a unos 173 millones en Nueva York taxi año Hola 2013. Existen dos tipos de datos: datos de los detalles de las carreras y datos sobre las tarifas. Como existe un archivo correspondiente a cada mes, tenemos, en total, 24 archivos, cada uno de los cuales tiene un tamaño de 2 GB sin comprimir.

## <a name="upload-data-tooazure-blob-storage"></a>Cargar el almacenamiento de blobs de datos tooAzure
feature pack local tooAzure del almacenamiento de blobs de datos de toomove mediante Hola SSIS, se utiliza una instancia de hello [ **tarea de carga de blobs de Azure**](https://msdn.microsoft.com/library/mt146776.aspx), se muestra aquí:

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

aquí se describen los parámetros de Hola que Hola tarea utiliza:

| Campo | Description |
| --- | --- |
| **AzureStorageConnection** |Especifica un administrador de conexiones de almacenamiento de Azure existente o crea un nuevo que hace referencia la cuenta de almacenamiento de Azure tooan que señala archivos de blob de hello toowhere se hospedan. |
| **BlobContainer** |Especifica el nombre de Hola Hola del contenedor de blobs que contiene los archivos de hello cargado como blobs. |
| **BlobDirectory** |Especifica el directorio de blob de Hola donde se almacena el archivo cargado Hola como un blob en bloques. directorio de blob de Hello es una estructura jerárquica virtual. Si ya existe el blob de hello, TI ia reemplazado. |
| **LocalDirectory** |Especifica Hola directorio local que contiene Hola archivos toobe cargado. |
| **FileName** |Especifica los archivos de tooselect de filtro de un nombre con el patrón de nombre especificado de Hola. Por ejemplo, MySheet\*.xls\* incluye archivos como MySheet001.xls y MySheetABC.xlsx |
| **TimeRangeFrom/TimeRangeTo** |Especifica un filtro de intervalo de tiempo. Se incluirán los archivos modificados después de *TimeRangeFrom* y antes de *TimeRangeTo*. |

> [!NOTE]
> Hola **AzureStorageConnection** credenciales deben hello y toobe correcta **BlobContainer** debe existir antes de que se intenta realizar la transferencia de Hola.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Cargar datos desde el almacenamiento de blobs de Azure
datos de toodownload de almacenamiento de tooon local de almacenamiento de blobs de Azure con SSIS, utilice una instancia de hello [tarea de carga de blobs de Azure](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Escenarios de SSIS-Azure más avanzados
feature pack de Hello SSIS permite más compleja toobe flujos controlada las tareas de empaquetado juntos. Por ejemplo, pudieron proporcionar los datos de blob de hello directamente en un clúster de HDInsight, cuyo resultado se pudieron descargar los blob tooa atrás y, a continuación, un almacenamiento local de tooon. SSIS puede ejecutar trabajos de Hive y Pig en un clúster de HDInsight, mediante el uso de conectores SSIS adicionales:

* toorun de clúster de un script de Hive en un HDInsight de Azure con SSIS, utilice [tarea de Hive de HDInsight de Azure](https://msdn.microsoft.com/library/mt146771.aspx).
* toorun de clúster de un script de Pig en un HDInsight de Azure con SSIS, utilice [tarea de Pig de HDInsight de Azure](https://msdn.microsoft.com/library/mt146781.aspx).

