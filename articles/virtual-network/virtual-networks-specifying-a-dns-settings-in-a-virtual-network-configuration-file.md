---
title: "aaaSpecifying configuración DNS en un archivo de configuración de red virtual | Documentos de Microsoft"
description: "¿Cómo toochange configuración del servidor DNS en una red virtual con una configuración de red virtual de archivos en el modelo de implementación clásica de Hola"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Especificación de una configuración DNS en un archivo de configuración de red virtual
Un archivo de configuración de red tiene dos elementos que puede usar la configuración del sistema de nombres de dominio (DNS) de toospecify: **DnsServers** y **DnsServerRef**. Puede agregar una lista de servidores DNS mediante la especificación de sus direcciones IP y hacer referencia a nombres toohello **DnsServers** elemento. A continuación, puede usar un **DnsServerRef** toospecify de elemento se usan las entradas de servidor DNS de elemento DnsServers de Hola para sitios de red diferente de la red virtual.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación clásica de Hola.

archivo de configuración de red de Hello puede contener Hola siguientes elementos. título de Hola de cada elemento es la página de tooa vinculado que proporciona información adicional acerca de los elementos de hello configuración de valor.

> [!IMPORTANT]
> Para obtener información acerca de cómo tooconfigure Hola archivo de configuración de red, consulte [configurar una red Virtual con un archivo de configuración de red](virtual-networks-using-network-configuration-file.md). Para obtener información acerca de cada elemento contenido en el archivo de configuración de red de hello, consulte [esquema de configuración de red Virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[Elemento DNS](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Hola **nombre** atributo Hola **DnsServer** elemento se usa solo como referencia para hello **DnsServerRef** elemento. No representa el nombre de host de hello para el servidor DNS de Hola. Cada **DnsServer** valor de atributo debe ser único en la suscripción de Microsoft Azure todo Hola
> 
> 

[Elemento Sitios de red virtual](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> En orden toospecify esta configuración para el elemento Virtual Network Sites de hello, deben estar definido previamente en el elemento DNS de Hola. Hola DnsServerRef *nombre* Hola Virtual Network Sites debe hacer referencia tooa nombre valor especificado en el elemento DNS de Hola para DnsServer *nombre*.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Comprender hello [esquema de configuración de red Virtual de Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Comprender hello [esquema de configuración de servicio de Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Configuración de una red virtual mediante un archivo de configuración de red](virtual-networks-using-network-configuration-file.md).

