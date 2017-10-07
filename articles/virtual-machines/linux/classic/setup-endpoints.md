---
title: "aaaSet extremos en una VM de Linux clásica | Documentos de Microsoft"
description: "Obtenga información acerca de tooset extremos de una VM de Linux en hello Azure tooallow portal clásico comunicación con una máquina virtual de Linux en Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>¿Cómo tooset extremos en una máquina virtual de Linux clásica de Azure
Todas las máquinas virtuales de Linux que se crean en Azure mediante el modelo de implementación clásica de hello pueden comunicarse automáticamente a través de un canal de red privada con otras máquinas virtuales en hello que mismo servicio o de red virtual en la nube. Sin embargo, los equipos de hello Internet u otras redes virtuales requieren máquina virtual del tooa de tráfico de los puntos de conexión toodirect Hola red de entrada. Este artículo también está disponible para [máquinas virtuales Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Hola **el Administrador de recursos** modelo de implementación, puntos de conexión se configuran mediante **grupos de seguridad de red (NSG)**. Para más información, consulte [Apertura de puertos y puntos de conexión](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Al crear una máquina virtual Linux en hello portal de Azure, un punto de conexión de Secure Shell (SSH) es normalmente crea automáticamente. Puede configurar extremos adicionales al crear la máquina virtual de Hola o posteriormente según sea necesario.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Pasos siguientes
* También puede crear un punto de conexión de máquina virtual mediante hello [interfaz de línea de comandos de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Ejecute hello **crear punto de conexión de máquina virtual de azure** comando.
* Si ha creado una máquina virtual en el modelo de implementación del Administrador de recursos de hello, puede usar hello Azure CLI en el modo de administrador de recursos demasiado[crear grupos de seguridad de red](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol tráfico toohello máquina virtual.
