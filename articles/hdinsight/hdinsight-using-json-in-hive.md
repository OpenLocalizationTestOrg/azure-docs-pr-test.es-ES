---
title: los documentos aaaAnalyze y proceso de JSON con Hive en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo los documentos y analizarlas toouse JSON con Hive en HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="ce058-103">Proceso y análisis de documentos JSON mediante Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce058-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="ce058-104">Obtenga información acerca de cómo tooprocess y analizar archivos JSON con Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ce058-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="ce058-105">Hola siguiendo el documento JSON se usa en tutorial Hola:</span><span class="sxs-lookup"><span data-stu-id="ce058-105">hello following JSON document is used in hello tutorial:</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="ce058-106">Encontrará el archivo Hello en wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="ce058-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="ce058-107">Para obtener más información sobre cómo usar el almacenamiento de blobs de Azure con HDInsight, consulte [Uso del almacenamiento de blobs de Azure compatibles con HDFS con Hadoop en HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ce058-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="ce058-108">Puede copiar el contenedor de hello archivo toohello predeterminado del clúster.</span><span class="sxs-lookup"><span data-stu-id="ce058-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="ce058-109">En este tutorial, use consola de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="ce058-110">Para obtener instrucciones de abrir la consola de Hive hello, consulte [uso de Hive con Hadoop en HDInsight con Escritorio remoto](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="ce058-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="ce058-111">Acoplamiento de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="ce058-111">Flatten JSON documents</span></span>
<span data-ttu-id="ce058-112">métodos de Hello enumerados en la sección siguiente de Hola requieren documento JSON de hello en una sola fila.</span><span class="sxs-lookup"><span data-stu-id="ce058-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="ce058-113">Por lo que debe Aplanar la cadena de tooa de documento de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="ce058-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="ce058-114">Si ya es plano el documento JSON, puede omitir este paso e ir toohello recta próxima sección en los datos de análisis de JSON.</span><span class="sxs-lookup"><span data-stu-id="ce058-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="ce058-115">Hello archivo sin formato de JSON se encuentra en  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="ce058-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="ce058-116">Hola *StudentsRaw* tabla de Hive señala toohello: documento JSON sin acoplar sin formato.</span><span class="sxs-lookup"><span data-stu-id="ce058-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="ce058-117">Hola *StudentsOneLine* tabla de Hive almacena los datos de hello en el sistema de archivos predeterminado de HDInsight en Hola Hola */json/estudiantes/* ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="ce058-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="ce058-118">instrucción INSERT de Hello rellena la tabla de StudentOneLine de hello con datos JSON de hello una estructura jerárquica.</span><span class="sxs-lookup"><span data-stu-id="ce058-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="ce058-119">instrucción SELECT Hola solo debe devolver una fila.</span><span class="sxs-lookup"><span data-stu-id="ce058-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="ce058-120">Este es el resultado de hello de instrucción SELECT hello:</span><span class="sxs-lookup"><span data-stu-id="ce058-120">Here is hello output of hello SELECT statement:</span></span>

![Reducción del documento JSON de Hola.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="ce058-122">Análisis de documentos JSON en Hive</span><span class="sxs-lookup"><span data-stu-id="ce058-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="ce058-123">Subárbol proporciona tres mecanismos distintos toorun consultas en documentos JSON:</span><span class="sxs-lookup"><span data-stu-id="ce058-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="ce058-124">usar hello GET\_JSON\_objeto UDF (función definida por el usuario)</span><span class="sxs-lookup"><span data-stu-id="ce058-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="ce058-125">usar hello JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="ce058-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="ce058-126">usar el SerDe personalizado</span><span class="sxs-lookup"><span data-stu-id="ce058-126">use custom SerDe</span></span>
* <span data-ttu-id="ce058-127">escribir la propia UDF con Python u otros lenguajes</span><span class="sxs-lookup"><span data-stu-id="ce058-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="ce058-128">Consulte [este artículo][hdinsight-python] para obtener información sobre cómo ejecutar su propio código de Python con Hive.</span><span class="sxs-lookup"><span data-stu-id="ce058-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="ce058-129">Hola use GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="ce058-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="ce058-130">Hive proporciona una función definida por el usuario integrada llamada [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), que puede realizar consultas JSON en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ce058-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="ce058-131">Este método toma dos argumentos: el nombre de la tabla de Hola y el nombre del método, que tiene Hola planas hello y documento JSON campo JSON que necesita toobe analizar.</span><span class="sxs-lookup"><span data-stu-id="ce058-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="ce058-132">Echemos un vistazo a una toosee de ejemplo cómo funciona esta UDF.</span><span class="sxs-lookup"><span data-stu-id="ce058-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="ce058-133">Obtener nombre hello y last name de cada estudiante</span><span class="sxs-lookup"><span data-stu-id="ce058-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="ce058-134">Aquí es el resultado de hello cuando se ejecuta esta consulta en la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="ce058-134">Here is hello output when running this query in console window.</span></span>

![UDF get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="ce058-136">Hay algunas limitaciones de hello get-json_object UDF.</span><span class="sxs-lookup"><span data-stu-id="ce058-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="ce058-137">Dado que cada campo de consulta de hello requiere volver a analizar consulta hello, afecta al rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="ce058-138">OBTENER\_JSON_OBJECT() devuelve la representación de cadena de Hola de una matriz.</span><span class="sxs-lookup"><span data-stu-id="ce058-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="ce058-139">tooconvert este subárbol tooa de matriz, tiene tooreplace de expresiones regulares toouse Hola corchetes ' [' y ']' y, a continuación, también llamada divide la matriz de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="ce058-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="ce058-140">Se trata de por qué Hola Hive wiki recomienda el uso de json_tuple.</span><span class="sxs-lookup"><span data-stu-id="ce058-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="ce058-141">Usar hello JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="ce058-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="ce058-142">Otra función definida por el usuario proporcionada por Hive se denomina [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), que es más eficaz que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="ce058-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="ce058-143">Este método toma un conjunto de claves y una cadena JSON y devuelve una tupla de valores mediante una función.</span><span class="sxs-lookup"><span data-stu-id="ce058-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="ce058-144">Hello consulta siguiente devuelve el identificador del estudiante de Hola y el grado de Hola desde documento JSON de Hola:</span><span class="sxs-lookup"><span data-stu-id="ce058-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="ce058-145">salida de Hello este script en la consola de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="ce058-145">hello output of this script in hello Hive console:</span></span>

![UDF json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="ce058-147">JSON\_TUPLA usa hello [lateral vista](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) sintaxis en el subárbol, lo que permite json\_tupla toocreate una tabla virtual aplicando Hola UDT función tooeach fila de tabla original Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="ce058-148">Complejos JSON se convierten en demasiado difícil de manejar debido a Hola repetido el uso de la vista LATERAL.</span><span class="sxs-lookup"><span data-stu-id="ce058-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="ce058-149">Además, JSON_TUPLE no puede controlar los JSON anidados.</span><span class="sxs-lookup"><span data-stu-id="ce058-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="ce058-150">Usar el SerDe personalizado</span><span class="sxs-lookup"><span data-stu-id="ce058-150">Use custom SerDe</span></span>
<span data-ttu-id="ce058-151">SerDe es Hola mejor opción para analizar documentos JSON anidados, podrá esquema JSON de hello toodefine y use Hola esquema tooparse Hola documentos.</span><span class="sxs-lookup"><span data-stu-id="ce058-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="ce058-152">En este tutorial, use uno de hello SerDe más popular que ha sido desarrollado por [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="ce058-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="ce058-153">**toouse Hola SerDe personalizado:**</span><span class="sxs-lookup"><span data-stu-id="ce058-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="ce058-154">Instale el [Kit de desarrollo de Java SE 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="ce058-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="ce058-155">Elija la versión de Windows X64 de Hola de hello JDK si va toobe usando la implementación de Windows hello de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce058-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="ce058-156">JDK 1.8 no funciona con este SerDe.</span><span class="sxs-lookup"><span data-stu-id="ce058-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="ce058-157">Una vez completada la instalación de hello, agregue una nueva variable de entorno de usuario:</span><span class="sxs-lookup"><span data-stu-id="ce058-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="ce058-158">Abra **vista Configuración avanzada del sistema** en pantalla de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="ce058-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="ce058-159">Haga clic en **Variables de entorno**.</span><span class="sxs-lookup"><span data-stu-id="ce058-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="ce058-160">Agregue un nuevo **JAVA_HOME** variable de entorno apunta demasiado**Files\Java\jdk1.7.0_55 C:\Program** o, donde está instalado el JDK.</span><span class="sxs-lookup"><span data-stu-id="ce058-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Configuración de los valores correctos para JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="ce058-162">Instalación de [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="ce058-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="ce058-163">Agregar ruta de acceso de hello bin carpeta tooyour yendo tooControl Panel--> Variables del sistema de Hola de edición para las variables de entorno de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="ce058-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="ce058-164">Hello captura de pantalla siguiente muestra cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="ce058-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Configuración de Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="ce058-166">Proyecto de Hola de clon de [SerDe de JSON de Hive](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) sitio de github.</span><span class="sxs-lookup"><span data-stu-id="ce058-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="ce058-167">Puede hacerlo haciendo clic en el botón "Descargar" Zip"de hello tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Proyecto de clonación de Hola][image-hdi-hivejson-serde]

<span data-ttu-id="ce058-169">4: vaya toohello carpeta donde ha descargado este paquete y, a continuación, "paquete de mvn" de tipo.</span><span class="sxs-lookup"><span data-stu-id="ce058-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="ce058-170">Esto debe cree Hola archivos jar necesarios que, a continuación, puede copiar sobre clúster toohello.</span><span class="sxs-lookup"><span data-stu-id="ce058-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="ce058-171">5: vaya toohello carpeta de destino en carpeta de raíz de Hola donde descargó el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="ce058-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="ce058-172">Cargar archivo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar hello toohead-nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="ce058-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="ce058-173">Normalmente coloca en la carpeta binaria del subárbol de hello: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin o algo similar.</span><span class="sxs-lookup"><span data-stu-id="ce058-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="ce058-174">6: en el símbolo del sistema de hello hive, escriba "Agregar jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar".</span><span class="sxs-lookup"><span data-stu-id="ce058-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="ce058-175">Puesto que en mi caso, jar de hello en carpeta de C:\apps\dist\hive-0.13.x\bin Hola, ¿se puede agregar directamente Hola jar con el nombre de hello tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="ce058-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Agregar proyecto de tooyour JAR][image-hdi-hivejson-addjar]

<span data-ttu-id="ce058-177">Ahora, está listo toouse hello SerDe toorun las consultas realizadas en documento JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="ce058-178">Hola siguiente instrucción crea una tabla con un esquema definido:</span><span class="sxs-lookup"><span data-stu-id="ce058-178">hello following statement creates a table with a defined schema:</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="ce058-179">Hola toolist nombre y apellido del alumno Hola</span><span class="sxs-lookup"><span data-stu-id="ce058-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="ce058-180">Éste es el resultado de hello desde la consola de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-180">Here is hello result from hello Hive console.</span></span>

![Consulta SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="ce058-182">suma de hello toocalculate de puntuaciones de documento JSON de Hola</span><span class="sxs-lookup"><span data-stu-id="ce058-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="ce058-183">Hola anterior consulta utiliza [vista lateral seccionar](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand Hola matriz de puntuaciones para que se pueden sumar.</span><span class="sxs-lookup"><span data-stu-id="ce058-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="ce058-184">Este es el resultado de hello desde la consola de Hive Hola.</span><span class="sxs-lookup"><span data-stu-id="ce058-184">Here is hello output from hello Hive console.</span></span>

![Consulta SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="ce058-186">toofind que somete a un estudiante determinado ha obtenido más de 80 puntos:</span><span class="sxs-lookup"><span data-stu-id="ce058-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="ce058-187">Hello consulta anterior devuelve una matriz de Hive a diferencia de get\_json\_objeto, que devuelve una cadena.</span><span class="sxs-lookup"><span data-stu-id="ce058-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Consulta SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="ce058-189">Si desea que tooskil JSON con formato incorrecto, a continuación, como Hola explicado en [página wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) de este SerDe puede lograr que escribiendo el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="ce058-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="ce058-190">Resumen</span><span class="sxs-lookup"><span data-stu-id="ce058-190">Summary</span></span>
<span data-ttu-id="ce058-191">En conclusión, tipo de hello del operador JSON en el subárbol que elija depende de su escenario.</span><span class="sxs-lookup"><span data-stu-id="ce058-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="ce058-192">Si tiene un documento JSON simple y solo tener toolook de un campo de seguridad: puede elegir toouse Hola Hive UDF get\_json\_objeto.</span><span class="sxs-lookup"><span data-stu-id="ce058-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="ce058-193">Si tiene toolook clave más de una en, puede usar json_tuple.</span><span class="sxs-lookup"><span data-stu-id="ce058-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="ce058-194">Si tiene un documento anidado, debe usar hello SerDe de JSON.</span><span class="sxs-lookup"><span data-stu-id="ce058-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce058-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce058-195">Next steps</span></span>

<span data-ttu-id="ce058-196">Para ver otros artículos relacionados, consulte</span><span class="sxs-lookup"><span data-stu-id="ce058-196">For other related articles, see</span></span>

* [<span data-ttu-id="ce058-197">Use Hive y HiveQL con Hadoop en HDInsight tooanalyze un archivo de ejemplo Apache log4j</span><span class="sxs-lookup"><span data-stu-id="ce058-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ce058-198">Análisis de datos de retraso de vuelos con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce058-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="ce058-199">Análisis de datos de Twitter con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce058-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="ce058-200">Ejecución de un trabajo de Hadoop con Azure Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce058-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
