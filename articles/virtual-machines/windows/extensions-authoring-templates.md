---
title: aaaAuthoring plantillas con las extensiones de VM de Windows | Documentos de Microsoft
description: "Obtenga información sobre cómo crear plantillas del Administrador de recursos de Azure con extensiones para máquinas virtuales de Windows."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Creación de plantillas del Administrador de recursos de Azure con extensiones de máquina virtual
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

De Azure PowerShell, ejecute hello siguiente cmdlet de PowerShell de Azure:

      Get-AzureVMAvailableExtension


Este cmdlet devuelve el nombre del publicador de hello, el nombre de extensión y la versión de la manera siguiente:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Estas tres propiedades se asignan demasiado "publisher", "type" y "typeHandlerVersion" respectivamente en hello por encima del fragmento de código de plantilla.

> [!NOTE]
> Siempre es toouse recomendada hello más reciente extensión versión tooget Hola actualizado más funcionalidad.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Esquema de identificación Hola para parámetros de configuración de extensión de Hola
Hola siguiente paso a la creación de una plantilla de la extensión es formato de hello tooidentify para proporcionar parámetros de configuración. Cada extensión es compatible con su propio conjunto de parámetros.

toolook en configuraciones de ejemplo para las extensiones de Windows, vea [ejemplos de extensiones de Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Consulte toohello después tooget una plantilla se completará con extensiones de máquina virtual.

[Extensión de script personalizada en una máquina virtual de Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Después de crear la plantilla de hello, puede implementar mediante PowerShell de Azure.

