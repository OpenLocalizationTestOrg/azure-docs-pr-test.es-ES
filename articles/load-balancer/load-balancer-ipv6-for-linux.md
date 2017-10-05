---
title: "Configuración de DHCPv6 para VM de Linux | Microsoft Docs"
description: "Cómo configurar DHCPv6 para VM de Linux."
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="98452-104">Configuración de DHCPv6 para VM de Linux</span><span class="sxs-lookup"><span data-stu-id="98452-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="98452-105">Algunas de las imágenes de la máquina virtual con Linux en Azure Marketplace no tienen DHCPv6 configurado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="98452-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="98452-106">Para admitir IPv6, DHCPv6 debe configurarse en la distribución de sistema operativo Linux que usa.</span><span class="sxs-lookup"><span data-stu-id="98452-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="98452-107">Las distintas distribuciones de Linux presentan diversas formas de configurar DHCPv6 al usar paquetes diferentes.</span><span class="sxs-lookup"><span data-stu-id="98452-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="98452-108">En Azure Marketplace se han configurado previamente imágenes de SUSE Linux y CoreOS recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="98452-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="98452-109">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="98452-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="98452-110">En este documento se describe cómo habilitar DHCPv6 para que su máquina virtual con Linux obtenga una dirección IPv6.</span><span class="sxs-lookup"><span data-stu-id="98452-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="98452-111">La edición incorrecta de archivos de configuración de red puede dar lugar a la pérdida de acceso de red a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="98452-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="98452-112">Recomendamos que pruebe los cambios de configuración en sistemas que no sean de producción.</span><span class="sxs-lookup"><span data-stu-id="98452-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="98452-113">Las instrucciones de este artículo se han probado en las versiones más recientes de las imágenes Linux en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="98452-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="98452-114">Consulte la documentación de su versión específica de Linux para obtener instrucciones más detalladas.</span><span class="sxs-lookup"><span data-stu-id="98452-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="98452-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="98452-115">Ubuntu</span></span>

1. <span data-ttu-id="98452-116">Edite el archivo `/etc/dhcp/dhclient6.conf` y agregue la línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="98452-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="98452-117">Edite la configuración de red de la interfaz eth0 con la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="98452-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="98452-118">En **Ubuntu 12.04 y 14.04**, edite el archivo `/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="98452-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="98452-119">En **Ubuntu 16.04**, edite el archivo `/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="98452-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="98452-120">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="98452-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="98452-121">Debian</span><span class="sxs-lookup"><span data-stu-id="98452-121">Debian</span></span>

1. <span data-ttu-id="98452-122">Edite el archivo `/etc/dhcp/dhclient6.conf` y agregue la línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="98452-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="98452-123">Edite el archivo `/etc/network/interfaces` y agregue la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="98452-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="98452-124">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="98452-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="98452-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="98452-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="98452-126">Edite el archivo `/etc/sysconfig/network` y agregue el parámetro siguiente:</span><span class="sxs-lookup"><span data-stu-id="98452-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="98452-127">Edite el archivo `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue los dos parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="98452-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="98452-128">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="98452-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="98452-129">SLES 11 y openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="98452-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="98452-130">En Azure se han configurado previamente imágenes de SLES y openSUSE recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="98452-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="98452-131">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="98452-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="98452-132">Si tiene una máquina virtual basada en una imagen de SUSE anterior o personalizada, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98452-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="98452-133">Instale el paquete `dhcp-client` , en caso de ser necesario:</span><span class="sxs-lookup"><span data-stu-id="98452-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="98452-134">Edite el archivo `/etc/sysconfig/network/ifcfg-eth0` y agregue el parámetro siguiente:</span><span class="sxs-lookup"><span data-stu-id="98452-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="98452-135">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="98452-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="98452-136">SLES 12 y openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="98452-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="98452-137">En Azure se han configurado previamente imágenes de SLES y openSUSE recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="98452-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="98452-138">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="98452-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="98452-139">Si tiene una máquina virtual basada en una imagen de SUSE anterior o personalizada, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98452-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="98452-140">Edite el archivo `/etc/sysconfig/network/ifcfg-eth0` y reemplace este parámetro</span><span class="sxs-lookup"><span data-stu-id="98452-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="98452-141">por el siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="98452-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="98452-142">Agregue el parámetro siguiente a `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="98452-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="98452-143">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="98452-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="98452-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="98452-144">CoreOS</span></span>

<span data-ttu-id="98452-145">En Azure se han configurado previamente imágenes de CoreOS recientes con DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="98452-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="98452-146">No es necesario realizar ningún cambio adicional al usar esas imágenes.</span><span class="sxs-lookup"><span data-stu-id="98452-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="98452-147">Si tiene una máquina virtual basada en una imagen de CoreOS anterior o personalizada, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98452-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="98452-148">Edite el archivo `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="98452-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="98452-149">Renueve la dirección IPv6:</span><span class="sxs-lookup"><span data-stu-id="98452-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
