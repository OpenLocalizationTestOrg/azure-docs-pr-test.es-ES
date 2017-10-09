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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="59ae1-103">Exploración de los datos de las tablas de Hive con consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="59ae1-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="59ae1-104">Este documento proporciona ejemplos de scripts de Hive que son datos tooexplore usado en las tablas de Hive en un clúster de Hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59ae1-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="59ae1-105">siguiente Hello **menú** vincula tootopics que describen cómo toouse herramientas tooexplore datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="59ae1-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="59ae1-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="59ae1-106">Prerequisites</span></span>
<span data-ttu-id="59ae1-107">En este artículo se supone que ha:</span><span class="sxs-lookup"><span data-stu-id="59ae1-107">This article assumes that you have:</span></span>

* <span data-ttu-id="59ae1-108">Creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="59ae1-108">Created an Azure storage account.</span></span> <span data-ttu-id="59ae1-109">Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="59ae1-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="59ae1-110">Aprovisionar un clúster de Hadoop personalizado con hello servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59ae1-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="59ae1-111">Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="59ae1-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="59ae1-112">datos de Hello ha sido cargado tooHive tablas en clústeres de HDInsight Hadoop de Azure.</span><span class="sxs-lookup"><span data-stu-id="59ae1-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="59ae1-113">Si no es así, siga las instrucciones de hello en [carga y crear tablas de tooHive datos](machine-learning-data-science-move-hive-tables.md) tooupload datos tooHive tablas en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="59ae1-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="59ae1-114">Clúster de toohello de acceso remoto habilitado.</span><span class="sxs-lookup"><span data-stu-id="59ae1-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="59ae1-115">Si necesita instrucciones, consulte [Hola de acceso principal del nodo de clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="59ae1-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="59ae1-116">Si necesita instrucciones acerca de cómo toosubmit consultas de Hive, vea [cómo tooSubmit consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="59ae1-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="59ae1-117">Ejemplo de scripts de consulta de Hive para la exploración de datos</span><span class="sxs-lookup"><span data-stu-id="59ae1-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="59ae1-118">Obtener el recuento de Hola de observaciones por partición`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="59ae1-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="59ae1-119">Obtener el recuento de Hola de observaciones por día`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="59ae1-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="59ae1-120">Obtener niveles de hello en una columna de categorías</span><span class="sxs-lookup"><span data-stu-id="59ae1-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="59ae1-121">Obtener número de Hola de niveles de combinación de dos columnas de categorías`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="59ae1-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="59ae1-122">Obtener la distribución de Hola para columnas numéricas</span><span class="sxs-lookup"><span data-stu-id="59ae1-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="59ae1-123">Extraer registros de la combinación de dos tablas</span><span class="sxs-lookup"><span data-stu-id="59ae1-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="59ae1-124">Scripts de consulta adicionales para escenarios de datos de trayectos en taxi</span><span class="sxs-lookup"><span data-stu-id="59ae1-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="59ae1-125">Ejemplos de consultas que son específicas de demasiado[NYC Taxi recorridos datos](http://chriswhong.com/open-data/foil_nyc_taxi/) escenarios también se proporcionan en [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="59ae1-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="59ae1-126">Estas consultas ya tiene el esquema de datos especificado y está listo toobe enviado toorun.</span><span class="sxs-lookup"><span data-stu-id="59ae1-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

