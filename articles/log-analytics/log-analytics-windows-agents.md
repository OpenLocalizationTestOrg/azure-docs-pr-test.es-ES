---
title: "aaaConnect Windows equipos tooAzure análisis de registros | Documentos de Microsoft"
description: "Este artículo muestra los equipos con Windows hello pasos tooconnect hello en su toohello de infraestructura local servicio de análisis de registros mediante el uso de una versión personalizada de hello Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="bb973-103">Conecta el servicio de análisis de registros de toohello de equipos de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="bb973-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="bb973-104">Este artículo muestra los pasos de hello tooconnect equipos de Windows en las áreas de trabajo de tooOMS de infraestructura local mediante el uso de una versión personalizada de hello Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="bb973-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="bb973-105">Es necesario tooinstall y conectar a agentes para todos los equipos de Hola que desea tooonboard en orden para ellos el servicio de análisis de registros de toosend datos toohello y tooview y actuar en los datos.</span><span class="sxs-lookup"><span data-stu-id="bb973-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="bb973-106">Cada agente puede informar toomultiple áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb973-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="bb973-107">Puede instalar los agentes a través del programa de instalación, a través de la línea de comandos o utilizando Configuración de estado deseado (DSC) en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb973-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="bb973-108">Para máquinas virtuales que se ejecutan en Azure, puede simplificar la instalación utilizando hello [extensión de máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bb973-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="bb973-109">En los equipos con conectividad a Internet, el agente de hello usa Hola conexión toohello Internet toosend datos tooOMS.</span><span class="sxs-lookup"><span data-stu-id="bb973-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="bb973-110">Para equipos que no tiene conectividad a Internet, puede usar un servidor proxy o hello [puerta de enlace de OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="bb973-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="bb973-111">Conectar su tooOMS de equipos de Windows es sencillo con tres sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="bb973-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="bb973-112">Descargar el archivo de instalación de agente de Hola Hola portal de OMS</span><span class="sxs-lookup"><span data-stu-id="bb973-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="bb973-113">Instalar a agente de hello mediante el método de Hola que elija</span><span class="sxs-lookup"><span data-stu-id="bb973-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="bb973-114">Configurar el agente de Hola o agregar áreas de trabajo adicionales, si es necesario</span><span class="sxs-lookup"><span data-stu-id="bb973-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="bb973-115">Hello siguiente diagrama muestra hello relación entre los equipos de Windows y OMS después de que haya instalado y configurado los agentes.</span><span class="sxs-lookup"><span data-stu-id="bb973-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="bb973-117">Si las directivas de seguridad de TI no permitir que los equipos en su toohello de tooconnect de la red Internet, puede configurar su toohello de tooconnect equipos puerta de enlace de OMS.</span><span class="sxs-lookup"><span data-stu-id="bb973-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="bb973-118">Para obtener más información y pasos acerca de cómo tooconfigure su toocommunicate de servidores a través de un servicio de OMS toohello de puerta de enlace de OMS, consulte [conectar tooOMS de equipos con hello puerta de enlace de OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="bb973-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="bb973-119">Requisitos del sistema y configuración necesaria</span><span class="sxs-lookup"><span data-stu-id="bb973-119">System requirements and required configuration</span></span>
<span data-ttu-id="bb973-120">Antes de instalar o implementar a agentes, revise Hola después tooensure detalles cumple los requisitos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb973-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="bb973-121">Hola OMS MMA solo se puede instalar en equipos que ejecutan Windows Server 2008 SP 1 o posterior o Windows 7 SP1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="bb973-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="bb973-122">Necesita una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb973-122">You need an Azure subscription.</span></span>  <span data-ttu-id="bb973-123">Para más información, consulte [Introducción a Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb973-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="bb973-124">Cada equipo de Windows debe ser capaz de tooconnect toohello Internet mediante HTTPS o toohello puerta de enlace de OMS.</span><span class="sxs-lookup"><span data-stu-id="bb973-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="bb973-125">Esta conexión puede ser directa a través de un proxy, o a través de hello puerta de enlace de OMS.</span><span class="sxs-lookup"><span data-stu-id="bb973-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="bb973-126">Puede instalar Hola OMS MMA en equipos independientes, servidores y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bb973-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="bb973-127">Si desea tooconnect tooOMS de máquinas virtuales hospedadas en Azure, consulte [tooLog de máquinas virtuales de Azure conectarse análisis](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bb973-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="bb973-128">agente de Hello debe toouse el puerto TCP 443 de distintos recursos.</span><span class="sxs-lookup"><span data-stu-id="bb973-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="bb973-129">Red</span><span class="sxs-lookup"><span data-stu-id="bb973-129">Network</span></span>

<span data-ttu-id="bb973-130">Para Windows agentes tooconnect tooand caja registradora con servicio OMS hello, deben tener acceso a los recursos toonetwork, incluidos los números de puerto de Hola y direcciones URL de dominio.</span><span class="sxs-lookup"><span data-stu-id="bb973-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="bb973-131">Para los servidores proxy, debe tooensure que Hola recursos se configuran en la configuración del agente de servidor de proxy correspondiente.</span><span class="sxs-lookup"><span data-stu-id="bb973-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="bb973-132">Para los firewalls que restringen el acceso toohello Internet, se o los ingenieros de red necesitan tooconfigure su tooOMS de acceso de firewall toopermit.</span><span class="sxs-lookup"><span data-stu-id="bb973-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="bb973-133">No es necesario realizar ninguna acción en la configuración del agente.</span><span class="sxs-lookup"><span data-stu-id="bb973-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="bb973-134">Hello en la tabla siguiente muestra los recursos necesarios para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="bb973-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="bb973-135">Algunos de hello recursos siguientes mencionan a visión operativa, lo que era un nombre para el análisis de registros anterior.</span><span class="sxs-lookup"><span data-stu-id="bb973-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="bb973-136">Recurso del agente</span><span class="sxs-lookup"><span data-stu-id="bb973-136">Agent Resource</span></span> | <span data-ttu-id="bb973-137">Puertos</span><span class="sxs-lookup"><span data-stu-id="bb973-137">Ports</span></span> | <span data-ttu-id="bb973-138">Omitir inspección de HTTPS</span><span class="sxs-lookup"><span data-stu-id="bb973-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="bb973-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bb973-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="bb973-140">443</span><span class="sxs-lookup"><span data-stu-id="bb973-140">443</span></span> | <span data-ttu-id="bb973-141">Sí</span><span class="sxs-lookup"><span data-stu-id="bb973-141">Yes</span></span> |
| <span data-ttu-id="bb973-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="bb973-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="bb973-143">443</span><span class="sxs-lookup"><span data-stu-id="bb973-143">443</span></span> | <span data-ttu-id="bb973-144">Sí</span><span class="sxs-lookup"><span data-stu-id="bb973-144">Yes</span></span> |
| <span data-ttu-id="bb973-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="bb973-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="bb973-146">443</span><span class="sxs-lookup"><span data-stu-id="bb973-146">443</span></span> | <span data-ttu-id="bb973-147">Sí</span><span class="sxs-lookup"><span data-stu-id="bb973-147">Yes</span></span> |
| <span data-ttu-id="bb973-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="bb973-148">*.azure-automation.net</span></span> | <span data-ttu-id="bb973-149">443</span><span class="sxs-lookup"><span data-stu-id="bb973-149">443</span></span> | <span data-ttu-id="bb973-150">Sí</span><span class="sxs-lookup"><span data-stu-id="bb973-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="bb973-151">Descargar el archivo de instalación de agente de Hola de OMS</span><span class="sxs-lookup"><span data-stu-id="bb973-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="bb973-152">Portal de OMS de hello, en hello **Introducción** página, haga clic en hello **configuración** icono.</span><span class="sxs-lookup"><span data-stu-id="bb973-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="bb973-153">Haga clic en hello **orígenes conectados** ficha situada en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb973-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="bb973-154">![Pestaña Connected Sources (Orígenes conectados)](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="bb973-155">Haga clic en **servidores Windows** y, a continuación, haga clic en **Download Windows Agent** archivo de tooyour aplicables equipo procesador tipo toodownload hello el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="bb973-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="bb973-156">En hello derecha de **Id. de área de trabajo**, haga clic en el icono de copiar de Hola y pegue el identificador hello en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="bb973-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="bb973-157">En hello derecha de **Primary Key**, haga clic en el icono de copiar de Hola y pegue la clave de hello en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="bb973-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="bb973-158">Instalación de agentes de hello mediante el programa de instalación</span><span class="sxs-lookup"><span data-stu-id="bb973-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="bb973-159">Ejecutar agente de hello tooinstall el programa de instalación en un equipo que desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="bb973-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="bb973-160">En la página de bienvenida de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb973-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="bb973-161">En la página términos de licencia de hello, lea el contrato de licencia de hello y, a continuación, haga clic en **acepto**.</span><span class="sxs-lookup"><span data-stu-id="bb973-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="bb973-162">En la página de la carpeta de destino de hello, cambiar o mantener la carpeta de instalación predeterminada de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb973-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="bb973-163">En la página de opciones de instalación del agente de hello, puede elegir tooconnect Hola agente tooAzure Log Analytics (OMS), Operations Manager, o puede dejar que las opciones de hello en blanco si desea que tooconfigure Hola agente más tarde.</span><span class="sxs-lookup"><span data-stu-id="bb973-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="bb973-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb973-164">Click **Next**.</span></span>   
    - <span data-ttu-id="bb973-165">Si ha elegido tooconnect tooAzure Log Analytics (OMS), pegue hello **Id. de área de trabajo** y **clave de área de trabajo (clave principal)** que ha copiado en el Bloc de notas en el procedimiento anterior de hello y, a continuación, haga clic en  **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb973-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="bb973-166">![pegar identificador del área de trabajo y clave principal](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="bb973-167">Si ha elegido tooconnect tooOperations Manager, escriba Hola **nombre del grupo de administración**, **Management Server** nombre, y **puerto del servidor de administración**y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb973-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="bb973-168">En la página de la cuenta de acción del agente de hello, elija la cuenta de sistema Local de Hola o una cuenta de dominio local y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bb973-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="bb973-169">![configuración del grupo de administración](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="bb973-170">En la página Listo tooInstall hello, revise las selecciones realizadas y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="bb973-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="bb973-171">En hello completó correctamente la configuración de página, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="bb973-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="bb973-172">Cuando haya finalizado, Hola **Microsoft Monitoring Agent** aparece en **el Panel de Control**.</span><span class="sxs-lookup"><span data-stu-id="bb973-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="bb973-173">Puede revisar la configuración no existe y comprobar que el agente Hola esté conectado tooOperational visión (OMS).</span><span class="sxs-lookup"><span data-stu-id="bb973-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="bb973-174">Cuando tooOMS conectados, Hola agente muestra un mensaje que indica: **Hola Microsoft Monitoring Agent se ha conectado correctamente toohello servicio de Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="bb973-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="bb973-175">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="bb973-175">Configure proxy settings</span></span>

<span data-ttu-id="bb973-176">Puede usar Hola después de la configuración de proxy de procedimiento tooconfigure de hello Microsoft Monitoring Agent mediante el Panel de Control.</span><span class="sxs-lookup"><span data-stu-id="bb973-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="bb973-177">Necesita toouse este procedimiento para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="bb973-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="bb973-178">Si tiene muchos servidores que necesite tooconfigure, le resultará más fácil toouse una secuencia de comandos tooautomate este proceso.</span><span class="sxs-lookup"><span data-stu-id="bb973-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="bb973-179">Si es así, vea el procedimiento siguiente hello [tooconfigure configuración de proxy para Microsoft Monitoring Agent mediante un script de Hola](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="bb973-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="bb973-180">configuración de proxy de tooconfigure de hello Microsoft Monitoring Agent mediante el Panel de Control</span><span class="sxs-lookup"><span data-stu-id="bb973-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="bb973-181">Abra el **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="bb973-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="bb973-182">Abra **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="bb973-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="bb973-183">Haga clic en hello **configuración de Proxy** ficha.</span><span class="sxs-lookup"><span data-stu-id="bb973-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="bb973-184">![Pestaña Configuración de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="bb973-185">Seleccione **utilizar un servidor proxy** y escriba la dirección URL de Hola y número de puerto, si hay alguna toohello necesario, de forma similar en el ejemplo se muestran.</span><span class="sxs-lookup"><span data-stu-id="bb973-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="bb973-186">Si el servidor proxy requiere autenticación, escriba Hola username y password tooaccess Hola servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="bb973-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="bb973-187">Compruebe tooOMS de conectividad del agente</span><span class="sxs-lookup"><span data-stu-id="bb973-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="bb973-188">Puede comprobar fácilmente si los agentes se comunican con OMS mediante Hola siguiendo el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="bb973-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="bb973-189">En el equipo de hello con el agente de Windows hello, abra el Panel de Control.</span><span class="sxs-lookup"><span data-stu-id="bb973-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="bb973-190">Abra Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="bb973-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="bb973-191">Haga clic en la pestaña de hello Azure Log Analytics (OMS).</span><span class="sxs-lookup"><span data-stu-id="bb973-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="bb973-192">En la columna de estado de hello, debería ver que ese agente Hola conectado correctamente el servicio de Operations Management Suite toohello.</span><span class="sxs-lookup"><span data-stu-id="bb973-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![agente conectado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="bb973-194">configuración de proxy de tooconfigure para Microsoft Monitoring Agent mediante un script de Hola</span><span class="sxs-lookup"><span data-stu-id="bb973-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="bb973-195">Copie Hola siguiente ejemplo, actualícelo con el entorno de tooyour específico de información, guárdelo con una extensión de nombre de archivo PS1 y, a continuación, ejecute el script de Hola en cada equipo que se conecta directamente a servicio OMS toohello.</span><span class="sxs-lookup"><span data-stu-id="bb973-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="bb973-196">Instalar a agente de hello mediante la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="bb973-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="bb973-197">Modificar y, a continuación, usar hello siguiente a agente de hello tooinstall de ejemplo mediante la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb973-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="bb973-198">ejemplo de Hola realiza una instalación completamente silenciosa.</span><span class="sxs-lookup"><span data-stu-id="bb973-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="bb973-199">Si desea tooupgrade un agente, debe toouse Hola análisis de registros de API de scripting.</span><span class="sxs-lookup"><span data-stu-id="bb973-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="bb973-200">Vea Hola siguiente sección tooupgrade un agente.</span><span class="sxs-lookup"><span data-stu-id="bb973-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="bb973-201">agente de Hello utiliza IExpress como su Self-extractor con hello `/c` comando.</span><span class="sxs-lookup"><span data-stu-id="bb973-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="bb973-202">Puede ver los modificadores de línea de comandos de hello en [modificadores de línea de comandos para IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) y, a continuación, actualización Hola toosuit de ejemplo a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="bb973-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="bb973-203">Opciones específicas de MMA</span><span class="sxs-lookup"><span data-stu-id="bb973-203">MMA-specific options</span></span>                   |<span data-ttu-id="bb973-204">Notas</span><span class="sxs-lookup"><span data-stu-id="bb973-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="bb973-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="bb973-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="bb973-206">1 = el área de trabajo de configurar Hola agente tooreport tooa</span><span class="sxs-lookup"><span data-stu-id="bb973-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="bb973-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="bb973-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="bb973-208">Id. de área de trabajo (guid) para hello tooadd de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="bb973-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="bb973-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="bb973-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="bb973-210">Tooinitially de uso clave de área de trabajo se autentican con el área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="bb973-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="bb973-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="bb973-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="bb973-212">Especificar el entorno de nube de Hola donde se encuentra el área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="bb973-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="bb973-213">0 = nube comercial de Azure (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="bb973-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="bb973-214">1= Azure Government</span><span class="sxs-lookup"><span data-stu-id="bb973-214">1 = Azure Government</span></span> |
|<span data-ttu-id="bb973-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="bb973-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="bb973-216">URI de hello proxy toouse</span><span class="sxs-lookup"><span data-stu-id="bb973-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="bb973-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="bb973-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="bb973-218">Nombre de usuario tooaccess un proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="bb973-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="bb973-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="bb973-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="bb973-220">Contraseña tooaccess un proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="bb973-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="bb973-221">límite de longitud de línea de comandos de hello posicionamiento de tooavoid de IExpress, instalar agente Hola con ningún área de trabajo configurado y, a continuación, utilizar una configuración de tooset de secuencia de comandos para el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb973-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="bb973-222">Si se produce un `Command line option syntax error.` al usar hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parámetro, puede usar Hola siguiente solución alternativa:</span><span class="sxs-lookup"><span data-stu-id="bb973-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="bb973-223">Incorporación de un área de trabajo mediante un script</span><span class="sxs-lookup"><span data-stu-id="bb973-223">Add a workspace using a script</span></span>
<span data-ttu-id="bb973-224">Agregar un área de trabajo con API de scripting del agente de análisis de registros de Hola Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb973-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="bb973-225">tooadd un área de trabajo en Azure para el gobierno de Estados Unidos, Hola de uso después de ejemplo de secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="bb973-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="bb973-226">Si ha usado la línea de comandos de Hola o script previamente tooinstall o configurar el agente de hello, `EnableAzureOperationalInsights` ha sido reemplazado por `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="bb973-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="bb973-227">Instalar a agente de hello con DSC en automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="bb973-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="bb973-228">Puede usar Hola sigue la secuencia de comandos en el ejemplo se tooinstall Hola agente con DSC en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb973-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="bb973-229">ejemplo de Hola instala Hola agente de 64 bits, identificado por hello `URI` valor.</span><span class="sxs-lookup"><span data-stu-id="bb973-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="bb973-230">También puede utilizar la versión de 32 bits de hello reemplazando el valor del URI Hola.</span><span class="sxs-lookup"><span data-stu-id="bb973-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="bb973-231">Hola URI para ambas versiones son:</span><span class="sxs-lookup"><span data-stu-id="bb973-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="bb973-232">Agente de Windows de 64 bits: https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="bb973-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="bb973-233">Agente de Windows de 32 bits: https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="bb973-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="bb973-234">Este ejemplo de script y procedimiento no actualizará un agente existente.</span><span class="sxs-lookup"><span data-stu-id="bb973-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="bb973-235">Importar hello xPSDesiredStateConfiguration módulo de DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb973-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="bb973-236">En Azure Automation, cree los recursos de variable *OPSINSIGHTS_WS_ID* y *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="bb973-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="bb973-237">Establecer *OPSINSIGHTS_WS_ID* Id. de área de trabajo de análisis de registros de OMS tooyour y establecer *OPSINSIGHTS_WS_KEY* toohello clave principal del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb973-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="bb973-238">Usar hello siguiente script y guárdelo como MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="bb973-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="bb973-239">Modificar y, a continuación, usar hello siguiente a agente de Hola de tooinstall de ejemplo con DSC en automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb973-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="bb973-240">Importar MMAgent.ps1 en automatización de Azure mediante la interfaz de automatización de Azure de Hola o el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb973-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="bb973-241">Asignar una configuración de toohello de nodo.</span><span class="sxs-lookup"><span data-stu-id="bb973-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="bb973-242">Dentro de 15 minutos, nodo de hello comprueba su configuración y Hola MMA se inserta el nodo toohello.</span><span class="sxs-lookup"><span data-stu-id="bb973-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="bb973-243">Obtener el valor de ProductId más reciente de Hola</span><span class="sxs-lookup"><span data-stu-id="bb973-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="bb973-244">Hola `ProductId value` en hello MMAgent.ps1 script es la versión del agente tooeach único.</span><span class="sxs-lookup"><span data-stu-id="bb973-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="bb973-245">Cuando se publica una versión actualizada de cada agente, Hola ProductId valor cambia.</span><span class="sxs-lookup"><span data-stu-id="bb973-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="bb973-246">Por lo tanto, cuando Hola ProductId cambia de hello futuro, puede averiguar la versión de agente de hello mediante un script sencillo.</span><span class="sxs-lookup"><span data-stu-id="bb973-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="bb973-247">Una vez que la última versión del agente Hola instalado en un servidor de prueba, puede usar Hola siguiente valor de ProductId de secuencia de comandos tooget Hola instalado.</span><span class="sxs-lookup"><span data-stu-id="bb973-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="bb973-248">Con el último valor de ProductId hello, puede actualizar el valor de Hola Hola MMAgent.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="bb973-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="bb973-249">Configuración de un agente de forma manual o incorporación de áreas de trabajo adicionales</span><span class="sxs-lookup"><span data-stu-id="bb973-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="bb973-250">Si instaló a agentes pero no los ha configurado o si desea que las áreas de trabajo de hello agente tooreport toomultiple, puede usar Hola después información tooenable un agente o volver a configurarlo.</span><span class="sxs-lookup"><span data-stu-id="bb973-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="bb973-251">Después de configurar al agente de hello, se registrará con el servicio del agente de Hola y le proporcionará información de configuración necesaria y módulos de administración que contienen información de la solución.</span><span class="sxs-lookup"><span data-stu-id="bb973-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="bb973-252">Después de instalar Microsoft Monitoring Agent hello, abra **el Panel de Control**.</span><span class="sxs-lookup"><span data-stu-id="bb973-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="bb973-253">Abra **Microsoft Monitoring Agent** y, a continuación, haga clic en hello **Azure Log Analytics (OMS)** ficha.</span><span class="sxs-lookup"><span data-stu-id="bb973-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="bb973-254">Haga clic en **agregar** tooopen hello **agregar un área de trabajo de análisis de registro** cuadro.</span><span class="sxs-lookup"><span data-stu-id="bb973-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="bb973-255">Hola pegar **Id. de área de trabajo** y **clave de área de trabajo (clave principal)** que ha copiado en el Bloc de notas en un procedimiento anterior para el área de trabajo de Hola que desee tooadd y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bb973-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="bb973-256">![configurar Visión operativa](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="bb973-257">Después de recopilar datos de los equipos supervisados por el agente de hello, número de Hola de equipos supervisados por OMS aparecerá en el portal de OMS de hello en hello **orígenes conectados** ficha **configuración** como  **Servidores conectados**.</span><span class="sxs-lookup"><span data-stu-id="bb973-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="bb973-258">toodisable un agente</span><span class="sxs-lookup"><span data-stu-id="bb973-258">toodisable an agent</span></span>
1. <span data-ttu-id="bb973-259">Después de instalar el agente de hello, abra **el Panel de Control**.</span><span class="sxs-lookup"><span data-stu-id="bb973-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="bb973-260">Abra el agente de supervisión de Microsoft y, a continuación, haga clic en hello **Azure Log Analytics (OMS)** ficha.</span><span class="sxs-lookup"><span data-stu-id="bb973-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="bb973-261">Seleccione un área de trabajo y haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="bb973-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="bb973-262">Repita este paso para el resto de áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb973-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="bb973-263">Opcionalmente, configure el grupo de administración de agentes tooreport tooan Operations Manager</span><span class="sxs-lookup"><span data-stu-id="bb973-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="bb973-264">Si usa Operations Manager en su infraestructura de TI, también puede utilizar el agente MMA Hola como un agente de Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="bb973-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="bb973-265">grupo de administración de Operations Manager de tooconfigure MMA agentes tooreport tooan</span><span class="sxs-lookup"><span data-stu-id="bb973-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="bb973-266">En el equipo de Hola donde está instalado el agente de hello, abra **el Panel de Control**.</span><span class="sxs-lookup"><span data-stu-id="bb973-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="bb973-267">Abra **Microsoft Monitoring Agent** y, a continuación, haga clic en hello **Operations Manager** ficha.</span><span class="sxs-lookup"><span data-stu-id="bb973-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="bb973-268">![Pestaña Operations Manager de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="bb973-269">Si los servidores de Operations Manager tienen integración con Active Directory, haga clic en **Actualizar automáticamente asignaciones de grupos de administración desde AD DS**.</span><span class="sxs-lookup"><span data-stu-id="bb973-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="bb973-270">Haga clic en **agregar** tooopen hello **agregar un grupo de administración** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb973-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="bb973-271">![Agregar un grupo de administración de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="bb973-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="bb973-272">En **nombre del grupo de administración** cuadro, escriba un nombre Hola de su grupo de administración.</span><span class="sxs-lookup"><span data-stu-id="bb973-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="bb973-273">Hola **servidor de administración principal** cuadro, escribe el nombre del equipo de Hola Hola principal del servidor de administración.</span><span class="sxs-lookup"><span data-stu-id="bb973-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="bb973-274">Hola **puerto del servidor de administración** cuadro de número de puerto TCP de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="bb973-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="bb973-275">En **cuenta de acción del agente**, elija la cuenta de sistema Local de Hola o una cuenta de dominio local.</span><span class="sxs-lookup"><span data-stu-id="bb973-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="bb973-276">Haga clic en **Aceptar** tooclose hello **agregar un grupo de administración** cuadro de diálogo y, a continuación, haga clic en **Aceptar** tooclose hello **propiedades de agente de supervisión de Microsoft**cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bb973-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bb973-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb973-277">Next steps</span></span>

- <span data-ttu-id="bb973-278">[Adición de soluciones de análisis de registros desde la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad y recopilar datos.</span><span class="sxs-lookup"><span data-stu-id="bb973-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
