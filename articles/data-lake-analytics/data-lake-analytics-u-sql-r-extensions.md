---
title: "Extend U-SQL scripts with R in Azure Data Lake Analytics (Extensión de los scripts de U-SQL con R en Azure Data Lake Analytics) | Microsoft Docs"
description: "Obtenga información sobre cómo ejecutar código R en scripts de U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="dc09e-103">Tutorial: Introducción a la extensión de U-SQL con Python (Tutorial: Introducción a la extensión de U-SQL con R)</span><span class="sxs-lookup"><span data-stu-id="dc09e-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="dc09e-104">En el ejemplo siguiente se muestran los pasos básicos para implementar código R:</span><span class="sxs-lookup"><span data-stu-id="dc09e-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="dc09e-105">Uso de la instrucción `REFERENCE ASSEMBLY` para habilitar las extensiones de R para el script de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc09e-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="dc09e-106">Use la operación ` REDUCE` para la partición de datos de entrada de una clave.</span><span class="sxs-lookup"><span data-stu-id="dc09e-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="dc09e-107">Las extensiones de R para U-SQL incluyen un reductor integrado (`Extension.R.Reducer`) que ejecuta código R en cada vértice asignado al reductor.</span><span class="sxs-lookup"><span data-stu-id="dc09e-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="dc09e-108">Uso de tramas de datos con nombre dedicadas llamadas `inputFromUSQL` y `outputToUSQL `, respectivamente, para pasar datos entre U-SQL y R. Los nombres del identificador DataFrame de entrada y salida son fijos (es decir, los usuarios no pueden cambiar estos nombres predefinidos de los identificadores DataFrame de entrada y salida).</span><span class="sxs-lookup"><span data-stu-id="dc09e-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="dc09e-109">Incrustación de código R en el script de U-SQL</span><span class="sxs-lookup"><span data-stu-id="dc09e-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="dc09e-110">Mediante el parámetro de comando `Extension.R.Reducer`, puede insertar el código R de su script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc09e-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="dc09e-111">Por ejemplo, puede declarar el script de R como una variable de cadena y pasarla como un parámetro al reductor.</span><span class="sxs-lookup"><span data-stu-id="dc09e-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="dc09e-112">Mantenga el código R en un archivo aparte y haga referencia a él mediante el script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc09e-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="dc09e-113">En el ejemplo siguiente se ilustra un uso más complejo.</span><span class="sxs-lookup"><span data-stu-id="dc09e-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="dc09e-114">En este caso, el código R se implementa como RESOURCE que es el script de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc09e-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="dc09e-115">Guarde este código R como un archivo aparte.</span><span class="sxs-lookup"><span data-stu-id="dc09e-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="dc09e-116">Use un script U-SQL para implementar ese script R con la instrucción DEPLOY RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="dc09e-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="dc09e-117">Cómo se integra R con U-SQL</span><span class="sxs-lookup"><span data-stu-id="dc09e-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="dc09e-118">Tipos de datos</span><span class="sxs-lookup"><span data-stu-id="dc09e-118">Datatypes</span></span>
* <span data-ttu-id="dc09e-119">Las columnas de cadena y numéricas de U-SQL se convierten tal cual entre R DataFrame y U-SQL [tipos admitidos: `double`, `string`, `bool`, `integer` y `byte`].</span><span class="sxs-lookup"><span data-stu-id="dc09e-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="dc09e-120">El tipo de datos `Factor` no se admite en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc09e-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="dc09e-121">`byte[]` debe serializarse como `string` codificada en base64.</span><span class="sxs-lookup"><span data-stu-id="dc09e-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="dc09e-122">Las cadenas de U-SQL se pueden convertir en factores en el código R, una vez que U-SQL cree una trama de datos de entrada de R o mediante el establecimiento del parámetro reductor `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="dc09e-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="dc09e-123">Esquemas</span><span class="sxs-lookup"><span data-stu-id="dc09e-123">Schemas</span></span>
* <span data-ttu-id="dc09e-124">Los conjuntos de datos de U-SQL no pueden tener nombres de columna duplicados.</span><span class="sxs-lookup"><span data-stu-id="dc09e-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="dc09e-125">Los nombres de columna de conjuntos de datos de U-SQL deben ser cadenas.</span><span class="sxs-lookup"><span data-stu-id="dc09e-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="dc09e-126">Los nombres de columna deben ser los mismos en los scripts de U-SQL y de R.</span><span class="sxs-lookup"><span data-stu-id="dc09e-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="dc09e-127">La columna de solo lectura no puede formar parte de la trama de datos de salida,</span><span class="sxs-lookup"><span data-stu-id="dc09e-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="dc09e-128">ya que las columnas de solo lectura vuelven a insertarse automáticamente en la tabla de U-SQL si forma parte del esquema de salida de UDO.</span><span class="sxs-lookup"><span data-stu-id="dc09e-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="dc09e-129">Limitaciones funcionales</span><span class="sxs-lookup"><span data-stu-id="dc09e-129">Functional limitations</span></span>
* <span data-ttu-id="dc09e-130">No se puede crear una instancia dos veces del motor de R en el mismo proceso.</span><span class="sxs-lookup"><span data-stu-id="dc09e-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="dc09e-131">En la actualidad, U-SQL no admite UDO de combinación para la predicción mediante modelos particionados generados con UDO de reducción.</span><span class="sxs-lookup"><span data-stu-id="dc09e-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="dc09e-132">Los usuarios pueden declarar los modelos particionados como recurso y usarlos en su script de R (consulte el código de ejemplo `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="dc09e-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="dc09e-133">Versiones de R</span><span class="sxs-lookup"><span data-stu-id="dc09e-133">R Versions</span></span>
<span data-ttu-id="dc09e-134">Solo se admite R 3.2.2.</span><span class="sxs-lookup"><span data-stu-id="dc09e-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="dc09e-135">Módulos de R estándar</span><span class="sxs-lookup"><span data-stu-id="dc09e-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="dc09e-136">Limitaciones de tamaño de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="dc09e-136">Input and Output size limitations</span></span>
<span data-ttu-id="dc09e-137">Cada vértice tiene una cantidad limitada de memoria asignada a él.</span><span class="sxs-lookup"><span data-stu-id="dc09e-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="dc09e-138">Dado que las tramas de datos de entrada y salida deben existir en memoria en el código R, el tamaño total de la entrada y la salida no puede ser superior a 500 MB.</span><span class="sxs-lookup"><span data-stu-id="dc09e-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="dc09e-139">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="dc09e-139">Sample Code</span></span>
<span data-ttu-id="dc09e-140">Puede encontrar más código de ejemplo en su cuenta Data Lake Store después de instalar las extensiones U-SQL Advanced Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc09e-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="dc09e-141">Ruta de acceso a más código de ejemplo: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="dc09e-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="dc09e-142">Implementación de módulos de R personalizados con U-SQL</span><span class="sxs-lookup"><span data-stu-id="dc09e-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="dc09e-143">En primer lugar, cree un módulo personalizado de R, comprímalo y luego cargue este archivo comprimido en su almacén de ADL.</span><span class="sxs-lookup"><span data-stu-id="dc09e-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="dc09e-144">En el ejemplo, cargaremos magittr_1.5.zip en la raíz de la cuenta de ADLS predeterminada para la cuenta de ADLA que vamos a usar.</span><span class="sxs-lookup"><span data-stu-id="dc09e-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="dc09e-145">Una vez que cargue el módulo en el almacén de ADL, declárelo como que usa DEPLOY RESOURCE para ponerlo a disposición en su script U-SQL y llame a `install.packages` para instalarlo.</span><span class="sxs-lookup"><span data-stu-id="dc09e-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="dc09e-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc09e-146">Next Steps</span></span>
* [<span data-ttu-id="dc09e-147">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc09e-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="dc09e-148">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc09e-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="dc09e-149">Uso de funciones de ventana de U-SQL para trabajos de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc09e-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
