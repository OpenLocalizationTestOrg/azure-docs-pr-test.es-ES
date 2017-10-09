---
title: plantillas de aaaDeploy con PowerShell en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy una máquina virtual mediante una plantilla de administrador de recursos y PowerShell."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: fb0d4b190e058b3c5c1273b6c91fc3d72dedeb1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a><span data-ttu-id="1cfca-103">Implementación de plantillas en Azure Stack con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cfca-103">Deploy templates in Azure Stack using PowerShell</span></span>
<span data-ttu-id="1cfca-104">Usar PowerShell toodeploy Azure Resource Manager plantillas toohello Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cfca-104">Use PowerShell toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span>  <span data-ttu-id="1cfca-105">Las plantillas de Resource Manager implementan y aprovisionan todos los recursos para su aplicación en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="1cfca-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span></span>

## <a name="run-azurerm-powershell-cmdlets"></a><span data-ttu-id="1cfca-106">Ejecución de cmdlets de AzureRM PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cfca-106">Run AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="1cfca-107">En este ejemplo, ejecute una secuencia de comandos toodeploy un Kit de desarrollo de pila mediante una plantilla de administrador de recursos de máquina virtual tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1cfca-107">In this example, you run a script toodeploy a virtual machine tooAzure Stack Development Kit using a Resource Manager template.</span></span>  <span data-ttu-id="1cfca-108">Antes de continuar, asegúrese de haber [configurado PowerShell](azure-stack-powershell-configure-user.md)</span><span class="sxs-lookup"><span data-stu-id="1cfca-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure-user.md)</span></span>  

<span data-ttu-id="1cfca-109">Hola VHD que se utiliza en esta plantilla de ejemplo es Windows Server 2012 R2 centros.</span><span class="sxs-lookup"><span data-stu-id="1cfca-109">hello VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span></span>

1. <span data-ttu-id="1cfca-110">Vaya demasiado<http://aka.ms/AzureStackGitHub>, busque hello **101-simple-windows-vm** plantilla y guárdelo toohello ubicación siguiente: c:\\plantillas\\ azuredeploy-101-simple-windows-vm.json.</span><span class="sxs-lookup"><span data-stu-id="1cfca-110">Go too<http://aka.ms/AzureStackGitHub>, search for hello **101-simple-windows-vm** template, and save it toohello following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span></span>
2. <span data-ttu-id="1cfca-111">En PowerShell, ejecute la siguiente secuencia de comandos de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1cfca-111">In PowerShell, run hello following deployment script.</span></span> <span data-ttu-id="1cfca-112">Reemplace *username* y *password* por su nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="1cfca-112">Replace *username* and *password* with your username and password.</span></span> <span data-ttu-id="1cfca-113">En los usos subsiguientes, incrementar el valor de Hola para hello *$myNum* tooprevent parámetro sobrescribiendo la implementación.</span><span class="sxs-lookup"><span data-stu-id="1cfca-113">On subsequent uses, increment hello value for hello *$myNum* parameter tooprevent overwriting your deployment.</span></span>
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. <span data-ttu-id="1cfca-114">Haga clic en de hello abrir pila Azure portal, **examinar**, haga clic en **máquinas virtuales**y busque la nueva máquina virtual (*myDeployment001*).</span><span class="sxs-lookup"><span data-stu-id="1cfca-114">Open hello Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1cfca-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1cfca-115">Next steps</span></span>
[<span data-ttu-id="1cfca-116">Implementación de plantillas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1cfca-116">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

