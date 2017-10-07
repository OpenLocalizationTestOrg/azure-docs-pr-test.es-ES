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
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="71a6c-103">Usar funciones definidas por el usuario de C# con el streaming de Hive y Pig en Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="71a6c-104">Obtenga información acerca de cómo toouse C# definido por el usuario (UDF) las funciones con Apache Hive y Pig en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71a6c-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71a6c-105">pasos de Hello en este documento funcionan con clústeres de HDInsight basados en Windows y basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="71a6c-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="71a6c-106">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="71a6c-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="71a6c-107">Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="71a6c-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="71a6c-108">Ambos Hive y Pig logra pasar las aplicaciones de tooexternal de datos para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="71a6c-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="71a6c-109">Este proceso se conoce como _streaming_.</span><span class="sxs-lookup"><span data-stu-id="71a6c-109">This process is known as _streaming_.</span></span> <span data-ttu-id="71a6c-110">Cuando se usa un dichos. NET, los datos de hello es pasar toohello aplicación STDIN y aplicación hello devuelve los resultados de hello en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="71a6c-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="71a6c-111">tooread y escritura desde STDIN y STDOUT, puede usar `Console.ReadLine()` y `Console.WriteLine()` desde una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71a6c-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="71a6c-112">Prerequisites</span></span>

* <span data-ttu-id="71a6c-113">Estar familiarizado con la escritura y la compilación del código C# orientado a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="71a6c-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="71a6c-114">Use el IDE que prefiera.</span><span class="sxs-lookup"><span data-stu-id="71a6c-114">Use whatever IDE you want.</span></span> <span data-ttu-id="71a6c-115">Recomendamos [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="71a6c-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="71a6c-116">Hola pasos de este documento, use Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="71a6c-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="71a6c-117">Una manera tooupload .exe archivos toohello clúster y ejecución de los trabajos de Pig y Hive.</span><span class="sxs-lookup"><span data-stu-id="71a6c-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="71a6c-118">Se recomiendan Hola Data Lake Tools para Visual Studio, PowerShell de Azure y Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="71a6c-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="71a6c-119">Hello pasos de este documento usar Hola Data Lake Tools archivos de Visual Studio tooupload hello y ejecutan la consulta de Hive de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="71a6c-120">Para obtener información sobre otras consultas de Hive de formas toorun y trabajos de Pig, consulte Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="71a6c-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="71a6c-121">Uso de Apache Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="71a6c-122">Uso de Apache Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="71a6c-123">Hadoop en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71a6c-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="71a6c-124">Para obtener más información sobre cómo crear un clúster, consulte [Creación de un clúster de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="71a6c-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="71a6c-125">.NET en HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-125">.NET on HDInsight</span></span>

* <span data-ttu-id="71a6c-126">__HDInsight basados en Linux__ clústeres mediante [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicaciones. NET.</span><span class="sxs-lookup"><span data-stu-id="71a6c-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="71a6c-127">La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71a6c-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="71a6c-128">Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="71a6c-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="71a6c-129">toouse una versión específica de Mono, vea hello [instalación o una actualización Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="71a6c-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="71a6c-130">__HDInsight basados en Windows__ clústeres usen las aplicaciones .NET de hello Microsoft .NET CLR toorun.</span><span class="sxs-lookup"><span data-stu-id="71a6c-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="71a6c-131">Para obtener más información sobre la versión de Hola de hello .NET framework y Mono incluida en versiones de HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="71a6c-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="71a6c-132">Crear hello C\# proyectos</span><span class="sxs-lookup"><span data-stu-id="71a6c-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="71a6c-133">UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="71a6c-133">Hive UDF</span></span>

1. <span data-ttu-id="71a6c-134">Abra Visual Studio y cree una solución.</span><span class="sxs-lookup"><span data-stu-id="71a6c-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="71a6c-135">Para el tipo de proyecto de hello, seleccione **aplicación de consola (.NET Framework)**y nombre hello nuevo proyecto **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="71a6c-136">Seleccione __.NET Framework 4.5__ si está usando un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="71a6c-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="71a6c-137">Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="71a6c-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="71a6c-138">Reemplace el contenido de Hola de **Program.cs** con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="71a6c-138">Replace hello contents of **Program.cs** with hello following:</span></span>

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

3. <span data-ttu-id="71a6c-139">Compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="71a6c-140">UDF de Pig</span><span class="sxs-lookup"><span data-stu-id="71a6c-140">Pig UDF</span></span>

1. <span data-ttu-id="71a6c-141">Abra Visual Studio y cree una solución.</span><span class="sxs-lookup"><span data-stu-id="71a6c-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="71a6c-142">Para el tipo de proyecto de hello, seleccione **aplicación de consola**y nombre hello nuevo proyecto **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="71a6c-143">Reemplazar contenido Hola de hello **Program.cs** archivo con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="71a6c-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

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

    <span data-ttu-id="71a6c-144">Esta aplicación analiza las líneas de hello enviadas desde Pig y volver a formatear líneas que comienzan por `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="71a6c-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="71a6c-145">Guardar **Program.cs**y, a continuación, compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="71a6c-146">Cargar toostorage</span><span class="sxs-lookup"><span data-stu-id="71a6c-146">Upload toostorage</span></span>

1. <span data-ttu-id="71a6c-147">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="71a6c-148">Expanda **Azure** y, después, haga lo mismo con **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="71a6c-149">Si se le solicitan, escriba sus credenciales de suscripción de Azure y, a continuación, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="71a6c-150">Expanda el clúster de HDInsight de Hola que desee toodeploy para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="71a6c-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="71a6c-151">Una entrada con el texto hello __(cuenta de almacenamiento predeterminada)__ aparece.</span><span class="sxs-lookup"><span data-stu-id="71a6c-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Explorador de servidores mostrando la cuenta de almacenamiento de hello para el clúster de Hola](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="71a6c-153">Si se puede expandir esta entrada, que usa un __cuenta de almacenamiento de Azure__ como almacenamiento predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="71a6c-154">archivos de Hola de tooview en almacenamiento predeterminado de Hola para clúster hello, expanda la entrada de hello y, a continuación, haga doble clic en hello __(contenedor predeterminado)__.</span><span class="sxs-lookup"><span data-stu-id="71a6c-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="71a6c-155">Si no se puede expandir esta entrada, que usa __almacén de Azure Data Lake__ como almacenamiento predeterminado de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="71a6c-156">archivos de hello tooview en almacenamiento predeterminado de hello para el clúster de hello, haga doble clic en hello __(cuenta de almacenamiento predeterminada)__ entrada.</span><span class="sxs-lookup"><span data-stu-id="71a6c-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="71a6c-157">archivos .exe de tooupload hello, use uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="71a6c-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="71a6c-158">Si usa un __cuenta de almacenamiento de Azure__, haga clic en el icono de carga de hello y, a continuación, examinar toohello **bin\debug** carpeta para hello **HiveCSharp** proyecto.</span><span class="sxs-lookup"><span data-stu-id="71a6c-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="71a6c-159">Por último, seleccione hello **HiveCSharp.exe** de archivo y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![icono para cargar](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="71a6c-161">Si usa __almacén de Azure Data Lake__, haga clic en un área vacía en lista de archivos de hello y, a continuación, seleccione __cargar__.</span><span class="sxs-lookup"><span data-stu-id="71a6c-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="71a6c-162">Por último, seleccione hello **HiveCSharp.exe** de archivo y haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="71a6c-163">Una vez Hola __HiveCSharp.exe__ carga haya finalizado, el proceso de carga de repetición Hola para hello __PigUDF.exe__ archivo.</span><span class="sxs-lookup"><span data-stu-id="71a6c-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="71a6c-164">Ejecución de una consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="71a6c-164">Run a Hive query</span></span>

1. <span data-ttu-id="71a6c-165">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="71a6c-166">Expanda **Azure** y, después, haga lo mismo con **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="71a6c-167">Clúster de hello contextual implementados hello **HiveCSharp** aplicación y, a continuación, seleccione **escribir una consulta de Hive**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="71a6c-168">Usar hello siguiendo el texto de consulta de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="71a6c-168">Use hello following text for hello Hive query:</span></span>

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
    > <span data-ttu-id="71a6c-169">Quite el comentario de hello `add file` instrucción que coincide con el tipo de saludo de almacenamiento predeterminado utilizado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="71a6c-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="71a6c-170">Esta consulta selecciona hello `clientid`, `devicemake`, y `devicemodel` campos de `hivesampletable`y pasa a campos de hello toohello HiveCSharp.exe aplicación.</span><span class="sxs-lookup"><span data-stu-id="71a6c-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="71a6c-171">espera de consulta de Hola Hola tooreturn tres campos de aplicación, que se almacenan como `clientid`, `phoneLabel`, y `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="71a6c-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="71a6c-172">consulta de Hello también espera toofind HiveCSharp.exe en la raíz de Hola Hola predeterminado del contenedor de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="71a6c-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="71a6c-173">Haga clic en **enviar** clúster de HDInsight de toosubmit Hola trabajo toohello.</span><span class="sxs-lookup"><span data-stu-id="71a6c-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="71a6c-174">Hola **resumen del trabajo de Hive** abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="71a6c-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="71a6c-175">Haga clic en **actualizar** toorefresh Hola resumen hasta **estado del trabajo** cambia demasiado**completado**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="71a6c-176">trabajo de hello tooview de salida, haga clic en **salida del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="71a6c-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="71a6c-177">Ejecución de un trabajo de Pig</span><span class="sxs-lookup"><span data-stu-id="71a6c-177">Run a Pig job</span></span>

1. <span data-ttu-id="71a6c-178">Use uno de hello después de clúster de HDInsight de tooyour tooconnect de métodos:</span><span class="sxs-lookup"><span data-stu-id="71a6c-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="71a6c-179">Si está usando un clúster de HDInsight __basado en Linux__, use SSH.</span><span class="sxs-lookup"><span data-stu-id="71a6c-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="71a6c-180">Por ejemplo: `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="71a6c-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="71a6c-181">Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="71a6c-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="71a6c-182">Si usas un __basados en Windows__ clúster de HDInsight, [conectar toohello clúster mediante Escritorio remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="71a6c-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="71a6c-183">Usar una hello después de la línea de comandos de comando toostart Hola Pig:</span><span class="sxs-lookup"><span data-stu-id="71a6c-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="71a6c-184">Si está usando un clúster basado en Windows, utilice Hola siguientes comandos en su lugar:</span><span class="sxs-lookup"><span data-stu-id="71a6c-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="71a6c-185">Se muestra un símbolo del sistema `grunt>`.</span><span class="sxs-lookup"><span data-stu-id="71a6c-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="71a6c-186">Escriba Hola después de un trabajo de Pig que usa la aplicación de .NET Framework de hello toorun:</span><span class="sxs-lookup"><span data-stu-id="71a6c-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="71a6c-187">Hola `DEFINE` instrucción crea un alias de `streamer` para las aplicaciones de hello pigudf.exe, y `CACHE` carga de almacenamiento predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="71a6c-188">Más adelante, `streamer` se utiliza con hello `STREAM` operador tooprocess Hola líneas individuales contenidas en el registro y datos de hello devuelto como una serie de columnas.</span><span class="sxs-lookup"><span data-stu-id="71a6c-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="71a6c-189">nombre de la aplicación Hello que se usa para la transmisión por secuencias debe estar rodeada de hello \` (acento grave) de caracteres cuando tiene un alias, y ' (comilla sencilla) cuando se utiliza con `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="71a6c-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="71a6c-190">Después de escribir la última línea de hello, debe iniciar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="71a6c-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="71a6c-191">Devuelve toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="71a6c-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="71a6c-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71a6c-192">Next steps</span></span>

<span data-ttu-id="71a6c-193">En este documento, ha aprendido cómo toouse una aplicación de .NET Framework de Hive y Pig en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71a6c-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="71a6c-194">Si desea que toolearn toouse Python con Hive y Pig, vea [uso de Python con Hive y Pig en HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="71a6c-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="71a6c-195">Para otras formas toouse Pig y Hive y toolearn sobre el uso de MapReduce, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="71a6c-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="71a6c-196">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="71a6c-197">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="71a6c-198">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="71a6c-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
