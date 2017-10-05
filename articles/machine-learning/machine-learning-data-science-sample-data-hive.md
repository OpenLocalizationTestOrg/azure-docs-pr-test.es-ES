---
title: Muestreo de datos en tablas de HDInsight Hive de Azure | Microsoft Docs
description: "Reducción del muestreo de datos en tablas de HDInsight Hive (Hadopop) de Azure"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="64c26-103">Muestreo de datos en tablas de HDInsight Hive de Azure</span><span class="sxs-lookup"><span data-stu-id="64c26-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="64c26-104">En este artículo, se describe cómo reducir la muestra de datos almacenados en tablas de HDInsight Hive de Azure mediante consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="64c26-104">In this article, we describe how to down-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="64c26-105">Se explican tres métodos de muestreo normalmente utilizados:</span><span class="sxs-lookup"><span data-stu-id="64c26-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="64c26-106">Muestreo aleatorio uniforme</span><span class="sxs-lookup"><span data-stu-id="64c26-106">Uniform random sampling</span></span>
* <span data-ttu-id="64c26-107">Muestreo aleatorio por grupos</span><span class="sxs-lookup"><span data-stu-id="64c26-107">Random sampling by groups</span></span>
* <span data-ttu-id="64c26-108">Muestreo estratificado</span><span class="sxs-lookup"><span data-stu-id="64c26-108">Stratified sampling</span></span>

<span data-ttu-id="64c26-109">El siguiente **menú** está vinculado a temas que describen cómo realizar un muestreo de datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="64c26-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="64c26-110">**¿Por qué realizar un muestreo de los datos?**</span><span class="sxs-lookup"><span data-stu-id="64c26-110">**Why sample your data?**</span></span>
<span data-ttu-id="64c26-111">Si el conjunto de datos que pretende analizar es grande, es recomendable reducirlo a un tamaño más pequeño, pero representativo, que sea más manejable.</span><span class="sxs-lookup"><span data-stu-id="64c26-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="64c26-112">Esto facilita la comprensión y exploración de los datos, y el diseño de características.</span><span class="sxs-lookup"><span data-stu-id="64c26-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="64c26-113">Su rol en el proceso de ciencia de datos en equipos es permitir la rápida creación de prototipos de las funciones de procesamiento de datos y de los modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="64c26-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="64c26-114">Esta tarea de muestreo es un paso en el [proceso de ciencia de datos en equipos (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="64c26-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="64c26-115">Cómo enviar consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="64c26-115">How to submit Hive queries</span></span>
<span data-ttu-id="64c26-116">Las consultas de subárbol se pueden enviar desde la consola de línea de comandos de Hadoop del nodo principal del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="64c26-116">Hive queries can be submitted from the Hadoop Command Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="64c26-117">Para ello, inicie sesión en el nodo principal del clúster de Hadoop, abra la consola de la línea de comandos de Hadoop y envíe las consultas de Hive desde allí.</span><span class="sxs-lookup"><span data-stu-id="64c26-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="64c26-118">Para obtener instrucciones sobre el envío de consultas de Hive en la consola de línea de comandos de Hadoop, consulte [Envío de consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="64c26-118">For instructions on submitting Hive queries in the Hadoop Command Line console, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="64c26-119"><a name="uniform"></a> Muestra aleatoria uniforme</span><span class="sxs-lookup"><span data-stu-id="64c26-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="64c26-120">El muestreo aleatorio uniforme implica que cada fila del conjunto de datos tiene la misma probabilidad de muestreo.</span><span class="sxs-lookup"><span data-stu-id="64c26-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="64c26-121">Esto se puede implementar añadiendo un campo adicional de rand() al conjunto de datos en la consulta "select" interna, y en la consulta "select" externa esa condición en ese campo aleatorio.</span><span class="sxs-lookup"><span data-stu-id="64c26-121">This can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="64c26-122">Aquí se muestra una consulta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64c26-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="64c26-123">En este caso, `<sample rate, 0-1>` especifica la proporción de registros que los usuarios quieren usar como muestra.</span><span class="sxs-lookup"><span data-stu-id="64c26-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <span data-ttu-id="64c26-124"><a name="group"></a> Muestreo aleatorio por grupos</span><span class="sxs-lookup"><span data-stu-id="64c26-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="64c26-125">Cuando se realiza un muestreo de datos de categoría, podría querer incluir o excluir todas las instancias de algún valor concreto de una variable de categoría.</span><span class="sxs-lookup"><span data-stu-id="64c26-125">When sampling categorical data, you may want to either include or exclude all of the instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="64c26-126">Esto es lo que significa "muestreo por grupos".</span><span class="sxs-lookup"><span data-stu-id="64c26-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="64c26-127">Por ejemplo, si tiene una variable de categoría "Estado", que tiene como valores NY, MA, CA, NJ, PA, etc., querrá que los registros de un mismo estado estén siempre juntos, ya están muestreados o no.</span><span class="sxs-lookup"><span data-stu-id="64c26-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of the same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="64c26-128">Aquí se muestra una consulta de ejemplo que realiza un muestreo por grupo:</span><span class="sxs-lookup"><span data-stu-id="64c26-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="64c26-129"><a name="stratified"></a>Muestreo estratificado</span><span class="sxs-lookup"><span data-stu-id="64c26-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="64c26-130">El muestreo aleatorio se estratifica con respecto a una variable de categoría cuando las muestras obtenidas tienen valores de esa categoría que se encuentran en la misma proporción que en la población original de la que se obtuvieron las muestras.</span><span class="sxs-lookup"><span data-stu-id="64c26-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have values of that categorical that are in the same ratio as in the parent population from which the samples were obtained.</span></span> <span data-ttu-id="64c26-131">En el mismo ejemplo que el anterior, suponga que los datos tienen subpoblaciones según los estados; por ejemplo, NJ tiene 100 observaciones, NY tiene 60 observaciones y WA tiene 300 observaciones.</span><span class="sxs-lookup"><span data-stu-id="64c26-131">Using the same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="64c26-132">Si especifica que la tasa de muestreo estratificado sea 0,5, la muestra obtenida debería tener aproximadamente 50, 30 y 150 observaciones de NJ, NY y WA, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="64c26-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="64c26-133">Aquí se muestra una consulta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64c26-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="64c26-134">Para obtener información sobre los métodos de muestreo más avanzados que están disponibles en Hive, consulte [Manual de lenguaje: muestreo](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="64c26-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

