---
title: trabajos de aaaDebug U-SQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodebug U-SQL no pudo vértices con Visual Studio."
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
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="4413f-103">Depuración de código C# definido por el usuario para trabajos de U-SQL con errores</span><span class="sxs-lookup"><span data-stu-id="4413f-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="4413f-104">U-SQL proporciona un modelo de extensibilidad con C#, por lo que puede escribir la funcionalidad de tooadd de código como un extractor personalizado o reductor.</span><span class="sxs-lookup"><span data-stu-id="4413f-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="4413f-105">más información, consulte toolearn [Guía de programación de SQL U](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="4413f-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="4413f-106">En la práctica, puede que un código necesite depuración y los sistemas de macrodatos solo pueden proporcionar información limitada de depuración de tiempo de ejecución, como los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="4413f-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="4413f-107">Azure Data Lake Tools para Visual Studio incluye una característica denominada **no se pudo depurar vértices**, lo que le permite clonar un trabajo con error desde el equipo local tooyour de hello en la nube para la depuración.</span><span class="sxs-lookup"><span data-stu-id="4413f-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="4413f-108">clon local Hola captura entorno de nube todo hello, incluidos los datos de entrada y el código de usuario.</span><span class="sxs-lookup"><span data-stu-id="4413f-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="4413f-109">Hello vídeo siguiente muestra no se pudo depurar vértices en Azure Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4413f-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="4413f-110">Visual Studio requiere Hola siguiendo dos actualizaciones si no están ya instalados: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) y [Universal en tiempo de ejecución de C para Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="4413f-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="4413f-111">Error al descargar el vértice toolocal máquina</span><span class="sxs-lookup"><span data-stu-id="4413f-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="4413f-112">Al abrir un trabajo con error en Azure Data Lake Tools para Visual Studio, verá una barra amarilla de alerta con mensajes de error detallados en la ficha de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="4413f-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="4413f-113">Haga clic en **descargar** necesarios de toodownload Hola a todos los recursos y los flujos de entrada.</span><span class="sxs-lookup"><span data-stu-id="4413f-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="4413f-114">Si no completa la descarga de hello, haga clic en **vuelva a intentar**.</span><span class="sxs-lookup"><span data-stu-id="4413f-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="4413f-115">Haga clic en **abiertos** al finalizar la descarga de hello toogenerate un entorno de depuración local.</span><span class="sxs-lookup"><span data-stu-id="4413f-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="4413f-116">Se creará y abrirá automáticamente una nueva instancia de Visual Studio con una solución de depuración.</span><span class="sxs-lookup"><span data-stu-id="4413f-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Descarga de vértices para depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="4413f-118">Los trabajos pueden incluir archivos de origen con código subyacente o ensamblados registrados, y estos dos tipos tienen escenarios de depuración diferentes.</span><span class="sxs-lookup"><span data-stu-id="4413f-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="4413f-119">Depuración de un trabajo con error con código subyacente</span><span class="sxs-lookup"><span data-stu-id="4413f-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="4413f-120">Depuración de un trabajo con error con ensamblados</span><span class="sxs-lookup"><span data-stu-id="4413f-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="4413f-121">Depuración de un trabajo con error con código subyacente</span><span class="sxs-lookup"><span data-stu-id="4413f-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="4413f-122">Si se produce un error en un trabajo de SQL de U y trabajo Hola incluye código de usuario (normalmente denominado `Script.usql.cs` en un proyecto de SQL U), que el código fuente se importa en hello depurar la solución.</span><span class="sxs-lookup"><span data-stu-id="4413f-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="4413f-123">Desde allí puede usar problema de hello Visual Studio depuración herramientas (inspección, variables, etc.) tootroubleshoot Hola.</span><span class="sxs-lookup"><span data-stu-id="4413f-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="4413f-124">Antes de depurar, ser seguro toocheck **excepciones de Common Language Runtime** en la ventana de configuración de excepciones de hello (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="4413f-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Configuración de depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="4413f-126">Presione **F5** código subyacente de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="4413f-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="4413f-127">Se ejecutará hasta que una excepción lo detenga.</span><span class="sxs-lookup"><span data-stu-id="4413f-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="4413f-128">Abra hello `ADLTool_Codebehind.usql.cs` de archivos y establecer puntos de interrupción, a continuación, presione **F5** código de hello toodebug paso a paso.</span><span class="sxs-lookup"><span data-stu-id="4413f-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Excepción de depuración de U-SQL de Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="4413f-130">Error de depuración del trabajo con ensamblados</span><span class="sxs-lookup"><span data-stu-id="4413f-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="4413f-131">Si utiliza ensamblados registrados en el script U-SQL, sistema de hello no puede obtener código de hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4413f-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="4413f-132">En este caso, agregue manualmente origen código archivos toohello solución los ensamblados Hola.</span><span class="sxs-lookup"><span data-stu-id="4413f-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="4413f-133">Configurar la solución de Hola</span><span class="sxs-lookup"><span data-stu-id="4413f-133">Configure hello solution</span></span>

1. <span data-ttu-id="4413f-134">Haga clic en **solución 'VertexDebug' > Agregar > proyecto existente...**  toofind Hola código de origen de ensamblados y agregue Hola proyecto toohello depurar la solución.</span><span class="sxs-lookup"><span data-stu-id="4413f-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Depuración de U-SQL de Azure Data Lake Analytics: agregar proyecto](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="4413f-136">Haga clic en **LocalVertexHost > propiedades** Hola Hola de soluciones y copie **Working Directory** ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="4413f-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="4413f-137">Haga clic en **proyecto de código fuente de ensamblado > propiedades**, seleccione hello **generar** ficha a la izquierda y pegue Hola Copiar ruta de acceso como **salida > ruta de acceso de salida**.</span><span class="sxs-lookup"><span data-stu-id="4413f-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Depuración de U-SQL de Azure Data Lake Analytics: definición de la ruta de acceso de pdb](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="4413f-139">Presione **Ctrl + Alt + E** y marque **Common Language Runtime Exceptions** (Excepciones de Common Language Runtime) en la ventana de configuración de excepciones.</span><span class="sxs-lookup"><span data-stu-id="4413f-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="4413f-140">Inicio de la depuración</span><span class="sxs-lookup"><span data-stu-id="4413f-140">Start debug</span></span>

1. <span data-ttu-id="4413f-141">Haga clic en **proyecto de código fuente de ensamblado > volver a generar** toohello los archivos .pdb toooutput `LocalVertexHost` directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4413f-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="4413f-142">Presione **F5** y proyecto de Hola se ejecutará hasta que se detiene debido a una excepción.</span><span class="sxs-lookup"><span data-stu-id="4413f-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="4413f-143">Es posible que vea Hola siguiente mensaje de advertencia, que se puede omitir con seguridad.</span><span class="sxs-lookup"><span data-stu-id="4413f-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="4413f-144">Puede tardar tooa tooget minuto toohello depuración pantalla hacia arriba.</span><span class="sxs-lookup"><span data-stu-id="4413f-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Advertencia de depuración de trabajos U-SQL de Azure Data Lake Analytics en Visual Studio](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="4413f-146">Abra el código fuente y establecer puntos de interrupción, a continuación, presione **F5** código de hello toodebug paso a paso.</span><span class="sxs-lookup"><span data-stu-id="4413f-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="4413f-147">También puede utilizar el problema de hello Visual Studio depuración herramientas (inspección, variables, etc.) tootroubleshoot Hola.</span><span class="sxs-lookup"><span data-stu-id="4413f-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="4413f-148">Vuelva a generar proyecto de código fuente de hello ensamblado cada vez después de modificar toogenerate actualizar código de hello, .pdb (archivos).</span><span class="sxs-lookup"><span data-stu-id="4413f-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="4413f-149">Tras la depuración, si se completa correctamente el proyecto de hello ventana de salida de hello muestra hello siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="4413f-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL debug succeed (La depuración de U-SQL de Azure Data Lake Analytics se realizó correctamente)](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="4413f-151">Vuelva a enviar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="4413f-151">Resubmit hello job</span></span>

<span data-ttu-id="4413f-152">Una vez haya completado la depuración, vuelva a enviar Hola trabajo con errores.</span><span class="sxs-lookup"><span data-stu-id="4413f-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="4413f-153">Para los trabajos con soluciones de código subyacente, copie el código de C# en el archivo de código fuente del código subyacente de hello (normalmente `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="4413f-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="4413f-154">Para los trabajos con ensamblados, registre los ensamblados .dll Hola actualizado en la base de datos ADLA:</span><span class="sxs-lookup"><span data-stu-id="4413f-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="4413f-155">Desde el Explorador de servidores o el explorador en la nube, expanda hello **cuenta ADLA > bases de datos** nodo.</span><span class="sxs-lookup"><span data-stu-id="4413f-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="4413f-156">Haga clic en **ensamblados** y registrar los ensamblados .dll nuevo con la base de datos de Hola ADLA: ![depuración de Azure Data Lake Analytics U-SQL registrar ensamblados](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="4413f-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="4413f-157">Vuelva a enviar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4413f-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4413f-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4413f-158">Next steps</span></span>

- [<span data-ttu-id="4413f-159">Guía de programación de U-SQL</span><span class="sxs-lookup"><span data-stu-id="4413f-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="4413f-160">Desarrollo de operadores U-SQL definidos por el usuario para trabajos de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4413f-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="4413f-161">Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4413f-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
