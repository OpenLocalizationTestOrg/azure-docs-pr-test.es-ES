---
title: "Herramientas de Azure Data Lake: Ejecución y depuración locales de U-SQL con Visual Studio Code | Microsoft Docs"
description: "Obtenga información sobre cómo usar Herramientas de Azure Data Lake para Visual Studio Code para la ejecución y depuración locales."
Keywords: "VSCode, Herramientas de Azure Data Lake, ejecución local, depuración local, archivo de almacenamiento de versión preliminar, cargar en la ruta de acceso de almacenamiento"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 367e4ba792f83d6ee246208306e4c09b69cb49ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="3a5aa-104">Ejecución y depuración locales de U-SQL con Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3a5aa-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a5aa-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3a5aa-105">Prerequisites</span></span>
<span data-ttu-id="3a5aa-106">Asegúrese de que tiene implementados los requisitos previos siguientes antes de comenzar con estos procedimientos:</span><span class="sxs-lookup"><span data-stu-id="3a5aa-106">Make sure you have the following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="3a5aa-107">Herramientas de Azure Data Lake para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="3a5aa-108">Para instrucciones, consulte [Uso de Herramientas de Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="3a5aa-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="3a5aa-109">C# para Visual Studio Code (si desea realizar la depuración local de U-SQL).</span><span class="sxs-lookup"><span data-stu-id="3a5aa-109">C# for Visual Studio Code (if you want to perform a U-SQL local debug).</span></span>

   ![Instalación de C# en Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="3a5aa-111">Las características de ejecución y depuración locales de U-SQL solo admiten actualmente usuarios de Windows.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-111">The U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-the-u-sql-local-run-environment"></a><span data-ttu-id="3a5aa-112">Configuración del entorno de ejecución local de U-SQL</span><span class="sxs-lookup"><span data-stu-id="3a5aa-112">Set up the U-SQL local run environment</span></span>

1. <span data-ttu-id="3a5aa-113">Seleccione Ctrl+Mayús+P para abrir la paleta de comandos y, luego, escriba **ADL: Download LocalRun Dependency** para descargar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-113">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Download LocalRun Dependency** to download the packages.</span></span>  

   ![Descarga de los paquetes de dependencia de ADL LocalRun](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="3a5aa-115">Busque los paquetes de dependencia de la ruta de acceso que se muestra en el panel **Salida** y, luego, instale BuildTools y Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-115">Locate the dependency packages from the path shown in the **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="3a5aa-116">A continuación se muestra una ruta de acceso de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3a5aa-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="3a5aa-117">![Ubicación de los paquetes de dependencia](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="3a5aa-117">![Locate the dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="3a5aa-118">a.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-118">a.</span></span> <span data-ttu-id="3a5aa-119">Para instalar BuildTools, siga las instrucciones del asistente.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-119">To install BuildTools, follow the wizard instructions.</span></span>   

  ![Instalación de BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="3a5aa-121">b.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-121">b.</span></span> <span data-ttu-id="3a5aa-122">Para instalar Win10SDK 10240, siga las instrucciones del asistente.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-122">To install Win10SDK 10240, follow the wizard instructions.</span></span>  

  ![Instalación de Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="3a5aa-124">Configure la variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-124">Set up the environment variable.</span></span> <span data-ttu-id="3a5aa-125">Establezca la variable de entorno **SCOPE_CPP_SDK** en:</span><span class="sxs-lookup"><span data-stu-id="3a5aa-125">Set the **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="3a5aa-126">Reinicie el SO para asegurarse de que la configuración de la variable de entorno surta efecto.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-126">Restart the OS to make sure that the environment variable settings take effect.</span></span>  

   ![Asegúrese de que la variable de entorno SCOPE_CPP_SDK está instalada](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-the-local-run-service-and-submit-the-u-sql-job-to-a-local-account"></a><span data-ttu-id="3a5aa-128">Inicio del servicio de ejecución local y envío del trabajo de U-SQL a la cuenta local</span><span class="sxs-lookup"><span data-stu-id="3a5aa-128">Start the local run service and submit the U-SQL job to a local account</span></span> 
<span data-ttu-id="3a5aa-129">Para los usuarios nuevos, se le pedirá descargar los paquetes de dependencia ADL: Download LocalRun si todavía no está instalados.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-129">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="3a5aa-130">Seleccione Ctrl+Mayús+P para abrir la paleta de comandos y, luego, escribir **ADL: Start Local Run Service**.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-130">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="3a5aa-131">Seleccione **Aceptar** para aceptar los Términos de licencia del software de Microsoft por primera vez.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-131">Select **Accept** to accept the Microsoft Software License Terms for the first time.</span></span> 

   ![Aceptación de los Términos de licencia del software de Microsoft](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="3a5aa-133">Se abre la consola cmd.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-133">The cmd console opens.</span></span> <span data-ttu-id="3a5aa-134">Para los usuarios nuevos, tiene que especificar **3** y asignar la ruta de acceso a la carpeta local para la entrada y salida de datos.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-134">For first-time users, you need to enter **3**, and then locate the local folder path for your data input and output.</span></span> <span data-ttu-id="3a5aa-135">Para otras opciones, puede usar los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-135">For other options, you can use the default values.</span></span> 

   ![Cmd de ejecución local de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="3a5aa-137">Seleccione Ctrl+Mayús+P para abrir la paleta de comandos, escriba **ADL: Submit Job** y, luego, seleccione **Local** para enviar el trabajo a la cuenta local.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-137">Select Ctrl+Shift+P to open the command palette, enter **ADL: Submit Job**, and then select **Local** to submit the job to your local account.</span></span>

   ![Selección local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="3a5aa-139">Una vez que envía el trabajo, puede ver los detalles del envío.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-139">After you submit the job, you can view the submission details.</span></span> <span data-ttu-id="3a5aa-140">Para hacerlo, seleccione **jobUrl** en la ventana **Salida**.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-140">To view the submission details select **jobUrl** in the **Output** window.</span></span> <span data-ttu-id="3a5aa-141">También puede ver el estado de envío del trabajo en la consola cmd.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-141">You can also view the job submission status from the cmd console.</span></span> <span data-ttu-id="3a5aa-142">Escriba **7** en la consola cmd si desea más información sobre los detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-142">Enter **7** in the cmd console if you want to know more job details.</span></span>

   <span data-ttu-id="3a5aa-143">![Salida d ejecución local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Herramientas de Data Lake para el estado de cmd de ejecución local de Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="3a5aa-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-the-u-sql-job"></a><span data-ttu-id="3a5aa-144">Inicio de una depuración local para el trabajo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="3a5aa-144">Start a local debug for the U-SQL job</span></span>  
<span data-ttu-id="3a5aa-145">Para los usuarios nuevos, se le pedirá descargar los paquetes de dependencia ADL: Download LocalRun si todavía no está instalados.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-145">For the first-time user, you are prompted to download the ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="3a5aa-146">Seleccione Ctrl+Mayús+P para abrir la paleta de comandos y, luego, escribir **ADL: Start Local Run Service**.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-146">Select Ctrl+Shift+P to open the command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="3a5aa-147">Se abre la consola cmd.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-147">The cmd console opens.</span></span> <span data-ttu-id="3a5aa-148">Asegúrese de que se establece **DataRoot**.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-148">Make sure that the **DataRoot** is set.</span></span>
3. <span data-ttu-id="3a5aa-149">Establezca un punto de interrupción en el código subyacente de C#.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="3a5aa-150">Vuelva al editor de scripts, seleccione Ctrl+Mayús+P para abrir la consola de comandos y, luego, escriba **Depuración local** para iniciar el servicio de depuración local.</span><span class="sxs-lookup"><span data-stu-id="3a5aa-150">Back in the script editor, select Ctrl+Shift+P to open the command console, and then enter **Local Debug** to start your local debug service.</span></span>

![Resultado de la depuración local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="3a5aa-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a5aa-152">Next steps</span></span>
- <span data-ttu-id="3a5aa-153">Para usar Herramientas de Azure Data Lake para Visual Studio, consulte [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md) (Uso de Herramientas de Azure Data Lake para Visual Studio Code).</span><span class="sxs-lookup"><span data-stu-id="3a5aa-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="3a5aa-154">Para información detallada sobre cómo empezar a trabajar con Data Lake Analytics, consulte [Tutorial: Introducción a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3a5aa-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="3a5aa-155">Para información sobre Herramientas de Data Lake para Visual Studio, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Herramientas de Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3a5aa-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="3a5aa-156">Para obtener información sobre el desarrollo de ensamblados, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="3a5aa-156">For the information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
