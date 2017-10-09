---
title: aaaExample tutorial de infraestructura de Azure | Documentos de Microsoft
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para implementar una infraestructura de ejemplo en Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a>Tutorial de la infraestructura de Azure de ejemplo para máquinas virtuales Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artículo le guía a través de la creación de una infraestructura de aplicación de ejemplo. Se detallan diseñar una infraestructura de una tienda en línea simple que reúne todas las instrucciones de Hola y tomar decisiones sobre las convenciones de nomenclatura, conjuntos de disponibilidad, las redes virtuales y equilibradores de carga y la implementación real de sus máquinas virtuales (VM).

## <a name="example-workload"></a>Carga de trabajo de ejemplo
Adventure Works Cycles desea toobuild una aplicación de tienda en línea en Azure que consta de:

* Dos servidores nginx ejecuta Hola cliente front-end en un nivel de web
* Dos servidores nginx que procesen datos y pedidos en un nivel de aplicación
* Dos servidores MongoDB parte de un clúster particionado para almacenar pedidos y datos de productos en un nivel de base de datos
* Dos controladores de dominio de Active Directory para los proveedores y las cuentas de cliente en un nivel de autenticación
* Todos los servidores de Hola se encuentran en dos subredes:
  * una subred para servidores de hello web front-end 
  * una subred de back-end para servidores de aplicaciones de hello, MongoDB clúster y controladores de dominio

![Diagrama de distintos niveles de infraestructura de aplicaciones](./media/infrastructure-example/example-tiers.png)

Entrada segura tráfico web debe tener equilibrio de carga entre los servidores web de Hola mientras navega por los clientes de tienda en línea hello. Orden de procesar el tráfico en forma de Hola de HTTP solicita desde web Hola servidores deben ser con equilibrio de carga entre los servidores de aplicación Hola. Además, la infraestructura de Hola debe diseñarse para lograr alta disponibilidad.

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
* **Almacenamiento Premium** para servidores de clúster particionada de MongoDB hello y sus discos de datos.

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
* **use azos como db** para servidores de hello en clúster de hello MongoDB particionada
* **use azos como dc** Hola para controladores de dominio

## <a name="virtual-machines"></a>Máquinas virtuales
Adventure Works Cycles decidió Hola después de nombres para sus máquinas virtuales de Azure:

* **azos-use-vm-web01** para el primer servidor de web Hola
* **azos-use-vm-web02** para el segundo servidor de web Hola
* **azos-use-vm-app01** Hola primer servidor de aplicaciones
* **azos-use-vm-app02** Hola segundo servidor de aplicaciones
* **azos-use-vm-db01** de primer servidor de MongoDB hello en clúster de Hola
* **azos-use-vm-db02** segundo servidor de MongoDB hello en clúster de Hola
* **azos-use-vm-dc01** Hola primer controlador de dominio
* **azos-use-vm-dc02** Hola segundo controlador de dominio

Esta es la configuración resultante de Hola.

![Infraestructura de aplicaciones final implementada en Azure](./media/infrastructure-example/example-config.png)

Esta configuración incluye:

* Una red virtual solo en la nube con dos subredes (FrontEnd y BackEnd)
* Azure Managed Disks que usa discos Standard y Premium
* Cuatro conjuntos de disponibilidad, uno para cada nivel de tienda en línea hello
* máquinas virtuales de Hola para los niveles de hello cuatro
* Un conjunto de carga equilibrada externo para el tráfico web basada en HTTPS desde servidores web de hello Internet toohello
* Una carga interna equilibrada conjunto para el tráfico web sin cifrar hello web servidores toohello desde servidores de aplicaciones
* Un único grupo de recursos