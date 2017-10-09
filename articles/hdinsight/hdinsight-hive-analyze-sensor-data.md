---
title: datos del sensor aaaAnalyze con Hive y Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooanalyze datos de sensor mediante Hola consola de consultas de Hive con HDInsight (Hadoop), a continuación, visualizar los datos de hello en Microsoft Excel con PowerView."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Analizar datos de sensor mediante Hola consola de consultas de Hive en Hadoop en HDInsight

Obtenga información acerca de cómo tooanalyze datos de sensor mediante Hola consola de consultas de Hive con HDInsight (Hadoop), a continuación, visualizar datos de hello en Microsoft Excel mediante el uso de Power View.

> [!IMPORTANT]
> Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows. HDInsight solo está disponible en Windows en versiones inferiores a la 3.4. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


En este ejemplo, usa datos históricos de Hive tooprocess e identifica los problemas con los sistemas de calefacción y aire acondicionado. En concreto, se puedan identificar sistemas se tooreliably no se puede mantener una temperatura de conjunto mediante la realización de hello siguientes tareas:

* Crear tablas de HIVE tooquery los datos almacenados en archivos de valores separados por comas (CSV).
* Crear consultas de HIVE tooanalyze datos de saludo.
* datos de hello analizado de tooretrieve, usar Microsoft Excel tooconnect tooHDInsight.
* datos de hello toovisualize, use Power View.

![Un diagrama de arquitectura de la solución de Hola](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de HDInsight (Hadoop): consulte [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener información sobre la creación de un clúster.
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel se usa para la visualización de datos con [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>ejemplo de Hola a toorun

1. Desde el explorador web, desplácese toohello después de la dirección URL: 

         https://<clustername>.azurehdinsight.net

    Reemplace `<clustername>` con el nombre de Hola de su clúster de HDInsight.

    Cuando se le solicite, autenticar mediante nombre de usuario de administrador de Hola y la contraseña que usó al aprovisionar este clúster.

2. Desde Hola página web que se abre, haga clic en hello **la Galería de introducción** ficha y, a continuación, en hello **soluciones con datos de ejemplo** categoría, haga clic en hello **análisis de datos de Sensor** ejemplo.

    ![Introducción a la galería de imágenes](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Siga las instrucciones de hello proporcionadas en el ejemplo de Hola Hola a toofinish página web.
