---
title: "grupos de aaaResource para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para la implementación de grupos de recursos en los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Directrices para el grupo de recursos de Azure para máquinas virtuales Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

En este artículo se centra en describir cómo toologically el entorno de compilación y todos los componentes de hello en grupos de recursos de grupo.

## <a name="implementation-guidelines-for-resource-groups"></a>Directrices de implementación para los grupos de recursos
Decisiones:

* ¿Vas toobuild grupos de recursos por componentes de la infraestructura básica hello, o por la implementación de la aplicación completa?
* ¿Necesita toorestrict acceso tooResource grupos mediante los controles de acceso basado en roles?

Tareas:

* Defina qué componentes de la infraestructura central y grupos de recursos específicos necesitará.
* Revisar cómo tooimplement plantillas de administrador de recursos para las implementaciones coherentes y reproducibles.
* Definir los roles de acceso de usuario que necesita para controlar el acceso a los grupos de tooResource.
* Crear conjunto de Hola de grupos de recursos con la convención de nomenclatura. Puede usar hello Azure CLI o portal.

## <a name="resource-groups"></a>Grupos de recursos
En Azure, se lógicamente agrupan recursos relacionados, como las cuentas de almacenamiento y redes virtuales, máquinas virtuales (VM) toodeploy, administrar y mantenerlos como una única entidad. Este enfoque resulta más fáciles aplicaciones toodeploy mientras mantiene Hola todos los recursos relacionados juntos desde una perspectiva de administración o toogrant otros toothat grupo de acceso de recursos. Los nombres de grupos de recursos pueden tener un máximo de 90 caracteres de longitud. Para más información acerca de los grupos de recursos, puede leer hello [Introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Una característica clave tooResource grupos es Hola toobuild de capacidad de su entorno mediante un archivo JSON que declara hello, de red de almacenamiento, y los recursos informáticos. También puede definir configuraciones tooapply ni relacionados scripts personalizados. Al usar estas plantillas JSON, crea implementaciones coherentes y reproducibles para sus aplicaciones. Este enfoque le permite crear un entorno de desarrollo y, a continuación, usar ese mismo toocreate de plantilla una implementación de producción, o viceversa. Para entender mejor sobre el uso de plantillas, lea [Hola plantilla tutorial](../../azure-resource-manager/resource-manager-template-walkthrough.md) que le guía a través de cada paso de la generación de una plantilla JSON.

Existen dos enfoques diferentes que puede adoptar al diseñar su entorno con los grupos de recursos:

* Grupos de recursos para cada implementación de aplicación que combina las cuentas de almacenamiento de hello, redes virtuales y subredes, las máquinas virtuales, cargar equilibradores, etcetera.
* Grupos de recursos centralizados que contienen las redes virtuales centrales y las subredes o cuentas de almacenamiento. Las aplicaciones, por tanto, se encontrarán en sus propios grupos de recursos, que solo contienen máquinas virtuales, equilibradores de carga, interfaces de red, etc.

Escalar horizontalmente, crear grupos de recursos centralizados para la red virtual y subredes resulta más fácil toobuild entre entornos conexiones de red para opciones de conectividad híbrida. método alternativo de Hello es para cada aplicación toohave su propia red virtual que requiere configuración y mantenimiento. [Controles de acceso basado en roles](../../active-directory/role-based-access-control-what-is.md) proporcionan un acceso de manera granular toocontrol tooResource grupos. Para las aplicaciones de producción, puede controlar los usuarios de Hola que pueden tener acceso a esos recursos o para recursos de infraestructura de hello principales puede limitar solo infraestructura ingenieros toowork con ellos. Los propietarios de la aplicación sólo tienen acceso a componentes de la aplicación toohello dentro de su grupo de recursos y no la infraestructura de Azure de su entorno de básica de Hola. Al diseñar su entorno, considere la posibilidad de los usuarios de Hola que requieren acceso a los recursos de toohello y diseñe, los grupos de recursos en consecuencia. 

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

