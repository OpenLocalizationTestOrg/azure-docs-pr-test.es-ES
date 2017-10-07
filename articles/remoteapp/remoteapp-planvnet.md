---
title: "aaaHow tooplan la red virtual para una colección de RemoteApp de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooplan la red virtual para una colección de RemoteApp de Azure."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>¿Cómo tooplan la red virtual de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Este documento se describe cómo tooset seguridad de la red virtual de Azure (VNET) y la subred de Hola para Azure RemoteApp. Si no está familiarizado con redes virtuales de Azure, esto es una capacidad que ayuda a toovirtualize su red infraestructura toohello en la nube y toocreate soluciones híbridas con Azure y a sus recursos locales. Puede leer más sobre este tema [aquí](../virtual-network/virtual-networks-overview.md).

Si desea que las directivas de seguridad de toodefine para el tráfico (entrante o saliente) en la red virtual donde va a implementar Azure RemoteApp, se recomienda crear una subred independiente de Azure RemoteApp del resto de Hola de las implementaciones en hello Azure red virtual. Para obtener más información sobre cómo toodefine las directivas de seguridad en Azure virtual subred de red, lea [¿qué es un grupo de seguridad de red (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Tipos de colecciones de RemoteApp de Azure con redes virtuales de Azure
Hello gráficos siguientes muestran Hola dos opciones de recopilación diferente cuando se desea toouse una red virtual.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Colección en la nube de Azure RemoteApp con VNET
 ![Colección en la nube de Azure RemoteApp con una VNET](./media/remoteapp-planvpn/ra-cloudvpn.png)

Representa una colección de RemoteApp de Azure en todos los recursos de Hola que los hosts de sesión de RemoteApp Hola necesitar tooaccess están implementados en Azure. Pueden estar en hello misma red virtual como Hola RemoteApp VNET o una red virtual diferente en Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Colección híbrida de Azure RemoteApp con VNET
![Colección híbrida de Azure RemoteApp con una VNET](./media/remoteapp-planvpn/ra-hybridvpn.png)

Representa una colección de RemoteApp de Azure donde algunos de los recursos de Hola que los hosts de sesión de RemoteApp Hola necesitar tooaccess están implementadas en las instalaciones. Hola RemoteApp VNET es toohello vinculado local usando tecnologías de híbridos de Azure como VPN de sitio a sitio o Express Route.

## <a name="how-hello-system-works"></a>Funcionamiento del sistema Hola
Tras los bastidores de hello Azure RemoteApp implementa máquinas virtuales de Azure (con la imagen cargada) toohello subred de red virtual que seleccionó durante el aprovisionamiento. Si ha optado por una colección híbrida, intentamos tooresolve Hola FQDN del controlador de dominio de Hola que escribió en hello aprovisionamiento flujo de trabajo con el servidor DNS de hello proporcionado en la red virtual de Hola.  
Si va a conectar tooan de red virtual existente, asegúrese de puertos necesarios de hello tooexpose seguro en los grupos de seguridad de red en la subred de Azure RemoteApp. 

Se recomienda usar una [subred lo suficientemente grande como para Azure RemoteApp](remoteapp-vnetsizing.md). Hola mayor admitida por la red Virtual de Azure es el prefijo/8 (usar definiciones de subred CIDR). La subred debe ser lo suficientemente grande como tooaccommodate todas hello Azure RemoteApp las máquinas virtuales durante la escala vertical cuando los usuarios más acceso a las aplicaciones de Hola. 

Siguiente es cosas Hola deberá tooenable en la subred de red virtual: 

1. Debe permitirse el tráfico saliente de la subred de hello en puerto intervalo 10101 10175 toocommunicate con uno de los servicios de Azure RemoteApp internos de Hola.
2. Se debería permitir el tráfico saliente de su tooAzure de tooconnect de subred almacenamiento en el puerto 443
3. Si tiene Active Directory hospedados en Azure, asegúrese de que todas las máquinas virtuales dentro de la subred de red virtual de Hola para Azure RemoteApp es controlador de dominio de tooconnect puede toothat. Hola DNS en la red virtual de hello debe ser capaz de tooresolve Hola FQDN de este controlador de dominio.

## <a name="virtual-network-with-forced-tunneling"></a>Red virtual con tunelización forzada
[Tunelización forzada](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) es compatible con todas las colecciones nuevas de Azure RemoteApp. Actualmente no admitimos migración Hola de un toosupport de colección existente tunelización forzada.  Deberá toodelete todas las colecciones existentes mediante Hola red virtual que está vinculando tooAzure RemoteApp y cree una una tooget nueva habilitada en las colecciones de tunelización forzada. 

