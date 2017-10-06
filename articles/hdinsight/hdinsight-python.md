---
title: aaaPython UDF con Apache Hive y Pig - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo la pila toouse Python usuario definido funciones (UDF) de Hive y Pig en HDInsight, Hola tecnología de Hadoop en Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Uso de funciones definidas por el usuario (UDF) de Python con Hive y Pig en HDInsight

Obtenga información acerca de cómo toouse Python definidos por el usuario (UDF) las funciones con Apache Hive y Pig en Hadoop en HDInsight de Azure.

## <a name="python"></a>Python en HDInsight

Python 2.7 se instala de forma predeterminada en HDInsight 3.0 y posteriores. Apache Hive puede usarse con esta versión de Python para el procesamiento de streaming. Procesamiento de flujo utiliza STDOUT y STDIN datos toopass entre Hive y Hola UDF.

HDInsight incluye también Jython, que es una implementación de Python escrita en Java. Jython se ejecuta directamente en la máquina Virtual Java de hello y no utiliza la transmisión por secuencias. Jython es Hola recomienda intérprete de Python para usar Python con Pig.

> [!WARNING]
> pasos de Hello en este documento muestran Hola siguientes supuestos: 
>
> * Crear scripts de Python de hello en el entorno de desarrollo local.
> * Cargar tooHDInsight de secuencias de comandos de hello mediante cualquier hello `scp` comando desde una sesión intensiva de errores local u Hola proporcionado script de PowerShell.
>
> Si desea que hello toouse [Shell de nube de Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) obtener una vista previa de toowork con HDInsight, a continuación, debe:
>
> * Crear secuencias de comandos de hello en el entorno del shell de hello en la nube.
> * Use `scp` archivos de hello tooupload de hello tooHDInsight de shell en la nube.
> * Use `ssh` de hello en la nube shell tooconnect tooHDInsight y ejemplos de ejecución Hola.

## <a name="hivepython"></a>UDF de Hive

Python puede utilizarse como una UDF de Hive a través de hello HiveQL `TRANSFORM` instrucción. Por ejemplo, hello después HiveQL invoca hello `hiveudf.py` archivo almacenado en la cuenta de almacenamiento de Azure Hola predeterminada para el clúster de Hola.

**HDInsight basado en Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight basado en Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> En los clústeres de HDInsight basados en Windows, Hola `USING` cláusula debe especificar Hola ruta de acceso completa toopython.exe.

A continuación se muestra lo que hace este ejemplo:

1. Hola `add file` instrucción al principio de hello del archivo hello agrega hello `hiveudf.py` toohello de archivos distribuido de memoria caché, por lo que es accesible para todos los nodos de clúster de Hola.
2. Hola `SELECT TRANSFORM ... USING` instrucción selecciona datos de hello `hivesampletable`. También pasa Hola clientid, devicemake y devicemodel valores toohello `hiveudf.py` secuencia de comandos.
3. Hola `AS` cláusula describe campos Hola devueltos desde `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Crear archivo de hello hiveudf.py


En el entorno de desarrollo, cree un archivo de texto denominado `hiveudf.py`. Usar hello siguiente código como contenido de Hola de archivo hello:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Este script realiza Hola siguientes acciones:

1. Leer una línea de datos de STDIN.
2. Hola caracteres de nueva línea final se quita mediante `string.strip(line, "\n ")`.
3. Al realizar el procesamiento de la secuencia, una sola línea contiene todos los valores de hello con un carácter de tabulación entre cada valor. Por lo que `string.split(line, "\t")` puede ser hello toosplit usado en cada pestaña, devolver simplemente Hola campos de entrada.
4. Una vez completado el procesamiento, salida de hello debe escribirse tooSTDOUT como una sola línea, con una tabulación entre cada campo. Por ejemplo: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Hola `while` bucle se repite hasta que no `line` se lee.

salida del script de Hola es una concatenación de valores de entrada de Hola para `devicemake` y `devicemodel`, y un hash del programa Hola a un valor concatenado.

Vea [ejecutar ejemplos de hello](#running) para saber cómo toorun este ejemplo en el clúster de HDInsight.

## <a name="pigpython"></a>UDF de Pig

Puede utilizar un script de Python como una UDF de Pig mediante hello `GENERATE` instrucción. Puede ejecutar script de Hola mediante Jython o C Python.

* Jython se ejecuta en hello JVM y forma nativa pueden llamarse desde Pig.
* C Python es un proceso externo, por lo que los datos de Hola de Pig en hello JVM se envía toohello script que se ejecuta en un proceso de Python. la salida de Hello de script de Python Hola se envía en Pig.

intérprete de Python toospecify hello, use `register` al hacer referencia a scripts de Python Hola. Hello en los ejemplos siguientes registrar scripts con Pig como `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Al utilizar Jython, toohello pig_jython archivo de hello ruta de acceso puede ser una ruta de acceso local o una WASB: / / ruta de acceso. Sin embargo, al utilizar C Python, debe hacer referencia a un archivo en el sistema de archivos local de hello del nodo de Hola que usa el trabajo de Pig toosubmit Hola.

Una vez más allá de registro, hello Pig latino para este ejemplo Hola mismo para ambos:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

A continuación se muestra lo que hace este ejemplo:

1. Hola primera línea carga el archivo de datos de ejemplo de Hola, `sample.log` en `LOGS`. También define cada registro como `chararray`.
2. línea siguiente de Hello filtra los valores null, almacenando el resultado de hello de operación de hello en `LOG`.
3. A continuación, recorre en iteración los registros de hello en `LOG` y utiliza `GENERATE` tooinvoke hello `create_structure` método incluido en script de Python/Jython Hola se carga como `myfuncs`. `LINE`es toopass utilizados en función de registro toohello actual de Hola.
4. Por último, salidas de hello son los tooSTDOUT con hello `DUMP` comando. Este comando muestra los resultados de hello al finalizar la operación de Hola.

### <a name="create-hello-pigudfpy-file"></a>Crear archivo de hello pigudf.py

En el entorno de desarrollo, cree un archivo de texto denominado `pigudf.py`. Usar hello siguiente código como contenido de Hola de archivo hello:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

En el ejemplo de Hola Pig latino, definimos hello `LINE` de entrada como un chararray porque no hay ningún esquema coherente para la entrada de Hola. Hola script de Python transforma los datos de hello en un esquema coherente para la salida.

1. Hola `@outputSchema` instrucción define el formato de Hola de datos de Hola que se devuelven tooPig. En este caso es un **contenedor de datos**, que es un tipo de datos de Pig. contenedor de Hello contiene Hola después de campos, todos ellos son chararray (cadenas):

   * fecha: hello entrada del registro de hello de fecha se creó
   * hora: Hola se creó la entrada de registro de hello
   * ClassName - entrada de Hola de nombre de clase de Hola se creó para
   * nivel - nivel de registro de hello
   * detalle: entrada de registro de información detallada para hello

2. A continuación, Hola `def create_structure(input)` define la función hello que Pig pasa artículos de línea.

3. datos de ejemplo de Hola `sample.log`, principalmente se ajusta toohello fecha, hora, classname, nivel y de detalle que deseamos tooreturn de esquema. Sin embargo, contiene unas pocas líneas que comienzan por `*java.lang.Exception*`. Estas líneas deben ser el esquema de hello toomatch modificado. Hola `if` instrucción comprueba para las que, a continuación, mensajes Hola Hola toomove de datos de entrada `*java.lang.Exception*` final de cadena toohello, volver a poner Hola datos en línea con el esquema de resultado esperado.

4. A continuación, Hola `split` comando es datos de hello toosplit usados en los primeros caracteres de espacio en cuatro Hola. salida de Hello se asigna en `date`, `time`, `classname`, `level`, y `detail`.

5. Por último, se devuelven valores de hello tooPig.

Cuando se devuelven datos de hello tooPig, tiene un esquema coherente tal como se define en hello `@outputSchema` instrucción.

## <a name="running"></a>Cargar y ejecutar los ejemplos de hello

> [!IMPORTANT]
> Hola **SSH** pasos sólo funcionan con un clúster de HDInsight basados en Linux. Hola **PowerShell** pasos de trabajo con clúster Linux o de HDInsight basados en Windows, pero requiere un cliente de Windows.

### <a name="ssh"></a>SSH

Para obtener más información sobre cómo usar SSH, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Use `scp` clúster de HDInsight de toocopy Hola archivos tooyour. Por ejemplo, Hola siguiente copias Hola clúster tooa de archivos con el nombre de comando **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. Utilizar SSH tooconnect toohello clúster.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Desde la sesión de SSH de hello, agregar archivos de python Hola cargan previamente toohello almacenamiento WASB Hola del clúster.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Después de cargar archivos de hello, pasos siguientes de Hola de uso toorun Hola Hive y los trabajos de Pig.

#### <a name="use-hello-hive-udf"></a>Usar hello Hive UDF

1. Hola de uso `hive` toostart Hola hive shell de comandos. Debería ver un `hive>` solicitar una vez que ha cargado el shell de Hola.

2. Escriba Hola después de consulta en hello `hive>` símbolo del sistema:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Después de escribir la última línea de hello, debe iniciar el trabajo de Hola. Cuando se completa el trabajo de hello, devuelve toohello similar de salida siguiente ejemplo:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Usar hello Pig UDF

1. Hola de uso `pig` toostart Hola shell de comandos. Verá un `grunt>` solicitar una vez que ha cargado el shell de Hola.

2. Escriba Hola siguiendo las instrucciones en hello `grunt>` símbolo del sistema:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Después de escribir Hola después de línea, debe iniciar el trabajo de Hola. Cuando se completa el trabajo de hello, devuelve toohello similar de salida datos siguientes:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Usar `quit` tooexit Hola shell Grunt y, a continuación, usar hello tooedit hello pigudf.py archivo en el sistema de archivos local de hello siguiente:

    ```bash
    nano pigudf.py
    ```

5. Una vez en el editor de hello, quite Hola después de línea mediante la eliminación de hello `#` carácter desde principio Hola de línea hello:

    ```bash
    #from pig_util import outputSchema
    ```

    Una vez que se ha realizado el cambio de hello, utilizarlo CTRL+x tooexit Hola. Seleccione Y y, a continuación, escriba los cambios de hello toosave.

6. Hola de uso `pig` comando shell de toostart Hola de nuevo. Una vez que esté en hello `grunt>` símbolo del sistema, use Hola después de script de Python de hello toorun con intérprete de Python C Hola.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Al finalizar este trabajo, verá Hola de salida igual que cuando se ejecuta antes script de Hola mediante Jython.

### <a name="powershell-upload-hello-files"></a>PowerShell: Cargar los archivos Hola

Puede usar PowerShell tooupload Hola archivos toohello HDInsight del servidor. Usar hello siguientes archivos de script tooupload Hola Python:

> [!IMPORTANT] 
> pasos de Hello en esta sección usan Azure PowerShell. Para obtener más información sobre cómo usar PowerShell de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Hola de cambio `C:\path\to` valor toohello archivos de toohello de ruta de acceso en el entorno de desarrollo.

Este script recupera información para el clúster de HDInsight, a continuación, extrae la cuenta de hello y la clave de cuenta de almacenamiento predeterminada de Hola y cargas Hola raíz de toohello los archivos del contenedor de Hola.

> [!NOTE]
> Para obtener más información sobre la carga de archivos, vea hello [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md) documento.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: Hola de uso Hive UDF

PowerShell también puede ser utilizados tooremotely ejecutar consultas de Hive. Hola de uso después de script de PowerShell toorun una consulta de Hive que usa **hiveudf.py** secuencia de comandos:

> [!IMPORTANT]
> Antes de ejecutar, script de Hola solicita Hola HTTPs/Admin de información de cuenta para el clúster de HDInsight.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Hola salida de hello **Hive** trabajo debe aparecer similar toohello siguiente ejemplo:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell también puede ser utilizados toorun Pig latino trabajos. un trabajo de Pig latino que utiliza hello toorun **pigudf.py** script, use el siguiente script de PowerShell de hello:

> [!NOTE]
> Al enviar remotamente un trabajo con PowerShell, no es posible toouse Python C como intérprete Hola.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Hola salida de hello **Pig** trabajo debe aparecer toohello similar datos siguientes:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Solución de problemas

### <a name="errors-when-running-jobs"></a>Errores en la ejecución de trabajos

Cuando se ejecuta el trabajo de hive de hello, puede producirse un toohello de error similar siguiente texto:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Este problema puede deberse a finales de línea hello en el archivo de Python de hello. Muchos editores de Windows predeterminado toousing CRLF como de fin de línea hello, pero las aplicaciones Linux usualmente esperan LF.

Puede usar Hola PowerShell instrucciones tooremove Hola CR caracteres que le siguen antes de cargar Hola archivo tooHDInsight:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>Scripts de PowerShell

Ambos de ejemplo de Hola a scripts de PowerShell usan los ejemplos de hello toorun contienen una línea comentada que muestra la salida de error de trabajo de Hola. Si no ve salida Hola espera trabajo de hello, quite la línea siguiente de Hola y vea si la información de error de hello indica un problema.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

información de error de Hello (STDERR) y el resultado de hello de trabajo de hello (STDOUT) también están registrados tooyour HDInsight almacenamiento.

| Para este trabajo... | Examine estos archivos en el contenedor de blobs de Hola |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>Pasos siguientes

Si tiene módulos de Python tooload que no se proporcionan de forma predeterminada, consulte [cómo toodeploy una tooAzure módulo HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Para otras formas toouse Pig, Hive y toolearn sobre el uso de MapReduce, vea Hola siguientes documentos:

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)
