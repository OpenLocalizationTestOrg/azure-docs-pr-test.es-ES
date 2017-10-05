---
title: "Serialización de datos en Hadoop - Microsoft Avro Library - Azure | Microsoft Docs"
description: Aprenda a serializar y deserializar los datos en Hadoop en HDInsight con Microsoft Avro Library para conservar en la memoria una base de datos o un archivo.
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: d06bf8ff4a21e4f4b29593bac32bfa2b32601fc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="serialize-data-in-hadoop-with-the-microsoft-avro-library"></a><span data-ttu-id="69219-104">Serialización de datos en Hadoop con Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="69219-104">Serialize data in Hadoop with the Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="69219-105">El SDK de Avro ya no es compatible con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69219-105">The Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="69219-106">La biblioteca es compatible con la comunidad de código abierto.</span><span class="sxs-lookup"><span data-stu-id="69219-106">The library is open source community supported.</span></span> <span data-ttu-id="69219-107">Los orígenes de la biblioteca se encuentran en [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="69219-107">The sources for the library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="69219-108">En este tema se muestra cómo a usar [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) con el fin de serializar objetos y otras estructuras de datos en secuencias para que persistan en la memoria, una base de datos o un archivo.</span><span class="sxs-lookup"><span data-stu-id="69219-108">This topic shows how to use the [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) to serialize objects and other data structures into streams to persist them to memory, a database, or a file.</span></span> <span data-ttu-id="69219-109">También muestra cómo deserializarlos para recuperar los objetos originales.</span><span class="sxs-lookup"><span data-stu-id="69219-109">It also shows how to deserialize them to recover the original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="69219-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="69219-110">Apache Avro</span></span>
<span data-ttu-id="69219-111"><a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementa el sistema de serialización de datos de Apache Avro para el entorno de Microsoft.NET.</span><span class="sxs-lookup"><span data-stu-id="69219-111">The <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements the Apache Avro data serialization system for the Microsoft.NET environment.</span></span> <span data-ttu-id="69219-112">Apache Avro proporciona un formato compacto de intercambio de datos binarios para la serialización.</span><span class="sxs-lookup"><span data-stu-id="69219-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="69219-113">Utiliza <a href="http://www.json.org" target="_blank">JSON</a> para definir un esquema independiente del lenguaje que garantiza la interoperabilidad de lenguajes.</span><span class="sxs-lookup"><span data-stu-id="69219-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> to define a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="69219-114">Los datos serializados en un lenguaje se pueden leer en otro.</span><span class="sxs-lookup"><span data-stu-id="69219-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="69219-115">Actualmente, se admiten C, C++, C#, Java, PHP, Python y Ruby.</span><span class="sxs-lookup"><span data-stu-id="69219-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="69219-116">Puede encontrar información detallada sobre el formato en la <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">especificación de Apache Avro</a>.</span><span class="sxs-lookup"><span data-stu-id="69219-116">Detailed information on the format can be found in the <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="69219-117">Microsoft Avro Library no admite la parte de llamadas a procedimientos remotos (RPC) de esta especificación.</span><span class="sxs-lookup"><span data-stu-id="69219-117">The Microsoft Avro Library does not support the remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="69219-118">La representación serializada de un objeto en el sistema Avro consta de dos partes: el esquema y el valor real.</span><span class="sxs-lookup"><span data-stu-id="69219-118">The serialized representation of an object in the Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="69219-119">El esquema de Avro describe el modelo de datos independiente del lenguaje de los datos serializados con JSON.</span><span class="sxs-lookup"><span data-stu-id="69219-119">The Avro schema describes the language-independent data model of the serialized data with JSON.</span></span> <span data-ttu-id="69219-120">Se presenta en paralelo con una representación binaria de los datos.</span><span class="sxs-lookup"><span data-stu-id="69219-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="69219-121">Tener el esquema aparte de la representación binaria permite escribir cada objeto sin sobrecargas por valor, lo que agiliza la serialización y reduce la representación.</span><span class="sxs-lookup"><span data-stu-id="69219-121">Having the schema separate from the binary representation permits each object to be written with no per-value overheads, making serialization fast, and the representation small.</span></span>

## <a name="the-hadoop-scenario"></a><span data-ttu-id="69219-122">Escenario de Hadoop</span><span class="sxs-lookup"><span data-stu-id="69219-122">The Hadoop scenario</span></span>
<span data-ttu-id="69219-123">El formato de serialización de Apache Avro se utiliza de forma generalizada en HDIngisht de Azure y otros entornos de Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="69219-123">The Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="69219-124">Avro proporciona una forma práctica de representar estructuras de datos complejas dentro de un trabajo MapReduce de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="69219-124">Avro provides a convenient way to represent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="69219-125">El formato de los archivos de Avro (archivo contenedor de objetos Avro) está diseñado para admitir el modelo de programación distribuida de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="69219-125">The format of Avro files (Avro object container file) has been designed to support the distributed MapReduce programming model.</span></span> <span data-ttu-id="69219-126">La característica clave que permite la distribución es que los archivos son "divisibles" en el sentido de que se puede buscar cualquier punto en un archivo y comenzar a leer desde un bloque concreto.</span><span class="sxs-lookup"><span data-stu-id="69219-126">The key feature that enables the distribution is that the files are “splittable” in the sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="69219-127">Serialización de Avro Library</span><span class="sxs-lookup"><span data-stu-id="69219-127">Serialization in Avro Library</span></span>
<span data-ttu-id="69219-128">La biblioteca de .NET para Avro admite dos formas de serialización de objetos:</span><span class="sxs-lookup"><span data-stu-id="69219-128">The .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="69219-129">**reflexión** : el esquema JSON para los tipos se compila automáticamente a partir de los atributos del contrato de datos de los tipos .NET que se van a serializar.</span><span class="sxs-lookup"><span data-stu-id="69219-129">**reflection** - The JSON schema for the types is automatically built from the data contract attributes of the .NET types to be serialized.</span></span>
* <span data-ttu-id="69219-130">**registro genérico**: el esquema JSON se especifica de forma explícita en un registro representado por la clase [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) cuando no hay tipos .NET para describir el esquema de los datos que se van a serializar.</span><span class="sxs-lookup"><span data-stu-id="69219-130">**generic record** - A JSON schema is explicitly specified in a record represented by the [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present to describe the schema for the data to be serialized.</span></span>

<span data-ttu-id="69219-131">Cuando tanto el escritor como el lector de la secuencia conocen el esquema de los datos, se pueden enviar los datos sin el esquema.</span><span class="sxs-lookup"><span data-stu-id="69219-131">When the data schema is known to both the writer and reader of the stream, the data can be sent without its schema.</span></span> <span data-ttu-id="69219-132">En aquellos casos en los que se utiliza el archivo contenedor de objetos Avro, el esquema se almacena en el archivo.</span><span class="sxs-lookup"><span data-stu-id="69219-132">In cases when an Avro object container file is used, the schema is stored within the file.</span></span> <span data-ttu-id="69219-133">Se pueden especificar otros parámetros, como el códec utilizado para la compresión de datos.</span><span class="sxs-lookup"><span data-stu-id="69219-133">Other parameters, such as the codec used for data compression, can be specified.</span></span> <span data-ttu-id="69219-134">Estos escenarios se explican e ilustran con más detalle en los ejemplos de código siguientes:</span><span class="sxs-lookup"><span data-stu-id="69219-134">These scenarios are outlined in more detail and illustrated in the following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="69219-135">Instalación de Avro Library</span><span class="sxs-lookup"><span data-stu-id="69219-135">Install Avro Library</span></span>
<span data-ttu-id="69219-136">Antes de instalar la biblioteca necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69219-136">The following are required before you install the library:</span></span>

* <span data-ttu-id="69219-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="69219-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="69219-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (v5.6.0.4 o posterior)</span><span class="sxs-lookup"><span data-stu-id="69219-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="69219-139">Tenga en cuenta que la dependencia de Newtonsoft.Json.dll se descarga automáticamente con la instalación de Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="69219-139">Note that the Newtonsoft.Json.dll dependency is downloaded automatically with the installation of the Microsoft Avro Library.</span></span> <span data-ttu-id="69219-140">En la sección siguiente se detalla el procedimiento para ello:</span><span class="sxs-lookup"><span data-stu-id="69219-140">The procedure is provided in the following section:</span></span>

<span data-ttu-id="69219-141">Microsoft Avro Library se distribuye como un paquete de NuGet que se puede instalar desde Visual Studio mediante el siguiente procedimiento:</span><span class="sxs-lookup"><span data-stu-id="69219-141">The Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via the following procedure:</span></span>

1. <span data-ttu-id="69219-142">Elija la pestaña **Proyecto** -> **Administrar paquetes de NuGet...**</span><span class="sxs-lookup"><span data-stu-id="69219-142">Select the **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="69219-143">Busque "Microsoft.Hadoop.Avro" en el cuadro **Búsqueda en línea** .</span><span class="sxs-lookup"><span data-stu-id="69219-143">Search for "Microsoft.Hadoop.Avro" in the **Search Online** box.</span></span>
3. <span data-ttu-id="69219-144">Haga clic en el botón **Instalar** junto a **Microsoft Azure HDInsight Avro Library**.</span><span class="sxs-lookup"><span data-stu-id="69219-144">Click the **Install** button next to **Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="69219-145">Tenga en cuenta que la dependencia de Newtonsoft.Json.dll (>= .6.0.4) se descarga también automáticamente con Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="69219-145">Note that the Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with the Microsoft Avro Library.</span></span>

<span data-ttu-id="69219-146">El código fuente de Microsoft Avro Library está disponible en [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="69219-146">The Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="69219-147">Compilación de esquemas con Avro Library</span><span class="sxs-lookup"><span data-stu-id="69219-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="69219-148">Microsoft Avro Library contiene una utilidad de generación de código que permite la creación de tipos de C# automáticamente en función del esquema JSON previamente definido.</span><span class="sxs-lookup"><span data-stu-id="69219-148">The Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on the previously defined JSON schema.</span></span> <span data-ttu-id="69219-149">La utilidad de generación de código no se distribuye como un ejecutable binario, pero se puede compilar fácilmente mediante el siguiente procedimiento:</span><span class="sxs-lookup"><span data-stu-id="69219-149">The code generation utility is not distributed as a binary executable, but can be easily built via the following procedure:</span></span>

1. <span data-ttu-id="69219-150">Descargue el archivo ZIP con la versión más reciente del código fuente del SDK de HDInsight desde <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK para Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="69219-150">Download the .zip file with the latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="69219-151">(Haga clic en el icono de **Descargar**, no en la pestaña **Descargas**).</span><span class="sxs-lookup"><span data-stu-id="69219-151">(Click the **Download** icon, not the **Downloads** tab.)</span></span>
2. <span data-ttu-id="69219-152">Extraiga el SDK de HDInsight en un directorio que se encuentre en el equipo que tiene .NET Framework 4 instalado y conectado a Internet para descargar los paquetes de NuGet de dependencias necesarios.</span><span class="sxs-lookup"><span data-stu-id="69219-152">Extract the HDInsight SDK to a directory on the machine with .NET Framework 4 installed and connected to the Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="69219-153">Supongamos que el código fuente se ha extraído en C:\SDK.</span><span class="sxs-lookup"><span data-stu-id="69219-153">Below, we assume that the source code is extracted to C:\SDK.</span></span>
3. <span data-ttu-id="69219-154">Vaya a la carpeta C:\SDK\src\Microsoft.Hadoop.Avro.Tools y ejecute build.bat.</span><span class="sxs-lookup"><span data-stu-id="69219-154">Go to the folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="69219-155">(El archivo llama a MS Build desde la distribución de 32 bits de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69219-155">(The file calls MSBuild from the 32-bit distribution of the .NET Framework.</span></span> <span data-ttu-id="69219-156">Si desea utilizar una versión de 64 bits, edite build.bat siguiendo los comentarios que se encuentran dentro del archivo). Asegúrese de que la compilación se haya realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="69219-156">If you would like to use the 64-bit version, edit build.bat, following the comments inside the file.) Ensure that the build is successful.</span></span> <span data-ttu-id="69219-157">(En algunos sistemas, MSBuild puede producir advertencias.</span><span class="sxs-lookup"><span data-stu-id="69219-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="69219-158">Estas advertencias no afectan a la utilidad siempre que no haya ningún error de compilación).</span><span class="sxs-lookup"><span data-stu-id="69219-158">These warnings do not affect the utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="69219-159">La utilidad compilada se encuentra en C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="69219-159">The compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="69219-160">Para familiarizarse con la sintaxis de la línea de comandos, ejecute el comando siguiente desde la carpeta en donde se encuentra la utilidad de generación de código: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="69219-160">To get familiar with the command-line syntax, execute the following command from the folder where the code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="69219-161">Para probar la utilidad, puede generar clases de C# a partir del archivo de esquema JSON de muestra proporcionado con el código fuente.</span><span class="sxs-lookup"><span data-stu-id="69219-161">To test the utility, you can generate C# classes from the sample JSON schema file provided with the source code.</span></span> <span data-ttu-id="69219-162">Ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="69219-162">Execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="69219-163">Se supone que va a producir dos archivos C# en el directorio actual: SensorData.cs y Location.cs.</span><span class="sxs-lookup"><span data-stu-id="69219-163">This is supposed to produce two C# files in the current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="69219-164">Para comprender la lógica que está utilizando la utilidad de generación de código mientras convierte el esquema JSON en tipos de C#, consulte el archivo GenerationVerification.feature que se encuentra en C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="69219-164">To understand the logic that the code generation utility is using while converting the JSON schema to C# types, see the file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="69219-165">Los espacios de nombres se extraen del esquema JSON mediante la lógica descrita en el archivo mencionado en el párrafo anterior.</span><span class="sxs-lookup"><span data-stu-id="69219-165">Namespaces are extracted from the JSON schema, using the logic described in the file mentioned in the previous paragraph.</span></span> <span data-ttu-id="69219-166">Los espacios de nombres extraídos del esquema tienen prioridad sobre lo que se proporcione con el parámetro /n en la línea de comandos de la utilidad.</span><span class="sxs-lookup"><span data-stu-id="69219-166">Namespaces extracted from the schema take precedence over whatever is provided with the /n parameter in the utility command line.</span></span> <span data-ttu-id="69219-167">Si desea reemplazar los espacios de nombres contenidos en el esquema, utilice el parámetro /nf.</span><span class="sxs-lookup"><span data-stu-id="69219-167">If you want to override the namespaces contained within the schema, use the /nf parameter.</span></span> <span data-ttu-id="69219-168">Por ejemplo, para cambiar todos los espacios de nombres de SampleJSONSchema.avsc a my.own.nspace, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="69219-168">For example, to change all namespaces from the SampleJSONSchema.avsc to my.own.nspace, execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-the-samples"></a><span data-ttu-id="69219-169">Información acerca de las muestras</span><span class="sxs-lookup"><span data-stu-id="69219-169">About the samples</span></span>
<span data-ttu-id="69219-170">En este tema se proporcionan seis ejemplos que ilustran escenarios diferentes admitidos por Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="69219-170">Six examples provided in this topic illustrate different scenarios supported by the Microsoft Avro Library.</span></span> <span data-ttu-id="69219-171">Microsoft Avro Library está diseñada para funcionar con cualquier secuencia.</span><span class="sxs-lookup"><span data-stu-id="69219-171">The Microsoft Avro Library is designed to work with any stream.</span></span> <span data-ttu-id="69219-172">En estos ejemplos, los datos se manipulan usando secuencias de memoria en lugar de secuencias de archivos o bases de datos por simplicidad y coherencia.</span><span class="sxs-lookup"><span data-stu-id="69219-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="69219-173">El método que se elija en un entorno de producción depende de los requisitos exactos del escenario, el origen de datos y el volumen, restricciones de rendimiento y otros factores.</span><span class="sxs-lookup"><span data-stu-id="69219-173">The approach taken in a production environment depends on the exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="69219-174">Los dos primeros ejemplos muestran cómo serializar y deserializar datos en búferes de secuencias de memoria usando reflexión y registros genéricos.</span><span class="sxs-lookup"><span data-stu-id="69219-174">The first two examples show how to serialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="69219-175">Se supone que el esquema en estos dos casos se va a compartir entre los lectores y escritores no conectados.</span><span class="sxs-lookup"><span data-stu-id="69219-175">The schema in these two cases is assumed to be shared between the readers and writers out-of-band.</span></span>

<span data-ttu-id="69219-176">Los ejemplos tercero y cuarto muestran cómo serializar y deserializar datos mediante los archivos contenedores de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-176">The third and fourth examples show how to serialize and deserialize data by using the Avro object container files.</span></span> <span data-ttu-id="69219-177">Cuando los datos se almacenan en un archivo contenedor de Avro, el esquema se almacena siempre con ellos porque debe compartirse para la deserialización.</span><span class="sxs-lookup"><span data-stu-id="69219-177">When data is stored in an Avro container file, its schema is always stored with it because the schema must be shared for deserialization.</span></span>

<span data-ttu-id="69219-178">La muestra que contiene los cuatro ejemplos primeros se puede descargar del sitio de <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">muestras de código de Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="69219-178">The sample containing the first four examples can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="69219-179">El quinto ejemplo muestra cómo usar un códec de compresión personalizado para archivos contenedores de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-179">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="69219-180">Puede descargar una muestra que contiene el código para este ejemplo desde el sitio de <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">muestras de código de Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="69219-180">A sample containing the code for this example can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="69219-181">El sexto ejemplo muestra cómo utilizar la serialización de Avro para cargar datos en Azure Blob Storage y después analizarlos mediante Hive con un clúster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="69219-181">The sixth sample shows how to use Avro serialization to upload data to Azure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="69219-182">Se puede descargar desde el sitio de <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">muestras de código de Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="69219-182">It can be downloaded from the <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="69219-183">Estos son los vínculos a los seis ejemplos tratados en el tema:</span><span class="sxs-lookup"><span data-stu-id="69219-183">Here are links to the six samples discussed in the topic:</span></span>

* <span data-ttu-id="69219-184"><a href="#Scenario1">**Serialización mediante reflexión**</a>: el esquema JSON para los tipos que se van a serializar se crea automáticamente a partir de los atributos del contrato de datos.</span><span class="sxs-lookup"><span data-stu-id="69219-184"><a href="#Scenario1">**Serialization with reflection**</a> - The JSON schema for types to be serialized is automatically built from the data contract attributes.</span></span>
* <span data-ttu-id="69219-185"><a href="#Scenario2">**Serialización mediante un registro genérico**</a>: el esquema JSON se especifica de forma explícita en un registro cuando no hay ningún tipo .NET disponible para reflexión.</span><span class="sxs-lookup"><span data-stu-id="69219-185"><a href="#Scenario2">**Serialization with generic record**</a> - The JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="69219-186"><a href="#Scenario3">**Serialización mediante archivos contenedores de objetos con reflexión**</a>: el esquema JSON se crea de manera automática y se comparte junto con los datos serializados mediante el uso de un archivo contenedor de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - The JSON schema is automatically built and shared together with the serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="69219-187"><a href="#Scenario4">**Serialización mediante archivos contenedores de objetos con un registro genérico**</a>: el esquema JSON se especifica explícitamente antes de la serialización y se comparte junto con los datos mediante el uso de un archivo contenedor de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - The JSON schema is explicitly specified before the serialization and shared together with the data via an Avro object container file.</span></span>
* <span data-ttu-id="69219-188"><a href="#Scenario5">**Serialización mediante archivos contenedores de objetos con un códec de compresión personalizado**</a>: este ejemplo muestra cómo crear un archivo contenedor de objetos de Avro con una implementación .NET personalizada del códec de compresión de datos Deflate.</span><span class="sxs-lookup"><span data-stu-id="69219-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - The example shows how to create an Avro object container file with a customized .NET implementation of the Deflate data compression codec.</span></span>
* <span data-ttu-id="69219-189"><a href="#Scenario6">**Uso de Avro para cargar datos para Microsoft Azure HDInsight**</a>: muestra cómo la serialización de Avro interactúa con el servicio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="69219-189"><a href="#Scenario6">**Using Avro to upload data for the Microsoft Azure HDInsight service**</a> - The example illustrates how Avro serialization interacts with the HDInsight service.</span></span> <span data-ttu-id="69219-190">Para ejecutar este ejemplo, se requiere una suscripción activa a Azure y acceso al clúster HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="69219-190">An active Azure subscription and access to an Azure HDInsight cluster are required to run this example.</span></span>

## <span data-ttu-id="69219-191"><a name="Scenario1"></a>Muestra 1: serialización mediante el uso de reflexión</span><span class="sxs-lookup"><span data-stu-id="69219-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="69219-192">El esquema JSON para los tipos se puede compilar automáticamente con Microsoft Avro Library usando reflexión a partir de los atributos del contrato de datos de los objetos de C# que se van a serializar.</span><span class="sxs-lookup"><span data-stu-id="69219-192">The JSON schema for the types can be automatically built by the Microsoft Avro Library via reflection from the data contract attributes of the C# objects to be serialized.</span></span> <span data-ttu-id="69219-193">Microsoft Avro Library crea un objeto [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) para identificar los campos que se van a serializar.</span><span class="sxs-lookup"><span data-stu-id="69219-193">The Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) to identify the fields to be serialized.</span></span>

<span data-ttu-id="69219-194">En este ejemplo, los objetos (una clase **SensorData** con un miembro struct **Location**) se serializan en una secuencia de memoria que, a su vez, se deserializa.</span><span class="sxs-lookup"><span data-stu-id="69219-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized to a memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="69219-195">Después, se compara el resultado con la instancia inicial para confirmar que el objeto **SensorData** recuperado es idéntico al original.</span><span class="sxs-lookup"><span data-stu-id="69219-195">The result is then compared to the initial instance to confirm that the **SensorData** object recovered is identical to the original.</span></span>

<span data-ttu-id="69219-196">En este ejemplo, se supone que el esquema está compartido entre los lectores y escritores, por lo que no es necesario el formato de contenedor de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-196">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="69219-197">Para ver un ejemplo de cómo serializar y deserializar datos en búferes de memoria usando reflexión con el formato de contenedor de objetos cuando debe compartirse el esquema con los datos, consulte <a href="#Scenario3">Serialización mediante el uso de archivos contenedores de objetos con reflexión</a>.</span><span class="sxs-lookup"><span data-stu-id="69219-197">For an example of how to serialize and deserialize data into memory buffers by using reflection with the object container format when the schema must be shared with the data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize the data to the specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from the stream and cast it to the same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches the original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization to memory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="69219-198">Ejemplo 2: Serialización con un registro genérico</span><span class="sxs-lookup"><span data-stu-id="69219-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="69219-199">Cuando no se puede usar reflexión porque los datos no se pueden representar mediante clases .NET con un contrato de datos, se puede especificar el esquema JSON de forma explícita en un registro genérico.</span><span class="sxs-lookup"><span data-stu-id="69219-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because the data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="69219-200">Este método es más lento que cuando se utiliza la reflexión.</span><span class="sxs-lookup"><span data-stu-id="69219-200">This method is slower than using reflection.</span></span> <span data-ttu-id="69219-201">En estos casos, el esquema de los datos puede ser dinámico, es decir, no se conoce hasta el momento de la compilación.</span><span class="sxs-lookup"><span data-stu-id="69219-201">In such cases, the schema for the data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="69219-202">Los datos representados como archivos de valores separados por comas (CSV) cuyo esquema se desconoce hasta que se transforman con el formato de Avro en tiempo de ejecución son un ejemplo de este tipo de escenario dinámico.</span><span class="sxs-lookup"><span data-stu-id="69219-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed to the Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="69219-203">En este ejemplo se muestra cómo crear y usar un objeto [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) para especificar un esquema JSON de forma explícita, cómo rellenarlo con los datos y cómo serializarlo y deserializarlo.</span><span class="sxs-lookup"><span data-stu-id="69219-203">This example shows how to create and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) to explicitly specify a JSON schema, how to populate it with the data, and then how to serialize and deserialize it.</span></span> <span data-ttu-id="69219-204">Después, se compara el resultado con la instancia inicial para confirmar que el registro recuperado es idéntico al original.</span><span class="sxs-lookup"><span data-stu-id="69219-204">The result is then compared to the initial instance to confirm that the record recovered is identical to the original.</span></span>

<span data-ttu-id="69219-205">En este ejemplo, se supone que el esquema está compartido entre los lectores y escritores, por lo que no es necesario el formato de contenedor de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-205">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="69219-206">Para ver un ejemplo de cómo serializar y deserializar datos en búferes de memoria usando un registro genérico con el formato de contenedor de objetos cuando debe incluirse el esquema con los datos serializados, consulte <a href="#Scenario4">Serialización mediante el uso de archivos contenedores de objetos con un registro genérico</a>.</span><span class="sxs-lookup"><span data-stu-id="69219-206">For an example of how to serialize and deserialize data into memory buffers by using a generic record with the object container format when the schema must be included with the serialized data, see the <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //the usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with the schema explicitly defined in JSON.
        //All serialized data should be mapped to the fields of the generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining the Schema and creating Sample Data Set...");

            //Define the schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on the schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record to represent the data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize the data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize the data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify the results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization to memory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key to exit.");
            Console.Read();
        }
    }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="69219-207">Ejemplo 3: Serialización mediante el uso de archivos contenedores de objetos y serialización con reflexión</span><span class="sxs-lookup"><span data-stu-id="69219-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="69219-208">Este ejemplo es similar al escenario del <a href="#Scenario1">primer ejemplo</a>, donde el esquema se especifica de forma implícita con reflexión.</span><span class="sxs-lookup"><span data-stu-id="69219-208">This example is similar to the scenario in the <a href="#Scenario1"> first example</a>, where the schema is implicitly specified with reflection.</span></span> <span data-ttu-id="69219-209">La diferencia es que aquí no se presupone su conocimiento por parte del lector que lo deserializa.</span><span class="sxs-lookup"><span data-stu-id="69219-209">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span> <span data-ttu-id="69219-210">Los objetos **SensorData** que se van a serializar y el esquema especificado de forma implícita se almacenan en un archivo contenedor de objetos representado por la clase [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="69219-210">The **SensorData** objects to be serialized and their implicitly specified schema are stored in an Avro object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="69219-211">En este ejemplo, los datos se serializan con [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) y se deserializan con [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="69219-211">The data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="69219-212">Después, se compara el resultado con las instancias iniciales para asegurarse de la identidad.</span><span class="sxs-lookup"><span data-stu-id="69219-212">The result then is compared to the initial instances to ensure identity.</span></span>

<span data-ttu-id="69219-213">Los datos del archivo contenedor de objetos se comprimen usando el códec de compresión predeterminado [**Deflate**][deflate-100] de .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="69219-213">The data in the object container file is compressed via the default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="69219-214">Consulte el <a href="#Scenario5">quinto ejemplo</a> de este tema para ver cómo se utiliza una versión más reciente y superior del códec de compresión [**Deflate**][deflate-110] disponible en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="69219-214">See the <a href="#Scenario5"> fifth example</a> in this topic to learn how to use a more recent and superior version of the [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes the sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is compressed using the Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="69219-215">Ejemplo 4: Serialización mediante el uso de archivos contenedores de objetos y serialización con registro genérico</span><span class="sxs-lookup"><span data-stu-id="69219-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="69219-216">Este ejemplo es similar al escenario del <a href="#Scenario2">segundo ejemplo</a>, donde el esquema se especifica de forma implícita con JSON.</span><span class="sxs-lookup"><span data-stu-id="69219-216">This example is similar to the scenario in the <a href="#Scenario2"> second example</a>, where the schema is explicitly specified with JSON.</span></span> <span data-ttu-id="69219-217">La diferencia es que aquí no se presupone su conocimiento por parte del lector que lo deserializa.</span><span class="sxs-lookup"><span data-stu-id="69219-217">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span>

<span data-ttu-id="69219-218">El conjunto de datos de prueba se recopila en una lista de objetos [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) usando un esquema JSON definido de forma explícita y se almacenan en un archivo contenedor de objetos representado por la clase [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="69219-218">The test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="69219-219">Este archivo contenedor crea un escritor que se usa para serializar los datos, descomprimidos, en una secuencia de memoria que se guarda después en un archivo.</span><span class="sxs-lookup"><span data-stu-id="69219-219">This container file creates a writer that is used to serialize the data, uncompressed, to a memory stream that is then saved to a file.</span></span> <span data-ttu-id="69219-220">El parámetro [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) que se usa para crear el lector especifica que estos datos no se comprimen.</span><span class="sxs-lookup"><span data-stu-id="69219-220">The [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating the reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="69219-221">Los datos se leen después en el archivo y se deserializan en una colección de objetos.</span><span class="sxs-lookup"><span data-stu-id="69219-221">The data is then read from the file and deserialized into a collection of objects.</span></span> <span data-ttu-id="69219-222">Esta colección se compara con la lista inicial de registros de Avro para confirmar que son idénticos.</span><span class="sxs-lookup"><span data-stu-id="69219-222">This collection is compared to the initial list of Avro records to confirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining the Schema and creating Sample Data Set...");

                //Define the schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on the schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record to represent the data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data to file.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data to file...");

                    //Save stream to file
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing the data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify the results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using the given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of the AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="69219-223">Ejemplo 5: Serialización mediante el uso de archivos contenedores de objetos con un códec de compresión personalizado</span><span class="sxs-lookup"><span data-stu-id="69219-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="69219-224">El quinto ejemplo muestra cómo usar un códec de compresión personalizado para archivos contenedores de objetos de Avro.</span><span class="sxs-lookup"><span data-stu-id="69219-224">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="69219-225">Puede descargar una muestra que contiene el código para este ejemplo desde el sitio de [muestras de código de Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) .</span><span class="sxs-lookup"><span data-stu-id="69219-225">A sample containing the code for this example can be downloaded from the [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="69219-226">La [especificación de Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permite el uso de un códec de compresión opcional (además de los predeterminados **Null** y **Deflate**).</span><span class="sxs-lookup"><span data-stu-id="69219-226">The [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition to **Null** and **Deflate** defaults).</span></span> <span data-ttu-id="69219-227">En este ejemplo, no se implementa el códec nuevo Snappy (mencionado como códec opcional admitido en la [especificación de Avro](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="69219-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in the [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="69219-228">Se muestra cómo usar la implementación de .NET Framework 4.5 del códec [**Deflate**][deflate-110], que proporciona un algoritmo de compresión basado en la biblioteca de compresión [zlib](http://zlib.net/) mejor que el predeterminado de la versión .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="69219-228">It shows how to use the .NET Framework 4.5 implementation of the [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on the [zlib](http://zlib.net/) compression library than the default .NET Framework 4 version.</span></span>

    //
    // This code needs to be compiled with the parameter Target Framework set as ".NET Framework 4.5"
    // to ensure the desired implementation of the Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are the key ones for data compression.
        //To enable a custom codec, one needs to implement these methods for the required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs to implement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed to be null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define the actual codec class containing the required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory to be used in the reader.
        //It catches the attempt to use "Deflate" and provide  a custom codec.
        //For all other cases, it relies on the base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related to serialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Here the custom codec is introduced. For convenience, the next commented code line shows how to use built-in Deflate.
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment the line below if you want to use built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    //Here the custom codec factory is introduced.
                    //For convenience, the next commented code line shows how to use built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete the file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using the given path to a memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection to Avro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.

## <a name="sample-6-using-avro-to-upload-data-for-the-microsoft-azure-hdinsight-service"></a><span data-ttu-id="69219-229">Ejemplo 6: Uso de Avro para cargar datos para el servicio Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="69219-229">Sample 6: Using Avro to upload data for the Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="69219-230">El sexto ejemplo muestra algunas técnicas de programación relacionadas para interactuar con el servicio HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="69219-230">The sixth example illustrates some programming techniques related to interacting with the Azure HDInsight service.</span></span> <span data-ttu-id="69219-231">Puede descargar una muestra que contiene el código para este ejemplo desde el sitio de [muestras de código de Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) .</span><span class="sxs-lookup"><span data-stu-id="69219-231">A sample containing the code for this example can be downloaded from the [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="69219-232">La muestra hace las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="69219-232">The sample does the following tasks:</span></span>

* <span data-ttu-id="69219-233">Se conecta a un clúster del servicio HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="69219-233">Connects to an existing HDInsight service cluster.</span></span>
* <span data-ttu-id="69219-234">Serializa varios archivos CSV y carga el resultado en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="69219-234">Serializes several CSV files and uploads the result to Azure Blob storage.</span></span> <span data-ttu-id="69219-235">(Los archivos CSV se distribuyen junto con la muestra y representan un extracto de los datos históricos del mercado de valores AMEX distribuidos por [Infochimps](http://www.infochimps.com/) para el período 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="69219-235">(The CSV files are distributed together with the sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for the period 1970-2010.</span></span> <span data-ttu-id="69219-236">La muestra lee los datos de los archivos CSV, convierte los registros en instancias de la clase **Stock** y, después, los serializa mediante el uso de la reflexión.</span><span class="sxs-lookup"><span data-stu-id="69219-236">The sample reads CSV file data, converts the records to instances of the **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="69219-237">La definición del tipo de valores se crea en un esquema JSON utilizando la utilidad de generación de código de Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="69219-237">Stock type definition is created from a JSON schema via the Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="69219-238">Crea una nueva tabla externa denominada **Stocks** en Hive y la vincula a los datos cargados en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="69219-238">Creates a new external table called **Stocks** in Hive, and links it to the data uploaded in the previous step.</span></span>
* <span data-ttu-id="69219-239">Ejecuta una consulta mediante Hive en la tabla **Stocks** .</span><span class="sxs-lookup"><span data-stu-id="69219-239">Executes a query by using Hive over the **Stocks** table.</span></span>

<span data-ttu-id="69219-240">Además, la muestra realiza un procedimiento de limpieza antes y después de realizar las principales operaciones.</span><span class="sxs-lookup"><span data-stu-id="69219-240">In addition, the sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="69219-241">Durante la limpieza, todos los datos y carpetas de blobs de Azure se quitan, y se elimina la tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="69219-241">During the clean-up, all of the related Azure Blob data and folders are removed, and the Hive table is dropped.</span></span> <span data-ttu-id="69219-242">También puede llamar al procedimiento de limpieza desde la línea de comandos de la muestra.</span><span class="sxs-lookup"><span data-stu-id="69219-242">You can also invoke the clean-up procedure from the sample command line.</span></span>

<span data-ttu-id="69219-243">La muestra cuenta con los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="69219-243">The sample has the following prerequisites:</span></span>

* <span data-ttu-id="69219-244">Una suscripción activa a Microsoft Azure y su identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="69219-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="69219-245">Un certificado de administración para la suscripción con la clave privada correspondiente.</span><span class="sxs-lookup"><span data-stu-id="69219-245">A management certificate for the subscription with the corresponding private key.</span></span> <span data-ttu-id="69219-246">El certificado debe estar instalado en el almacenamiento privado del usuario actual en el equipo utilizado para ejecutar la muestra.</span><span class="sxs-lookup"><span data-stu-id="69219-246">The certificate should be installed in the current user private storage on the machine used to run the sample.</span></span>
* <span data-ttu-id="69219-247">Un clúster de HDInsight activo.</span><span class="sxs-lookup"><span data-stu-id="69219-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="69219-248">Una cuenta de almacenamiento de Azure vinculada a un clúster de HDInsight desde el requisito previo anterior junto con la clave de acceso secundaria o primaria correspondiente.</span><span class="sxs-lookup"><span data-stu-id="69219-248">An Azure Storage account linked to the HDInsight cluster from the previous prerequisite, together with the corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="69219-249">Debe introducirse toda la información de los requisitos previos en el archivo de configuración de muestra antes de ejecutar la muestra.</span><span class="sxs-lookup"><span data-stu-id="69219-249">All of the information from the prerequisites should be entered to the sample configuration file before the sample is run.</span></span> <span data-ttu-id="69219-250">Existen dos formas posibles de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="69219-250">There are two possible ways to do it:</span></span>

* <span data-ttu-id="69219-251">Editar el archivo app.config en el directorio raíz de la muestra y después compilar la muestra.</span><span class="sxs-lookup"><span data-stu-id="69219-251">Edit the app.config file in the sample root directory and then build the sample</span></span>
* <span data-ttu-id="69219-252">Compilar primero la muestra y después editar AvroHDISample.exe.config en el directorio de compilación.</span><span class="sxs-lookup"><span data-stu-id="69219-252">First build the sample, and then edit AvroHDISample.exe.config in the build directory</span></span>

<span data-ttu-id="69219-253">En ambos casos, todas las modificaciones deben realizarse en la sección de configuración **<appSettings>**.</span><span class="sxs-lookup"><span data-stu-id="69219-253">In both cases, all edits should be done in the **<appSettings>** settings section.</span></span> <span data-ttu-id="69219-254">Siga los comentarios del archivo.</span><span class="sxs-lookup"><span data-stu-id="69219-254">Follow the comments in the file.</span></span>
<span data-ttu-id="69219-255">La muestra se ejecuta en la línea de comandos ejecutando el comando siguiente (donde se supone que el archivo .zip con la muestra se va a extraer en C:\AvroHDISample; en caso contrario, utilice la ruta de acceso al archivo pertinente):</span><span class="sxs-lookup"><span data-stu-id="69219-255">The sample is run from the command line by executing the following command (where the .zip file with the sample was assumed to be extracted to C:\AvroHDISample; if otherwise, use the relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="69219-256">Para limpiar el clúster, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="69219-256">To clean up the cluster, run the following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
