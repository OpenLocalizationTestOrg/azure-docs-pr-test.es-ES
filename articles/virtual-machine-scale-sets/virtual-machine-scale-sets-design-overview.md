---
title: "aaaDesign consideraciones para conjuntos de escalas de máquina Virtual de Azure | Documentos de Microsoft"
description: "Conozca las consideraciones de diseño de los Conjuntos de escalado de máquinas virtuales de Azure"
keywords: "máquina virtual Linux,conjuntos de escalado de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Consideraciones de diseño para conjuntos de escalado
Este tema analiza consideraciones de diseño para conjuntos de escalado de máquinas virtuales. Para obtener información acerca de qué son los conjuntos de escalas de máquina Virtual, consulte demasiado[información general de conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>¿Cuando se establece toouse escala en lugar de máquinas virtuales?
Por lo general, los conjuntos de escala son útiles para implementar infraestructura altamente disponible donde un conjunto de máquinas tiene una configuración similar. Sin embargo, algunas características solo están disponibles en los conjuntos de escalado, mientras que otras características solo están disponibles en las máquinas virtuales. En Ordenar toomake una decisión informada acerca de cuándo toouse cada tecnología, primero se deberíamos Eche un vistazo a algunas de las características de hello frecuente que están disponibles en conjuntos de escalas pero no las máquinas virtuales:

### <a name="scale-set-specific-features"></a>Características específicas de los conjuntos de escalado

- Una vez que se especifica la configuración de conjunto de escala de hello, simplemente puede actualizar Hola "capacidad" propiedad toodeploy más máquinas virtuales en paralelo. Esto es mucho más fácil que escribir un tooorchestrate script implementar muchas máquinas virtuales individuales en paralelo.
- También puede [use tooautomatically de escalado automático de Azure escalar un conjunto de escala](./virtual-machine-scale-sets-autoscale-overview.md) pero no individuales máquinas virtuales.
- Puede [restablecer la imagen inicial de máquinas virtuales del conjunto de escalado](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm), pero [no las máquinas virtuales individuales](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- También puede [sobreaprovisionar](./virtual-machine-scale-sets-design-overview.md) máquinas virtuales del conjunto de escalado para lograr una mejor confiabilidad y tiempos de implementación más rápidos. No se puede hacer esto con máquinas virtuales individuales a menos que escriba código personalizado toodo esto.
- Puede especificar un [actualizar directiva](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake lo fácil tooroll espera las actualizaciones a través de las máquinas virtuales en el conjunto de escala. Con las máquinas virtuales individuales, debe organizar usted mismo las actualizaciones.

### <a name="vm-specific-features"></a>Características específicas de máquinas virtuales

En Hola otra parte, algunas características solo están disponibles en las máquinas virtuales (al menos por hello momento):

- Puede adjuntar datos discos toospecific máquinas virtuales individuales, pero los discos de datos adjuntos están configurados para todas las máquinas virtuales en un conjunto de escala.
- Puede adjuntar datos vacíos no son discos tooindividual máquinas virtuales pero no las máquinas virtuales en un conjunto de escala.
- Puede crear una instantánea de una máquina virtual individual, pero no una máquina virtual en un conjunto de escalado.
- Puede capturar una imagen desde una máquina virtual individual, pero no desde una máquina virtual en un conjunto de escalado.
- Puede migrar una máquina virtual individual de los discos de toomanaged discos nativos, pero no se puede hacer esto para las máquinas virtuales en un conjunto de escala.
- Puede asignar direcciones IP públicas de IPv6 tooindividual VM nics pero no puede hacerlo para las máquinas virtuales en un conjunto de escala. Tenga en cuenta que puede asignar direcciones IP públicas de IPv6 equilibradores tooload delante de cualquier máquinas virtuales individuales o conjunto de escalado de máquinas virtuales.

## <a name="storage"></a>Storage

### <a name="scale-sets-with-azure-managed-disks"></a>Conjuntos de escalado con Azure Managed Disks
Los conjuntos de escalado se pueden crear con [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) en lugar de las cuentas de Azure Storage tradicionales. Discos administrados proporcionan Hola siguientes ventajas:
- No es necesario toopre-crear un conjunto de cuentas de almacenamiento de Azure para las máquinas virtuales del conjunto de escala de Hola.
- Puede definir [discos de datos conectados](virtual-machine-scale-sets-attached-disks.md) para hello las máquinas virtuales en la escala de conjunto.
- Se pueden configurar conjuntos de escalas de demasiado[admiten hasta too1, 000 máquinas virtuales en un conjunto](virtual-machine-scale-sets-placement-groups.md). 

Si tiene una plantilla existente, también puede [actualizar Hola plantilla toouse administrado discos](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Almacenamiento administrado por el usuario
Un conjunto de escala que no se define con discos de Azure administrados se basa en discos de sistemas operativos de almacenamiento creados por el usuario cuentas toostore Hola de máquinas virtuales de hello en el conjunto de Hola. Se recomienda una proporción de 20 máquinas virtuales por cuenta de almacenamiento o incluso menos E/S máxima tooachieve y también aprovechar las ventajas de _en exceso_ (ver abajo). También se recomienda que distribuir caracteres iniciales de Hola de nombres de cuenta de almacenamiento de hello en alfabeto Hola. Esto ayuda a distribuir la carga en diferentes sistemas internos. 


## <a name="overprovisioning"></a>Aprovisionamiento en exceso
Conjuntos de escala actualmente demasiado "exceso" VM de forma predeterminada. Con exceso activado, escala de hello establezca realmente gira más las máquinas virtuales que se solicitaron los usuarios y luego elimina Hola máquinas virtuales adicionales una vez Hola solicita el número de máquinas virtuales se aprovisionan correctamente. El aprovisionamiento en exceso mejora las tasas de éxito y disminuye el tiempo de implementación. No se le facturará de hello máquinas virtuales adicionales y no cuentan para los límites de cuota.

Si bien en exceso mejoran el aprovisionamiento de las tasas de éxito, puede ser confusos para una aplicación que está diseñada no toohandle máquinas virtuales adicionales que aparecen y, a continuación, desaparecen. tooturn en exceso, asegúrese de tener Hola después de la cadena en la plantilla de: `"overprovision": "false"`. Pueden encontrar más detalles en hello [documentación de API de REST establecer escala](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Si el conjunto de escala usa almacenamiento administradas por el usuario y desactivar en exceso, puede tener más de 20 máquinas virtuales por cuenta de almacenamiento, pero no se recomienda toogo por encima de 40 por motivos de rendimiento de E/S. 

## <a name="limits"></a>límites
Un conjunto de escala había basada en una imagen de Marketplace (también conocido como una imagen de plataforma) y configura toouse discos administrados de Azure es compatible con una capacidad de seguridad too1, 000 máquinas virtuales. Si configura su toosupport de conjunto de escalado más de 100 máquinas virtuales, no todos los trabajos de escenarios Hola mismo (por ejemplo el equilibrio de carga). Para más información, consulte [Uso de grandes conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-placement-groups.md). 

Una escala configurada con cuentas de almacenamiento administradas por el usuario está actualmente limitado too100 las máquinas virtuales (y 5 cuentas de almacenamiento se recomiendan para esta escala).

Un conjunto de escala que se basa en una imagen personalizada (una creada por el usuario) puede tener una capacidad de too100 las máquinas virtuales cuando se configura con discos administrados de Azure. Si el conjunto de escalas de hello está configurado con cuentas de almacenamiento administradas por el usuario, debe crear todos los VHD de disco de sistema operativo dentro de una cuenta de almacenamiento. Como resultado, Hola máxima recomendada para el número de máquinas virtuales en un conjunto de escala que se basa en una imagen personalizada y almacenamiento administradas por el usuario es 20. Si desactiva el exceso, puede subir too40.

Para más máquinas virtuales de permitir que estos límites, necesita toodeploy varios escala se establece como se muestra en [esta plantilla](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

