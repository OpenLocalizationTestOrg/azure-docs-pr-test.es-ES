---
title: Grupos de recursos para VM de Linux en Azure| Microsoft Docs
description: "Obtenga información sobre las directrices clave de diseño e implementación para implementar grupos de recursos en los servicios de infraestructura de Azure."
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
ms.openlocfilehash: 452acde571164a3ab4ce2dcccf99d2aed90361fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Directrices para el grupo de recursos de Azure para máquinas virtuales Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artículo se centra en describir cómo crear su entorno de forma lógica y agrupar todos los componentes en grupos de recursos.

## <a name="implementation-guidelines-for-resource-groups"></a>Directrices de implementación para los grupos de recursos
Decisiones:

* ¿Va a crear grupos de recursos mediante los componentes de la infraestructura central o la implementación de la aplicación completa?
* ¿Necesita restringir el acceso a grupos de recursos mediante controles de acceso basados en rol?

Tareas:

* Defina qué componentes de la infraestructura central y grupos de recursos específicos necesitará.
* Revise la forma en que se pueden implementar plantillas de Resource Manager para realizar implementaciones coherentes y reproducibles.
* Defina qué roles de acceso de usuario necesitará para controlar el acceso a grupos de recursos.
* Cree el conjunto de grupos de recursos usando su convención de nomenclatura. Puede usar la CLI o el Portal de Azure.

## <a name="resource-groups"></a>Grupos de recursos
En Azure, puede agrupar de forma lógica recursos relacionados tales como cuentas de almacenamiento, redes virtuales y máquinas virtuales para implementarlos, administrarlos y mantenerlos como entidad única. Con este enfoque, resulta más fácil implementar aplicaciones al mismo tiempo que se mantienen juntos todos los recursos relacionados desde una perspectiva de administración, así como conceder acceso a otros usuarios a ese grupo de recursos. Los nombres de grupos de recursos pueden tener un máximo de 90 caracteres de longitud. Para una descripción más completa de los grupos de recursos, puede leer [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Una función clave de los grupos de recursos es la capacidad de crear su entorno mediante un archivo JSON que declara los recursos de proceso, redes y almacenamiento. También puede definir todos los scripts personalizados relacionados o configuraciones que correspondan. Al usar estas plantillas JSON, crea implementaciones coherentes y reproducibles para sus aplicaciones. Este enfoque le permite crear un entorno en desarrollo y, a continuación, el uso de esa misma plantilla para crear una implementación de producción, o viceversa. Para comprender mejor el uso de plantillas, puede leer [el tutorial de plantillas](../../azure-resource-manager/resource-manager-template-walkthrough.md) , que lo guiará en cada paso de la creación de una plantilla JSON.

Existen dos enfoques diferentes que puede adoptar al diseñar su entorno con los grupos de recursos:

* Grupos de recursos para cada implementación de aplicaciones que combina las cuentas de almacenamiento, las redes virtuales y subredes, las máquinas virtuales, los equilibradores de carga, etc.
* Grupos de recursos centralizados que contienen las redes virtuales centrales y las subredes o cuentas de almacenamiento. Las aplicaciones, por tanto, se encontrarán en sus propios grupos de recursos, que solo contienen máquinas virtuales, equilibradores de carga, interfaces de red, etc.

A medida que escale horizontalmente, la creación de grupos de recursos centralizados para sus redes virtuales y subredes facilitará la creación, a su vez, de conexiones de red entre locales con el fin de proporcionar opciones de conectividad híbrida. El enfoque alternativo consiste en que cada aplicación tenga su propia red virtual, que requiere realizar tareas de configuración y mantenimiento. [controles de acceso basado en rol](../../active-directory/role-based-access-control-what-is.md) proporcionan una forma pormenorizada de controlar el acceso a grupos de recursos. En el caso de las aplicaciones de producción, puede controlar los usuarios que es posible que tengan acceso a esos recursos, o bien, en el caso de los recursos de la infraestructura central, puede limitar solo el número de ingenieros de infraestructura que deben trabajar con ellos. Los propietarios de su aplicación solo tendrán acceso a los componentes de esta en su grupo de recursos, y no a la infraestructura central de Azure de su entorno. A medida que plantee el entorno, tenga en cuenta qué usuarios requerirán acceso a los recursos y diseñe sus grupos de recursos según corresponda. 

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

