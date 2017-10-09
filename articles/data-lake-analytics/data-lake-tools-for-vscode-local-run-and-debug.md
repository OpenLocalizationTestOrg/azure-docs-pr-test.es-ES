---
title: "Herramientas de Azure Data Lake: Ejecución y depuración locales de U-SQL con Visual Studio Code | Microsoft Docs"
description: "Obtenga información acerca de cómo depurar toouse Azure Data Lake Tools para Visual Studio Code toolocal local y de ejecución."
Keywords: "Ruta de acceso de toostorage de carga de VScode, Azure Data Lake Tools, ejecución, depuración Local, depuración Local, archivo de almacenamiento de información de vista previa, Local"
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
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="d74fe-104">Ejecución y depuración locales de U-SQL con Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d74fe-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d74fe-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d74fe-105">Prerequisites</span></span>
<span data-ttu-id="d74fe-106">Asegúrese de que tiene Hola siguiendo los requisitos previos en su lugar antes de iniciar estos procedimientos:</span><span class="sxs-lookup"><span data-stu-id="d74fe-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="d74fe-107">Herramientas de Azure Data Lake para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d74fe-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="d74fe-108">Para instrucciones, consulte [Uso de Herramientas de Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="d74fe-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="d74fe-109">C# para código de Visual Studio (si quiere que la depuración local tooperform U-SQL).</span><span class="sxs-lookup"><span data-stu-id="d74fe-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Instalación de C# en Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="d74fe-111">Hola ejecución local de SQL de U y características de depuración solo admiten actualmente los usuarios de Windows.</span><span class="sxs-lookup"><span data-stu-id="d74fe-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="d74fe-112">Configurar el entorno de ejecución local de hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="d74fe-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="d74fe-113">Seleccione la paleta de comando de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **ADL: Descargar LocalRun dependencia** paquetes de saludo toodownload.</span><span class="sxs-lookup"><span data-stu-id="d74fe-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Descargar los paquetes de dependencia de LocalRun ADL Hola](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="d74fe-115">Busque los paquetes de dependencia de Hola de ruta de acceso de Hola se muestra en hello **salida** panel y, a continuación, instalar BuildTools y Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="d74fe-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="d74fe-116">A continuación se muestra una ruta de acceso de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d74fe-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="d74fe-117">![Busque los paquetes de dependencia de Hola](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="d74fe-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="d74fe-118">a.</span><span class="sxs-lookup"><span data-stu-id="d74fe-118">a.</span></span> <span data-ttu-id="d74fe-119">tooinstall BuildTools, siga las instrucciones del asistente Hola.</span><span class="sxs-lookup"><span data-stu-id="d74fe-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Instalación de BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="d74fe-121">b.</span><span class="sxs-lookup"><span data-stu-id="d74fe-121">b.</span></span> <span data-ttu-id="d74fe-122">tooinstall Win10SDK 10240, siga las instrucciones del Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d74fe-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Instalación de Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="d74fe-124">Configurar la variable de entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="d74fe-124">Set up hello environment variable.</span></span> <span data-ttu-id="d74fe-125">Conjunto hello **SCOPE_CPP_SDK** variable de entorno:</span><span class="sxs-lookup"><span data-stu-id="d74fe-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="d74fe-126">Reinicie Hola OS toomake seguro de que los valores de variable de entorno de hello surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="d74fe-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Asegúrese de variable de entorno de hello SCOPE_CPP_SDK está instalado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="d74fe-128">Iniciar el servicio de ejecución local de Hola y enviar la cuenta local de hello U-SQL trabajo tooa</span><span class="sxs-lookup"><span data-stu-id="d74fe-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="d74fe-129">Para el usuario de la primera vez de hello, son hello toodownload solicitadas ADL: Descargar LocalRun dependencia paquetes si ya no están instalados.</span><span class="sxs-lookup"><span data-stu-id="d74fe-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="d74fe-130">Seleccione la paleta de comando de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **ADL: iniciar el servicio ejecutar Local**.</span><span class="sxs-lookup"><span data-stu-id="d74fe-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="d74fe-131">Seleccione **Accept** tooaccept Hola términos de licencia de Software de Microsoft para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="d74fe-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Acepte los términos de licencia del Software de Microsoft de Hola](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="d74fe-133">Abre la consola de Hello cmd.</span><span class="sxs-lookup"><span data-stu-id="d74fe-133">hello cmd console opens.</span></span> <span data-ttu-id="d74fe-134">Para los usuarios de la primera vez, deberá tooenter **3**y, a continuación, busque la ruta de acceso de carpeta local de Hola para los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="d74fe-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="d74fe-135">Para ver otras opciones, puede usar valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="d74fe-135">For other options, you can use hello default values.</span></span> 

   ![Cmd de ejecución local de Data Lake Tools para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="d74fe-137">Seleccione Ctrl + Mayús + P tooopen Hola comando paleta, especifique **ADL: enviar trabajo**y, a continuación, seleccione **Local** toosubmit cuenta local de hello trabajo tooyour.</span><span class="sxs-lookup"><span data-stu-id="d74fe-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Selección local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="d74fe-139">Después de enviar el trabajo de hello, puede ver detalles de envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="d74fe-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="d74fe-140">Seleccione detalles de envío de hello tooview **jobUrl** en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="d74fe-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="d74fe-141">También puede ver el estado de envío del trabajo de Hola desde la consola de cmd de Hola.</span><span class="sxs-lookup"><span data-stu-id="d74fe-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="d74fe-142">Escriba **7** en la consola de cmd de hello si desea que tooknow más detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="d74fe-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="d74fe-143">![Salida d ejecución local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Herramientas de Data Lake para el estado de cmd de ejecución local de Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="d74fe-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="d74fe-144">Iniciar una depuración local de trabajo de SQL U Hola</span><span class="sxs-lookup"><span data-stu-id="d74fe-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="d74fe-145">Para el usuario de la primera vez de hello, son hello toodownload solicitadas ADL: Descargar LocalRun dependencia paquetes si ya no están instalados.</span><span class="sxs-lookup"><span data-stu-id="d74fe-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="d74fe-146">Seleccione la paleta de comando de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **ADL: iniciar el servicio ejecutar Local**.</span><span class="sxs-lookup"><span data-stu-id="d74fe-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="d74fe-147">Abre la consola de Hello cmd.</span><span class="sxs-lookup"><span data-stu-id="d74fe-147">hello cmd console opens.</span></span> <span data-ttu-id="d74fe-148">Asegúrese de que ese hello **DataRoot** se establece.</span><span class="sxs-lookup"><span data-stu-id="d74fe-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="d74fe-149">Establezca un punto de interrupción en el código subyacente de C#.</span><span class="sxs-lookup"><span data-stu-id="d74fe-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="d74fe-150">En el editor de secuencias de comandos de hello, seleccione la consola de comandos de Ctrl + Mayús + P tooopen hello y, a continuación, escriba **depurar Local** toostart su servicio en la depuración local.</span><span class="sxs-lookup"><span data-stu-id="d74fe-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Resultado de la depuración local de Herramientas de Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="d74fe-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d74fe-152">Next steps</span></span>
- <span data-ttu-id="d74fe-153">Para usar Herramientas de Azure Data Lake para Visual Studio, consulte [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md) (Uso de Herramientas de Azure Data Lake para Visual Studio Code).</span><span class="sxs-lookup"><span data-stu-id="d74fe-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="d74fe-154">Para información detallada sobre cómo empezar a trabajar con Data Lake Analytics, consulte [Tutorial: Introducción a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d74fe-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="d74fe-155">Para información sobre Herramientas de Data Lake para Visual Studio, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Herramientas de Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d74fe-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="d74fe-156">Para obtener información de hello en desarrollar ensamblados, vea [ensamblados desarrollar U-SQL para trabajos de análisis de Azure Data Lake](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="d74fe-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
