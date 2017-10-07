---
title: "aaaPass JSON objeto tooan runbook de automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toopass parámetros tooa runbook como un objeto JSON"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell, runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="b3827-104">Pasar un runbook de automatización de Azure de tooan de objeto JSON</span><span class="sxs-lookup"><span data-stu-id="b3827-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="b3827-105">Puede ser datos toostore útil que desea toopass tooa runbook en un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="b3827-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="b3827-106">Por ejemplo, podría crear un archivo JSON que contiene todos los parámetros de hello desea toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="b3827-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="b3827-107">toodo, tiene tooconvert Hola JSON tooa cadena y, a continuación, convertir Hola string tooa PowerShell (objeto) antes de pasar su runbook toohello de contenido.</span><span class="sxs-lookup"><span data-stu-id="b3827-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="b3827-108">En este ejemplo, vamos a crear un script de PowerShell que llame [AzureRmAutomationRunbook inicio](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook de PowerShell, pasar el contenido de Hola de hello JSON toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="b3827-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="b3827-109">Hola PowerShell runbook inicia una máquina virtual de Azure, obtiene los parámetros de Hola para hello VM de Hola JSON que se pasó en.</span><span class="sxs-lookup"><span data-stu-id="b3827-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3827-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b3827-110">Prerequisites</span></span>
<span data-ttu-id="b3827-111">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b3827-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b3827-112">Suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3827-112">Azure subscription.</span></span> <span data-ttu-id="b3827-113">Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b3827-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b3827-114">[Cuenta de automatización](automation-sec-configure-azure-runas-account.md) toohold Hola runbook y autenticar tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="b3827-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="b3827-115">Esta cuenta debe tener permiso toostart y detener la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3827-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="b3827-116">Una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3827-116">An Azure virtual machine.</span></span> <span data-ttu-id="b3827-117">Detendremos e iniciaremos esta máquina, por lo que no debería ser una máquina virtual de producción.</span><span class="sxs-lookup"><span data-stu-id="b3827-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="b3827-118">Azure Powershell instalado en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="b3827-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="b3827-119">Vea [instalar y configurar Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obtener información acerca de cómo tooget PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3827-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="b3827-120">Crear archivo JSON de hello</span><span class="sxs-lookup"><span data-stu-id="b3827-120">Create hello JSON file</span></span>

<span data-ttu-id="b3827-121">Escriba lo siguiente Hola de prueba en un archivo de texto y guárdelo como `test.json` en algún lugar en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="b3827-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="b3827-122">Crear Hola runbook</span><span class="sxs-lookup"><span data-stu-id="b3827-122">Create hello runbook</span></span>

<span data-ttu-id="b3827-123">Cree un runbook de PowerShell denominado "Test-Json" en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b3827-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="b3827-124">toolearn toocreate un nuevo runbook de PowerShell, vea [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b3827-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="b3827-125">datos JSON de tooaccept hello, Hola runbook debe tomar un objeto como un parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="b3827-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="b3827-126">Hola runbook, a continuación, puede usar propiedades de hello definidas en hello JSON.</span><span class="sxs-lookup"><span data-stu-id="b3827-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="b3827-127">Guarde y publique este runbook en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="b3827-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="b3827-128">Llamada Hola runbook de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3827-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="b3827-129">Ahora puede llamar a runbook Hola desde el equipo local mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3827-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="b3827-130">Ejecute hello siga los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b3827-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="b3827-131">Inicie sesión en tooAzure:</span><span class="sxs-lookup"><span data-stu-id="b3827-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="b3827-132">Se está tooenter solicitada sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3827-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="b3827-133">Para obtener contenido de hello del archivo JSON de hello y convertir tooa cadena:</span><span class="sxs-lookup"><span data-stu-id="b3827-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="b3827-134">`JsonPath`es la ruta de acceso de Hola donde guardó el archivo JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="b3827-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="b3827-135">Convertir el contenido de la cadena de hello `$json` tooa objeto de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b3827-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="b3827-136">Crear una tabla hash para los parámetros de Hola para `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="b3827-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="b3827-137">Tenga en cuenta que se va a establecer valor de Hola de `Parameters` toohello objeto de PowerShell que contiene valores de hello de archivo JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="b3827-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="b3827-138">Iniciar runbook Hola</span><span class="sxs-lookup"><span data-stu-id="b3827-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="b3827-139">Hola runbook usa valores de hello de hello JSON archivo toostart una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b3827-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3827-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3827-140">Next steps</span></span>

* <span data-ttu-id="b3827-141">toolearn más información acerca de la edición de runbooks de flujo de trabajo de PowerShell y PowerShell con un editor de texto, consulte [edición textuales runbooks en automatización de Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="b3827-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="b3827-142">toolearn más información sobre la creación e importación de runbooks, vea [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="b3827-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


