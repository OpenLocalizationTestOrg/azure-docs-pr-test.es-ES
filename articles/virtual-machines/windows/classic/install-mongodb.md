---
title: "aaaInstall MongoDB en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se crea tooinstall MongoDB en una máquina virtual de Azure con el modelo de implementación clásica de hello ejecuta Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Instalación de MongoDB en una máquina virtual de Windows en Azure
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).  Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. tooinstall y configurar MongoDB utilizando el modelo de implementación del Administrador de recursos de hello, consulte [este artículo](../install-mongodb.md).

[MongoDB][MongoDB] es una conocida base de datos NoSQL de código abierto y alto rendimiento. En este artículo le guía por la creación de una máquina virtual de Windows Server (VM) con hello [portal de Azure][AzurePortal]. A continuación, crear y adjuntar un toohello de disco de datos VM antes de instalar y configurar MongoDB. Si tiene una máquina virtual existente en Azure que desearía toouse, también puede avanzar directamente demasiado[instalación y configuración de MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Creación de una máquina virtual que ejecuta Windows Server
Siga estos toocreate instrucciones una máquina virtual.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Puede agregar un extremo para MongoDB al crear la máquina virtual de Hola y configurarlo como sigue: nombre como **Mongo**, use **TCP** como protocolo de Hola y el conjunto ambos demasiado Hola puertos públicos y privados**27017**.
>
>

## <a name="attach-a-data-disk"></a>Acoplamiento de un disco de datos
almacenamiento de tooprovide para la máquina virtual de hello, adjuntar un disco de datos y e inicializarlo después para que Windows pueda usarlo. Si ya tiene un disco de datos, puede conectar ese disco existente o conectar un disco vacío.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Para obtener instrucciones acerca de cómo inicializar disco hello, consulte "Cómo: inicializar un nuevo disco de datos en Windows Server" en [cómo tooattach datos de un disco de máquina virtual de Windows tooa](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Instalar y ejecutar MongoDB en la máquina virtual de Hola
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Resumen
En este tutorial, aprendió cómo toocreate una máquina virtual que ejecuta Windows Server, remotamente conectar tooit y adjuntar un disco de datos.  También habrá aprendido cómo tooinstall y configurar MongoDB en la máquina virtual basada en Windows de Hola. Ahora puedes acceder MongoDB en máquina virtual basada en Windows hello, por siguientes Hola temas avanzados de hello [la documentación de MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

