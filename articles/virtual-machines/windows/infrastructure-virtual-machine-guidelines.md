---
title: "aaaAzure directrices de máquinas virtuales | Documentos de Microsoft"
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para la implementación de máquinas virtuales de Windows en Azure"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f932e65a-437b-48b0-8d70-f61ded8ce1c6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: d2c8043cd5829b54a5d57e56533122e42021797d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-windows"></a>Directrices de máquinas virtuales de Azure para Windows
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

En este artículo se centra en hello descripción requerido planeamiento de los pasos para crear y administrar máquinas virtuales (VM) en su entorno de Azure.

## <a name="implementation-guidelines-for-vms"></a>Directrices de implementación para las máquinas virtuales
Decisiones:

* ¿Cuántas máquinas virtuales necesita para sus diversos niveles de aplicación y los componentes de su infraestructura?
* ¿Qué recursos de CPU y memoria necesita cada máquina virtual, y cuáles son los requisitos de almacenamiento de Hola?

Tareas:

* Definir las cargas de trabajo de Hola para su hello recursos hello y aplicación de que las máquinas virtuales requieren.
* Alinear Hola demandas de recursos para cada máquina virtual con el tipo de máquina virtual adecuado tamaño y el almacenamiento de Hola.
* Definir los grupos de recursos para distintos niveles de Hola y componentes de la infraestructura.
* Defina la convención de nomenclatura de la máquina virtual.
* Cree las máquinas virtuales con hello Azure PowerShell, web portal, o con plantillas de administrador de recursos.

## <a name="virtual-machines"></a>Máquinas virtuales
Uno de los recursos principales de hello en el entorno de Azure es probable que máquinas virtuales. Este recurso es donde ejecutará sus aplicaciones, bases de datos, servicios de autenticación, etc.

Es importante toounderstand hello [diferentes tamaños VM](sizes.md) toocorrectly cambiar el tamaño de su entorno desde la perspectiva del rendimiento y el costo. Si sus máquinas virtuales no tienen una cantidad adecuada de núcleos de CPU o memoria, el rendimiento de su aplicación se verá afectado independientemente de su diseño y desarrollo. Hola de revisión sugiere las cargas de trabajo para cada serie de máquina virtual como un punto de partida cuando decida qué toouse de máquina virtual de tamaño para cada componente en su infraestructura. También puede [cambiar el tamaño de Hola de una máquina virtual](resize-vm.md) después de la implementación.

El almacenamiento desempeña un papel clave en el rendimiento de la máquina virtual. Puede usar Standard Storage que utilizan los discos giratorios habituales, o bien Premium Storage para altas cargas de trabajo de E/S y el máximo rendimiento que utilizan los discos SSD. Como con hello tamaño de máquina virtual, hay coste medio de almacenamiento de las consideraciones tooselecting Hola. Puede leer hello [artículo de directrices de infraestructura de almacenamiento](infrastructure-storage-solutions-guidelines.md) toounderstand cómo toodesign adecuados almacenamiento para un rendimiento óptimo de las máquinas virtuales.

## <a name="resource-groups"></a>Grupos de recursos
Componentes como las máquinas virtuales se agrupan de forma lógica para facilitar la administración y el mantenimiento mediante los [grupos de recursos de Azure](../../azure-resource-manager/resource-group-overview.md). Mediante el uso de grupos de recursos, puede crear, administrar y supervisar todos los recursos de Hola que componen una aplicación determinada. También puede implementar [controles de acceso basado en roles](../../active-directory/role-based-access-control-what-is.md) toogrant acceso tooothers dentro de los recursos de equipo tooonly Hola necesiten. Tardar tiempo tooplan los grupos de recursos y las asignaciones de roles. Hay diferentes enfoques tooactually grupos de recursos de diseño e implementación, así que seguro tooread hello [artículo de directrices de grupos de recursos](infrastructure-resource-groups-guidelines.md) toounderstand toobuild la mejor forma de salida de las máquinas virtuales.

## <a name="templates"></a>Plantillas
Puede crear plantillas, definidas por los archivos JSON declarativos, toocreate las máquinas virtuales. Plantillas normalmente también crear almacenamiento Hola necesario, redes, interfaces de red, una dirección IP, etc. junto con hello las propias máquinas virtuales. Usar plantillas toocreate coherente y reproducible los entornos de desarrollo y pruebas tooeasily fines replican los entornos de producción y viceversa. Más información sobre [generar y utilizar plantillas](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand cómo puede usarlos para crear e implementar las máquinas virtuales.

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

