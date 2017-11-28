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
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="e1065-103">Uso de funciones definidas por el usuario (UDF) de Python con Hive y Pig en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1065-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="e1065-104">Obtenga información acerca de cómo toouse Python definidos por el usuario (UDF) las funciones con Apache Hive y Pig en Hadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1065-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="e1065-105"><a name="python"></a>Python en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1065-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="e1065-106">Python 2.7 se instala de forma predeterminada en HDInsight 3.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="e1065-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="e1065-107">Apache Hive puede usarse con esta versión de Python para el procesamiento de streaming.</span><span class="sxs-lookup"><span data-stu-id="e1065-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="e1065-108">Procesamiento de flujo utiliza STDOUT y STDIN datos toopass entre Hive y Hola UDF.</span><span class="sxs-lookup"><span data-stu-id="e1065-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="e1065-109">HDInsight incluye también Jython, que es una implementación de Python escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="e1065-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="e1065-110">Jython se ejecuta directamente en la máquina Virtual Java de hello y no utiliza la transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="e1065-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="e1065-111">Jython es Hola recomienda intérprete de Python para usar Python con Pig.</span><span class="sxs-lookup"><span data-stu-id="e1065-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="e1065-112">pasos de Hello en este documento muestran Hola siguientes supuestos:</span><span class="sxs-lookup"><span data-stu-id="e1065-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="e1065-113">Crear scripts de Python de hello en el entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="e1065-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="e1065-114">Cargar tooHDInsight de secuencias de comandos de hello mediante cualquier hello `scp` comando desde una sesión intensiva de errores local u Hola proporcionado script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1065-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="e1065-115">Si desea que hello toouse [Shell de nube de Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) obtener una vista previa de toowork con HDInsight, a continuación, debe:</span><span class="sxs-lookup"><span data-stu-id="e1065-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="e1065-116">Crear secuencias de comandos de hello en el entorno del shell de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="e1065-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="e1065-117">Use `scp` archivos de hello tooupload de hello tooHDInsight de shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="e1065-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="e1065-118">Use `ssh` de hello en la nube shell tooconnect tooHDInsight y ejemplos de ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="e1065-119"><a name="hivepython"></a>UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="e1065-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="e1065-120">Python puede utilizarse como una UDF de Hive a través de hello HiveQL `TRANSFORM` instrucción.</span><span class="sxs-lookup"><span data-stu-id="e1065-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="e1065-121">Por ejemplo, hello después HiveQL invoca hello `hiveudf.py` archivo almacenado en la cuenta de almacenamiento de Azure Hola predeterminada para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="e1065-122">**HDInsight basado en Linux**</span><span class="sxs-lookup"><span data-stu-id="e1065-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="e1065-123">**HDInsight basado en Windows**</span><span class="sxs-lookup"><span data-stu-id="e1065-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="e1065-124">En los clústeres de HDInsight basados en Windows, Hola `USING` cláusula debe especificar Hola ruta de acceso completa toopython.exe.</span><span class="sxs-lookup"><span data-stu-id="e1065-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="e1065-125">A continuación se muestra lo que hace este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e1065-125">Here's what this example does:</span></span>

1. <span data-ttu-id="e1065-126">Hola `add file` instrucción al principio de hello del archivo hello agrega hello `hiveudf.py` toohello de archivos distribuido de memoria caché, por lo que es accesible para todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="e1065-127">Hola `SELECT TRANSFORM ... USING` instrucción selecciona datos de hello `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="e1065-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="e1065-128">También pasa Hola clientid, devicemake y devicemodel valores toohello `hiveudf.py` secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="e1065-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="e1065-129">Hola `AS` cláusula describe campos Hola devueltos desde `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="e1065-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="e1065-130">Crear archivo de hello hiveudf.py</span><span class="sxs-lookup"><span data-stu-id="e1065-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="e1065-131">En el entorno de desarrollo, cree un archivo de texto denominado `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="e1065-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="e1065-132">Usar hello siguiente código como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="e1065-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="e1065-133">Este script realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="e1065-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="e1065-134">Leer una línea de datos de STDIN.</span><span class="sxs-lookup"><span data-stu-id="e1065-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="e1065-135">Hola caracteres de nueva línea final se quita mediante `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="e1065-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="e1065-136">Al realizar el procesamiento de la secuencia, una sola línea contiene todos los valores de hello con un carácter de tabulación entre cada valor.</span><span class="sxs-lookup"><span data-stu-id="e1065-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="e1065-137">Por lo que `string.split(line, "\t")` puede ser hello toosplit usado en cada pestaña, devolver simplemente Hola campos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e1065-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="e1065-138">Una vez completado el procesamiento, salida de hello debe escribirse tooSTDOUT como una sola línea, con una tabulación entre cada campo.</span><span class="sxs-lookup"><span data-stu-id="e1065-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="e1065-139">Por ejemplo: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="e1065-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="e1065-140">Hola `while` bucle se repite hasta que no `line` se lee.</span><span class="sxs-lookup"><span data-stu-id="e1065-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="e1065-141">salida del script de Hola es una concatenación de valores de entrada de Hola para `devicemake` y `devicemodel`, y un hash del programa Hola a un valor concatenado.</span><span class="sxs-lookup"><span data-stu-id="e1065-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="e1065-142">Vea [ejecutar ejemplos de hello](#running) para saber cómo toorun este ejemplo en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1065-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="e1065-143"><a name="pigpython"></a>UDF de Pig</span><span class="sxs-lookup"><span data-stu-id="e1065-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="e1065-144">Puede utilizar un script de Python como una UDF de Pig mediante hello `GENERATE` instrucción.</span><span class="sxs-lookup"><span data-stu-id="e1065-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="e1065-145">Puede ejecutar script de Hola mediante Jython o C Python.</span><span class="sxs-lookup"><span data-stu-id="e1065-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="e1065-146">Jython se ejecuta en hello JVM y forma nativa pueden llamarse desde Pig.</span><span class="sxs-lookup"><span data-stu-id="e1065-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="e1065-147">C Python es un proceso externo, por lo que los datos de Hola de Pig en hello JVM se envía toohello script que se ejecuta en un proceso de Python.</span><span class="sxs-lookup"><span data-stu-id="e1065-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="e1065-148">la salida de Hello de script de Python Hola se envía en Pig.</span><span class="sxs-lookup"><span data-stu-id="e1065-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="e1065-149">intérprete de Python toospecify hello, use `register` al hacer referencia a scripts de Python Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="e1065-150">Hello en los ejemplos siguientes registrar scripts con Pig como `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="e1065-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="e1065-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="e1065-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="e1065-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="e1065-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1065-153">Al utilizar Jython, toohello pig_jython archivo de hello ruta de acceso puede ser una ruta de acceso local o una WASB: / / ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="e1065-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="e1065-154">Sin embargo, al utilizar C Python, debe hacer referencia a un archivo en el sistema de archivos local de hello del nodo de Hola que usa el trabajo de Pig toosubmit Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="e1065-155">Una vez más allá de registro, hello Pig latino para este ejemplo Hola mismo para ambos:</span><span class="sxs-lookup"><span data-stu-id="e1065-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="e1065-156">A continuación se muestra lo que hace este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e1065-156">Here's what this example does:</span></span>

1. <span data-ttu-id="e1065-157">Hola primera línea carga el archivo de datos de ejemplo de Hola, `sample.log` en `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="e1065-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="e1065-158">También define cada registro como `chararray`.</span><span class="sxs-lookup"><span data-stu-id="e1065-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="e1065-159">línea siguiente de Hello filtra los valores null, almacenando el resultado de hello de operación de hello en `LOG`.</span><span class="sxs-lookup"><span data-stu-id="e1065-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="e1065-160">A continuación, recorre en iteración los registros de hello en `LOG` y utiliza `GENERATE` tooinvoke hello `create_structure` método incluido en script de Python/Jython Hola se carga como `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="e1065-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="e1065-161">`LINE`es toopass utilizados en función de registro toohello actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="e1065-162">Por último, salidas de hello son los tooSTDOUT con hello `DUMP` comando.</span><span class="sxs-lookup"><span data-stu-id="e1065-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="e1065-163">Este comando muestra los resultados de hello al finalizar la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="e1065-164">Crear archivo de hello pigudf.py</span><span class="sxs-lookup"><span data-stu-id="e1065-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="e1065-165">En el entorno de desarrollo, cree un archivo de texto denominado `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="e1065-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="e1065-166">Usar hello siguiente código como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="e1065-166">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="e1065-167">En el ejemplo de Hola Pig latino, definimos hello `LINE` de entrada como un chararray porque no hay ningún esquema coherente para la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="e1065-168">Hola script de Python transforma los datos de hello en un esquema coherente para la salida.</span><span class="sxs-lookup"><span data-stu-id="e1065-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="e1065-169">Hola `@outputSchema` instrucción define el formato de Hola de datos de Hola que se devuelven tooPig.</span><span class="sxs-lookup"><span data-stu-id="e1065-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="e1065-170">En este caso es un **contenedor de datos**, que es un tipo de datos de Pig.</span><span class="sxs-lookup"><span data-stu-id="e1065-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="e1065-171">contenedor de Hello contiene Hola después de campos, todos ellos son chararray (cadenas):</span><span class="sxs-lookup"><span data-stu-id="e1065-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="e1065-172">fecha: hello entrada del registro de hello de fecha se creó</span><span class="sxs-lookup"><span data-stu-id="e1065-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="e1065-173">hora: Hola se creó la entrada de registro de hello</span><span class="sxs-lookup"><span data-stu-id="e1065-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="e1065-174">ClassName - entrada de Hola de nombre de clase de Hola se creó para</span><span class="sxs-lookup"><span data-stu-id="e1065-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="e1065-175">nivel - nivel de registro de hello</span><span class="sxs-lookup"><span data-stu-id="e1065-175">level - hello log level</span></span>
   * <span data-ttu-id="e1065-176">detalle: entrada de registro de información detallada para hello</span><span class="sxs-lookup"><span data-stu-id="e1065-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="e1065-177">A continuación, Hola `def create_structure(input)` define la función hello que Pig pasa artículos de línea.</span><span class="sxs-lookup"><span data-stu-id="e1065-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="e1065-178">datos de ejemplo de Hola `sample.log`, principalmente se ajusta toohello fecha, hora, classname, nivel y de detalle que deseamos tooreturn de esquema.</span><span class="sxs-lookup"><span data-stu-id="e1065-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="e1065-179">Sin embargo, contiene unas pocas líneas que comienzan por `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="e1065-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="e1065-180">Estas líneas deben ser el esquema de hello toomatch modificado.</span><span class="sxs-lookup"><span data-stu-id="e1065-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="e1065-181">Hola `if` instrucción comprueba para las que, a continuación, mensajes Hola Hola toomove de datos de entrada `*java.lang.Exception*` final de cadena toohello, volver a poner Hola datos en línea con el esquema de resultado esperado.</span><span class="sxs-lookup"><span data-stu-id="e1065-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="e1065-182">A continuación, Hola `split` comando es datos de hello toosplit usados en los primeros caracteres de espacio en cuatro Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="e1065-183">salida de Hello se asigna en `date`, `time`, `classname`, `level`, y `detail`.</span><span class="sxs-lookup"><span data-stu-id="e1065-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="e1065-184">Por último, se devuelven valores de hello tooPig.</span><span class="sxs-lookup"><span data-stu-id="e1065-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="e1065-185">Cuando se devuelven datos de hello tooPig, tiene un esquema coherente tal como se define en hello `@outputSchema` instrucción.</span><span class="sxs-lookup"><span data-stu-id="e1065-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="e1065-186"><a name="running"></a>Cargar y ejecutar los ejemplos de hello</span><span class="sxs-lookup"><span data-stu-id="e1065-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1065-187">Hola **SSH** pasos sólo funcionan con un clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="e1065-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e1065-188">Hola **PowerShell** pasos de trabajo con clúster Linux o de HDInsight basados en Windows, pero requiere un cliente de Windows.</span><span class="sxs-lookup"><span data-stu-id="e1065-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="e1065-189">SSH</span><span class="sxs-lookup"><span data-stu-id="e1065-189">SSH</span></span>

<span data-ttu-id="e1065-190">Para obtener más información sobre cómo usar SSH, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e1065-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="e1065-191">Use `scp` clúster de HDInsight de toocopy Hola archivos tooyour.</span><span class="sxs-lookup"><span data-stu-id="e1065-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="e1065-192">Por ejemplo, Hola siguiente copias Hola clúster tooa de archivos con el nombre de comando **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="e1065-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="e1065-193">Utilizar SSH tooconnect toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="e1065-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="e1065-194">Desde la sesión de SSH de hello, agregar archivos de python Hola cargan previamente toohello almacenamiento WASB Hola del clúster.</span><span class="sxs-lookup"><span data-stu-id="e1065-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="e1065-195">Después de cargar archivos de hello, pasos siguientes de Hola de uso toorun Hola Hive y los trabajos de Pig.</span><span class="sxs-lookup"><span data-stu-id="e1065-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="e1065-196">Usar hello Hive UDF</span><span class="sxs-lookup"><span data-stu-id="e1065-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="e1065-197">Hola de uso `hive` toostart Hola hive shell de comandos.</span><span class="sxs-lookup"><span data-stu-id="e1065-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="e1065-198">Debería ver un `hive>` solicitar una vez que ha cargado el shell de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="e1065-199">Escriba Hola después de consulta en hello `hive>` símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="e1065-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="e1065-200">Después de escribir la última línea de hello, debe iniciar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="e1065-201">Cuando se completa el trabajo de hello, devuelve toohello similar de salida siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e1065-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="e1065-202">Usar hello Pig UDF</span><span class="sxs-lookup"><span data-stu-id="e1065-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="e1065-203">Hola de uso `pig` toostart Hola shell de comandos.</span><span class="sxs-lookup"><span data-stu-id="e1065-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="e1065-204">Verá un `grunt>` solicitar una vez que ha cargado el shell de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="e1065-205">Escriba Hola siguiendo las instrucciones en hello `grunt>` símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="e1065-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="e1065-206">Después de escribir Hola después de línea, debe iniciar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="e1065-207">Cuando se completa el trabajo de hello, devuelve toohello similar de salida datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1065-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="e1065-208">Usar `quit` tooexit Hola shell Grunt y, a continuación, usar hello tooedit hello pigudf.py archivo en el sistema de archivos local de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1065-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="e1065-209">Una vez en el editor de hello, quite Hola después de línea mediante la eliminación de hello `#` carácter desde principio Hola de línea hello:</span><span class="sxs-lookup"><span data-stu-id="e1065-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="e1065-210">Una vez que se ha realizado el cambio de hello, utilizarlo CTRL+x tooexit Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="e1065-211">Seleccione Y y, a continuación, escriba los cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e1065-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="e1065-212">Hola de uso `pig` comando shell de toostart Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e1065-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="e1065-213">Una vez que esté en hello `grunt>` símbolo del sistema, use Hola después de script de Python de hello toorun con intérprete de Python C Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="e1065-214">Al finalizar este trabajo, verá Hola de salida igual que cuando se ejecuta antes script de Hola mediante Jython.</span><span class="sxs-lookup"><span data-stu-id="e1065-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="e1065-215">PowerShell: Cargar los archivos Hola</span><span class="sxs-lookup"><span data-stu-id="e1065-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="e1065-216">Puede usar PowerShell tooupload Hola archivos toohello HDInsight del servidor.</span><span class="sxs-lookup"><span data-stu-id="e1065-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="e1065-217">Usar hello siguientes archivos de script tooupload Hola Python:</span><span class="sxs-lookup"><span data-stu-id="e1065-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e1065-218">pasos de Hello en esta sección usan Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1065-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="e1065-219">Para obtener más información sobre cómo usar PowerShell de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e1065-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

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
> <span data-ttu-id="e1065-220">Hola de cambio `C:\path\to` valor toohello archivos de toohello de ruta de acceso en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e1065-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="e1065-221">Este script recupera información para el clúster de HDInsight, a continuación, extrae la cuenta de hello y la clave de cuenta de almacenamiento predeterminada de Hola y cargas Hola raíz de toohello los archivos del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="e1065-222">Para obtener más información sobre la carga de archivos, vea hello [cargar datos para los trabajos de Hadoop en HDInsight](hdinsight-upload-data.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e1065-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="e1065-223">PowerShell: Hola de uso Hive UDF</span><span class="sxs-lookup"><span data-stu-id="e1065-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="e1065-224">PowerShell también puede ser utilizados tooremotely ejecutar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="e1065-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="e1065-225">Hola de uso después de script de PowerShell toorun una consulta de Hive que usa **hiveudf.py** secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="e1065-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1065-226">Antes de ejecutar, script de Hola solicita Hola HTTPs/Admin de información de cuenta para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1065-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

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

<span data-ttu-id="e1065-227">Hola salida de hello **Hive** trabajo debe aparecer similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e1065-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="e1065-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="e1065-228">Pig (Jython)</span></span>

<span data-ttu-id="e1065-229">PowerShell también puede ser utilizados toorun Pig latino trabajos.</span><span class="sxs-lookup"><span data-stu-id="e1065-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="e1065-230">un trabajo de Pig latino que utiliza hello toorun **pigudf.py** script, use el siguiente script de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="e1065-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="e1065-231">Al enviar remotamente un trabajo con PowerShell, no es posible toouse Python C como intérprete Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

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

<span data-ttu-id="e1065-232">Hola salida de hello **Pig** trabajo debe aparecer toohello similar datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1065-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="e1065-233"><a name="troubleshooting"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e1065-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="e1065-234">Errores en la ejecución de trabajos</span><span class="sxs-lookup"><span data-stu-id="e1065-234">Errors when running jobs</span></span>

<span data-ttu-id="e1065-235">Cuando se ejecuta el trabajo de hive de hello, puede producirse un toohello de error similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e1065-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="e1065-236">Este problema puede deberse a finales de línea hello en el archivo de Python de hello.</span><span class="sxs-lookup"><span data-stu-id="e1065-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="e1065-237">Muchos editores de Windows predeterminado toousing CRLF como de fin de línea hello, pero las aplicaciones Linux usualmente esperan LF.</span><span class="sxs-lookup"><span data-stu-id="e1065-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="e1065-238">Puede usar Hola PowerShell instrucciones tooremove Hola CR caracteres que le siguen antes de cargar Hola archivo tooHDInsight:</span><span class="sxs-lookup"><span data-stu-id="e1065-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="e1065-239">Scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1065-239">PowerShell scripts</span></span>

<span data-ttu-id="e1065-240">Ambos de ejemplo de Hola a scripts de PowerShell usan los ejemplos de hello toorun contienen una línea comentada que muestra la salida de error de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1065-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="e1065-241">Si no ve salida Hola espera trabajo de hello, quite la línea siguiente de Hola y vea si la información de error de hello indica un problema.</span><span class="sxs-lookup"><span data-stu-id="e1065-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="e1065-242">información de error de Hello (STDERR) y el resultado de hello de trabajo de hello (STDOUT) también están registrados tooyour HDInsight almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e1065-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="e1065-243">Para este trabajo...</span><span class="sxs-lookup"><span data-stu-id="e1065-243">For this job...</span></span> | <span data-ttu-id="e1065-244">Examine estos archivos en el contenedor de blobs de Hola</span><span class="sxs-lookup"><span data-stu-id="e1065-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="e1065-245">Hive</span><span class="sxs-lookup"><span data-stu-id="e1065-245">Hive</span></span> |<span data-ttu-id="e1065-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="e1065-246">/HivePython/stderr</span></span><p><span data-ttu-id="e1065-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="e1065-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="e1065-248">Pig</span><span class="sxs-lookup"><span data-stu-id="e1065-248">Pig</span></span> |<span data-ttu-id="e1065-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="e1065-249">/PigPython/stderr</span></span><p><span data-ttu-id="e1065-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="e1065-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="e1065-251"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1065-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="e1065-252">Si tiene módulos de Python tooload que no se proporcionan de forma predeterminada, consulte [cómo toodeploy una tooAzure módulo HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1065-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="e1065-253">Para otras formas toouse Pig, Hive y toolearn sobre el uso de MapReduce, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="e1065-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="e1065-254">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1065-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e1065-255">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1065-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e1065-256">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1065-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
