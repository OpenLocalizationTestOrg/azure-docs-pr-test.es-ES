---
title: "Análisis y procesamiento de documentos JSON con Hive en HDInsight | Microsoft Docs"
description: Aprenda a utilizar documentos JSON y analizarlos mediante Hive en HDInsight.
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
ms.openlocfilehash: bd136afebeceb0cd9c24cfc5f15601caa80a755e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="4b38e-103">Proceso y análisis de documentos JSON mediante Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b38e-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="4b38e-104">Aprenda a procesar y a analizar archivos JSON mediante Hive en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4b38e-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="4b38e-105">En el tutorial se usa el siguiente documento JSON:</span><span class="sxs-lookup"><span data-stu-id="4b38e-105">The following JSON document is used in the tutorial:</span></span>

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

<span data-ttu-id="4b38e-106">El archivo se encuentra en wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="4b38e-106">The file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="4b38e-107">Para obtener más información sobre cómo usar el almacenamiento de blobs de Azure con HDInsight, consulte [Uso del almacenamiento de blobs de Azure compatibles con HDFS con Hadoop en HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4b38e-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="4b38e-108">Puede copiar el archivo en el contenedor predeterminado del clúster.</span><span class="sxs-lookup"><span data-stu-id="4b38e-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="4b38e-109">En este tutorial, se utiliza la consola de Hive.</span><span class="sxs-lookup"><span data-stu-id="4b38e-109">In this tutorial, you use the Hive console.</span></span>  <span data-ttu-id="4b38e-110">Para obtener instrucciones sobre cómo abrir la consola de Hive, consulte [Uso de Hive con Hadoop en HDInsight con Escritorio remoto](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="4b38e-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="4b38e-111">Acoplamiento de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="4b38e-111">Flatten JSON documents</span></span>
<span data-ttu-id="4b38e-112">Los métodos enumerados en la siguiente sección requieren que el documento JSON esté en una sola fila.</span><span class="sxs-lookup"><span data-stu-id="4b38e-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="4b38e-113">Por lo tanto, debe acoplar el documento JSON a una cadena.</span><span class="sxs-lookup"><span data-stu-id="4b38e-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="4b38e-114">Si el documento JSON ya está acoplado, puede omitir este paso e ir directamente a la sección siguiente sobre Análisis de los datos JSON.</span><span class="sxs-lookup"><span data-stu-id="4b38e-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="4b38e-115">El archivo sin formato JSON se encuentra en **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="4b38e-115">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="4b38e-116">La tabla de Hive *StudentsRaw* apunta al documento JSON sin formato y no acoplado.</span><span class="sxs-lookup"><span data-stu-id="4b38e-116">The *StudentsRaw* Hive table points to the raw unflattened JSON document.</span></span>

<span data-ttu-id="4b38e-117">La tabla de Hive *StudentsOneLine* almacena los datos en el sistema de archivos predeterminado de HDInsight en la ruta de acceso */json/students/*.</span><span class="sxs-lookup"><span data-stu-id="4b38e-117">The *StudentsOneLine* Hive table stores the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="4b38e-118">La instrucción INSERT rellena la tabla StudentOneLine con los datos de JSON acoplados.</span><span class="sxs-lookup"><span data-stu-id="4b38e-118">The INSERT statement populates the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="4b38e-119">La instrucción SELECT solo devolverá una fila.</span><span class="sxs-lookup"><span data-stu-id="4b38e-119">The SELECT statement shall only return one row.</span></span>

<span data-ttu-id="4b38e-120">Este es el resultado de la instrucción SELECT:</span><span class="sxs-lookup"><span data-stu-id="4b38e-120">Here is the output of the SELECT statement:</span></span>

![Acoplamiento del documento JSON.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="4b38e-122">Análisis de documentos JSON en Hive</span><span class="sxs-lookup"><span data-stu-id="4b38e-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="4b38e-123">Hive proporciona tres mecanismos distintos para ejecutar consultas en documentos JSON:</span><span class="sxs-lookup"><span data-stu-id="4b38e-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="4b38e-124">usar la UDF (función definida por el usuario) GET\_JSON\_OBJECT</span><span class="sxs-lookup"><span data-stu-id="4b38e-124">use the GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="4b38e-125">usar la UDF JSON_TUPLE</span><span class="sxs-lookup"><span data-stu-id="4b38e-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="4b38e-126">usar el SerDe personalizado</span><span class="sxs-lookup"><span data-stu-id="4b38e-126">use custom SerDe</span></span>
* <span data-ttu-id="4b38e-127">escribir la propia UDF con Python u otros lenguajes</span><span class="sxs-lookup"><span data-stu-id="4b38e-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="4b38e-128">Consulte [este artículo][hdinsight-python] para obtener información sobre cómo ejecutar su propio código de Python con Hive.</span><span class="sxs-lookup"><span data-stu-id="4b38e-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="4b38e-129">Uso de la UDF GET\_JSON_OBJECT</span><span class="sxs-lookup"><span data-stu-id="4b38e-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="4b38e-130">Hive proporciona una función definida por el usuario integrada llamada [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), que puede realizar consultas JSON en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4b38e-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="4b38e-131">Este método toma dos argumentos: el nombre de la tabla y el nombre del método que tiene el documento JSON acoplado y el campo JSON que debe analizarse.</span><span class="sxs-lookup"><span data-stu-id="4b38e-131">This method takes two arguments – the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="4b38e-132">Veamos un ejemplo para ver cómo funciona esta UDF.</span><span class="sxs-lookup"><span data-stu-id="4b38e-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="4b38e-133">Obtener el nombre y el apellido de cada estudiante</span><span class="sxs-lookup"><span data-stu-id="4b38e-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="4b38e-134">Este es el resultado cuando se ejecuta esta consulta en la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="4b38e-134">Here is the output when running this query in console window.</span></span>

![UDF get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="4b38e-136">Existen algunas limitaciones de la UDF de get-json_object.</span><span class="sxs-lookup"><span data-stu-id="4b38e-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="4b38e-137">Como cada campo de la consulta requiere volver a analizar la consulta, afecta al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="4b38e-137">Because each field in the query requires reparsing the query, it affects the performance.</span></span>
* <span data-ttu-id="4b38e-138">GET\_JSON_OBJECT() devuelve la representación de cadena de una matriz.</span><span class="sxs-lookup"><span data-stu-id="4b38e-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="4b38e-139">Para convertir esta matriz en una matriz de Hive, tiene que utilizar expresiones regulares para reemplazar los corchetes '[' y ']' y luego llamar también a split para obtener la matriz.</span><span class="sxs-lookup"><span data-stu-id="4b38e-139">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="4b38e-140">Este es el motivo de que el sitio wiki de Hive recomiende el uso de json_tuple.</span><span class="sxs-lookup"><span data-stu-id="4b38e-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="4b38e-141">Use la UDF JSON_TUPLE.</span><span class="sxs-lookup"><span data-stu-id="4b38e-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="4b38e-142">Otra función definida por el usuario proporcionada por Hive se denomina [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), que es más eficaz que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="4b38e-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="4b38e-143">Este método toma un conjunto de claves y una cadena JSON y devuelve una tupla de valores mediante una función.</span><span class="sxs-lookup"><span data-stu-id="4b38e-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="4b38e-144">La siguiente consulta devuelve el identificador y el curso del estudiante del documento JSON:</span><span class="sxs-lookup"><span data-stu-id="4b38e-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="4b38e-145">Salida de este script en la consola de Hive:</span><span class="sxs-lookup"><span data-stu-id="4b38e-145">The output of this script in the Hive console:</span></span>

![UDF json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="4b38e-147">JSON\_TUPLE usa la sintaxis [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) de Hive, que permite que json\_tuple cree una tabla virtual aplicando la función UDT a cada fila de la tabla original.</span><span class="sxs-lookup"><span data-stu-id="4b38e-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="4b38e-148">Los JSON complejos se vuelven demasiado difíciles de manejar debido al uso repetido de LATERAL VIEW.</span><span class="sxs-lookup"><span data-stu-id="4b38e-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="4b38e-149">Además, JSON_TUPLE no puede controlar los JSON anidados.</span><span class="sxs-lookup"><span data-stu-id="4b38e-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="4b38e-150">Usar el SerDe personalizado</span><span class="sxs-lookup"><span data-stu-id="4b38e-150">Use custom SerDe</span></span>
<span data-ttu-id="4b38e-151">SerDe es la mejor opción para analizar documentos JSON anidados ya que le permite definir el esquema JSON y usar el esquema para analizar los documentos.</span><span class="sxs-lookup"><span data-stu-id="4b38e-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="4b38e-152">En este tutorial, usará uno de los SerDe más conocidos desarrollado por [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="4b38e-152">In this tutorial, you use one of the more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="4b38e-153">**Para usar el SerDe personalizado:**</span><span class="sxs-lookup"><span data-stu-id="4b38e-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="4b38e-154">Instale el [Kit de desarrollo de Java SE 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="4b38e-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="4b38e-155">Si va a usar la implementación de Windows de HDInsight, elija la versión Windows x 64 del JDK.</span><span class="sxs-lookup"><span data-stu-id="4b38e-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="4b38e-156">JDK 1.8 no funciona con este SerDe.</span><span class="sxs-lookup"><span data-stu-id="4b38e-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="4b38e-157">Una vez completada la instalación, agregue una nueva variable de entorno de usuario:</span><span class="sxs-lookup"><span data-stu-id="4b38e-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="4b38e-158">Abra **Ver la configuración avanzada del sistema** desde la pantalla de Windows.</span><span class="sxs-lookup"><span data-stu-id="4b38e-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="4b38e-159">Haga clic en **Variables de entorno**.</span><span class="sxs-lookup"><span data-stu-id="4b38e-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="4b38e-160">Agregue una nueva variable de entorno **JAVA_HOME** que apunte a **C:\Program Files\Java\jdk1.7.0_55** o a donde esté instalado el JDK.</span><span class="sxs-lookup"><span data-stu-id="4b38e-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Configuración de los valores correctos para JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="4b38e-162">Instalación de [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="4b38e-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="4b38e-163">Para agregar la carpeta bin a la ruta de acceso, vaya a Panel de control-->Edit the System Variables (Editar las variables del sistema) para su cuenta Variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="4b38e-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="4b38e-164">La captura de pantalla siguiente muestra cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="4b38e-164">The following screenshot shows you how to do this.</span></span>
   
    ![Configuración de Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="4b38e-166">Clone el proyecto del sitio de github [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) .</span><span class="sxs-lookup"><span data-stu-id="4b38e-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="4b38e-167">Para ello, haga clic en el botón "Download Zip" (Descargar archivo comprimido) como se muestra en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="4b38e-167">You can do this by clicking on the “Download Zip” button as shown in the following screenshot.</span></span>
   
    ![Clonación del proyecto][image-hdi-hivejson-serde]

<span data-ttu-id="4b38e-169">4: Vaya a la carpeta donde ha descargado este paquete y escriba "mvn.package".</span><span class="sxs-lookup"><span data-stu-id="4b38e-169">4: Go to the folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="4b38e-170">Esta acción debe crear los archivos jar necesarios que luego puede copiar en el clúster.</span><span class="sxs-lookup"><span data-stu-id="4b38e-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="4b38e-171">5: Vaya a la carpeta de destino bajo la carpeta raíz donde descargó el paquete.</span><span class="sxs-lookup"><span data-stu-id="4b38e-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="4b38e-172">Cargue el archivo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar en el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="4b38e-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="4b38e-173">Yo lo coloco normalmente bajo la carpeta de archivos binarios de Hive: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin o algo similar.</span><span class="sxs-lookup"><span data-stu-id="4b38e-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="4b38e-174">6: En el símbolo del sistema de Hive, escriba "add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar".</span><span class="sxs-lookup"><span data-stu-id="4b38e-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="4b38e-175">Como en mi caso el archivo jar está en la carpeta C:\apps\dist\hive-0.13.x\bin, puedo agregarlo directamente con el nombre tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="4b38e-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Agregar JAR a su proyecto][image-hdi-hivejson-addjar]

<span data-ttu-id="4b38e-177">Ahora, ya está listo para usar el SerDe para ejecutar consultas en el documento JSON.</span><span class="sxs-lookup"><span data-stu-id="4b38e-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="4b38e-178">La siguiente instrucción crea una tabla con un esquema definido:</span><span class="sxs-lookup"><span data-stu-id="4b38e-178">The following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="4b38e-179">Mostrar el nombre y el apellido del alumno</span><span class="sxs-lookup"><span data-stu-id="4b38e-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="4b38e-180">Este es el resultado de la consola de Hive.</span><span class="sxs-lookup"><span data-stu-id="4b38e-180">Here is the result from the Hive console.</span></span>

![Consulta SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="4b38e-182">Calcular la suma de puntuaciones del documento JSON</span><span class="sxs-lookup"><span data-stu-id="4b38e-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="4b38e-183">La consulta anterior utiliza la función definida por el usuario [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) para expandir la matriz de puntuaciones de manera que se puedan sumar.</span><span class="sxs-lookup"><span data-stu-id="4b38e-183">The preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="4b38e-184">Este es el resultado de la consola de Hive.</span><span class="sxs-lookup"><span data-stu-id="4b38e-184">Here is the output from the Hive console.</span></span>

![Consulta SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="4b38e-186">Para buscar en qué materias un estudiante concreto tiene más de 80 puntos:</span><span class="sxs-lookup"><span data-stu-id="4b38e-186">To find which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="4b38e-187">La consulta anterior devuelve una matriz de Hive a diferencia de get\_json\_object, que devuelve una cadena.</span><span class="sxs-lookup"><span data-stu-id="4b38e-187">The preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Consulta SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="4b38e-189">Si desea eliminar documentos JSON con formato incorrecto, como se explica en la [página wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) de este SerDe, puede hacerlo escribiendo el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="4b38e-189">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="4b38e-190">Resumen</span><span class="sxs-lookup"><span data-stu-id="4b38e-190">Summary</span></span>
<span data-ttu-id="4b38e-191">En conclusión, el tipo de operador JSON en Hive que elija depende de su escenario.</span><span class="sxs-lookup"><span data-stu-id="4b38e-191">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="4b38e-192">Si tiene un documento JSON sencillo y solo tiene un campo por el que buscar, puede elegir usar la UDF de Hive get\_json\_object.</span><span class="sxs-lookup"><span data-stu-id="4b38e-192">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="4b38e-193">Si tiene varias claves por las que buscar, puede utilizar json_tuple.</span><span class="sxs-lookup"><span data-stu-id="4b38e-193">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="4b38e-194">Si tiene un documento anidado, debe utilizar el SerDe de JSON.</span><span class="sxs-lookup"><span data-stu-id="4b38e-194">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b38e-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b38e-195">Next steps</span></span>

<span data-ttu-id="4b38e-196">Para ver otros artículos relacionados, consulte</span><span class="sxs-lookup"><span data-stu-id="4b38e-196">For other related articles, see</span></span>

* [<span data-ttu-id="4b38e-197">Usar Hive y HiveQL con Hadoop en HDInsight para analizar un archivo log4j de Apache de muestra</span><span class="sxs-lookup"><span data-stu-id="4b38e-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4b38e-198">Análisis de datos de retraso de vuelos con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b38e-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="4b38e-199">Análisis de datos de Twitter con Hive en HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b38e-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="4b38e-200">Ejecución de un trabajo de Hadoop con Azure Cosmos DB y HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b38e-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
