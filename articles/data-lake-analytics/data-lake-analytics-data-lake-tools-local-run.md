---
title: "aaaTest y depuración SQL U trabajos mediante el uso locales ejecutar y Hola SDK de Azure datos Lake U-SQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure Data Lake Tools para Visual Studio y tootest del SDK de SQL Azure datos Lake U hello y depuración SQL U trabajos en la estación de trabajo local."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="ebfce-103">Probar y depurar los trabajos de SQL U mediante local ejecutar y Hola SDK de SQL Azure datos Lake U</span><span class="sxs-lookup"><span data-stu-id="ebfce-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="ebfce-104">Puede usar Azure Data Lake Tools para Visual Studio y trabajos de hello SDK de Azure datos Lake U-SQL toorun U-SQL en la estación de trabajo, igual que lo haría en el servicio de Azure Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfce-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="ebfce-105">Estas dos características de ejecución local ahorran tiempo para probar y depurar los trabajos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfce-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="ebfce-106">Comprender la carpeta de datos raíz de Hola y ruta de acceso de archivo de Hola</span><span class="sxs-lookup"><span data-stu-id="ebfce-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="ebfce-107">Ejecución local y hello U-SQL SDK requieren una carpeta raíz de datos.</span><span class="sxs-lookup"><span data-stu-id="ebfce-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="ebfce-108">carpeta de datos raíz de Hello es un "almacén local" para la cuenta de proceso local Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfce-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="ebfce-109">Es la cuenta de almacén de Azure Data Lake toohello equivalente de una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ebfce-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="ebfce-110">Cambiar tooa carpeta raíz de datos diferentes es igual que cambiar la cuenta de otro almacén de tooa.</span><span class="sxs-lookup"><span data-stu-id="ebfce-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="ebfce-111">Si desea tooaccess comúnmente suelen compartir datos con las carpetas raíz de datos diferente, debe usar rutas de acceso absolutas en las secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="ebfce-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="ebfce-112">O bien, crear vínculos simbólicos de sistema de archivos (por ejemplo, **mklink** en NTFS) en la carpeta toopoint toohello de hello raíz de datos de los datos compartidos.</span><span class="sxs-lookup"><span data-stu-id="ebfce-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="ebfce-113">carpeta de datos raíz de Hola se utiliza para:</span><span class="sxs-lookup"><span data-stu-id="ebfce-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="ebfce-114">Almacenar metadatos, lo que incluye bases de datos, tablas, funciones con valores de tabla (TVF) y ensamblados.</span><span class="sxs-lookup"><span data-stu-id="ebfce-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="ebfce-115">Buscar Hola de entrada y las rutas de acceso de salida que se definen como rutas de acceso relativas en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfce-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="ebfce-116">Usar rutas de acceso relativas resulta más fácil toodeploy su tooAzure de proyectos U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfce-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="ebfce-117">Puede usar tanto una ruta de acceso relativa como una ruta de acceso absoluta local en los scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfce-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="ebfce-118">ruta de acceso relativa de Hello es relativa toohello ruta de la carpeta de raíz de datos especificado.</span><span class="sxs-lookup"><span data-stu-id="ebfce-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="ebfce-119">Se recomienda que se utilice "/" como Hola toomake de separador de ruta de acceso las secuencias de comandos compatibles con el lado del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfce-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="ebfce-120">Estos son algunos ejemplos de rutas de acceso relativas y sus rutas de acceso absolutas equivalentes.</span><span class="sxs-lookup"><span data-stu-id="ebfce-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="ebfce-121">En estos ejemplos, C:\LocalRunDataRoot es la carpeta de datos raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfce-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="ebfce-122">Ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="ebfce-122">Relative path</span></span>|<span data-ttu-id="ebfce-123">Ruta de acceso absoluta</span><span class="sxs-lookup"><span data-stu-id="ebfce-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="ebfce-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="ebfce-124">/abc/def/input.csv</span></span> |<span data-ttu-id="ebfce-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="ebfce-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="ebfce-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="ebfce-126">abc/def/input.csv</span></span>  |<span data-ttu-id="ebfce-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="ebfce-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="ebfce-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="ebfce-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="ebfce-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="ebfce-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="ebfce-130">Uso de ejecución local desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebfce-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="ebfce-131">Data Lake Tools para Visual Studio proporciona la experiencia de ejecución local de U-SQL en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebfce-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="ebfce-132">Con esta característica, puede:</span><span class="sxs-lookup"><span data-stu-id="ebfce-132">By using this feature, you can:</span></span>

- <span data-ttu-id="ebfce-133">Ejecutar scripts U-SQL localmente, junto con los ensamblados de C#.</span><span class="sxs-lookup"><span data-stu-id="ebfce-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="ebfce-134">Depurar un ensamblado de C# localmente.</span><span class="sxs-lookup"><span data-stu-id="ebfce-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="ebfce-135">Crear, ver y eliminar catálogos de U-SQL (bases de datos locales, ensamblados, esquemas y tablas) desde el Explorador de servidores.</span><span class="sxs-lookup"><span data-stu-id="ebfce-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="ebfce-136">También puede encontrar el catálogo local hello también desde el Explorador de servidores.</span><span class="sxs-lookup"><span data-stu-id="ebfce-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Catálogo local de ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="ebfce-138">instalador de Data Lake Tools Hola crea un toobe de carpeta C:\LocalRunRoot utilizado como carpeta raíz de datos predeterminada del saludo.</span><span class="sxs-lookup"><span data-stu-id="ebfce-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="ebfce-139">paralelismo de ejecución local de Hello predeterminado es 1.</span><span class="sxs-lookup"><span data-stu-id="ebfce-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="ebfce-140">tooconfigure local se ejecuta en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebfce-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="ebfce-141">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebfce-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="ebfce-142">Abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="ebfce-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="ebfce-143">Expanda **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ebfce-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="ebfce-144">Haga clic en hello **Data Lake** menú y, a continuación, haga clic en **opciones y configuración**.</span><span class="sxs-lookup"><span data-stu-id="ebfce-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="ebfce-145">En el árbol de la izquierda hello, expanda **Azure Data Lake**y, a continuación, expanda **General**.</span><span class="sxs-lookup"><span data-stu-id="ebfce-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Configuración de ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="ebfce-147">Se necesita un proyecto de U-SQL de Visual Studio para realizar la ejecución local.</span><span class="sxs-lookup"><span data-stu-id="ebfce-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="ebfce-148">Esta parte es diferente de la ejecución de scripts U-SQL desde Azure.</span><span class="sxs-lookup"><span data-stu-id="ebfce-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="ebfce-149">la secuencia de comandos de toorun un U-SQL localmente</span><span class="sxs-lookup"><span data-stu-id="ebfce-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="ebfce-150">En Visual Studio, abra el proyecto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfce-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="ebfce-151">Haga clic con el botón derecho en un script U-SQL en el Explorador de soluciones y después haga clic en **Submit Script** (Enviar script).</span><span class="sxs-lookup"><span data-stu-id="ebfce-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="ebfce-152">Seleccione **(Local)** hello análisis cuenta toorun localmente la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="ebfce-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="ebfce-153">También puede hacer clic en hello **(Local)** cuenta en la parte superior de Hola de ventana de script y, a continuación, haga clic en **enviar** (o utilice Hola Ctrl + método abreviado de teclado F5).</span><span class="sxs-lookup"><span data-stu-id="ebfce-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Trabajos de envío de ejecución local de Data Lake Tools para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="ebfce-155">Depurar scripts y ensamblados de C# localmente</span><span class="sxs-lookup"><span data-stu-id="ebfce-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="ebfce-156">Puede depurar los ensamblados de C# sin enviar y registrar tooAzure servicio de análisis de datos Lake.</span><span class="sxs-lookup"><span data-stu-id="ebfce-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="ebfce-157">Puede establecer puntos de interrupción en ambos Hola archivo de código subyacente y en un proyecto de C# que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="ebfce-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="ebfce-158">toodebug código local en el archivo de código subyacente</span><span class="sxs-lookup"><span data-stu-id="ebfce-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="ebfce-159">Establezca puntos de interrupción Hola archivo de código subyacente.</span><span class="sxs-lookup"><span data-stu-id="ebfce-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="ebfce-160">Presione F5 toodebug hello secuencia de comandos de forma local.</span><span class="sxs-lookup"><span data-stu-id="ebfce-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="ebfce-161">Hola siguiendo el procedimiento solo funciona en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ebfce-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="ebfce-162">En Visual Studio anterior puede ser necesario toomanually agregar archivos pdb de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfce-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="ebfce-163">toodebug código local en un proyecto de C# que se hace referencia</span><span class="sxs-lookup"><span data-stu-id="ebfce-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="ebfce-164">Crear un proyecto de ensamblado de C# y genérelo dll de salida de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="ebfce-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="ebfce-165">Registre la dll de hello mediante una instrucción SQL U:</span><span class="sxs-lookup"><span data-stu-id="ebfce-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="ebfce-166">Establecer puntos de interrupción en código C# Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfce-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="ebfce-167">Presione F5 toodebug hello secuencia de comandos que hacen referencia a la dll de hello C# localmente.</span><span class="sxs-lookup"><span data-stu-id="ebfce-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="ebfce-168">Usar local ejecutar de hello datos Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="ebfce-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="ebfce-169">Además de scripts toorunning U-SQL localmente mediante Visual Studio, puede usar secuencias de comandos de hello SDK de Azure datos Lake U-SQL toorun U-SQL localmente con interfaces de línea de comandos y programación.</span><span class="sxs-lookup"><span data-stu-id="ebfce-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="ebfce-170">A través de estos elementos, puede escalar la prueba local de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ebfce-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="ebfce-171">Obtenga más información sobre el [SDK de U-SQL para Azure Data Lake](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ebfce-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ebfce-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebfce-172">Next steps</span></span>

* <span data-ttu-id="ebfce-173">toosee una consulta más compleja, vea [analizar registros de sitio Web mediante el análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="ebfce-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="ebfce-174">Ver detalles del trabajo tooview, [utilizar un trabajo del explorador y la vista de trabajos de trabajos de análisis de Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="ebfce-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="ebfce-175">vista de ejecución de toouse Hola vértices, consulte [Hola Use vista de ejecución de vértices de Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="ebfce-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
