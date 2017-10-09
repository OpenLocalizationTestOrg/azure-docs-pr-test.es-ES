---
title: "una red virtual de Azure (clásica) desde un área de grupo de afinidad tooa aaaMigrate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomigrate una red virtual (clásica) desde una afinidad de grupo tooa región."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Migrar una red virtual (clásica) de una región de tooa grupo de afinidad

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones utilizarán modelo de implementación del Administrador de recursos de Hola.

Grupos de afinidad asegurarse de que los recursos crean dentro de hello al mismo grupo de afinidad físicamente están hospedadas por servidores que están muy próximas, habilitar estos toocommunicate recursos más rápida. Hola anteriores, grupos de afinidad eran un requisito para crear redes virtuales (clásicas). En ese momento, el servicio de administrador de red de Hola que administrar redes virtuales (clásicas) solo podía trabajar dentro de un conjunto de servidores físicos o unidad de escala. Mejoras arquitectónicas han aumentado el ámbito de Hola de región de tooa de administración de red.

Como resultado de estas mejoras de arquitectura, los grupos de afinidad ya no se recomiendan ni son necesarios para las redes virtuales (clásicas). uso de Hola de grupos de afinidad para redes virtuales (clásicas) se reemplaza por regiones. Las redes virtuales (clásicas) que están asociadas a regiones se denominan redes virtuales regionales.

Por lo general, se recomienda no usar grupos de afinidad. Además de requisito de la red virtual de hello, grupos de afinidad también eran importante toouse tooensure recursos, como proceso (clásico) y almacenamiento (clásica), se coloca cerca entre sí. Sin embargo, con la arquitectura de red de Azure actual hello, estos requisitos de ubicación ya no son necesarios.

> [!IMPORTANT]
> Aunque es técnicamente posible toocreate una red virtual que está asociada a un grupo de afinidad, no hay ningún toodo motivo convincente así. Muchas características de red virtual, como los grupos de seguridad de red, solo están disponibles cuando se usa una red virtual regional y no están disponibles para las redes virtuales que están asociadas a grupos de afinidad.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Editar el archivo de configuración de red de hello

1. Exportar archivo de configuración de red de Hola. toolearn cómo tooexport una configuración de red con PowerShell de archivo o hello Azure interfaz de línea de comandos (CLI) 1.0, vea [configurar una red virtual con un archivo de configuración de red](virtual-networks-using-network-configuration-file.md#export).
2. Editar el archivo de configuración de red de hello, reemplazando **AffinityGroup** con **ubicación**. Especifique una [región](https://azure.microsoft.com/regions) de Azure para **Location**.
   
   > [!NOTE]
   > Hola **ubicación** es Hola región que especificó para el grupo de afinidad de Hola que está asociado a la red virtual (clásica). Por ejemplo, si la red virtual (clásica) está asociada a un grupo de afinidad que se encuentra la zona horaria del Pacífico occidental, cuando se migran, el **ubicación** debe apuntar tooWest Estados Unidos. 
   > 
   > 
   
    Editar Hola siguiendo las líneas en el archivo de configuración de red, reemplazando los valores de hello con su propio: 
   
    **Valor antiguo:**\<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\> 
   
    **Valor nuevo:**\<VirtualNetworkSitename="VNetUSWest" Location="West US"\>
3. Guarde los cambios y [importar](virtual-networks-using-network-configuration-file.md#import) Hola tooAzure de configuración de red.

> [!NOTE]
> Esta migración no hace que los tiempos de inactividad tooyour servicios.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>¿Qué toodo si tiene una máquina virtual (clásica) en un grupo de afinidad
Máquinas virtuales (clásicas) que están en un grupo de afinidad no es necesario toobe quita del grupo de afinidad de Hola. Una vez que se implementa una máquina virtual, es implementada tooa sola unidad de escala. Grupos de afinidad puede restringir el conjunto de Hola de tamaños de máquina virtual disponibles para una nueva implementación de máquina virtual, pero todas las máquinas virtuales existentes que se implementaron ya se haya restringido toohello conjunto de VM tamaños disponibles en la unidad de escala de hello en qué Hola se implementa la máquina virtual. Porque Hola que VM ya está implementado tooa unidad de escala, quitar una máquina virtual de un grupo de afinidad no tiene ningún efecto en hello máquina virtual.
