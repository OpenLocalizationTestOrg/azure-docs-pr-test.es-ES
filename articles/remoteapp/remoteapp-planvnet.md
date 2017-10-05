---
title: "Planeación de la red virtual para una colección de Azure RemoteApp | Microsoft Docs"
description: "Información sobre cómo planificar la red virtual para una colección de Azure RemoteApp."
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
ms.openlocfilehash: 1eb8115b13fb18074b4c4726b69e3d9faf387c32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a>Cómo planificar la red virtual para Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

En este documento se describe cómo configurar la red virtual (VNET) de Azure y la subred para Azure RemoteApp. Si no estás familiarizado con las redes virtuales de Azure, esta es una capacidad que te ayuda a virtualizar tu infraestructura de red en la nube y a crear soluciones híbridas con Azure y con tus recursos locales. Puede leer más sobre este tema [aquí](../virtual-network/virtual-networks-overview.md).

Si quieres definir directivas de seguridad para el tráfico (entrante y saliente) en la red virtual donde vas a implementar Azure RemoteApp, te recomendamos que crees una subred de Azure RemoteApp independiente del resto de las implementaciones de la red virtual de Azure. Para obtener más información sobre cómo definir las directivas de seguridad de la subred de red virtual de Azure, lee [¿Qué es un grupo de seguridad de red (NSG)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Tipos de colecciones de RemoteApp de Azure con redes virtuales de Azure
Los gráficos siguientes muestran las dos opciones de colección diferentes para cuando quieres usar una red virtual.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Colección en la nube de Azure RemoteApp con VNET
 ![Colección en la nube de Azure RemoteApp con una VNET](./media/remoteapp-planvpn/ra-cloudvpn.png)

Esto representa una colección de Azure RemoteApp donde se implementan en Azure todos los recursos a los que necesitan acceder los hosts de sesión de RemoteApp. Pueden estar en la misma VNET que la VNET de RemoteApp o en una VNET de Azure diferente.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Colección híbrida de Azure RemoteApp con VNET
![Colección híbrida de Azure RemoteApp con una VNET](./media/remoteapp-planvpn/ra-hybridvpn.png)

Esto representa una colección de Azure RemoteApp donde se implementan localmente algunos de los recursos a los que necesitan acceder los hosts de sesión de RemoteApp. La RemoteApp de VNET está vinculada a la red local mediante tecnologías híbridas de Azure como las VPN de sitio a sitio o Express Route.

## <a name="how-the-system-works"></a>Funcionamiento del sistema
En un segundo plano, Azure RemoteApp implementa máquinas virtuales de Azure (con tu imagen cargada) a la subred de red virtual que elegiste durante el aprovisionamiento. Si optaste por una colección híbrida, se intenta resolver el FQDN del controlador de dominio que escribiste en el flujo de trabajo de aprovisionamiento con el servidor DNS proporcionado en la red virtual.  
Si te conectas a una red virtual existente, asegúrate de exponer los puertos necesarios en los grupos de seguridad de red en la subred de Azure RemoteApp. 

Se recomienda usar una [subred lo suficientemente grande como para Azure RemoteApp](remoteapp-vnetsizing.md). La más grande compatible con la Red virtual de Azure es de /8 (usando las definiciones de subred CIDR). La subred tiene que ser lo suficientemente grande como para dar cabida a todas las VM de Azure RemoteApp durante la escala vertical cuando hay más usuarios accediendo a las aplicaciones. 

Esto es lo que tienes que habilitar en la subred de red virtual: 

1. Se debe permitir el tráfico saliente de la subred en el intervalo de puertos 10101-10175 para que se pueda comunicar con uno de los servicios internos de Azure RemoteApp.
2. Se debe permitir el tráfico saliente desde tu subred para que se pueda conectar al almacenamiento de Azure en el puerto 443
3. Si dispones de Active Directory hospedado en Azure, asegúrate de que todas las VM de la subred de red virtual de RemoteApp de Azure se pueden conxtar a ese controlador de dominio. El DNS de la red virtual tiene que poder resolver el FQDN de este controlador de dominio.

## <a name="virtual-network-with-forced-tunneling"></a>Red virtual con tunelización forzada
[Tunelización forzada](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) es compatible con todas las colecciones nuevas de Azure RemoteApp. Actualmente no se admite que la migración de una colección existente admita la tunelización forzada.  Tendrás que eliminar todas las colecciones existentes mediante la VNET que quieres vincular a Azure RemoteApp y crear una nueva para tener habilitada la tunelización forzada en las colecciones. 

