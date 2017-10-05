---
title: "Exploración de los datos de las tablas de Hive con consultas de Hive | Microsoft Docs"
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
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="63f61-103">Exploración de los datos de las tablas de Hive con consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="63f61-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="63f61-104">Este documento proporciona scripts de Hive de ejemplo que se usan para explorar los datos de las tablas de Hive en un clúster de Hadoop para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63f61-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="63f61-105">El siguiente **menú** vincula a temas que describen cómo usar herramientas para explorar los datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="63f61-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="63f61-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63f61-106">Prerequisites</span></span>
<span data-ttu-id="63f61-107">En este artículo se supone que ha:</span><span class="sxs-lookup"><span data-stu-id="63f61-107">This article assumes that you have:</span></span>

* <span data-ttu-id="63f61-108">Creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="63f61-108">Created an Azure storage account.</span></span> <span data-ttu-id="63f61-109">Si necesita instrucciones, consulte [Creación de una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="63f61-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="63f61-110">Aprovisionado un clúster de Hadoop personalizado con el servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63f61-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="63f61-111">Si necesita instrucciones, consulte [Personalización de clústeres de Hadoop de HDInsight de Azure para análisis avanzado](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="63f61-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="63f61-112">Se han cargado los datos en tablas de subárbol en clústeres de Hadoop de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="63f61-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="63f61-113">Si no es así, siga las instrucciones proporcionadas en [Crear y cargar datos en tablas de Hive](machine-learning-data-science-move-hive-tables.md) para cargar los datos en tablas de Hive primero.</span><span class="sxs-lookup"><span data-stu-id="63f61-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="63f61-114">Habilitado el acceso remoto al clúster.</span><span class="sxs-lookup"><span data-stu-id="63f61-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="63f61-115">Si necesita instrucciones, consulte [Acceso al nodo principal del clúster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="63f61-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="63f61-116">Si necesita instrucciones sobre cómo enviar consultas de Hive, consulte [Envío de consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="63f61-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="63f61-117">Ejemplo de scripts de consulta de Hive para la exploración de datos</span><span class="sxs-lookup"><span data-stu-id="63f61-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="63f61-118">Obtención del número de observaciones por partición `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="63f61-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="63f61-119">Obtención del número de observaciones por día `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="63f61-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="63f61-120">Obtención de los niveles de una columna de categorías </span><span class="sxs-lookup"><span data-stu-id="63f61-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="63f61-121">Obtención del número de niveles de combinación de dos columnas de categorías `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="63f61-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="63f61-122">Obtención de la distribución para columnas numéricas </span><span class="sxs-lookup"><span data-stu-id="63f61-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="63f61-123">Extraer registros de la combinación de dos tablas</span><span class="sxs-lookup"><span data-stu-id="63f61-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="63f61-124">Scripts de consulta adicionales para escenarios de datos de trayectos en taxi</span><span class="sxs-lookup"><span data-stu-id="63f61-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="63f61-125">También se ofrecen ejemplos de consultas que son específicos de escenarios de [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) en el [repositorio de GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="63f61-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="63f61-126">Estas consultas ya tienen el esquema de datos especificado y están listas para enviarse para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="63f61-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

