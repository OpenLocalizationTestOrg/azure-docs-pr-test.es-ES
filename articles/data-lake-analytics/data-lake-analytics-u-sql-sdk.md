---
title: "Escalado de prueba y depuración local de U-SQL con el SDK de U-SQL para Azure Data Lake | Microsoft Docs"
description: "Obtenga información acerca de cómo usar el SDK de U-SQL para Azure Data Lake para escalar pruebas y depuraciones locales de trabajos de U-SQL con línea de comandos e interfaces de programación en la estación de trabajo local."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="50861-103">Escalado de prueba y depuración local de U-SQL con el SDK de U-SQL para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="50861-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="50861-104">Al desarrollar el script U-SQL, es frecuente ejecutarlo y probarlo localmente antes de enviarlo a la nube.</span><span class="sxs-lookup"><span data-stu-id="50861-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="50861-105">Azure Data Lake proporciona un paquete Nuget denominado SDK de U-SQL para Azure Data Lake para esta situación, por lo que le resultará muy fácil realizar el escalado de prueba y ejecución local de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="50861-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="50861-106">También es posible integrar esta prueba de U-SQL con el sistema de CI (integración continua) para automatizar la compilación y la prueba.</span><span class="sxs-lookup"><span data-stu-id="50861-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="50861-107">Si está interesado en cómo ejecutar y depurar localmente y de forma manual el script U-SQL con las herramientas GUI, entonces puede usar las Herramientas de Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50861-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="50861-108">Puede obtener más información sobre esto [aquí](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="50861-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="50861-109">Instalación del SDK de U-SQL para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="50861-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="50861-110">Puede obtener el SDK de U-SQL para Azure Data Lake [aquí](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) en Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="50861-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="50861-111">Y, antes de usarlo, debe asegurarse de que dispone de las siguientes dependencias.</span><span class="sxs-lookup"><span data-stu-id="50861-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="50861-112">Dependencias</span><span class="sxs-lookup"><span data-stu-id="50861-112">Dependencies</span></span>

<span data-ttu-id="50861-113">El SDK de U-SQL para Data Lake requiere las siguientes dependencias:</span><span class="sxs-lookup"><span data-stu-id="50861-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="50861-114">[Microsoft .NET Framework 4.6 o superior](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="50861-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="50861-115">Microsoft Visual C++ 14 y el SDK de Windows 10.0.10240.0 o posterior (que se denomina CppSDK en este artículo).</span><span class="sxs-lookup"><span data-stu-id="50861-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="50861-116">Existen dos formas de obtener CppSDK:</span><span class="sxs-lookup"><span data-stu-id="50861-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="50861-117">Instale [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="50861-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="50861-118">Debe tener una carpeta \Windows Kits\10 en la carpeta de archivos de programa, por ejemplo, C:\Program Files (x86)\Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="50861-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="50861-119">También encontrará la versión del SDK de Windows 10 en \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="50861-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="50861-120">Si no ve estas carpetas, vuelva a instalar Visual Studio y asegúrese de seleccionar el SDK de Windows 10 durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="50861-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="50861-121">Si ya lo tiene instalado con Visual Studio, el compilador local de U-SQL lo encontrará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="50861-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![SDK de Windows 10 para ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="50861-123">Instale [Data Lake Tools para Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="50861-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="50861-124">Puede encontrar los archivos preconfigurados del SDK de Windows y Visual C++ en C:\Archivos de programa (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="50861-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="50861-125">En este caso, el script del compilador local de U-SQL no podrá encontrar estas dependencias automáticamente.</span><span class="sxs-lookup"><span data-stu-id="50861-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="50861-126">Debe especificar la ruta de acceso de CppSDK para él.</span><span class="sxs-lookup"><span data-stu-id="50861-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="50861-127">Puede copiar los archivos en otra ubicación o simplemente usarla como está.</span><span class="sxs-lookup"><span data-stu-id="50861-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="50861-128">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="50861-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="50861-129">Raíz de datos</span><span class="sxs-lookup"><span data-stu-id="50861-129">Data root</span></span>

<span data-ttu-id="50861-130">La carpeta raíz de datos es un "almacén local" de la cuenta de proceso local.</span><span class="sxs-lookup"><span data-stu-id="50861-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="50861-131">Es equivalente a la cuenta de Azure Data Lake Store de una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="50861-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="50861-132">Cambiar a una carpeta raíz de datos diferente es como que cambiar a otra cuenta de almacén.</span><span class="sxs-lookup"><span data-stu-id="50861-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="50861-133">Si desea tener acceso a datos compartidos normalmente con carpetas raíz de datos diferentes, debe usar rutas de acceso absolutas en los scripts.</span><span class="sxs-lookup"><span data-stu-id="50861-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="50861-134">O bien, cree vínculos simbólicos del sistema de archivos (por ejemplo, **mklink** en NTFS) en la carpeta raíz de datos para que apunte a los datos compartidos.</span><span class="sxs-lookup"><span data-stu-id="50861-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="50861-135">La carpeta raíz de datos se utiliza para:</span><span class="sxs-lookup"><span data-stu-id="50861-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="50861-136">Almacenar metadatos, lo que incluye bases de datos, tablas, funciones con valores de tabla (TVF) y ensamblados.</span><span class="sxs-lookup"><span data-stu-id="50861-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="50861-137">Buscar las rutas de acceso de entrada y salida que se definen como rutas de acceso relativas en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="50861-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="50861-138">El uso de rutas de acceso relativas facilita la implementación de sus proyectos U-SQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="50861-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="50861-139">Ruta de archivo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="50861-139">File path in U-SQL</span></span>

<span data-ttu-id="50861-140">Puede usar tanto una ruta de acceso relativa como una ruta de acceso absoluta local en los scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="50861-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="50861-141">La ruta de acceso relativa es relativa a la ruta de acceso de la carpeta raíz de datos especificada.</span><span class="sxs-lookup"><span data-stu-id="50861-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="50861-142">Se recomienda usar "/" como separador de ruta de acceso para que los scripts sean compatibles con el lado servidor.</span><span class="sxs-lookup"><span data-stu-id="50861-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="50861-143">Estos son algunos ejemplos de rutas de acceso relativas y sus rutas de acceso absolutas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="50861-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="50861-144">En estos ejemplos, C:\LocalRunDataRoot es la carpeta raíz de datos.</span><span class="sxs-lookup"><span data-stu-id="50861-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="50861-145">Ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="50861-145">Relative path</span></span>|<span data-ttu-id="50861-146">Ruta de acceso absoluta</span><span class="sxs-lookup"><span data-stu-id="50861-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="50861-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="50861-147">/abc/def/input.csv</span></span> |<span data-ttu-id="50861-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="50861-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="50861-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="50861-149">abc/def/input.csv</span></span>  |<span data-ttu-id="50861-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="50861-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="50861-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="50861-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="50861-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="50861-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="50861-153">Directorio de trabajo</span><span class="sxs-lookup"><span data-stu-id="50861-153">Working directory</span></span>

<span data-ttu-id="50861-154">Al ejecutar localmente el script U-SQL, se crea un directorio de trabajo durante la compilación en el directorio que se está ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="50861-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="50861-155">Además de las salidas de compilación, se creará una instantánea de los archivos del runtime necesarios para la ejecución local en este directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="50861-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="50861-156">La carpeta de raíz del directorio de trabajo se denomina "ScopeWorkDir" y los archivos dentro el directorio de trabajo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="50861-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="50861-157">Directorio o archivo</span><span class="sxs-lookup"><span data-stu-id="50861-157">Directory/file</span></span>|<span data-ttu-id="50861-158">Directorio o archivo</span><span class="sxs-lookup"><span data-stu-id="50861-158">Directory/file</span></span>|<span data-ttu-id="50861-159">Directorio o archivo</span><span class="sxs-lookup"><span data-stu-id="50861-159">Directory/file</span></span>|<span data-ttu-id="50861-160">Definición</span><span class="sxs-lookup"><span data-stu-id="50861-160">Definition</span></span>|<span data-ttu-id="50861-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="50861-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="50861-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="50861-163">Cadena de hash de la versión del runtime</span><span class="sxs-lookup"><span data-stu-id="50861-163">Hash string of runtime version</span></span>|<span data-ttu-id="50861-164">Instantánea de los archivos del runtime necesarios para la ejecución local</span><span class="sxs-lookup"><span data-stu-id="50861-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="50861-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="50861-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="50861-166">Nombre de script + cadena de hash de la ruta de acceso del script</span><span class="sxs-lookup"><span data-stu-id="50861-166">Script name + hash string of script path</span></span>|<span data-ttu-id="50861-167">Resultados de compilación y registro de los pasos de ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="50861-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="50861-168">\_script\_.abr</span></span>|<span data-ttu-id="50861-169">Salida del compilador</span><span class="sxs-lookup"><span data-stu-id="50861-169">Compiler output</span></span>|<span data-ttu-id="50861-170">Archivo de álgebra</span><span class="sxs-lookup"><span data-stu-id="50861-170">Algebra file</span></span>|
| | |<span data-ttu-id="50861-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="50861-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="50861-172">Salida del compilador</span><span class="sxs-lookup"><span data-stu-id="50861-172">Compiler output</span></span>|<span data-ttu-id="50861-173">Código administrado generado</span><span class="sxs-lookup"><span data-stu-id="50861-173">Generated managed code</span></span>|
| | |<span data-ttu-id="50861-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="50861-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="50861-175">Salida del compilador</span><span class="sxs-lookup"><span data-stu-id="50861-175">Compiler output</span></span>|<span data-ttu-id="50861-176">Código nativo generado</span><span class="sxs-lookup"><span data-stu-id="50861-176">Generated native code</span></span>|
| | |<span data-ttu-id="50861-177">ensamblados de referencia</span><span class="sxs-lookup"><span data-stu-id="50861-177">referenced assemblies</span></span>|<span data-ttu-id="50861-178">Referencia de ensamblado</span><span class="sxs-lookup"><span data-stu-id="50861-178">Assembly reference</span></span>|<span data-ttu-id="50861-179">Archivos de ensamblados de referencia</span><span class="sxs-lookup"><span data-stu-id="50861-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="50861-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="50861-180">deployed_resources</span></span>|<span data-ttu-id="50861-181">Implementación de recursos</span><span class="sxs-lookup"><span data-stu-id="50861-181">Resource deployment</span></span>|<span data-ttu-id="50861-182">Archivos de implementación de recursos</span><span class="sxs-lookup"><span data-stu-id="50861-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="50861-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="50861-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="50861-184">Registro de ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-184">Execution log</span></span>|<span data-ttu-id="50861-185">Registro de pasos de ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="50861-186">Uso del SDK desde la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="50861-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="50861-187">Interfaz de la línea de comandos de la aplicación auxiliar</span><span class="sxs-lookup"><span data-stu-id="50861-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="50861-188">El archivo LocalRunHelper.exe se encuentra en el directorio del SDK, en build/runtime, y es la aplicación auxiliar de línea de comandos que proporciona interfaces a la mayoría de las funciones de ejecución local de uso frecuente.</span><span class="sxs-lookup"><span data-stu-id="50861-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="50861-189">Tenga en cuenta que tanto el comando como los modificadores de argumentos distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="50861-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="50861-190">Para invocarla:</span><span class="sxs-lookup"><span data-stu-id="50861-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="50861-191">Ejecute LocalRunHelper.exe sin argumentos o con el modificador **help** para mostrar la información de ayuda:</span><span class="sxs-lookup"><span data-stu-id="50861-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="50861-192">En la información de ayuda:</span><span class="sxs-lookup"><span data-stu-id="50861-192">In the help information:</span></span>

-  <span data-ttu-id="50861-193">**Command** proporciona el nombre del comando.</span><span class="sxs-lookup"><span data-stu-id="50861-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="50861-194">**Required Argument** enumera los argumentos que se deben proporcionar.</span><span class="sxs-lookup"><span data-stu-id="50861-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="50861-195">**Optional Argument** enumera argumentos que son opcionales, con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="50861-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="50861-196">Los argumentos opcionales booleanos no tienen parámetros y sus repeticiones implican un valor negativo de sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="50861-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="50861-197">Valor devuelto y registro</span><span class="sxs-lookup"><span data-stu-id="50861-197">Return value and logging</span></span>

<span data-ttu-id="50861-198">La aplicación auxiliar devuelve **0** si se ha realizado correctamente y **-1** en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="50861-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="50861-199">De forma predeterminada, la aplicación auxiliar envía todos los mensajes a la consola actual.</span><span class="sxs-lookup"><span data-stu-id="50861-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="50861-200">Sin embargo, la mayoría de los comandos admiten el argumento opcional **-MessageOut ruta_de_acceso_al_archivo_de_registro** que redirige las salidas a un archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="50861-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="50861-201">Configuración de la variable de entorno</span><span class="sxs-lookup"><span data-stu-id="50861-201">Environment variable configuring</span></span>

<span data-ttu-id="50861-202">La ejecución local de U-SQL requiere una raíz de datos explícita como cuenta de almacenamiento local, así como una ruta de acceso de CppSDK explícita para las dependencias.</span><span class="sxs-lookup"><span data-stu-id="50861-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="50861-203">Puede establecer el argumento en la línea de comandos o bien puede establecer la variable de entorno para ellos.</span><span class="sxs-lookup"><span data-stu-id="50861-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="50861-204">Establezca la variable de entorno **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="50861-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="50861-205">Si obtiene Microsoft Visual C++ y Windows SDK con la instalación de Data Lake Tools para Visual Studio, compruebe que dispone de la siguiente carpeta:</span><span class="sxs-lookup"><span data-stu-id="50861-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="50861-206">Defina una nueva variable de entorno denominada **SCOPE_CPP_SDK** para que apunte a este directorio.</span><span class="sxs-lookup"><span data-stu-id="50861-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="50861-207">O copie la carpeta en otra ubicación y especifique **SCOPE_CPP_SDK** como eso.</span><span class="sxs-lookup"><span data-stu-id="50861-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="50861-208">Además de establecer la variable de entorno, también puede especificar el argumento **-CppSDK** cuando se utiliza la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="50861-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="50861-209">Este argumento sobrescribe la variable de entorno CppSDK predeterminada.</span><span class="sxs-lookup"><span data-stu-id="50861-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="50861-210">Establezca la variable de entorno **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="50861-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="50861-211">Defina una nueva variable de entorno denominada **LOCALRUN_DATAROOT** que apunte a la raíz de datos.</span><span class="sxs-lookup"><span data-stu-id="50861-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="50861-212">Además de establecer la variable de entorno, puede especificar el argumento **-DataRoot** con la ruta de acceso raíz de datos cuando se utiliza la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="50861-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="50861-213">Este argumento sobrescribe la variable de entorno raíz de datos predeterminada.</span><span class="sxs-lookup"><span data-stu-id="50861-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="50861-214">Necesita agregar este argumento a cada línea de comandos que esté ejecutando para que pueda sobrescribir la variable de entorno raíz de datos predeterminada para todas las operaciones.</span><span class="sxs-lookup"><span data-stu-id="50861-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="50861-215">Ejemplos de uso de línea de comandos del SDK</span><span class="sxs-lookup"><span data-stu-id="50861-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="50861-216">Compilación y ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-216">Compile and run</span></span>

<span data-ttu-id="50861-217">El comando **run** se utiliza para compilar el script y ejecutar después los resultados compilados.</span><span class="sxs-lookup"><span data-stu-id="50861-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="50861-218">Sus argumentos de línea de comandos son una combinación de los de **compile** y **execute**.</span><span class="sxs-lookup"><span data-stu-id="50861-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="50861-219">A continuación se muestran los argumentos opcionales para **run**:</span><span class="sxs-lookup"><span data-stu-id="50861-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="50861-220">Argumento</span><span class="sxs-lookup"><span data-stu-id="50861-220">Argument</span></span>|<span data-ttu-id="50861-221">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="50861-221">Default value</span></span>|<span data-ttu-id="50861-222">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="50861-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="50861-223">-CodeBehind</span></span>|<span data-ttu-id="50861-224">False</span><span class="sxs-lookup"><span data-stu-id="50861-224">False</span></span>|<span data-ttu-id="50861-225">El script tiene código subyacente .cs</span><span class="sxs-lookup"><span data-stu-id="50861-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="50861-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="50861-226">-CppSDK</span></span>| |<span data-ttu-id="50861-227">Directorio CppSDK</span><span class="sxs-lookup"><span data-stu-id="50861-227">CppSDK Directory</span></span>|
|<span data-ttu-id="50861-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="50861-228">-DataRoot</span></span>| <span data-ttu-id="50861-229">Variable de entorno de DataRoot</span><span class="sxs-lookup"><span data-stu-id="50861-229">DataRoot environment variable</span></span>|<span data-ttu-id="50861-230">DataRoot para ejecución local; el valor predeterminado es la variable de entorno 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="50861-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="50861-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="50861-231">-MessageOut</span></span>| |<span data-ttu-id="50861-232">Volcar mensajes de la consola en un archivo</span><span class="sxs-lookup"><span data-stu-id="50861-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="50861-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="50861-233">-Parallel</span></span>|<span data-ttu-id="50861-234">1</span><span class="sxs-lookup"><span data-stu-id="50861-234">1</span></span>|<span data-ttu-id="50861-235">Ejecutar el plan con el paralelismo especificado</span><span class="sxs-lookup"><span data-stu-id="50861-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="50861-236">-References</span><span class="sxs-lookup"><span data-stu-id="50861-236">-References</span></span>| |<span data-ttu-id="50861-237">Lista de rutas de acceso a los ensamblados de referencia adicionales o archivos de datos de código subyacente, separadas por ';'</span><span class="sxs-lookup"><span data-stu-id="50861-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="50861-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="50861-238">-UdoRedirect</span></span>|<span data-ttu-id="50861-239">False</span><span class="sxs-lookup"><span data-stu-id="50861-239">False</span></span>|<span data-ttu-id="50861-240">Generar la configuración de redirección de ensamblado de Udo</span><span class="sxs-lookup"><span data-stu-id="50861-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="50861-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="50861-241">-UseDatabase</span></span>|<span data-ttu-id="50861-242">principal</span><span class="sxs-lookup"><span data-stu-id="50861-242">master</span></span>|<span data-ttu-id="50861-243">Base de datos que se utilizará para el registro de ensamblados temporal de código subyacente</span><span class="sxs-lookup"><span data-stu-id="50861-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="50861-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="50861-244">-Verbose</span></span>|<span data-ttu-id="50861-245">False</span><span class="sxs-lookup"><span data-stu-id="50861-245">False</span></span>|<span data-ttu-id="50861-246">Mostrar resultados detallados del runtime</span><span class="sxs-lookup"><span data-stu-id="50861-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="50861-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="50861-247">-WorkDir</span></span>|<span data-ttu-id="50861-248">Directorio actual</span><span class="sxs-lookup"><span data-stu-id="50861-248">Current Directory</span></span>|<span data-ttu-id="50861-249">Directorio para las salidas y el uso del compilador</span><span class="sxs-lookup"><span data-stu-id="50861-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="50861-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="50861-250">-RunScopeCEP</span></span>|<span data-ttu-id="50861-251">0</span><span class="sxs-lookup"><span data-stu-id="50861-251">0</span></span>|<span data-ttu-id="50861-252">Modo de ScopeCEP que se utilizará</span><span class="sxs-lookup"><span data-stu-id="50861-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="50861-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="50861-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="50861-254">temp</span><span class="sxs-lookup"><span data-stu-id="50861-254">temp</span></span>|<span data-ttu-id="50861-255">Ruta de acceso temporal que se usará para el streaming de datos</span><span class="sxs-lookup"><span data-stu-id="50861-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="50861-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="50861-256">-OptFlags</span></span>| |<span data-ttu-id="50861-257">Lista de marcas de optimizador separadas por comas</span><span class="sxs-lookup"><span data-stu-id="50861-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="50861-258">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="50861-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="50861-259">Además de combinar **compile** y **execute**, puede compilar y ejecutar los ejecutables compilados por separado.</span><span class="sxs-lookup"><span data-stu-id="50861-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="50861-260">Compilación de un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="50861-260">Compile a U-SQL script</span></span>

<span data-ttu-id="50861-261">El comando **compile** se utiliza para compilar un script U-SQL en los archivos ejecutables.</span><span class="sxs-lookup"><span data-stu-id="50861-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="50861-262">A continuación, se muestran los argumentos opcionales para **compile**:</span><span class="sxs-lookup"><span data-stu-id="50861-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="50861-263">Argumento</span><span class="sxs-lookup"><span data-stu-id="50861-263">Argument</span></span>|<span data-ttu-id="50861-264">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="50861-265">-CodeBehind [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="50861-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="50861-266">El script tiene código subyacente .cs</span><span class="sxs-lookup"><span data-stu-id="50861-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="50861-267">-CppSDK [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="50861-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="50861-268">Directorio CppSDK</span><span class="sxs-lookup"><span data-stu-id="50861-268">CppSDK Directory</span></span>|
| <span data-ttu-id="50861-269">-DataRoot [valor predeterminado 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="50861-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="50861-270">DataRoot para ejecución local; el valor predeterminado es la variable de entorno 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="50861-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="50861-271">-MessageOut [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="50861-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="50861-272">Volcar mensajes de la consola en un archivo</span><span class="sxs-lookup"><span data-stu-id="50861-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="50861-273">-References [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="50861-273">-References [default value '']</span></span>|<span data-ttu-id="50861-274">Lista de rutas de acceso a los ensamblados de referencia adicionales o archivos de datos de código subyacente, separadas por ';'</span><span class="sxs-lookup"><span data-stu-id="50861-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="50861-275">-Shallow [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="50861-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="50861-276">Compilación superficial</span><span class="sxs-lookup"><span data-stu-id="50861-276">Shallow compile</span></span>|
| <span data-ttu-id="50861-277">-UdoRedirect [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="50861-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="50861-278">Generar la configuración de redirección de ensamblado de Udo</span><span class="sxs-lookup"><span data-stu-id="50861-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="50861-279">-UseDatabase [valor predeterminado 'master']</span><span class="sxs-lookup"><span data-stu-id="50861-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="50861-280">Base de datos que se utilizará para el registro de ensamblados temporal de código subyacente</span><span class="sxs-lookup"><span data-stu-id="50861-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="50861-281">-WorkDir [valor predeterminado 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="50861-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="50861-282">Directorio para las salidas y el uso del compilador</span><span class="sxs-lookup"><span data-stu-id="50861-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="50861-283">-RunScopeCEP [valor predeterminado '0']</span><span class="sxs-lookup"><span data-stu-id="50861-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="50861-284">Modo de ScopeCEP que se utilizará</span><span class="sxs-lookup"><span data-stu-id="50861-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="50861-285">-ScopeCEPTempPath [valor predeterminado 'temp']</span><span class="sxs-lookup"><span data-stu-id="50861-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="50861-286">Ruta de acceso temporal que se usará para el streaming de datos</span><span class="sxs-lookup"><span data-stu-id="50861-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="50861-287">-OptFlags [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="50861-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="50861-288">Lista de marcas de optimizador separadas por comas</span><span class="sxs-lookup"><span data-stu-id="50861-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="50861-289">Estos son algunos ejemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="50861-289">Here are some usage examples.</span></span>

<span data-ttu-id="50861-290">Compile un script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="50861-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="50861-291">Compile un script U-SQL y establezca la carpeta raíz de datos.</span><span class="sxs-lookup"><span data-stu-id="50861-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="50861-292">Tenga en cuenta que esta acción sobrescribirá la variable de entorno del conjunto.</span><span class="sxs-lookup"><span data-stu-id="50861-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="50861-293">Compile un script U-SQL y establezca el directorio de trabajo, el ensamblado de referencia y la base de datos:</span><span class="sxs-lookup"><span data-stu-id="50861-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="50861-294">Ejecución de resultados compilados</span><span class="sxs-lookup"><span data-stu-id="50861-294">Execute compiled results</span></span>

<span data-ttu-id="50861-295">El comando **execute** se usa para ejecutar resultados compilados.</span><span class="sxs-lookup"><span data-stu-id="50861-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="50861-296">A continuación, se muestran los argumentos opcionales para **execute**:</span><span class="sxs-lookup"><span data-stu-id="50861-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="50861-297">Argumento</span><span class="sxs-lookup"><span data-stu-id="50861-297">Argument</span></span>|<span data-ttu-id="50861-298">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="50861-299">-DataRoot [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="50861-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="50861-300">Raíz de datos para la ejecución de metadatos.</span><span class="sxs-lookup"><span data-stu-id="50861-300">Data root for metadata execution.</span></span> <span data-ttu-id="50861-301">De manera predeterminada, es la variable de entorno **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="50861-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="50861-302">-MessageOut [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="50861-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="50861-303">Volcar mensajes de la consola en un archivo.</span><span class="sxs-lookup"><span data-stu-id="50861-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="50861-304">-Parallel [valor predeterminado '1']</span><span class="sxs-lookup"><span data-stu-id="50861-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="50861-305">Indicador para ejecutar los pasos de ejecución local generados con el nivel de paralelismo especificado.</span><span class="sxs-lookup"><span data-stu-id="50861-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="50861-306">-Verbose [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="50861-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="50861-307">Indicador para mostrar las salidas detalladas del tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="50861-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="50861-308">Presentamos un ejemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="50861-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="50861-309">Uso del SDK con las interfaces de programación</span><span class="sxs-lookup"><span data-stu-id="50861-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="50861-310">Las interfaces de programación se encuentran en LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="50861-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="50861-311">Puede utilizarlas para integrar la funcionalidad del SDK de U-SQL y la plataforma de pruebas de C# para escalar la prueba local del script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="50861-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="50861-312">En este artículo, utilizaré el proyecto estándar de prueba unitaria de C# para mostrar cómo se usan estas interfaces para probar el script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="50861-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="50861-313">Paso 1: Crear la configuración y el proyecto de prueba unitaria de C#</span><span class="sxs-lookup"><span data-stu-id="50861-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="50861-314">Cree un proyecto de prueba unitaria de C# en Archivo > Nuevo > Proyecto > Visual C# > Probar > Proyecto de prueba unitaria.</span><span class="sxs-lookup"><span data-stu-id="50861-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="50861-315">Agregue LocalRunHelper.exe como referencia para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="50861-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="50861-316">LocalRunHelper.exe se encuentra en \build\runtime\LocalRunHelper.exe en el paquete de Nuget.</span><span class="sxs-lookup"><span data-stu-id="50861-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Agregar referencia del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="50861-318">El SDK de U-SQL **solo** admite entornos x64. Asegúrese de establecer el destino de la plataforma de compilación en x64.</span><span class="sxs-lookup"><span data-stu-id="50861-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="50861-319">Se puede establecer en Propiedad del proyecto > Compilar > Destino de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="50861-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Configurar proyecto x64 del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="50861-321">Asegúrese de establecer el entorno de prueba en x64.</span><span class="sxs-lookup"><span data-stu-id="50861-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="50861-322">En Visual Studio, se puede establecer en Probar > Configuración de pruebas > Arquitectura del procesador predeterminada > x64.</span><span class="sxs-lookup"><span data-stu-id="50861-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Configurar el entorno de prueba x64 del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="50861-324">Asegúrese de copiar todos los archivos de dependencias del directorio build\runtime\ del paquete de Nuget en el directorio de trabajo del proyecto que se suele encontrar en [carpetaDelProyecto]\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="50861-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="50861-325">Paso 2: Crear caso de prueba del script U-SQL</span><span class="sxs-lookup"><span data-stu-id="50861-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="50861-326">A continuación, se muestra el ejemplo de código para la prueba del script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="50861-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="50861-327">Para las pruebas, debe preparar los scripts, los archivos de entrada y los archivos de resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="50861-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget to close MessageOutput to get logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="50861-328">Interfaces de programación de LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="50861-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="50861-329">LocalRunHelper.exe proporciona las interfaces de programación de compilación local ejecución, etc. de U-SQL. A continuación, se enumeran las interfaces.</span><span class="sxs-lookup"><span data-stu-id="50861-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="50861-330">**Constructor**</span><span class="sxs-lookup"><span data-stu-id="50861-330">**Constructor**</span></span>

<span data-ttu-id="50861-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="50861-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="50861-332">.</span><span class="sxs-lookup"><span data-stu-id="50861-332">Parameter</span></span>|<span data-ttu-id="50861-333">Tipo</span><span class="sxs-lookup"><span data-stu-id="50861-333">Type</span></span>|<span data-ttu-id="50861-334">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="50861-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="50861-335">messageOutput</span></span>|<span data-ttu-id="50861-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="50861-336">System.IO.TextWriter</span></span>|<span data-ttu-id="50861-337">para los mensajes de salida; establézcalo en null para usar la consola</span><span class="sxs-lookup"><span data-stu-id="50861-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="50861-338">**Propiedades**</span><span class="sxs-lookup"><span data-stu-id="50861-338">**Properties**</span></span>

|<span data-ttu-id="50861-339">Propiedad</span><span class="sxs-lookup"><span data-stu-id="50861-339">Property</span></span>|<span data-ttu-id="50861-340">Escriba</span><span class="sxs-lookup"><span data-stu-id="50861-340">Type</span></span>|<span data-ttu-id="50861-341">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="50861-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="50861-342">AlgebraPath</span></span>|<span data-ttu-id="50861-343">string</span><span class="sxs-lookup"><span data-stu-id="50861-343">string</span></span>|<span data-ttu-id="50861-344">La ruta de acceso al archivo álgebra (el archivo álgebra es uno de los resultados de compilación)</span><span class="sxs-lookup"><span data-stu-id="50861-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="50861-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="50861-345">CodeBehindReferences</span></span>|<span data-ttu-id="50861-346">string</span><span class="sxs-lookup"><span data-stu-id="50861-346">string</span></span>|<span data-ttu-id="50861-347">Si el script tiene referencias adicionales de código subyacente, especifique las rutas de acceso separadas por ";".</span><span class="sxs-lookup"><span data-stu-id="50861-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="50861-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="50861-348">CppSdkDir</span></span>|<span data-ttu-id="50861-349">string</span><span class="sxs-lookup"><span data-stu-id="50861-349">string</span></span>|<span data-ttu-id="50861-350">Directorio CppSDK</span><span class="sxs-lookup"><span data-stu-id="50861-350">CppSDK directory</span></span>|
|<span data-ttu-id="50861-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="50861-351">CurrentDir</span></span>|<span data-ttu-id="50861-352">string</span><span class="sxs-lookup"><span data-stu-id="50861-352">string</span></span>|<span data-ttu-id="50861-353">Directorio actual</span><span class="sxs-lookup"><span data-stu-id="50861-353">Current directory</span></span>|
|<span data-ttu-id="50861-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="50861-354">DataRoot</span></span>|<span data-ttu-id="50861-355">cadena</span><span class="sxs-lookup"><span data-stu-id="50861-355">string</span></span>|<span data-ttu-id="50861-356">Ruta de acceso raíz de datos</span><span class="sxs-lookup"><span data-stu-id="50861-356">Data root path</span></span>|
|<span data-ttu-id="50861-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="50861-357">DebuggerMailPath</span></span>|<span data-ttu-id="50861-358">string</span><span class="sxs-lookup"><span data-stu-id="50861-358">string</span></span>|<span data-ttu-id="50861-359">La ruta de acceso al buzón interproceso del depurador</span><span class="sxs-lookup"><span data-stu-id="50861-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="50861-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="50861-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="50861-361">booleano</span><span class="sxs-lookup"><span data-stu-id="50861-361">bool</span></span>|<span data-ttu-id="50861-362">Si desea generar carga la configuración de invalidación de redirección de carga de ensamblados</span><span class="sxs-lookup"><span data-stu-id="50861-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="50861-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="50861-363">HasCodeBehind</span></span>|<span data-ttu-id="50861-364">booleano</span><span class="sxs-lookup"><span data-stu-id="50861-364">bool</span></span>|<span data-ttu-id="50861-365">Si el script tiene código subyacente</span><span class="sxs-lookup"><span data-stu-id="50861-365">If the script has code behind</span></span>|
|<span data-ttu-id="50861-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="50861-366">InputDir</span></span>|<span data-ttu-id="50861-367">cadena</span><span class="sxs-lookup"><span data-stu-id="50861-367">string</span></span>|<span data-ttu-id="50861-368">Directorio de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="50861-368">Directory for input data</span></span>|
|<span data-ttu-id="50861-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="50861-369">MessagePath</span></span>|<span data-ttu-id="50861-370">cadena</span><span class="sxs-lookup"><span data-stu-id="50861-370">string</span></span>|<span data-ttu-id="50861-371">Ruta de acceso del archivo de volcado de memoria de mensajes</span><span class="sxs-lookup"><span data-stu-id="50861-371">Message dump file path</span></span>|
|<span data-ttu-id="50861-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="50861-372">OutputDir</span></span>|<span data-ttu-id="50861-373">string</span><span class="sxs-lookup"><span data-stu-id="50861-373">string</span></span>|<span data-ttu-id="50861-374">Directorio de datos de salida</span><span class="sxs-lookup"><span data-stu-id="50861-374">Directory for output data</span></span>|
|<span data-ttu-id="50861-375">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="50861-375">Parallelism</span></span>|<span data-ttu-id="50861-376">int</span><span class="sxs-lookup"><span data-stu-id="50861-376">int</span></span>|<span data-ttu-id="50861-377">Paralelismo para ejecutar el álgebra</span><span class="sxs-lookup"><span data-stu-id="50861-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="50861-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="50861-378">ParentPid</span></span>|<span data-ttu-id="50861-379">int</span><span class="sxs-lookup"><span data-stu-id="50861-379">int</span></span>|<span data-ttu-id="50861-380">PID del elemento primario en el que se supervisa el servicio; para salir se establece en 0 o en un valor negativo para omitirlo.</span><span class="sxs-lookup"><span data-stu-id="50861-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="50861-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="50861-381">ResultPath</span></span>|<span data-ttu-id="50861-382">string</span><span class="sxs-lookup"><span data-stu-id="50861-382">string</span></span>|<span data-ttu-id="50861-383">Ruta de acceso del archivo de volcado de memoria de resultados</span><span class="sxs-lookup"><span data-stu-id="50861-383">Result dump file path</span></span>|
|<span data-ttu-id="50861-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="50861-384">RuntimeDir</span></span>|<span data-ttu-id="50861-385">string</span><span class="sxs-lookup"><span data-stu-id="50861-385">string</span></span>|<span data-ttu-id="50861-386">Directorio del entorno en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-386">Runtime directory</span></span>|
|<span data-ttu-id="50861-387">scriptPath</span><span class="sxs-lookup"><span data-stu-id="50861-387">ScriptPath</span></span>|<span data-ttu-id="50861-388">string</span><span class="sxs-lookup"><span data-stu-id="50861-388">string</span></span>|<span data-ttu-id="50861-389">Lugar donde se puede encontrar el script</span><span class="sxs-lookup"><span data-stu-id="50861-389">Where to find the script</span></span>|
|<span data-ttu-id="50861-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="50861-390">Shallow</span></span>|<span data-ttu-id="50861-391">booleano</span><span class="sxs-lookup"><span data-stu-id="50861-391">bool</span></span>|<span data-ttu-id="50861-392">Compilación superficial o no</span><span class="sxs-lookup"><span data-stu-id="50861-392">Shallow compile or not</span></span>|
|<span data-ttu-id="50861-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="50861-393">TempDir</span></span>|<span data-ttu-id="50861-394">cadena</span><span class="sxs-lookup"><span data-stu-id="50861-394">string</span></span>|<span data-ttu-id="50861-395">Directorio temporal</span><span class="sxs-lookup"><span data-stu-id="50861-395">Temp directory</span></span>|
|<span data-ttu-id="50861-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="50861-396">UseDataBase</span></span>|<span data-ttu-id="50861-397">string</span><span class="sxs-lookup"><span data-stu-id="50861-397">string</span></span>|<span data-ttu-id="50861-398">Especifique la base de datos que se utilizará para el registro de ensamblados temporal de código subyacente; la maestra de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="50861-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="50861-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="50861-399">WorkDir</span></span>|<span data-ttu-id="50861-400">string</span><span class="sxs-lookup"><span data-stu-id="50861-400">string</span></span>|<span data-ttu-id="50861-401">Directorio de trabajo preferido</span><span class="sxs-lookup"><span data-stu-id="50861-401">Preferred working directory</span></span>|


<span data-ttu-id="50861-402">**Método**</span><span class="sxs-lookup"><span data-stu-id="50861-402">**Method**</span></span>

|<span data-ttu-id="50861-403">Método</span><span class="sxs-lookup"><span data-stu-id="50861-403">Method</span></span>|<span data-ttu-id="50861-404">Descripción</span><span class="sxs-lookup"><span data-stu-id="50861-404">Description</span></span>|<span data-ttu-id="50861-405">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="50861-405">Return</span></span>|<span data-ttu-id="50861-406">Parámetro</span><span class="sxs-lookup"><span data-stu-id="50861-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="50861-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="50861-407">public bool DoCompile()</span></span>|<span data-ttu-id="50861-408">Compilación del script U-SQL</span><span class="sxs-lookup"><span data-stu-id="50861-408">Compile the U-SQL script</span></span>|<span data-ttu-id="50861-409">Si se realiza correctamente, devuelve True.</span><span class="sxs-lookup"><span data-stu-id="50861-409">True on success</span></span>| |
|<span data-ttu-id="50861-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="50861-410">public bool DoExec()</span></span>|<span data-ttu-id="50861-411">Ejecución del resultado compilado</span><span class="sxs-lookup"><span data-stu-id="50861-411">Execute the compiled result</span></span>|<span data-ttu-id="50861-412">Si se realiza correctamente, devuelve True.</span><span class="sxs-lookup"><span data-stu-id="50861-412">True on success</span></span>| |
|<span data-ttu-id="50861-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="50861-413">public bool DoRun()</span></span>|<span data-ttu-id="50861-414">Ejecución del script U-SQL (compilación + ejecución)</span><span class="sxs-lookup"><span data-stu-id="50861-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="50861-415">Si se realiza correctamente, devuelve True.</span><span class="sxs-lookup"><span data-stu-id="50861-415">True on success</span></span>| |
|<span data-ttu-id="50861-416">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="50861-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="50861-417">Comprobación de si la ruta de acceso especificada es la ruta de acceso válida al entorno en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="50861-418">True para válida</span><span class="sxs-lookup"><span data-stu-id="50861-418">True for valid</span></span>|<span data-ttu-id="50861-419">La ruta de acceso del directorio del entorno en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="50861-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="50861-420">Preguntas más frecuentes sobre problemas comunes</span><span class="sxs-lookup"><span data-stu-id="50861-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="50861-421">Error 1:</span><span class="sxs-lookup"><span data-stu-id="50861-421">Error 1:</span></span>
<span data-ttu-id="50861-422">E_CSC_SYSTEM_INTERNAL: Error interno.</span><span class="sxs-lookup"><span data-stu-id="50861-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="50861-423">No se pudo cargar el archivo o ensamblado 'ScopeEngineManaged.dll' ni una de sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="50861-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="50861-424">No se pudo encontrar el módulo especificado.</span><span class="sxs-lookup"><span data-stu-id="50861-424">The specified module could not be found.</span></span>

<span data-ttu-id="50861-425">Compruebe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="50861-425">Please check the following:</span></span>

- <span data-ttu-id="50861-426">Asegúrese de que tiene un entorno x64.</span><span class="sxs-lookup"><span data-stu-id="50861-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="50861-427">La plataforma de destino de compilación y el entorno de prueba deben ser x64. Consulte el **Paso 1: Crear la configuración y el proyecto de prueba unitaria de C#** más arriba.</span><span class="sxs-lookup"><span data-stu-id="50861-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="50861-428">Asegúrese de que ha copiado todos los archivos de dependencias del directorio \build\runtime\ del paquete Nuget al directorio de trabajo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="50861-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="50861-429">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50861-429">Next steps</span></span>

* <span data-ttu-id="50861-430">Para obtener más información sobre U-SQL, consulte [Introducción al lenguaje U-SQL de Análisis de Azure Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="50861-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="50861-431">Para registrar información de diagnóstico, consulte [Acceso a los registros de diagnóstico de Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="50861-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="50861-432">Para ver una consulta más compleja, consulte [Tutorial: Análisis de registros de sitios web mediante Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="50861-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="50861-433">Para ver los detalles del trabajo, consulte [Usar el explorador de trabajos y la vista de trabajos para trabajos de Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="50861-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="50861-434">Para usar la vista de ejecución de vértices, vea [Uso de la vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="50861-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
