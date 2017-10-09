---
title: "aaaConnect máquinas virtuales de Windows en un servicio en la nube | Documentos de Microsoft"
description: "Conectar máquinas virtuales de Windows creadas con tooan de modelo de implementación clásica de hello servicio en la nube o red virtual."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: d19dc555694eab8a7e790c970cfb5e6a53aa7a7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Conectar máquinas virtuales de Windows creadas con el modelo de implementación clásica de hello con un servicio de nube o de red virtual
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Máquinas virtuales de Windows creadas con el modelo de implementación clásica de hello siempre se colocan en un servicio de nube. servicio de nube de Hello actúa como un contenedor y proporciona un único nombre DNS público, una dirección IP pública y un conjunto de máquina virtual de los puntos de conexión tooaccess hello en hello Internet. servicio de nube de Hello puede estar en una red virtual, pero no es un requisito. También puede [conectar máquinas virtuales creadas con el modelo de implementación clásico con un servicio en la nube o red virtual](../../linux/classic/connect-vms.md).

Si no es un servicio en la nube en una red virtual, se denomina un servicio en la nube *independiente* . máquinas virtuales de Hello en un servicio de nube independiente comunicarse con otras máquinas virtuales mediante el uso de Hola nombres DNS públicos de otras máquinas virtuales y tráfico de hello transmite a través de Internet de Hola. Si un servicio de nube está en una red virtual, máquinas virtuales de hello en que el servicio de nube puede comunicarse con todas las otras máquinas virtuales en la red virtual de hello sin necesidad de enviar todo el tráfico a través de Internet de Hola.

Si coloca las máquinas virtuales en Hola mismo servicio en la nube independiente, todavía puede usar Equilibrio de carga y conjuntos de disponibilidad. Para obtener más información, consulte [máquinas virtuales de equilibrio de carga](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [administrar Hola disponibilidad de máquinas virtuales](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Sin embargo, no se puede organizar las máquinas virtuales de hello en subredes o conectar una red independiente en la nube servicio tooyour local. Este es un ejemplo:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Pasos siguientes
Después de crear una máquina virtual, es una buena idea demasiado[agregar un disco de datos](attach-disk.md) para los servicios y las cargas de trabajo tienen un ubicación toostore de datos.
