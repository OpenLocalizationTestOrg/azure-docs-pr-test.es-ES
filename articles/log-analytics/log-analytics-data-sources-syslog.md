---
title: "Recopilación y análisis de mensajes de Syslog en Log Analytics (OMS) | Microsoft Docs"
description: "Syslog es un protocolo de registro de eventos que es común a Linux. En este artículo se describe cómo configurar la recopilación de mensajes de Syslog en Log Analytics y detalles de los registros que crean en el repositorio de OMS."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="12bdd-104">Orígenes de datos de Syslog en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="12bdd-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="12bdd-105">Syslog es un protocolo de registro de eventos que es común a Linux.</span><span class="sxs-lookup"><span data-stu-id="12bdd-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="12bdd-106">Las aplicaciones envían mensajes que pueden almacenarse en la máquina local o entregarse a un recopilador de Syslog.</span><span class="sxs-lookup"><span data-stu-id="12bdd-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="12bdd-107">Al instalar el agente de OMS para Linux, este configura el demonio Syslog local para que reenvíe mensajes al agente.</span><span class="sxs-lookup"><span data-stu-id="12bdd-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="12bdd-108">En ese momento, el agente envía el mensaje a Log Analytics, donde se crea un registro correspondiente en el repositorio de OMS.</span><span class="sxs-lookup"><span data-stu-id="12bdd-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="12bdd-109">Log Analytics admite la recopilación de mensajes enviados por rsyslog o syslog-ng, donde rsyslog es el demonio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="12bdd-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="12bdd-110">El demonio predeterminado de Syslog en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (Sysklog) no se admite para la recopilación de eventos de Syslog.</span><span class="sxs-lookup"><span data-stu-id="12bdd-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="12bdd-111">Para recopilar datos de Syslog de esta versión de estas distribuciones, es necesario instalar el [demonio rsyslog](http://rsyslog.com) y configurarlo para reemplazar Sysklog.</span><span class="sxs-lookup"><span data-stu-id="12bdd-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Recopilación de Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="12bdd-113">Configuración de Syslog</span><span class="sxs-lookup"><span data-stu-id="12bdd-113">Configuring Syslog</span></span>
<span data-ttu-id="12bdd-114">El agente de OMS para Linux solo recopilará los eventos con los recursos y los niveles de gravedad que se especifican en su configuración.</span><span class="sxs-lookup"><span data-stu-id="12bdd-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="12bdd-115">Puede configurar Syslog a través del portal de OMS o mediante la administración de archivos de configuración de sus agentes de Linux.</span><span class="sxs-lookup"><span data-stu-id="12bdd-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="12bdd-116">Configuración de Syslog en el portal de OMS</span><span class="sxs-lookup"><span data-stu-id="12bdd-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="12bdd-117">Configure Syslog desde el [menú de datos en la configuración de Log Analytics](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="12bdd-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="12bdd-118">Esta configuración se entrega al archivo de configuración de cada agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="12bdd-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="12bdd-119">Para agregar un nuevo recurso, escriba su nombre y haga clic en **+**.</span><span class="sxs-lookup"><span data-stu-id="12bdd-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="12bdd-120">Para cada recurso, solo se recopilarán los mensajes con los niveles de gravedad seleccionados.</span><span class="sxs-lookup"><span data-stu-id="12bdd-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="12bdd-121">Compruebe los niveles de gravedad del recurso determinado que desea recopilar.</span><span class="sxs-lookup"><span data-stu-id="12bdd-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="12bdd-122">No puede proporcionar criterios adicionales para filtrar mensajes.</span><span class="sxs-lookup"><span data-stu-id="12bdd-122">You cannot provide any additional criteria to filter messages.</span></span>

![Configuración de Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="12bdd-124">De forma predeterminada, todos los cambios realizados en la configuración se insertan automáticamente en todos los agentes.</span><span class="sxs-lookup"><span data-stu-id="12bdd-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="12bdd-125">Si desea configurar Syslog manualmente en cada uno de los agentes de Linux, desactive la casilla *Apply below configuration to my Linux machines*(Aplicar la configuración siguiente a mis máquinas Linux).</span><span class="sxs-lookup"><span data-stu-id="12bdd-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="12bdd-126">Configuración de Syslog en agente de Linux</span><span class="sxs-lookup"><span data-stu-id="12bdd-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="12bdd-127">Cuando el [agente de OMS se instala en un cliente Linux](log-analytics-linux-agents.md), instala un archivo de configuración de Syslog predeterminado que define el recurso y la gravedad de los mensajes que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="12bdd-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="12bdd-128">Puede modificar este archivo para cambiar la configuración.</span><span class="sxs-lookup"><span data-stu-id="12bdd-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="12bdd-129">El archivo de configuración es diferente según el demonio Syslog que ha instalado el cliente.</span><span class="sxs-lookup"><span data-stu-id="12bdd-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="12bdd-130">Si modifica la configuración de Syslog, tiene que reiniciar el demonio Syslog para que los cambios surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="12bdd-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="12bdd-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="12bdd-131">rsyslog</span></span>
<span data-ttu-id="12bdd-132">El archivo de configuración de rsyslog se encuentra en **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="12bdd-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="12bdd-133">A continuación se muestra su contenido predeterminado.</span><span class="sxs-lookup"><span data-stu-id="12bdd-133">Its default contents are shown below.</span></span>  <span data-ttu-id="12bdd-134">Recopila mensajes de Syslog enviados desde el agente local para todos los recursos con, al menos, un nivel de advertencia.</span><span class="sxs-lookup"><span data-stu-id="12bdd-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="12bdd-135">Para quitar un recurso, elimine su sección del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="12bdd-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="12bdd-136">Puede limitar los niveles de gravedad que se recopilan para un recurso determinado mediante la modificación de la entrada de ese recurso.</span><span class="sxs-lookup"><span data-stu-id="12bdd-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="12bdd-137">Por ejemplo, para limitar el recurso del usuario a mensajes con una gravedad de error o superior, debe modificar esa línea del archivo de configuración de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="12bdd-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="12bdd-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="12bdd-138">syslog-ng</span></span>
<span data-ttu-id="12bdd-139">El archivo de configuración de syslog-ng se encuentra en **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="12bdd-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="12bdd-140">A continuación se muestra su contenido predeterminado.</span><span class="sxs-lookup"><span data-stu-id="12bdd-140">Its default contents are shown below.</span></span>  <span data-ttu-id="12bdd-141">Recopila mensajes de Syslog enviados desde el agente local para todos los recursos y todos los niveles de gravedad.</span><span class="sxs-lookup"><span data-stu-id="12bdd-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="12bdd-142">Para quitar un recurso, elimine su sección del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="12bdd-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="12bdd-143">Puede limitar los niveles de gravedad que se recopilan de un recurso determinado, para lo que debe eliminarlos de la lista.</span><span class="sxs-lookup"><span data-stu-id="12bdd-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="12bdd-144">Por ejemplo, para limitar el recurso del usuario solo a mensajes de alerta y críticos, debe modificar la sección del archivo de configuración de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="12bdd-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="12bdd-145">Recopilación de datos de puertos de Syslog adicionales</span><span class="sxs-lookup"><span data-stu-id="12bdd-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="12bdd-146">El agente de OMS escucha los mensajes de Syslog en el cliente local en el puerto 25224.</span><span class="sxs-lookup"><span data-stu-id="12bdd-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="12bdd-147">Cuando se instala el agente, se aplica una configuración de Syslog predeterminada, que se encuentra en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="12bdd-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="12bdd-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="12bdd-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="12bdd-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="12bdd-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="12bdd-150">Puede cambiar el número de puerto si crea dos archivos de configuración: un archivo de configuración de FluentD y un archivo rsyslog-or-syslog-ng según el demonio Syslog que haya instalado.</span><span class="sxs-lookup"><span data-stu-id="12bdd-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="12bdd-151">El archivo de configuración de FluentD debe ser un nuevo archivo ubicado en: `/etc/opt/microsoft/omsagent/conf/omsagent.d`; reemplace el valor de la entrada **port** por el número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="12bdd-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="12bdd-152">Para rsyslog, debe crear un archivo de configuración ubicado en: `/etc/rsyslog.d/`; reemplace el valor %SYSLOG_PORT% por el número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="12bdd-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="12bdd-153">Si modifica este valor en el archivo de configuración `95-omsagent.conf`, se sobrescribirá cuando el agente aplique una configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="12bdd-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="12bdd-154">Para modificar la configuración de syslog-ng, copie la configuración del ejemplo que se muestra a continuación y agregue la configuración modificada personalizada al final del archivo de configuración syslog-ng.conf ubicado en `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="12bdd-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="12bdd-155">**No** use la etiqueta predeterminada **%WORKSPACE_ID%_oms** ni **%WORKSPACE_ID_OMS**; defina una etiqueta personalizada para ayudar a distinguir los cambios.</span><span class="sxs-lookup"><span data-stu-id="12bdd-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="12bdd-156">Si modifica los valores predeterminados en el archivo de configuración, se sobrescribirán cuando el agente aplique una configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="12bdd-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="12bdd-157">Después de completar los cambios, Syslog y el servicio de agente de OMS deben reiniciarse para asegurarse de que los cambios de configuración surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="12bdd-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="12bdd-158">Propiedades de registros de Syslog</span><span class="sxs-lookup"><span data-stu-id="12bdd-158">Syslog record properties</span></span>
<span data-ttu-id="12bdd-159">Los registros de Syslog tienen un tipo **Syslog** y las propiedades que aparecen en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="12bdd-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="12bdd-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="12bdd-160">Property</span></span> | <span data-ttu-id="12bdd-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="12bdd-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="12bdd-162">Equipo</span><span class="sxs-lookup"><span data-stu-id="12bdd-162">Computer</span></span> |<span data-ttu-id="12bdd-163">Nombre del equipo desde el que se recopiló el evento.</span><span class="sxs-lookup"><span data-stu-id="12bdd-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="12bdd-164">Facility</span><span class="sxs-lookup"><span data-stu-id="12bdd-164">Facility</span></span> |<span data-ttu-id="12bdd-165">Define la parte del sistema que ha generado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="12bdd-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="12bdd-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="12bdd-166">HostIP</span></span> |<span data-ttu-id="12bdd-167">Dirección IP del sistema que envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="12bdd-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="12bdd-168">HostName</span><span class="sxs-lookup"><span data-stu-id="12bdd-168">HostName</span></span> |<span data-ttu-id="12bdd-169">Nombre del sistema que envía el mensaje.</span><span class="sxs-lookup"><span data-stu-id="12bdd-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="12bdd-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="12bdd-170">SeverityLevel</span></span> |<span data-ttu-id="12bdd-171">Nivel de gravedad del evento.</span><span class="sxs-lookup"><span data-stu-id="12bdd-171">Severity level of the event.</span></span> |
| <span data-ttu-id="12bdd-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="12bdd-172">SyslogMessage</span></span> |<span data-ttu-id="12bdd-173">Texto del mensaje.</span><span class="sxs-lookup"><span data-stu-id="12bdd-173">Text of the message.</span></span> |
| <span data-ttu-id="12bdd-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="12bdd-174">ProcessID</span></span> |<span data-ttu-id="12bdd-175">Identificador del proceso que ha generado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="12bdd-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="12bdd-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="12bdd-176">EventTime</span></span> |<span data-ttu-id="12bdd-177">Fecha y hora en que se generó el evento.</span><span class="sxs-lookup"><span data-stu-id="12bdd-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="12bdd-178">Consultas de registro con registros de Syslog</span><span class="sxs-lookup"><span data-stu-id="12bdd-178">Log queries with Syslog records</span></span>
<span data-ttu-id="12bdd-179">La tabla siguiente proporciona ejemplos distintos de consultas de registro que recuperan registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="12bdd-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="12bdd-180">Consultar</span><span class="sxs-lookup"><span data-stu-id="12bdd-180">Query</span></span> | <span data-ttu-id="12bdd-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="12bdd-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="12bdd-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="12bdd-182">Type=Syslog</span></span> |<span data-ttu-id="12bdd-183">Todos los registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="12bdd-183">All Syslogs.</span></span> |
| <span data-ttu-id="12bdd-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="12bdd-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="12bdd-185">Todos los registros de Syslog con gravedad de error.</span><span class="sxs-lookup"><span data-stu-id="12bdd-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="12bdd-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="12bdd-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="12bdd-187">Número de registros de Syslog por equipo.</span><span class="sxs-lookup"><span data-stu-id="12bdd-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="12bdd-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="12bdd-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="12bdd-189">Número de registros de Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="12bdd-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="12bdd-190">Si el área de trabajo se ha actualizado al [nuevo lenguaje de consulta Log Analytics](log-analytics-log-search-upgrade.md), las consultas anteriores cambiarían como sigue.</span><span class="sxs-lookup"><span data-stu-id="12bdd-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="12bdd-191">Consultar</span><span class="sxs-lookup"><span data-stu-id="12bdd-191">Query</span></span> | <span data-ttu-id="12bdd-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="12bdd-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="12bdd-193">syslog</span><span class="sxs-lookup"><span data-stu-id="12bdd-193">Syslog</span></span> |<span data-ttu-id="12bdd-194">Todos los registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="12bdd-194">All Syslogs.</span></span> |
| <span data-ttu-id="12bdd-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="12bdd-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="12bdd-196">Todos los registros de Syslog con gravedad de error.</span><span class="sxs-lookup"><span data-stu-id="12bdd-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="12bdd-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="12bdd-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="12bdd-198">Número de registros de Syslog por equipo.</span><span class="sxs-lookup"><span data-stu-id="12bdd-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="12bdd-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="12bdd-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="12bdd-200">Número de registros de Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="12bdd-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12bdd-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12bdd-201">Next steps</span></span>
* <span data-ttu-id="12bdd-202">Obtenga información acerca de las [búsquedas de registros](log-analytics-log-searches.md) para analizar los datos recopilados de orígenes de datos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="12bdd-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="12bdd-203">Use [Campos personalizados](log-analytics-custom-fields.md) para analizar datos de registros de Syslog en campos individuales.</span><span class="sxs-lookup"><span data-stu-id="12bdd-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="12bdd-204">[Configure agentes de Linux](log-analytics-linux-agents.md) para recopilar otros tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="12bdd-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
