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
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="c0ed2-103">Solución de problemas de la extensión de máquina virtual de Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="c0ed2-104">Consulta del estado de la extensión</span><span class="sxs-lookup"><span data-stu-id="c0ed2-104">Viewing extension status</span></span>
<span data-ttu-id="c0ed2-105">Plantillas de administrador de recursos de Azure se pueden ejecutar desde Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="c0ed2-106">Una vez que se ejecuta la plantilla de hello, el estado de extensión Hola puede verse desde el Explorador de recursos de Azure o hello herramientas de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="c0ed2-107">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c0ed2-107">Here is an example:</span></span>

<span data-ttu-id="c0ed2-108">CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="c0ed2-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="c0ed2-109">Este es el resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c0ed2-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="c0ed2-110">]</span><span class="sxs-lookup"><span data-stu-id="c0ed2-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="c0ed2-111">Solucionar problemas de errores de extensión:</span><span class="sxs-lookup"><span data-stu-id="c0ed2-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="c0ed2-112">Volver a ejecutar la extensión de hello en hello VM</span><span class="sxs-lookup"><span data-stu-id="c0ed2-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="c0ed2-113">Si se ejecutan las secuencias de comandos en la máquina virtual con la extensión de Script personalizado de hello, en ocasiones, podría ejecutar en un error en máquina virtual se creó correctamente pero que ha fallado script de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="c0ed2-114">En estas condiciones, Hola recomienda toorecover forma de este error es tooremove Hola extensión y vuelva a ejecutar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="c0ed2-115">Nota: En el futuro, esta funcionalidad sería tooremove mejorada Hola necesidad de desinstalar extensión Hola.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="c0ed2-116">Quitar extensión Hola de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c0ed2-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="c0ed2-117">Donde "Publisher-name" corresponde toohello el tipo de extensión de salida de hello de "vm de azure get-instancia-view" y nombre es nombre hello del recurso de extensión de Hola desde la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="c0ed2-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="c0ed2-118">Una vez que se ha quitado la extensión de hello, plantilla de hello puede ser toorun volverá a ejecutar scripts de hello en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0ed2-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

