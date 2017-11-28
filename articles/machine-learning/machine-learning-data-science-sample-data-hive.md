---
title: aaaSample datos en tablas de HDInsight Hive de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="762e3-103">Muestreo de datos en tablas de HDInsight Hive de Azure</span><span class="sxs-lookup"><span data-stu-id="762e3-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="762e3-104">En este artículo, se describen los datos de ejemplo de toodown cómo almacenados en tablas de HDInsight Hive de Azure usan consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="762e3-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="762e3-105">Se explican tres métodos de muestreo normalmente utilizados:</span><span class="sxs-lookup"><span data-stu-id="762e3-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="762e3-106">Muestreo aleatorio uniforme</span><span class="sxs-lookup"><span data-stu-id="762e3-106">Uniform random sampling</span></span>
* <span data-ttu-id="762e3-107">Muestreo aleatorio por grupos</span><span class="sxs-lookup"><span data-stu-id="762e3-107">Random sampling by groups</span></span>
* <span data-ttu-id="762e3-108">Muestreo estratificado</span><span class="sxs-lookup"><span data-stu-id="762e3-108">Stratified sampling</span></span>

<span data-ttu-id="762e3-109">siguiente Hello **menú** vincula tootopics que describen cómo toosample datos desde varios entornos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="762e3-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="762e3-110">**¿Por qué realizar un muestreo de los datos?**</span><span class="sxs-lookup"><span data-stu-id="762e3-110">**Why sample your data?**</span></span>
<span data-ttu-id="762e3-111">Si piensa tooanalyze de conjunto de datos de hello es grande, normalmente es un tooreduce de datos de ejemplo toodown Hola buena idea tooa más pequeño pero representativo y más fáciles de administrar el tamaño.</span><span class="sxs-lookup"><span data-stu-id="762e3-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="762e3-112">Esto facilita la comprensión y exploración de los datos, y el diseño de características.</span><span class="sxs-lookup"><span data-stu-id="762e3-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="762e3-113">Su función en hello proceso de ciencia de datos de equipo es tooenable la creación de prototipos rápida de las funciones de procesamiento de datos de Hola y modelos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="762e3-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="762e3-114">Esta tarea de muestreo es un paso en hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="762e3-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="762e3-115">¿Cómo toosubmit consultas de Hive</span><span class="sxs-lookup"><span data-stu-id="762e3-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="762e3-116">Las consultas de Hive pueden enviarse desde la consola de línea de comandos de Hadoop de hello en del nodo principal del clúster de Hadoop de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="762e3-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="762e3-117">toodo esto, inicie sesión en el nodo principal de Hola de clúster de Hadoop de hello, abra Hola consola de línea de comandos de Hadoop así como enviar consultas de Hive Hola desde allí.</span><span class="sxs-lookup"><span data-stu-id="762e3-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="762e3-118">Para obtener instrucciones sobre cómo enviar consultas de Hive en la consola de línea de comandos de Hadoop de hello, consulte [cómo tooSubmit consultas de Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="762e3-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="762e3-119"><a name="uniform"></a> Muestra aleatoria uniforme</span><span class="sxs-lookup"><span data-stu-id="762e3-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="762e3-120">Muestreo aleatorio uniforme significa que cada fila de conjunto de datos de hello tiene la misma probabilidad de que se va a muestrear.</span><span class="sxs-lookup"><span data-stu-id="762e3-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="762e3-121">Esto puede implementarse mediante la adición de un conjunto de datos de campo adicional rand() toohello en la consulta "select" interna de Hola y de Hola externa consulta "select" esa condición en ese campo aleatorio.</span><span class="sxs-lookup"><span data-stu-id="762e3-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="762e3-122">Aquí se muestra una consulta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="762e3-122">Here is an example query:</span></span>

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

<span data-ttu-id="762e3-123">En este caso, `<sample rate, 0-1>` especifica la proporción de Hola de registros que desean que los usuarios de hello toosample.</span><span class="sxs-lookup"><span data-stu-id="762e3-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="762e3-124"><a name="group"></a> Muestreo aleatorio por grupos</span><span class="sxs-lookup"><span data-stu-id="762e3-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="762e3-125">Cuando los datos de categorías de muestreo, puede que desee tooeither incluir o excluir todas las instancias de Hola de algún valor de una variable de categoría determinado.</span><span class="sxs-lookup"><span data-stu-id="762e3-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="762e3-126">Esto es lo que significa "muestreo por grupos".</span><span class="sxs-lookup"><span data-stu-id="762e3-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="762e3-127">Por ejemplo, si tiene una variable de categoría "Estado", que tiene valores de Nueva York, MA, CA, NJ, PA, etcetera, desea que los registros de hello mismo estado ser siempre juntos, si están muestreadas o no.</span><span class="sxs-lookup"><span data-stu-id="762e3-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="762e3-128">Aquí se muestra una consulta de ejemplo que realiza un muestreo por grupo:</span><span class="sxs-lookup"><span data-stu-id="762e3-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="762e3-129"><a name="stratified"></a>Muestreo estratificado</span><span class="sxs-lookup"><span data-stu-id="762e3-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="762e3-130">Muestreo aleatorio es estratificado con sentido tooa variable de categoría cuando las muestras Hola obtenidas tienen valores de categorías es que se encuentran en hello misma relación como en la población de hello primario desde qué Hola se obtuvieron los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="762e3-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="762e3-131">Uso de Hola mismo ejemplo anterior, supongamos que los datos tienen subcarpetas rellenados por los Estados, digamos NJ tiene 100 observaciones, NY tiene 60 observaciones y WA tiene 300 observaciones.</span><span class="sxs-lookup"><span data-stu-id="762e3-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="762e3-132">Si se especifica la velocidad de Hola de estratificado muestreo toobe 0,5, a continuación, hello muestra obtenido debe tener aproximadamente 50, 30 y 150 observaciones de nueva Jersey y Nueva York, WA respectivamente.</span><span class="sxs-lookup"><span data-stu-id="762e3-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="762e3-133">Aquí se muestra una consulta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="762e3-133">Here is an example query:</span></span>

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


<span data-ttu-id="762e3-134">Para obtener información sobre los métodos de muestreo más avanzados que están disponibles en Hive, consulte [Manual de lenguaje: muestreo](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="762e3-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

