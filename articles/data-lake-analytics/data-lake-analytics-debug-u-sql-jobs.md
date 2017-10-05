---
title: "Depuración de trabajos U-SQL | Microsoft Docs"
description: "Obtenga información sobre cómo depurar vértices U-SQL con error mediante Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="b77a5-103">Depuración de código C# definido por el usuario para trabajos de U-SQL con errores</span><span class="sxs-lookup"><span data-stu-id="b77a5-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="b77a5-104">U-SQL proporciona un modelo de extensibilidad con C#, por lo que puede escribir el código para agregar funcionalidad, como un extractor o reductor personalizados.</span><span class="sxs-lookup"><span data-stu-id="b77a5-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="b77a5-105">Para más información, vea [Guía de programación de U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="b77a5-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="b77a5-106">En la práctica, puede que un código necesite depuración y los sistemas de macrodatos solo pueden proporcionar información limitada de depuración de tiempo de ejecución, como los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="b77a5-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="b77a5-107">Herramientas de Azure Data Lake para Visual Studio proporciona una característica denominada **Depuración de vértice con errores**, que le permite clonar un trabajo erróneo de la nube a la máquina local para la depuración.</span><span class="sxs-lookup"><span data-stu-id="b77a5-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="b77a5-108">El clon local captura todo el entorno en la nube, incluidos el código de usuario y los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="b77a5-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="b77a5-109">En el siguiente vídeo se demuestra la depuración de vértice con errores en las Herramientas de Azure Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b77a5-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="b77a5-110">Visual Studio requiere las siguientes dos actualizaciones, si no están ya instaladas: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) y [Universal C Runtime en Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="b77a5-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="b77a5-111">Error al descargar el vértice en la máquina local</span><span class="sxs-lookup"><span data-stu-id="b77a5-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="b77a5-112">Al abrir un trabajo erróneo en Herramientas de Azure Data Lake para Visual Studio, verá una barra de alerta amarilla con mensajes de error detallados en la pestaña Error.</span><span class="sxs-lookup"><span data-stu-id="b77a5-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="b77a5-113">Haga clic en **Descargar** para descargar todos los flujos de entrada y recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="b77a5-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="b77a5-114">Si la descarga no se completa, haga clic en **Reintentar**.</span><span class="sxs-lookup"><span data-stu-id="b77a5-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="b77a5-115">Haga clic en **Abrir** después de que finalice la descarga para generar el entorno de depuración local.</span><span class="sxs-lookup"><span data-stu-id="b77a5-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="b77a5-116">Se creará y abrirá automáticamente una nueva instancia de Visual Studio con una solución de depuración.</span><span class="sxs-lookup"><span data-stu-id="b77a5-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Descarga de vértices para depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="b77a5-118">Los trabajos pueden incluir archivos de origen con código subyacente o ensamblados registrados, y estos dos tipos tienen escenarios de depuración diferentes.</span><span class="sxs-lookup"><span data-stu-id="b77a5-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="b77a5-119">Depuración de un trabajo con error con código subyacente</span><span class="sxs-lookup"><span data-stu-id="b77a5-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="b77a5-120">Depuración de un trabajo con error con ensamblados</span><span class="sxs-lookup"><span data-stu-id="b77a5-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="b77a5-121">Depuración de un trabajo con error con código subyacente</span><span class="sxs-lookup"><span data-stu-id="b77a5-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="b77a5-122">Si se produce un error del trabajo U-SQL (normalmente denominado `Script.usql.cs` en un proyecto U-SQL), el código fuente se importa en la solución de depuración.</span><span class="sxs-lookup"><span data-stu-id="b77a5-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="b77a5-123">Desde aquí, puede usar las herramientas de depuración de Visual Studio (visualización, variables, etc.) para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="b77a5-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b77a5-124">Antes de realizar la depuración, asegúrese de que ha activado **Common Language Runtime Exceptions** (Excepciones de Common Language Runtime) en la ventana de configuración de excepciones (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="b77a5-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Configuración de depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="b77a5-126">Pulse **F5** para ejecutar el código subyacente.</span><span class="sxs-lookup"><span data-stu-id="b77a5-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="b77a5-127">Se ejecutará hasta que una excepción lo detenga.</span><span class="sxs-lookup"><span data-stu-id="b77a5-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="b77a5-128">Abra el archivo `ADLTool_Codebehind.usql.cs` y establezca los puntos de interrupción. A continuación, pulse **F5** para depurar el código paso por paso.</span><span class="sxs-lookup"><span data-stu-id="b77a5-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Excepción de depuración de U-SQL de Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="b77a5-130">Error de depuración del trabajo con ensamblados</span><span class="sxs-lookup"><span data-stu-id="b77a5-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="b77a5-131">Si utiliza ensamblados registrados en el script de U-SQL, el sistema no puede obtener el código fuente automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b77a5-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="b77a5-132">En este caso, agregue manualmente los archivos de código fuente de los ensamblados a la solución.</span><span class="sxs-lookup"><span data-stu-id="b77a5-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="b77a5-133">Configuración de la solución</span><span class="sxs-lookup"><span data-stu-id="b77a5-133">Configure the solution</span></span>

1. <span data-ttu-id="b77a5-134">Haga clic con el botón derecho en **Solution 'VertexDebug' > Add > Existing Project...** (Solución 'VertexDebug' > Agregar > proyecto existente) para buscar el código fuente de los ensamblados y agregar el proyecto a la solución de depuración.</span><span class="sxs-lookup"><span data-stu-id="b77a5-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Depuración de U-SQL de Azure Data Lake Analytics: agregar proyecto](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="b77a5-136">Haga clic con el botón derecho en **LocalVertexHost > Properties** (Propiedades) en la solución y copie la ruta del **directorio de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="b77a5-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="b77a5-137">Haga clic con el botón derecho en el **proyecto de código fuente del ensamblado > Properties** (Propiedades), seleccione la pestaña **Build** (Recompilar) a la izquierda y pegue la ruta de acceso en **Output > Output path** (Salida > Ruta de salida).</span><span class="sxs-lookup"><span data-stu-id="b77a5-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Depuración de U-SQL de Azure Data Lake Analytics: definición de la ruta de acceso de pdb](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="b77a5-139">Presione **Ctrl + Alt + E** y marque **Common Language Runtime Exceptions** (Excepciones de Common Language Runtime) en la ventana de configuración de excepciones.</span><span class="sxs-lookup"><span data-stu-id="b77a5-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="b77a5-140">Inicio de la depuración</span><span class="sxs-lookup"><span data-stu-id="b77a5-140">Start debug</span></span>

1. <span data-ttu-id="b77a5-141">Haga clic con el botón derecho en el **proyecto de código fuente de ensamblado > Rebuild** (Recompilar) para enviar los archivos .pdb de salida al directorio de trabajo de `LocalVertexHost`.</span><span class="sxs-lookup"><span data-stu-id="b77a5-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="b77a5-142">Presione **F5** y el proyecto se ejecutará e hasta que se detenga debido a una excepción.</span><span class="sxs-lookup"><span data-stu-id="b77a5-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="b77a5-143">Es posible que vea el siguiente mensaje de advertencia, del que puede hacer caso omiso sin problemas.</span><span class="sxs-lookup"><span data-stu-id="b77a5-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="b77a5-144">La pantalla de depuración puede tardar en mostrarse hasta un minuto.</span><span class="sxs-lookup"><span data-stu-id="b77a5-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Advertencia de depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="b77a5-146">Abra el código fuente y establezca los puntos de interrupción; a continuación, pulse **F5** para depurar el código paso a paso.</span><span class="sxs-lookup"><span data-stu-id="b77a5-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="b77a5-147">También puede usar las herramientas de depuración de Visual Studio (visualización, variables, etc.) para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="b77a5-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b77a5-148">Recompile el proyecto de código fuente de ensamblado cada vez que modifique el código para generar archivos .pdb actualizados.</span><span class="sxs-lookup"><span data-stu-id="b77a5-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="b77a5-149">Tras la depuración, si el proyecto se completa correctamente, la ventana de salida muestra el siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="b77a5-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL debug succeed (La depuración de U-SQL de Azure Data Lake Analytics se realizó correctamente)](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="b77a5-151">Reenviar el trabajo</span><span class="sxs-lookup"><span data-stu-id="b77a5-151">Resubmit the job</span></span>

<span data-ttu-id="b77a5-152">Cuando haya terminado la depuración, vuelva a enviar el trabajo con error.</span><span class="sxs-lookup"><span data-stu-id="b77a5-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="b77a5-153">Para los trabajos con soluciones con código subyacente, copie el código de C# en el archivo de origen de código subyacente (normalmente, `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="b77a5-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="b77a5-154">Para los trabajos con ensamblados, registre los ensamblados .dll actualizados en la base de datos ADLA:</span><span class="sxs-lookup"><span data-stu-id="b77a5-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="b77a5-155">Desde el Explorador de servidores o Cloud Explorer, expanda el nodo **ADLA account > Databases** (Cuenta de ADLA > Bases de datos).</span><span class="sxs-lookup"><span data-stu-id="b77a5-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="b77a5-156">Haga clic con el botón derecho en **Ensamblados** y registre los nuevos ensamblados .dll con la base de datos ADLA: ![Ensamblado de registro de depuración de U-SQL de Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="b77a5-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="b77a5-157">Vuelva a enviar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="b77a5-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b77a5-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b77a5-158">Next steps</span></span>

- [<span data-ttu-id="b77a5-159">Guía de programación de U-SQL</span><span class="sxs-lookup"><span data-stu-id="b77a5-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="b77a5-160">Desarrollo de operadores U-SQL definidos por el usuario para trabajos de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b77a5-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="b77a5-161">Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b77a5-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
