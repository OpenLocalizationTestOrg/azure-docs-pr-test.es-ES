---
title: "Compilación de configuraciones en DSC de Azure Automation | Microsoft Docs"
description: "En este artículo se describe cómo compilar configuraciones de configuración de estado deseado (DSC) para Azure Automation."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="4e4d3-103">Compilación de configuraciones en DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="4e4d3-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="4e4d3-104">Puede compilar las configuraciones de configuración de estado deseado (DSC) de dos formas con Azure Automation: en Azure Portal y con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in the Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="4e4d3-105">La tabla siguiente le ayudará a determinar cuándo se debe usar cada método en base a las características de cada uno:</span><span class="sxs-lookup"><span data-stu-id="4e4d3-105">The following table will help you determine when to use which method based on the characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4e4d3-106">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4e4d3-106">Azure portal</span></span>

* <span data-ttu-id="4e4d3-107">Método más sencillo con la interfaz de usuario interactiva</span><span class="sxs-lookup"><span data-stu-id="4e4d3-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="4e4d3-108">Forma para proporcionar valores de parámetro simples</span><span class="sxs-lookup"><span data-stu-id="4e4d3-108">Form to provide simple parameter values</span></span>
* <span data-ttu-id="4e4d3-109">Seguimiento sencillo del estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="4e4d3-109">Easily track job state</span></span>
* <span data-ttu-id="4e4d3-110">Acceso autenticado con inicio de sesión de Azure</span><span class="sxs-lookup"><span data-stu-id="4e4d3-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="4e4d3-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4d3-111">Windows PowerShell</span></span>

* <span data-ttu-id="4e4d3-112">Llamar desde la línea de comandos con los cmdlets de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4d3-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="4e4d3-113">Poder incluirse en una solución automatizada con varios pasos</span><span class="sxs-lookup"><span data-stu-id="4e4d3-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="4e4d3-114">Proporcionar valores de parámetro simples y complejos</span><span class="sxs-lookup"><span data-stu-id="4e4d3-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="4e4d3-115">Realizar el seguimiento del estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="4e4d3-115">Track job state</span></span>
* <span data-ttu-id="4e4d3-116">Responder a la necesidad del cliente para admitir los cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4d3-116">Client required to support PowerShell cmdlets</span></span>
* <span data-ttu-id="4e4d3-117">Pasar ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="4e4d3-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="4e4d3-118">Compilar configuraciones que usan credenciales</span><span class="sxs-lookup"><span data-stu-id="4e4d3-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="4e4d3-119">Una vez que haya decidido un método de compilación, puede seguir los procedimientos correspondientes que se presentan a continuación para empezar a compilar.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-119">Once you have decided on a compilation method, you can follow the respective procedures below to start compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a><span data-ttu-id="4e4d3-120">Compilación de una configuración de DSC con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4e4d3-120">Compiling a DSC Configuration with the Azure portal</span></span>

1. <span data-ttu-id="4e4d3-121">En su cuenta de Automation, haga clic en **DSC Configurations** (Configuraciones DSC).</span><span class="sxs-lookup"><span data-stu-id="4e4d3-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="4e4d3-122">Haga clic en una configuración para abrir su hoja.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-122">Click a configuration to open its blade.</span></span>
3. <span data-ttu-id="4e4d3-123">Haga clic en **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-123">Click **Compile**.</span></span>
4. <span data-ttu-id="4e4d3-124">Si la configuración no tiene parámetros, se le pedirá que confirme si desea compilarla.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-124">If the configuration has no parameters, you will be prompted to confirm whether you want to compile it.</span></span> <span data-ttu-id="4e4d3-125">Si la configuración tiene parámetros, se abrirá la hoja **Compilar configuración** para que pueda proporcionar valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-125">If the configuration has parameters, the **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="4e4d3-126">Consulte más abajo la sección [**Parámetros básicos**](#basic-parameters) para más información sobre los parámetros.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-126">See the [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="4e4d3-127">La hoja **Trabajo de compilación** está abierta para que puede realizar un seguimiento de estado del trabajo de compilación y las configuraciones de nodo (documentos de configuración de MOF) que ocasiona que se colocará en el servidor de extracción de DSC de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-127">The **Compilation Job** blade is opened so that you can track the compilation job's status, and the node configurations (MOF configuration documents) it caused to be placed on the Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="4e4d3-128">Compilación de una configuración DSC con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4d3-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="4e4d3-129">Puede usar [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) para iniciar la compilación con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) to start compiling with Windows PowerShell.</span></span> <span data-ttu-id="4e4d3-130">El código de ejemplo siguiente inicia la compilación de una configuración DSC denominada **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-130">The following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="4e4d3-131">`Start-AzureRmAutomationDscCompilationJob` devuelve un objeto de trabajo de compilación que puede usar para realizar el seguimiento de su estado.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use to track its status.</span></span> <span data-ttu-id="4e4d3-132">A continuación, puede usar dicho objeto de trabajo de compilación con [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) para determinar el estado del trabajo de compilación y [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) para ver sus transmisiones (salida).</span><span class="sxs-lookup"><span data-stu-id="4e4d3-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) to determine the status of the compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) to view its streams (output).</span></span> <span data-ttu-id="4e4d3-133">El código de ejemplo siguiente inicia la compilación de la configuración **SampleConfig** , espera hasta que finalice y, a continuación, muestra sus flujos.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-133">The following sample code starts compilation of the **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="4e4d3-134">Parámetros básicos</span><span class="sxs-lookup"><span data-stu-id="4e4d3-134">Basic Parameters</span></span>
<span data-ttu-id="4e4d3-135">La declaración de parámetro en configuraciones DSC, incluidos los tipos de parámetro y las propiedades, funciona igual que en los runbooks de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-135">Parameter declaration in DSC configurations, including parameter types and properties, works the same as in Azure Automation runbooks.</span></span> <span data-ttu-id="4e4d3-136">Vea [Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) para obtener más información acerca de los parámetros del runbook.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to learn more about runbook parameters.</span></span>

<span data-ttu-id="4e4d3-137">En el ejemplo siguiente se usan dos parámetros, **FeatureName** e **IsPresent**, para determinar los valores de las propiedades de la configuración del nodo **ParametersExample.sample**, que se ha generado durante la compilación.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-137">The following example uses two parameters called **FeatureName** and **IsPresent**, to determine the values of properties in the **ParametersExample.sample** node configuration, generated during compilation.</span></span>

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

<span data-ttu-id="4e4d3-138">Puede compilar configuraciones DSC que usan parámetros básicos en el portal de DSC de Automatización de Azure o Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4e4d3-138">You can compile DSC Configurations that use basic parameters in the Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="4e4d3-139">Portal</span><span class="sxs-lookup"><span data-stu-id="4e4d3-139">Portal</span></span>

<span data-ttu-id="4e4d3-140">En el portal, puede especificar valores de parámetro después de hacer clic **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-140">In the portal, you can enter parameter values after clicking **Compile**.</span></span>

![texto alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="4e4d3-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4d3-142">PowerShell</span></span>

<span data-ttu-id="4e4d3-143">PowerShell requiere parámetros de un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) donde la clave coincide con el nombre del parámetro y el valor es igual al valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key matches the parameter name, and the value equals the parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="4e4d3-144">Para obtener información acerca de cómo pasar PSCredentials como parámetros, consulte más abajo la sección <a href="#credential-assets">**Recursos de credenciales**</a> .</span><span class="sxs-lookup"><span data-stu-id="4e4d3-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="4e4d3-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="4e4d3-145">ConfigurationData</span></span>
<span data-ttu-id="4e4d3-146">**ConfigurationData** le permite separar la configuración estructural de cualquier configuración específica del entorno al usar DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-146">**ConfigurationData** allows you to separate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="4e4d3-147">Consulte [Diferenciación de "Qué" y "Dónde" en DSC de PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) para obtener más información sobre **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) to learn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="4e4d3-148">Puede usar **ConfigurationData** cuando compile en DSC de Automatización de Azure con Azure PowerShell, pero no en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in the Azure portal.</span></span>

<span data-ttu-id="4e4d3-149">En el siguiente ejemplo la configuración de DSC usa **ConfigurationData** a través de las palabras clave **$ConfigurationData** y **$AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-149">The following example DSC configuration uses **ConfigurationData** via the **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="4e4d3-150">Para este ejemplo también necesitará el [módulo **xWebAdministration**](https://www.powershellgallery.com/packages/xWebAdministration/):</span><span class="sxs-lookup"><span data-stu-id="4e4d3-150">You'll also need the [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

<span data-ttu-id="4e4d3-151">Puede compilar la configuración de DSC anterior con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-151">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="4e4d3-152">PowerShell agrega las configuraciones de dos nodos al servidor de extracción de DSC de Azure Automation: **ConfigurationDataSample.MyVM1** y **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="4e4d3-152">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a><span data-ttu-id="4e4d3-153">Recursos</span><span class="sxs-lookup"><span data-stu-id="4e4d3-153">Assets</span></span>

<span data-ttu-id="4e4d3-154">Las referencias de recursos son las mismas en las configuraciones de DSC de Automatización de Azure y en los runbooks.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-154">Asset references are the same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="4e4d3-155">Para obtener más información, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e4d3-155">See the following for more information:</span></span>

* [<span data-ttu-id="4e4d3-156">Certificados</span><span class="sxs-lookup"><span data-stu-id="4e4d3-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="4e4d3-157">Conexiones</span><span class="sxs-lookup"><span data-stu-id="4e4d3-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="4e4d3-158">Credenciales</span><span class="sxs-lookup"><span data-stu-id="4e4d3-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="4e4d3-159">Variables</span><span class="sxs-lookup"><span data-stu-id="4e4d3-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="4e4d3-160">Recursos de credenciales</span><span class="sxs-lookup"><span data-stu-id="4e4d3-160">Credential Assets</span></span>

<span data-ttu-id="4e4d3-161">Mientras que las configuraciones DSC en Azure Automation pueden hacer referencia a los recursos de credenciales mediante **Get-AzureRmAutomationCredential**, los recursos de credenciales también se pueden pasar mediante parámetros, si se desea.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="4e4d3-162">Si una configuración toma un parámetro del tipo **PSCredential** , tendrá que pasar el nombre de cadena de un activo de credencial de Automatización de Azure como el valor de ese parámetro en lugar de como un objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-162">If a configuration takes a parameter of **PSCredential** type, then you need to pass the string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="4e4d3-163">En segundo plano, se recuperará el recurso de credencial de Automatización de Azure con ese nombre y se pasará a la configuración.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-163">Behind the scenes, the Azure Automation credential asset with that name will be retrieved and passed to the configuration.</span></span>

<span data-ttu-id="4e4d3-164">Mantener las credenciales seguras en configuraciones de nodo (documentos de configuración MOF) exige el cifrado de las credenciales en el archivo MOF de configuración de nodo.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting the credentials in the node configuration MOF file.</span></span> <span data-ttu-id="4e4d3-165">Automatización de Azure va un poco más allá y cifra todo el archivo MOF.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-165">Azure Automation takes this one step further and encrypts the entire MOF file.</span></span> <span data-ttu-id="4e4d3-166">Sin embargo, actualmente tiene que indicar a DSC de PowerShell que no importa que las credenciales tengan salida como texto sin formato durante la generación del MOF de configuración de nodo, porque PowerShell DSC desconoce que Automatización de Azure cifrará todo el archivo MOF después de su generación a través de un trabajo de compilación.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-166">However, currently you must tell PowerShell DSC it is okay for credentials to be outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting the entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="4e4d3-167">Puede indicar a DSC de PowerShell que es correcto que las credenciales tengan salida como texto sin formato en el MOF de configuración de nodo generado mediante [**ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="4e4d3-167">You can tell PowerShell DSC that it is okay for credentials to be outputted in plain text in the generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="4e4d3-168">Debe pasar `PSDscAllowPlainTextPassword = $true` a través de **ConfigurationData** para el nombre de cada bloque de nodo que aparezca en la configuración de DSC y use las credenciales.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in the DSC configuration and uses credentials.</span></span>

<span data-ttu-id="4e4d3-169">En el ejemplo siguiente se muestra una configuración de DSC que usa un recurso de la credencial de Automatización.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-169">The following example shows a DSC configuration that uses an Automation credential asset.</span></span>

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

<span data-ttu-id="4e4d3-170">Puede compilar la configuración de DSC anterior con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-170">You can compile the DSC configuration above with PowerShell.</span></span> <span data-ttu-id="4e4d3-171">PowerShell agrega las configuraciones de dos nodos al servidor de extracción de DSC de Azure Automation: **CredentialSample.MyVM1** y **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-171">The below PowerShell adds two node configurations to the Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a><span data-ttu-id="4e4d3-172">Importación de configuraciones de nodo</span><span class="sxs-lookup"><span data-stu-id="4e4d3-172">Importing node configurations</span></span>

<span data-ttu-id="4e4d3-173">También puede importar configuraciones de nodo (MOF) que se hayan compilado fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="4e4d3-174">Una ventaja de esta posibilidad es que las configuraciones de nodo pueden estar firmadas.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="4e4d3-175">Una configuración de nodo firmada se comprueba localmente en un nodo administrado mediante el agente DSC; de este modo, se garantiza que la configuración que se va a aplicar al nodo proviene de una fuente autorizada.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-175">A signed node configuration is verified locally on a managed node by the DSC agent, ensuring that the configuration being applied to the node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="4e4d3-176">Puede usar importar configuraciones firmadas en su cuenta de Azure Automation, pero Azure Automation no admite actualmente la compilación de configuraciones firmadas.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="4e4d3-177">Un archivo de configuración de nodo debe ocupar más de 1 MB para poderlo importar en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-177">A node configuration file must be no larger than 1 MB to allow it to be imported into Azure Automation.</span></span>

<span data-ttu-id="4e4d3-178">Puede descubrir cómo firmar configuraciones de nodo en https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-178">You can learn how to sign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-the-azure-portal"></a><span data-ttu-id="4e4d3-179">Importación de una configuración de nodo en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4e4d3-179">Importing a node configuration in the Azure portal</span></span>

1. <span data-ttu-id="4e4d3-180">En su cuenta de Automation, haga clic en **DSC node configurations** (Configuraciones de nodo DSC).</span><span class="sxs-lookup"><span data-stu-id="4e4d3-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configuraciones de nodo DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="4e4d3-182">En la hoja **Configuraciones de nodo DSC**, haga clic en **Agregar NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-182">In the **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="4e4d3-183">En la hoja **Importar**, haga clic en el icono de carpeta situado junto al cuadro de texto **Node Configuration File** (Archivo de configuración de nodo) para buscar un archivo de configuración de nodo (MOF) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-183">In the **Import** blade, click the folder icon next to the **Node Configuration File** textbox to browse for a node configuration file (MOF) on your local computer.</span></span>

    ![Buscar archivo local](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="4e4d3-185">Escriba un nombre en el cuadro de texto **Nombre de la configuración**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-185">Enter a name in the **Configuration Name** textbox.</span></span> <span data-ttu-id="4e4d3-186">Este nombre debe coincidir con el de la configuración desde la que se compiló la configuración del nodo.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-186">This name must match the name of the configuration from which the node configuration was compiled.</span></span>
5. <span data-ttu-id="4e4d3-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="4e4d3-188">Importación de una configuración de nodo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4d3-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="4e4d3-189">Puede usar el cmdlet [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) para importar una configuración de nodo en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="4e4d3-189">You can use the [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet to import a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



