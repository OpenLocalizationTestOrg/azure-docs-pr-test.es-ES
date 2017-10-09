---
title: aaaExplore datos en las tablas de Hive con consultas de Hive | Documentos de Microsoft
description: "Exploración de los datos de las tablas de Hive con consultas de Hive."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Exploración de los datos de las tablas de Hive con consultas de Hive
Este documento proporciona ejemplos de scripts de Hive que son datos tooexplore usado en las tablas de Hive en un clúster de Hadoop de HDInsight.

siguiente Hello **menú** vincula tootopics que describen cómo toouse herramientas tooexplore datos desde varios entornos de almacenamiento.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Requisitos previos
En este artículo se supone que ha:

* Creado una cuenta de almacenamiento de Azure. Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Aprovisionar un clúster de Hadoop personalizado con hello servicio HDInsight. Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).
* datos de Hello ha sido cargado tooHive tablas en clústeres de HDInsight Hadoop de Azure. Si no es así, siga las instrucciones de hello en [carga y crear tablas de tooHive datos](machine-learning-data-science-move-hive-tables.md) tooupload datos tooHive tablas en primer lugar.
* Clúster de toohello de acceso remoto habilitado. Si necesita instrucciones, consulte [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Si necesita instrucciones acerca de cómo toosubmit consultas de Hive, vea [cómo tooSubmit consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Ejemplo de scripts de consulta de Hive para la exploración de datos
1. Obtener el recuento de Hola de observaciones por partición`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Obtener el recuento de Hola de observaciones por día`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Obtener niveles de hello en una columna de categorías  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Obtener número de Hola de niveles de combinación de dos columnas de categorías`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Obtener la distribución de Hola para columnas numéricas  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Extraer registros de la combinación de dos tablas
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Scripts de consulta adicionales para escenarios de datos de trayectos en taxi
Ejemplos de consultas que son específicas de demasiado[NYC Taxi recorridos datos](http://chriswhong.com/open-data/foil_nyc_taxi/) escenarios también se proporcionan en [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Estas consultas ya tiene el esquema de datos especificado y está listo toobe enviado toorun.

