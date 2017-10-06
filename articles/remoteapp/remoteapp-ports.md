---
title: aaaList de toowhitelist de puertos y las direcciones URL para Azure RemoteApp implementado en la red virtual de cliente | Documentos de Microsoft
description: "Obtenga información acerca de qué puertos y direcciones URL que necesitará tooconfigure para la comunicación a través de Azure RemoteApp."
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
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Lista de puertos y direcciones URL de acceso de toopermit para Azure RemoteApp implementado en el cliente de red Virtual
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Si va a implementar una colección de nube o híbridas de Azure RemoteApp en una red virtual (VNET), revise Hola siguiendo la información de puerto. Para obtener más información sobre las redes virtuales, consulte la [información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md). Si ha creado un grupo de seguridad de red (NSG) restringir los recursos de red virtual de tráfico toohello en la colección, asegúrese de que Hola después puertos sean accesibles y permitida a través de directivas de seguridad de hello en red virtual de Hola. Para obtener más información sobre los grupos de seguridad de red, consulte el artículo sobre [qué es un grupo de seguridad de red. (NSG)](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Subred de Azure RemoteApp necesita acceso toothese extremos y direcciones URL:
* *.servicebus.windows.net
* *.servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* Saliente: TCP: TCP: 443, 9351, 9352, 10101-10175 
* Opcional. UDP: 10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Clientes de Azure RemoteApp necesitan tener acceso a los puntos de conexión de toothese y las direcciones URL:
Los clientes que quiero decir Hola escritorios, dispositivos, etc. que las personas uso tooconnect toohello aplicaciones implementan en hello colección RemoteApp de Azure.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (puertos UDP opcionales de hello son para esta dirección) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* Saliente: TCP: 443  
* Opcional: UDP: 3391 

