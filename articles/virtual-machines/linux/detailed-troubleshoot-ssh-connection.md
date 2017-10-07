---
title: "aaaDetailed solucionar problemas de SSH para una máquina virtual de Azure | Documentos de Microsoft"
description: "Obtener más pasos para problemas de conexión tooan máquina virtual de Azure para solucionar problemas de SSH"
keywords: "conexión ssh rechazada, error de ssh azure ssh, error de conexión ssh"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>Pasos para problemas de conexión tooa VM de Linux en Azure para solucionar problemas de SSH detallada
Hay muchas razones posibles que ese cliente SSH de hello no podría ser servicio pueda tooreach Hola SSH Hola máquina virtual. Si ha seguido a través de hello más [pasos para solucionar problemas de SSH general](troubleshoot-ssh-connection.md), necesita toofurther solucionar el problema de conexión de Hola. En este artículo le guía a través de toodetermine de pasos de solución de problemas detallada donde no se puede realizar la conexión SSH hello y cómo tooresolve lo.

## <a name="take-preliminary-steps"></a>Pasos previos
Hello siguiente diagrama muestra los componentes de Hola que participan.

![Diagrama que muestra los componentes del servicio SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Hello pasos siguientes ayudarle a aislar el origen de Hola de error de Hola y averiguar soluciones o alternativas.

1. Comprobar estado de Hola de hello VM en el portal de Hola.
   Hola [portal de Azure](https://portal.azure.com), seleccione **máquinas virtuales** > *nombre de máquina virtual*.

   Hello panel de estado para hello VM debe mostrar **ejecutando**. Desplácese hacia abajo de la actividad reciente de tooshow para recursos de red, almacenamiento y proceso.

2. Seleccione **configuración** tooexamine puntos de conexión, direcciones IP, los grupos de seguridad de red y otros valores de configuración.

   Hola VM debe tener un extremo definido para el tráfico SSH que se puede ver en **extremos** o  **[grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md)**. Los puntos de conexión en las máquinas virtuales que se crearon con Resource Manager se almacenan en un grupo de seguridad de red. Además, compruebe que las reglas de hello han aplicado toohello grupo de seguridad de red y que le hace referencia en la subred de Hola.

tooverify conectividad de red, compruebe los puntos de conexión de hello configurado y vea si puede llegar a Hola VM a través de otro protocolo, como HTTP o de otro servicio.

Después de realizar estos pasos, inténtelo de nuevo la conexión de SSH de Hola.

## <a name="find-hello-source-of-hello-issue"></a>Buscar origen Hola problema Hola
cliente de SSH de Hello en el equipo podría producir un error de servicio tooreach Hola SSH hello Azure VM debido tooissues o configuraciones incorrectas en hello siguientes áreas:

* [Equipo cliente de SSH](#source-1-ssh-client-computer)
* [Dispositivo perimetral de la organización](#source-2-organization-edge-device)
* [Extremo de servicio en la nube y lista de control de acceso (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Grupos de seguridad de red](#source-4-network-security-groups)
* [Máquina virtual de Azure basada en Linux](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Causa 1: Equipo cliente de SSH
tooeliminate el equipo como origen de Hola de error de hello, compruebe que puede crear el SSH conexiones tooanother local, equipo basado en Linux.

![Diagrama que resalta los componentes del equipo cliente de SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Si se produce un error en la conexión de hello, busque Hola problemas siguientes en el equipo:

* Una configuración del firewall local que está bloqueando el tráfico SSH entrante o saliente (TCP 22)
* Software de proxy de cliente instalado localmente que impide las conexiones a SSH
* Software de supervisión de red instalado localmente que impide las conexiones a SSH
* Otro tipo de software de seguridad que o bien, supervisar el tráfico o bien, permite o impide ciertos tipos de tráfico.

Si alguna de estas condiciones se aplica, temporalmente deshabilitar software Hola e intente un toofind de equipo local SSH conexión tooan razón Hola conexión Hola está bloqueado en el equipo. Trabajar con las conexiones de SSH red administrador toocorrect Hola software configuración tooallow.

Si usa la autenticación de certificado, compruebe que dispone de estos permisos toohello .ssh carpeta en su directorio particular:

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (o cualquier otro archivo en el que tenga almacenadas las claves privadas)
* Chmod 644 ~/.ssh/known_hosts (contiene hosts que se haya conectado toovia SSH)

## <a name="source-2-organization-edge-device"></a>Causa 2: Dispositivo perimetral de la organización
tooeliminate el dispositivo de borde de la organización como origen de Hola de error de hello, compruebe que un equipo que está conectado directamente toohello Internet puede crear conexiones de SSH tooyour máquina virtual de Azure. Si tiene acceso Hola VM mediante una VPN de sitio a sitio o una conexión ExpressRoute de Azure, omitir demasiado[origen 4: grupos de seguridad de red](#nsg).

![Diagrama que resalta el dispositivo perimetral de la organización](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Si no tiene un equipo que está conectado directamente toohello Internet, cree una nueva máquina virtual de Azure en su propio servicio de nube o de grupo de recursos y usarlo. Para más información, consulte [Creación de una máquina virtual que ejecuta Linux en Azure](quick-create-cli.md). Eliminar servicio de grupo o máquina virtual y en la nube de recursos de hello cuando haya terminado con las pruebas.

Si puede crear una conexión SSH con un equipo que está conectado directamente toohello Internet, compruebe el dispositivo de borde de la organización para:

* Un servidor de seguridad interno que está bloqueando el tráfico SSH con hello Internet
* Un servidor proxy que impide las conexiones SSH
* Software de detección de intrusiones o supervisión de red en ejecución en los dispositivos de la red perimetral que impide las conexiones SSH

Trabajar con la configuración de Hola de toocorrect de administrador de red del tráfico organización borde dispositivos tooallow SSH con hello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Causa 3: extremo de servicio en la nube y ACL
> [!NOTE]
> Este origen aplica solo tooVMs que se crearon con el modelo de implementación clásica de Hola. Para las máquinas virtuales que se crearon mediante el Administrador de recursos, omita demasiado[origen 4: grupos de seguridad de red](#nsg).

extremo de servicio de nube de hello tooeliminate y ACL como origen de Hola de error de hello, compruebe que otra máquina virtual de Azure en Hola misma red virtual puede hacer SSH conexiones tooyour máquina virtual.

![Diagrama que resalta el punto de conexión del servicio en la nube y ACL](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Si no tienes otra máquina virtual en hello misma red virtual, puede crear fácilmente uno. Para obtener más información, consulte [crear una VM de Linux en Azure con hello CLI](quick-create-cli.md). Eliminar Hola máquina virtual extra cuando haya terminado con las pruebas.

Si puede crear una conexión SSH con una máquina virtual en mismo virtual Hola de red, compruebe Hola siguientes áreas:

* **configuración de extremo de Hello para el tráfico SSH en el destino de hello máquina virtual.** Hola privada el puerto TCP del extremo de hello debe coincidir con el puerto TCP de hello en qué Hola SSH servicio en hello VM está escuchando. (el puerto predeterminado de hello es 22). Compruebe el número de puerto TCP SSH Hola Hola portal de Azure seleccionando **máquinas virtuales** > *nombre de máquina virtual* > **configuración**  >  **Extremos**.
* **Hola ACL para punto de conexión del tráfico SSH de hello en la máquina virtual de destino de Hola.** Una ACL permite toospecify permitirá o denegará el tráfico entrante de hello Internet, en función de su dirección IP de origen. ACL mal configuradas pueden impedir que el punto de conexión de entrada SSH tráfico toohello. Compruebe su tooensure de ACL que se permite el tráfico entrante desde direcciones IP públicas de Hola de su servidor proxy u otro servidor de borde. Para obtener más información, consulte [Acerca de las listas de control de acceso (ACL) de red](../../virtual-network/virtual-networks-acl.md).

extremo de hello tooeliminate como origen del problema de hello, quitar punto de conexión actual de hello, crear otro punto de conexión y especificar nombre SSH de hello (puerto TCP 22 para el número de puerto público y privado de hello). Para obtener más información, vea [Configuración de puntos de conexión en una máquina virtual en Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Causa 4: Grupos de seguridad de red
Grupos de seguridad de red permiten toohave tener más control sobre el tráfico entrante y saliente permitido. Puede crear reglas que abarquen subredes y servicios en la nube en una red virtual de Azure. Compruebe su tooensure de reglas del grupo de seguridad de red que tooand de tráfico SSH de hello que Internet está permitido.
Para obtener más información, consulte [Acerca de los grupos de seguridad de red](../../virtual-network/virtual-networks-nsg.md).

También puede utilizar la configuración de IP comprobar toovalidate hello NSG. Para más información, consulte [Información general sobre la supervisión de red de Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Causa 5: Máquina virtual de Azure basada en Linux
Hola último origen de los posibles problemas es hello Azure máquina virtual propiamente dicha.

![Diagrama que resalta la máquina virtual de Azure basada en Linux](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Si aún no lo ha hecho lo ha hecho, siga las instrucciones de hello [tooreset una contraseña o SSH para máquinas virtuales basadas en Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Pruebe de nuevo la conexión desde su equipo. Si sigue sin funcionar, siguiente Hola es algunos de los posibles problemas de hello:

* Hola servicio SSH no se está ejecutando en la máquina virtual de destino de Hola.
* Hola servicio SSH no está escuchando en el puerto TCP 22. tootest, instale un cliente telnet en el equipo local y ejecute "telnet *cloudServiceName*. cloudapp.net 22". Este paso determina si máquina virtual de hello permite que el punto de conexión de comunicación entrante y saliente toohello SSH.
* firewall local de Hello en la máquina virtual de destino de hello tiene reglas que impidan que el tráfico entrante o saliente de SSH.
* La detección de intrusiones o software que se ejecuta en la máquina virtual de Azure Hola de supervisión de red impide las conexiones SSH.

## <a name="additional-resources"></a>Recursos adicionales
Para obtener más información sobre cómo solucionar problemas de acceso a la aplicación, consulte [aplicación tooan solucionar access que ejecuta en una máquina virtual de Azure](troubleshoot-app-connection.md)
