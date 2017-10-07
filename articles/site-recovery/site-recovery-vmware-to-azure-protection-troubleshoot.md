---
title: "aaaTroubleshoot protección errores físicos/VMware tooAzure | Documentos de Microsoft"
description: "Este artículo describe errores de replicación en la máquina de VMware de hello comunes y cómo tootroubleshoot ellos"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Solucionar problemas de replicación de servidores locales VMware y físicos
Puede recibir un mensaje de error específico al proteger sus máquinas virtuales de VMware o servidores físicos con Azure Site Recovery. Este artículo se detallan Hola encontrados, junto con tooresolve de pasos de solución de problemas de mensajes de error más comunes a algunos de ellos.


## <a name="initial-replication-is-stuck-at-0"></a>La replicación inicial está atascada en 0 %
La mayoría de los errores de replicación inicial de Hola que se encuentran en el soporte técnico son debido a problemas de tooconnectivity entre el servidor de proceso del servidor de origen o el proceso de servidor en Azure.
Para la mayoría de los casos, en sí mismo puede solucionar estos problemas siguiendo los pasos de hello enumerados a continuación.

###<a name="check-hello-following-on-source-machine"></a>Compruebe Hola siguiente en la máquina de origen
* Desde la línea de comandos de la máquina de servidor de origen, utilice Telnet tooping Hola servidor de procesos con el puerto https (el valor predeterminado es 9443) tal como se muestra a continuación toosee si hay problemas de conectividad de red o problemas de bloqueo de puerto de firewall.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Usar Telnet, no usar la conectividad de tootest de PING.  Si Telnet no está instalado, siga la lista de pasos de hello [aquí](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Si no se puede tooconnect, permitir que el puerto de entrada 9443 en el servidor de procesos de Hola y compruebe si hello problema todavía se cierra. Ha habido algunos casos en los que el servidor de proceso está detrás de la DMZ y que fue la causa del problema.

* Comprobar estado de saludo del servicio `InMage Scout VX Agent – Sentinel/OutpostStart` si no está ejecutando y compruebe si aún existe el problema de Hola.   
 
###<a name="check-hello-following-on-process-server"></a>Compruebe Hola siguiente en el servidor de procesos

* **Compruebe si el servidor de proceso activamente insertando datos tooAzure** 

Desde el equipo de servidor de procesos, abra Hola el Administrador de tareas (presione Ctrl-Mayús-Esc). Ficha de rendimiento de toohello y haga clic en el vínculo 'Abrir el Monitor de recursos'. Desde el Administrador de recursos, vaya la ficha tooNetwork. Compruebe en 'Procesos con actividad de red' si cbengine.exe está enviando activamente gran volumen (en MB) de datos.

![Habilitar replicación](./media/site-recovery-protection-common-errors/cbengine.png)

Si no siga los pasos de hello indicados a continuación:

* **Compruebe si el servidor de procesos es capaz de tooconnect Azure Blob**: seleccione y compruebe cbengine.exe tooview hello 'Conexiones TCP' toosee si hay conectividad entre la dirección URL de blob de almacenamiento de tooAzure del servidor proceso.

![Habilitar replicación](./media/site-recovery-protection-common-errors/rmonitor.png)

Si no es así, haga clic tooControl Panel > Servicios, compruebe si Hola después servicios estén en ejecución:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Inicie cualquier servicio que no se está ejecutando y compruebe si el problema de hello sigue existiendo.

* **Compruebe si el servidor de procesos es capaz de tooconnect tooAzure mediante el puerto 443 la dirección IP pública**

Abra Hola CBEngineCurr.errlog más reciente de `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` y busque: 443 y conexión error en el intento.

![Habilitar replicación](./media/site-recovery-protection-common-errors/logdetails1.png)

Si hay problemas, a continuación, desde la línea de comandos del servidor de procesos, usar telnet tooping su dirección IP pública de Azure (se enmascaran en por encima de la imagen) encontrado en hello CBEngineCurr.currLog mediante el puerto 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Si es que no se puede tooconnect, a continuación, compruebe si los problemas de acceso de hello es vencimiento toofirewall o Proxy, como se describe en el paso siguiente.


* **Compruebe si firewall de basados en direcciones IP en el servidor de procesos no está bloqueando el acceso**: Si usas un reglas de firewall basado en la dirección IP en el servidor de hello, a continuación, descargue la lista completa de Hola de centro de datos de intervalos IP Microsoft Azure desde [aquí ](https://www.microsoft.com/download/details.aspx?id=41653) y agregarlas tooensure de configuración de firewall tooyour permiten comunicación tooAzure (hello y puerto HTTPS (443)).  Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).

* **Compruebe si firewall basado en la dirección URL en el servidor de procesos no está bloqueando el acceso**: si está usando un reglas de firewall de la dirección URL basada en servidor hello, asegúrese de hello las siguientes direcciones URL se agrega toofirewall configuración. 
     
  `*.accesscontrol.windows.net:` Se usa para el control de acceso y la administración de identidades

  `*.backup.windowsazure.com:` Se usa para la transferencia y orquestación de los datos de replicación

  `*.blob.core.windows.net:`Utilizado para acceso toohello cuenta de almacenamiento que almacena los datos replicados

  `*.hypervrecoverymanager.windowsazure.com:` Se usa para las operaciones de administración de replicación y la orquestación

  `time.nist.gov`y `time.windows.com`: utiliza la sincronización de hora de toocheck entre el sistema y la hora global.

Direcciones URL para **Azure Government Cloud**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Compruebe si la configuración del Proxy del servidor de proceso no está bloqueando el acceso**.  Si está utilizando un servidor Proxy, asegúrese de que está resolviendo el nombre del servidor proxy Hola por servidor DNS de Hola.
toocheck proporcionada en tiempo de presentación del programa de instalación de servidor de configuración. Vaya tooregistry clave

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Asegurarse de que hello en la misma configuración que se usan los datos de toosend de agente de Azure Site Recovery.
Busque Microsoft Azure Backup 

![Habilitar replicación](./media/site-recovery-protection-common-errors/mab.png)

Ábralo y haga clic en Acción > Cambiar propiedades. En la ficha Configuración de Proxy, debería ver la dirección de proxy de hello, que debe ser los mismo tal y como se muestra en la configuración del registro de hello. Si no es así, cámbielo toohello misma dirección.

![Habilitar replicación](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Compruebe si la limitación de ancho de banda no está restringido en servidor de proceso**: aumentar el ancho de banda de Hola y compruebe si el problema de hello sigue existiendo.

##<a name="next-steps"></a>Pasos siguientes
Si necesita más ayuda, a continuación, publique la consulta demasiado[foro de ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). Tenemos una comunidad activa y uno de nuestros ingenieros será capaz de tooassist.
