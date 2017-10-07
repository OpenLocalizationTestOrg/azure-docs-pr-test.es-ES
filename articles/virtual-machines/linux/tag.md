---
title: "aaaHow tootag una máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Obtenga información sobre cómo etiquetar una máquina virtual de Linux de Azure creada en Azure con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>¿Cómo tootag una máquina virtual de Linux en Azure
Este artículo describen distintas formas tootag una máquina virtual de Linux en Azure a través del modelo de implementación del Administrador de recursos de Hola. Las etiquetas son pares clave-valor definidos por el usuario que se pueden colocar directamente en un recurso o un grupo de recursos. Azure admite actualmente hasta etiquetas de too15 por cada recurso y el grupo de recursos. Etiquetas se pueden colocar en un recurso en tiempo de presentación de la creación o agregan tooan de recurso existente. Tenga en cuenta los recursos creados a través del modelo de implementación de administrador de recursos de hello solo se admiten etiquetas.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Etiquetado con la CLI de Azure
toobegin, necesita hello más reciente [2.0 de CLI de Azure (vista previa)](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

También puede realizar estos pasos con hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Puede ver todas las propiedades de una máquina Virtual determinada, incluidas las etiquetas de hello, utilizar el siguiente comando:

        az vm show --resource-group MyResourceGroup --name MyTestVM

tooadd una nueva etiqueta de la máquina virtual a través de hello CLI de Azure, puede usar hello `azure vm update` comando junto con el parámetro de la etiqueta de hello **--establecer**:

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

etiquetas de tooremove, puede usar hello **--quitar** parámetro Hola `azure vm update` comando.

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


Ahora que se han aplicado etiquetas tooour recursos CLI de Azure y Hola Portal, echemos un vistazo a toosee de detalles de uso de hello etiquetas hello en el portal de facturación de Hola.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de etiquetado de los recursos de Azure, consulte [Azure Resource Manager Overview] [ Azure Resource Manager Overview] y [tooorganize etiquetas utilizando los recursos de Azure] [ Using Tags tooorganize your Azure Resources].
* toosee cómo etiquetas pueden ayudar a administrar el uso de recursos de Azure, consulte [descripción de la factura de Azure] [ Understanding your Azure Bill] y [obtener información sobre el consumo de recursos de Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
