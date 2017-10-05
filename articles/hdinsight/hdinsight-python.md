---
title: Funciones definidas por el usuario (UDF) de Python con Apache Hive y Pig - Azure HDInsight | Microsoft Docs
description: "Vea cómo usar funciones definidas por el usuario (UDF) de Python desde Hive y Pig en HDInsight, la pila de tecnología de Hadoop en Azure."
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
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="5006d-103">Uso de funciones definidas por el usuario (UDF) de Python con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5006d-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="5006d-104">Aprenda a usar funciones definidas por el usuario (UDF) de Python con Apache Hive y Pig en Hadoop en Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="5006d-105"><a name="python"></a>Python en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5006d-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="5006d-106">Python 2.7 se instala de forma predeterminada en HDInsight 3.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="5006d-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="5006d-107">Apache Hive puede usarse con esta versión de Python para el procesamiento de streaming.</span><span class="sxs-lookup"><span data-stu-id="5006d-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="5006d-108">El procesamiento de streaming utiliza STDOUT y STDIN para pasar datos entre Hive y UDF.</span><span class="sxs-lookup"><span data-stu-id="5006d-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="5006d-109">HDInsight incluye también Jython, que es una implementación de Python escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="5006d-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="5006d-110">Jython se ejecuta directamente en Máquina virtual Java y no utiliza streaming.</span><span class="sxs-lookup"><span data-stu-id="5006d-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="5006d-111">Jython es el intérprete de Python recomendado cuando se usa Python con Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="5006d-112">En los pasos de este documento se realizan las hipótesis siguientes:</span><span class="sxs-lookup"><span data-stu-id="5006d-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="5006d-113">Se crean los scripts de Python en el entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="5006d-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="5006d-114">Se cargan los scripts en HDInsight con el comando `scp` desde una sesión de Bash local o el script de PowerShell proporcionado.</span><span class="sxs-lookup"><span data-stu-id="5006d-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="5006d-115">Si desea utilizar la versión preliminar de [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) para trabajar con HDInsight, debe:</span><span class="sxs-lookup"><span data-stu-id="5006d-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="5006d-116">Crear los scripts dentro del entorno de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="5006d-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="5006d-117">Usar `scp` para cargar los archivos de Cloud Shell a HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="5006d-118">Usar `ssh` de Cloud Shell para conectarse a HDInsight y ejecutar los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="5006d-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="5006d-119"><a name="hivepython"></a>UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="5006d-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="5006d-120">Python se puede usar como UDF desde Hive a través de la instrucción `TRANSFORM` de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="5006d-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="5006d-121">Por ejemplo, el siguiente archivo HiveQL invoca el archivo `hiveudf.py` almacenado en la cuenta de Azure Storage predeterminada para el clúster.</span><span class="sxs-lookup"><span data-stu-id="5006d-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="5006d-122">**HDInsight basado en Linux**</span><span class="sxs-lookup"><span data-stu-id="5006d-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="5006d-123">**HDInsight basado en Windows**</span><span class="sxs-lookup"><span data-stu-id="5006d-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="5006d-124">En los clústeres de HDInsight basados en Windows, la cláusula `USING` debe especificar la ruta completa a python.exe.</span><span class="sxs-lookup"><span data-stu-id="5006d-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="5006d-125">A continuación se muestra lo que hace este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5006d-125">Here's what this example does:</span></span>

1. <span data-ttu-id="5006d-126">La instrucción `add file` al comienzo del archivo agrega el archivo `hiveudf.py` a la memoria caché distribuida, de modo que todos los nodos del clúster puedan acceder a él.</span><span class="sxs-lookup"><span data-stu-id="5006d-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="5006d-127">La instrucción `SELECT TRANSFORM ... USING` selecciona datos desde `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="5006d-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="5006d-128">También pasa los valores clientid, devicemake y devicemodel al script `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="5006d-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="5006d-129">La cláusula `AS` describe los campos devueltos por `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="5006d-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="5006d-130">Creación del archivo hiveudf.py</span><span class="sxs-lookup"><span data-stu-id="5006d-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="5006d-131">En el entorno de desarrollo, cree un archivo de texto denominado `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="5006d-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="5006d-132">Use el siguiente código como contenido del archivo:</span><span class="sxs-lookup"><span data-stu-id="5006d-132">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="5006d-133">Este script realiza las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="5006d-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="5006d-134">Leer una línea de datos de STDIN.</span><span class="sxs-lookup"><span data-stu-id="5006d-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="5006d-135">El carácter de nueva línea final se quita mediante `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="5006d-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="5006d-136">Al realizar el procesamiento por secuencias, una sola línea contiene todos los valores con un carácter de tabulación entre cada uno.</span><span class="sxs-lookup"><span data-stu-id="5006d-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="5006d-137">Por tanto se puede usar `string.split(line, "\t")` para dividir la entrada en cada tabulación y que solo se devuelvan los campos.</span><span class="sxs-lookup"><span data-stu-id="5006d-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="5006d-138">Cuando el procesamiento haya finalizado, la salida se debe escribir en STDOUT como una sola línea, con una tabulación entre cada campo.</span><span class="sxs-lookup"><span data-stu-id="5006d-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="5006d-139">Por ejemplo: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="5006d-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="5006d-140">El bucle `while` se repite hasta que no se lee ningún `line`.</span><span class="sxs-lookup"><span data-stu-id="5006d-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="5006d-141">La salida del script es una concatenación de los valores de entrada de `devicemake` y `devicemodel`, y un hash del valor concatenado.</span><span class="sxs-lookup"><span data-stu-id="5006d-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="5006d-142">Consulte [Ejecución de los ejemplos](#running) para obtener información sobre cómo ejecutar este ejemplo en su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="5006d-143"><a name="pigpython"></a>UDF de Pig</span><span class="sxs-lookup"><span data-stu-id="5006d-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="5006d-144">Un script de Python se puede usar como UDF desde Pig a través de la instrucción `GENERATE`.</span><span class="sxs-lookup"><span data-stu-id="5006d-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="5006d-145">Puede ejecutar el script mediante Jython o C Python.</span><span class="sxs-lookup"><span data-stu-id="5006d-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="5006d-146">Jython se ejecuta en JVM y se puede llamar de forma nativa desde Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="5006d-147">C Python es un proceso externo, por lo que los datos de Pig en JVM se envían al script que se ejecuta en un proceso de Python.</span><span class="sxs-lookup"><span data-stu-id="5006d-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="5006d-148">La salida del script de Python se devuelve a Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="5006d-149">Para especificar el intérprete de Python, use `register` al hacer referencia al script de Python.</span><span class="sxs-lookup"><span data-stu-id="5006d-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="5006d-150">Los ejemplos siguientes registran scripts con Pig como `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="5006d-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="5006d-151">**Para usar Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="5006d-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="5006d-152">**Para usar C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="5006d-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5006d-153">Al usar Jython, la ruta de acceso al archivo pig_jython puede ser una ruta de acceso local o una ruta de acceso WASB://.</span><span class="sxs-lookup"><span data-stu-id="5006d-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="5006d-154">Sin embargo, cuando se usa C Python, se debe hacer referencia a un archivo local en el sistema de archivos local del nodo que se usa para enviar el trabajo de Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="5006d-155">Pasado el registro, el Pig Latin en este ejemplo es el mismo para ambos:</span><span class="sxs-lookup"><span data-stu-id="5006d-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="5006d-156">A continuación se muestra lo que hace este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5006d-156">Here's what this example does:</span></span>

1. <span data-ttu-id="5006d-157">La primera línea carga el archivo de datos de ejemplo `sample.log` en `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="5006d-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="5006d-158">También define cada registro como `chararray`.</span><span class="sxs-lookup"><span data-stu-id="5006d-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="5006d-159">La siguiente línea filtra los valores nulos y almacena el resultado de la operación en `LOG`.</span><span class="sxs-lookup"><span data-stu-id="5006d-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="5006d-160">A continuación, recorre en iteración los registros de `LOG` y usa `GENERATE` para invocar el método `create_structure` en el script de Python/Jython cargado como `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="5006d-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="5006d-161">`LINE` se usa para pasar el registro actual a la función.</span><span class="sxs-lookup"><span data-stu-id="5006d-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="5006d-162">Por último, los resultados se vuelcan en STDOUT con el comando `DUMP`.</span><span class="sxs-lookup"><span data-stu-id="5006d-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="5006d-163">Este comando muestra los resultados una vez finalizada la operación.</span><span class="sxs-lookup"><span data-stu-id="5006d-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="5006d-164">Creación del archivo pigudf.py</span><span class="sxs-lookup"><span data-stu-id="5006d-164">Create the pigudf.py file</span></span>

<span data-ttu-id="5006d-165">En el entorno de desarrollo, cree un archivo de texto denominado `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="5006d-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="5006d-166">Use el siguiente código como contenido del archivo:</span><span class="sxs-lookup"><span data-stu-id="5006d-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="5006d-167">En el ejemplo de Pig Latin hemos definido la entrada `LINE` como chararray porque no había un esquema coherente para la entrada.</span><span class="sxs-lookup"><span data-stu-id="5006d-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="5006d-168">El script de Python transforma los datos en un esquema coherente para la salida.</span><span class="sxs-lookup"><span data-stu-id="5006d-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="5006d-169">La instrucción `@outputSchema` define el formato de los datos que se devuelven a Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="5006d-170">En este caso es un **contenedor de datos**, que es un tipo de datos de Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="5006d-171">El contenedor contiene los siguientes campos, los cuales son todos chararray (cadenas):</span><span class="sxs-lookup"><span data-stu-id="5006d-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="5006d-172">date: la fecha en la que se creó la entrada del registro</span><span class="sxs-lookup"><span data-stu-id="5006d-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="5006d-173">time: la hora a la que se creó la entrada del registro</span><span class="sxs-lookup"><span data-stu-id="5006d-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="5006d-174">classname: el nombre de la clase para la que se creó la entrada</span><span class="sxs-lookup"><span data-stu-id="5006d-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="5006d-175">level: el nivel de registro</span><span class="sxs-lookup"><span data-stu-id="5006d-175">level - the log level</span></span>
   * <span data-ttu-id="5006d-176">detail: los detalles de la entrada del registro</span><span class="sxs-lookup"><span data-stu-id="5006d-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="5006d-177">A continuación, `def create_structure(input)` define la función a la que Pig pasa elementos de línea.</span><span class="sxs-lookup"><span data-stu-id="5006d-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="5006d-178">Los datos de ejemplo, `sample.log`se ajustan principalmente al esquema de date, time, classname, level y detail que queremos devolver.</span><span class="sxs-lookup"><span data-stu-id="5006d-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="5006d-179">Sin embargo, contiene unas pocas líneas que comienzan por `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="5006d-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="5006d-180">Estas líneas deben modificarse para que coincidan con el esquema.</span><span class="sxs-lookup"><span data-stu-id="5006d-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="5006d-181">La instrucción `if` las busca y luego modifica los datos de entrada para mover la cadena `*java.lang.Exception*` al final, de forma que pone los datos en línea con nuestro esquema de salida esperado.</span><span class="sxs-lookup"><span data-stu-id="5006d-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="5006d-182">A continuación, se usa el comando `split` para dividir los datos en los primeros cuatro caracteres de espacio.</span><span class="sxs-lookup"><span data-stu-id="5006d-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="5006d-183">La salida se asigna a `date`, `time`, `classname`, `level` y `detail`.</span><span class="sxs-lookup"><span data-stu-id="5006d-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="5006d-184">Finalmente, los valores se devuelven a Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="5006d-185">Entonces tendremos un esquema coherente tal y como se define en la instrucción `@outputSchema`.</span><span class="sxs-lookup"><span data-stu-id="5006d-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="5006d-186"><a name="running"></a>Carga y ejecución de los ejemplos</span><span class="sxs-lookup"><span data-stu-id="5006d-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5006d-187">Los pasos de **SSH** solo funcionan con un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="5006d-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5006d-188">Los pasos de **PowerShell** funcionan con un clúster de HDInsight basado tanto en Linux como en Windows pero es necesario tener un cliente Windows.</span><span class="sxs-lookup"><span data-stu-id="5006d-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="5006d-189">SSH</span><span class="sxs-lookup"><span data-stu-id="5006d-189">SSH</span></span>

<span data-ttu-id="5006d-190">Para obtener más información sobre cómo usar SSH, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5006d-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="5006d-191">Use `scp` para copiar los archivos en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="5006d-192">Por ejemplo, el siguiente comando copia los archivos a un clúster denominado **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="5006d-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="5006d-193">Use SSH para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="5006d-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="5006d-194">En la sesión de SSH, agregue los archivos de python cargados anteriormente en el almacenamiento de WASB para el clúster.</span><span class="sxs-lookup"><span data-stu-id="5006d-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="5006d-195">Después de cargar los archivos, siga los pasos siguientes para ejecutar los trabajos de Hive y Pig.</span><span class="sxs-lookup"><span data-stu-id="5006d-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="5006d-196">Uso del UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="5006d-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="5006d-197">Use el comando `hive` para iniciar el shell de Hive.</span><span class="sxs-lookup"><span data-stu-id="5006d-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="5006d-198">Debería ver un símbolo del sistema `hive>` cuando se haya cargado el shell.</span><span class="sxs-lookup"><span data-stu-id="5006d-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="5006d-199">En el símbolo del sistema `hive>`, escriba la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="5006d-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="5006d-200">Después de escribir la última línea, debe iniciarse el trabajo.</span><span class="sxs-lookup"><span data-stu-id="5006d-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="5006d-201">Cuando el trabajo se completa, devuelve una salida similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5006d-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="5006d-202">Uso del UDF de Pig</span><span class="sxs-lookup"><span data-stu-id="5006d-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="5006d-203">Use el comando `pig` para iniciar el shell.</span><span class="sxs-lookup"><span data-stu-id="5006d-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="5006d-204">Verá un símbolo del sistema `grunt>` cuando se haya cargado el shell.</span><span class="sxs-lookup"><span data-stu-id="5006d-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="5006d-205">En el símbolo del sistema `grunt>`, escriba las siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="5006d-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="5006d-206">Después de escribir la siguiente línea, debe iniciarse el trabajo.</span><span class="sxs-lookup"><span data-stu-id="5006d-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="5006d-207">Cuando el trabajo se completa, devuelve una salida similar a los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5006d-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="5006d-208">Use `quit` para salir del shell de Grunt y use lo siguiente para editar el archivo pigudf.py en el sistema de archivos local:</span><span class="sxs-lookup"><span data-stu-id="5006d-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="5006d-209">Una vez en el editor, quite la siguiente línea de comentario eliminando el carácter `#` del principio de la línea:</span><span class="sxs-lookup"><span data-stu-id="5006d-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="5006d-210">Cuando se haya realizado el cambio, use Ctrl + X para salir del editor.</span><span class="sxs-lookup"><span data-stu-id="5006d-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="5006d-211">Seleccione Y y, a continuación, Entrar para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="5006d-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="5006d-212">Use el comando `pig` para iniciar de nuevo el shell.</span><span class="sxs-lookup"><span data-stu-id="5006d-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="5006d-213">Cuando esté en el símbolo del sistema `grunt>` , use lo siguiente para ejecutar el script de Python con el intérprete de C Python.</span><span class="sxs-lookup"><span data-stu-id="5006d-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="5006d-214">Una vez completado este trabajo, verá la misma salida que cuando anteriormente ejecutó el script mediante Jython.</span><span class="sxs-lookup"><span data-stu-id="5006d-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="5006d-215">PowerShell: carga de los archivos</span><span class="sxs-lookup"><span data-stu-id="5006d-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="5006d-216">Puede usar PowerShell para cargar los archivos en el servidor de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="5006d-217">Use el siguiente script de para cargar los archivos de Python:</span><span class="sxs-lookup"><span data-stu-id="5006d-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5006d-218">En los pasos de esta sección se usa Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5006d-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="5006d-219">Para más información sobre cómo usar Azure PowerShell, consulte [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalación y configuración de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5006d-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
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
> <span data-ttu-id="5006d-220">Cambiar el valor `C:\path\to` a la ruta de acceso a los archivos del entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="5006d-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="5006d-221">Este script recupera información del clúster de HDInsight, luego extrae la cuenta y la clave de la cuenta de almacenamiento predeterminada y seguidamente carga los archivos en la raíz del contenedor.</span><span class="sxs-lookup"><span data-stu-id="5006d-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="5006d-222">Para más información sobre la carga de archivos, consulte el documento [Carga de datos para trabajos de Hadoop en HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="5006d-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="5006d-223">PowerShell: uso del UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="5006d-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="5006d-224">PowerShell también puede utilizarse para ejecutar consultas de Hive de forma remota.</span><span class="sxs-lookup"><span data-stu-id="5006d-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="5006d-225">Use el siguiente script de PowerShell para ejecutar una consulta de Hive que use el script **hiveudf.py**:</span><span class="sxs-lookup"><span data-stu-id="5006d-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5006d-226">Antes de ejecutarse, el script solicita la información de la cuenta de administrador/HTTPs para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
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
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="5006d-227">La salida del trabajo de **Hive** debe parecerse al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5006d-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="5006d-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="5006d-228">Pig (Jython)</span></span>

<span data-ttu-id="5006d-229">PowerShell también puede utilizarse para ejecutar trabajos de Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="5006d-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="5006d-230">Para ejecutar un trabajo de Pig Latin que utilice el script **pigudf.py**, use el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5006d-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="5006d-231">Al enviar de forma remota un trabajo mediante PowerShell, no es posible usar Python C como intérprete.</span><span class="sxs-lookup"><span data-stu-id="5006d-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

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

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="5006d-232">La salida del trabajo de **Pig** debe parecerse a los datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5006d-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="5006d-233"><a name="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5006d-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="5006d-234">Errores en la ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="5006d-234">Errors when running jobs</span></span>

<span data-ttu-id="5006d-235">Al ejecutar el trabajo de Hive, es posible que se produzca un error similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="5006d-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="5006d-236">Este problema puede deberse a los finales de línea del archivo de Python.</span><span class="sxs-lookup"><span data-stu-id="5006d-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="5006d-237">De forma predeterminada, muchos editores de Windows usan CRLF como final de línea, pero las aplicaciones Linux normalmente esperan caracteres LF.</span><span class="sxs-lookup"><span data-stu-id="5006d-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="5006d-238">Puede usar las siguientes instrucciones de PowerShell para quitar los caracteres CR antes de cargar el archivo en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5006d-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="5006d-239">Scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5006d-239">PowerShell scripts</span></span>

<span data-ttu-id="5006d-240">Ambos scripts de ejemplo de PowerShell usados para ejecutar los ejemplos contienen una línea comentada que muestra una salida con error para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="5006d-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="5006d-241">Si no ve la salida esperada del trabajo, quite los comentarios de la siguiente línea y observe si la información de error indica un problema.</span><span class="sxs-lookup"><span data-stu-id="5006d-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="5006d-242">La información de error (STDERR) y el resultado del trabajo (STDOUT) también se registran en el almacenamiento para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5006d-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="5006d-243">Para este trabajo...</span><span class="sxs-lookup"><span data-stu-id="5006d-243">For this job...</span></span> | <span data-ttu-id="5006d-244">Examine estos archivos en el contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="5006d-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="5006d-245">Hive</span><span class="sxs-lookup"><span data-stu-id="5006d-245">Hive</span></span> |<span data-ttu-id="5006d-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="5006d-246">/HivePython/stderr</span></span><p><span data-ttu-id="5006d-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="5006d-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="5006d-248">Pig</span><span class="sxs-lookup"><span data-stu-id="5006d-248">Pig</span></span> |<span data-ttu-id="5006d-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="5006d-249">/PigPython/stderr</span></span><p><span data-ttu-id="5006d-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="5006d-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="5006d-251"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5006d-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="5006d-252">Si necesita cargar módulos de Python que no se proporcionan de forma predeterminada, consulte [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx) (Implementación de un módulo en HDInsight de Azure).</span><span class="sxs-lookup"><span data-stu-id="5006d-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="5006d-253">Para conocer otras formas de usar Pig y Hive, y para obtener información sobre el uso de MapReduce, consulte los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="5006d-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="5006d-254">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="5006d-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5006d-255">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="5006d-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5006d-256">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="5006d-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
