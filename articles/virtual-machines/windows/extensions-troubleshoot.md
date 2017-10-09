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
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Solución de problemas de la extensión de máquina virtual de Microsoft Azure.
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Consulta del estado de la extensión
Las plantillas de Azure Resource Manager se pueden ejecutar desde Azure PowerShell. Una vez que se ejecuta la plantilla de hello, el estado de extensión Hola puede verse desde el Explorador de recursos de Azure o hello herramientas de línea de comandos.

Aquí tiene un ejemplo:

Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Este es el resultado de ejemplo de Hola:

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
  ]

## <a name="troubleshooting-extension-failures"></a>Solución de problemas de errores de extensión
### <a name="re-running-hello-extension-on-hello-vm"></a>Volver a ejecutar la extensión de hello en hello VM
Si se ejecutan las secuencias de comandos en la máquina virtual con la extensión de Script personalizado de hello, en ocasiones, podría ejecutar en un error en máquina virtual se creó correctamente pero que ha fallado script de Hola. En estas condiciones, Hola recomienda toorecover forma de este error es tooremove Hola extensión y vuelva a ejecutar la plantilla de Hola.
Nota: En el futuro, esta funcionalidad sería tooremove mejorada Hola necesidad de desinstalar extensión Hola.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Quitar extensión Hola de PowerShell de Azure
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Una vez que se ha quitado la extensión de hello, plantilla de hello puede ser toorun volverá a ejecutar scripts de hello en hello máquina virtual.

