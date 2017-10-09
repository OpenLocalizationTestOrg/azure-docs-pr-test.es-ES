---
title: "aaaConfiguring DHCPv6 para máquinas virtuales Linux | Documentos de Microsoft"
description: "¿Cómo tooconfigure DHCPv6 para máquinas virtuales de Linux."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, Azure Load Balancer, pila doble, dirección ip pública, ipv6 nativo, móvil, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="92cb4-104">Configuración de DHCPv6 para VM de Linux</span><span class="sxs-lookup"><span data-stu-id="92cb4-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="92cb4-105">Algunas de las imágenes de máquina virtual de Linux de hello en hello Azure Marketplace no tiene DHCPv6 configurado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="92cb4-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="92cb4-106">toosupport IPv6, DHCPv6 debe configurarse en dentro de la distribución del sistema operativo Linux de Hola que está usando.</span><span class="sxs-lookup"><span data-stu-id="92cb4-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="92cb4-107">Las distintas distribuciones de Linux presentan diversas formas de configurar DHCPv6 al usar paquetes diferentes.</span><span class="sxs-lookup"><span data-stu-id="92cb4-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="92cb4-108">Se han configurado previamente con DHCPv6 recientes imágenes de SUSE Linux y CoreOS en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="92cb4-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="92cb4-109">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="92cb4-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="92cb4-110">Este documento se describe cómo tooenable DHCPv6 para que la máquina virtual de Linux Obtenga una dirección IPv6.</span><span class="sxs-lookup"><span data-stu-id="92cb4-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="92cb4-111">Editar correctamente los archivos de configuración de red puede provocar toolose red acceso tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="92cb4-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="92cb4-112">Recomendamos que pruebe los cambios de configuración en sistemas que no sean de producción.</span><span class="sxs-lookup"><span data-stu-id="92cb4-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="92cb4-113">instrucciones de Hello en este artículo se han probado en las últimas versiones de Hola de imágenes de Linux de hello en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="92cb4-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="92cb4-114">Consulte la documentación de Hola de su versión específica de Linux para obtener instrucciones más detalladas.</span><span class="sxs-lookup"><span data-stu-id="92cb4-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="92cb4-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="92cb4-115">Ubuntu</span></span>

1. <span data-ttu-id="92cb4-116">Editar archivo hello `/etc/dhcp/dhclient6.conf` y agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="92cb4-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="92cb4-117">Modificar configuración de red de hello para la interfaz de hello eth0 con hello siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="92cb4-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="92cb4-118">En **Ubuntu 12.04 y 14.04**, edite el archivo hello`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="92cb4-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="92cb4-119">En **16.04 Ubuntu**, edite el archivo hello`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="92cb4-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="92cb4-120">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="92cb4-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="92cb4-121">Debian</span><span class="sxs-lookup"><span data-stu-id="92cb4-121">Debian</span></span>

1. <span data-ttu-id="92cb4-122">Editar archivo hello `/etc/dhcp/dhclient6.conf` y agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="92cb4-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="92cb4-123">Editar archivo hello `/etc/network/interfaces` y agregue la siguiente configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="92cb4-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="92cb4-124">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="92cb4-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="92cb4-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="92cb4-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="92cb4-126">Editar archivo hello `/etc/sysconfig/network` y agregue Hola después de parámetro:</span><span class="sxs-lookup"><span data-stu-id="92cb4-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="92cb4-127">Editar archivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue Hola dos parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="92cb4-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="92cb4-128">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="92cb4-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="92cb4-129">SLES 11 y openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="92cb4-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="92cb4-130">En Azure se han configurado previamente imágenes de SLES y openSUSE recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="92cb4-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="92cb4-131">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="92cb4-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="92cb4-132">Si tiene una máquina virtual basada en una imagen SUSE anterior o personalizada, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="92cb4-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="92cb4-133">Instalar hello `dhcp-client` del paquete, si es necesario:</span><span class="sxs-lookup"><span data-stu-id="92cb4-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="92cb4-134">Editar archivo hello `/etc/sysconfig/network/ifcfg-eth0` y agregue Hola después de parámetro:</span><span class="sxs-lookup"><span data-stu-id="92cb4-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="92cb4-135">Renovar dirección Hola IPv6:</span><span class="sxs-lookup"><span data-stu-id="92cb4-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="92cb4-136">SLES 12 y openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="92cb4-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="92cb4-137">En Azure se han configurado previamente imágenes de SLES y openSUSE recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="92cb4-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="92cb4-138">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="92cb4-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="92cb4-139">Si tiene una máquina virtual basada en una imagen SUSE anterior o personalizada, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="92cb4-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="92cb4-140">Editar archivo hello `/etc/sysconfig/network/ifcfg-eth0` y reemplazar este parámetro</span><span class="sxs-lookup"><span data-stu-id="92cb4-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="92cb4-141">con hello siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="92cb4-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="92cb4-142">Agregar Hola después parámetro demasiado`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="92cb4-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="92cb4-143">Renovar dirección Hola IPv6:</span><span class="sxs-lookup"><span data-stu-id="92cb4-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="92cb4-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="92cb4-144">CoreOS</span></span>

<span data-ttu-id="92cb4-145">En Azure se han configurado previamente imágenes de CoreOS recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="92cb4-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="92cb4-146">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="92cb4-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="92cb4-147">Si tiene una máquina virtual basada en una imagen de CoreOS anterior o personalizada, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="92cb4-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="92cb4-148">Editar archivo hello`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="92cb4-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="92cb4-149">Renovar dirección Hola IPv6:</span><span class="sxs-lookup"><span data-stu-id="92cb4-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
