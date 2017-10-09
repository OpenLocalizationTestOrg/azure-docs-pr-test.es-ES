---
title: "aaaAvailability se establece para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para la implementación de conjuntos de disponibilidad en los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78e4da5c8fd9eb186cafacb46454444b73a9439c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a>Directrices de conjuntos de disponibilidad de Azure para máquinas virtuales Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

En este artículo se centra en hello descripción necesario pasos de planeación para conjuntos de disponibilidad tooensure sus aplicaciones permanecen accesible durante eventos planeados o no.

## <a name="implementation-guidelines-for-availability-sets"></a>Directrices de implementación para los conjuntos de disponibilidad
Decisiones:

* ¿Cuántos conjuntos de disponibilidad ¿necesita para hello diversas funciones y niveles de su infraestructura de aplicación?

Tareas:

* Definir el número de Hola de máquinas virtuales en cada nivel de aplicación que necesite.
* Determine si necesita que el número de hello tooadjust de toobe de dominios de error o actualización usada para la aplicación.
* Definir conjuntos de disponibilidad de hello necesario con la convención de nomenclatura y las máquinas virtuales que residen en ellas. Una máquina virtual solo puede residir en un conjunto de disponibilidad. 

## <a name="availability-sets"></a>Conjuntos de disponibilidad
En Azure, máquinas virtuales (VM) puede colocarse en la agrupación lógica de tooa llamado a un conjunto de disponibilidad. Al crear máquinas virtuales dentro de un conjunto de disponibilidad, Hola plataforma Windows Azure distribuye colocación Hola de esas máquinas virtuales entre Hola infraestructura subyacente. Debe haber un toohello de evento de mantenimiento planificado de la plataforma Azure o un hardware subyacente / error de infraestructura, uso de Hola de conjuntos de disponibilidad garantiza que al menos una máquina virtual sigue ejecutándose.

Como procedimiento recomendado, las aplicaciones no deben residir en una sola máquina virtual. Un conjunto de disponibilidad que contiene una sola máquina virtual no obtiene ninguna protección para evitar eventos planeadas o no dentro de hello plataforma Windows Azure. Hola [SLA de Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) requiere dos o más máquinas virtuales dentro de una disponibilidad conjunto tooallow Hola distribución de máquinas virtuales a través de hello infraestructura subyacente. Si utilizas [almacenamiento de Azure Premium](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Hola SLA de Azure aplica tooa única máquina virtual.

la infraestructura subyacente de Hello en Azure se divide en clústeres de hardware de toomultiple. Cada uno de ellos puede admitir una gran variedad de tamaños de máquina virtual. Un conjunto de disponibilidad solo se hospedada en un clúster de hardware único en cualquier momento. Por lo tanto, los tamaños de intervalo de VM de Hola que pueden existir en un único conjunto de disponibilidad es limitado toohello tamaños de intervalo de la máquina virtual compatibles con clústeres de hardware de Hola. clúster de hardware de Hello para el conjunto de disponibilidad de hello es seleccionado al hello primera VM en el conjunto de disponibilidad de Hola se implementa o a partir de Hola primera VM en un conjunto de disponibilidad en todas las máquinas virtuales actualmente están en el estado de detenido-desasignado Hola. Hola siguiente comando CLI puede ser usado toodetermine Hola intervalo de VM tamaños disponibles para un conjunto de disponibilidad: "az vm lista-tamaños--ubicación \<cadena\>"

Cada clúster de hardware se divide en toomultiple actualizar dominios y dominios de error. Estos dominios se definen teniendo en cuenta qué hosts compartirán un ciclo de actualización común o una infraestructura física similar como la energía y redes. Azure distribuye automáticamente las máquinas virtuales dentro de un conjunto a través de dominios toomaintain disponibilidad y tolerancia a errores de disponibilidad. Según el tamaño de saludo de la aplicación y la cantidad de Hola de máquinas virtuales dentro de un conjunto de disponibilidad, puede ajustar el número de Hola de dominios que se va toouse. Puede leer más sobre la [administración de la disponibilidad y el uso de los dominios de actualización y error](manage-availability.md).

Al diseñar la infraestructura de aplicación, planifique toouse de niveles de aplicación Hola. Máquinas virtuales del grupo que actuar Hola mismo propósito en conjuntos de tooavailability, como un conjunto de disponibilidad para las máquinas virtuales front-end ejecuta nginx o Apache. Cree un conjunto de disponibilidad independiente para las máquinas virtuales de back-end que ejecutan MongoDB o MySQL. objetivo de Hello es tooensure que cada componente de la aplicación está protegido por un conjunto de disponibilidad y al menos una vez instancia siempre sigue ejecutándose.

Equilibradores de carga se pueden utilizar delante de cada toowork de nivel de aplicación junto con un conjunto de disponibilidad y asegúrese de tráfico siempre puede ser enrutado tooa ejecuta la instancia. Sin un equilibrador de carga, las máquinas virtuales pueden seguir ejecutándose a lo largo de los eventos de mantenimiento planeadas y no planeadas, pero el usuario final no puede ser capaz de tooresolve ellos si hello máquina virtual principal no está disponible.

Diseñe su aplicación para lograr una alta disponibilidad en la capa de almacenamiento. procedimiento recomendado de Hello es demasiado[usar discos administrados para las máquinas virtuales en un conjunto de disponibilidad](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Si actualmente utilizas discos no administrados, es muy recomendable demasiado[convertir máquinas virtuales en el conjunto de disponibilidad toouse administrado discos](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

