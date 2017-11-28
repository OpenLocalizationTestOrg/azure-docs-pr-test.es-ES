---
title: "aaaConnecting la solución de auditoría y seguridad productos toohello seguridad Operations Management Suite (OMS) | Documentos de Microsoft"
description: "Este documento le ayuda a tooconnect su tooOperations de productos de seguridad, seguridad del conjunto de administración y solución de auditoría con formato de eventos común."
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
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="3295d-103">Conectar la solución de auditoría y seguridad productos toohello seguridad Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="3295d-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="3295d-104">Este documento le ayuda a conectar sus productos de seguridad en hello seguridad de OMS y solución de auditoría.</span><span class="sxs-lookup"><span data-stu-id="3295d-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="3295d-105">se admite Hola siguientes orígenes:</span><span class="sxs-lookup"><span data-stu-id="3295d-105">hello following sources are supported:</span></span>

- <span data-ttu-id="3295d-106">Eventos de formato de evento común (CEF)</span><span class="sxs-lookup"><span data-stu-id="3295d-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="3295d-107">Eventos de Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="3295d-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="3295d-108">¿Qué es el formato de evento común (CEF)?</span><span class="sxs-lookup"><span data-stu-id="3295d-108">What is CEF?</span></span>
<span data-ttu-id="3295d-109">Formato de evento comunes (CEF) es un formato estándar del sector sobre mensajes de Syslog, utilizado por muchos proveedores tooallow evento interoperabilidad de la seguridad entre varias plataformas distintas.</span><span class="sxs-lookup"><span data-stu-id="3295d-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="3295d-110">Solución de auditoría y seguridad de OMS admiten la ingesta de datos con los productos de seguridad CEF, lo que permite tooconnect con seguridad de OMS.</span><span class="sxs-lookup"><span data-stu-id="3295d-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="3295d-111">Al conectar su tooOMS de origen de datos, son tootake puede aprovechar Hola siguiendo las capacidades que forman parte de esta plataforma:</span><span class="sxs-lookup"><span data-stu-id="3295d-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="3295d-112">Búsqueda y correlación</span><span class="sxs-lookup"><span data-stu-id="3295d-112">Search & Correlation</span></span>
- <span data-ttu-id="3295d-113">Auditoría</span><span class="sxs-lookup"><span data-stu-id="3295d-113">Auditing</span></span>
- <span data-ttu-id="3295d-114">Alerta</span><span class="sxs-lookup"><span data-stu-id="3295d-114">Alert</span></span>
- <span data-ttu-id="3295d-115">Información sobre amenazas</span><span class="sxs-lookup"><span data-stu-id="3295d-115">Threat Intelligence</span></span>
- <span data-ttu-id="3295d-116">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="3295d-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="3295d-117">Colección de registros de soluciones de seguridad</span><span class="sxs-lookup"><span data-stu-id="3295d-117">Collection of security solution logs</span></span>

<span data-ttu-id="3295d-118">Seguridad de OMS admite la recopilación de registros utilizando CEF sobre Syslogs y registros [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="3295d-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="3295d-119">En este ejemplo, el origen de hello (equipo que genera registros de hello) es un equipo de Linux que se ejecuta el demonio syslog-ng y destino de hello es seguridad de OMS.</span><span class="sxs-lookup"><span data-stu-id="3295d-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="3295d-120">tareas de equipo Linux tooprepare Hola que necesitará hello tooperform siguientes:</span><span class="sxs-lookup"><span data-stu-id="3295d-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="3295d-121">Descargar Hola agente de OMS para Linux, versión 1.2.0-25 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="3295d-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="3295d-122">Siga la sección de hello **Guía de instalación rápida** de [este artículo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall y el área de trabajo de hello incorporar agente tooyour.</span><span class="sxs-lookup"><span data-stu-id="3295d-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="3295d-123">Normalmente, el agente de hello está instalado en un equipo diferente de hello uno en los registros de Hola se generan.</span><span class="sxs-lookup"><span data-stu-id="3295d-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="3295d-124">Equipo de agente de reenvío Hola registros toohello normalmente requerirá Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3295d-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="3295d-125">Configurar Hola registro producto/máquina tooforward Hola eventos necesarios toohello demonio syslog (rsyslog o syslog-ng) en el equipo del agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3295d-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="3295d-126">Habilitar el demonio de syslog hello en los mensajes de Hola agente máquina tooreceive desde un sistema remoto.</span><span class="sxs-lookup"><span data-stu-id="3295d-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="3295d-127">En el equipo de agente de hello, eventos de hello necesitan toobe enviado desde el puerto UDP 25226 del toolocal de demonio de syslog Hola.</span><span class="sxs-lookup"><span data-stu-id="3295d-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="3295d-128">agente de Hello está realizando escuchas para los eventos entrantes en este puerto.</span><span class="sxs-lookup"><span data-stu-id="3295d-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="3295d-129">Hola te mostramos un ejemplo de configuración para enviar todos los eventos de hello local system toohello agent (puede modificar Hola configuración toofit la configuración regional):</span><span class="sxs-lookup"><span data-stu-id="3295d-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="3295d-130">Ventana de terminal de hello abierta y vaya toohello directorio */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="3295d-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="3295d-131">Crear un nuevo archivo *omsagent.conf de configuración de seguridad* y agregue Hola siguen contenido: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="3295d-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="3295d-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="3295d-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="3295d-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="3295d-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="3295d-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="3295d-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="3295d-135">Descargar archivo hello *security_events.conf* y colóquelo en */etc/opt/microsoft/omsagent/conf/omsagent.d/* en el equipo del agente de OMS de Hola.</span><span class="sxs-lookup"><span data-stu-id="3295d-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="3295d-136">Escriba comando hello debajo de demonio de syslog de Hola toorestart: *para syslog-ng ejecutar:*</span><span class="sxs-lookup"><span data-stu-id="3295d-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="3295d-137">*Para la ejecución de rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="3295d-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="3295d-138">Escriba el comando de hello debajo de hello toorestart agente de OMS:</span><span class="sxs-lookup"><span data-stu-id="3295d-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="3295d-139">*Para la ejecución de syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="3295d-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="3295d-140">*Para la ejecución de rsyslog:*</span><span class="sxs-lookup"><span data-stu-id="3295d-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="3295d-141">Escriba el siguiente comando de Hola y revise hello tooconfirm de resultado que no hay ningún error en el registro del agente de OMS de hello:</span><span class="sxs-lookup"><span data-stu-id="3295d-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="3295d-142">Revisión de eventos de seguridad recopilados</span><span class="sxs-lookup"><span data-stu-id="3295d-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="3295d-143">Una vez hello configuración finalizado, eventos de seguridad de hello iniciará toobe ingerida por la seguridad de OMS.</span><span class="sxs-lookup"><span data-stu-id="3295d-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="3295d-144">toovisualize esos eventos, abra Hola búsqueda de registros, escriba el comando de hello *tipo = CommonSecurityLog* en Hola campo de búsqueda y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="3295d-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="3295d-145">Hello en el ejemplo siguiente se muestra resultado de hello de este comando, tenga en cuenta que en este caso seguridad OMS ya ingestión registros de seguridad en varios proveedores:</span><span class="sxs-lookup"><span data-stu-id="3295d-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Evaluación de línea base de Seguridad y auditoría de OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="3295d-147">Puede refinar la búsqueda de un proveedor único, por ejemplo, toovisualize registra Cisco en línea, escriba: *tipo = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="3295d-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="3295d-148">Hola "CommonSecurityLog" tiene predefinidos los campos para cualquier encabezado CEF incluidos extensios básica de hello, mientras otra extensión, ya sea "Custom Extension" o no es así, se insertará en el campo "AdditionalExtensions".</span><span class="sxs-lookup"><span data-stu-id="3295d-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="3295d-149">Puede usar campos de tooget dedicado de característica de campos personalizados de Hola de él.</span><span class="sxs-lookup"><span data-stu-id="3295d-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="3295d-150">Acceso a equipos sin evaluación de línea base</span><span class="sxs-lookup"><span data-stu-id="3295d-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="3295d-151">OMS admite el perfil de línea de base de miembro de dominio de hello en Windows Server 2008 R2 hasta tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="3295d-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="3295d-152">La línea base de Windows Server 2016 todavía no está finalizada y se agregará en cuanto se publique.</span><span class="sxs-lookup"><span data-stu-id="3295d-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="3295d-153">Todos los demás sistemas operativos analizados a través de evaluación de línea de base de seguridad de OMS y auditoría aparecen bajo hello **equipos falta la evaluación de la línea de base** sección.</span><span class="sxs-lookup"><span data-stu-id="3295d-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="3295d-154">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3295d-154">See also</span></span>
<span data-ttu-id="3295d-155">En este documento, se habrá aprendido cómo tooconnect su tooOMS de solución CEF.</span><span class="sxs-lookup"><span data-stu-id="3295d-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="3295d-156">toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="3295d-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="3295d-157">Información general de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="3295d-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="3295d-158">Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría</span><span class="sxs-lookup"><span data-stu-id="3295d-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="3295d-159">Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3295d-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

