---
title: "aaaOverview de un escenario de recuperación ante desastres de Oracle en el entorno de Azure | Documentos de Microsoft"
description: "Un escenario de recuperación ante desastres para Oracle Database 12c en el entorno de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Recuperación ante desastres para Oracle Database 12c en el entorno de Azure

## <a name="assumptions"></a>Supuestos

- Tiene conocimientos sobre el diseño de Oracle Data Guard y el entorno de Azure.


## <a name="goals"></a>Objetivos
- Diseñar la topología de Hola y configuración que satisfacen las necesidades de recuperación ante desastres.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Escenario 1: sitios principal y de recuperación ante desastres en Azure

Un cliente tiene un Oracle base de datos establecido seguridad en el sitio principal de Hola. El sitio de recuperación ante desastres (DR) se encuentra en una región diferente. cliente de Hello usa a Oracle Data Guard para la recuperación rápida entre estos sitios. sitio primario de Hello también tiene una base de datos secundaria para los informes y otros usos. 

### <a name="topology"></a>Topología

Este es un resumen de hello el programa de instalación de Azure:

- Dos sitios (un sitio principal y un sitio de recuperación ante desastres)
- Dos redes virtuales
- Dos bases de datos de Oracle con Data Guard (principal y en espera)
- Dos bases de datos de Oracle con Golden Gate o Data Guard (solo para el sitio principal)
- Dos de los servicios de aplicaciones, uno principal y otro en el sitio de recuperación ante desastres de Hola
- Un *conjunto de disponibilidad,* que se usa para el servicio de base de datos y aplicaciones en el sitio principal de Hola
- Uno jumpbox en cada sitio, lo que restringe la red privada de acceso toohello y solamente permite el inicio de sesión en un administrador
- El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN en subredes independientes
- El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos

![Captura de pantalla de página de la topología de hello recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Escenario 2: sitio principal en ubicación local y sitio de recuperación ante desastres en Azure

Un cliente tiene una instalación de base de datos de Oracle en un sitio local (sitio principal). Un sitio de recuperación ante desastres en Azure. Oracle Data Guard se usa para la recuperación rápida entre estos sitios. sitio primario de Hello también tiene una base de datos secundaria para los informes y otros usos. 

Existen dos enfoques para esta instalación.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Enfoque 1: Conexiones directas entre local y Azure, la necesidad de abrir los puertos TCP en firewall de Hola 

No se recomienda conexiones directas porque exponen toohello de puertos TCP de hello fuera del mundo.

#### <a name="topology"></a>Topología

Aquí te mostramos un resumen de hello el programa de instalación de Azure:

- Un sitio de recuperación ante desastres 
- Una red virtual
- Una base de datos de Oracle con Data Guard (activo)
- Servicio de una aplicación en el sitio de recuperación ante desastres de Hola
- Uno jumpbox, lo que restringe la red privada de acceso toohello y solamente permite el inicio de sesión en un administrador
- El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN en subredes independientes
- El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos
- El puerto TCP 1521 (o un puerto definido por el usuario) de entrada de un tooallow de directiva o la regla NSG
- Una NSG o la regla de directiva toorestrict solo Hola IP dirección/direcciones locales (base de datos o aplicación) tooaccess Hola red virtual

![Captura de pantalla de página de la topología de hello recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Enfoque 2: VPN de sitio a sitio
Un mejor enfoque consiste en el uso de una VPN de sitio a sitio. Para más información acerca de cómo configurar una VPN, consulte [Creación de una red virtual con una conexión VPN de sitio a sitio mediante la CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Topología

Aquí te mostramos un resumen de hello el programa de instalación de Azure:

- Un sitio de recuperación ante desastres 
- Una red virtual 
- Una base de datos de Oracle con Data Guard (activo)
- Servicio de una aplicación en el sitio de recuperación ante desastres de Hola
- Uno jumpbox, lo que restringe la red privada de acceso toohello y solamente permite el inicio de sesión en un administrador
- El Jumpbox, el servicio de aplicación, la base de datos y la puerta de enlace de VPN se encuentran en subredes independientes
- El grupo de seguridad de red se aplica en las subredes de la aplicación y de base de datos
- Conexión VPN de sitio a sitio entre sistemas locales y Azure

![Captura de pantalla de página de la topología de hello recuperación ante desastres](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Lecturas adicionales

- [Diseño e implementación de una base de datos de Oracle en Azure](oracle-design.md)
- [Configuración de Oracle Data Guard](configure-oracle-dataguard.md)
- [Configuración de Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Copia de seguridad y recuperación de Oracle](oracle-backup-recovery.md)


## <a name="next-steps"></a>Pasos siguientes

- [Tutorial: Creación de máquinas virtuales de alta disponibilidad](../../linux/create-cli-complete.md)
- [Ejemplos de la CLI de Azure para implementación de máquinas virtuales](../../linux/cli-samples.md)
