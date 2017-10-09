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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Proceso y análisis de documentos JSON mediante Hive en HDInsight

Obtenga información acerca de cómo tooprocess y analizar archivos JSON con Hive en HDInsight. Hola siguiendo el documento JSON se usa en tutorial Hola:

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

Encontrará el archivo Hello en wasb://processjson@hditutorialdata.blob.core.windows.net/. Para obtener más información sobre cómo usar el almacenamiento de blobs de Azure con HDInsight, consulte [Uso del almacenamiento de blobs de Azure compatibles con HDFS con Hadoop en HDInsight](hdinsight-hadoop-use-blob-storage.md). Puede copiar el contenedor de hello archivo toohello predeterminado del clúster.

En este tutorial, use consola de Hive Hola.  Para obtener instrucciones de abrir la consola de Hive hello, consulte [uso de Hive con Hadoop en HDInsight con Escritorio remoto](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>Acoplamiento de documentos JSON
métodos de Hello enumerados en la sección siguiente de Hola requieren documento JSON de hello en una sola fila. Por lo que debe Aplanar la cadena de tooa de documento de hello JSON. Si ya es plano el documento JSON, puede omitir este paso e ir toohello recta próxima sección en los datos de análisis de JSON.

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

Hello archivo sin formato de JSON se encuentra en  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Hola *StudentsRaw* tabla de Hive señala toohello: documento JSON sin acoplar sin formato.

Hola *StudentsOneLine* tabla de Hive almacena los datos de hello en el sistema de archivos predeterminado de HDInsight en Hola Hola */json/estudiantes/* ruta de acceso.

instrucción INSERT de Hello rellena la tabla de StudentOneLine de hello con datos JSON de hello una estructura jerárquica.

instrucción SELECT Hola solo debe devolver una fila.

Este es el resultado de hello de instrucción SELECT hello:

![Reducción del documento JSON de Hola.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Análisis de documentos JSON en Hive
Subárbol proporciona tres mecanismos distintos toorun consultas en documentos JSON:

* usar hello GET\_JSON\_objeto UDF (función definida por el usuario)
* usar hello JSON_TUPLE UDF
* usar el SerDe personalizado
* escribir la propia UDF con Python u otros lenguajes Consulte [este artículo][hdinsight-python] para obtener información sobre cómo ejecutar su propio código de Python con Hive.

### <a name="use-hello-getjsonobject-udf"></a>Hola use GET\_JSON_OBJECT UDF
Hive proporciona una función definida por el usuario integrada llamada [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), que puede realizar consultas JSON en tiempo de ejecución. Este método toma dos argumentos: el nombre de la tabla de Hola y el nombre del método, que tiene Hola planas hello y documento JSON campo JSON que necesita toobe analizar. Echemos un vistazo a una toosee de ejemplo cómo funciona esta UDF.

Obtener nombre hello y last name de cada estudiante

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Aquí es el resultado de hello cuando se ejecuta esta consulta en la ventana de la consola.

![UDF get_json_object][image-hdi-hivejson-getjsonobject]

Hay algunas limitaciones de hello get-json_object UDF.

* Dado que cada campo de consulta de hello requiere volver a analizar consulta hello, afecta al rendimiento de Hola.
* OBTENER\_JSON_OBJECT() devuelve la representación de cadena de Hola de una matriz. tooconvert este subárbol tooa de matriz, tiene tooreplace de expresiones regulares toouse Hola corchetes ' [' y ']' y, a continuación, también llamada divide la matriz de hello tooget.

Se trata de por qué Hola Hive wiki recomienda el uso de json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Usar hello JSON_TUPLE UDF
Otra función definida por el usuario proporcionada por Hive se denomina [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), que es más eficaz que [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Este método toma un conjunto de claves y una cadena JSON y devuelve una tupla de valores mediante una función. Hello consulta siguiente devuelve el identificador del estudiante de Hola y el grado de Hola desde documento JSON de Hola:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

salida de Hello este script en la consola de Hive hello:

![UDF json_tuple][image-hdi-hivejson-jsontuple]

JSON\_TUPLA usa hello [lateral vista](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) sintaxis en el subárbol, lo que permite json\_tupla toocreate una tabla virtual aplicando Hola UDT función tooeach fila de tabla original Hola.  Complejos JSON se convierten en demasiado difícil de manejar debido a Hola repetido el uso de la vista LATERAL. Además, JSON_TUPLE no puede controlar los JSON anidados.

### <a name="use-custom-serde"></a>Usar el SerDe personalizado
SerDe es Hola mejor opción para analizar documentos JSON anidados, podrá esquema JSON de hello toodefine y use Hola esquema tooparse Hola documentos. En este tutorial, use uno de hello SerDe más popular que ha sido desarrollado por [Roberto Congiu](https://github.com/rcongiu).

**toouse Hola SerDe personalizado:**

1. Instale el [Kit de desarrollo de Java SE 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Elija la versión de Windows X64 de Hola de hello JDK si va toobe usando la implementación de Windows hello de HDInsight
   
   > [!WARNING]
   > JDK 1.8 no funciona con este SerDe.
   > 
   > 
   
    Una vez completada la instalación de hello, agregue una nueva variable de entorno de usuario:
   
   1. Abra **vista Configuración avanzada del sistema** en pantalla de Windows hello.
   2. Haga clic en **Variables de entorno**.  
   3. Agregue un nuevo **JAVA_HOME** variable de entorno apunta demasiado**Files\Java\jdk1.7.0_55 C:\Program** o, donde está instalado el JDK.
      
      ![Configuración de los valores correctos para JDK][image-hdi-hivejson-jdk]
2. Instalación de [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Agregar ruta de acceso de hello bin carpeta tooyour yendo tooControl Panel--> Variables del sistema de Hola de edición para las variables de entorno de la cuenta. Hello captura de pantalla siguiente muestra cómo toodo esto.
   
    ![Configuración de Maven][image-hdi-hivejson-maven]
3. Proyecto de Hola de clon de [SerDe de JSON de Hive](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) sitio de github. Puede hacerlo haciendo clic en el botón "Descargar" Zip"de hello tal y como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Proyecto de clonación de Hola][image-hdi-hivejson-serde]

4: vaya toohello carpeta donde ha descargado este paquete y, a continuación, "paquete de mvn" de tipo. Esto debe cree Hola archivos jar necesarios que, a continuación, puede copiar sobre clúster toohello.

5: vaya toohello carpeta de destino en carpeta de raíz de Hola donde descargó el paquete de saludo. Cargar archivo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar hello toohead-nodo del clúster. Normalmente coloca en la carpeta binaria del subárbol de hello: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin o algo similar.

6: en el símbolo del sistema de hello hive, escriba "Agregar jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar". Puesto que en mi caso, jar de hello en carpeta de C:\apps\dist\hive-0.13.x\bin Hola, ¿se puede agregar directamente Hola jar con el nombre de hello tal como se muestra:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Agregar proyecto de tooyour JAR][image-hdi-hivejson-addjar]

Ahora, está listo toouse hello SerDe toorun las consultas realizadas en documento JSON de Hola.

Hola siguiente instrucción crea una tabla con un esquema definido:

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

Hola toolist nombre y apellido del alumno Hola

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Éste es el resultado de hello desde la consola de Hive Hola.

![Consulta SerDe 1][image-hdi-hivejson-serde_query1]

suma de hello toocalculate de puntuaciones de documento JSON de Hola

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Hola anterior consulta utiliza [vista lateral seccionar](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand Hola matriz de puntuaciones para que se pueden sumar.

Este es el resultado de hello desde la consola de Hive Hola.

![Consulta SerDe 2][image-hdi-hivejson-serde_query2]

toofind que somete a un estudiante determinado ha obtenido más de 80 puntos:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Hello consulta anterior devuelve una matriz de Hive a diferencia de get\_json\_objeto, que devuelve una cadena.

![Consulta SerDe 3][image-hdi-hivejson-serde_query3]

Si desea que tooskil JSON con formato incorrecto, a continuación, como Hola explicado en [página wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) de este SerDe puede lograr que escribiendo el siguiente código de hello:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Resumen
En conclusión, tipo de hello del operador JSON en el subárbol que elija depende de su escenario. Si tiene un documento JSON simple y solo tener toolook de un campo de seguridad: puede elegir toouse Hola Hive UDF get\_json\_objeto. Si tiene toolook clave más de una en, puede usar json_tuple. Si tiene un documento anidado, debe usar hello SerDe de JSON.

## <a name="next-steps"></a>Pasos siguientes

Para ver otros artículos relacionados, consulte

* [Use Hive y HiveQL con Hadoop en HDInsight tooanalyze un archivo de ejemplo Apache log4j](hdinsight-use-hive.md)
* [Análisis de datos de retraso de vuelos con Hive en HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Análisis de datos de Twitter con Hive en HDInsight](hdinsight-analyze-twitter-data.md)
* [Ejecución de un trabajo de Hadoop con Azure Cosmos DB y HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
