---
title: "aaaUse Hive con Hadoop para análisis de registros de sitio Web - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se registra toouse Hive con el sitio Web de tooanalyze de HDInsight. Podrá utilizar un archivo de registro como entrada en una tabla de HDInsight y usar datos de HiveQL tooquery Hola."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Usar el subárbol con registros de tooanalyze de HDInsight basados en Windows de sitios Web
Obtenga información acerca de cómo se registra toouse HiveQL con HDInsight tooanalyze desde un sitio Web. Análisis de registro del sitio Web que pueden ser utilizado toosegment la audiencia basada en actividades similares, clasificar los visitantes del sitio por datos demográficos y toofind contenido Hola vean, los sitios Web de hello provienen de y así sucesivamente.

> [!IMPORTANT]
> Hola pasos de este trabajo único documento con clústeres de HDInsight basados en Windows. HDInsight solo está disponible en Windows en versiones inferiores a la 3.4. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

En este ejemplo, usará una HDInsight clúster tooanalyze sitio Web registro archivos tooget una visión general de frecuencia de Hola de toohello visita el sitio Web de sitios Web externos en un día. También generará un resumen de errores de sitio Web que los usuarios de hello experimentar. Aprenderá a:

* Conectar tooa almacenamiento de blobs de Azure, que contiene los archivos de registro del sitio Web.
* Crear tablas de HIVE tooquery esos registros.
* Crear consultas de HIVE tooanalyze datos de saludo.
* Usar Microsoft Excel tooconnect tooHDInsight (mediante datos de abrir base de datos ODBC (conectividad) tooretrieve Hola analizado.

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Requisitos previos
* Debe aprovisionar un clúster de Hadoop en HDInsight de Azure. Para obtener instrucciones, consulte [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].
* Debe tener instalado Microsoft Excel 2013 o Excel 2010.
* Debe tener [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport datos de Hive en Excel.

## <a name="toorun-hello-sample"></a>ejemplo de Hola a toorun
1. De hello [Portal de Azure](https://portal.azure.com/), de hello panel de inicio (si está anclado clúster de hello no existe), haga clic en el icono de clúster de Hola que servirá de ejemplo de Hola a toorun.
2. De hello clúster hoja, en **vínculos rápidos**, haga clic en **panel clúster**y, a continuación, desde hello **panel clúster** hoja, haga clic en **clúster de HDInsight Panel**. Como alternativa, puede abrir directamente panel hello mediante Hola después de la dirección URL:

         https://<clustername>.azurehdinsight.net

    Cuando se le solicite, autenticar mediante nombre de usuario de administrador de Hola y la contraseña que usó al aprovisionar el clúster de Hola.
3. Desde Hola página web que se abre, haga clic en hello **Galería de introducción** ficha y, a continuación, en hello **soluciones con datos de ejemplo** categoría, haga clic en hello **análisis de registro del sitio Web** ejemplo.
4. Siga las instrucciones de hello proporcionadas en el ejemplo de Hola Hola a toofinish página web.

## <a name="next-steps"></a>Pasos siguientes
Intente Hola según muestra: [analizar datos de sensor con Hive con HDInsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
