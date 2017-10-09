---
title: "aaaHow tootag un recurso de máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información sobre cómo etiquetar una máquina virtual de Windows creada en Azure con el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>¿Cómo tootag una máquina virtual de Windows en Azure
Este artículo describen distintas formas tootag una máquina virtual de Windows en Azure a través del modelo de implementación del Administrador de recursos de Hola. Las etiquetas son pares clave-valor definidos por el usuario que se pueden colocar directamente en un recurso o un grupo de recursos. Azure admite actualmente hasta etiquetas de too15 por cada recurso y el grupo de recursos. Etiquetas se pueden colocar en un recurso en tiempo de presentación de la creación o agregan tooan de recurso existente. Tenga en cuenta que los recursos creados a través del modelo de implementación de administrador de recursos de hello solo se admiten etiquetas. Si desea tootag una máquina virtual Linux, consulte [cómo tootag una máquina virtual de Linux en Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Etiquetado con PowerShell
toocreate, agregar y eliminar etiquetas a través de PowerShell, primero debe tooset seguridad su [entorno de PowerShell con el Administrador de recursos de Azure][PowerShell environment with Azure Resource Manager]. Una vez haya completado el programa de instalación de hello, puede colocar etiquetas en los recursos de proceso, red y almacenamiento en la creación o después de crea el recurso de Hola a través de PowerShell. En este artículo se centrará en la visualización y edición de etiquetas en máquinas virtuales.

En primer lugar, navegue tooa Máquina Virtual a través de hello `Get-AzureRmVM` cmdlet.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Si la máquina Virtual ya contiene etiquetas, a continuación, verá todas las etiquetas de hello en el recurso:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Si desea que las etiquetas tooadd a través de PowerShell, puede usar hello `Set-AzureRmResource` comando. Tenga en cuenta que si actualiza las etiquetas a través de PowerShell, se actualizan todas ellas en conjunto. Por lo que si va a agregar un recurso de tooa de etiqueta que ya tiene etiquetas, necesitará tooinclude todas las etiquetas de Hola que desee toobe colocado en el recurso de Hola. A continuación se muestra un ejemplo de cómo tooadd adicional etiquetas tooa recursos mediante Cmdlets de PowerShell.

Este primer cmdlet establece todas etiquetas Hola colocadas en *MyTestVM* toohello *$tags* variable, con hello `Get-AzureRmResource` y `Tags` propiedad.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Hola segundo comando muestra etiquetas de Hola para hello dada variable.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

Hola tercer comando agrega una etiqueta adicional toohello *$tags* variable. Tenga en cuenta use Hola de hello  **+=**  tooappend Hola toohello de par clave/valor nuevo *$tags* lista.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

comando cuarto Hola establece todas las etiquetas de hello definidas en Hola de *$tags* toohello variable tiene recursos. En este caso, es MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

comando quinto Hello muestra todas las etiquetas de hello en recursos de Hola. Como puede ver, *ubicación* ahora está definida como una etiqueta con *MyLocation* como valor de Hola.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

Obtenga más información sobre toolearn etiquetado a través de PowerShell, desproteger hello [Cmdlets de recurso de Azure][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de etiquetado de los recursos de Azure, consulte [Azure Resource Manager Overview] [ Azure Resource Manager Overview] y [tooorganize etiquetas utilizando los recursos de Azure] [ Using Tags tooorganize your Azure Resources].
* toosee cómo etiquetas pueden ayudar a administrar el uso de recursos de Azure, consulte [descripción de la factura de Azure] [ Understanding your Azure Bill] y [obtener información sobre el consumo de recursos de Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
