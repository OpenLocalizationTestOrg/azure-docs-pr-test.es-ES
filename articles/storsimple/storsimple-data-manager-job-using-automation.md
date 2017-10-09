---
title: "Automatización de Azure de aaaUse tootrigger un trabajo | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse automatización de Azure para la activación de trabajos de administrador de datos de StorSimple (vista previa privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="35469-103">Usar la automatización de Azure tootrigger un trabajo (Private Preview)</span><span class="sxs-lookup"><span data-stu-id="35469-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="35469-104">En este artículo se describe cómo tootrigger de automatización de Azure toouse un trabajo del Administrador de datos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="35469-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35469-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="35469-105">Prerequisites</span></span>

<span data-ttu-id="35469-106">Antes de comenzar, asegúrese de que dispone de:</span><span class="sxs-lookup"><span data-stu-id="35469-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="35469-107">Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="35469-107">Azure Powershell installed.</span></span> <span data-ttu-id="35469-108">[Descarga de Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="35469-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="35469-109">Trabajo de transformación de datos Hola de configuración configuración tooinitialize (instrucciones tooobtain estas opciones se incluyen aquí).</span><span class="sxs-lookup"><span data-stu-id="35469-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="35469-110">Una definición del trabajo que se ha configurado correctamente en un recurso de datos híbridos de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="35469-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="35469-111">Descargar `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) archivos del repositorio de github de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="35469-112">Descargar `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) del repositorio de github de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="35469-113">Descargar `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) del repositorio de github de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="35469-114">Paso a paso</span><span class="sxs-lookup"><span data-stu-id="35469-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="35469-115">Obtener permisos de Azure Active Directory de definición de trabajo de hello automatización trabajo toorun Hola</span><span class="sxs-lookup"><span data-stu-id="35469-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="35469-116">parámetros de configuración de hello tooretrieve para Active Directory, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="35469-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="35469-117">Abra Windows PowerShell en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="35469-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="35469-118">Asegúrese de que [Azure PowerShell](https://azure.microsoft.com/downloads/) esté instalado.</span><span class="sxs-lookup"><span data-stu-id="35469-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="35469-119">Ejecute hello `Get-ConfigurationParams.ps1` script (en la carpeta de hello descargó anteriormente).</span><span class="sxs-lookup"><span data-stu-id="35469-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="35469-120">Escriba el siguiente comando en la ventana de PowerShell de hello de Hola:</span><span class="sxs-lookup"><span data-stu-id="35469-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="35469-121">Hola ActiveDirectoryKey es una contraseña que utilizar más adelante.</span><span class="sxs-lookup"><span data-stu-id="35469-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="35469-122">Escriba una contraseña de su elección.</span><span class="sxs-lookup"><span data-stu-id="35469-122">Enter a password of your choice.</span></span> <span data-ttu-id="35469-123">AppName puede ser cualquier cadena.</span><span class="sxs-lookup"><span data-stu-id="35469-123">AppName can be any string.</span></span>

2. <span data-ttu-id="35469-124">Este script genera Hola después valores que deben usarse durante la activación de runbook de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="35469-125">Anote estos valores.</span><span class="sxs-lookup"><span data-stu-id="35469-125">Make a note of these values.</span></span>

    - <span data-ttu-id="35469-126">Id. de cliente</span><span class="sxs-lookup"><span data-stu-id="35469-126">Client ID</span></span>
    - <span data-ttu-id="35469-127">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="35469-127">Tenant ID</span></span>
    - <span data-ttu-id="35469-128">Claves de Active Directory (igual que uno que Arri Hola)</span><span class="sxs-lookup"><span data-stu-id="35469-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="35469-129">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="35469-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="35469-130">Configurar la cuenta de automatización de Hola</span><span class="sxs-lookup"><span data-stu-id="35469-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="35469-131">Inicie sesión en tooAzure y abra su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="35469-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="35469-132">Haga clic en **activos** icono tooopen Hola lista de activos.</span><span class="sxs-lookup"><span data-stu-id="35469-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="35469-133">Haga clic en **módulos** icono tooopen Hola lista de módulos.</span><span class="sxs-lookup"><span data-stu-id="35469-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="35469-134">Haga clic en **+ agregar un módulo** hello y botón hoja de módulo de complemento se inicia.</span><span class="sxs-lookup"><span data-stu-id="35469-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Configuración de la cuenta de Automation](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="35469-136">Después de haber seleccionado hello `DataTransformationApp.zip` de archivos desde el equipo local, haga clic en **Aceptar** módulo de hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="35469-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="35469-137">Cuando una cuenta de tooyour de módulo se importa en automatización de Azure, extrae metadatos sobre el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="35469-138">Esta operación puede demorar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="35469-138">This operation may take a couple of minutes.</span></span>

   ![Configuración de la cuenta de Automation](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="35469-140">Recibirá una notificación se va a implementar ese módulo hello y otra notificación cuando se complete el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="35469-141">También puede comprobar el estado de hello **módulos** icono.</span><span class="sxs-lookup"><span data-stu-id="35469-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="35469-142">tooimport Hola runbook que desencadena la definición del trabajo Hola</span><span class="sxs-lookup"><span data-stu-id="35469-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="35469-143">Hola portal de Azure, abra su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="35469-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="35469-144">Haga clic en **Runbooks** icono tooopen Hola lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="35469-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="35469-145">Haga clic en **+ Agregar un runbook** y, luego, en **Importar un runbook existente**.</span><span class="sxs-lookup"><span data-stu-id="35469-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importar un runbook existente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="35469-147">Haga clic en **archivo de Runbook** y Hola Seleccione archivo tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="35469-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="35469-148">Haga clic en **crear** tooimport Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="35469-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="35469-149">Hola nuevo runbook aparecerá en lista de Hola de runbooks para hello cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="35469-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="35469-150">Haga clic en el runbook **Trigger-DataTransformation-Job** y, luego, en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="35469-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="35469-151">Haga clic en **Publicar** y, luego, en **Sí** cuando se pida confirmación.</span><span class="sxs-lookup"><span data-stu-id="35469-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="35469-152">toorun Hola runbook:</span><span class="sxs-lookup"><span data-stu-id="35469-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="35469-153">Hola portal de Azure, abra su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="35469-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="35469-154">Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="35469-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="35469-155">Haga clic en **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="35469-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="35469-156">Haga clic en **iniciar** toostart Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="35469-156">Click **Start** toostart hello runbook.</span></span>

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="35469-158">Hola **iniciar runbook** hoja, escriba todos los parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="35469-159">Haga clic en **Aceptar** trabajo de transformación de datos de toosubmit Hola.</span><span class="sxs-lookup"><span data-stu-id="35469-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Iniciar runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="35469-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35469-161">Next steps</span></span>

<span data-ttu-id="35469-162">[Usar los datos de interfaz de usuario de administrador de datos de StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="35469-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
