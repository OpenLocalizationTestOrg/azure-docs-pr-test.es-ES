---
title: "aaaSet extremos en una VM de Windows clásico | Documentos de Microsoft"
description: "Obtenga información acerca de tooset extremos de una VM de Windows en hello Azure tooallow portal clásico comunicación con una máquina virtual de Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>¿Cómo tooset extremos en una máquina virtual de Windows clásica de Azure
Hola a todas las ventanas de máquinas virtuales que cree en Azure mediante el modelo de implementación clásica de hello pueden comunicarse automáticamente a través de un canal de red privada con otras máquinas virtuales en el mismo servicio en la nube o red virtual. Sin embargo, los equipos de hello Internet u otras redes virtuales requieren máquina virtual del tooa de tráfico de los puntos de conexión toodirect Hola red de entrada. Este artículo también está disponible para [máquinas virtuales Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Hola **el Administrador de recursos** modelo de implementación, puntos de conexión se configuran mediante **grupos de seguridad de red (NSG)**. Para obtener más información, consulte [permitir acceso externo tooyour VM con Hola portal de Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Cuando crea una máquina virtual Windows Hola portal de Azure, los puntos de conexión comunes como las de escritorio remoto y acceso remoto a Windows PowerShell son normalmente crea automáticamente. Puede configurar extremos adicionales al crear la máquina virtual de Hola o posteriormente según sea necesario.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Pasos siguientes
* toouse un tooset de cmdlet de PowerShell de Azure un punto de conexión de máquina virtual, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse un toomanage de cmdlet de PowerShell de Azure una ACL en un extremo, vea [listas de control de acceso de administración (ACL) para los puntos de conexión mediante el uso de PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Si ha creado una máquina virtual en el modelo de implementación del Administrador de recursos de hello, puede usar Azure PowerShell demasiado[crear grupos de seguridad de red](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol tráfico toohello máquina virtual.
