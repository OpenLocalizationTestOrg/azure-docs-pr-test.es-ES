---
title: "aaaCreate una VM de Linux clásica con Hola 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual de Linux con el uso de hello Azure CLI 1.0 Hola modelo de implementación clásica"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>¿Cómo tooCreate una VM de Linux clásica con Hola 1.0 de CLI de Azure
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para la versión del Administrador de recursos de hello, consulte [aquí](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este tema describe cómo toocreate una máquina virtual de Linux (VM) con el uso de hello Azure CLI 1.0 Hola modelo de implementación clásica. Se utiliza una imagen de Linux de hello disponible **imágenes** en Azure. comandos de Hello 1.0 de CLI de Azure permiten Hola siguientes opciones de configuración, entre otros:

* Conexión de red virtual de hello VM tooa
* Agregar servicio de nube existente de hello VM tooan
* Agregar cuenta de almacenamiento existente de hello VM tooan
* Agregar conjunto de disponibilidad de hello VM tooan o ubicación

> [!IMPORTANT]
> Si desea que su toouse de máquina virtual una red virtual para que pueda conectarse tooit directamente por el nombre de host o configurar las conexiones entre entornos, asegúrese de que especificar red virtual de Hola cuando creas Hola máquina virtual. Una máquina virtual solo puede tener toojoin configurado una red virtual cuando cree Hola máquina virtual. Para obtener detalles acerca de las redes virtuales, consulte [Información general sobre redes virtuales de Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>¿Cómo toocreate una VM de Linux con Hola modelo de implementación clásica
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

