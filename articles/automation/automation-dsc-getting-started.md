---
title: "Introducción al DSC de Azure Automation | Microsoft Docs"
description: "Explicación y ejemplos de las tareas más comunes de la configuración de estado deseado (DSC) de Automatización de Azure"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="5035e-103">Introducción al DSC de Automatización de Azure:</span><span class="sxs-lookup"><span data-stu-id="5035e-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="5035e-104">En este tema se explica cómo realizar las mayoría de las tareas comunes con configuración de estado deseado (DSC) de Automatización de Azure, como crear, importar y compilar configuraciones, incorporar máquinas para administrarlas y ver informes.</span><span class="sxs-lookup"><span data-stu-id="5035e-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="5035e-105">Para obtener información general sobre qué es DSC de Automatización de Azure es, consulte [Información general de DSC de Automatización de Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5035e-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="5035e-106">Para obtener documentación de DSC, consulte [Información general sobre la configuración de estado deseado de Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="5035e-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="5035e-107">Este tema proporciona a una guía paso a paso para usar DSC de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="5035e-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="5035e-108">Si busca un entorno de ejemplo que ya se haya configurado sin seguir los pasos descritos en este tema, puede usar [la siguiente plantilla de ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="5035e-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="5035e-109">Esta plantilla configura un entorno de DSC de Automatización de Azure completado, incluida una máquina virtual de Azure administrada por DSC de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="5035e-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5035e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5035e-110">Prerequisites</span></span>
<span data-ttu-id="5035e-111">Para completar los ejemplos de este tema, se requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5035e-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="5035e-112">Una cuenta de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-112">An Azure Automation account.</span></span> <span data-ttu-id="5035e-113">Para obtener instrucciones sobre cómo crear una cuenta de ejecución de Azure Automation, consulte el artículo sobre las [cuentas de ejecución de Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="5035e-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="5035e-114">Una máquina virtual de Azure Resource Manager (no clásico) ejecuta Windows Server 2008 R2, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="5035e-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="5035e-115">Para obtener instrucciones sobre la creación de una máquina virtual, consulte [Creación de la primera máquina virtual de Windows en el Portal de Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="5035e-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="5035e-116">Creación de una configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="5035e-116">Creating a DSC configuration</span></span>
<span data-ttu-id="5035e-117">Crearemos una [configuración DSC](https://msdn.microsoft.com/powershell/dsc/configurations) simple que garantice la presencia o ausencia de la característica de Windows **Web-Server** (IIS), en función de cómo se asignen los nodos.</span><span class="sxs-lookup"><span data-stu-id="5035e-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="5035e-118">Inicie Windows PowerShell ISE (o cualquier editor de texto).</span><span class="sxs-lookup"><span data-stu-id="5035e-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="5035e-119">Escriba el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5035e-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="5035e-120">Guarde el archivo como `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="5035e-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="5035e-121">Esta configuración llama a un recurso de cada bloque del nodo, el recurso [WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), que garantiza la presencia o ausencia de la característica **Web-Server** .</span><span class="sxs-lookup"><span data-stu-id="5035e-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="5035e-122">Importación de una configuración en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="5035e-123">A continuación, importaremos la configuración en la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="5035e-124">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-125">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-126">En la hoja **Cuenta de Automation**, haga clic en **Configuraciones DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="5035e-127">En la hoja **Configuraciones DSC**, haga clic en **Agregar una configuración**.</span><span class="sxs-lookup"><span data-stu-id="5035e-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="5035e-128">En la hoja **Importar configuración**, vaya al archivo `TestConfig.ps1` del equipo.</span><span class="sxs-lookup"><span data-stu-id="5035e-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Captura de pantalla de la hoja **Importar configuración**](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="5035e-130">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5035e-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="5035e-131">Visualización de una configuración en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="5035e-132">Después de importar una configuración, puede verla en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5035e-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="5035e-133">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-134">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-135">En la hoja **Cuenta de Automation**, haga clic en **Configuraciones DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="5035e-136">En la hoja **Configuraciones DSC**, haga clic en **TestConfig** (es el nombre de la configuración que importó en el procedimiento anterior).</span><span class="sxs-lookup"><span data-stu-id="5035e-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="5035e-137">En la hoja **TestConfig Configuration** (Configuración de TestConfig), haga clic en **Ver el origen de configuración**.</span><span class="sxs-lookup"><span data-stu-id="5035e-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Captura de pantalla de la hoja TestConfig configuration (Configuración de TestConfig)](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="5035e-139">Se abre una hoja de **origen de Configuración de TestConfig** , que muestra el código de PowerShell de la configuración.</span><span class="sxs-lookup"><span data-stu-id="5035e-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="5035e-140">Compilación de una configuración en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="5035e-141">Para poder aplicar un estado deseado a un nodo, se debe compilar una configuración de DSC que defina dicho estado en una o varias configuraciones de nodo (documento de MOF) y se debe colocar en el servidor de extracción de DSC de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="5035e-142">Para obtener una descripción más detallada de la compilación de configuraciones en DSC de Automatización de Azure, consulte [Compilación de configuraciones en DSC de Automatización de Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="5035e-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="5035e-143">Para más información sobre la compilación de configuraciones, consulte [Configuraciones DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="5035e-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="5035e-144">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-145">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-146">En la hoja **Cuenta de Automation**, haga clic en **Configuraciones DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="5035e-147">En la hoja **Configuraciones DSC**, haga clic en **TestConfig** (el nombre de la configuración importada previamente).</span><span class="sxs-lookup"><span data-stu-id="5035e-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="5035e-148">En la hoja **TestConfig Configuration** (Configuración de TestConfig), haga clic en **Compilar** y luego en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="5035e-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="5035e-149">Así se inicia un trabajo de compilación.</span><span class="sxs-lookup"><span data-stu-id="5035e-149">This starts a compilation job.</span></span>
   
    ![Captura de pantalla de la hoja TestConfig configuration (Configuración de TestConfig) en la que se resalta el botón Compilar](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="5035e-151">Cuando se compila una configuración en Automatización de Azure, esta implementa todos los archivos MOF de configuración de nodo creados en el servidor de extracción.</span><span class="sxs-lookup"><span data-stu-id="5035e-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="5035e-152">Visualización de un trabajo de compilación</span><span class="sxs-lookup"><span data-stu-id="5035e-152">Viewing a compilation job</span></span>
<span data-ttu-id="5035e-153">Después de iniciar una compilación, puede verla en el icono **Trabajos de compilación** de la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="5035e-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="5035e-154">El icono **Trabajos de compilación** muestra los trabajos con errores, completados y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5035e-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="5035e-155">Cuando abra la hoja de un trabajo de compilación, mostrará información acerca del trabajo, incluidos los errores o advertencias encontrados, los parámetros de entrada usados en la configuración y los registros de compilación.</span><span class="sxs-lookup"><span data-stu-id="5035e-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="5035e-156">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-157">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-158">En la hoja **Cuenta de Automation**, haga clic en **Configuraciones DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="5035e-159">En la hoja **Configuraciones DSC**, haga clic en **TestConfig** (el nombre de la configuración importada previamente).</span><span class="sxs-lookup"><span data-stu-id="5035e-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="5035e-160">En el icono **Trabajos de compilación** de la hoja **TestConfig Configuration** (Configuración de TestConfig), haga clic en cualquiera de los trabajos enumerados.</span><span class="sxs-lookup"><span data-stu-id="5035e-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="5035e-161">Se abre la hoja de un **trabajo de compilación** , etiquetada con la fecha en que se inició el trabajo de compilación.</span><span class="sxs-lookup"><span data-stu-id="5035e-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Captura de pantalla de la hoja Trabajo de compilación](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="5035e-163">Haga clic en cualquiera de los iconos de la hoja **Trabajo de compilación** para ver detalles adicionales acerca del trabajo.</span><span class="sxs-lookup"><span data-stu-id="5035e-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="5035e-164">Visualización de configuraciones de nodo</span><span class="sxs-lookup"><span data-stu-id="5035e-164">Viewing node configurations</span></span>
<span data-ttu-id="5035e-165">La finalización correcta de un trabajo de compilación crea una o varias configuraciones de nodo nuevas.</span><span class="sxs-lookup"><span data-stu-id="5035e-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="5035e-166">Una configuración de nodo es un documento MOF que se implementa en el servidor de extracción y está listo ser extraído y que lo apliquen uno o varios nodos.</span><span class="sxs-lookup"><span data-stu-id="5035e-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="5035e-167">Las configuraciones de nodo de su cuenta de Automatización las puede ver en la hoja **Configuraciones del nodo de DSC** .</span><span class="sxs-lookup"><span data-stu-id="5035e-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="5035e-168">Los nombres de las configuraciones de nodo tienen el formato *ConfigurationName*.*NodeName*.</span><span class="sxs-lookup"><span data-stu-id="5035e-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="5035e-169">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-170">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-171">En la hoja **Cuenta de Automation**, haga clic en **Configuraciones del nodo de DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Captura de pantalla de la hoja Configuraciones del nodo de DSC ](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="5035e-173">Incorporación de una máquina virtual de Azure para la administración con DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="5035e-174">DSC de automatización de Azure se puede usar para administrar máquinas virtuales de Azure (tanto el enfoque clásico como el de Resource Manager), máquinas virtuales locales, máquinas de Linux, máquinas virtuales de AWS y máquinas físicas locales.</span><span class="sxs-lookup"><span data-stu-id="5035e-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="5035e-175">En este tema, se explicará cómo incorporar solo máquinas virtuales de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5035e-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="5035e-176">Para más información sobre la incorporación de otros tipos de máquinas, consulte [Incorporación de máquinas para administrarlas con DSC de Automatización de Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="5035e-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="5035e-177">Para incorporar una máquina virtual de Azure Resource Manager para que DSC de Automatización de Azure la administre</span><span class="sxs-lookup"><span data-stu-id="5035e-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="5035e-178">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-179">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-180">En la hoja **Cuenta de Automation**, haga clic en **Nodos DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5035e-181">En la hoja **Nodos DSC**, haga clic en **Agregar máquina virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="5035e-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Captura de pantalla de la hoja Nodos DSC en la que se resalta el botón Agregar máquina virtual de Azure](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="5035e-183">En la hoja **Agregar máquinas virtuales de Azure**, haga clic en **Seleccionar máquinas virtuales para incorporar**.</span><span class="sxs-lookup"><span data-stu-id="5035e-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="5035e-184">En la hoja **Seleccionar máquinas virtuales**, seleccione la máquina virtual que desea incorporar y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5035e-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5035e-185">Debe ser una máquina virtual de Azure Resource Manager que ejecute Windows Server 2008 R2, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="5035e-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="5035e-186">En la hoja **Agregar máquinas virtuales de Azure**, haga clic en **Configurar datos de registro**.</span><span class="sxs-lookup"><span data-stu-id="5035e-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="5035e-187">En la hoja **Registro**, escriba el nombre de la configuración del nodo que quiere aplicar a la máquina virtual en el cuadro **Nombre de la configuración del nodo**.</span><span class="sxs-lookup"><span data-stu-id="5035e-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="5035e-188">Debe coincidir exactamente con el nombre de una configuración de nodo de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="5035e-189">Especificar un nombre en este momento es opcional.</span><span class="sxs-lookup"><span data-stu-id="5035e-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="5035e-190">Puede cambiar la configuración de nodo asignada después de la incorporación del nodo.</span><span class="sxs-lookup"><span data-stu-id="5035e-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="5035e-191">Marque **Reiniciar el nodo si es necesario** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5035e-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Captura de pantalla de la hoja Registro](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="5035e-193">La configuración de nodo que especificó se aplicará a la máquina virtual según los intervalos especificados por el valor de **Frecuencia del modo de configuración** y la máquina virtual buscará actualizaciones en la configuración del nodo según los intervalos especificados por el valor de **Frecuencia de actualización**.</span><span class="sxs-lookup"><span data-stu-id="5035e-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="5035e-194">Para más información sobre cómo se utilizan estos valores, consulte [Configuración del administrador de configuración local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="5035e-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="5035e-195">En la hoja **Agregar máquinas virtuales de Azure**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5035e-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="5035e-196">Azure iniciará el proceso de incorporación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5035e-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="5035e-197">Cuando se complete, la máquina virtual se mostrará en la hoja **Nodos DSC** en la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="5035e-198">Visualización de la lista de nodos DSC</span><span class="sxs-lookup"><span data-stu-id="5035e-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="5035e-199">Puede ver la lista de todas las máquinas que han sido incorporados para la administración de la cuenta de Automatización en la hoja **Nodos DSC** .</span><span class="sxs-lookup"><span data-stu-id="5035e-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="5035e-200">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-201">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-202">En la hoja **Cuenta de Automation**, haga clic en **Nodos DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="5035e-203">Visualización de informes de los nodos DSC</span><span class="sxs-lookup"><span data-stu-id="5035e-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="5035e-204">Cada vez que DSC de Automatización de Azure realiza una comprobación de coherencia en un nodos administrado, el nodo envía un informe de estado al servidor de extracción.</span><span class="sxs-lookup"><span data-stu-id="5035e-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="5035e-205">Estos informes se pueden ver en la hoja de dicho nodo.</span><span class="sxs-lookup"><span data-stu-id="5035e-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="5035e-206">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-207">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-208">En la hoja **Cuenta de Automation**, haga clic en **Nodos DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5035e-209">En el icono **Informes** , haga clic en cualquiera de los informes de la lista.</span><span class="sxs-lookup"><span data-stu-id="5035e-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Captura de pantalla de la hoja Informe](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="5035e-211">En la hoja de un informe individual puede ver la siguiente información de estado de la comprobación de coherencia correspondiente:</span><span class="sxs-lookup"><span data-stu-id="5035e-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="5035e-212">El estado del informe, si el nodo es "Compatible", la configuración "Error" o el nodo es "No compatible" (cuando el nodo está en modo **applyandmonitor** y la máquina no está en el estado deseado).</span><span class="sxs-lookup"><span data-stu-id="5035e-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="5035e-213">La hora de inicio de la comprobación de coherencia.</span><span class="sxs-lookup"><span data-stu-id="5035e-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="5035e-214">El tiempo de ejecución total de la comprobación de coherencia.</span><span class="sxs-lookup"><span data-stu-id="5035e-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="5035e-215">El tipo de comprobación de coherencia.</span><span class="sxs-lookup"><span data-stu-id="5035e-215">The type of consistency check.</span></span>
* <span data-ttu-id="5035e-216">Todos los errores, incluidos el código de error y el mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="5035e-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="5035e-217">Los recursos de DSC utilizados en la configuración y el estado de cada recurso (si el nodo está en el estado deseado para dicho recurso): puede hacer clic en cada recurso para más información.</span><span class="sxs-lookup"><span data-stu-id="5035e-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="5035e-218">El nombre, la dirección IP y el modo de configuración del nodo.</span><span class="sxs-lookup"><span data-stu-id="5035e-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="5035e-219">También puede hacer clic en **Ver informe sin formato** para ver los datos reales que el nodo envía al servidor.</span><span class="sxs-lookup"><span data-stu-id="5035e-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="5035e-220">Para más información sobre el uso de esos datos, consulte [Uso de un servidor de informes de DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="5035e-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="5035e-221">Después de que se incorpora un nodo puede pasar un tiempo antes de que el primer informe esté disponible.</span><span class="sxs-lookup"><span data-stu-id="5035e-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="5035e-222">Después de incorporar un nodo es posible que tenga que esperar hasta 30 minutos para que aparezca el primer informe.</span><span class="sxs-lookup"><span data-stu-id="5035e-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="5035e-223">Reasignación de un nodo a una configuración de nodo diferente</span><span class="sxs-lookup"><span data-stu-id="5035e-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="5035e-224">Puede asignar un nodo para que use una configuración de nodo diferente a la que le asignó inicialmente.</span><span class="sxs-lookup"><span data-stu-id="5035e-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="5035e-225">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-226">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-227">En la hoja **Cuenta de Automation**, haga clic en **Nodos DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5035e-228">En la hoja **Nodos DSC** , haga clic en el nombre del nodo que quiere reasignar.</span><span class="sxs-lookup"><span data-stu-id="5035e-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="5035e-229">En la hoja de dicho nodo, haga clic en **Asignar nodo**.</span><span class="sxs-lookup"><span data-stu-id="5035e-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Captura de pantalla de la hoja Nodo en la que se resalta el botón Asignar nodo](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="5035e-231">En la hoja **Asignar configuración de nodo**, seleccione la configuración de nodo a la que desea asignar el nodo y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5035e-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Captura de pantalla de la hoja Asignar configuración de nodo](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="5035e-233">Anulación del registro de un nodo</span><span class="sxs-lookup"><span data-stu-id="5035e-233">Unregistering a node</span></span>
<span data-ttu-id="5035e-234">Si ya no desea que DSC de Automatización de Azure administre un nodo, puede anular su registro.</span><span class="sxs-lookup"><span data-stu-id="5035e-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="5035e-235">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5035e-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5035e-236">En el menú del concentrador, haga clic en **Todos los recursos** y, luego, en el nombre de la cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="5035e-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="5035e-237">En la hoja **Cuenta de Automation**, haga clic en **Nodos DSC**.</span><span class="sxs-lookup"><span data-stu-id="5035e-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="5035e-238">En la hoja **Nodos DSC** , haga clic en el nombre del nodo que quiere reasignar.</span><span class="sxs-lookup"><span data-stu-id="5035e-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="5035e-239">En la hoja de dicho nodo, haga clic en **Anular registro**.</span><span class="sxs-lookup"><span data-stu-id="5035e-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Captura de pantalla de la hoja Nodo en la que se resalta el botón Anular registro](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="5035e-241">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="5035e-241">Related Articles</span></span>
* [<span data-ttu-id="5035e-242">Información general de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="5035e-243">Incorporación de máquinas para administrarlas con DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="5035e-244">Windows PowerShell Desired State Configuration Overview (Información general de la configuración de estado deseado de Windows Powershell)</span><span class="sxs-lookup"><span data-stu-id="5035e-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="5035e-245">Cmdlets de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="5035e-246">Precios de DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="5035e-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

