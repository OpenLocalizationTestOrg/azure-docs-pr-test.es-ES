---
title: "aaaRun runbooks en Hybrid Runbook Worker de automatización de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información acerca de cómo ejecutar runbooks en equipos de su centro de datos local o el proveedor de nube con el rol de hello Hybrid Runbook Worker."
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
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="0eef3-103">Ejecución de runbooks en Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="0eef3-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="0eef3-104">No hay ninguna diferencia en la estructura de Hola de runbooks que se ejecutan en automatización de Azure y los que se ejecutan en un Runbook Worker híbrido.</span><span class="sxs-lookup"><span data-stu-id="0eef3-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="0eef3-105">Runbooks que se utilizan con cada uno de ellos más probable es que difieren de forma significativa aunque runbooks que se dirige a un Runbook Worker híbrido normalmente administran recursos en el mismo equipo local de Hola o con recursos en entorno local de Hola donde se implementa, mientras runbooks en la automatización de Azure suelen administrar recursos de nube de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="0eef3-106">Puede editar un runbook para Hybrid Runbook Worker de automatización de Azure, pero puede tener dificultades si intentas tootest Hola runbook en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="0eef3-107">módulos de PowerShell de Hola que tienen acceso a recursos locales de hello podrán no esté instalados en su entorno de automatización de Azure en cuyo caso, no podrá prueba Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="0eef3-108">Si instala Hola necesario módulos, a continuación, Hola runbook se ejecutará, pero no será capaz de tooaccess recursos locales para una prueba completa.</span><span class="sxs-lookup"><span data-stu-id="0eef3-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="0eef3-109">Inicio de un runbook en Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="0eef3-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="0eef3-110">[Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) describe los distintos métodos para iniciar un runbook.</span><span class="sxs-lookup"><span data-stu-id="0eef3-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="0eef3-111">Hybrid Runbook Worker agrega un **RunOn** opción donde puede especificar el nombre de Hola de un grupo de Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="0eef3-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="0eef3-112">Si se especifica un grupo, a continuación, Hola runbook recuperan y ejecutar de trabajadores de hello en ese grupo.</span><span class="sxs-lookup"><span data-stu-id="0eef3-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="0eef3-113">Si no se especifica esta opción, se ejecuta en Automatización de Azure de la manera normal.</span><span class="sxs-lookup"><span data-stu-id="0eef3-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="0eef3-114">Cuando se inicia un runbook en hello portal de Azure, se le presentará una **ejecutar en** opción donde puede seleccionar **Azure** o **Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="0eef3-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="0eef3-115">Si selecciona **Hybrid Worker**, después, puede seleccionar el grupo de hello en una lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="0eef3-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="0eef3-116">Hola de uso **RunOn** parámetro.</span><span class="sxs-lookup"><span data-stu-id="0eef3-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="0eef3-117">Puede usar Hola después comando toostart un runbook denominado Test-Runbook en un grupo de Hybrid Runbook Worker denominado MyHybridGroup mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eef3-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="0eef3-118">Hola **RunOn** parámetro agregó toohello **Start-AzureAutomationRunbook** cmdlet en la versión 0.9.1 de Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eef3-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="0eef3-119">Debería [descargar la versión más reciente de hello](https://azure.microsoft.com/downloads/) si tienes una anterior instalada.</span><span class="sxs-lookup"><span data-stu-id="0eef3-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="0eef3-120">Solo necesita tooinstall esta versión en una estación de trabajo donde está iniciando runbook Hola desde Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eef3-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="0eef3-121">No es necesario tooinstall en el equipo de trabajo de Hola a menos que piense toostart runbooks desde ese equipo.</span><span class="sxs-lookup"><span data-stu-id="0eef3-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="0eef3-122">Actualmente no se puede iniciar un runbook en un Hybrid Runbook Worker desde otro runbook, ya que esto requeriría la versión más reciente de Hola de toobe de Powershell de Azure instalado en su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="0eef3-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="0eef3-123">versión más reciente de Hola se actualizan automáticamente en automatización de Azure y automáticamente trasladará trabajadores toohello pronto.</span><span class="sxs-lookup"><span data-stu-id="0eef3-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="0eef3-124">Permisos de runbooks</span><span class="sxs-lookup"><span data-stu-id="0eef3-124">Runbook permissions</span></span>
<span data-ttu-id="0eef3-125">Runbooks que se ejecutan en un Runbook Worker híbrido no puede usar Hola mismo método que se utiliza normalmente para runbooks autenticar tooAzure recursos, ya que obtiene acceso a recursos fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eef3-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="0eef3-126">Hola runbook puede proporcionar su propia autenticación toolocal recursos, o bien puede especificar un tooprovide de cuenta de RunAs un contexto de usuario para todos los runbooks.</span><span class="sxs-lookup"><span data-stu-id="0eef3-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="0eef3-127">Autenticación de runbook</span><span class="sxs-lookup"><span data-stu-id="0eef3-127">Runbook authentication</span></span>
<span data-ttu-id="0eef3-128">De forma predeterminada, los runbooks se ejecutarán en el contexto de saludo de la cuenta de sistema local de hello en el equipo local de hello, por lo que deben proporcionar sus propios tooresources de autenticación que tendrá acceso.</span><span class="sxs-lookup"><span data-stu-id="0eef3-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="0eef3-129">Puede usar [credencial](http://msdn.microsoft.com/library/dn940015.aspx) y [certificado](http://msdn.microsoft.com/library/dn940013.aspx) activos en su runbook con los cmdlets que le permiten toospecify credenciales para poder autenticar a los recursos de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="0eef3-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="0eef3-130">Hello en el ejemplo siguiente se muestra una parte de un runbook que se reinicia un equipo.</span><span class="sxs-lookup"><span data-stu-id="0eef3-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="0eef3-131">Recupera las credenciales de un nombre de credencial hello y activos del equipo de Hola desde un recurso de variable y, a continuación, usa estos valores con el cmdlet de hello Restart-Computer.</span><span class="sxs-lookup"><span data-stu-id="0eef3-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="0eef3-132">También puede aprovechar la [InlineScript](automation-powershell-workflow.md#inlinescript), que le permite toorun bloques de código en otro equipo con las credenciales especificadas por hello [parámetro común de PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="0eef3-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="0eef3-133">Cuenta RunAs</span><span class="sxs-lookup"><span data-stu-id="0eef3-133">RunAs account</span></span>
<span data-ttu-id="0eef3-134">En lugar de tener runbooks proporcionar su propia autenticación toolocal recursos, puede especificar un **RunAs** cuenta para un grupo de Hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="0eef3-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="0eef3-135">Especifica un [activo de credencial](automation-credentials.md) que tiene acceso a los recursos de toolocal y todos los runbooks se ejecutan en estas credenciales cuando se ejecuta en un Hybrid Runbook Worker en grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="0eef3-136">nombre de usuario de Hello para la credencial de hello debe estar en uno de hello siguientes formatos:</span><span class="sxs-lookup"><span data-stu-id="0eef3-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="0eef3-137">dominio\nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="0eef3-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="0eef3-138">nombre de usuario (por equipo de cuentas local toohello local)</span><span class="sxs-lookup"><span data-stu-id="0eef3-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="0eef3-139">Usar hello siguiendo el procedimiento toospecify una cuenta de ejecución para un grupo de Hybrid worker:</span><span class="sxs-lookup"><span data-stu-id="0eef3-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="0eef3-140">Crear un [activo de credencial](automation-credentials.md) con acceso a los recursos de toolocal.</span><span class="sxs-lookup"><span data-stu-id="0eef3-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="0eef3-141">Abrir cuenta de automatización de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0eef3-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="0eef3-142">Seleccione hello **grupos de trabajo híbrido** icono y, a continuación, seleccione el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="0eef3-143">Seleccione **Toda la configuración** y luego **Configuración del grupo de Hybrid Worker**.</span><span class="sxs-lookup"><span data-stu-id="0eef3-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="0eef3-144">Cambio **ejecución** de **predeterminado** demasiado**personalizado**.</span><span class="sxs-lookup"><span data-stu-id="0eef3-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="0eef3-145">Seleccione la credencial de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0eef3-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="0eef3-146">Cuenta de ejecución de Automation</span><span class="sxs-lookup"><span data-stu-id="0eef3-146">Automation Run As account</span></span>
<span data-ttu-id="0eef3-147">Como parte del proceso automatizado de compilación para implementar recursos en Azure, puede requerir acceso local tooon sistemas toosupport una tarea o un conjunto de pasos en la secuencia de implementación.</span><span class="sxs-lookup"><span data-stu-id="0eef3-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="0eef3-148">autenticación de toosupport con Azure con la cuenta de identificación de hello, debe tooinstall Hola ejecutar como certificado de cuenta.</span><span class="sxs-lookup"><span data-stu-id="0eef3-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="0eef3-149">Hola siguiente runbook de PowerShell, *RunAsCertificateToHybridWorker de exportación*, exporta Hola ejecutar como certificado de la cuenta de automatización de Azure y descarga y lo importa en el almacén de certificados del equipo local de hello en un Worker híbrido conectado toohello misma cuenta.</span><span class="sxs-lookup"><span data-stu-id="0eef3-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="0eef3-150">Una vez completado este paso, comprueba trabajo Hola puede autenticar correctamente tooAzure con hello cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0eef3-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

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
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="0eef3-151">Guardar hello *exportación RunAsCertificateToHybridWorker* runbook tooyour equipo con un `.ps1` extensión.</span><span class="sxs-lookup"><span data-stu-id="0eef3-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="0eef3-152">Importar a la cuenta de automatización y editar runbook hello, cambiar valor Hola de variable de hello `$Password` con su propia contraseña.</span><span class="sxs-lookup"><span data-stu-id="0eef3-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="0eef3-153">Publicar y, a continuación, ejecutar runbook Hola grupo Hybrid Worker de Hola que se ejecutan y autenticar runbooks mediante Hola cuenta de ejecución de destino.</span><span class="sxs-lookup"><span data-stu-id="0eef3-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="0eef3-154">Hola trabajo flujo informes Hola intento tooimport Hola certificado en el almacén del equipo local de Hola y sigue con varias líneas, dependiendo de cuántas de las cuentas de automatización se definen en la suscripción y si la autenticación es correcta.</span><span class="sxs-lookup"><span data-stu-id="0eef3-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="0eef3-155">Solución de problemas de runbooks en Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="0eef3-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="0eef3-156">Los registros se almacenan localmente en cada Hybrid Worker en C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="0eef3-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="0eef3-157">Worker híbrido también registra los errores y eventos en el registro de eventos de Windows hello en **aplicaciones y servicios Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="0eef3-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="0eef3-158">Eventos relacionados con toorunbooks que se ejecuta en el trabajo de Hola se escriben demasiado**aplicaciones y servicios Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="0eef3-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="0eef3-159">Hola **Microsoft SMA** registro incluye muchos más eventos relacionados toohello runbook toohello insertado hello y trabajo procesamiento de trabajos de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="0eef3-160">Mientras hello **automatización de Microsoft** registro de eventos no tiene muchos eventos con detalles a prestar asistencia con hello solución de problemas de ejecución de un runbook, al menos, encontrará resultados Hola de trabajo de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="0eef3-161">[Runbook de salida y mensajes](automation-runbook-output-and-messages.md) se envían tooAzure automatización de hybrid Worker simplemente como trabajos de runbook en la nube Hola.</span><span class="sxs-lookup"><span data-stu-id="0eef3-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="0eef3-162">También puede habilitar Hola detallado y Hola secuencias de progreso de la misma manera que lo haría para otros runbooks.</span><span class="sxs-lookup"><span data-stu-id="0eef3-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="0eef3-163">Si no se completan correctamente los runbooks y resumen de trabajos de hello muestra un estado de **Suspended**, revise el artículo de solución de problemas de hello [Hybrid Runbook Worker: un trabajo de runbook finaliza con el estado Suspende](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="0eef3-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="0eef3-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0eef3-164">Next steps</span></span>
* <span data-ttu-id="0eef3-165">toolearn más información acerca de métodos diferentes de Hola que pueden ser utilizado toostart un runbook, consulte [a partir de un Runbook en automatización de Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="0eef3-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="0eef3-166">toounderstand Hola diferentes procedimientos para trabajar con runbooks de flujo de trabajo de PowerShell y PowerShell en automatización de Azure mediante el editor de texto hello, vea [editar un Runbook en automatización de Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0eef3-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
