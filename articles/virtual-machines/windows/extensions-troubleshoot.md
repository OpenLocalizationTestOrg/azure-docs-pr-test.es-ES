---
title: "errores de extensión de máquina virtual de Windows aaaTroubleshooting | Documentos de Microsoft"
description: "Más información sobre la solución de problemas de la extensión de máquina virtual de Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="ce5d3-103">Solución de problemas de la extensión de máquina virtual de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="ce5d3-104">Consulta del estado de la extensión</span><span class="sxs-lookup"><span data-stu-id="ce5d3-104">Viewing extension status</span></span>
<span data-ttu-id="ce5d3-105">Las plantillas de Azure Resource Manager se pueden ejecutar desde Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="ce5d3-106">Una vez que se ejecuta la plantilla de hello, el estado de extensión Hola puede verse desde el Explorador de recursos de Azure o hello herramientas de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="ce5d3-107">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce5d3-107">Here is an example:</span></span>

<span data-ttu-id="ce5d3-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ce5d3-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="ce5d3-109">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ce5d3-109">Here is hello sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="ce5d3-110">]</span><span class="sxs-lookup"><span data-stu-id="ce5d3-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="ce5d3-111">Solución de problemas de errores de extensión</span><span class="sxs-lookup"><span data-stu-id="ce5d3-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="ce5d3-112">Volver a ejecutar la extensión de hello en hello VM</span><span class="sxs-lookup"><span data-stu-id="ce5d3-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="ce5d3-113">Si se ejecutan las secuencias de comandos en la máquina virtual con la extensión de Script personalizado de hello, en ocasiones, podría ejecutar en un error en máquina virtual se creó correctamente pero que ha fallado script de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="ce5d3-114">En estas condiciones, Hola recomienda toorecover forma de este error es tooremove Hola extensión y vuelva a ejecutar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="ce5d3-115">Nota: En el futuro, esta funcionalidad sería tooremove mejorada Hola necesidad de desinstalar extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="ce5d3-116">Quitar extensión Hola de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="ce5d3-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="ce5d3-117">Una vez que se ha quitado la extensión de hello, plantilla de hello puede ser toorun volverá a ejecutar scripts de hello en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ce5d3-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

