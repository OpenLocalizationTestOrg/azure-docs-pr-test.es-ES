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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="a8a6d-103">Especificación de una configuración DNS en un archivo de configuración de red virtual</span><span class="sxs-lookup"><span data-stu-id="a8a6d-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="a8a6d-104">Un archivo de configuración de red tiene dos elementos que puede usar la configuración del sistema de nombres de dominio (DNS) de toospecify: **DnsServers** y **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="a8a6d-105">Puede agregar una lista de servidores DNS mediante la especificación de sus direcciones IP y hacer referencia a nombres toohello **DnsServers** elemento.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="a8a6d-106">A continuación, puede usar un **DnsServerRef** toospecify de elemento se usan las entradas de servidor DNS de elemento DnsServers de Hola para sitios de red diferente de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a8a6d-107">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="a8a6d-108">archivo de configuración de red de Hello puede contener Hola siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="a8a6d-109">título de Hola de cada elemento es la página de tooa vinculado que proporciona información adicional acerca de los elementos de hello configuración de valor.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8a6d-110">Para obtener información acerca de cómo tooconfigure Hola archivo de configuración de red, consulte [configurar una red Virtual con un archivo de configuración de red](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="a8a6d-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="a8a6d-111">Para obtener información acerca de cada elemento contenido en el archivo de configuración de red de hello, consulte [esquema de configuración de red Virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8a6d-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="a8a6d-112">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="a8a6d-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="a8a6d-113">Hola **nombre** atributo Hola **DnsServer** elemento se usa solo como referencia para hello **DnsServerRef** elemento.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="a8a6d-114">No representa el nombre de host de hello para el servidor DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="a8a6d-115">Cada **DnsServer** valor de atributo debe ser único en la suscripción de Microsoft Azure todo Hola</span><span class="sxs-lookup"><span data-stu-id="a8a6d-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="a8a6d-116">Elemento Sitios de red virtual</span><span class="sxs-lookup"><span data-stu-id="a8a6d-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="a8a6d-117">En orden toospecify esta configuración para el elemento Virtual Network Sites de hello, deben estar definido previamente en el elemento DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="a8a6d-118">Hola DnsServerRef *nombre* Hola Virtual Network Sites debe hacer referencia tooa nombre valor especificado en el elemento DNS de Hola para DnsServer *nombre*.</span><span class="sxs-lookup"><span data-stu-id="a8a6d-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a8a6d-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8a6d-119">Next steps</span></span>
* <span data-ttu-id="a8a6d-120">Comprender hello [esquema de configuración de red Virtual de Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="a8a6d-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="a8a6d-121">Comprender hello [esquema de configuración de servicio de Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="a8a6d-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="a8a6d-122">[Configuración de una red virtual mediante un archivo de configuración de red](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="a8a6d-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

