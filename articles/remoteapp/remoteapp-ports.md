---
title: Lista de puertos y direcciones URL que se deben incluir en la lista blanca de Azure RemoteApp implementada en la red virtual de cliente | Microsoft Docs
description: "Obtenga información sobre qué puertos y direcciones URL tendrá que configurar para la comunicación a través de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Lista de puertos y direcciones URL para permitir el acceso a Azure RemoteApp implementada en el cliente de red virtual
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Si va a implementar una nube de Azure RemoteApp o una colección híbrida en una red virtual (VNET), consulte la siguiente información sobre puertos. Para obtener más información sobre las redes virtuales, consulte la [información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md). Si creó un grupo de seguridad de red (NSG) que restringe el tráfico dirigido a los recursos de red virtual de su colección, asegúrese de que los siguientes puertos sean accesibles y estén permitidos en las directivas de seguridad de la red virtual. Para obtener más información sobre los grupos de seguridad de red, consulte el artículo sobre [qué es un grupo de seguridad de red. (NSG)](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a>La subred de Azure RemoteApp necesita acceso a estos puntos de conexión y direcciones URL:
* *.servicebus.windows.net
* *.servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* Saliente: TCP: TCP: 443, 9351, 9352, 10101-10175 
* Opcional. UDP: 10201-10275  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a>Los clientes Azure RemoteApp necesitan acceso a estos puntos de conexión y direcciones URL:
Por clientes, me refiero a los escritorios, dispositivos etc. que los usuarios usan para conectarse a las aplicaciones implementadas en la colección de Azure RemoteApp.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* Saliente: TCP: 443  
* Opcional: UDP: 3391 

