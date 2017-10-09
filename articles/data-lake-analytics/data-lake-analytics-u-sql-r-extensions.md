---
title: "aaaExtend U-SQL scripts con R en análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorun R código de secuencias de comandos SQL U"
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
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="e5ba6-103">Tutorial: Introducción a la extensión de U-SQL con Python (Tutorial: Introducción a la extensión de U-SQL con R)</span><span class="sxs-lookup"><span data-stu-id="e5ba6-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="e5ba6-104">Hola siguiente ejemplo ilustra Hola pasos básicos para implementar código R:</span><span class="sxs-lookup"><span data-stu-id="e5ba6-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="e5ba6-105">Hola de uso `REFERENCE ASSEMBLY` extensiones de tooenable R de instrucción para hello Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="e5ba6-106">Use la` REDUCE` Hola de operación toopartition los datos en una clave de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="e5ba6-107">las extensiones de Hello R para SQL U incluyen un reductor integrado (`Extension.R.Reducer`) que ejecuta código R en cada reductor de toohello vértices asignado.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="e5ba6-108">Uso de dedicado denominado tramas de datos denominadas `inputFromUSQL` y `outputToUSQL `respectivamente toopass datos entre U-SQL y R. entrada y salida se corrigen los nombres de identificador de trama de datos (es decir, los usuarios no pueden cambiar estos nombres predefinidos de entrada y salida trama de datos identificadores).</span><span class="sxs-lookup"><span data-stu-id="e5ba6-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="e5ba6-109">Incrustar código R en hello script U-SQL</span><span class="sxs-lookup"><span data-stu-id="e5ba6-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="e5ba6-110">Se puede aplicar en línea hello R código el script U-SQL mediante el uso de parámetros de comando de Hola de hello `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="e5ba6-111">Por ejemplo, puede declarar Hola script de R como una variable de cadena y pasarla como un toohello parámetro reductor.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="e5ba6-112">Mantener el código de hello R en un archivo independiente y hacer referencia a él script hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="e5ba6-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="e5ba6-113">Hola siguiente ejemplo muestra un uso más complejo.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="e5ba6-114">En este caso, el código de hello R se implementa como un recurso que es hello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="e5ba6-115">Guarde este código R como un archivo aparte.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="e5ba6-116">Utilice un toodeploy de script U-SQL ese script de R con hello instrucción implementar recursos.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="e5ba6-117">Cómo se integra R con U-SQL</span><span class="sxs-lookup"><span data-stu-id="e5ba6-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="e5ba6-118">Tipos de datos</span><span class="sxs-lookup"><span data-stu-id="e5ba6-118">Datatypes</span></span>
* <span data-ttu-id="e5ba6-119">Las columnas de cadena y numéricas de U-SQL se convierten tal cual entre R DataFrame y U-SQL [tipos admitidos: `double`, `string`, `bool`, `integer` y `byte`].</span><span class="sxs-lookup"><span data-stu-id="e5ba6-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="e5ba6-120">Hola `Factor` no se admite el tipo de datos en SQL U.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="e5ba6-121">`byte[]` debe serializarse como `string` codificada en base64.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="e5ba6-122">Cadenas de U-SQL pueden ser toofactors convertido en el código de R, una vez U-SQL cree trama de datos de entrada de R o establecer parámetros de hello reductor `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="e5ba6-123">Esquemas</span><span class="sxs-lookup"><span data-stu-id="e5ba6-123">Schemas</span></span>
* <span data-ttu-id="e5ba6-124">Los conjuntos de datos de U-SQL no pueden tener nombres de columna duplicados.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="e5ba6-125">Los nombres de columna de conjuntos de datos de U-SQL deben ser cadenas.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="e5ba6-126">Nombres de columna debe ser Hola igual en secuencias de comandos U-SQL y R.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="e5ba6-127">Columna de solo lectura no puede formar parte de la trama de datos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="e5ba6-128">Dado que las columnas de solo lectura se insertan automáticamente en tabla de U-SQL de hello si forma parte del esquema de salida del UDO.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="e5ba6-129">Limitaciones funcionales</span><span class="sxs-lookup"><span data-stu-id="e5ba6-129">Functional limitations</span></span>
* <span data-ttu-id="e5ba6-130">Hello motor de R no pueden crearse instancias dos veces en Hola mismo proceso.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="e5ba6-131">En la actualidad, U-SQL no admite UDO de combinación para la predicción mediante modelos particionados generados con UDO de reducción.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="e5ba6-132">Los usuarios pueden declarar modelos Hola particionado como recurso y usarlos en su Script de R (vea el código de ejemplo `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="e5ba6-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="e5ba6-133">Versiones de R</span><span class="sxs-lookup"><span data-stu-id="e5ba6-133">R Versions</span></span>
<span data-ttu-id="e5ba6-134">Solo se admite R 3.2.2.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="e5ba6-135">Módulos de R estándar</span><span class="sxs-lookup"><span data-stu-id="e5ba6-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="e5ba6-136">Limitaciones de tamaño de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="e5ba6-136">Input and Output size limitations</span></span>
<span data-ttu-id="e5ba6-137">Cada vértice tiene una cantidad limitada de memoria asignada tooit.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="e5ba6-138">Porque hello deben existir tramas de datos de entrada y salida en la memoria en el código de hello R, tamaño total del Hola Hola entrada y salida no puede superar los 500 MB.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="e5ba6-139">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e5ba6-139">Sample Code</span></span>
<span data-ttu-id="e5ba6-140">Más código de ejemplo está disponible en su cuenta de almacén de Data Lake después de instalar las extensiones de análisis avanzado de U-SQL Hola.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="e5ba6-141">ruta de acceso de Hello para el código de ejemplo más es: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="e5ba6-142">Implementación de módulos de R personalizados con U-SQL</span><span class="sxs-lookup"><span data-stu-id="e5ba6-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="e5ba6-143">En primer lugar, crea un módulo personalizado de R y código postal y, a continuación, cargar Hola zip almacén de ADL de tooyour de archivos de módulo personalizado de R.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="e5ba6-144">En el ejemplo de Hola, se cargará magittr_1.5.zip toohello raíz de hello cuenta predeterminada de ADLS Hola cuenta ADLA que usamos.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="e5ba6-145">Una vez que cargue el almacén de hello módulo tooADL, declárelo como utilizar toomake implementar recursos estén disponibles en el script U-SQL y llame a `install.packages` tooinstall lo.</span><span class="sxs-lookup"><span data-stu-id="e5ba6-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
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

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="e5ba6-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5ba6-146">Next Steps</span></span>
* [<span data-ttu-id="e5ba6-147">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e5ba6-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="e5ba6-148">Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5ba6-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="e5ba6-149">Uso de funciones de ventana de U-SQL para trabajos de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e5ba6-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
