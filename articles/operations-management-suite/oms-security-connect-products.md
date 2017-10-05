---
title: "Conexión de productos de seguridad a la solución Seguridad y auditoría de Operations Management Suite (OMS) | Microsoft Docs"
description: "Este documento le ayuda a conectar sus productos de seguridad a la solución Seguridad y auditoría de Operations Management Suite usando el formato de evento común."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="5e5b8-103">Conexión de productos de seguridad a la solución Seguridad y auditoría de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="5e5b8-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="5e5b8-104">Este documento le ayuda a conectar sus productos de seguridad en la solución Seguridad y auditoría de OMS.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="5e5b8-105">Se admiten los siguientes orígenes:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-105">The following sources are supported:</span></span>

- <span data-ttu-id="5e5b8-106">Eventos de formato de evento común (CEF)</span><span class="sxs-lookup"><span data-stu-id="5e5b8-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="5e5b8-107">Eventos de Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="5e5b8-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="5e5b8-108">¿Qué es el formato de evento común (CEF)?</span><span class="sxs-lookup"><span data-stu-id="5e5b8-108">What is CEF?</span></span>
<span data-ttu-id="5e5b8-109">El formato de evento común (CEF) es un formato estándar del sector sobre mensajes de Syslog, que utilizan muchos proveedores de seguridad para facilitar la interoperabilidad entre distintas plataformas.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="5e5b8-110">La solución Seguridad y auditoría de OMS admite la ingesta de datos usando CEF, lo que le permite conectar sus productos de seguridad con Seguridad de OMS.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="5e5b8-111">Al conectar el origen de datos a OMS, podrá sacar partido de las siguientes funcionalidades que forman parte de esta plataforma:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="5e5b8-112">Búsqueda y correlación</span><span class="sxs-lookup"><span data-stu-id="5e5b8-112">Search & Correlation</span></span>
- <span data-ttu-id="5e5b8-113">Auditoría</span><span class="sxs-lookup"><span data-stu-id="5e5b8-113">Auditing</span></span>
- <span data-ttu-id="5e5b8-114">Alerta</span><span class="sxs-lookup"><span data-stu-id="5e5b8-114">Alert</span></span>
- <span data-ttu-id="5e5b8-115">Información sobre amenazas</span><span class="sxs-lookup"><span data-stu-id="5e5b8-115">Threat Intelligence</span></span>
- <span data-ttu-id="5e5b8-116">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="5e5b8-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="5e5b8-117">Colección de registros de soluciones de seguridad</span><span class="sxs-lookup"><span data-stu-id="5e5b8-117">Collection of security solution logs</span></span>

<span data-ttu-id="5e5b8-118">Seguridad de OMS admite la recopilación de registros utilizando CEF sobre Syslogs y registros [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="5e5b8-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="5e5b8-119">En este ejemplo, el origen (el equipo que genera los registros) es un equipo de Linux que ejecuta el demonio syslog-ng y el destino es Seguridad de OMS.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="5e5b8-120">Para preparar el equipo Linux, tendrá que realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="5e5b8-121">Descargar el agente OMS para Linux, versión 1.2.0-25 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="5e5b8-122">Consulte la sección con la **guía de instalación rápida** de [este artículo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) para instalar e incorporar el agente al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="5e5b8-123">Normalmente, el agente se instala en un equipo diferente de aquel en el que se generan los registros.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="5e5b8-124">El reenvío de los registros al equipo con el agente, normalmente requiere los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="5e5b8-125">Configurar el producto/máquina con los registros para que reenvíe los eventos necesarios al demonio syslog (rsyslog o syslog-ng) en el equipo con el agente.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="5e5b8-126">Habilitar el demonio syslog en el equipo del agente para recibir mensajes desde un sistema remoto.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="5e5b8-127">En el equipo del agente, los eventos tienen que enviarse desde el demonio syslog al puerto UDP 25226 local.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="5e5b8-128">El agente escucha los eventos entrantes en este puerto.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="5e5b8-129">Este es un ejemplo de configuración para enviar todos los eventos desde el sistema local al agente (puede modificar la configuración para ajustarla a su configuración regional):</span><span class="sxs-lookup"><span data-stu-id="5e5b8-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="5e5b8-130">Abra la ventana de terminal y vaya al directorio */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="5e5b8-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="5e5b8-131">Cree un nuevo archivo *security-config-omsagent.conf* y agregue el siguiente contenido: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="5e5b8-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="5e5b8-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="5e5b8-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="5e5b8-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="5e5b8-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="5e5b8-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="5e5b8-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="5e5b8-135">Descargue el archivo *security_events.conf* y colóquelo en */etc/opt/microsoft/omsagent/conf/omsagent.d/* en el equipo del agente OMS.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="5e5b8-136">Escriba el siguiente comando para reiniciar el demonio syslog: *para syslog-ng ejecutar:*</span><span class="sxs-lookup"><span data-stu-id="5e5b8-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="5e5b8-137">*Para la ejecución de rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="5e5b8-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="5e5b8-138">Escriba el siguiente comando para reiniciar el agente OMS:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="5e5b8-139">*Para la ejecución de syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="5e5b8-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="5e5b8-140">*Para la ejecución de rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="5e5b8-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="5e5b8-141">Escriba el siguiente comando y revise el resultado para confirmar que no hay ningún error en el registro del agente OMS:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="5e5b8-142">Revisión de eventos de seguridad recopilados</span><span class="sxs-lookup"><span data-stu-id="5e5b8-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="5e5b8-143">Una vez finalizada la configuración, Seguridad de OMS iniciará la ingesta del evento de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="5e5b8-144">Para visualizar esos eventos, abra la búsqueda de registros, escriba el comando *Type=CommonSecurityLog* en el campo de búsqueda y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="5e5b8-145">En el ejemplo siguiente se muestra el resultado de este comando, tenga en cuenta que en este caso Seguridad OMS ya ha ingerido los registros de seguridad en varios proveedores:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Evaluación de línea base de Seguridad y auditoría de OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="5e5b8-147">Puede refinar la búsqueda para un proveedor único, por ejemplo, para visualizar los registros de Cisco en línea, escriba: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="5e5b8-148">"CommonSecurityLog" tiene campos predefinidos para cualquier encabezado CEF incluida las extensiones básicas, mientras cualquier otra extensión tanto si se trata de una "Extensión personalizada" como si no, se insertará en el campo "AdditionalExtensions".</span><span class="sxs-lookup"><span data-stu-id="5e5b8-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="5e5b8-149">Puede usar la característica de campos personalizados para obtener campos dedicados.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="5e5b8-150">Acceso a equipos sin evaluación de línea base</span><span class="sxs-lookup"><span data-stu-id="5e5b8-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="5e5b8-151">OMS admite el perfil de línea base de miembros de dominio en Windows Server 2008 R2 y hasta Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="5e5b8-152">La línea base de Windows Server 2016 todavía no está finalizada y se agregará en cuanto se publique.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="5e5b8-153">Todos los demás sistemas operativos examinados mediante la evaluación de línea base de Seguridad y auditoría de OMS aparecen en la sección **Acceso a equipos sin evaluación de línea base**.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="5e5b8-154">Consulte también</span><span class="sxs-lookup"><span data-stu-id="5e5b8-154">See also</span></span>
<span data-ttu-id="5e5b8-155">En este documento, ha aprendido a conectar su solución CEF a OMS.</span><span class="sxs-lookup"><span data-stu-id="5e5b8-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="5e5b8-156">Para obtener más información sobre Seguridad de OMS, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="5e5b8-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="5e5b8-157">Información general de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="5e5b8-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="5e5b8-158">Supervisión de las alertas de seguridad y su respuesta en la solución Security and Audit de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5e5b8-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="5e5b8-159">Supervisión de los recursos en la solución Security and Audit de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5e5b8-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

