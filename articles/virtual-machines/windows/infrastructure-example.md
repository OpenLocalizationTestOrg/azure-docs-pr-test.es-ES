---
title: aaaExample tutorial de infraestructura de Azure | Documentos de Microsoft
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para implementar una infraestructura de ejemplo en Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a>Tutorial de la infraestructura de Azure de ejemplo para máquinas virtuales Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artículo le guía a través de la creación de una infraestructura de aplicación de ejemplo. Se detallan diseñar una infraestructura de una tienda en línea simple que reúne todas las instrucciones de Hola y tomar decisiones sobre las convenciones de nomenclatura, conjuntos de disponibilidad, las redes virtuales y equilibradores de carga y la implementación real de sus máquinas virtuales (VM).

## <a name="example-workload"></a>Carga de trabajo de ejemplo
Adventure Works Cycles desea toobuild una aplicación de tienda en línea en Azure que consta de:

* Dos servidores IIS que se ejecutan cliente hello front-end en un nivel de web
* Dos servidores IIS que procesen datos y pedidos en un nivel de aplicación
* Dos instancias de Microsoft SQL Server con grupos de disponibilidad AlwaysOn (dos servidores SQL Server y un testigo de mayoría de nodo) para almacenar datos de productos y pedidos en un nivel de base de datos
* Dos controladores de dominio de Active Directory para los proveedores y las cuentas de cliente en un nivel de autenticación
* Todos los servidores de Hola se encuentran en dos subredes:
  * una subred para servidores de hello web front-end 
  * una subred de back-end para servidores de aplicaciones de hello, clúster de SQL y los controladores de dominio

![Diagrama de distintos niveles de infraestructura de aplicaciones](./media/infrastructure-example/example-tiers.png)

Entrada segura tráfico web debe tener equilibrio de carga entre los servidores web de Hola mientras navega por los clientes de tienda en línea hello. Orden de procesamiento de tráfico en forma de Hola de las solicitudes HTTP desde web Hola servidores deben estar equilibrados entre servidores de aplicaciones de Hola. Además, la infraestructura de Hola debe diseñarse para lograr alta disponibilidad.

diseño de Hello resultante debe incorporar:

* Una suscripción y una cuenta de Azure
* Un único grupo de recursos
* Azure Managed Disks
* Una red virtual con dos subredes
* Conjuntos de disponibilidad para hello las máquinas virtuales con una función similar
* Máquinas virtuales

Hola todos los anteriores seguir estas convenciones de nomenclaturas:

* Adventure Works Cycles usa **[carga de trabajo de TI]-[ubicación]-[recurso de Azure]** como prefijo
  * En este ejemplo, "**azos**" (tienda en línea de Azure) se Hola nombre de cargas de trabajo de TI y "**usar**" (este de EE. 2) es la ubicación de Hola
* Las redes virtuales usan AZOS-USE-VN**[número]**
* Los conjuntos de disponibilidad usan azos-use-as-**[rol]**
* Los nombres de máquinas virtuales usan azos-use-vm-**[vmname]**

## <a name="azure-subscriptions-and-accounts"></a>Suscripciones y cuentas de Azure
Adventure Works Cycles es con su suscripción de Enterprise, con el nombre Adventure Works Enterprise Subscription, tooprovide de facturación para esta carga de trabajo de TI.

## <a name="storage"></a>Storage
Adventure Works Cycles determina que deben usar Azure Managed Disks. Al crear máquinas virtuales, se utilizan ambos niveles de almacenamiento disponible:

* **Almacenamiento estándar** para servidores de hello web, servidores de aplicaciones y controladores de dominio y sus discos de datos.
* **Almacenamiento Premium** para hello VM de SQL Server y sus discos de datos.

## <a name="virtual-network-and-subnets"></a>Red virtual y subredes
Red virtual de hello no necesite red local de conectividad en curso toohello Adventure ciclos de trabajo, decidió en una red virtual solo en la nube.

Crea una red virtual solo en la nube con hello después de la configuración mediante Hola portal de Azure:

* Nombre: AZOS-USE-VN01
* Ubicación: Este de EE. UU. 2
* Espacio de direcciones de red virtual: 10.0.0.0/8
* Primera subred:
  * Nombre: FrontEnd
  * Espacio de direcciones: 10.0.1.0/24
* Segunda subred:
  * Nombre: BackEnd
  * Espacio de direcciones: 10.0.2.0/24

## <a name="availability-sets"></a>Conjuntos de disponibilidad
toomaintain alta disponibilidad de los cuatro niveles de su tienda en línea, Adventure Works Cycles decidir sobre cuatro conjuntos de disponibilidad:

* **use azos como web** para servidores web de Hola
* **use azos como aplicación** hello en servidores de aplicaciones
* **uso de azos como sql** para hello servidores SQL Server
* **use azos como dc** Hola para controladores de dominio

## <a name="virtual-machines"></a>Máquinas virtuales
Adventure Works Cycles decidió Hola después de nombres para sus máquinas virtuales de Azure:

* **azos-use-vm-web01** para el primer servidor de web Hola
* **azos-use-vm-web02** para el segundo servidor de web Hola
* **azos-use-vm-app01** Hola primer servidor de aplicaciones
* **azos-use-vm-app02** Hola segundo servidor de aplicaciones
* **azos-use-vm-sql01** para hello primer de SQL server en clúster de Hola
* **azos-use-vm-sql02** para hello segundo SQL server en clúster de Hola
* **azos-use-vm-dc01** Hola primer controlador de dominio
* **azos-use-vm-dc02** Hola segundo controlador de dominio

Esta es la configuración resultante de Hola.

![Infraestructura de aplicaciones final implementada en Azure](./media/infrastructure-example/example-config.png)

Esta configuración incluye:

* Una red virtual solo en la nube con dos subredes (FrontEnd y BackEnd)
* Azure Managed Disks con discos Standard y Premium
* Cuatro conjuntos de disponibilidad, uno para cada nivel de tienda en línea hello
* máquinas virtuales de Hola para los niveles de hello cuatro
* Un conjunto de carga equilibrada externo para el tráfico web basada en HTTPS desde servidores web de hello Internet toohello
* Una carga interna equilibrada conjunto para el tráfico web sin cifrar hello web servidores toohello desde servidores de aplicaciones
* Un único grupo de recursos