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
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="161e7-103">Solucionar problemas de replicación de servidores locales VMware y físicos</span><span class="sxs-lookup"><span data-stu-id="161e7-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="161e7-104">Puede recibir un mensaje de error específico al proteger sus máquinas virtuales de VMware o servidores físicos con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="161e7-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="161e7-105">Este artículo se detallan Hola encontrados, junto con tooresolve de pasos de solución de problemas de mensajes de error más comunes a algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="161e7-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="161e7-106">La replicación inicial está atascada en 0 %</span><span class="sxs-lookup"><span data-stu-id="161e7-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="161e7-107">La mayoría de los errores de replicación inicial de Hola que se encuentran en el soporte técnico son debido a problemas de tooconnectivity entre el servidor de proceso del servidor de origen o el proceso de servidor en Azure.</span><span class="sxs-lookup"><span data-stu-id="161e7-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="161e7-108">Para la mayoría de los casos, en sí mismo puede solucionar estos problemas siguiendo los pasos de hello enumerados a continuación.</span><span class="sxs-lookup"><span data-stu-id="161e7-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="161e7-109">Compruebe Hola siguiente en la máquina de origen</span><span class="sxs-lookup"><span data-stu-id="161e7-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="161e7-110">Desde la línea de comandos de la máquina de servidor de origen, utilice Telnet tooping Hola servidor de procesos con el puerto https (el valor predeterminado es 9443) tal como se muestra a continuación toosee si hay problemas de conectividad de red o problemas de bloqueo de puerto de firewall.</span><span class="sxs-lookup"><span data-stu-id="161e7-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="161e7-111">Usar Telnet, no usar la conectividad de tootest de PING.</span><span class="sxs-lookup"><span data-stu-id="161e7-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="161e7-112">Si Telnet no está instalado, siga la lista de pasos de hello [aquí](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="161e7-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="161e7-113">Si no se puede tooconnect, permitir que el puerto de entrada 9443 en el servidor de procesos de Hola y compruebe si hello problema todavía se cierra.</span><span class="sxs-lookup"><span data-stu-id="161e7-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="161e7-114">Ha habido algunos casos en los que el servidor de proceso está detrás de la DMZ y que fue la causa del problema.</span><span class="sxs-lookup"><span data-stu-id="161e7-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="161e7-115">Comprobar estado de saludo del servicio `InMage Scout VX Agent – Sentinel/OutpostStart` si no está ejecutando y compruebe si aún existe el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="161e7-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="161e7-116">Compruebe Hola siguiente en el servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="161e7-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="161e7-117">**Compruebe si el servidor de proceso activamente insertando datos tooAzure**</span><span class="sxs-lookup"><span data-stu-id="161e7-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="161e7-118">Desde el equipo de servidor de procesos, abra Hola el Administrador de tareas (presione Ctrl-Mayús-Esc).</span><span class="sxs-lookup"><span data-stu-id="161e7-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="161e7-119">Ficha de rendimiento de toohello y haga clic en el vínculo 'Abrir el Monitor de recursos'.</span><span class="sxs-lookup"><span data-stu-id="161e7-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="161e7-120">Desde el Administrador de recursos, vaya la ficha tooNetwork. Compruebe en 'Procesos con actividad de red' si cbengine.exe está enviando activamente gran volumen (en MB) de datos.</span><span class="sxs-lookup"><span data-stu-id="161e7-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Habilitar replicación](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="161e7-122">Si no siga los pasos de hello indicados a continuación:</span><span class="sxs-lookup"><span data-stu-id="161e7-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="161e7-123">**Compruebe si el servidor de procesos es capaz de tooconnect Azure Blob**: seleccione y compruebe cbengine.exe tooview hello 'Conexiones TCP' toosee si hay conectividad entre la dirección URL de blob de almacenamiento de tooAzure del servidor proceso.</span><span class="sxs-lookup"><span data-stu-id="161e7-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Habilitar replicación](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="161e7-125">Si no es así, haga clic tooControl Panel > Servicios, compruebe si Hola después servicios estén en ejecución:</span><span class="sxs-lookup"><span data-stu-id="161e7-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="161e7-126">(Re) Inicie cualquier servicio que no se está ejecutando y compruebe si el problema de hello sigue existiendo.</span><span class="sxs-lookup"><span data-stu-id="161e7-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="161e7-127">**Compruebe si el servidor de procesos es capaz de tooconnect tooAzure mediante el puerto 443 la dirección IP pública**</span><span class="sxs-lookup"><span data-stu-id="161e7-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="161e7-128">Abra Hola CBEngineCurr.errlog más reciente de `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` y busque: 443 y conexión error en el intento.</span><span class="sxs-lookup"><span data-stu-id="161e7-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Habilitar replicación](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="161e7-130">Si hay problemas, a continuación, desde la línea de comandos del servidor de procesos, usar telnet tooping su dirección IP pública de Azure (se enmascaran en por encima de la imagen) encontrado en hello CBEngineCurr.currLog mediante el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="161e7-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="161e7-131">Si es que no se puede tooconnect, a continuación, compruebe si los problemas de acceso de hello es vencimiento toofirewall o Proxy, como se describe en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="161e7-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="161e7-132">**Compruebe si firewall de basados en direcciones IP en el servidor de procesos no está bloqueando el acceso**: Si usas un reglas de firewall basado en la dirección IP en el servidor de hello, a continuación, descargue la lista completa de Hola de centro de datos de intervalos IP Microsoft Azure desde [aquí ](https://www.microsoft.com/download/details.aspx?id=41653) y agregarlas tooensure de configuración de firewall tooyour permiten comunicación tooAzure (hello y puerto HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="161e7-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="161e7-133">Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).</span><span class="sxs-lookup"><span data-stu-id="161e7-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="161e7-134">**Compruebe si firewall basado en la dirección URL en el servidor de procesos no está bloqueando el acceso**: si está usando un reglas de firewall de la dirección URL basada en servidor hello, asegúrese de hello las siguientes direcciones URL se agrega toofirewall configuración.</span><span class="sxs-lookup"><span data-stu-id="161e7-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="161e7-135">`*.accesscontrol.windows.net:` Se usa para el control de acceso y la administración de identidades</span><span class="sxs-lookup"><span data-stu-id="161e7-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="161e7-136">`*.backup.windowsazure.com:` Se usa para la transferencia y orquestación de los datos de replicación</span><span class="sxs-lookup"><span data-stu-id="161e7-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="161e7-137">`*.blob.core.windows.net:`Utilizado para acceso toohello cuenta de almacenamiento que almacena los datos replicados</span><span class="sxs-lookup"><span data-stu-id="161e7-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="161e7-138">`*.hypervrecoverymanager.windowsazure.com:` Se usa para las operaciones de administración de replicación y la orquestación</span><span class="sxs-lookup"><span data-stu-id="161e7-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="161e7-139">`time.nist.gov`y `time.windows.com`: utiliza la sincronización de hora de toocheck entre el sistema y la hora global.</span><span class="sxs-lookup"><span data-stu-id="161e7-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="161e7-140">Direcciones URL para **Azure Government Cloud**:</span><span class="sxs-lookup"><span data-stu-id="161e7-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="161e7-141">**Compruebe si la configuración del Proxy del servidor de proceso no está bloqueando el acceso**.</span><span class="sxs-lookup"><span data-stu-id="161e7-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="161e7-142">Si está utilizando un servidor Proxy, asegúrese de que está resolviendo el nombre del servidor proxy Hola por servidor DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="161e7-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="161e7-143">toocheck proporcionada en tiempo de presentación del programa de instalación de servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="161e7-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="161e7-144">Vaya tooregistry clave</span><span class="sxs-lookup"><span data-stu-id="161e7-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="161e7-145">Asegurarse de que hello en la misma configuración que se usan los datos de toosend de agente de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="161e7-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="161e7-146">Busque Microsoft Azure Backup</span><span class="sxs-lookup"><span data-stu-id="161e7-146">Search Microsoft Azure  Backup</span></span> 

![Habilitar replicación](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="161e7-148">Ábralo y haga clic en Acción > Cambiar propiedades.</span><span class="sxs-lookup"><span data-stu-id="161e7-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="161e7-149">En la ficha Configuración de Proxy, debería ver la dirección de proxy de hello, que debe ser los mismo tal y como se muestra en la configuración del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="161e7-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="161e7-150">Si no es así, cámbielo toohello misma dirección.</span><span class="sxs-lookup"><span data-stu-id="161e7-150">If not, please change it toohello same address.</span></span>

![Habilitar replicación](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="161e7-152">**Compruebe si la limitación de ancho de banda no está restringido en servidor de proceso**: aumentar el ancho de banda de Hola y compruebe si el problema de hello sigue existiendo.</span><span class="sxs-lookup"><span data-stu-id="161e7-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="161e7-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="161e7-153">Next steps</span></span>
<span data-ttu-id="161e7-154">Si necesita más ayuda, a continuación, publique la consulta demasiado[foro de ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="161e7-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="161e7-155">Tenemos una comunidad activa y uno de nuestros ingenieros será capaz de tooassist.</span><span class="sxs-lookup"><span data-stu-id="161e7-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
