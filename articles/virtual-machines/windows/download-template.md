---
title: "plantilla de hello aaaDownload para una máquina virtual de Azure | Documentos de Microsoft"
description: "Descargar plantilla de hello formularioPor un toohelp VM con la automatización de las implementaciones en el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Descargue la plantilla de Hola para una máquina virtual
Cuando se crea una máquina virtual en Azure mediante el portal de Hola o PowerShell, un administrador de recursos plantilla se crea automáticamente. Puede usar este duplicado de tooquickly una implementación de plantilla. plantilla de Hello contiene información acerca de todos los recursos de hello en un grupo de recursos. Para una máquina virtual, esto significa plantilla hello contiene todo lo que se crea para admitir Hola VM en ese grupo de recursos, incluidos los recursos de red de Hola.

## <a name="download-hello-template-using-hello-portal"></a>Descargar plantilla de hello mediante el portal de Hola
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Menú del concentrador uno Hola, seleccione **máquinas virtuales**.
3. Seleccione la máquina virtual de Hola de lista de Hola.
4. Seleccione **Script de Automation**.
5. Seleccione **descargar** y guarde el equipo local del tooyour de archivo .zip Hola.
6. Abra el archivo .zip de hello y extraer carpeta tooa Hola. archivo .zip de Hello contendrá:
   
   * deploy.ps1
   * deploy.sh 
   * deployer.rb
   * DeploymentHelper.cs
   * parameters.json
   * template.json

archivo de template.json Hello es la plantilla de Hola.

## <a name="download-hello-template-using-powershell"></a>Descargar plantilla de hello mediante PowerShell
También puede descargar el archivo de plantilla de hello .json con hello [AzureRMResourceGroup de exportación](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet. Puede usar hello `-path` parámetro tooprovide Hola filename y ruta de acceso de archivo de .json Hola. Este ejemplo muestra cómo se denomina plantilla de hello toodownload para el grupo de recursos de hello **myResourceGroup** toohello **C:\users\public\downloads** carpeta en el equipo local.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de implementar los recursos con plantillas, consulte [tutorial de la plantilla de administrador de recursos](../../azure-resource-manager/resource-manager-template-walkthrough.md).

