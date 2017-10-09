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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Tutorial: Introducción a la extensión de U-SQL con Python (Tutorial: Introducción a la extensión de U-SQL con R)

Hola siguiente ejemplo ilustra Hola pasos básicos para implementar código R:
* Hola de uso `REFERENCE ASSEMBLY` extensiones de tooenable R de instrucción para hello Script U-SQL.
* Use la` REDUCE` Hola de operación toopartition los datos en una clave de entrada.
* las extensiones de Hello R para SQL U incluyen un reductor integrado (`Extension.R.Reducer`) que ejecuta código R en cada reductor de toohello vértices asignado. 
* Uso de dedicado denominado tramas de datos denominadas `inputFromUSQL` y `outputToUSQL `respectivamente toopass datos entre U-SQL y R. entrada y salida se corrigen los nombres de identificador de trama de datos (es decir, los usuarios no pueden cambiar estos nombres predefinidos de entrada y salida trama de datos identificadores).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>Incrustar código R en hello script U-SQL

Se puede aplicar en línea hello R código el script U-SQL mediante el uso de parámetros de comando de Hola de hello `Extension.R.Reducer`. Por ejemplo, puede declarar Hola script de R como una variable de cadena y pasarla como un toohello parámetro reductor.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Mantener el código de hello R en un archivo independiente y hacer referencia a él script hello U-SQL

Hola siguiente ejemplo muestra un uso más complejo. En este caso, el código de hello R se implementa como un recurso que es hello script U-SQL.

Guarde este código R como un archivo aparte.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Utilice un toodeploy de script U-SQL ese script de R con hello instrucción implementar recursos.

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

## <a name="how-r-integrates-with-u-sql"></a>Cómo se integra R con U-SQL

### <a name="datatypes"></a>Tipos de datos
* Las columnas de cadena y numéricas de U-SQL se convierten tal cual entre R DataFrame y U-SQL [tipos admitidos: `double`, `string`, `bool`, `integer` y `byte`].
* Hola `Factor` no se admite el tipo de datos en SQL U.
* `byte[]` debe serializarse como `string` codificada en base64.
* Cadenas de U-SQL pueden ser toofactors convertido en el código de R, una vez U-SQL cree trama de datos de entrada de R o establecer parámetros de hello reductor `stringsAsFactors: true`.

### <a name="schemas"></a>Esquemas
* Los conjuntos de datos de U-SQL no pueden tener nombres de columna duplicados.
* Los nombres de columna de conjuntos de datos de U-SQL deben ser cadenas.
* Nombres de columna debe ser Hola igual en secuencias de comandos U-SQL y R.
* Columna de solo lectura no puede formar parte de la trama de datos de salida de hello. Dado que las columnas de solo lectura se insertan automáticamente en tabla de U-SQL de hello si forma parte del esquema de salida del UDO.

### <a name="functional-limitations"></a>Limitaciones funcionales
* Hello motor de R no pueden crearse instancias dos veces en Hola mismo proceso. 
* En la actualidad, U-SQL no admite UDO de combinación para la predicción mediante modelos particionados generados con UDO de reducción. Los usuarios pueden declarar modelos Hola particionado como recurso y usarlos en su Script de R (vea el código de ejemplo `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>Versiones de R
Solo se admite R 3.2.2.

### <a name="standard-r-modules"></a>Módulos de R estándar

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

### <a name="input-and-output-size-limitations"></a>Limitaciones de tamaño de entrada y salida
Cada vértice tiene una cantidad limitada de memoria asignada tooit. Porque hello deben existir tramas de datos de entrada y salida en la memoria en el código de hello R, tamaño total del Hola Hola entrada y salida no puede superar los 500 MB.

### <a name="sample-code"></a>Código de ejemplo
Más código de ejemplo está disponible en su cuenta de almacén de Data Lake después de instalar las extensiones de análisis avanzado de U-SQL Hola. ruta de acceso de Hello para el código de ejemplo más es: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Implementación de módulos de R personalizados con U-SQL

En primer lugar, crea un módulo personalizado de R y código postal y, a continuación, cargar Hola zip almacén de ADL de tooyour de archivos de módulo personalizado de R. En el ejemplo de Hola, se cargará magittr_1.5.zip toohello raíz de hello cuenta predeterminada de ADLS Hola cuenta ADLA que usamos. Una vez que cargue el almacén de hello módulo tooADL, declárelo como utilizar toomake implementar recursos estén disponibles en el script U-SQL y llame a `install.packages` tooinstall lo.

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

## <a name="next-steps"></a>Pasos siguientes
* [Información general de Análisis de Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Desarrollo de scripts de U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Uso de funciones de ventana de U-SQL para trabajos de Análisis de Azure Data Lake](data-lake-analytics-use-window-functions.md)
