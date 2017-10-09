---
title: "Tutorial de Data Factory: primera canalización de datos | Microsoft Docs"
description: "Este tutorial de Data Factory de Azure muestra cómo toocreate y programación de una factoría de datos que procesa los datos mediante el subárbol de script en un clúster de Hadoop."
services: data-factory
keywords: "Tutorial de Data Factory de Azure, clúster de Hadoop, Hive de Hadoop"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Tutorial: Compilar los datos primera canalización tootransform con clúster de Hadoop
> [!div class="op_single_selector"]
> * [Introducción y requisitos previos](data-factory-build-your-first-pipeline.md)
> * [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API de REST](data-factory-build-your-first-pipeline-using-rest-api.md)

En este tutorial, se crea una instancia de Azure Data Factory con una canalización de datos. canalización de Hello transforma los datos de entrada mediante la ejecución de script de Hive en un datos de salida de tooproduce de clúster de HDInsight de Azure (Hadoop).  

Este artículo proporciona información general y requisitos previos para el tutorial de Hola. Después de completar los requisitos previos de hello, puede hacer tutorial Hola mediante uno de hello después herramientas/SDK: portal de Azure, Visual Studio, PowerShell, la plantilla de administrador de recursos, API de REST. Seleccione una de las opciones de hello en la lista desplegable de hello en Hola principio (o) vínculos al final de Hola de este tutorial de artículo toodo hello mediante una de estas opciones.    

## <a name="tutorial-overview"></a>Información general del tutorial
En este tutorial, realizará Hola pasos:

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o varias canalizaciones de datos que mueven y procesan datos. 

    En este tutorial, creará una canalización de factoría de datos de Hola. 
2. Crear una **canalización**. Una canalización puede tener una o varias actividades (ejemplos: actividad de copia, actividad de Hive en HDInsight). Este ejemplo utiliza Hola actividad de HDInsight Hive que se ejecuta un script de Hive en un clúster de Hadoop de HDInsight. script de Hola crea primero una tabla que Hola de referencias de datos de registro sin procesar web almacenados en el almacenamiento de blobs de Azure y, a continuación, las particiones Hola datos sin procesar por año y mes.

    En este tutorial, canalización de hello usa datos de tootransform de actividad de Hive hello mediante la ejecución de una consulta de Hive en un clúster de Hadoop de HDInsight de Azure. 
3. Cree **servicios vinculados**. Para crear un servicio vinculado toolink un almacén de datos o una factoría de datos de toohello de servicio de proceso. Un almacén de datos, como el almacenamiento de Azure contiene los datos de entrada/salida de actividades en la canalización de Hola. Un servicio de proceso como un clúster de Hadoop de HDInsight procesa y transforma los datos.

    En este tutorial se crean dos servicios vinculados: **Azure Storage** y **Azure HDInsight**. Hola almacenamiento de Azure vinculados a los vínculos de servicio una cuenta de almacenamiento de Azure que contiene la factoría de datos de toohello de datos de entrada/salida de hello. HDInsight de Azure había vinculada vínculos de servicio en un clúster de HDInsight de Azure que está factoría de datos de uso tootransform datos toohello. 
3. Crear **conjuntos de datos**de entrada y salida. Un conjunto de datos de entrada representa la entrada de Hola para una actividad de canalización de Hola y un conjunto de datos de salida representa la salida de hello para la actividad de Hola.

    En este tutorial, Hola de entrada y salida de los conjuntos de datos especifican ubicaciones de entrada y Hola de datos de salida en almacenamiento de blobs de Azure. Hola servicio vinculado de almacenamiento de Azure especifica qué cuenta de almacenamiento de Azure es usar. Un conjunto de datos de entrada especifica donde se encuentran los archivos de entrada de Hola y un conjunto de datos de salida especifica donde se colocan los archivos de salida de hello. 


Vea [tooAzure Introducción factoría de datos](data-factory-introduction.md) artículo para obtener una descripción detallada de la factoría de datos de Azure.
  
Aquí es hello **vista de diagrama** de factoría de datos de ejemplo de Hola se crean en este tutorial. **MyFirstPipeline** tiene una actividad del tipo Hive que consume el conjunto de datos **AzureBlobInput** como entrada y genera el conjunto de datos **AzureBlobOutput** como salida. 

![Vista de diagrama en el tutorial de Data Factory](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


En este tutorial, **inputdata** carpeta de hello **adfgetstarted** contenedor de blobs de Azure contiene un archivo denominado input.log. Este archivo de registro tiene entradas de tres meses: enero, febrero y marzo de 2016. Aquí son filas de ejemplo de Hola para cada mes en el archivo de entrada de Hola. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Cuando se procesa el archivo hello canalización Hola con actividad de Hive de HDInsight, actividad hello ejecuta un script de Hive en clúster de HDInsight de Hola que las particiones de entrada de datos por año y mes. script de Hola crea tres carpetas de salida que contienen un archivo con las entradas de cada mes.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

De las líneas de ejemplo de Hola mostradas anteriormente, hello en primer lugar (con 2016-01-01) se escribe uno toohello 000000_0 archivo mes hello = 1 carpeta. De forma similar, hello otra se escribe toohello archivo mes hello = 2 hello y carpeta en tercer lugar se escribe uno toohello archivo mes hello = carpeta 3.  

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener Hola siguiendo los requisitos previos:

1. **Suscripción de Azure** : si no tiene ninguna, puede crear una cuenta de evaluación gratuita en un par de minutos. Vea hello [evaluación gratuita de](https://azure.microsoft.com/pricing/free-trial/) artículo sobre cómo obtener una cuenta de prueba gratuita.
2. **Almacenamiento de Azure** : usar una cuenta de almacenamiento de Azure estándar general para almacenar datos de hello en este tutorial. Si no tienes una cuenta de almacenamiento de Azure estándar general, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo. Una vez haya creado la cuenta de almacenamiento de hello, anote hello **nombre-cuenta** y **clave de acceso**. Consulte [Visualización y copia de las claves de acceso de almacenamiento](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Descargue y revise el archivo de consulta de Hive hello (**HQL**) ubicado en: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Esta consulta transforma los datos de salida de tooproduce de datos de entrada. 
4. Descargue y revise el archivo de entrada de ejemplo de Hola (**input.log**) ubicado en: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Crear un contenedor de blobs denominado **adfgetstarted** en Azure Blob Storage. 
6. Cargar **partitionweblogs.hql** archivo toohello **script** carpeta Hola **adfgetstarted** contenedor. Use herramientas como el [Explorador de Microsoft Azure Storage](http://storageexplorer.com/). 
7. Cargar **input.log** archivo toohello **inputdata** carpeta Hola **adfgetstarted** contenedor. 

Después de completar los requisitos previos de hello, seleccione uno de hello sigue herramientas/SDK toodo Hola tutorial: 

- [Portal de Azure](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Plantilla de Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
- [API de REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Azure Portal y Visual Studio proporcionan una forma de generar factorías de datos mediante GUI. Mientras que las opciones de PowerShell, la plantilla de Resource Manager y la API de REST proporcionan una forma de generar factorías de datos mediante scripts/programación.

> [!NOTE]
> canalización de datos de Hello en este tutorial transforma los datos de salida de tooproduce de datos de entrada. No copia datos de un almacén de datos de destino de origen datos almacén tooa. Para obtener un tutorial sobre cómo toocopy los datos mediante Data Factory de Azure, consulte [Tutorial: copiar los datos de la base de datos del almacenamiento de blobs tooSQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Se pueden encadenar dos actividades (ejecutar actividades de una tras otra) estableciendo el conjunto de datos de salida de hello de una actividad Hola de entrada de conjunto de datos del programa Hola a otra actividad. Para más información, consulte [Programación y ejecución en Data Factory](data-factory-scheduling-and-execution.md). 





  
