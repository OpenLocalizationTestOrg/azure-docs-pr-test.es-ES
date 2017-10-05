---
title: Paso de un objeto JSON a un runbook de Azure Automation | Microsoft Docs
description: "Procedimiento para pasar parámetros a un runbook como un objeto JSON"
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
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="380e8-104">Paso de un objeto JSON a un runbook de Azure Automation</span><span class="sxs-lookup"><span data-stu-id="380e8-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="380e8-105">Puede ser útil almacenar los datos que desea pasar a un runbook en un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="380e8-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="380e8-106">Por ejemplo, podría crear un archivo JSON que contiene todos los parámetros que desea pasar a un runbook.</span><span class="sxs-lookup"><span data-stu-id="380e8-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="380e8-107">Para hacerlo, debe convertir el archivo JSON en una cadena y luego convertir esta cadena en un objeto de PowerShell antes de pasar el contenido al runbook.</span><span class="sxs-lookup"><span data-stu-id="380e8-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="380e8-108">En este ejemplo, se creará un script de PowerShell que llamará a [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) para iniciar un runbook de PowerShell, pasando el contenido del archivo JSON al runbook.</span><span class="sxs-lookup"><span data-stu-id="380e8-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="380e8-109">El runbook de PowerShell inicia una máquina virtual de Azure y se obtienen los parámetros de la máquina virtual desde el archivo JSON que se pasó.</span><span class="sxs-lookup"><span data-stu-id="380e8-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="380e8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="380e8-110">Prerequisites</span></span>
<span data-ttu-id="380e8-111">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="380e8-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="380e8-112">Suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="380e8-112">Azure subscription.</span></span> <span data-ttu-id="380e8-113">Si aún no tiene ninguna, puede [activar las ventajas de la suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o <a href="/pricing/free-account/" target="_blank">[registrarse para obtener una cuenta gratis](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="380e8-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="380e8-114">[Cuenta de Automatización](automation-sec-configure-azure-runas-account.md) para contener el Runbook y autenticarse en recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="380e8-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="380e8-115">Esta cuenta debe tener permiso para iniciar y detener la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="380e8-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="380e8-116">Una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="380e8-116">An Azure virtual machine.</span></span> <span data-ttu-id="380e8-117">Detendremos e iniciaremos esta máquina, por lo que no debería ser una máquina virtual de producción.</span><span class="sxs-lookup"><span data-stu-id="380e8-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="380e8-118">Azure Powershell instalado en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="380e8-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="380e8-119">Consulte [Instalación y configuración de Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para información sobre cómo obtener Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="380e8-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="380e8-120">Creación del archivo JSON</span><span class="sxs-lookup"><span data-stu-id="380e8-120">Create the JSON file</span></span>

<span data-ttu-id="380e8-121">Escriba el texto siguiente en un archivo de texto y guárdelo como `test.json` en algún lugar del equipo local.</span><span class="sxs-lookup"><span data-stu-id="380e8-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="380e8-122">Creación del runbook</span><span class="sxs-lookup"><span data-stu-id="380e8-122">Create the runbook</span></span>

<span data-ttu-id="380e8-123">Cree un runbook de PowerShell denominado "Test-Json" en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="380e8-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="380e8-124">Para saber cómo crear un runbook de PowerShell, consulte [Mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="380e8-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="380e8-125">Para aceptar los datos de JSON, el runbook debe tomar un objeto como parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="380e8-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="380e8-126">De ese modo, el runbook puede usar las propiedades definidas en el archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="380e8-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="380e8-127">Guarde y publique este runbook en su cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="380e8-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="380e8-128">Llamada al runbook desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="380e8-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="380e8-129">Ahora puede llamar al runbook desde la máquina local mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="380e8-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="380e8-130">Ejecute los comandos de PowerShell siguientes:</span><span class="sxs-lookup"><span data-stu-id="380e8-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="380e8-131">Inicie sesión en Azure:</span><span class="sxs-lookup"><span data-stu-id="380e8-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="380e8-132">Se le pedirá que escriba las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="380e8-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="380e8-133">Obtenga el contenido del archivo JSON y conviértalo en una cadena:</span><span class="sxs-lookup"><span data-stu-id="380e8-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="380e8-134">`JsonPath` es la ruta de acceso donde se guardó el archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="380e8-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="380e8-135">Convierta el contenido de la cadena de `$json` en un objeto de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="380e8-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="380e8-136">Cree una tabla hash para los parámetros de `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="380e8-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="380e8-137">Tenga en cuenta que se establece el valor de `Parameters` en el objeto de PowerShell que contiene los valores desde el archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="380e8-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="380e8-138">Inicio del runbook</span><span class="sxs-lookup"><span data-stu-id="380e8-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="380e8-139">El runbook usa los valores del archivo JSON para iniciar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="380e8-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="380e8-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="380e8-140">Next steps</span></span>

* <span data-ttu-id="380e8-141">Para más información acerca de la edición de runbooks de PowerShell y flujo de trabajo de PowerShell, consulte [Edición de runbooks de texto en Automatización de Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="380e8-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="380e8-142">Para información sobre cómo crear e importar runbooks, consulte [Creación o importación de un runbook en Azure Automation](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="380e8-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


