---
title: "Conexión de equipos Windows a Azure Log Analytics | Microsoft Docs"
description: "En este artículo, se explican los pasos necesarios para conectar los equipos Windows de la infraestructura local directamente al servicio Log Analytics a través de una versión personalizada de Microsoft Monitoring Agent (MMA)."
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="a08d7-103">Conexión de equipos Windows al servicio Log Analytics de Azure</span><span class="sxs-lookup"><span data-stu-id="a08d7-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="a08d7-104">En este artículo, se explican los pasos necesarios para conectar los equipos Windows de la infraestructura local a áreas de trabajo de OMS a través de una versión personalizada de Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="a08d7-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="a08d7-105">Deberá instalar y conectar agentes en todos los equipos que quiera incorporar para que puedan enviar datos al servicio Log Analytics, así como ver esos datos y actuar sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="a08d7-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="a08d7-106">Cada agente puede informar a varias áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a08d7-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="a08d7-107">Puede instalar los agentes a través del programa de instalación, a través de la línea de comandos o utilizando Configuración de estado deseado (DSC) en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a08d7-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="a08d7-108">Para las máquinas virtuales que se ejecutan en Azure, puede simplificar la instalación con la [extensión de máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a08d7-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="a08d7-109">En los equipos que tengan conectividad a Internet, el agente usa esta conexión para enviar datos a OMS.</span><span class="sxs-lookup"><span data-stu-id="a08d7-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="a08d7-110">En los equipos que no tengan conectividad a Internet, puede usar un proxy o la [puerta de enlace de OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a08d7-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="a08d7-111">Para conectar equipos Windows a OMS, solo se necesitan tres sencillos pasos:</span><span class="sxs-lookup"><span data-stu-id="a08d7-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="a08d7-112">Descargar el archivo del programa de instalación del agente desde el portal de OMS</span><span class="sxs-lookup"><span data-stu-id="a08d7-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="a08d7-113">Instalación del agente a través del método elegido</span><span class="sxs-lookup"><span data-stu-id="a08d7-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="a08d7-114">Configuración del agente o incorporación de áreas de trabajo adicionales, si es necesario</span><span class="sxs-lookup"><span data-stu-id="a08d7-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="a08d7-115">En el siguiente diagrama se muestra la relación entre los equipos Windows y OMS después de instalar y configurar los agentes.</span><span class="sxs-lookup"><span data-stu-id="a08d7-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="a08d7-117">Si las directivas de seguridad de TI no permiten que los equipos de la red se conecten a Internet, puede configurarlos para que se conecten a la puerta de enlace de OMS.</span><span class="sxs-lookup"><span data-stu-id="a08d7-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="a08d7-118">Para obtener más información y pasos sobre cómo configurar los servidores para que se comuniquen por una puerta de enlace de OMS con el servicio OMS, consulte [Conexión de equipos sin acceso a OMS mediante la puerta de enlace de OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a08d7-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="a08d7-119">Requisitos del sistema y configuración necesaria</span><span class="sxs-lookup"><span data-stu-id="a08d7-119">System requirements and required configuration</span></span>
<span data-ttu-id="a08d7-120">Antes de instalar o implementar agentes, consulte la siguiente información para asegurarse de que cumple los requisitos.</span><span class="sxs-lookup"><span data-stu-id="a08d7-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="a08d7-121">MMA de OMS solo puede instalarse en equipos con Windows Server 2008 SP 1 o versiones posteriores y en equipos con Windows 7 SP1 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="a08d7-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="a08d7-122">Necesita una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a08d7-122">You need an Azure subscription.</span></span>  <span data-ttu-id="a08d7-123">Para más información, consulte [Introducción a Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a08d7-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="a08d7-124">Todos los equipos Windows necesitan tener conexión a Internet con HTTPS o la puerta de enlace de OMS.</span><span class="sxs-lookup"><span data-stu-id="a08d7-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="a08d7-125">Esta conexión puede ser directa, a través de un proxy o a través de la puerta de enlace de OMS.</span><span class="sxs-lookup"><span data-stu-id="a08d7-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="a08d7-126">Puede instalar MMA de OMS en equipos independientes, servidores y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a08d7-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="a08d7-127">Si quiere conectar a OMS máquinas virtuales hospedadas en Azure, consulte [Connect Azure storage to Log Analytics](log-analytics-azure-vm-extension.md)(Conectar Azure Storage a Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="a08d7-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="a08d7-128">El agente debe usar el puerto TCP 443 para diversos recursos.</span><span class="sxs-lookup"><span data-stu-id="a08d7-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="a08d7-129">Red</span><span class="sxs-lookup"><span data-stu-id="a08d7-129">Network</span></span>

<span data-ttu-id="a08d7-130">Para que los agentes de Windows se conecten y se registren con el servicio OMS, deben tener acceso a los recursos de red, incluidos los números de puerto y las direcciones URL de dominio.</span><span class="sxs-lookup"><span data-stu-id="a08d7-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="a08d7-131">Para los servidores proxy, debe asegurarse de que los recursos de servidor proxy adecuados están configurados en la configuración del agente.</span><span class="sxs-lookup"><span data-stu-id="a08d7-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="a08d7-132">Para firewalls que restringen el acceso a Internet, usted o el ingeniero de redes deberán configurarlo para que permita el acceso a OMS.</span><span class="sxs-lookup"><span data-stu-id="a08d7-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="a08d7-133">No es necesario realizar ninguna acción en la configuración del agente.</span><span class="sxs-lookup"><span data-stu-id="a08d7-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="a08d7-134">En la siguiente tabla se muestran los recursos necesarios para la comunicación.</span><span class="sxs-lookup"><span data-stu-id="a08d7-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="a08d7-135">Algunos de los siguientes recursos mencionan Operational Insights, que era el nombre anterior de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a08d7-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="a08d7-136">Recurso del agente</span><span class="sxs-lookup"><span data-stu-id="a08d7-136">Agent Resource</span></span> | <span data-ttu-id="a08d7-137">Puertos</span><span class="sxs-lookup"><span data-stu-id="a08d7-137">Ports</span></span> | <span data-ttu-id="a08d7-138">Omitir inspección de HTTPS</span><span class="sxs-lookup"><span data-stu-id="a08d7-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="a08d7-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="a08d7-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="a08d7-140">443</span><span class="sxs-lookup"><span data-stu-id="a08d7-140">443</span></span> | <span data-ttu-id="a08d7-141">Sí</span><span class="sxs-lookup"><span data-stu-id="a08d7-141">Yes</span></span> |
| <span data-ttu-id="a08d7-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="a08d7-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="a08d7-143">443</span><span class="sxs-lookup"><span data-stu-id="a08d7-143">443</span></span> | <span data-ttu-id="a08d7-144">Sí</span><span class="sxs-lookup"><span data-stu-id="a08d7-144">Yes</span></span> |
| <span data-ttu-id="a08d7-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="a08d7-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="a08d7-146">443</span><span class="sxs-lookup"><span data-stu-id="a08d7-146">443</span></span> | <span data-ttu-id="a08d7-147">Sí</span><span class="sxs-lookup"><span data-stu-id="a08d7-147">Yes</span></span> |
| <span data-ttu-id="a08d7-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="a08d7-148">*.azure-automation.net</span></span> | <span data-ttu-id="a08d7-149">443</span><span class="sxs-lookup"><span data-stu-id="a08d7-149">443</span></span> | <span data-ttu-id="a08d7-150">Sí</span><span class="sxs-lookup"><span data-stu-id="a08d7-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="a08d7-151">Descarga del archivo de instalación del agente desde OMS</span><span class="sxs-lookup"><span data-stu-id="a08d7-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="a08d7-152">En el portal de OMS, en la página **Overview** (Información general), haga clic en el icono **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="a08d7-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="a08d7-153">Haga clic en la pestaña **Orígenes conectados** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="a08d7-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="a08d7-154">![Pestaña Connected Sources (Orígenes conectados)](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="a08d7-155">Haga clic en **Servidores de Windows** y, después, haga clic en **Descargar el agente de Windows** (según el tipo de procesador del equipo) para descargar el archivo del programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="a08d7-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="a08d7-156">A la derecha de **Id. del área de trabajo**, haga clic en el icono Copiar y pegue el id. en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="a08d7-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="a08d7-157">A la derecha de **Clave principal**, haga clic en el icono Copiar y pegue la clave en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="a08d7-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="a08d7-158">Instalación del agente con el programa de instalación</span><span class="sxs-lookup"><span data-stu-id="a08d7-158">Install the agent using setup</span></span>
1. <span data-ttu-id="a08d7-159">Ejecute la configuración para instalar el agente en un equipo que desee administrar.</span><span class="sxs-lookup"><span data-stu-id="a08d7-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="a08d7-160">En la página de bienvenida, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="a08d7-161">En la página Términos de licencia, lea la licencia y haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="a08d7-162">En la página Carpeta de destino, cambie o mantenga la carpeta de instalación predeterminada y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="a08d7-163">En la página Opciones de instalación del agente, puede conectar el agente a Azure Log Analytics (OMS), Operations Manager. También puede dejar las opciones en blanco si prefiere configurar al agente más tarde.</span><span class="sxs-lookup"><span data-stu-id="a08d7-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="a08d7-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-164">Click **Next**.</span></span>   
    - <span data-ttu-id="a08d7-165">Si decide conectar el agente a Azure Log Analytics (OMS), pegue el **identificador del área de trabajo** y la **clave del área de trabajo (clave principal)** que copió en el Bloc de notas durante el procedimiento anterior y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="a08d7-166">![pegar identificador del área de trabajo y clave principal](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="a08d7-167">Si decide conectar el agente a Operations Manager, especifique el **nombre del grupo de administración**, el nombre del **servidor de administración** y el **puerto del servidor de administración**; después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="a08d7-168">En la página Cuenta de acción del agente, seleccione la cuenta de sistema local o una cuenta de dominio local y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="a08d7-169">![configuración del grupo de administración](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="a08d7-170">En la página Preparado para instalar, revise las opciones seleccionadas y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="a08d7-171">En la página La configuración finalizó correctamente, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="a08d7-172">Una vez completado el proceso, el **Agente de administración de Microsoft** aparece en el **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="a08d7-173">Allí puede revisar la configuración y comprobar que el agente esté conectado a Visión operativa (OMS).</span><span class="sxs-lookup"><span data-stu-id="a08d7-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="a08d7-174">Cuando se conecta a OMS, el agente muestra un mensaje similar al siguiente: **Microsoft Monitoring Agent se conectó correctamente al servicio Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="a08d7-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="a08d7-175">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="a08d7-175">Configure proxy settings</span></span>

<span data-ttu-id="a08d7-176">Puede utilizar el procedimiento siguiente para configurar el proxy para Microsoft Monitoring Agent mediante el Panel de Control.</span><span class="sxs-lookup"><span data-stu-id="a08d7-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="a08d7-177">Deberá usar este procedimiento para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="a08d7-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="a08d7-178">Si tiene muchos servidores que necesite configurar, le resultará más fácil usar un script para automatizar este proceso.</span><span class="sxs-lookup"><span data-stu-id="a08d7-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="a08d7-179">Puede utilizar el procedimiento siguiente para [configurar el proxy para Microsoft Monitoring Agent mediante el Panel de Control](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="a08d7-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="a08d7-180">Para configurar el proxy para Microsoft Monitoring Agent mediante el Panel de control</span><span class="sxs-lookup"><span data-stu-id="a08d7-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="a08d7-181">Abra el **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="a08d7-182">Abra **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="a08d7-183">Haga clic en la pestaña **Configuración de proxy**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="a08d7-184">![Pestaña Configuración de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="a08d7-185">Seleccione **Usar un servidor proxy** y escriba la dirección URL y el número de puerto, si uno es necesario, de forma similar al ejemplo mostrado.</span><span class="sxs-lookup"><span data-stu-id="a08d7-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="a08d7-186">Si el servidor proxy requiere autenticación, escriba el nombre de usuario y la contraseña para acceder al servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="a08d7-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="a08d7-187">Comprobar la conectividad del agente a OMS</span><span class="sxs-lookup"><span data-stu-id="a08d7-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="a08d7-188">Puede comprobar fácilmente si los agentes se comunican con OMS con el procedimiento siguiente:</span><span class="sxs-lookup"><span data-stu-id="a08d7-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="a08d7-189">En el equipo con el agente de Windows, abra el Panel de Control.</span><span class="sxs-lookup"><span data-stu-id="a08d7-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="a08d7-190">Abra Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="a08d7-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="a08d7-191">Haga clic en la pestaña Azure Log Analytics (OMS).</span><span class="sxs-lookup"><span data-stu-id="a08d7-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="a08d7-192">En la columna Estado, verá que el agente se conectó correctamente al servicio Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="a08d7-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![agente conectado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="a08d7-194">configurar el proxy para Microsoft Monitoring Agent mediante el Panel de Control</span><span class="sxs-lookup"><span data-stu-id="a08d7-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="a08d7-195">Copie el ejemplo siguiente, actualícelo con la información específica para su entorno, guárdelo con una extensión de nombre de archivo PS1 y luego ejecute el script en cada equipo que se conecta directamente al servicio de OMS.</span><span class="sxs-lookup"><span data-stu-id="a08d7-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="a08d7-196">Instalación del agente a través de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="a08d7-196">Install the agent using the command line</span></span>
- <span data-ttu-id="a08d7-197">Modifique y, a continuación, use el siguiente ejemplo para instalar el agente con la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a08d7-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="a08d7-198">En el ejemplo se realiza una instalación silenciosa completa.</span><span class="sxs-lookup"><span data-stu-id="a08d7-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="a08d7-199">Si desea actualizar a un agente, debe utilizar la API de scripting de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a08d7-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="a08d7-200">Consulte la sección siguiente para actualizar un agente.</span><span class="sxs-lookup"><span data-stu-id="a08d7-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="a08d7-201">El agente usa IExpress como autoextractor mediante el comando `/c`.</span><span class="sxs-lookup"><span data-stu-id="a08d7-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="a08d7-202">Puede ver los modificadores de la línea de comandos en [Modificadores de la línea de comandos para los paquetes de actualización de software de IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) y, a continuación, actualizar el ejemplo para adaptarlo a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="a08d7-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="a08d7-203">Opciones específicas de MMA</span><span class="sxs-lookup"><span data-stu-id="a08d7-203">MMA-specific options</span></span>                   |<span data-ttu-id="a08d7-204">Notas</span><span class="sxs-lookup"><span data-stu-id="a08d7-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="a08d7-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="a08d7-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="a08d7-206">1 = Configurar el agente para informar a un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a08d7-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="a08d7-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="a08d7-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="a08d7-208">Id. de área de trabajo (guid) para el área de trabajo que se agregará</span><span class="sxs-lookup"><span data-stu-id="a08d7-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="a08d7-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="a08d7-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="a08d7-210">Clave del área de trabajo que se usa para autenticar inicialmente con el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a08d7-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="a08d7-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="a08d7-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="a08d7-212">Especificar el entorno en la nube donde se encuentra el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a08d7-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="a08d7-213">0 = nube comercial de Azure (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="a08d7-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="a08d7-214">1= Azure Government</span><span class="sxs-lookup"><span data-stu-id="a08d7-214">1 = Azure Government</span></span> |
|<span data-ttu-id="a08d7-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="a08d7-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="a08d7-216">Identificador URI del proxy que se va a usar</span><span class="sxs-lookup"><span data-stu-id="a08d7-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="a08d7-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="a08d7-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="a08d7-218">Nombre de usuario para acceder a un proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="a08d7-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="a08d7-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="a08d7-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="a08d7-220">Contraseña para acceder a un proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="a08d7-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="a08d7-221">Para evitar llegar al límite de longitud de la línea de comandos de IExpress, instale el agente sin ningún área de trabajo configurada y, después, use un script para configurar dicha área.</span><span class="sxs-lookup"><span data-stu-id="a08d7-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="a08d7-222">Si obtiene `Command line option syntax error.` al usar el parámetro `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE`, puede usar la siguiente solución alternativa:</span><span class="sxs-lookup"><span data-stu-id="a08d7-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="a08d7-223">Incorporación de un área de trabajo mediante un script</span><span class="sxs-lookup"><span data-stu-id="a08d7-223">Add a workspace using a script</span></span>
<span data-ttu-id="a08d7-224">Agregue un área de trabajo mediante la API de scripting del agente de Log Analytics siguiendo este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a08d7-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="a08d7-225">Para agregar un área de trabajo en Azure para el gobierno de EE. UU., use el siguiente ejemplo de secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="a08d7-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="a08d7-226">Si ha usado la línea de comandos o el script anteriormente para instalar o configurar el agente, `EnableAzureOperationalInsights` se ha reemplazado por `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="a08d7-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="a08d7-227">Instalación del agente utilizando DSC en Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="a08d7-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="a08d7-228">Puede usar el siguiente script de ejemplo para instalar el agente mediante DSC en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="a08d7-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="a08d7-229">En el ejemplo se instala el agente de 64 bits, identificado por el valor `URI`.</span><span class="sxs-lookup"><span data-stu-id="a08d7-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="a08d7-230">También puede utilizar la versión de 32 bits si se reemplaza el valor del identificador URI.</span><span class="sxs-lookup"><span data-stu-id="a08d7-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="a08d7-231">Estos son los identificadores URI para ambas versiones:</span><span class="sxs-lookup"><span data-stu-id="a08d7-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="a08d7-232">Agente de Windows de 64 bits: https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="a08d7-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="a08d7-233">Agente de Windows de 32 bits: https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="a08d7-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="a08d7-234">Este ejemplo de script y procedimiento no actualizará un agente existente.</span><span class="sxs-lookup"><span data-stu-id="a08d7-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="a08d7-235">Importe el módulo de DSC xPSDesiredStateConfiguration desde [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a08d7-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="a08d7-236">En Azure Automation, cree los recursos de variable *OPSINSIGHTS_WS_ID* y *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="a08d7-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="a08d7-237">Establezca *OPSINSIGHTS_WS_ID* en el identificador del área de trabajo de Log Analytics de OMS y *OPSINSIGHTS_WS_KEY* en la clave principal del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a08d7-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="a08d7-238">Use el siguiente script y guárdelo como MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="a08d7-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="a08d7-239">Después de modificar el ejemplo, úselo para instalar el agente utilizando DSC en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a08d7-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="a08d7-240">Importe MMAgent.ps1 en Automatización de Azure a través de la interfaz o el cmdlet de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="a08d7-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="a08d7-241">Asigne un nodo a la configuración.</span><span class="sxs-lookup"><span data-stu-id="a08d7-241">Assign a node to the configuration.</span></span> <span data-ttu-id="a08d7-242">Durante los 15 minutos siguientes, el nodo comprueba la configuración y MMA se inserta en el nodo.</span><span class="sxs-lookup"><span data-stu-id="a08d7-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="a08d7-243">Obtención del valor de ProductId más reciente</span><span class="sxs-lookup"><span data-stu-id="a08d7-243">Get the latest ProductId value</span></span>

<span data-ttu-id="a08d7-244">El valor `ProductId value` del script MMAgent.ps1 es exclusivo de cada versión del agente.</span><span class="sxs-lookup"><span data-stu-id="a08d7-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="a08d7-245">Cuando se publica una versión actualizada de cada agente, el valor de ProductId cambia.</span><span class="sxs-lookup"><span data-stu-id="a08d7-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="a08d7-246">Por lo tanto, cuando ProductId cambie en el futuro, podrá encontrar la versión del agente mediante un sencillo script.</span><span class="sxs-lookup"><span data-stu-id="a08d7-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="a08d7-247">Una vez que haya instalado la última versión del agente en un servidor de prueba, puede usar el siguiente script para obtener el valor de ProductId instalado.</span><span class="sxs-lookup"><span data-stu-id="a08d7-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="a08d7-248">Con el último valor de ProductId, puede actualizar el del script MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="a08d7-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="a08d7-249">Configuración de un agente de forma manual o incorporación de áreas de trabajo adicionales</span><span class="sxs-lookup"><span data-stu-id="a08d7-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="a08d7-250">Si tiene instalados los agentes pero aún no los ha configurado o si quiere que el agente informe a varias áreas de trabajo, puede usar la siguiente información para habilitarlos o volver a configurarlos.</span><span class="sxs-lookup"><span data-stu-id="a08d7-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="a08d7-251">Una vez configurado el agente, se registrará con el servicio de agente y obtendrá la información de configuración necesaria y los paquetes de administración que contienen la información de la solución.</span><span class="sxs-lookup"><span data-stu-id="a08d7-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="a08d7-252">Una vez que Microsoft Monitoring Agent esté instalado, abra el **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="a08d7-253">**Abra Microsoft Monitoring Agent** y haga clic en la pestaña **Azure Log Analytics (OMS)**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="a08d7-254">Haga clic en **Agregar** para abrir el cuadro **Add a Log Analytics Workspace** (Agregar un área de trabajo de Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="a08d7-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="a08d7-255">Pegue el **identificador del área de trabajo** y la **clave del área de trabajo (clave principal)** que copió en el Bloc de notas durante un procedimiento anterior para el área de trabajo que desee agregar y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="a08d7-256">![configurar Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="a08d7-257">Una vez que los datos se hayan recopilado de los equipos supervisados por el agente, el número de equipos supervisados por OMS aparecerá como **Servers Connected** (Servidores conectados) en el portal de OMS, en la pestaña **Connected Sources** (Orígenes conectados) de **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="a08d7-258">Para deshabilitar un agente</span><span class="sxs-lookup"><span data-stu-id="a08d7-258">To disable an agent</span></span>
1. <span data-ttu-id="a08d7-259">Después de instalar el agente, abra el **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="a08d7-260">Abra Microsoft Monitoring Agent y haga clic en la pestaña **Azure Log Analytics (OMS)** .</span><span class="sxs-lookup"><span data-stu-id="a08d7-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="a08d7-261">Seleccione un área de trabajo y haga clic en **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="a08d7-262">Repita este paso para el resto de áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a08d7-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="a08d7-263">(Opcional) Configurar los agentes para que envíen notificaciones a un grupo de administración de Operations Manager</span><span class="sxs-lookup"><span data-stu-id="a08d7-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="a08d7-264">Si utiliza Operations Manager en su infraestructura de TI, también puede usar el agente de MMA como agente de Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="a08d7-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="a08d7-265">Si desea configurar los agentes de MMA para que envíen notificaciones a un grupo de administración de Operations Manager</span><span class="sxs-lookup"><span data-stu-id="a08d7-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="a08d7-266">En el equipo en el que está instalado el agente, abra el **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="a08d7-267">Abra **Microsoft Monitoring Agent** y haga clic en la pestaña **Operations Manager**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="a08d7-268">![Pestaña Operations Manager de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="a08d7-269">Si los servidores de Operations Manager tienen integración con Active Directory, haga clic en **Actualizar automáticamente asignaciones de grupos de administración desde AD DS**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="a08d7-270">Haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar un grupo de administración**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="a08d7-271">![Agregar un grupo de administración de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="a08d7-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="a08d7-272">En el cuadro **Nombre del grupo de administración** , especifique un nombre para el grupo de administración.</span><span class="sxs-lookup"><span data-stu-id="a08d7-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="a08d7-273">En el cuadro **Servidor de administración principal** , escriba el nombre de equipo del servidor de administración principal.</span><span class="sxs-lookup"><span data-stu-id="a08d7-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="a08d7-274">En el cuadro **Puerto de servidor de administración** , escriba el número de puerto TCP.</span><span class="sxs-lookup"><span data-stu-id="a08d7-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="a08d7-275">En **Cuenta de acción del agente**, seleccione la cuenta de sistema local o una cuenta de dominio local.</span><span class="sxs-lookup"><span data-stu-id="a08d7-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="a08d7-276">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Agregar un grupo de administración** y después haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="a08d7-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a08d7-277">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a08d7-277">Next steps</span></span>

- <span data-ttu-id="a08d7-278">[Incorporación de soluciones de Log Analytics desde la galería de soluciones](log-analytics-add-solutions.md) para agregar funcionalidad y recopilar información.</span><span class="sxs-lookup"><span data-stu-id="a08d7-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
