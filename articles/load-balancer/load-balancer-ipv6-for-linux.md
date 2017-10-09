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
# <a name="configuring-dhcpv6-for-linux-vms"></a>Configuración de DHCPv6 para VM de Linux

Algunas de las imágenes de máquina virtual de Linux de hello en hello Azure Marketplace no tiene DHCPv6 configurado de forma predeterminada. toosupport IPv6, DHCPv6 debe configurarse en dentro de la distribución del sistema operativo Linux de Hola que está usando. Las distintas distribuciones de Linux presentan diversas formas de configurar DHCPv6 al usar paquetes diferentes.

> [!NOTE]
> Se han configurado previamente con DHCPv6 recientes imágenes de SUSE Linux y CoreOS en hello Azure Marketplace. No es necesario realizar ningún cambio adicional al usar esas imágenes.

Este documento se describe cómo tooenable DHCPv6 para que la máquina virtual de Linux Obtenga una dirección IPv6.

> [!WARNING]
> Editar correctamente los archivos de configuración de red puede provocar toolose red acceso tooyour máquina virtual. Recomendamos que pruebe los cambios de configuración en sistemas que no sean de producción. instrucciones de Hello en este artículo se han probado en las últimas versiones de Hola de imágenes de Linux de hello en hello Azure Marketplace. Consulte la documentación de Hola de su versión específica de Linux para obtener instrucciones más detalladas.

## <a name="ubuntu"></a>Ubuntu

1. Editar archivo hello `/etc/dhcp/dhclient6.conf` y agregue Hola después de línea:

        timeout 10;

2. Modificar configuración de red de hello para la interfaz de hello eth0 con hello siguiente configuración:

   * En **Ubuntu 12.04 y 14.04**, edite el archivo hello`/etc/network/interfaces.d/eth0.cfg`
   * En **16.04 Ubuntu**, edite el archivo hello`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renueve la dirección IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Editar archivo hello `/etc/dhcp/dhclient6.conf` y agregue Hola después de línea:

        timeout 10;

2. Editar archivo hello `/etc/network/interfaces` y agregue la siguiente configuración de hello:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renueve la dirección IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Editar archivo hello `/etc/sysconfig/network` y agregue Hola después de parámetro:

        NETWORKING_IPV6=yes

2. Editar archivo hello `/etc/sysconfig/network-scripts/ifcfg-eth0` y agregue Hola dos parámetros siguientes:

        IPV6INIT=yes
        DHCPV6C=yes

3. Renueve la dirección IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 y openSUSE 13

En Azure se han configurado previamente imágenes de SLES y openSUSE recientes con DHCPv6. No es necesario realizar ningún cambio adicional al usar esas imágenes. Si tiene una máquina virtual basada en una imagen SUSE anterior o personalizada, use Hola pasos:

1. Instalar hello `dhcp-client` del paquete, si es necesario:

    ```bash
    sudo zypper install dhcp-client
    ```

2. Editar archivo hello `/etc/sysconfig/network/ifcfg-eth0` y agregue Hola después de parámetro:

        DHCLIENT6_MODE='managed'

3. Renovar dirección Hola IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 y openSUSE Leap

En Azure se han configurado previamente imágenes de SLES y openSUSE recientes con DHCPv6. No es necesario realizar ningún cambio adicional al usar esas imágenes. Si tiene una máquina virtual basada en una imagen SUSE anterior o personalizada, use Hola pasos:

1. Editar archivo hello `/etc/sysconfig/network/ifcfg-eth0` y reemplazar este parámetro

        #BOOTPROTO='dhcp4'

    con hello siguiente valor:

        BOOTPROTO='dhcp'

2. Agregar Hola después parámetro demasiado`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Renovar dirección Hola IPv6:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

En Azure se han configurado previamente imágenes de CoreOS recientes con DHCPv6. No es necesario realizar ningún cambio adicional al usar esas imágenes. Si tiene una máquina virtual basada en una imagen de CoreOS anterior o personalizada, use Hola pasos:

1. Editar archivo hello`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Renovar dirección Hola IPv6:

    ```bash
    sudo systemctl restart systemd-networkd
    ```
