---
title: aaaScale U-SQL local ejecutar y probar con el SDK de Azure datos Lake U-SQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo trabajos de tooscale U-SQL de SDK de Azure datos Lake U-SQL toouse locales ejecutan y probar con la línea de comandos e interfaces de programación en la estación de trabajo local."
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
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="a31df-103">Escalado de prueba y depuración local de U-SQL con el SDK de U-SQL para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a31df-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="a31df-104">Al desarrollar el script U-SQL, es común toorun y script de prueba U SQL localmente antes de enviar se toocloud.</span><span class="sxs-lookup"><span data-stu-id="a31df-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="a31df-105">Azure Data Lake proporciona un paquete Nuget denominado SDK de U-SQL para Azure Data Lake para esta situación, por lo que le resultará muy fácil realizar el escalado de prueba y ejecución local de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="a31df-106">También es posible toointegrate esta U-SQL probar con la compilación de CI (integración continua) sistema tooautomate hello y prueba.</span><span class="sxs-lookup"><span data-stu-id="a31df-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="a31df-107">Si le interesa cómo toomanually local ejecutar y depurar el script U-SQL con herramientas de interfaz gráfica de usuario, puede usar Azure Data Lake Tools para Visual Studio para.</span><span class="sxs-lookup"><span data-stu-id="a31df-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="a31df-108">Puede obtener más información sobre esto [aquí](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="a31df-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="a31df-109">Instalación del SDK de U-SQL para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a31df-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="a31df-110">Puede obtener Hola SDK de SQL Azure datos Lake U [aquí](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) en Nuget.org. Y antes de usarlo, debe toomake que tengan dependencias como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="a31df-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="a31df-111">Dependencias</span><span class="sxs-lookup"><span data-stu-id="a31df-111">Dependencies</span></span>

<span data-ttu-id="a31df-112">Hola datos Lake U-SQL SDK requiere Hola siguientes dependencias:</span><span class="sxs-lookup"><span data-stu-id="a31df-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="a31df-113">[Microsoft .NET Framework 4.6 o superior](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="a31df-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="a31df-114">Microsoft Visual C++ 14 y el SDK de Windows 10.0.10240.0 o posterior (que se denomina CppSDK en este artículo).</span><span class="sxs-lookup"><span data-stu-id="a31df-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="a31df-115">Hay dos maneras tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="a31df-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="a31df-116">Instale [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="a31df-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="a31df-117">Tendrá una carpeta \Windows Kits\10 en la carpeta de archivos de programa Hola: por ejemplo, C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="a31df-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="a31df-118">También encontrará la versión del SDK de Windows 10 de hello en \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="a31df-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="a31df-119">Si no ve estas carpetas, vuelva a instalar Visual Studio y estar seguro de tooselect Hola SDK de Windows 10 durante la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="a31df-120">Si tiene instalado con Visual Studio, compilador de saludo U-SQL local considerará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a31df-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![SDK de Windows 10 para ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="a31df-122">Instale [Data Lake Tools para Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="a31df-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="a31df-123">Puede encontrar Hola preestablecido archivos de Visual C++ y el SDK de Windows en C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="a31df-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="a31df-124">En este caso, compilador de saludo U-SQL local no encuentra las dependencias de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a31df-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="a31df-125">Necesita ruta de acceso de toospecify hello CppSDK para él.</span><span class="sxs-lookup"><span data-stu-id="a31df-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="a31df-126">Puede copiar la ubicación de los archivos tooanother Hola o utilizarlo tal como está.</span><span class="sxs-lookup"><span data-stu-id="a31df-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="a31df-127">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="a31df-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="a31df-128">Raíz de datos</span><span class="sxs-lookup"><span data-stu-id="a31df-128">Data root</span></span>

<span data-ttu-id="a31df-129">carpeta de datos raíz de Hello es un "almacén local" para la cuenta de proceso local Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="a31df-130">Es la cuenta de almacén de Azure Data Lake toohello equivalente de una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a31df-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="a31df-131">Cambiar tooa carpeta raíz de datos diferentes es igual que cambiar la cuenta de otro almacén de tooa.</span><span class="sxs-lookup"><span data-stu-id="a31df-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="a31df-132">Si desea tooaccess comúnmente suelen compartir datos con las carpetas raíz de datos diferente, debe usar rutas de acceso absolutas en las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="a31df-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="a31df-133">O bien, crear vínculos simbólicos de sistema de archivos (por ejemplo, **mklink** en NTFS) en la carpeta toopoint toohello de hello raíz de datos de los datos compartidos.</span><span class="sxs-lookup"><span data-stu-id="a31df-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="a31df-134">carpeta de datos raíz de Hola se utiliza para:</span><span class="sxs-lookup"><span data-stu-id="a31df-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="a31df-135">Almacenar metadatos, lo que incluye bases de datos, tablas, funciones con valores de tabla (TVF) y ensamblados.</span><span class="sxs-lookup"><span data-stu-id="a31df-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="a31df-136">Buscar Hola de entrada y las rutas de acceso de salida que se definen como rutas de acceso relativas en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="a31df-137">Usar rutas de acceso relativas resulta más fácil toodeploy su tooAzure de proyectos U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="a31df-138">Ruta de archivo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="a31df-138">File path in U-SQL</span></span>

<span data-ttu-id="a31df-139">Puede usar tanto una ruta de acceso relativa como una ruta de acceso absoluta local en los scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="a31df-140">ruta de acceso relativa de Hello es relativa toohello ruta de la carpeta de raíz de datos especificado.</span><span class="sxs-lookup"><span data-stu-id="a31df-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="a31df-141">Se recomienda que se utilice "/" como Hola toomake de separador de ruta de acceso las secuencias de comandos compatibles con el lado del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="a31df-142">Estos son algunos ejemplos de rutas de acceso relativas y sus rutas de acceso absolutas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="a31df-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="a31df-143">En estos ejemplos, C:\LocalRunDataRoot es la carpeta de datos raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="a31df-144">Ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="a31df-144">Relative path</span></span>|<span data-ttu-id="a31df-145">Ruta de acceso absoluta</span><span class="sxs-lookup"><span data-stu-id="a31df-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="a31df-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="a31df-146">/abc/def/input.csv</span></span> |<span data-ttu-id="a31df-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="a31df-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="a31df-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="a31df-148">abc/def/input.csv</span></span>  |<span data-ttu-id="a31df-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="a31df-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="a31df-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="a31df-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="a31df-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="a31df-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="a31df-152">Directorio de trabajo</span><span class="sxs-lookup"><span data-stu-id="a31df-152">Working directory</span></span>

<span data-ttu-id="a31df-153">Cuando se ejecuta el script de Hola U-SQL localmente, se crea un directorio de trabajo durante la compilación en el directorio de ejecución actual.</span><span class="sxs-lookup"><span data-stu-id="a31df-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="a31df-154">Además toohello compilación genera, hello necesarios en tiempo de ejecución para la ejecución local se generarán directorio de trabajo de instantáneas toothis copiada.</span><span class="sxs-lookup"><span data-stu-id="a31df-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="a31df-155">Hola carpeta raíz de directorio de trabajo se denomina "ScopeWorkDir" y archivos de hello en hello directorio de trabajo son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a31df-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="a31df-156">Directorio o archivo</span><span class="sxs-lookup"><span data-stu-id="a31df-156">Directory/file</span></span>|<span data-ttu-id="a31df-157">Directorio o archivo</span><span class="sxs-lookup"><span data-stu-id="a31df-157">Directory/file</span></span>|<span data-ttu-id="a31df-158">Directorio o archivo</span><span class="sxs-lookup"><span data-stu-id="a31df-158">Directory/file</span></span>|<span data-ttu-id="a31df-159">Definición</span><span class="sxs-lookup"><span data-stu-id="a31df-159">Definition</span></span>|<span data-ttu-id="a31df-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="a31df-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="a31df-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="a31df-162">Cadena de hash de la versión del runtime</span><span class="sxs-lookup"><span data-stu-id="a31df-162">Hash string of runtime version</span></span>|<span data-ttu-id="a31df-163">Instantánea de los archivos del runtime necesarios para la ejecución local</span><span class="sxs-lookup"><span data-stu-id="a31df-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="a31df-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="a31df-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="a31df-165">Nombre de script + cadena de hash de la ruta de acceso del script</span><span class="sxs-lookup"><span data-stu-id="a31df-165">Script name + hash string of script path</span></span>|<span data-ttu-id="a31df-166">Resultados de compilación y registro de los pasos de ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="a31df-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="a31df-167">\_script\_.abr</span></span>|<span data-ttu-id="a31df-168">Salida del compilador</span><span class="sxs-lookup"><span data-stu-id="a31df-168">Compiler output</span></span>|<span data-ttu-id="a31df-169">Archivo de álgebra</span><span class="sxs-lookup"><span data-stu-id="a31df-169">Algebra file</span></span>|
| | |<span data-ttu-id="a31df-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="a31df-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="a31df-171">Salida del compilador</span><span class="sxs-lookup"><span data-stu-id="a31df-171">Compiler output</span></span>|<span data-ttu-id="a31df-172">Código administrado generado</span><span class="sxs-lookup"><span data-stu-id="a31df-172">Generated managed code</span></span>|
| | |<span data-ttu-id="a31df-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="a31df-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="a31df-174">Salida del compilador</span><span class="sxs-lookup"><span data-stu-id="a31df-174">Compiler output</span></span>|<span data-ttu-id="a31df-175">Código nativo generado</span><span class="sxs-lookup"><span data-stu-id="a31df-175">Generated native code</span></span>|
| | |<span data-ttu-id="a31df-176">ensamblados de referencia</span><span class="sxs-lookup"><span data-stu-id="a31df-176">referenced assemblies</span></span>|<span data-ttu-id="a31df-177">Referencia de ensamblado</span><span class="sxs-lookup"><span data-stu-id="a31df-177">Assembly reference</span></span>|<span data-ttu-id="a31df-178">Archivos de ensamblados de referencia</span><span class="sxs-lookup"><span data-stu-id="a31df-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="a31df-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="a31df-179">deployed_resources</span></span>|<span data-ttu-id="a31df-180">Implementación de recursos</span><span class="sxs-lookup"><span data-stu-id="a31df-180">Resource deployment</span></span>|<span data-ttu-id="a31df-181">Archivos de implementación de recursos</span><span class="sxs-lookup"><span data-stu-id="a31df-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="a31df-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="a31df-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="a31df-183">Registro de ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-183">Execution log</span></span>|<span data-ttu-id="a31df-184">Registro de pasos de ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="a31df-185">Usar hello SDK desde la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="a31df-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="a31df-186">Interfaz de línea de comandos de la aplicación auxiliar de Hola</span><span class="sxs-lookup"><span data-stu-id="a31df-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="a31df-187">En SDK directory\build\runtime, LocalRunHelper.exe es aplicación de línea de comandos auxiliar de Hola que proporciona interfaces toomost de hello usada local y ejecutar funciones.</span><span class="sxs-lookup"><span data-stu-id="a31df-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="a31df-188">Tenga en cuenta que ambos Hola comandos y modificadores de argumento Hola distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a31df-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="a31df-189">tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="a31df-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="a31df-190">Ejecutar LocalRunHelper.exe sin argumentos o con hello **ayuda** cambiar información de Ayuda de Hola tooshow:</span><span class="sxs-lookup"><span data-stu-id="a31df-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="a31df-191">Hola información de ayuda:</span><span class="sxs-lookup"><span data-stu-id="a31df-191">In hello help information:</span></span>

-  <span data-ttu-id="a31df-192">**Comando** proporciona Hola el nombre de comando.</span><span class="sxs-lookup"><span data-stu-id="a31df-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="a31df-193">**Required Argument** enumera los argumentos que se deben proporcionar.</span><span class="sxs-lookup"><span data-stu-id="a31df-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="a31df-194">**Optional Argument** enumera argumentos que son opcionales, con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="a31df-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="a31df-195">Argumentos booleanos opcionales no tienen parámetros y sus repeticiones significan el valor predeterminado de tootheir negativo.</span><span class="sxs-lookup"><span data-stu-id="a31df-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="a31df-196">Valor devuelto y registro</span><span class="sxs-lookup"><span data-stu-id="a31df-196">Return value and logging</span></span>

<span data-ttu-id="a31df-197">Devuelve la aplicación auxiliar de Hello **0** para el éxito y **-1** error.</span><span class="sxs-lookup"><span data-stu-id="a31df-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="a31df-198">De forma predeterminada, auxiliar Hola envía consola actual de todos los mensajes toohello.</span><span class="sxs-lookup"><span data-stu-id="a31df-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="a31df-199">Sin embargo, la mayoría de los comandos de hello admite hello **- MessageOut rutaDeAccesoAlArchivoDeRegistro** argumento opcional que redirija Hola genera el archivo de registro tooa.</span><span class="sxs-lookup"><span data-stu-id="a31df-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="a31df-200">Configuración de la variable de entorno</span><span class="sxs-lookup"><span data-stu-id="a31df-200">Environment variable configuring</span></span>

<span data-ttu-id="a31df-201">La ejecución local de U-SQL requiere una raíz de datos explícita como cuenta de almacenamiento local, así como una ruta de acceso de CppSDK explícita para las dependencias.</span><span class="sxs-lookup"><span data-stu-id="a31df-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="a31df-202">Puede ambos argumento de hello establecido en la variable de entorno de línea de comandos o está establecida para ellos.</span><span class="sxs-lookup"><span data-stu-id="a31df-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="a31df-203">Conjunto hello **SCOPE_CPP_SDK** variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="a31df-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="a31df-204">Si se producen hello SDK de Windows y Microsoft Visual C++ mediante la instalación de Data Lake Tools para Visual Studio, compruebe que dispone de hello siguiente carpeta:</span><span class="sxs-lookup"><span data-stu-id="a31df-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="a31df-205">Definir una nueva variable de entorno denominada **SCOPE_CPP_SDK** toopoint toothis directory.</span><span class="sxs-lookup"><span data-stu-id="a31df-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="a31df-206">O copie Hola carpeta toohello otra ubicación y especificar **SCOPE_CPP_SDK** que.</span><span class="sxs-lookup"><span data-stu-id="a31df-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="a31df-207">En la variable de entorno de suma toosetting hello, puede especificar hello **- CppSDK** argumento cuando se usa la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="a31df-208">Este argumento sobrescribe la variable de entorno CppSDK predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a31df-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="a31df-209">Conjunto hello **LOCALRUN_DATAROOT** variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="a31df-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="a31df-210">Definir una nueva variable de entorno denominada **LOCALRUN_DATAROOT** que apunta la raíz de datos de toohello.</span><span class="sxs-lookup"><span data-stu-id="a31df-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="a31df-211">En la variable de entorno de suma toosetting hello, puede especificar hello **- DataRoot** argumento con ruta de acceso de datos raíz de hello cuando se usa una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a31df-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="a31df-212">Este argumento sobrescribe la variable de entorno raíz de datos predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a31df-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="a31df-213">Debe tooadd esta línea de comandos de tooevery de argumento que está ejecutando para que se puede sobrescribir la variable de entorno de datos raíz de hello predeterminada para todas las operaciones.</span><span class="sxs-lookup"><span data-stu-id="a31df-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="a31df-214">Ejemplos de uso de línea de comandos del SDK</span><span class="sxs-lookup"><span data-stu-id="a31df-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="a31df-215">Compilación y ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-215">Compile and run</span></span>

<span data-ttu-id="a31df-216">Hola **ejecutar** se utiliza el comando toocompile Hola script y, a continuación, ejecutar resultados compilados.</span><span class="sxs-lookup"><span data-stu-id="a31df-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="a31df-217">Sus argumentos de línea de comandos son una combinación de los de **compile** y **execute**.</span><span class="sxs-lookup"><span data-stu-id="a31df-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="a31df-218">Hello siguiente es argumentos opcionales para **ejecutar**:</span><span class="sxs-lookup"><span data-stu-id="a31df-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="a31df-219">Argumento</span><span class="sxs-lookup"><span data-stu-id="a31df-219">Argument</span></span>|<span data-ttu-id="a31df-220">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="a31df-220">Default value</span></span>|<span data-ttu-id="a31df-221">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="a31df-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="a31df-222">-CodeBehind</span></span>|<span data-ttu-id="a31df-223">False</span><span class="sxs-lookup"><span data-stu-id="a31df-223">False</span></span>|<span data-ttu-id="a31df-224">script de Hola tiene .cs código subyacente</span><span class="sxs-lookup"><span data-stu-id="a31df-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="a31df-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="a31df-225">-CppSDK</span></span>| |<span data-ttu-id="a31df-226">Directorio CppSDK</span><span class="sxs-lookup"><span data-stu-id="a31df-226">CppSDK Directory</span></span>|
|<span data-ttu-id="a31df-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="a31df-227">-DataRoot</span></span>| <span data-ttu-id="a31df-228">Variable de entorno de DataRoot</span><span class="sxs-lookup"><span data-stu-id="a31df-228">DataRoot environment variable</span></span>|<span data-ttu-id="a31df-229">DataRoot para la ejecución local, predeterminado demasiado variable de entorno 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="a31df-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="a31df-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="a31df-230">-MessageOut</span></span>| |<span data-ttu-id="a31df-231">Mensajes de volcado de memoria en el archivo de consola tooa</span><span class="sxs-lookup"><span data-stu-id="a31df-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="a31df-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="a31df-232">-Parallel</span></span>|<span data-ttu-id="a31df-233">1</span><span class="sxs-lookup"><span data-stu-id="a31df-233">1</span></span>|<span data-ttu-id="a31df-234">Ejecute hello plan con hello especificado paralelismo</span><span class="sxs-lookup"><span data-stu-id="a31df-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="a31df-235">-References</span><span class="sxs-lookup"><span data-stu-id="a31df-235">-References</span></span>| |<span data-ttu-id="a31df-236">Lista de ensamblados de referencia de las rutas de acceso tooextra o archivos de datos de código subyacente, separado por ';'</span><span class="sxs-lookup"><span data-stu-id="a31df-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="a31df-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="a31df-237">-UdoRedirect</span></span>|<span data-ttu-id="a31df-238">False</span><span class="sxs-lookup"><span data-stu-id="a31df-238">False</span></span>|<span data-ttu-id="a31df-239">Generar la configuración de redirección de ensamblado de Udo</span><span class="sxs-lookup"><span data-stu-id="a31df-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="a31df-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="a31df-240">-UseDatabase</span></span>|<span data-ttu-id="a31df-241">maestro</span><span class="sxs-lookup"><span data-stu-id="a31df-241">master</span></span>|<span data-ttu-id="a31df-242">Toouse de base de datos para el código subyacente de registro de ensamblados temporales</span><span class="sxs-lookup"><span data-stu-id="a31df-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="a31df-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="a31df-243">-Verbose</span></span>|<span data-ttu-id="a31df-244">False</span><span class="sxs-lookup"><span data-stu-id="a31df-244">False</span></span>|<span data-ttu-id="a31df-245">Mostrar resultados detallados del runtime</span><span class="sxs-lookup"><span data-stu-id="a31df-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="a31df-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="a31df-246">-WorkDir</span></span>|<span data-ttu-id="a31df-247">Directorio actual</span><span class="sxs-lookup"><span data-stu-id="a31df-247">Current Directory</span></span>|<span data-ttu-id="a31df-248">Directorio para las salidas y el uso del compilador</span><span class="sxs-lookup"><span data-stu-id="a31df-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="a31df-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="a31df-249">-RunScopeCEP</span></span>|<span data-ttu-id="a31df-250">0</span><span class="sxs-lookup"><span data-stu-id="a31df-250">0</span></span>|<span data-ttu-id="a31df-251">ScopeCEP modo toouse</span><span class="sxs-lookup"><span data-stu-id="a31df-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="a31df-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="a31df-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="a31df-253">temp</span><span class="sxs-lookup"><span data-stu-id="a31df-253">temp</span></span>|<span data-ttu-id="a31df-254">Ruta de acceso temporal toouse streaming de datos</span><span class="sxs-lookup"><span data-stu-id="a31df-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="a31df-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="a31df-255">-OptFlags</span></span>| |<span data-ttu-id="a31df-256">Lista de marcas de optimizador separadas por comas</span><span class="sxs-lookup"><span data-stu-id="a31df-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="a31df-257">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a31df-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="a31df-258">Además de combinación **compilar** y **ejecutar**, puede compilar y ejecutar ejecutables Hola compilado por separado.</span><span class="sxs-lookup"><span data-stu-id="a31df-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="a31df-259">Compilación de un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="a31df-259">Compile a U-SQL script</span></span>

<span data-ttu-id="a31df-260">Hola **compilar** comando es tooexecutables de script usados toocompile U T-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="a31df-261">Hello siguiente es argumentos opcionales para **compilar**:</span><span class="sxs-lookup"><span data-stu-id="a31df-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="a31df-262">Argumento</span><span class="sxs-lookup"><span data-stu-id="a31df-262">Argument</span></span>|<span data-ttu-id="a31df-263">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="a31df-264">-CodeBehind [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="a31df-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="a31df-265">script de Hola tiene .cs código subyacente</span><span class="sxs-lookup"><span data-stu-id="a31df-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="a31df-266">-CppSDK [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="a31df-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="a31df-267">Directorio CppSDK</span><span class="sxs-lookup"><span data-stu-id="a31df-267">CppSDK Directory</span></span>|
| <span data-ttu-id="a31df-268">-DataRoot [valor predeterminado 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="a31df-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="a31df-269">DataRoot para la ejecución local, predeterminado demasiado variable de entorno 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="a31df-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="a31df-270">-MessageOut [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="a31df-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="a31df-271">Mensajes de volcado de memoria en el archivo de consola tooa</span><span class="sxs-lookup"><span data-stu-id="a31df-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="a31df-272">-References [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="a31df-272">-References [default value '']</span></span>|<span data-ttu-id="a31df-273">Lista de ensamblados de referencia de las rutas de acceso tooextra o archivos de datos de código subyacente, separado por ';'</span><span class="sxs-lookup"><span data-stu-id="a31df-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="a31df-274">-Shallow [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="a31df-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="a31df-275">Compilación superficial</span><span class="sxs-lookup"><span data-stu-id="a31df-275">Shallow compile</span></span>|
| <span data-ttu-id="a31df-276">-UdoRedirect [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="a31df-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="a31df-277">Generar la configuración de redirección de ensamblado de Udo</span><span class="sxs-lookup"><span data-stu-id="a31df-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="a31df-278">-UseDatabase [valor predeterminado 'master']</span><span class="sxs-lookup"><span data-stu-id="a31df-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="a31df-279">Toouse de base de datos para el código subyacente de registro de ensamblados temporales</span><span class="sxs-lookup"><span data-stu-id="a31df-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="a31df-280">-WorkDir [valor predeterminado 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="a31df-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="a31df-281">Directorio para las salidas y el uso del compilador</span><span class="sxs-lookup"><span data-stu-id="a31df-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="a31df-282">-RunScopeCEP [valor predeterminado '0']</span><span class="sxs-lookup"><span data-stu-id="a31df-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="a31df-283">ScopeCEP modo toouse</span><span class="sxs-lookup"><span data-stu-id="a31df-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="a31df-284">-ScopeCEPTempPath [valor predeterminado 'temp']</span><span class="sxs-lookup"><span data-stu-id="a31df-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="a31df-285">Ruta de acceso temporal toouse streaming de datos</span><span class="sxs-lookup"><span data-stu-id="a31df-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="a31df-286">-OptFlags [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="a31df-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="a31df-287">Lista de marcas de optimizador separadas por comas</span><span class="sxs-lookup"><span data-stu-id="a31df-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="a31df-288">Estos son algunos ejemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="a31df-288">Here are some usage examples.</span></span>

<span data-ttu-id="a31df-289">Compile un script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a31df-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="a31df-290">Compilar un script U-SQL y establecer carpeta de datos raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="a31df-291">Tenga en cuenta que esta acción sobrescribirá la variable de entorno de conjunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="a31df-292">Compile un script U-SQL y establezca el directorio de trabajo, el ensamblado de referencia y la base de datos:</span><span class="sxs-lookup"><span data-stu-id="a31df-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="a31df-293">Ejecución de resultados compilados</span><span class="sxs-lookup"><span data-stu-id="a31df-293">Execute compiled results</span></span>

<span data-ttu-id="a31df-294">Hola **ejecutar** comando es resultados tooexecute usado compilado.</span><span class="sxs-lookup"><span data-stu-id="a31df-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="a31df-295">Hello siguiente es argumentos opcionales para **ejecutar**:</span><span class="sxs-lookup"><span data-stu-id="a31df-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="a31df-296">Argumento</span><span class="sxs-lookup"><span data-stu-id="a31df-296">Argument</span></span>|<span data-ttu-id="a31df-297">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="a31df-298">-DataRoot [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="a31df-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="a31df-299">Raíz de datos para la ejecución de metadatos.</span><span class="sxs-lookup"><span data-stu-id="a31df-299">Data root for metadata execution.</span></span> <span data-ttu-id="a31df-300">El valor predeterminado es toohello **LOCALRUN_DATAROOT** variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="a31df-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="a31df-301">-MessageOut [valor predeterminado '']</span><span class="sxs-lookup"><span data-stu-id="a31df-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="a31df-302">Los mensajes en el archivo de hello consola tooa de volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="a31df-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="a31df-303">-Parallel [valor predeterminado '1']</span><span class="sxs-lookup"><span data-stu-id="a31df-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="a31df-304">Pasos de ejecución local de indicador toorun Hola generado con hello especifican el nivel de paralelismo.</span><span class="sxs-lookup"><span data-stu-id="a31df-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="a31df-305">-Verbose [valor predeterminado 'False']</span><span class="sxs-lookup"><span data-stu-id="a31df-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="a31df-306">Indicador tooshow detallada genera una salida en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a31df-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="a31df-307">Presentamos un ejemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="a31df-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="a31df-308">Usar hello SDK con interfaces de programación</span><span class="sxs-lookup"><span data-stu-id="a31df-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="a31df-309">interfaces de programación de Hola se encuentran en hello LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="a31df-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="a31df-310">Puede usar funcionalidad de hello toointegrate de hello U-SQL SDK y Hola tooscale de marco de pruebas de C# de la prueba local del script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="a31df-311">En este artículo, usaré Hola estándar C# unidad prueba proyecto tooshow cómo toouse estas interfaces tootest el script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="a31df-312">Paso 1: Crear la configuración y el proyecto de prueba unitaria de C#</span><span class="sxs-lookup"><span data-stu-id="a31df-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="a31df-313">Cree un proyecto de prueba unitaria de C# en Archivo > Nuevo > Proyecto > Visual C# > Probar > Proyecto de prueba unitaria.</span><span class="sxs-lookup"><span data-stu-id="a31df-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="a31df-314">Agregar LocalRunHelper.exe como una referencia de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="a31df-315">Hola LocalRunHelper.exe se encuentra en \build\runtime\LocalRunHelper.exe en el paquete de Nuget.</span><span class="sxs-lookup"><span data-stu-id="a31df-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Agregar referencia del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="a31df-317">SDK de U-SQL **sólo** soporte x64 entorno, asegúrese de tooset seguro el destino de plataforma de compilación como x64.</span><span class="sxs-lookup"><span data-stu-id="a31df-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="a31df-318">Se puede establecer en Propiedad del proyecto > Compilar > Destino de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="a31df-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Configurar proyecto x64 del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="a31df-320">Hacer tooset seguro de que el entorno de prueba como x64.</span><span class="sxs-lookup"><span data-stu-id="a31df-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="a31df-321">En Visual Studio, se puede establecer en Probar > Configuración de pruebas > Arquitectura del procesador predeterminada > x64.</span><span class="sxs-lookup"><span data-stu-id="a31df-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Configurar el entorno de prueba x64 del SDK de U-SQL para Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="a31df-323">Asegúrese de que toocopy todos los archivos de dependencia en el directorio de trabajo de tooproject NugetPackage\build\runtime\ que se encuentra normalmente en ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="a31df-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="a31df-324">Paso 2: Crear caso de prueba del script U-SQL</span><span class="sxs-lookup"><span data-stu-id="a31df-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="a31df-325">A continuación se muestra código de ejemplo de Hola para prueba de script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a31df-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="a31df-326">Para las pruebas, deberá tooprepare scripts, archivos de entrada y archivos de resultados esperado.</span><span class="sxs-lookup"><span data-stu-id="a31df-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

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
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
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

                //Don't forget tooclose MessageOutput tooget logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="a31df-327">Interfaces de programación de LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="a31df-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="a31df-328">LocalRunHelper.exe proporciona Hola interfaces de programación para compilación local U-SQL, ejecutar, interfaces de hello etc. se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="a31df-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="a31df-329">**Constructor**</span><span class="sxs-lookup"><span data-stu-id="a31df-329">**Constructor**</span></span>

<span data-ttu-id="a31df-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="a31df-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="a31df-331">.</span><span class="sxs-lookup"><span data-stu-id="a31df-331">Parameter</span></span>|<span data-ttu-id="a31df-332">Tipo</span><span class="sxs-lookup"><span data-stu-id="a31df-332">Type</span></span>|<span data-ttu-id="a31df-333">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="a31df-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="a31df-334">messageOutput</span></span>|<span data-ttu-id="a31df-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="a31df-335">System.IO.TextWriter</span></span>|<span data-ttu-id="a31df-336">para los mensajes de salida, establezca toonull toouse consola</span><span class="sxs-lookup"><span data-stu-id="a31df-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="a31df-337">**Propiedades**</span><span class="sxs-lookup"><span data-stu-id="a31df-337">**Properties**</span></span>

|<span data-ttu-id="a31df-338">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a31df-338">Property</span></span>|<span data-ttu-id="a31df-339">Escriba</span><span class="sxs-lookup"><span data-stu-id="a31df-339">Type</span></span>|<span data-ttu-id="a31df-340">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="a31df-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="a31df-341">AlgebraPath</span></span>|<span data-ttu-id="a31df-342">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-342">string</span></span>|<span data-ttu-id="a31df-343">archivo de tooalgebra de ruta de acceso de Hello (archivo álgebra es uno de los resultados de compilación de hello)</span><span class="sxs-lookup"><span data-stu-id="a31df-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="a31df-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="a31df-344">CodeBehindReferences</span></span>|<span data-ttu-id="a31df-345">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-345">string</span></span>|<span data-ttu-id="a31df-346">Si el script de Hola tiene código adicional detrás de las referencias, especificar rutas de acceso de hello separados por ';'</span><span class="sxs-lookup"><span data-stu-id="a31df-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="a31df-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="a31df-347">CppSdkDir</span></span>|<span data-ttu-id="a31df-348">string</span><span class="sxs-lookup"><span data-stu-id="a31df-348">string</span></span>|<span data-ttu-id="a31df-349">Directorio CppSDK</span><span class="sxs-lookup"><span data-stu-id="a31df-349">CppSDK directory</span></span>|
|<span data-ttu-id="a31df-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="a31df-350">CurrentDir</span></span>|<span data-ttu-id="a31df-351">string</span><span class="sxs-lookup"><span data-stu-id="a31df-351">string</span></span>|<span data-ttu-id="a31df-352">Directorio actual</span><span class="sxs-lookup"><span data-stu-id="a31df-352">Current directory</span></span>|
|<span data-ttu-id="a31df-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="a31df-353">DataRoot</span></span>|<span data-ttu-id="a31df-354">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-354">string</span></span>|<span data-ttu-id="a31df-355">Ruta de acceso raíz de datos</span><span class="sxs-lookup"><span data-stu-id="a31df-355">Data root path</span></span>|
|<span data-ttu-id="a31df-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="a31df-356">DebuggerMailPath</span></span>|<span data-ttu-id="a31df-357">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-357">string</span></span>|<span data-ttu-id="a31df-358">el procesador de mensajes de Hola ruta de acceso toodebugger</span><span class="sxs-lookup"><span data-stu-id="a31df-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="a31df-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="a31df-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="a31df-360">booleano</span><span class="sxs-lookup"><span data-stu-id="a31df-360">bool</span></span>|<span data-ttu-id="a31df-361">Si lo deseamos carga de ensamblado toogenerate redirección invalidar configuración</span><span class="sxs-lookup"><span data-stu-id="a31df-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="a31df-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="a31df-362">HasCodeBehind</span></span>|<span data-ttu-id="a31df-363">booleano</span><span class="sxs-lookup"><span data-stu-id="a31df-363">bool</span></span>|<span data-ttu-id="a31df-364">Si el script de Hola tiene código subyacente</span><span class="sxs-lookup"><span data-stu-id="a31df-364">If hello script has code behind</span></span>|
|<span data-ttu-id="a31df-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="a31df-365">InputDir</span></span>|<span data-ttu-id="a31df-366">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-366">string</span></span>|<span data-ttu-id="a31df-367">Directorio de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="a31df-367">Directory for input data</span></span>|
|<span data-ttu-id="a31df-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="a31df-368">MessagePath</span></span>|<span data-ttu-id="a31df-369">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-369">string</span></span>|<span data-ttu-id="a31df-370">Ruta de acceso del archivo de volcado de memoria de mensajes</span><span class="sxs-lookup"><span data-stu-id="a31df-370">Message dump file path</span></span>|
|<span data-ttu-id="a31df-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="a31df-371">OutputDir</span></span>|<span data-ttu-id="a31df-372">string</span><span class="sxs-lookup"><span data-stu-id="a31df-372">string</span></span>|<span data-ttu-id="a31df-373">Directorio de datos de salida</span><span class="sxs-lookup"><span data-stu-id="a31df-373">Directory for output data</span></span>|
|<span data-ttu-id="a31df-374">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="a31df-374">Parallelism</span></span>|<span data-ttu-id="a31df-375">int</span><span class="sxs-lookup"><span data-stu-id="a31df-375">int</span></span>|<span data-ttu-id="a31df-376">Álgebra de paralelismo toorun Hola</span><span class="sxs-lookup"><span data-stu-id="a31df-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="a31df-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="a31df-377">ParentPid</span></span>|<span data-ttu-id="a31df-378">int</span><span class="sxs-lookup"><span data-stu-id="a31df-378">int</span></span>|<span data-ttu-id="a31df-379">PID del elemento primario de hello en qué Hola servicio supervisa tooexit, conjunto too0 o tooignore negativo</span><span class="sxs-lookup"><span data-stu-id="a31df-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="a31df-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="a31df-380">ResultPath</span></span>|<span data-ttu-id="a31df-381">string</span><span class="sxs-lookup"><span data-stu-id="a31df-381">string</span></span>|<span data-ttu-id="a31df-382">Ruta de acceso del archivo de volcado de memoria de resultados</span><span class="sxs-lookup"><span data-stu-id="a31df-382">Result dump file path</span></span>|
|<span data-ttu-id="a31df-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="a31df-383">RuntimeDir</span></span>|<span data-ttu-id="a31df-384">string</span><span class="sxs-lookup"><span data-stu-id="a31df-384">string</span></span>|<span data-ttu-id="a31df-385">Directorio del entorno en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-385">Runtime directory</span></span>|
|<span data-ttu-id="a31df-386">scriptPath</span><span class="sxs-lookup"><span data-stu-id="a31df-386">ScriptPath</span></span>|<span data-ttu-id="a31df-387">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-387">string</span></span>|<span data-ttu-id="a31df-388">Donde toofind hello secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="a31df-388">Where toofind hello script</span></span>|
|<span data-ttu-id="a31df-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="a31df-389">Shallow</span></span>|<span data-ttu-id="a31df-390">booleano</span><span class="sxs-lookup"><span data-stu-id="a31df-390">bool</span></span>|<span data-ttu-id="a31df-391">Compilación superficial o no</span><span class="sxs-lookup"><span data-stu-id="a31df-391">Shallow compile or not</span></span>|
|<span data-ttu-id="a31df-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="a31df-392">TempDir</span></span>|<span data-ttu-id="a31df-393">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-393">string</span></span>|<span data-ttu-id="a31df-394">Directorio temporal</span><span class="sxs-lookup"><span data-stu-id="a31df-394">Temp directory</span></span>|
|<span data-ttu-id="a31df-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="a31df-395">UseDataBase</span></span>|<span data-ttu-id="a31df-396">cadena</span><span class="sxs-lookup"><span data-stu-id="a31df-396">string</span></span>|<span data-ttu-id="a31df-397">Especificar hello toouse de base de datos para el código subyacente de registro del ensamblado temporal, maestro de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="a31df-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="a31df-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="a31df-398">WorkDir</span></span>|<span data-ttu-id="a31df-399">string</span><span class="sxs-lookup"><span data-stu-id="a31df-399">string</span></span>|<span data-ttu-id="a31df-400">Directorio de trabajo preferido</span><span class="sxs-lookup"><span data-stu-id="a31df-400">Preferred working directory</span></span>|


<span data-ttu-id="a31df-401">**Método**</span><span class="sxs-lookup"><span data-stu-id="a31df-401">**Method**</span></span>

|<span data-ttu-id="a31df-402">Método</span><span class="sxs-lookup"><span data-stu-id="a31df-402">Method</span></span>|<span data-ttu-id="a31df-403">Descripción</span><span class="sxs-lookup"><span data-stu-id="a31df-403">Description</span></span>|<span data-ttu-id="a31df-404">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="a31df-404">Return</span></span>|<span data-ttu-id="a31df-405">Parámetro</span><span class="sxs-lookup"><span data-stu-id="a31df-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="a31df-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="a31df-406">public bool DoCompile()</span></span>|<span data-ttu-id="a31df-407">Compilar el script de Hola U-SQL</span><span class="sxs-lookup"><span data-stu-id="a31df-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="a31df-408">Si se realiza correctamente, devuelve True.</span><span class="sxs-lookup"><span data-stu-id="a31df-408">True on success</span></span>| |
|<span data-ttu-id="a31df-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="a31df-409">public bool DoExec()</span></span>|<span data-ttu-id="a31df-410">Ejecutar el resultado de hello compilado</span><span class="sxs-lookup"><span data-stu-id="a31df-410">Execute hello compiled result</span></span>|<span data-ttu-id="a31df-411">Si se realiza correctamente, devuelve True.</span><span class="sxs-lookup"><span data-stu-id="a31df-411">True on success</span></span>| |
|<span data-ttu-id="a31df-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="a31df-412">public bool DoRun()</span></span>|<span data-ttu-id="a31df-413">Ejecutar script de Hola U-SQL (compilación + Execute)</span><span class="sxs-lookup"><span data-stu-id="a31df-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="a31df-414">Si se realiza correctamente, devuelve True.</span><span class="sxs-lookup"><span data-stu-id="a31df-414">True on success</span></span>| |
|<span data-ttu-id="a31df-415">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="a31df-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="a31df-416">Comprobar si Hola ruta de acceso dada es la ruta de acceso válida en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="a31df-417">True para válida</span><span class="sxs-lookup"><span data-stu-id="a31df-417">True for valid</span></span>|<span data-ttu-id="a31df-418">ruta de acceso de Hello del directorio en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="a31df-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="a31df-419">Preguntas más frecuentes sobre problemas comunes</span><span class="sxs-lookup"><span data-stu-id="a31df-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="a31df-420">Error 1:</span><span class="sxs-lookup"><span data-stu-id="a31df-420">Error 1:</span></span>
<span data-ttu-id="a31df-421">E_CSC_SYSTEM_INTERNAL: Error interno.</span><span class="sxs-lookup"><span data-stu-id="a31df-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="a31df-422">No se pudo cargar el archivo o ensamblado 'ScopeEngineManaged.dll' ni una de sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="a31df-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="a31df-423">no se pudo encontrar el módulo especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="a31df-423">hello specified module could not be found.</span></span>

<span data-ttu-id="a31df-424">Consulte el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="a31df-424">Please check hello following:</span></span>

- <span data-ttu-id="a31df-425">Asegúrese de que tiene un entorno x64.</span><span class="sxs-lookup"><span data-stu-id="a31df-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="a31df-426">plataforma de destino de compilación de Hola y el entorno de prueba de hello debe ser x64, consulte demasiado**paso 1: prueba unitaria de C# crear proyecto y configuración** anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a31df-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="a31df-427">Asegúrese de que ha copiado todos los archivos de dependencia en el directorio de trabajo de NugetPackage\build\runtime\ tooproject.</span><span class="sxs-lookup"><span data-stu-id="a31df-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a31df-428">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a31df-428">Next steps</span></span>

* <span data-ttu-id="a31df-429">toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a31df-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="a31df-430">información de diagnóstico de toolog, consulte [acceso a registros de diagnóstico para el análisis de Azure Data Lake](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a31df-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="a31df-431">toosee una consulta más compleja, vea [analizar registros de sitio Web mediante el análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="a31df-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a31df-432">Ver detalles del trabajo tooview, [utilizar un trabajo del explorador y la vista de trabajos de trabajos de análisis de Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a31df-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="a31df-433">vista de ejecución de toouse Hola vértices, consulte [Hola Use vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="a31df-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
