---
title: "Ejecución de runbooks en Azure Automation Hybrid Runbook Worker | Microsoft Docs"
description: "Este artículo proporciona información acerca de cómo ejecutar runbooks en máquinas de un centro de datos local o en el proveedor de la nube con el rol Hybrid Runbook Worker."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 993bc3ea480a329541ca4ae825189cdb5a2b4a8b
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="6c21e-103">Ejecución de runbooks en Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="6c21e-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="6c21e-104">No hay ninguna diferencia en la estructura de runbooks que se ejecutan en Automatización de Azure y los que se ejecutan en un Trabajo híbrido de runbook.</span><span class="sxs-lookup"><span data-stu-id="6c21e-104">There is no difference in the structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="6c21e-105">Los runbooks que usa con cada uno de ellos probablemente sean muy distintos entre sí, debido a que los runbooks destinados a Hybrid Runbook Worker normalmente administran los recursos en el propio equipo local donde se implementan, mientras que los runbooks en Azure Automation suelen hacerlo en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c21e-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on the local computer itself or against resources in the local environment where it is deployed, while runbooks in Azure Automation typically manage resources in the Azure cloud.</span></span>

<span data-ttu-id="6c21e-106">Puede editar un runbook para Trabajo híbrido de runbook en Automatización de Azure, pero es probable que tenga dificultades si intenta probar el runbook en el editor.</span><span class="sxs-lookup"><span data-stu-id="6c21e-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try to test the runbook in the editor.</span></span>  <span data-ttu-id="6c21e-107">Es posible que los módulos de PowerShell que tienen acceso a los recursos locales no estén instalados en el entorno de Automatización de Azure; si este es el caso, la prueba presentará errores.</span><span class="sxs-lookup"><span data-stu-id="6c21e-107">The PowerShell modules that access the local resources may not be installed in your Azure Automation environment in which case, the test would fail.</span></span>  <span data-ttu-id="6c21e-108">Si instala los módulos necesarios, se ejecutará el runbook, pero no podrá tener acceso a los recursos locales para una prueba completa.</span><span class="sxs-lookup"><span data-stu-id="6c21e-108">If you do install the required modules, then the runbook will run, but it will not be able to access local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="6c21e-109">Inicio de un runbook en Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="6c21e-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="6c21e-110">[Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) describe los distintos métodos para iniciar un runbook.</span><span class="sxs-lookup"><span data-stu-id="6c21e-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="6c21e-111">Trabajo híbrido de runbook agrega una opción **Ejecutar en** donde puede especificar el nombre de un grupo de Trabajos híbridos de runbook.</span><span class="sxs-lookup"><span data-stu-id="6c21e-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify the name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="6c21e-112">Si se especifica un grupo, los trabajos de ese grupo recuperan y ejecutan el runbook.</span><span class="sxs-lookup"><span data-stu-id="6c21e-112">If a group is specified, then the runbook is retrieved and run by of the workers in that group.</span></span>  <span data-ttu-id="6c21e-113">Si no se especifica esta opción, se ejecuta en Automatización de Azure de la manera normal.</span><span class="sxs-lookup"><span data-stu-id="6c21e-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="6c21e-114">Cuando inicie un runbook en Azure Portal, verá una opción **Ejecutar en** donde puede seleccionar **Azure** o **Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-114">When you start a runbook in the Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="6c21e-115">Si selecciona **Trabajo híbrido**, puede seleccionar el grupo en una lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="6c21e-115">If you select **Hybrid Worker**, then you can select the group from a dropdown.</span></span>

<span data-ttu-id="6c21e-116">Use el parámetro **RunOn**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-116">Use the **RunOn** parameter.</span></span>  <span data-ttu-id="6c21e-117">Puede usar el comando siguiente para iniciar un runbook llamado Test-Runbook en un grupo de Hybrid Runbook Worker denominado MyHybridGroup con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c21e-117">You can use the following command to start a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="6c21e-118">El parámetro **RunOn** se agregó al cmdlet **Start-AzureAutomationRunbook** en la versión 0.9.1 de Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c21e-118">The **RunOn** parameter was added to the **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="6c21e-119">Si tiene instalada una versión anterior, deberá [descargar la versión más reciente](https://azure.microsoft.com/downloads/) .</span><span class="sxs-lookup"><span data-stu-id="6c21e-119">You should [download the latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="6c21e-120">Solo necesita instalar esta versión en una estación de trabajo donde inicia el runbook desde Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c21e-120">You only need to install this version on a workstation where you are starting the runbook from Windows PowerShell.</span></span>  <span data-ttu-id="6c21e-121">No es necesario que la instale en el equipo de trabajo, a menos que tenga la intención de iniciar runbooks desde ese equipo.</span><span class="sxs-lookup"><span data-stu-id="6c21e-121">You do not need to install it on the worker computer unless you intend to start runbooks from that computer.</span></span>  <span data-ttu-id="6c21e-122">Actualmente no puede iniciar un runbook en un Trabajo híbrido de runbook desde otro runbook, debido a que esto requeriría que la versión más reciente de PowerShell de Azure esté instalada en su cuenta de Automatización.</span><span class="sxs-lookup"><span data-stu-id="6c21e-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require the latest version of Azure Powershell to be installed in your Automation account.</span></span>  <span data-ttu-id="6c21e-123">La versión más reciente se actualiza automáticamente en Azure Automation y pronto se insertará de manera automática en los trabajos.</span><span class="sxs-lookup"><span data-stu-id="6c21e-123">The latest version is automatically updated in Azure Automation and automatically pushed down to the workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="6c21e-124">Permisos de runbooks</span><span class="sxs-lookup"><span data-stu-id="6c21e-124">Runbook permissions</span></span>
<span data-ttu-id="6c21e-125">Los runbooks que se ejecutan en una instancia de Hybrid Runbook Worker no pueden usar el mismo método que se usa normalmente para los runbooks que se autentican en los recursos de Azure, debido a que tendrán acceso a recursos fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c21e-125">Runbooks running on a Hybrid Runbook Worker cannot use the same method that is typically used for runbooks authenticating to Azure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="6c21e-126">El runbook puede proporcionar su propia autenticación a los recursos locales, o puede especificar una cuenta RunAs para proporcionar un contexto de usuario para todos los runbooks.</span><span class="sxs-lookup"><span data-stu-id="6c21e-126">The runbook can either provide its own authentication to local resources, or you can specify a RunAs account to provide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="6c21e-127">Autenticación de runbook</span><span class="sxs-lookup"><span data-stu-id="6c21e-127">Runbook authentication</span></span>
<span data-ttu-id="6c21e-128">De forma predeterminada, los Runbooks se ejecutarán en el contexto de la cuenta de sistema local en el equipo local, por lo que deben proporcionar su propia autenticación a los recursos a los que tienen acceso.</span><span class="sxs-lookup"><span data-stu-id="6c21e-128">By default, runbooks will run in the context of the local System account on the on-premises computer, so they must provide their own authentication to resources that they will access.</span></span>  

<span data-ttu-id="6c21e-129">Puede usar los recursos [redencial](http://msdn.microsoft.com/library/dn940015.aspx) y [ertificado](http://msdn.microsoft.com/library/dn940013.aspx) en el Runbook con cmdlets que le permitan especificar las credenciales, para que así pueda autenticarse en distintos recursos.</span><span class="sxs-lookup"><span data-stu-id="6c21e-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you to specify credentials so you can authenticate to different resources.</span></span>  <span data-ttu-id="6c21e-130">El ejemplo siguiente muestra una porción de un runbook que reinicia un equipo.</span><span class="sxs-lookup"><span data-stu-id="6c21e-130">The following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="6c21e-131">Recupera las credenciales desde un recurso de Credencial y el nombre del equipo desde un recurso de Variable y, a continuación, usa estos valores con el cmdlet Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="6c21e-131">It retrieves credentials from a credential asset and the name of the computer from a variable asset and then uses these values with the Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="6c21e-132">También puede aprovechar [InlineScript](automation-powershell-workflow.md#inlinescript), que le permite ejecutar bloques de código en otro equipo con credenciales especificadas por el [parámetro común PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c21e-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you to run blocks of code on another computer with credentials specified by the [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="6c21e-133">Cuenta RunAs</span><span class="sxs-lookup"><span data-stu-id="6c21e-133">RunAs account</span></span>
<span data-ttu-id="6c21e-134">En lugar de hacer que los runbooks proporcionen su propia autenticación a los recursos locales, puede especificar una cuenta **RunAs** para un grupo de Hybrid Worker.</span><span class="sxs-lookup"><span data-stu-id="6c21e-134">Instead of having runbooks provide their own authentication to local resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="6c21e-135">Especifique un [recurso de credencial](automation-credentials.md) que tenga acceso a los recursos locales. Todos los runbooks se ejecutan con estas credenciales si se ejecutan en una instancia de Hybrid Runbook Worker del grupo.</span><span class="sxs-lookup"><span data-stu-id="6c21e-135">You specify a [credential asset](automation-credentials.md) that has access to local resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in the group.</span></span>  

<span data-ttu-id="6c21e-136">El nombre de usuario de la credencial debe tener uno de los siguientes formatos:</span><span class="sxs-lookup"><span data-stu-id="6c21e-136">The user name for the credential must be in one of the following formats:</span></span>

* <span data-ttu-id="6c21e-137">dominio\nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="6c21e-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="6c21e-138">nombre de usuario (para cuentas locales en el equipo local)</span><span class="sxs-lookup"><span data-stu-id="6c21e-138">username (for accounts local to the on-premises computer)</span></span>

<span data-ttu-id="6c21e-139">Utilice el procedimiento siguiente para especificar una cuenta RunAs de un grupo de Hybrid Worker:</span><span class="sxs-lookup"><span data-stu-id="6c21e-139">Use the following procedure to specify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="6c21e-140">Cree un [recurso de credencial](automation-credentials.md) con acceso a los recursos locales.</span><span class="sxs-lookup"><span data-stu-id="6c21e-140">Create a [credential asset](automation-credentials.md) with access to local resources.</span></span>
2. <span data-ttu-id="6c21e-141">Abra la cuenta de Automatización en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c21e-141">Open the Automation account in the Azure portal.</span></span>
3. <span data-ttu-id="6c21e-142">Seleccione el icono **Grupos de Hybrid Worker** y luego seleccione el grupo.</span><span class="sxs-lookup"><span data-stu-id="6c21e-142">Select the **Hybrid Worker Groups** tile, and then select the group.</span></span>
4. <span data-ttu-id="6c21e-143">Seleccione **Toda la configuración** y luego **Configuración del grupo de Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="6c21e-144">Cambie **Ejecutar como** de **Predeterminado** a **Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-144">Change **Run As** from **Default** to **Custom**.</span></span>
6. <span data-ttu-id="6c21e-145">Seleccione la credencial y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-145">Select the credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="6c21e-146">Cuenta de ejecución de Automation</span><span class="sxs-lookup"><span data-stu-id="6c21e-146">Automation Run As account</span></span>
<span data-ttu-id="6c21e-147">Como parte del proceso de compilación automatizado para implementar recursos en Azure, es posible que sea necesario acceder a los sistemas locales para admitir una tarea o conjunto de pasos en la secuencia de implementación.</span><span class="sxs-lookup"><span data-stu-id="6c21e-147">As part of your automated build process for deploying resources in Azure, you may require access to on-premise systems to support a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="6c21e-148">A fin de admitir la autenticación en Azure mediante la cuenta de ejecución, debe instalar el certificado de la cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c21e-148">To support authentication against Azure using the Run As account, you need to install the Run As account certificate.</span></span>  

<span data-ttu-id="6c21e-149">El siguiente runbook de PowerShell, *Export-RunAsCertificateToHybridWorker*, exporta el certificado de ejecución desde la cuenta de Azure Automation y lo descarga e importa en el almacén de certificados de la máquina local de un Hybrid Worker conectado a la misma cuenta.</span><span class="sxs-lookup"><span data-stu-id="6c21e-149">The following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports the Run As certificate from your Azure Automation account and downloads and imports it into the local machine certificate store on a Hybrid worker connected to the same account.</span></span>  <span data-ttu-id="6c21e-150">Una vez completado dicho paso, comprueba que el trabajo puede autenticarse correctamente en Azure con la cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c21e-150">Once that step is completed, it verifies the worker can successfully authenticate to Azure using the Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports the Run As certificate from an Azure Automation account to a hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports the Run As certificate from an Azure Automation account to a hybrid worker in that account.
    Run this runbook in the hybrid worker where you want the certificate installed.
    This allows the use of the AzureRunAsConnection to authenticate to Azure and manage Azure resources from runbooks running in the hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set the password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get the management certificate that will be used to make calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location to store temporary certificate in the Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save the certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication to Azure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts to confirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="6c21e-151">Guarde el runbook *Export-RunAsCertificateToHybridWorker* en el equipo con una extensión `.ps1`.</span><span class="sxs-lookup"><span data-stu-id="6c21e-151">Save the *Export-RunAsCertificateToHybridWorker* runbook to your computer with a `.ps1` extension.</span></span>  <span data-ttu-id="6c21e-152">Impórtelo en la cuenta de Automation y edite el runbook, cambiando el valor de la variable `$Password` con su propia contraseña.</span><span class="sxs-lookup"><span data-stu-id="6c21e-152">Import it into your Automation account and edit the runbook, changing the value of the variable `$Password` with your own password.</span></span>  <span data-ttu-id="6c21e-153">Publique y, a continuación, ejecute el runbook dirigido al grupo de Hybrid Worker que ejecuta y autentica runbooks con la cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6c21e-153">Publish and then run the runbook targeting the Hybrid Worker group that run and authenticate runbooks using the Run As account.</span></span>  <span data-ttu-id="6c21e-154">La transmisión del trabajo informa sobre el intento de importar el certificado en el almacén de la máquina local y sigue con varias líneas dependiendo del número de cuentas de Automation definidas en la suscripción y de si la autenticación se realiza correctamente.</span><span class="sxs-lookup"><span data-stu-id="6c21e-154">The job stream reports the attempt to import the certificate into the local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="6c21e-155">Solución de problemas de runbooks en Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="6c21e-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="6c21e-156">Los registros se almacenan localmente en cada Hybrid Worker en C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="6c21e-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="6c21e-157">Hybrid Worker también registra los errores y eventos en el registro de eventos de Windows, en **Registros de aplicaciones y servicios\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-157">Hybrid worker also records errors and events in the Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="6c21e-158">Los eventos relacionados con los runbooks ejecutados en el trabajo de runbook se escriben en **Registros de aplicaciones y servicios\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="6c21e-158">Events related to runbooks executed on the worker are written to **Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="6c21e-159">El registro **Microsoft SMA** incluye muchos más eventos relacionados con los procesos de runbook insertados en el trabajo de runbook y el procesamiento del runbook.</span><span class="sxs-lookup"><span data-stu-id="6c21e-159">The **Microsoft-SMA** log includes many more events related to the runbook job pushed to the worker and the processing of the runbook.</span></span>  <span data-ttu-id="6c21e-160">Aunque el registro de eventos **Microsoft-Automation** no tenga muchos eventos con detalles relacionados con la solución de problemas de ejecución de un runbook, al menos encontrará los resultados del trabajo de runbook.</span><span class="sxs-lookup"><span data-stu-id="6c21e-160">While the **Microsoft-Automation** event log does not have many events with details assisting with the troubleshooting of runbook execution, you will at least find the results of the runbook job.</span></span>  

<span data-ttu-id="6c21e-161">[La salida y los mensajes de runbooks](automation-runbook-output-and-messages.md) se envían a Automatización de Azure desde los trabajos híbridos igual que los trabajos de runbook que se ejecutan en la nube.</span><span class="sxs-lookup"><span data-stu-id="6c21e-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span>  <span data-ttu-id="6c21e-162">También puede habilitar los flujos Detallado y Progreso de la misma manera que haría para otros runbooks.</span><span class="sxs-lookup"><span data-stu-id="6c21e-162">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>  

<span data-ttu-id="6c21e-163">Si sus runbooks no están finalizando correctamente y el resumen del trabajo muestra el estado **Suspendido**, consulte el artículo de solución de problemas [Hybrid Runbook Worker: un trabajo de Runbook finaliza con el estado Suspendido](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="6c21e-163">If your runbooks are not completing successfully and the job summary shows a status of **Suspended**, please review the troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6c21e-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c21e-164">Next steps</span></span>
* <span data-ttu-id="6c21e-165">Para más información sobre los distintos métodos que se pueden utilizar para iniciar un runbook, consulte [Inicio de un runbook en Azure Automation](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="6c21e-165">To learn more about the different methods that can be used to start a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="6c21e-166">Para entender los diferentes procedimientos para trabajar con runbooks de PowerShell y de flujo de trabajo de PowerShell en Automatización de Azure mediante el editor de texto, consulte [Edición de runbooks de texto en Automatización de Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="6c21e-166">To understand the different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using the textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>