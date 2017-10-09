---
title: "los nombres de host de DNS dinámico tooregister aaaUsing"
description: "Esta página ofrece detalles acerca de cómo tooset los nombres de host de DNS dinámico tooregister en sus propios servidores DNS."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="e1cee-103">Usar nombres de host de DNS dinámico tooregister en su propio servidor DNS</span><span class="sxs-lookup"><span data-stu-id="e1cee-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="e1cee-104">[Azure ofrece resolución de nombres](virtual-networks-name-resolution-for-vms-and-role-instances.md) para las máquinas virtuales y las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="e1cee-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="e1cee-105">Sin embargo, cuando la resolución de nombres tiene que ir más allá de lo que Azure ofrece, puede proporcionar sus propios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="e1cee-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="e1cee-106">Esto deja Hola power tootailor su toosuit de solución DNS sus propias necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="e1cee-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="e1cee-107">Por ejemplo, puede que necesite recursos locales de tooaccess a través de su controlador de dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1cee-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="e1cee-108">Cuando se hospedan los servidores DNS personalizados como máquinas virtuales de Azure, puede reenviar hostname consulta Hola mismo los nombres de host de red virtual tooAzure tooresolve.</span><span class="sxs-lookup"><span data-stu-id="e1cee-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="e1cee-109">Si no desea toouse esta ruta, puede registrar los nombres de host de máquina virtual en el servidor DNS mediante DNS dinámico.</span><span class="sxs-lookup"><span data-stu-id="e1cee-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="e1cee-110">Azure no tiene Hola capacidad (por ejemplo, credenciales) toodirectly crear registros en los servidores DNS, por lo que a menudo son necesarias medidas alternativas.</span><span class="sxs-lookup"><span data-stu-id="e1cee-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="e1cee-111">Aquí presentamos algunos escenarios comunes con alternativas.</span><span class="sxs-lookup"><span data-stu-id="e1cee-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="e1cee-112">Clientes Windows</span><span class="sxs-lookup"><span data-stu-id="e1cee-112">Windows clients</span></span>
<span data-ttu-id="e1cee-113">Los clientes Windows no unidos a dominio intenta realizar actualizaciones de DNS dinámico (DDNS) no seguro cuando arrancan o cuando su dirección IP cambia.</span><span class="sxs-lookup"><span data-stu-id="e1cee-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="e1cee-114">nombre DNS de Hello es el nombre de host de hello más sufijo DNS principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1cee-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="e1cee-115">Azure deja que el sufijo DNS principal de hello en blanco, pero puede establecer esto en Hola de máquina virtual, a través de hello [UI](https://technet.microsoft.com/library/cc794784.aspx) o [mediante automatización](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="e1cee-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="e1cee-116">Los clientes Unidos a un dominio de Windows registren sus direcciones IP con el controlador de dominio de hello mediante DNS dinámica segura.</span><span class="sxs-lookup"><span data-stu-id="e1cee-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="e1cee-117">proceso de unión a dominio de Hello establece el sufijo DNS principal de hello en el cliente de Hola y crea y mantiene la relación de confianza de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1cee-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="e1cee-118">Clientes Linux</span><span class="sxs-lookup"><span data-stu-id="e1cee-118">Linux clients</span></span>
<span data-ttu-id="e1cee-119">Los clientes de Linux normalmente no se registran con el servidor DNS de Hola durante el inicio, adoptan el servidor DHCP de hello lo hace.</span><span class="sxs-lookup"><span data-stu-id="e1cee-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="e1cee-120">Los servidores DHCP de Azure no tiene capacidad de Hola o registros de tooregister de credenciales en el servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="e1cee-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="e1cee-121">Puede utilizar una herramienta denominada *nsupdate*, que se incluye en el paquete de enlace de hello, las actualizaciones de DNS dinámico toosend.</span><span class="sxs-lookup"><span data-stu-id="e1cee-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="e1cee-122">Dado que está normalizado Hola protocolo DNS dinámico, puede usar *nsupdate* incluso cuando no está utilizando enlace en el servidor DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1cee-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="e1cee-123">Puede usar enlaces de Hola que proceden de toocreate de cliente DHCP de Hola y mantener la entrada de nombre de host de hello en el servidor DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1cee-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="e1cee-124">Durante el ciclo DHCP de Hola, cliente de hello ejecuta scripts de hello en */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="e1cee-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="e1cee-125">Esto puede ser utilizado Hola de tooregister nueva dirección IP mediante el uso de *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="e1cee-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="e1cee-126">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e1cee-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="e1cee-127">También puede usar hello *nsupdate* tooperform comando actualiza DNS dinámica segura.</span><span class="sxs-lookup"><span data-stu-id="e1cee-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="e1cee-128">Por ejemplo, cuando usa un servidor Bind DNS, se [genera](http://linux.yyz.us/nsupdate/)un par de claves pública-privada.</span><span class="sxs-lookup"><span data-stu-id="e1cee-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="e1cee-129">el servidor DNS Hello es [configurado](http://linux.yyz.us/dns/ddns-server.html) con la parte pública de Hola de clave de hello, por lo que TI puede comprobar la firma de hello en solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="e1cee-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="e1cee-130">Debe usar hello *-k* tooprovide opción Hola par de claves demasiado*nsupdate* en orden para hello toobe solicitud firmada de actualización de DNS dinámico.</span><span class="sxs-lookup"><span data-stu-id="e1cee-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="e1cee-131">Si está utilizando un servidor de DNS de Windows, puede utilizar la autenticación Kerberos con hello *-g* parámetro en *nsupdate* (no está disponible en la versión de Windows hello *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="e1cee-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="e1cee-132">toodo, use *kinit* credenciales de hello tooload (por ejemplo, desde un [archivo keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="e1cee-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="e1cee-133">A continuación, *nsupdate -g* recogerá credenciales Hola de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1cee-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="e1cee-134">Si es necesario, puede agregar un sufijo de búsqueda DNS tooyour máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e1cee-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="e1cee-135">sufijo DNS de Hola se especifica en hello */etc/resolv.conf* archivo.</span><span class="sxs-lookup"><span data-stu-id="e1cee-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="e1cee-136">La mayoría de distribuciones de Linux administran automáticamente el contenido de Hola de este archivo, por lo tanto, no se puede editar.</span><span class="sxs-lookup"><span data-stu-id="e1cee-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="e1cee-137">Sin embargo, puede invalidar el sufijo de hello mediante el uso del cliente DHCP de hello *sustituir* comando.</span><span class="sxs-lookup"><span data-stu-id="e1cee-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="e1cee-138">toodo esto, en */etc/dhcp/dhclient.conf*, agregue:</span><span class="sxs-lookup"><span data-stu-id="e1cee-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

