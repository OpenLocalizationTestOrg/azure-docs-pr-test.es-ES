---
title: "Importación de datos en Machine Learning Studio | Microsoft Docs"
description: "Cómo importar los datos en Estudio de aprendizaje automático de Azure desde varios orígenes de datos. Obtenga información sobre qué tipos de datos y formatos de datos son compatibles."
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
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="3299e-105">Importación de datos de entrenamiento en Estudio de aprendizaje automático de Azure desde varios orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="3299e-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="3299e-106">Para usar sus propios datos en Estudio de aprendizaje automático para desarrollar y entrenar una solución de análisis predictivo, puede:</span><span class="sxs-lookup"><span data-stu-id="3299e-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="3299e-107">Cargar datos de un **archivo local** con antelación desde el disco duro para crear un módulo de conjunto de datos en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3299e-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="3299e-108">Acceder a los datos desde cualquiera de los **orígenes de datos** en línea mientras su experimento se ejecuta con el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="3299e-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="3299e-109">Usar datos de otro **experimento** de Azure Machine Learning guardado como un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3299e-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="3299e-110">Usar los datos de instancia local de **SQL Server Database**.</span><span class="sxs-lookup"><span data-stu-id="3299e-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="3299e-111">Cada una de estas opciones se describen en uno de los temas del menú inferior.</span><span class="sxs-lookup"><span data-stu-id="3299e-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="3299e-112">En estos temas se muestra cómo importar datos desde estos diversos orígenes de datos para usarlos en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3299e-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="3299e-113">Existe una gran variedad de conjuntos de datos de ejemplo disponibles en Machine Learning Studio que puede usar como datos de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="3299e-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="3299e-114">Para obtener información al respecto, consulte [Uso de los conjuntos de datos de ejemplo en Estudio de aprendizaje automático de Azure](machine-learning-use-sample-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3299e-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="3299e-115">En este tema de introducción también se explica cómo obtener datos listos para su uso en Machine Learning Studio de aprendizaje automático y se describe qué tipos y formatos de datos son compatibles.</span><span class="sxs-lookup"><span data-stu-id="3299e-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="3299e-116">Preparación de los datos para usarlos en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3299e-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="3299e-117">Estudio de aprendizaje automático está diseñado para trabajar con datos rectangulares o tabulares, como datos de texto delimitados o datos estructurados de una base de datos, aunque en algunas circunstancias, es posible usar datos no rectangulares.</span><span class="sxs-lookup"><span data-stu-id="3299e-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="3299e-118">Se recomienda que los datos estén relativamente limpios.</span><span class="sxs-lookup"><span data-stu-id="3299e-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="3299e-119">Es decir, querrá ocuparse de problemas como las cadenas sin comillas antes de cargar los datos en su experimento.</span><span class="sxs-lookup"><span data-stu-id="3299e-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="3299e-120">Sin embargo, hay módulos disponibles en Estudio de aprendizaje automáticos que le permitirán manipular levemente los datos en el experimento.</span><span class="sxs-lookup"><span data-stu-id="3299e-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="3299e-121">Dependiendo de los algoritmos de aprendizaje automático que usará, es posible que deba decidir cómo controlar los problemas estructurales de los datos, como valores que faltan y datos esparcidos y existen módulos que pueden ayudar en esto.</span><span class="sxs-lookup"><span data-stu-id="3299e-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="3299e-122">Observe la sección **Transformación de datos** de la paleta de módulos para los módulos que realizan estas funciones.</span><span class="sxs-lookup"><span data-stu-id="3299e-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="3299e-123">En cualquier momento del experimento puede ver o descargar los datos que genera un módulo con un clic en el puerto de salida.</span><span class="sxs-lookup"><span data-stu-id="3299e-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="3299e-124">Dependiendo del módulo, es posible que haya distintas opciones de descarga disponibles, o bien que se puedan visualizar los datos dentro del explorador web en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3299e-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="3299e-125">Tipos y formatos de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="3299e-125">Data formats and data types supported</span></span>
<span data-ttu-id="3299e-126">Puede importar diversos tipos de datos al experimento, dependiendo del mecanismo que usa para importar los datos y de dónde provienen estos:</span><span class="sxs-lookup"><span data-stu-id="3299e-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="3299e-127">Texto sin formato (.txt)</span><span class="sxs-lookup"><span data-stu-id="3299e-127">Plain text (.txt)</span></span>
* <span data-ttu-id="3299e-128">Valores separados por coma (CSV) con un encabezado (.csv) o sin encabezado (.nh.csv)</span><span class="sxs-lookup"><span data-stu-id="3299e-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="3299e-129">Valores separados con tabulaciones (TSV) con un encabezado (.tsv) o sin encabezado (.nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="3299e-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="3299e-130">Archivo de Excel</span><span class="sxs-lookup"><span data-stu-id="3299e-130">Excel file</span></span>
* <span data-ttu-id="3299e-131">Tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="3299e-131">Azure table</span></span>
* <span data-ttu-id="3299e-132">Tabla de Hive</span><span class="sxs-lookup"><span data-stu-id="3299e-132">Hive table</span></span>
* <span data-ttu-id="3299e-133">Tabla de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3299e-133">SQL database table</span></span>
* <span data-ttu-id="3299e-134">Valores de OData</span><span class="sxs-lookup"><span data-stu-id="3299e-134">OData values</span></span>
* <span data-ttu-id="3299e-135">Datos SVMLight (.svmlight) (consulte la [definición de SVMLight](http://svmlight.joachims.org/) para obtener más información sobre el formato)</span><span class="sxs-lookup"><span data-stu-id="3299e-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="3299e-136">Datos de formato de archivo con relación de atributo (ARFF) (.arff) (consulte la [definición de ARFF](http://weka.wikispaces.com/ARFF) si desea ver información sobre el formato)</span><span class="sxs-lookup"><span data-stu-id="3299e-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="3299e-137">Archivo ZIP (.zip)</span><span class="sxs-lookup"><span data-stu-id="3299e-137">Zip file (.zip)</span></span>
* <span data-ttu-id="3299e-138">Archivo de área de trabajo u objeto de R (.RData)</span><span class="sxs-lookup"><span data-stu-id="3299e-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="3299e-139">Si importa datos en un formato distinto de ARFF que incluyan metadatos, Estudio de aprendizaje automático usa estos metadatos para definir el tipo de datos y encabezado de cada columna.</span><span class="sxs-lookup"><span data-stu-id="3299e-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="3299e-140">Si importa datos en formato TSV o CSV que no incluyan estos metadatos, Estudio de aprendizaje automático infiere el tipo de datos de cada columna tomando una muestra de los mismos.</span><span class="sxs-lookup"><span data-stu-id="3299e-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="3299e-141">Si los datos no tienen encabezados de columna, Estudio de aprendizaje automático proporciona nombres predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3299e-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="3299e-142">Puede especificar o cambiar explícitamente los encabezados y los tipos de datos de las columnas usando el módulo [Editar metadatos][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3299e-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="3299e-143">Estudio de aprendizaje automático reconoce los siguientes **tipos de datos** :</span><span class="sxs-lookup"><span data-stu-id="3299e-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="3299e-144">String</span><span class="sxs-lookup"><span data-stu-id="3299e-144">String</span></span>
* <span data-ttu-id="3299e-145">Entero</span><span class="sxs-lookup"><span data-stu-id="3299e-145">Integer</span></span>
* <span data-ttu-id="3299e-146">Doble</span><span class="sxs-lookup"><span data-stu-id="3299e-146">Double</span></span>
* <span data-ttu-id="3299e-147">Booleano</span><span class="sxs-lookup"><span data-stu-id="3299e-147">Boolean</span></span>
* <span data-ttu-id="3299e-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="3299e-148">DateTime</span></span>
* <span data-ttu-id="3299e-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3299e-149">TimeSpan</span></span>

<span data-ttu-id="3299e-150">Machine Learning Studio usa un tipo de datos interno llamado ***Tabla de datos*** para pasar datos entre los módulos.</span><span class="sxs-lookup"><span data-stu-id="3299e-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="3299e-151">Puede convertir explícitamente sus datos en formato de tabla de datos con el módulo [Convertir al conjunto de datos][convert-to-dataset].</span><span class="sxs-lookup"><span data-stu-id="3299e-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="3299e-152">Todo módulo que acepta formatos distintos de Tabla de datos convertirá los datos a Tabla de datos de manera silenciosa antes de pasarlos al módulo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3299e-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="3299e-153">En caso de ser necesario, puede convertir el formato Tabla de datos de vuelta al formato CSV, TSV, ARFF o SVMLight mediante el uso de otros módulos de conversión.</span><span class="sxs-lookup"><span data-stu-id="3299e-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="3299e-154">Consulte la sección **Conversiones de formatos de datos** de la paleta de módulos para ver los módulos que realizan estas funciones.</span><span class="sxs-lookup"><span data-stu-id="3299e-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
