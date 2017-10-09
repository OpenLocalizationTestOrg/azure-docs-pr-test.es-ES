---
title: aaaOverview de IPv6 para el equilibrador de carga de Azure | Documentos de Microsoft
description: "Información sobre la compatibilidad de IPv6 con Azure Load Balancer y máquinas virtuales de carga equilibrada."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, Azure Load Balancer, pila doble, dirección ip pública, ipv6 nativo, móvil, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Información general de IPv6 para Azure Load Balancer

Los equilibradores de carga con conexión a Internet pueden implementarse con una dirección IPv6. Además tooIPv4 conectividad, esto permite Hola siguientes capacidades:

* To-end conectividad IPv6 nativa entre los clientes de Internet públicos y máquinas virtuales (VM) de Azure a través del equilibrador de carga de Hola.
* Conectividad IPv6 nativa saliente de un extremo a otro entre máquinas virtuales y los clientes de Internet públicos con IPv6 habilitado.

Hola siguiente imagen ilustra funcionalidad Hola IPv6 de equilibrador de carga de Azure.

![Azure Load Balancer con IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

Una vez implementado, un cliente IPv4 o IPv6 habilitado Internet puede comunicarse con hello pública direcciones IPv4 o IPv6 (o los nombres de host) de hello equilibrador de carga a través de Internet de Azure. rutas de equilibrador de carga de Hola Hola IPv6 paquetes toohello IPv6 direcciones privadas de las máquinas virtuales de hello con traducción de direcciones de red (NAT). cliente de Internet IPv6 Hello no puede comunicarse directamente con hello dirección IPv6 de hello las máquinas virtuales.

## <a name="features"></a>Características

La compatibilidad nativa de IPv6 para máquinas virtuales implementadas a través de Azure Resource Manager ofrece:

1. Equilibrio de carga de servicios de IPv6 para los clientes de IPv6 en hello Internet
2. Puntos de conexión de IPv4 y IPv6 nativas en máquinas virtuales ("dual apilada")
3. Conexiones de IPv6 nativas iniciadas de entrada y salida
4. Protocolos compatibles como TCP, UDP y HTTP (S) admiten una amplia gama de arquitecturas de servicio

## <a name="benefits"></a>Ventajas

Esta funcionalidad permite Hola siguientes ventajas principales:

* Cumplir las normas gubernamentales que requieren que las nuevas aplicaciones sea accesibles clientes solo tooIPv6
* Habilitar mobile e Internet de las cosas (IOT) a los desarrolladores toouse apiladas dos máquinas virtuales de Azure (IPv4 + IPv6) tooaddress Hola mobile creciente y mercados IOT

## <a name="details-and-limitations"></a>Detalles y limitaciones

Detalles

* Hola servicio DNS de Azure contiene registros de nombre A IPv4 y IPv6 AAAA y responde con ambos registros Hola equilibrador de carga. cliente de Hello elige qué toocommunicate de dirección (IPv4 o IPv6) con.
* Cuando una máquina virtual inicia un dispositivo de conectada a Internet IPv6 público de conexión tooa, dirección IPv6 de origen de la máquina virtual de hello es traducido de dirección de red (NAT) toohello pública dirección IPv6 del equilibrador de carga de Hola.
* Máquinas virtuales que ejecutan el sistema operativo de Linux de hello deben ser tooreceive configurada una dirección IP de IPv6 a través de DHCP. Muchas de las imágenes de Linux de hello en hello Galería de Azure ya están configuran toosupport IPv6 sin ninguna modificación. Para más información, vea [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)
* Si elige toouse un estado de sondeo con el equilibrador de carga, crear una prueba de IPv4 y usarlo con hello IPv4 y IPv6 extremos. Si el servicio de hello en su máquina virtual deja de funcionar, Hola IPv4 y IPv6 extremos se realizan fuera de la rotación.

Limitaciones

* No se puede agregar reglas de equilibrio de carga de IPv6 en hello portal de Azure. reglas de Hello solo pueden crearse a través de la plantilla de hello, CLI, PowerShell.
* No puede actualizar las direcciones de IPv6 de toouse de máquinas virtuales existentes. Debe implementar nuevas máquinas virtuales.
* Puede asignarse a una sola dirección IPv6 tooa única interfaz de red en cada máquina virtual.
* las direcciones IPv6 de Hello públicas no se puede asignar tooa máquina virtual. Solo se puede asignar tooa equilibrador de carga.
* No puede configurar la búsqueda DNS inversa Hola para las direcciones IPv6 públicas.
* Hola máquinas virtuales con direcciones IPv6 de hello no puede ser miembros de un servicio de nube de Azure. Se pueden tooan conectado (VNet) de red Virtual de Azure y comunicarse entre sí a través de sus direcciones IPv4.
* Las direcciones IPv6 privadas se pueden implementar en máquinas virtuales individuales en un grupo de recursos, pero no se pueden implementar en un grupo de recursos a través de conjuntos de escalas.
* Máquinas virtuales de Azure no se pueden conectar a través de las máquinas virtuales de IPv6 tooother, otros servicios de Azure o los dispositivos locales. Sólo puede comunicarse con el equilibrador de carga de Azure de Hola a través de IPv6. Sin embargo, pueden comunicarse con estos otros recursos mediante IPv4.
* La protección del grupo de seguridad de red (NSG) para IPv4 es compatible con las implementaciones de pila doble (IPv4 + IPv6). Los NSG no aplican a los puntos de conexión de toohello IPv6.
* extremo de Hello IPv6 en hello VM no está directamente expuesto toohello internet. Lo hace a través de un equilibrador de carga. Solo los puertos de hello especificados en las reglas de equilibrador de carga de hello son accesibles a través de IPv6.
* Cambiar Hola IdleTimeout parámetro para IPv6 es **no admiten**. valor predeterminado de Hello es cuatro minutos.
* Cambiar Hola parámetro loadDistributionMethod para IPv6 es **no admiten**.
* Las direcciones IP de reserva de IPv6 (donde IPAllocationMethod = static) **no se admiten actualmente**.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toodeploy un equilibrador de carga con IPv6.

* [Disponibilidad de IPv6 por región](https://go.microsoft.com/fwlink/?linkid=828357)
* [Implementación de un equilibrador de carga con IPv6 mediante una plantilla](load-balancer-ipv6-internet-template.md)
* [Implementación de un equilibrador de carga con IPv6 mediante Azure PowerShell](load-balancer-ipv6-internet-ps.md)
* [Implementación de un equilibrador de carga con IPv6 mediante la CLI de Azure](load-balancer-ipv6-internet-cli.md)
