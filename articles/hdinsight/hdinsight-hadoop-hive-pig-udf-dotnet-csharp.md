---
title: aaaUse C# con Hive y Pig en Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse C# definida por el usuario (UDF) de las funciones con Hive y Pig de HDInsight de Azure transmisión por secuencias."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>Usar funciones definidas por el usuario de C# con el streaming de Hive y Pig en Hadoop de HDInsight

Obtenga información acerca de cómo toouse C# definido por el usuario (UDF) las funciones con Apache Hive y Pig en HDInsight.

> [!IMPORTANT]
> pasos de Hello en este documento funcionan con clústeres de HDInsight basados en Windows y basados en Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md).

Ambos Hive y Pig logra pasar las aplicaciones de tooexternal de datos para su procesamiento. Este proceso se conoce como _streaming_. Cuando se usa un dichos. NET, los datos de hello es pasar toohello aplicación STDIN y aplicación hello devuelve los resultados de hello en STDOUT. tooread y escritura desde STDIN y STDOUT, puede usar `Console.ReadLine()` y `Console.WriteLine()` desde una aplicación de consola.

## <a name="prerequisites"></a>Requisitos previos

* Estar familiarizado con la escritura y la compilación del código C# orientado a .NET Framework 4.5.

    * Use el IDE que prefiera. Recomendamos [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 o [Visual Studio Code](https://code.visualstudio.com/). Hola pasos de este documento, use Visual Studio de 2017.

* Una manera tooupload .exe archivos toohello clúster y ejecución de los trabajos de Pig y Hive. Se recomiendan Hola Data Lake Tools para Visual Studio, PowerShell de Azure y Azure CLI. Hello pasos de este documento usar Hola Data Lake Tools archivos de Visual Studio tooupload hello y ejecutan la consulta de Hive de ejemplo de Hola.

    Para obtener información sobre otras consultas de Hive de formas toorun y trabajos de Pig, consulte Hola siguientes documentos:

    * [Uso de Apache Hive con HDInsight](hdinsight-use-hive.md)

    * [Uso de Apache Pig con HDInsight](hdinsight-use-pig.md)

* Hadoop en un clúster de HDInsight. Para obtener más información sobre cómo crear un clúster, consulte [Creación de un clúster de HDInsight](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET en HDInsight

* __HDInsight basados en Linux__ clústeres mediante [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicaciones. NET. La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight.

    Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse una versión específica de Mono, vea hello [instalación o una actualización Mono](hdinsight-hadoop-install-mono.md) documento.

* __HDInsight basados en Windows__ clústeres usen las aplicaciones .NET de hello Microsoft .NET CLR toorun.

Para obtener más información sobre la versión de Hola de hello .NET framework y Mono incluida en versiones de HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Crear hello C\# proyectos

### <a name="hive-udf"></a>UDF de Hive

1. Abra Visual Studio y cree una solución. Para el tipo de proyecto de hello, seleccione **aplicación de consola (.NET Framework)**y nombre hello nuevo proyecto **HiveCSharp**.

    > [!IMPORTANT]
    > Seleccione __.NET Framework 4.5__ si está usando un clúster de HDInsight basado en Linux. Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Reemplace el contenido de Hola de **Program.cs** con siguiente hello:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Compile el proyecto de Hola.

### <a name="pig-udf"></a>UDF de Pig

1. Abra Visual Studio y cree una solución. Para el tipo de proyecto de hello, seleccione **aplicación de consola**y nombre hello nuevo proyecto **PigUDF**.

2. Reemplazar contenido Hola de hello **Program.cs** archivo con el siguiente código de hello:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Esta aplicación analiza las líneas de hello enviadas desde Pig y volver a formatear líneas que comienzan por `java.lang.Exception`.

3. Guardar **Program.cs**y, a continuación, compile el proyecto de Hola.

## <a name="upload-toostorage"></a>Cargar toostorage

1. En Visual Studio, abra el **Explorador de servidores**.

2. Expanda **Azure** y, después, haga lo mismo con **HDInsight**.

3. Si se le solicitan, escriba sus credenciales de suscripción de Azure y, a continuación, haga clic en **Iniciar sesión**.

4. Expanda el clúster de HDInsight de Hola que desee toodeploy para esta aplicación. Una entrada con el texto hello __(cuenta de almacenamiento predeterminada)__ aparece.

    ![Explorador de servidores mostrando la cuenta de almacenamiento de hello para el clúster de Hola](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Si se puede expandir esta entrada, que usa un __cuenta de almacenamiento de Azure__ como almacenamiento predeterminado para el clúster de Hola. archivos de Hola de tooview en almacenamiento predeterminado de Hola para clúster hello, expanda la entrada de hello y, a continuación, haga doble clic en hello __(contenedor predeterminado)__.

    * Si no se puede expandir esta entrada, que usa __almacén de Azure Data Lake__ como almacenamiento predeterminado de hello para el clúster de Hola. archivos de hello tooview en almacenamiento predeterminado de hello para el clúster de hello, haga doble clic en hello __(cuenta de almacenamiento predeterminada)__ entrada.

6. archivos .exe de tooupload hello, use uno de los siguientes métodos de hello:

    * Si usa un __cuenta de almacenamiento de Azure__, haga clic en el icono de carga de hello y, a continuación, examinar toohello **bin\debug** carpeta para hello **HiveCSharp** proyecto. Por último, seleccione hello **HiveCSharp.exe** de archivo y haga clic en **Aceptar**.

        ![icono para cargar](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Si usa __almacén de Azure Data Lake__, haga clic en un área vacía en lista de archivos de hello y, a continuación, seleccione __cargar__. Por último, seleccione hello **HiveCSharp.exe** de archivo y haga clic en **abiertos**.

    Una vez Hola __HiveCSharp.exe__ carga haya finalizado, el proceso de carga de repetición Hola para hello __PigUDF.exe__ archivo.

## <a name="run-a-hive-query"></a>Ejecución de una consulta de Hive

1. En Visual Studio, abra el **Explorador de servidores**.

2. Expanda **Azure** y, después, haga lo mismo con **HDInsight**.

3. Clúster de hello contextual implementados hello **HiveCSharp** aplicación y, a continuación, seleccione **escribir una consulta de Hive**.

4. Usar hello siguiendo el texto de consulta de Hive hello:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Quite el comentario de hello `add file` instrucción que coincide con el tipo de saludo de almacenamiento predeterminado utilizado para el clúster.

    Esta consulta selecciona hello `clientid`, `devicemake`, y `devicemodel` campos de `hivesampletable`y pasa a campos de hello toohello HiveCSharp.exe aplicación. espera de consulta de Hola Hola tooreturn tres campos de aplicación, que se almacenan como `clientid`, `phoneLabel`, y `phoneHash`. consulta de Hello también espera toofind HiveCSharp.exe en la raíz de Hola Hola predeterminado del contenedor de almacenamiento.

5. Haga clic en **enviar** clúster de HDInsight de toosubmit Hola trabajo toohello. Hola **resumen del trabajo de Hive** abre la ventana.

6. Haga clic en **actualizar** toorefresh Hola resumen hasta **estado del trabajo** cambia demasiado**completado**. trabajo de hello tooview de salida, haga clic en **salida del trabajo**.

## <a name="run-a-pig-job"></a>Ejecución de un trabajo de Pig

1. Use uno de hello después de clúster de HDInsight de tooyour tooconnect de métodos:

    * Si está usando un clúster de HDInsight __basado en Linux__, use SSH. Por ejemplo: `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
    
    * Si usas un __basados en Windows__ clúster de HDInsight, [conectar toohello clúster mediante Escritorio remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Usar una hello después de la línea de comandos de comando toostart Hola Pig:

        pig

    > [!IMPORTANT]
    > Si está usando un clúster basado en Windows, utilice Hola siguientes comandos en su lugar:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    Se muestra un símbolo del sistema `grunt>`.

3. Escriba Hola después de un trabajo de Pig que usa la aplicación de .NET Framework de hello toorun:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Hola `DEFINE` instrucción crea un alias de `streamer` para las aplicaciones de hello pigudf.exe, y `CACHE` carga de almacenamiento predeterminado para el clúster de Hola. Más adelante, `streamer` se utiliza con hello `STREAM` operador tooprocess Hola líneas individuales contenidas en el registro y datos de hello devuelto como una serie de columnas.

    > [!NOTE]
    > nombre de la aplicación Hello que se usa para la transmisión por secuencias debe estar rodeada de hello \` (acento grave) de caracteres cuando tiene un alias, y ' (comilla sencilla) cuando se utiliza con `SHIP`.

4. Después de escribir la última línea de hello, debe iniciar el trabajo de Hola. Devuelve toohello similar de salida siguiente texto:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Pasos siguientes

En este documento, ha aprendido cómo toouse una aplicación de .NET Framework de Hive y Pig en HDInsight. Si desea que toolearn toouse Python con Hive y Pig, vea [uso de Python con Hive y Pig en HDInsight](hdinsight-python.md).

Para otras formas toouse Pig y Hive y toolearn sobre el uso de MapReduce, vea Hola siguientes documentos:

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)
