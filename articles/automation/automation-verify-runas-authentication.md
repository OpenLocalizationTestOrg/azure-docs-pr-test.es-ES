---
title: "configuración de cuenta de automatización de Azure aaaValidate | Documentos de Microsoft"
description: "Este artículo describe la configuración de hello tooconfirm de su cuenta de automatización está configurado correctamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="0b6b9-103">Comprobación de la autenticación con la cuenta de ejecución de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0b6b9-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="0b6b9-104">Una vez se haya creado correctamente una cuenta de automatización, puede realizar un tooconfirm de prueba simple puede toosuccessfully autenticar en el Administrador de recursos de Azure o Azure implementación clásica usando su cuenta de automatización Run As recién creado o actualizado.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="0b6b9-105">Autenticación con la cuenta de ejecución de Automation</span><span class="sxs-lookup"><span data-stu-id="0b6b9-105">Automation Run As authentication</span></span>
<span data-ttu-id="0b6b9-106">Utilice el siguiente código de ejemplo de Hola demasiado[crear un runbook de PowerShell](automation-creating-importing-runbook.md) autenticación tooverify mediante Hola se ejecutan como cuenta de y también en su tooauthenticate runbooks personalizados y administrar los recursos del Administrador de recursos con su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="0b6b9-107">Observe Hola cmdlet que se usa para autenticar en runbook hello - **agregar AzureRmAccount**, usa Hola *ServicePrincipalCertificate* conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="0b6b9-108">Se autentica mediante el certificado de la entidad de servicio, no las credenciales.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="0b6b9-109">Cuando se [ejecutar runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate su cuenta de ejecución, un [trabajo del runbook](automation-runbook-execution.md) está creado, se muestra la hoja de trabajo de Hola y muestra el estado del trabajo de Hola Hola **trabajo resumen**icono.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="0b6b9-110">estado del trabajo Hola se iniciará como *en cola* que indica que está esperando un runbook worker en hello toobecome de nube disponible.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="0b6b9-111">A continuación, moverá demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="0b6b9-112">Cuando se completa el trabajo de runbook de hello, deberíamos ver estado **completado**.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="0b6b9-113">toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="0b6b9-114">En hello **salida** hoja, debería ver se ha autenticado correctamente y devuelve una lista de todos los recursos en todos los grupos de recursos en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="0b6b9-115">Recuerde solo bloque de hello tooremove de código a partir de comentarios de Hola `#Get all ARM resources from all resource groups` cuando reutilizar el código de hello para sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="0b6b9-116">Autenticación con la cuenta de ejecución del modelo de implementación clásica de Azure</span><span class="sxs-lookup"><span data-stu-id="0b6b9-116">Classic Run As authentication</span></span>
<span data-ttu-id="0b6b9-117">Utilice el siguiente código de ejemplo de Hola demasiado[crear un runbook de PowerShell](automation-creating-importing-runbook.md) tooverify autenticación mediante Hola clásico se ejecutan como cuenta de y también en su tooauthenticate runbooks personalizados y administrar recursos en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="0b6b9-118">Cuando se [ejecutar runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate su cuenta de ejecución, un [trabajo del runbook](automation-runbook-execution.md) está creado, se muestra la hoja de trabajo de Hola y muestra el estado del trabajo de Hola Hola **trabajo resumen**icono.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="0b6b9-119">estado del trabajo Hola se iniciará como *en cola* que indica que está esperando un runbook worker en hello toobecome de nube disponible.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="0b6b9-120">A continuación, moverá demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="0b6b9-121">Cuando se completa el trabajo de runbook de hello, deberíamos ver estado **completado**.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="0b6b9-122">toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="0b6b9-123">En hello **salida** hoja, debería ver se ha autenticado correctamente y devuelve una lista de todas las máquinas virtuales de Azure por VMName que se implementan en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="0b6b9-124">Recuerde tooremove Hola cmdlet **Get-AzureVM** cuando reutilizar el código de hello para sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b6b9-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b6b9-125">Next steps</span></span>
* <span data-ttu-id="0b6b9-126">tooget a trabajar con runbooks de PowerShell, consulte [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="0b6b9-127">toolearn más información acerca de la creación de gráficos, consulte [edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
