---
title: "Especificación de la configuración DNS en un archivo de configuración de servicio | Microsoft Docs"
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
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="11539-103">Especificar la configuración DNS en un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="11539-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="11539-104">Elementos DNS</span><span class="sxs-lookup"><span data-stu-id="11539-104">DNS elements</span></span>
<span data-ttu-id="11539-105">Un archivo de configuración de servicio puede contener un elemento DnsServers con una lista de direcciones IPv4 de los servidores de sistema de nombres de dominio (DNS) que el servicio usará.</span><span class="sxs-lookup"><span data-stu-id="11539-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="11539-106">La configuración en el archivo de configuración de servicio sobrescribirá la del archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="11539-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="11539-107">Para obtener más información, consulte [Esquema de configuración del servicio de Azure (archivo .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="11539-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="11539-108">**Elemento NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="11539-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="11539-109">El atributo **name** en el elemento **DnsServer** solo se usa como nombre de referencia.</span><span class="sxs-lookup"><span data-stu-id="11539-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="11539-110">No representa el nombre de host del servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="11539-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="11539-111">Cada valor del atributo **DnsServer** debe ser único en toda la suscripción de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="11539-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="11539-112">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="11539-112">See Also</span></span>
[<span data-ttu-id="11539-113">Esquema de configuración del servicio de Azure (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="11539-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="11539-114">Esquema de configuración de red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="11539-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="11539-115">Configuración de una red virtual mediante un archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="11539-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="11539-116">Información acerca de la configuración de red virtual en el Portal de administración</span><span class="sxs-lookup"><span data-stu-id="11539-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

