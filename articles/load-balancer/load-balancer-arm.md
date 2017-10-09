---
title: compatibilidad con el Administrador de recursos para el equilibrador de carga aaaAzure | Documentos de Microsoft
description: Uso de PowerShell para el equilibrador de carga con Azure Resource Manager. Uso de plantillas para el equilibrador de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Uso de la compatibilidad de Azure Resource Manager con Azure Load Balancer

Administrador de recursos de Azure es el marco de trabajo de administración preferido de hello de servicios de Azure. Azure Load Balancer puede administrarse ahora mediante las herramientas y las API basadas en Azure Resource Manager.

## <a name="concepts"></a>Conceptos

Con el Administrador de recursos, el equilibrador de carga de Azure contiene Hola recursos secundarios siguientes:

* Configuración de dirección IP front-end: un equilibrador de carga puede incluir una o varias direcciones IP front-end, conocidas también como IP virtuales (VIP). Estas direcciones IP servir como entrada para el tráfico de Hola.
* Grupo de direcciones de back-end: se trata de direcciones IP asociadas a la máquina virtual de Hola se distribuirá carga toowhich tarjeta de interfaz de red (NIC).
* Reglas de equilibrio de carga: una propiedad de regla asigna una dirección IP determinada front-end y puerto conjunto tooa de combinación de direcciones IP de back-end y combinación de puerto. Un solo equilibrador de carga puede tener varias reglas de equilibrio de carga. Cada regla tiene una combinación de una IP de front-end y un puerto y una IP de back-end asociados a las máquinas virtuales.
* Sondeos: sondeos permiten tookeep realizar un seguimiento del estado de Hola de instancias de máquina virtual. Si se produce un error en un sondeo de estado, instancia de máquina virtual de hello le llevará automáticamente fuera de la rotación.
* Las reglas NAT de entrada: las reglas NAT definir Hola tráfico entrante que fluyen a través de IP de front-end de Hola y distribuida toohello volver terminar IP.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Plantillas de inicio rápido

Azure Resource Manager le permite tooprovision las aplicaciones utilizando una plantilla declarativa. En una plantilla, puede implementar varios servicios junto con sus dependencias. Usar hello mismo toorepeatedly plantilla implementar la aplicación durante cada fase del ciclo de vida de aplicación Hola.

Las plantillas pueden incluir definiciones de máquinas virtuales, redes virtuales, conjuntos de disponibilidad, interfaces de red (NIC), cuentas de almacenamiento, equilibradores de carga, grupos de seguridad de red y direcciones IP públicas. Con las plantillas puede crear todo lo que necesita para una aplicación compleja. archivo de plantilla de Hello pueda proteger en el sistema de administración de contenido para control de versiones y la colaboración.

[Más información sobre las plantillas](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Más información sobre los recursos de red](../virtual-network/resource-groups-networking.md)

Las plantillas de inicio rápido que usan Azure Load Balancer se pueden encontrar en un [repositorio de GitHub](https://github.com/Azure/azure-quickstart-templates) que hospeda un conjunto de plantillas generadas por la comunidad.

Ejemplos de plantillas:

* [Dos máquinas virtuales en un Equilibrador de carga y reglas de equilibrio de carga](http://go.microsoft.com/fwlink/?LinkId=544799)
* [Dos máquinas virtuales en una red virtual con un Equilibrador de carga interno y reglas del Equilibrador de carga](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 máquinas virtuales en un equilibrador de carga y configurar las reglas NAT en hello LB](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Configuración del Equilibrador de carga de Azure con PowerShell o CLI

Introducción a los cmdlets de Azure Resource Manager, las herramientas de línea de comandos y las API de REST

* [Cmdlets de redes de Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) puede ser toocreate usa un equilibrador de carga.
* [¿Cómo toocreate un equilibrador de carga con el Administrador de recursos de Azure](load-balancer-get-started-ilb-arm-ps.md)
* [Uso de hello CLI de Azure con administración de recursos de Azure](../xplat-cli-azure-resource-manager.md)
* [API de REST del Equilibrador de carga](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Pasos siguientes

También puede [empezar a crear un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento especifico del tráfico de red del equilibrador de carga.

Obtenga información acerca de cómo toomanage [inactivo de la configuración de tiempo de espera TCP para un equilibrador de carga](load-balancer-tcp-idle-timeout.md). Esto es importante cuando la aplicación necesita que las conexiones de tookeep activo para servidores detrás de un equilibrador de carga.
