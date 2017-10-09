---
title: "aaaCompiling configuraciones de DSC de automatización de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo toocompile las configuraciones de configuración de estado deseado (DSC) para la automatización de Azure."
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
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a><span data-ttu-id="c2375-103">Compilación de configuraciones en DSC de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="c2375-103">Compiling configurations in Azure Automation DSC</span></span>

<span data-ttu-id="c2375-104">Puede compilar configuraciones de configuración de estado deseado (DSC) de dos maneras con automatización de Azure: Hola portal de Azure y con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2375-104">You can compile Desired State Configuration (DSC) configurations in two ways with Azure Automation: in hello Azure portal, and with Windows PowerShell.</span></span> <span data-ttu-id="c2375-105">Hello tabla siguiente le ayudará a determinar cuándo toouse qué método basándose en características de Hola de cada uno:</span><span class="sxs-lookup"><span data-stu-id="c2375-105">hello following table will help you determine when toouse which method based on hello characteristics of each:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="c2375-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c2375-106">Azure portal</span></span>

* <span data-ttu-id="c2375-107">Método más sencillo con la interfaz de usuario interactiva</span><span class="sxs-lookup"><span data-stu-id="c2375-107">Simplest method with interactive user interface</span></span>
* <span data-ttu-id="c2375-108">Valores de parámetro simples de formulario tooprovide</span><span class="sxs-lookup"><span data-stu-id="c2375-108">Form tooprovide simple parameter values</span></span>
* <span data-ttu-id="c2375-109">Seguimiento sencillo del estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="c2375-109">Easily track job state</span></span>
* <span data-ttu-id="c2375-110">Acceso autenticado con inicio de sesión de Azure</span><span class="sxs-lookup"><span data-stu-id="c2375-110">Access authenticated with Azure logon</span></span>

### <a name="windows-powershell"></a><span data-ttu-id="c2375-111">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2375-111">Windows PowerShell</span></span>

* <span data-ttu-id="c2375-112">Llamar desde la línea de comandos con los cmdlets de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2375-112">Call from command line with Windows PowerShell cmdlets</span></span>
* <span data-ttu-id="c2375-113">Poder incluirse en una solución automatizada con varios pasos</span><span class="sxs-lookup"><span data-stu-id="c2375-113">Can be included in automated solution with multiple steps</span></span>
* <span data-ttu-id="c2375-114">Proporcionar valores de parámetro simples y complejos</span><span class="sxs-lookup"><span data-stu-id="c2375-114">Provide simple and complex parameter values</span></span>
* <span data-ttu-id="c2375-115">Realizar el seguimiento del estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="c2375-115">Track job state</span></span>
* <span data-ttu-id="c2375-116">Cliente requerido toosupport cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2375-116">Client required toosupport PowerShell cmdlets</span></span>
* <span data-ttu-id="c2375-117">Pasar ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="c2375-117">Pass ConfigurationData</span></span>
* <span data-ttu-id="c2375-118">Compilar configuraciones que usan credenciales</span><span class="sxs-lookup"><span data-stu-id="c2375-118">Compile configurations that use credentials</span></span>

<span data-ttu-id="c2375-119">Una vez que haya decidido en un método de compilación, puede seguir Hola respectivos procedimientos a continuación toostart compilar.</span><span class="sxs-lookup"><span data-stu-id="c2375-119">Once you have decided on a compilation method, you can follow hello respective procedures below toostart compiling.</span></span>

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a><span data-ttu-id="c2375-120">Compilar una configuración de DSC con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c2375-120">Compiling a DSC Configuration with hello Azure portal</span></span>

1. <span data-ttu-id="c2375-121">En su cuenta de Automation, haga clic en **DSC Configurations** (Configuraciones DSC).</span><span class="sxs-lookup"><span data-stu-id="c2375-121">From your Automation account, click **DSC Configurations**.</span></span>
2. <span data-ttu-id="c2375-122">Haga clic en una configuración tooopen su hoja.</span><span class="sxs-lookup"><span data-stu-id="c2375-122">Click a configuration tooopen its blade.</span></span>
3. <span data-ttu-id="c2375-123">Haga clic en **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="c2375-123">Click **Compile**.</span></span>
4. <span data-ttu-id="c2375-124">Si configuración de hello no tiene parámetros, es posible que tooconfirm solicitada si desea que toocompile lo.</span><span class="sxs-lookup"><span data-stu-id="c2375-124">If hello configuration has no parameters, you will be prompted tooconfirm whether you want toocompile it.</span></span> <span data-ttu-id="c2375-125">Si la configuración de hello tiene parámetros, Hola **compilar configuración** hoja se abrirá por lo que puede proporcionar valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="c2375-125">If hello configuration has parameters, hello **Compile Configuration** blade will open so you can provide parameter values.</span></span> <span data-ttu-id="c2375-126">Vea hello [ **parámetros básicos** ](#basic-parameters) sección para obtener más información sobre parámetros.</span><span class="sxs-lookup"><span data-stu-id="c2375-126">See hello [**Basic Parameters**](#basic-parameters) section below for further details on parameters.</span></span>
5. <span data-ttu-id="c2375-127">Hola **trabajo de compilación** hoja se abre para que puede realizar un seguimiento de estado del trabajo de compilación de Hola y Hola configuraciones del nodo (documentos MOF de configuración) que ocasiona toobe colocado en hello servidor de extracción de DSC de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2375-127">hello **Compilation Job** blade is opened so that you can track hello compilation job's status, and hello node configurations (MOF configuration documents) it caused toobe placed on hello Azure Automation DSC Pull Server.</span></span>

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a><span data-ttu-id="c2375-128">Compilación de una configuración DSC con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2375-128">Compiling a DSC Configuration with Windows PowerShell</span></span>

<span data-ttu-id="c2375-129">Puede usar [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compilar con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2375-129">You can use [`Start-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compiling with Windows PowerShell.</span></span> <span data-ttu-id="c2375-130">Hola siguiente código de ejemplo inicia la compilación de una configuración de DSC conocida como **SampleConfig**.</span><span class="sxs-lookup"><span data-stu-id="c2375-130">hello following sample code starts compilation of a DSC configuration called **SampleConfig**.</span></span>

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

<span data-ttu-id="c2375-131">`Start-AzureRmAutomationDscCompilationJob`Devuelve una compilación de trabajos que se puede usar tootrack su estado de objeto.</span><span class="sxs-lookup"><span data-stu-id="c2375-131">`Start-AzureRmAutomationDscCompilationJob` returns a compilation job object that you can use tootrack its status.</span></span> <span data-ttu-id="c2375-132">A continuación, puede usar este objeto de trabajo de compilación con [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine estado de Hola de trabajo de compilación de Hola y [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview sus secuencias (salida).</span><span class="sxs-lookup"><span data-stu-id="c2375-132">You can then use this compilation job object with [`Get-AzureRmAutomationDscCompilationJob`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello status of hello compilation job, and [`Get-AzureRmAutomationDscCompilationJobOutput`](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview its streams (output).</span></span> <span data-ttu-id="c2375-133">Hola siguiente código de ejemplo inicia la compilación del programa Hola a **SampleConfig** configuración, espera hasta que se ha completado y, a continuación, muestra sus secuencias.</span><span class="sxs-lookup"><span data-stu-id="c2375-133">hello following sample code starts compilation of hello **SampleConfig** configuration, waits until it has completed, and then displays its streams.</span></span>

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a><span data-ttu-id="c2375-134">Parámetros básicos</span><span class="sxs-lookup"><span data-stu-id="c2375-134">Basic Parameters</span></span>
<span data-ttu-id="c2375-135">Declaración de parámetro en las configuraciones de DSC, incluidos los tipos de parámetros y propiedades, funciona igual Hola como en los runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2375-135">Parameter declaration in DSC configurations, including parameter types and properties, works hello same as in Azure Automation runbooks.</span></span> <span data-ttu-id="c2375-136">Vea [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md) toolearn más información acerca de los parámetros del runbook.</span><span class="sxs-lookup"><span data-stu-id="c2375-136">See [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toolearn more about runbook parameters.</span></span>

<span data-ttu-id="c2375-137">Hello en el ejemplo siguiente se utiliza dos parámetros llamados **NombreCaracterística** y **IsPresent**, valores de hello de toodetermine de propiedades de hello **ParametersExample.sample** nodo configuración, generada durante la compilación.</span><span class="sxs-lookup"><span data-stu-id="c2375-137">hello following example uses two parameters called **FeatureName** and **IsPresent**, toodetermine hello values of properties in hello **ParametersExample.sample** node configuration, generated during compilation.</span></span>

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

<span data-ttu-id="c2375-138">Puede compilar las configuraciones de DSC que usan parámetros básicos en el portal de DSC de automatización de Azure de Hola o con Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2375-138">You can compile DSC Configurations that use basic parameters in hello Azure Automation DSC portal, or with Azure PowerShell:</span></span>

### <a name="portal"></a><span data-ttu-id="c2375-139">Portal</span><span class="sxs-lookup"><span data-stu-id="c2375-139">Portal</span></span>

<span data-ttu-id="c2375-140">En el portal de hello, puede especificar valores de parámetro después de hacer clic **compilar**.</span><span class="sxs-lookup"><span data-stu-id="c2375-140">In hello portal, you can enter parameter values after clicking **Compile**.</span></span>

![texto alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a><span data-ttu-id="c2375-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2375-142">PowerShell</span></span>

<span data-ttu-id="c2375-143">PowerShell requiere parámetros en un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) donde clave Hola coincide con el nombre del parámetro de Hola y el valor de hello es igual al valor del parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="c2375-143">PowerShell requires parameters in a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key matches hello parameter name, and hello value equals hello parameter value.</span></span>

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

<span data-ttu-id="c2375-144">Para obtener información acerca de cómo pasar PSCredentials como parámetros, consulte más abajo la sección <a href="#credential-assets">**Recursos de credenciales**</a> .</span><span class="sxs-lookup"><span data-stu-id="c2375-144">For information about passing PSCredentials as parameters, see <a href="#credential-assets">**Credential Assets**</a> below.</span></span>

## <a name="configurationdata"></a><span data-ttu-id="c2375-145">ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="c2375-145">ConfigurationData</span></span>
<span data-ttu-id="c2375-146">**ConfigurationData** permite tooseparate configuración estructural de cualquier configuración específica del entorno durante el uso de DSC de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2375-146">**ConfigurationData** allows you tooseparate structural configuration from any environment specific configuration while using PowerShell DSC.</span></span> <span data-ttu-id="c2375-147">Vea [separar "Qué" de "Where" en el DSC de PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn más información sobre **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="c2375-147">See [Separating "What" from "Where" in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn more about **ConfigurationData**.</span></span>

> [!NOTE]
> <span data-ttu-id="c2375-148">Puede usar **ConfigurationData** cuando se compila en DSC de automatización de Azure con Azure PowerShell, pero no en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2375-148">You can use **ConfigurationData** when compiling in Azure Automation DSC using Azure PowerShell, but not in hello Azure portal.</span></span>

<span data-ttu-id="c2375-149">Hello ejemplo DSC configuración siguiente utiliza **ConfigurationData** a través de hello **$ConfigurationData** y **$AllNodes** palabras clave.</span><span class="sxs-lookup"><span data-stu-id="c2375-149">hello following example DSC configuration uses **ConfigurationData** via hello **$ConfigurationData** and **$AllNodes** keywords.</span></span> <span data-ttu-id="c2375-150">También necesitará hello [ **xWebAdministration** módulo](https://www.powershellgallery.com/packages/xWebAdministration/) en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c2375-150">You'll also need hello [**xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) for this example:</span></span>

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

<span data-ttu-id="c2375-151">Puede compilar la configuración de DSC Hola anteriormente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2375-151">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="c2375-152">Hola situada bajo PowerShell agrega dos toohello de configuraciones de nodo servidor de extracción de DSC de automatización de Azure: **ConfigurationDataSample.MyVM1** y **ConfigurationDataSample.MyVM3**:</span><span class="sxs-lookup"><span data-stu-id="c2375-152">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server: **ConfigurationDataSample.MyVM1** and **ConfigurationDataSample.MyVM3**:</span></span>

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

## <a name="assets"></a><span data-ttu-id="c2375-153">Recursos</span><span class="sxs-lookup"><span data-stu-id="c2375-153">Assets</span></span>

<span data-ttu-id="c2375-154">Referencias de activos son Hola igual en runbooks y las configuraciones de DSC de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2375-154">Asset references are hello same in Azure Automation DSC configurations and runbooks.</span></span> <span data-ttu-id="c2375-155">Vea Hola siguientes para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="c2375-155">See hello following for more information:</span></span>

* [<span data-ttu-id="c2375-156">Certificados</span><span class="sxs-lookup"><span data-stu-id="c2375-156">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="c2375-157">Conexiones</span><span class="sxs-lookup"><span data-stu-id="c2375-157">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="c2375-158">Credenciales</span><span class="sxs-lookup"><span data-stu-id="c2375-158">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="c2375-159">Variables</span><span class="sxs-lookup"><span data-stu-id="c2375-159">Variables</span></span>](automation-variables.md)

### <a name="credential-assets"></a><span data-ttu-id="c2375-160">Recursos de credenciales</span><span class="sxs-lookup"><span data-stu-id="c2375-160">Credential Assets</span></span>

<span data-ttu-id="c2375-161">Mientras que las configuraciones DSC en Azure Automation pueden hacer referencia a los recursos de credenciales mediante **Get-AzureRmAutomationCredential**, los recursos de credenciales también se pueden pasar mediante parámetros, si se desea.</span><span class="sxs-lookup"><span data-stu-id="c2375-161">While DSC configurations in Azure Automation can reference credential assets using **Get-AzureRmAutomationCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="c2375-162">Si una configuración toma un parámetro de **PSCredential** escribe, debe tener un nombre de cadena de hello toopass de un activo de credencial de automatización de Azure como valor del parámetro de ese, en lugar de un objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="c2375-162">If a configuration takes a parameter of **PSCredential** type, then you need toopass hello string name of an Azure Automation credential asset as that parameter’s value, rather than a PSCredential object.</span></span> <span data-ttu-id="c2375-163">Entre bastidores de hello, se recuperará y pasa toohello configuración activo de credencial de automatización de Azure Hola con ese nombre.</span><span class="sxs-lookup"><span data-stu-id="c2375-163">Behind hello scenes, hello Azure Automation credential asset with that name will be retrieved and passed toohello configuration.</span></span>

<span data-ttu-id="c2375-164">Mantener las credenciales seguras en configuraciones de nodo (documentos de configuración de MOF) requiere cifrado de credenciales de hello en el archivo MOF de configuración de nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2375-164">Keeping credentials secure in node configurations (MOF configuration documents) requires encrypting hello credentials in hello node configuration MOF file.</span></span> <span data-ttu-id="c2375-165">Automatización de Azure tiene un paso más y cifra el archivo MOF completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2375-165">Azure Automation takes this one step further and encrypts hello entire MOF file.</span></span> <span data-ttu-id="c2375-166">Sin embargo, actualmente debe indicar DSC de PowerShell es correcto para toobe de credenciales en texto sin formato que produce durante la generación de MOF de configuración de nodo, porque no sabe DSC de PowerShell que automatización de Azure se pueden cifrar archivo MOF de hello completa después de su generación a través de un trabajo de compilación.</span><span class="sxs-lookup"><span data-stu-id="c2375-166">However, currently you must tell PowerShell DSC it is okay for credentials toobe outputted in plain text during node configuration MOF generation, because PowerShell DSC doesn’t know that Azure Automation will be encrypting hello entire MOF file after its generation via a compilation job.</span></span>

<span data-ttu-id="c2375-167">Puede indicar que DSC de PowerShell que es correcto para toobe de credenciales que se va a producir en texto sin formato en la configuración de nodo de hello genera MOF con [ **ConfigurationData**](#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="c2375-167">You can tell PowerShell DSC that it is okay for credentials toobe outputted in plain text in hello generated node configuration MOFs using [**ConfigurationData**](#configurationdata).</span></span> <span data-ttu-id="c2375-168">Debería pasar `PSDscAllowPlainTextPassword = $true` a través de **ConfigurationData** para el nombre de cada bloque de nodo que aparece en la configuración de DSC de Hola y usa las credenciales.</span><span class="sxs-lookup"><span data-stu-id="c2375-168">You should pass `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** for each node block’s name that appears in hello DSC configuration and uses credentials.</span></span>

<span data-ttu-id="c2375-169">Hello en el ejemplo siguiente se muestra una configuración de DSC que usa un recurso de credencial de automatización.</span><span class="sxs-lookup"><span data-stu-id="c2375-169">hello following example shows a DSC configuration that uses an Automation credential asset.</span></span>

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

<span data-ttu-id="c2375-170">Puede compilar la configuración de DSC Hola anteriormente con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2375-170">You can compile hello DSC configuration above with PowerShell.</span></span> <span data-ttu-id="c2375-171">Hola situada bajo PowerShell agrega dos toohello de configuraciones de nodo servidor de extracción de DSC de automatización de Azure: **CredentialSample.MyVM1** y **CredentialSample.MyVM2**.</span><span class="sxs-lookup"><span data-stu-id="c2375-171">hello below PowerShell adds two node configurations toohello Azure Automation DSC Pull Server:  **CredentialSample.MyVM1** and **CredentialSample.MyVM2**.</span></span>

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

## <a name="importing-node-configurations"></a><span data-ttu-id="c2375-172">Importación de configuraciones de nodo</span><span class="sxs-lookup"><span data-stu-id="c2375-172">Importing node configurations</span></span>

<span data-ttu-id="c2375-173">También puede importar configuraciones de nodo (MOF) que se hayan compilado fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2375-173">You can also import node configuratons (MOFs) that you have compiled outside of Azure.</span></span> <span data-ttu-id="c2375-174">Una ventaja de esta posibilidad es que las configuraciones de nodo pueden estar firmadas.</span><span class="sxs-lookup"><span data-stu-id="c2375-174">One advantage of this is that node confiturations can be signed.</span></span>
<span data-ttu-id="c2375-175">Una configuración de nodo firmado se comprueba localmente en un nodo administrado por agente Hola DSC, asegurándose de que la configuración de hello está aplicada toohello nodo procede de un origen autorizado.</span><span class="sxs-lookup"><span data-stu-id="c2375-175">A signed node configuration is verified locally on a managed node by hello DSC agent, ensuring that hello configuration being applied toohello node comes from an authorized source.</span></span>

> [!NOTE]
> <span data-ttu-id="c2375-176">Puede usar importar configuraciones firmadas en su cuenta de Azure Automation, pero Azure Automation no admite actualmente la compilación de configuraciones firmadas.</span><span class="sxs-lookup"><span data-stu-id="c2375-176">You can use import signed configurations into your Azure Automation account, but Azure Automation does not currently support compiling signed configurations.</span></span>

> [!NOTE]
> <span data-ttu-id="c2375-177">Un archivo de configuración de nodo debe ser no superior a 1 MB tooallow se toobe importado en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2375-177">A node configuration file must be no larger than 1 MB tooallow it toobe imported into Azure Automation.</span></span>

<span data-ttu-id="c2375-178">Puede obtener información sobre cómo las configuraciones de nodo de toosign en https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span><span class="sxs-lookup"><span data-stu-id="c2375-178">You can learn how toosign node configurations at https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.</span></span>

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a><span data-ttu-id="c2375-179">Importar una configuración de nodo en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c2375-179">Importing a node configuration in hello Azure portal</span></span>

1. <span data-ttu-id="c2375-180">En su cuenta de Automation, haga clic en **DSC node configurations** (Configuraciones de nodo DSC).</span><span class="sxs-lookup"><span data-stu-id="c2375-180">From your Automation account, click **DSC node configurations**.</span></span>

    ![Configuraciones de nodo DSC](./media/automation-dsc-compile/node-config.png)
2. <span data-ttu-id="c2375-182">Hola **configuraciones del nodo DSC** hoja, haga clic en **agregar un NodeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="c2375-182">In hello **DSC node configurations** blade, click **Add a NodeConfiguration**.</span></span>
3. <span data-ttu-id="c2375-183">Hola **importación** hoja, haga clic en el icono de carpeta hello toohello siguiente **archivo de configuración de nodo** toobrowse de cuadro de texto para un archivo de configuración de nodo (MOF) en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="c2375-183">In hello **Import** blade, click hello folder icon next toohello **Node Configuration File** textbox toobrowse for a node configuration file (MOF) on your local computer.</span></span>

    ![Buscar archivo local](./media/automation-dsc-compile/import-browse.png)
4. <span data-ttu-id="c2375-185">Escriba un nombre en hello **nombre de configuración** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c2375-185">Enter a name in hello **Configuration Name** textbox.</span></span> <span data-ttu-id="c2375-186">Este nombre debe coincidir con hello de configuración de Hola desde el que se compiló la configuración del nodo Hola.</span><span class="sxs-lookup"><span data-stu-id="c2375-186">This name must match hello name of hello configuration from which hello node configuration was compiled.</span></span>
5. <span data-ttu-id="c2375-187">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c2375-187">Click **OK**.</span></span>

### <a name="importing-a-node-configuration-with-powershell"></a><span data-ttu-id="c2375-188">Importación de una configuración de nodo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2375-188">Importing a node configuration with PowerShell</span></span>

<span data-ttu-id="c2375-189">Puede usar hello [AzureRmAutomationDscNodeConfiguration de importación](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport una configuración de nodo en su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="c2375-189">You can use hello [Import-AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport a node configuration into your automation account.</span></span>

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



