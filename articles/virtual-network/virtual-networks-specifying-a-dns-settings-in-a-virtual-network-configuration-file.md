---
title: "Especificación de una configuración DNS en un archivo de configuración de red virtual | Microsoft Docs"
description: "Cómo cambiar la configuración del servidor DNS en una red virtual con un archivo de configuración de red virtual en el modelo de implementación clásico"
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
ms.openlocfilehash: ec33268915a1888509834ce6a5b2bc782a12ce4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="334cc-103">Especificación de una configuración DNS en un archivo de configuración de red virtual</span><span class="sxs-lookup"><span data-stu-id="334cc-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="334cc-104">Un archivo de configuración de red tiene dos elementos que puede usar para especificar la configuración del sistema de nombres de dominio (DNS): **DnsServers** y **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="334cc-104">A network configuration file has two elements that you can use to specify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="334cc-105">Puede agregar una lista de los servidores DNS especificando sus direcciones IP y nombres de referencia en el elemento **DnsServers** .</span><span class="sxs-lookup"><span data-stu-id="334cc-105">You can add a list of DNS servers by specifying their IP addresses and reference names to the **DnsServers** element.</span></span> <span data-ttu-id="334cc-106">Asimismo, puede usar un elemento **DnsServerRef** para especificar qué entradas del servidor DNS desde el elemento DnsServers se usan en diferentes sitios de red de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="334cc-106">You can then use a **DnsServerRef** element to specify which DNS server entries from the DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="334cc-107">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="334cc-107">This article covers the classic deployment model.</span></span>

<span data-ttu-id="334cc-108">El archivo de configuración de red puede contener los siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="334cc-108">The network configuration file may contain the following elements.</span></span> <span data-ttu-id="334cc-109">El título de cada elemento se vincula a una página que proporciona información adicional acerca de la configuración del valor de elemento.</span><span class="sxs-lookup"><span data-stu-id="334cc-109">The title of each element is linked to a page that provides additional information about the element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="334cc-110">Para obtener más información sobre cómo configurar el archivo de configuración de red, consulte [Configuración de una red virtual mediante un archivo de configuración de red](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="334cc-110">For information about how to configure the network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="334cc-111">Para obtener más información acerca de cada elemento de un archivo de configuración de red, consulte [Esquema de configuración de redes virtuales de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="334cc-111">For information about each element contained in the network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="334cc-112">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="334cc-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="334cc-113">El atributo **name** en el elemento **DnsServer** solo se usa como referencia del elemento **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="334cc-113">The **name** attribute in the **DnsServer** element is used only as a reference for the **DnsServerRef** element.</span></span> <span data-ttu-id="334cc-114">No representa el nombre de host del servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="334cc-114">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="334cc-115">Cada valor del atributo **DnsServer** debe ser único en toda la suscripción de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="334cc-115">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="334cc-116">Elemento Sitios de red virtual</span><span class="sxs-lookup"><span data-stu-id="334cc-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="334cc-117">Para especificar la configuración del elemento Sitios de red virtual, debe definirse previamente en el elemento DNS.</span><span class="sxs-lookup"><span data-stu-id="334cc-117">In order to specify this setting for the Virtual Network Sites element, it must be previously defined in the DNS element.</span></span> <span data-ttu-id="334cc-118">El atributo *name* DnsServerRef del elemento Sitios de red virtual tiene que hacer referencia a un valor de nombre especificado en el elemento DNS del atributo *name* DnsServer.</span><span class="sxs-lookup"><span data-stu-id="334cc-118">The DnsServerRef *name* in the Virtual Network Sites element must refer to a name value specified in the DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="334cc-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="334cc-119">Next steps</span></span>
* <span data-ttu-id="334cc-120">Entienda el [esquema de configuración de la red virtual de Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="334cc-120">Understand the [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="334cc-121">Entienda el [esquema de configuración del servicio de Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="334cc-121">Understand the [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="334cc-122">[Configuración de una red virtual mediante un archivo de configuración de red](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="334cc-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

