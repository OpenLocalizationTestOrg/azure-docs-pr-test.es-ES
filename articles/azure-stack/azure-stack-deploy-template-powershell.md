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
# <a name="deploy-templates-in-azure-stack-using-powershell"></a>Implementación de plantillas en Azure Stack con PowerShell
Usar PowerShell toodeploy Azure Resource Manager plantillas toohello Kit de desarrollo de pila de Azure.  Las plantillas de Resource Manager implementan y aprovisionan todos los recursos para su aplicación en una única operación coordinada.

## <a name="run-azurerm-powershell-cmdlets"></a>Ejecución de cmdlets de AzureRM PowerShell
En este ejemplo, ejecute una secuencia de comandos toodeploy un Kit de desarrollo de pila mediante una plantilla de administrador de recursos de máquina virtual tooAzure.  Antes de continuar, asegúrese de haber [configurado PowerShell](azure-stack-powershell-configure-user.md)  

Hola VHD que se utiliza en esta plantilla de ejemplo es Windows Server 2012 R2 centros.

1. Vaya demasiado<http://aka.ms/AzureStackGitHub>, busque hello **101-simple-windows-vm** plantilla y guárdelo toohello ubicación siguiente: c:\\plantillas\\ azuredeploy-101-simple-windows-vm.json.
2. En PowerShell, ejecute la siguiente secuencia de comandos de implementación de Hola. Reemplace *username* y *password* por su nombre de usuario y contraseña. En los usos subsiguientes, incrementar el valor de Hola para hello *$myNum* tooprevent parámetro sobrescribiendo la implementación.
   
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
3. Haga clic en de hello abrir pila Azure portal, **examinar**, haga clic en **máquinas virtuales**y busque la nueva máquina virtual (*myDeployment001*).


## <a name="next-steps"></a>Pasos siguientes
[Implementación de plantillas con Visual Studio](azure-stack-deploy-template-visual-studio.md)

