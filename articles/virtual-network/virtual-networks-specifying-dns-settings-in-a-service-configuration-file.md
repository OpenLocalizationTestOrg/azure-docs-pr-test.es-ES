---
title: "aaaSpecifying configuración de DNS en un archivo de configuración de servicio | Documentos de Microsoft"
description: "Especificación de la configuración de DNS personalizada mediante un archivo de configuración de servicio para una red virtual"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Especificar la configuración DNS en un archivo de configuración de servicio
## <a name="dns-elements"></a>Elementos DNS
Un archivo de configuración de servicio puede contener un elemento DnsServers con una lista de direcciones IPv4 para los servidores de sistema de nombres de dominio (DNS) de Hola Hola servicio va a usar. Configuración de archivo de configuración de servicio de hello tiene prioridad sobre la configuración de archivo de configuración de red de Hola. Para obtener más información, consulte [Esquema de configuración del servicio de Azure (archivo .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Elemento NetworkConfiguration**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Hola **nombre** atributo Hola **DnsServer** elemento solo se usa como un nombre de referencia. No representa el nombre de host de hello para el servidor DNS de Hola. Cada **DnsServer** valor de atributo debe ser único en la suscripción de Microsoft Azure todo Hola.
> 
> 

## <a name="see-also"></a>Otras referencias
[Esquema de configuración del servicio de Azure (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Esquema de configuración de red virtual de Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Configuración de una red virtual mediante un archivo de configuración de red](http://go.microsoft.com/fwlink/?LinkId=248094)

[Acerca de la configuración de red Virtual en el Portal de administración de Hola](http://go.microsoft.com/fwlink/?LinkId=248092)

