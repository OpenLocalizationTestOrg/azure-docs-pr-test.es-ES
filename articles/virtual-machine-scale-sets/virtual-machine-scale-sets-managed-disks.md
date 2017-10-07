---
title: "aaaUsing administrar discos con Azure escala conjuntos de máquinas virtuales | Documentos de Microsoft"
description: "Obtenga información acerca de cómo y por qué toouse administrar discos con conjuntos de escalas de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Conjuntos de escalado de máquinas virtuales y discos administrados

Los [conjuntos de escalado de máquinas virtuales](/azure/virtual-machine-scale-sets/) de Azure admiten máquinas virtuales con discos administrados. El uso de discos administrados con conjuntos de escalado resulta ventajoso de varias maneras, como por ejemplo:

* Ya no necesita toopre-crear y administrar discos de hello SO de toostore de cuentas de almacenamiento para las máquinas virtuales del conjunto de escala de Hola.

* Puede asociar el conjunto de escalas de toohello de discos de datos administrados.

* Con discos administrados, un conjunto de escalado puede tener una capacidad tan alta como 1000 máquinas virtuales, si se basa en una imagen de plataforma o 100 máquinas virtuales, si se basa en una imagen personalizada.

## <a name="get-started"></a>Primeros pasos

Una manera sencilla de tooget a trabajar con conjuntos de escalas de disco administrado es toodeploy de hello portal de Azure. Para obtener más información, consulte [este artículo](./virtual-machine-scale-sets-portal-create.md). Otra manera simple tooget iniciado es toouse [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy una escala configurada. Hello en el ejemplo siguiente se muestra cómo toocreate una Ubuntu basada escala establecida con 10 máquinas virtuales, cada uno con un disco de 50 GB y 100 GB de datos:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Como alternativa, también puede buscar en hello [repositorio de GitHub de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) en las carpetas que contienen `vmss` toosee pregeneradas ejemplos de plantillas que implementación conjuntos de escalado. tootell las plantillas que ya está usando discos administrados, puede hacer referencia demasiado[esta lista](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los discos administrados en general, consulte [este artículo](../virtual-machines/windows/managed-disks-overview.md).

toosee modo tooconvert establece una escala de tooprovision de plantilla de administrador de recursos con administra los discos, consulte [este artículo](./virtual-machine-scale-sets-convert-template-to-md.md). Hello mismas plantillas de administrador de recursos de toohello modificaciones aplican toohello API de REST de Azure.

toolearn más sobre el uso de discos de datos administrados con conjuntos de escalado, consulte [este artículo](./virtual-machine-scale-sets-attached-disks.md).

toobegin trabajar con conjuntos de gran escala, consulte demasiado[este artículo](./virtual-machine-scale-sets-placement-groups.md).


