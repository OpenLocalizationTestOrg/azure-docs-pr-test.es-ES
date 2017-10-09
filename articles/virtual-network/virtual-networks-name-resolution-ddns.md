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
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Usar nombres de host de DNS dinámico tooregister en su propio servidor DNS
[Azure ofrece resolución de nombres](virtual-networks-name-resolution-for-vms-and-role-instances.md) para las máquinas virtuales y las instancias de rol. Sin embargo, cuando la resolución de nombres tiene que ir más allá de lo que Azure ofrece, puede proporcionar sus propios servidores DNS. Esto deja Hola power tootailor su toosuit de solución DNS sus propias necesidades específicas. Por ejemplo, puede que necesite recursos locales de tooaccess a través de su controlador de dominio de Active Directory.

Cuando se hospedan los servidores DNS personalizados como máquinas virtuales de Azure, puede reenviar hostname consulta Hola mismo los nombres de host de red virtual tooAzure tooresolve. Si no desea toouse esta ruta, puede registrar los nombres de host de máquina virtual en el servidor DNS mediante DNS dinámico.  Azure no tiene Hola capacidad (por ejemplo, credenciales) toodirectly crear registros en los servidores DNS, por lo que a menudo son necesarias medidas alternativas. Aquí presentamos algunos escenarios comunes con alternativas.

## <a name="windows-clients"></a>Clientes Windows
Los clientes Windows no unidos a dominio intenta realizar actualizaciones de DNS dinámico (DDNS) no seguro cuando arrancan o cuando su dirección IP cambia. nombre DNS de Hello es el nombre de host de hello más sufijo DNS principal de Hola. Azure deja que el sufijo DNS principal de hello en blanco, pero puede establecer esto en Hola de máquina virtual, a través de hello [UI](https://technet.microsoft.com/library/cc794784.aspx) o [mediante automatización](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Los clientes Unidos a un dominio de Windows registren sus direcciones IP con el controlador de dominio de hello mediante DNS dinámica segura. proceso de unión a dominio de Hello establece el sufijo DNS principal de hello en el cliente de Hola y crea y mantiene la relación de confianza de Hola.

## <a name="linux-clients"></a>Clientes Linux
Los clientes de Linux normalmente no se registran con el servidor DNS de Hola durante el inicio, adoptan el servidor DHCP de hello lo hace. Los servidores DHCP de Azure no tiene capacidad de Hola o registros de tooregister de credenciales en el servidor DNS.  Puede utilizar una herramienta denominada *nsupdate*, que se incluye en el paquete de enlace de hello, las actualizaciones de DNS dinámico toosend. Dado que está normalizado Hola protocolo DNS dinámico, puede usar *nsupdate* incluso cuando no está utilizando enlace en el servidor DNS de Hola.

Puede usar enlaces de Hola que proceden de toocreate de cliente DHCP de Hola y mantener la entrada de nombre de host de hello en el servidor DNS de Hola. Durante el ciclo DHCP de Hola, cliente de hello ejecuta scripts de hello en */etc/dhcp/dhclient-exit-hooks.d/*. Esto puede ser utilizado Hola de tooregister nueva dirección IP mediante el uso de *nsupdate*. Por ejemplo:

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

        
        

También puede usar hello *nsupdate* tooperform comando actualiza DNS dinámica segura. Por ejemplo, cuando usa un servidor Bind DNS, se [genera](http://linux.yyz.us/nsupdate/)un par de claves pública-privada.  el servidor DNS Hello es [configurado](http://linux.yyz.us/dns/ddns-server.html) con la parte pública de Hola de clave de hello, por lo que TI puede comprobar la firma de hello en solicitud de saludo. Debe usar hello *-k* tooprovide opción Hola par de claves demasiado*nsupdate* en orden para hello toobe solicitud firmada de actualización de DNS dinámico.

Si está utilizando un servidor de DNS de Windows, puede utilizar la autenticación Kerberos con hello *-g* parámetro en *nsupdate* (no está disponible en la versión de Windows hello *nsupdate* ). toodo, use *kinit* credenciales de hello tooload (por ejemplo, desde un [archivo keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). A continuación, *nsupdate -g* recogerá credenciales Hola de caché de Hola.

Si es necesario, puede agregar un sufijo de búsqueda DNS tooyour máquinas virtuales. sufijo DNS de Hola se especifica en hello */etc/resolv.conf* archivo. La mayoría de distribuciones de Linux administran automáticamente el contenido de Hola de este archivo, por lo tanto, no se puede editar. Sin embargo, puede invalidar el sufijo de hello mediante el uso del cliente DHCP de hello *sustituir* comando. toodo esto, en */etc/dhcp/dhclient.conf*, agregue:

        supersede domain-name <required-dns-suffix>;

