---
title: "VM de Linux aaaTroubleshooting errores de extensión | Documentos de Microsoft"
description: "Información sobre la solución de problemas de la extensión de máquina virtual de Azure"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Solución de problemas de la extensión de máquina virtual de Linux Azure.
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Consulta del estado de la extensión
Plantillas de administrador de recursos de Azure se pueden ejecutar desde Hola CLI de Azure. Una vez que se ejecuta la plantilla de hello, el estado de extensión Hola puede verse desde el Explorador de recursos de Azure o hello herramientas de línea de comandos.

Aquí tiene un ejemplo:

CLI de Azure:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Solucionar problemas de errores de extensión:
### <a name="re-running-hello-extension-on-hello-vm"></a>Volver a ejecutar la extensión de hello en hello VM
Si se ejecutan las secuencias de comandos en la máquina virtual con la extensión de Script personalizado de hello, en ocasiones, podría ejecutar en un error en máquina virtual se creó correctamente pero que ha fallado script de Hola. En estas condiciones, Hola recomienda toorecover forma de este error es tooremove Hola extensión y vuelva a ejecutar la plantilla de Hola.
Nota: En el futuro, esta funcionalidad sería tooremove mejorada Hola necesidad de desinstalar extensión Hola.

#### <a name="remove-hello-extension-from-azure-cli"></a>Quitar extensión Hola de CLI de Azure
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Donde "Publisher-name" corresponde toohello el tipo de extensión de salida de hello de "vm de azure get-instancia-view" y nombre es nombre hello del recurso de extensión de Hola desde la plantilla de Hola

Una vez que se ha quitado la extensión de hello, plantilla de hello puede ser toorun volverá a ejecutar scripts de hello en hello máquina virtual.
