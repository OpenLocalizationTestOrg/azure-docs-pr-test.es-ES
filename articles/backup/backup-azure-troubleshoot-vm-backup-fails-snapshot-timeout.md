---
title: "Solución del error de Azure Backup: no está disponible el estado del agente invitado | Documentos de Microsoft"
description: "Síntomas, causas y soluciones de copia de seguridad de Azure errores relacionado tooerror: no se pudo comunicar con el agente de máquina virtual de Hola"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Azure Backup; Agente de máquina virtual; Conectividad de red;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Solución de errores de Azure Backup: problemas con el agente o la extensión

Este artículo proporciona tooproblems en la comunicación con el agente de máquina virtual y la extensión relacionados con la solución de problemas de pasos toohelp resolver errores de copia de seguridad.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Agente de máquina virtual no se puede toocommunicate con copia de seguridad de Azure
Después de registrar y programar una máquina virtual para hello servicio de copia de seguridad de Azure, copia de seguridad inicia el trabajo de Hola comunicándose con hello tootake de agente de máquina virtual una instantánea en un momento. Cualquiera de hello condiciones siguientes pueden impedir instantánea Hola desde que se desencadena, lo que a su vez puede provocar errores de tooBackup. Siga debajo de la solución de problemas de pasos de hello dado orden y vuelva a intentar la operación.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [Hola VM no tiene acceso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [agente Hola se instala en hello VM pero no responde (para máquinas virtuales de Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [agente Hola instalado Hola VM está anticuada (para máquinas virtuales de Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [no se puede recuperar el estado de la instantánea de Hola o no se puede tomar una instantánea](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [se produce un error en la extensión de copia de seguridad de hello tooupdate o carga](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Error en la operación de instantánea debido toono conectividad de red en la máquina virtual de Hola
Después de registrar y programar una máquina virtual para hello servicio copia de seguridad de Azure, copia de seguridad inicia trabajo Hola comunicándose con instantánea de tootake un punto en el tiempo de extensión de copia de seguridad de VM de Hola. Cualquiera de hello condiciones siguientes pueden impedir instantánea Hola desde que se desencadena, lo que a su vez puede provocar errores de tooBackup. Siga debajo de la solución de problemas de pasos de hello dado orden y vuelva a intentar la operación.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [Hola VM no tiene acceso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 2: [no se puede recuperar el estado de la instantánea de Hola o no se puede tomar una instantánea](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 3: [se produce un error en la extensión de copia de seguridad de hello tooupdate o carga](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Error en la operación de extensión de VMSnapshot

Después de registrar y programar una máquina virtual para hello servicio copia de seguridad de Azure, copia de seguridad inicia trabajo Hola comunicándose con instantánea de tootake un punto en el tiempo de extensión de copia de seguridad de VM de Hola. Cualquiera de hello condiciones siguientes pueden impedir instantánea Hola desde que se desencadena, lo que a su vez puede provocar errores de tooBackup. Siga debajo de la solución de problemas de pasos de hello dado orden y vuelva a intentar la operación.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 1: [no se puede recuperar el estado de la instantánea de Hola o no se puede tomar una instantánea](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 2: [se produce un error en la extensión de copia de seguridad de hello tooupdate o carga](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [Hola VM no tiene acceso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 4: [agente Hola se instala en hello VM pero no responde (para máquinas virtuales de Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 5: [agente Hola instalado Hola VM está anticuada (para máquinas virtuales de Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Operación de hello tooperform no se puede como Hola agente de máquina virtual no está respondiendo

Después de registrar y programar una máquina virtual para hello servicio copia de seguridad de Azure, copia de seguridad inicia trabajo Hola comunicándose con instantánea de tootake un punto en el tiempo de extensión de copia de seguridad de VM de Hola. Cualquiera de hello condiciones siguientes pueden impedir instantánea Hola desde que se desencadena, lo que a su vez puede provocar errores de tooBackup. Siga debajo de la solución de problemas de pasos de hello dado orden y vuelva a intentar la operación.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 1: [agente Hola se instala en hello VM pero no responde (para máquinas virtuales de Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 2: [agente Hola instalado Hola VM está anticuada (para máquinas virtuales de Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [Hola VM no tiene acceso a Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Error de copia de seguridad a un error interno: vuelva a intentar la operación de hello en unos minutos

Después de registrar y programar una máquina virtual para hello servicio copia de seguridad de Azure, copia de seguridad inicia trabajo Hola comunicándose con instantánea de tootake un punto en el tiempo de extensión de copia de seguridad de VM de Hola. Cualquiera de hello condiciones siguientes pueden impedir instantánea Hola desde que se desencadena, lo que a su vez puede provocar errores de tooBackup. Siga debajo de la solución de problemas de pasos de hello dado orden y vuelva a intentar la operación.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [Hola VM no tiene acceso a Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [agente de hello instalado Hola VM pero no responde (para máquinas virtuales de Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [agente Hola instalado Hola VM está anticuada (para máquinas virtuales de Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [no se puede recuperar el estado de la instantánea de Hola o no se puede tomar una instantánea](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [se produce un error en la extensión de copia de seguridad de hello tooupdate o carga](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Causas y soluciones

### <a name="hello-vm-has-no-internet-access"></a>Hola VM no tiene acceso a Internet
Por requisitos de implementación de Hola Hola VM no tiene acceso a Internet, o tiene restricciones en su lugar que impiden el acceso toohello infraestructura de Azure.

toofunction correctamente, extensión de copia de seguridad de hello requiere conectividad toohello las direcciones IP pública de Azure. extensión de Hello envía comandos tooan almacenamiento de Azure extremo (dirección URL de HTTP) toomanage hello las instantáneas de hello máquina virtual. Si hello extensión no tiene ningún toohello de acceso que se produce un error en la red pública de Internet, copia de seguridad al final.

####  <a name="solution"></a>Solución
problema de hello tooresolve, pruebe uno de métodos de hello enumerados aquí.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Permitir el acceso a los intervalos IP de centro de datos Azure toohello

1. Obtener hello [lista de direcciones IP del centro de datos Azure](https://www.microsoft.com/download/details.aspx?id=41653) tooallow acceso a.
2. Desbloquear Hola direcciones IP mediante la ejecución de hello **New-NetRoute** cmdlet Hola VM de Azure en una ventana de PowerShell con privilegios elevados. Ejecute el cmdlet de hello como administrador.
3. tooallow toohello de acceso de direcciones IP, agregue el grupo de seguridad de red de toohello de reglas si dispone de uno.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Crear una ruta de acceso para tooflow de tráfico HTTP

1. Si tiene las restricciones de red en su lugar (por ejemplo, un grupo de seguridad de red), implementar un proxy server tooroute Hola el tráfico HTTP.
2. tooallow toohello de acceso a Internet desde el servidor de proxy HTTP de hello, agregue el grupo de seguridad de red de toohello de reglas si dispone de uno.

toolearn tooset un proxy HTTP para copias de seguridad de la máquina virtual, vea [preparar su tooback entorno las máquinas virtuales de Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

En caso de que usas discos administrados, puede que necesite un puerto adicional (8443) abre firewalls Hola.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>agente de Hello instalado Hola VM pero no responde (para máquinas virtuales de Windows)

#### <a name="solution"></a>Solución
Hola agente de máquina virtual podría haberse dañado o servicio Hola se han detenido. Volver a instalar agente de máquina virtual de hello ayudaría a obtener la versión más reciente de Hola y reinicie la comunicación de Hola.

1. Compruebe si el servicio de agente de invitado de Windows que se ejecuta en servicios (services.msc) de Hola Máquina Virtual. Pruebe a reiniciar el servicio del agente de invitado de Windows hello e iniciar Hola copia de seguridad<br>
2. Si no lo ve en los servicios, compruebe en Programas y características si el servicio Windows Guest Agent está instalado.
4. Si es capaz de tooview en programas y características Hola Desinstalar agente de invitado de Windows.
5. Descargue e instale hello [versión más reciente de MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Necesita la instalación de Hola de toocomplete de privilegios de administrador.
6. A continuación, debe ser capaz de tooview servicios de agente de invitado de Windows en servicios
7. Vuelva a ejecutar una copia de seguridad de en-petición / "ad hoc", haga clic en "Copia de seguridad ahora" en el portal de Hola.

Compruebe también la máquina Virtual tiene  **[.NET 4.5 instalado en el sistema de hello](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Se requiere para hello toocommunicate de agente VM con el servicio de Hola

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>agente de Hello instalado en hello VM está anticuada (para máquinas virtuales de Linux)

#### <a name="solution"></a>Solución
La mayoría de los errores relacionados con el agente o la extensión de máquinas virtuales de Linux están provocados por problemas que afectan a un agente VM obsoleto. tootroubleshoot este problema, siga estas directrices generales:

1. Siga las instrucciones de Hola para [actualizar Hola agente de VM de Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Se *recomienda* actualizar agente Hola sólo a través de un repositorio de distribución. No se recomienda descargar código de hello agente directamente desde GitHub y actualizarlo. Si no está disponible para su distribución agente más reciente de hello, póngase en contacto con el soporte de distribución para obtener instrucciones sobre cómo tooinstall lo. toocheck para hello más reciente del agente, vaya toohello [agente Linux de Windows Azure](https://github.com/Azure/WALinuxAgent/releases) página en el repositorio de GitHub de Hola.

2. Asegúrese de que ese Hola agente de Azure se ejecuta en hello VM ejecutando el siguiente comando de hello:`ps -e`

 Si no se está ejecutando el proceso de hello, reinícielo con hello siguientes comandos:

 * Para Ubuntu: `service walinuxagent start`
 * Para otras distribuciones: `service waagent start`

3. [Configurar el agente de reinicio automático de hello](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Ejecute una nueva copia de seguridad de prueba. Si persiste el problema de hello, recopile Hola siguientes registros de VM del cliente de hello:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Si se requiere el registro detallado para waagent, siga estos pasos:

1. Hola /etc/waagent.conf, busque Hola después de línea: **habilitar el registro detallado (y | n)**
2. Hola de cambio **Logs.Verbose** valor de  *n*  demasiado*y*.
3. Guardar el cambio de Hola y reinicie waagent siguiendo los pasos anteriores de hello en esta sección.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>no se puede recuperar el estado de la instantánea de Hola o no se puede tomar una instantánea
copia de seguridad de máquina virtual de Hola se basa en la emisión de una cuenta de almacenamiento subyacente de instantánea comando toohello. Copia de seguridad puede producir un error porque no tiene ninguna cuenta de almacenamiento de toohello de acceso o porque se retrasa la ejecución Hola de tarea de instantánea de hello.

#### <a name="solution"></a>Solución
Hola condiciones siguientes puede provocar errores de tarea de instantánea:

| Causa | Solución |
| --- | --- |
| Hola VM tiene copia de seguridad de SQL Server configurada. | De forma predeterminada, copia de seguridad de máquina virtual de Hola ejecuta una copia de seguridad completa de VSS en máquinas virtuales de Windows. En las máquinas virtuales que se ejecutan en servidores basados en SQL Server y en las que se configura la copia de seguridad de SQL Server, se pueden producir retrasos en la ejecución de instantáneas.<br><br>Si experimenta un error de copia de seguridad debido a un problema de instantáneas, establezca Hola después de la clave del registro:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| Hola estado de la VM se notifica incorrectamente porque Hola VM se apaga en RDP. | Si apaga Hola VM en el protocolo de escritorio remoto (RDP), compruebe Hola portal toodetermine si Hola estado de la VM sea correcto. Si no es correcta, cerrar Hola VM en el portal de hello mediante hello **apagado** opción en el panel de la máquina virtual de Hola. |
| Muchas máquinas virtuales de hello son del mismo servicio en la nube configuraron tooback seguridad en hello mismo tiempo. | Es una mejor toospread práctica out programaciones de copia de seguridad de Hola para las máquinas virtuales de hello mismo servicio en la nube. |
| Hola máquina virtual se está ejecutando en uso elevado de CPU o memoria. | Si Hola máquina virtual se está ejecutando en el uso de la CPU (más del 90%) o el uso de memoria alta, se ponen en cola y se retrasa tarea de instantánea de hello y agota el tiempo de. Pruebe la copia de seguridad a petición en estas situaciones. |
| Hola VM no puede obtener la dirección de host/tejido Hola de DHCP. | DHCP debe estar habilitado en hello invitado para hello toowork de copia de seguridad de VM IaaS.  Si hello VM no puede obtener dirección de host/tejido Hola de respuesta DHCP 245, no se puede descargar o se ejecute cualquier extensión. Si necesita una dirección IP estática privada, debe configurarlo a través de la plataforma de Hola. Hola opción DHCP Hola se debe dejar la máquina virtual habilitada. Para más información, consulte el artículo sobre el [establecimiento de una dirección IP privada interna estática](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>se produce un error en la extensión de copia de seguridad de Hello tooupdate o carga
Si no se pueden cargar las extensiones, Backup producirá un error porque no se puede tomar una instantánea.

#### <a name="solution"></a>Solución

**Para los invitados de Windows:** Compruebe que el servicio de iaasvmprovider de hello está habilitado y tiene un tipo de inicio de *automática*. Si el servicio de hello no está configurado de esta manera, habilitar esta toodetermine si es correcta la siguiente copia de seguridad de Hola.

**Para los invitados Linux:** versión más reciente de hello compruebe de VMSnapshot para Linux (extensión de hello utilizada por copia de seguridad) es 1.0.91.0.<br>


Si extensión de copia de seguridad de hello sigue sin funcionar tooupdate o carga, puede forzar hello VMSnapshot extensión toobe a cargar, desinstale la extensión de Hola. próximo intento de copia de seguridad de Hola se volverá a cargar la extensión de Hola.

toouninstall Hola extensión, Hola siguientes:

1. Vaya toohello [portal de Azure](https://portal.azure.com/).
2. Busque Hola máquina virtual que tiene problemas de copia de seguridad.
3. Haga clic en **Configuración**.
4. Haga clic en **Extensiones**.
5. Haga clic en **Extensión de Vmsnapshot**.
6. Hacer clic en **Desinstalar**.

Este procedimiento hace Hola extensión toobe reinstalado durante la siguiente copia de seguridad de Hola.

