---
title: "aaaVM conserva el mantenimiento de máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Migración local de máquinas virtuales para la realización de actualizaciones con conservación de memoria."
services: virtual-machines-windows
documentationcenter: 
author: 
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: 
ms.openlocfilehash: 544a2dcca52bb3ac51d341bceaf4ba3e7c71fd82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-in-place-vm-migration"></a>Mantenimiento de conservación de máquinas virtuales (migración local de máquinas virtuales)

Aunque mayoría Hola de las actualizaciones no tienen ningún toohosted de impacto en las máquinas virtuales, hay casos donde toocomponents actualizaciones o servicios producir interferencias mínimo toorunning máquinas virtuales (sin un reinicio completo de la máquina virtual de hello).

Estas actualizaciones se realizan con la tecnología que permite la migración local en vivo, también llamada "actualización con conservación de memoria". Al actualizar el host de hello, máquina virtual de Hola se coloca en un estado "en pausa", conservar memoria hello en la RAM, mientras hello (por ejemplo, el sistema operativo subyacente) del entorno de hospedaje aplica revisiones y actualizaciones necesarias de Hola.
máquina virtual de Hello, a continuación, se reanuda en 30 segundos de pausa.
Después de reanudar, reloj Hola de máquina virtual de Hola se sincronizará automáticamente.

No todas las actualizaciones se pueden implementar mediante este mecanismo, pero dado el período breve pausa, implementar las actualizaciones de esta forma en gran medida reduce máquinas toovirtual de impacto.

Las actualizaciones de varias instancias (máquinas virtuales en un conjunto de disponibilidad) se aplican a un dominio de actualización a la vez.

Algunas aplicaciones pueden resultar afectadas por estas actualizaciones más que otras. Las aplicaciones que realizan procesamiento de eventos en tiempo real, transmisión por secuencias multimedia o transcodificación o alto rendimiento redes escenarios, por ejemplo, no pueden ser tootolerate diseñado una pausa de segundo 30. Aplicaciones que se ejecutan en una máquina virtual pueden obtener información acerca de las próximas actualizaciones que realiza la llamada hello [eventos programados](../virtual-machines-scheduled-events.md) API de hello [el servicio de metadatos de Azure](../virtual-machines-instancemetadataservice-overview.md).
