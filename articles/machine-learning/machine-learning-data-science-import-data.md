---
title: "datos de aaaImport en estudio de aprendizaje automático | Documentos de Microsoft"
description: "¿Cómo tooimport los datos en estudio de aprendizaje automático de Azure desde varios orígenes de datos. Obtenga información sobre qué tipos de datos y formatos de datos son compatibles."
keywords: "importar datos, formato de datos, tipos de datos, orígenes de datos, datos de entrenamiento"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="f9059-105">Importación de datos de entrenamiento en Estudio de aprendizaje automático de Azure desde varios orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="f9059-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="f9059-106">toouse sus propios datos en estudio de aprendizaje automático toodevelop y entrenar una solución de análisis predictivos, puede:</span><span class="sxs-lookup"><span data-stu-id="f9059-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="f9059-107">cargar datos desde una **archivo local** de tiempo de la unidad de disco duro toocreate un módulo de conjunto de datos en el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="f9059-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="f9059-108">acceso a datos de uno de varios **orígenes de datos en línea** mientras está ejecutando el experimento usando hello [importar datos] [ import-data] módulo</span><span class="sxs-lookup"><span data-stu-id="f9059-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="f9059-109">Usar datos de otro **experimento** de Azure Machine Learning guardado como un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f9059-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="f9059-110">Usar los datos de instancia local de **SQL Server Database**.</span><span class="sxs-lookup"><span data-stu-id="f9059-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="f9059-111">Cada una de estas opciones se describe en uno de los temas de hello en el menú de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="f9059-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="f9059-112">Estos temas muestra cómo toouse en estudio de aprendizaje automático de los orígenes de datos de tooimport de estos datos distintos.</span><span class="sxs-lookup"><span data-stu-id="f9059-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="f9059-113">Existe una gran variedad de conjuntos de datos de ejemplo disponibles en Machine Learning Studio que puede usar como datos de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="f9059-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="f9059-114">Para obtener información al respecto, consulte [usar conjuntos de datos de ejemplo de Hola en estudio de aprendizaje automático de Azure](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="f9059-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="f9059-115">Este tema de Introducción también describe cómo tooget datos listos para usar en estudio de aprendizaje automático y se admiten los tipos de datos y formatos de datos.</span><span class="sxs-lookup"><span data-stu-id="f9059-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="f9059-116">Preparación de los datos para usarlos en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="f9059-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="f9059-117">Estudio de aprendizaje automático es toowork diseñada con datos rectangulares o tabulares, como datos de texto que se delimitan o estructura de una base de datos, aunque en algunas circunstancias se pueden usar datos no rectangulares.</span><span class="sxs-lookup"><span data-stu-id="f9059-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="f9059-118">Se recomienda que los datos estén relativamente limpios.</span><span class="sxs-lookup"><span data-stu-id="f9059-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="f9059-119">Es decir, le interesará tootake atención problemas tales como las cadenas sin comillas antes de cargar datos de hello en el experimento.</span><span class="sxs-lookup"><span data-stu-id="f9059-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="f9059-120">Sin embargo, hay módulos disponibles en Estudio de aprendizaje automáticos que le permitirán manipular levemente los datos en el experimento.</span><span class="sxs-lookup"><span data-stu-id="f9059-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="f9059-121">Dependiendo de los algoritmos de aprendizaje automático de Hola que vamos a usar, puede que necesite toodecide cómo podrá controlar problemas estructurales de datos como los valores que faltan y datos dispersos, y hay módulos que pueden ayudar a que.</span><span class="sxs-lookup"><span data-stu-id="f9059-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="f9059-122">Buscar en hello **transformación de datos** sección de la paleta de módulo de Hola para módulos que llevan a cabo estas funciones.</span><span class="sxs-lookup"><span data-stu-id="f9059-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="f9059-123">Puede ver o descargar datos Hola generado por un módulo haciendo clic en el puerto de salida de hello en cualquier momento en el experimento.</span><span class="sxs-lookup"><span data-stu-id="f9059-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="f9059-124">Función de módulo de hello, puede haber descarga diferentes opciones disponibles o es posible que los datos de hello toovisualize pueda dentro del explorador web en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="f9059-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="f9059-125">Tipos y formatos de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="f9059-125">Data formats and data types supported</span></span>
<span data-ttu-id="f9059-126">Puede importar un número de tipos de datos en el experimento, dependiendo de qué mecanismo use datos tooimport y donde procede de:</span><span class="sxs-lookup"><span data-stu-id="f9059-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="f9059-127">Texto sin formato (.txt)</span><span class="sxs-lookup"><span data-stu-id="f9059-127">Plain text (.txt)</span></span>
* <span data-ttu-id="f9059-128">Valores separados por coma (CSV) con un encabezado (.csv) o sin encabezado (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="f9059-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="f9059-129">Valores separados con tabulaciones (TSV) con un encabezado (.tsv) o sin encabezado (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="f9059-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="f9059-130">Archivo de Excel</span><span class="sxs-lookup"><span data-stu-id="f9059-130">Excel file</span></span>
* <span data-ttu-id="f9059-131">Tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="f9059-131">Azure table</span></span>
* <span data-ttu-id="f9059-132">Tabla de Hive</span><span class="sxs-lookup"><span data-stu-id="f9059-132">Hive table</span></span>
* <span data-ttu-id="f9059-133">Tabla de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f9059-133">SQL database table</span></span>
* <span data-ttu-id="f9059-134">Valores de OData</span><span class="sxs-lookup"><span data-stu-id="f9059-134">OData values</span></span>
* <span data-ttu-id="f9059-135">Datos de SVMLight (.svmlight) (vea hello [SVMLight definición](http://svmlight.joachims.org/) para obtener información de formato)</span><span class="sxs-lookup"><span data-stu-id="f9059-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="f9059-136">Atributo de datos de formato de archivo de relación (ARFF) (.arff) (vea hello [definición ARFF](http://weka.wikispaces.com/ARFF) para obtener información de formato)</span><span class="sxs-lookup"><span data-stu-id="f9059-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="f9059-137">Archivo ZIP (.zip)</span><span class="sxs-lookup"><span data-stu-id="f9059-137">Zip file (.zip)</span></span>
* <span data-ttu-id="f9059-138">Archivo de área de trabajo u objeto de R (.RData)</span><span class="sxs-lookup"><span data-stu-id="f9059-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="f9059-139">Si importa los datos en un formato como ARFF que incluya los metadatos, estudio de aprendizaje automático utiliza este encabezado de metadatos toodefine Hola y el tipo de datos de cada columna.</span><span class="sxs-lookup"><span data-stu-id="f9059-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="f9059-140">Si importa los datos como formato TSV o CSV que no incluya estos metadatos, estudio de aprendizaje automático deduce el tipo de datos de Hola para cada columna mediante el muestreo de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9059-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="f9059-141">Si los datos de hello también no tienen encabezados de columna, estudio de aprendizaje automático proporciona nombres predeterminados.</span><span class="sxs-lookup"><span data-stu-id="f9059-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="f9059-142">Puede especificar explícitamente o cambiar Hola encabezados y tipos de datos para las columnas con hello [editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f9059-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="f9059-143">siguiente Hello **tipos de datos** reconocidos por estudio de aprendizaje automático:</span><span class="sxs-lookup"><span data-stu-id="f9059-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="f9059-144">String</span><span class="sxs-lookup"><span data-stu-id="f9059-144">String</span></span>
* <span data-ttu-id="f9059-145">Entero</span><span class="sxs-lookup"><span data-stu-id="f9059-145">Integer</span></span>
* <span data-ttu-id="f9059-146">Doble</span><span class="sxs-lookup"><span data-stu-id="f9059-146">Double</span></span>
* <span data-ttu-id="f9059-147">Booleano</span><span class="sxs-lookup"><span data-stu-id="f9059-147">Boolean</span></span>
* <span data-ttu-id="f9059-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="f9059-148">DateTime</span></span>
* <span data-ttu-id="f9059-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f9059-149">TimeSpan</span></span>

<span data-ttu-id="f9059-150">Estudio de aprendizaje automático utiliza un tipo de datos interno denominado ***tabla de datos*** datos toopass entre módulos.</span><span class="sxs-lookup"><span data-stu-id="f9059-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="f9059-151">Puede convertir explícitamente los datos en formato de tabla de datos mediante hello [convertir tooDataset] [ convert-to-dataset] módulo.</span><span class="sxs-lookup"><span data-stu-id="f9059-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="f9059-152">Cualquier módulo que acepta formatos distintos de la tabla de datos, Hola datos tooData tabla se convertirá en modo silencioso antes de pasarlo toohello siguiente módulo.</span><span class="sxs-lookup"><span data-stu-id="f9059-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="f9059-153">En caso de ser necesario, puede convertir el formato Tabla de datos de vuelta al formato CSV, TSV, ARFF o SVMLight mediante el uso de otros módulos de conversión.</span><span class="sxs-lookup"><span data-stu-id="f9059-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="f9059-154">Buscar en hello **conversiones de formato de datos** sección de la paleta de módulo de Hola para módulos que llevan a cabo estas funciones.</span><span class="sxs-lookup"><span data-stu-id="f9059-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
