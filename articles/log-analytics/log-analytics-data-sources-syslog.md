---
title: aaaCollect y analizar los mensajes de Syslog en OMS Log Analytics | Documentos de Microsoft
description: "Syslog es un protocolo de registro de eventos que es común tooLinux. Este artículo describe cómo tooconfigure colección de mensajes de Syslog en análisis de registros y detalles de los registros de hello crean en el repositorio de OMS Hola."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="e19ff-104">Orígenes de datos de Syslog en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e19ff-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="e19ff-105">Syslog es un protocolo de registro de eventos que es común tooLinux.</span><span class="sxs-lookup"><span data-stu-id="e19ff-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="e19ff-106">Las aplicaciones enviará los mensajes que pueden almacenados en el equipo local de Hola o entregar a tooa Syslog recopilador.</span><span class="sxs-lookup"><span data-stu-id="e19ff-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="e19ff-107">Cuando se instala el agente de OMS para Linux hello, configura el agente de toohello de hello local Syslog daemon tooforward mensajes.</span><span class="sxs-lookup"><span data-stu-id="e19ff-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="e19ff-108">agente de Hello, a continuación, envía tooLog de mensaje de Hola análisis donde se crea un registro correspondiente en el repositorio OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="e19ff-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="e19ff-109">Análisis de registros es compatible con la colección de mensajes enviados por rsyslog o syslog-ng, donde rsyslog es el demonio de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="e19ff-110">demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="e19ff-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="e19ff-111">Hola toocollect datos de syslog de esta versión de las distribuciones, [demonio rsyslog](http://rsyslog.com) debe estar instalado y configurado tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="e19ff-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Recopilación de Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="e19ff-113">Configuración de Syslog</span><span class="sxs-lookup"><span data-stu-id="e19ff-113">Configuring Syslog</span></span>
<span data-ttu-id="e19ff-114">Hola agente de OMS para Linux solo recopilará eventos con instalaciones de Hola y niveles de gravedad que se especifican en su configuración.</span><span class="sxs-lookup"><span data-stu-id="e19ff-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="e19ff-115">Puede configurar Syslog a través del portal de OMS de Hola o mediante la administración de archivos de configuración en los agentes de Linux.</span><span class="sxs-lookup"><span data-stu-id="e19ff-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="e19ff-116">Configurar Syslog en portal de OMS Hola</span><span class="sxs-lookup"><span data-stu-id="e19ff-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="e19ff-117">Configurar Syslog desde hello [menú datos de configuración de análisis de registro](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="e19ff-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="e19ff-118">Esta configuración se entrega el archivo de configuración de toohello en cada agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="e19ff-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="e19ff-119">Para agregar un nuevo recurso, escriba su nombre y haga clic en **+**.</span><span class="sxs-lookup"><span data-stu-id="e19ff-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="e19ff-120">Para cada instalación, se recopilarán sólo los mensajes con una gravedad de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="e19ff-121">Comprobar los niveles de gravedad de Hola para hello equipamiento que desea toocollect.</span><span class="sxs-lookup"><span data-stu-id="e19ff-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="e19ff-122">No puede proporcionar los criterios adicionales toofilter mensajes.</span><span class="sxs-lookup"><span data-stu-id="e19ff-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Configuración de Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="e19ff-124">De forma predeterminada, todos los cambios de configuración se insertan automáticamente agentes tooall.</span><span class="sxs-lookup"><span data-stu-id="e19ff-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="e19ff-125">Si desea tooconfigure Syslog manualmente en cada agente de Linux, a continuación, desactive la casilla de hello *aplicar la siguiente máquinas de Linux de configuración toomy*.</span><span class="sxs-lookup"><span data-stu-id="e19ff-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="e19ff-126">Configuración de Syslog en agente de Linux</span><span class="sxs-lookup"><span data-stu-id="e19ff-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="e19ff-127">Cuando Hola [agente de OMS se instala en un cliente Linux](log-analytics-linux-agents.md), instala un archivo de configuración de syslog predeterminada que define la función hello y gravedad de hello los mensajes que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="e19ff-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="e19ff-128">Puede modificar este archivo de configuración de hello toochange.</span><span class="sxs-lookup"><span data-stu-id="e19ff-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="e19ff-129">archivo de configuración de Hello es diferente según Hola Syslog demonio que Hola cliente se ha instalado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="e19ff-130">Si modifica la configuración de syslog hello, debe reiniciar el demonio de syslog Hola Hola cambios tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="e19ff-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="e19ff-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="e19ff-131">rsyslog</span></span>
<span data-ttu-id="e19ff-132">Hello archivo de configuración para rsyslog se encuentra en **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="e19ff-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="e19ff-133">A continuación se muestra su contenido predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-133">Its default contents are shown below.</span></span>  <span data-ttu-id="e19ff-134">Aquí reúnen los mensajes de syslog enviados del agente local Hola para todas las instalaciones con un nivel de advertencia o superior.</span><span class="sxs-lookup"><span data-stu-id="e19ff-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="e19ff-135">Puede quitar una instalación mediante la eliminación de su sección del archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e19ff-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="e19ff-136">Puede limitar los niveles de gravedad de Hola que se recopilan para una instalación determinada mediante la modificación de la entrada de dicha instalación.</span><span class="sxs-lookup"><span data-stu-id="e19ff-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="e19ff-137">Por ejemplo, instalaciones de usuario de toolimit hello toomessages con una gravedad de error o superior modificaría esa línea de toohello de archivo de configuración de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e19ff-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="e19ff-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="e19ff-138">syslog-ng</span></span>
<span data-ttu-id="e19ff-139">archivo de configuración de Hola de syslog-ng es la ubicación en **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="e19ff-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="e19ff-140">A continuación se muestra su contenido predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-140">Its default contents are shown below.</span></span>  <span data-ttu-id="e19ff-141">Aquí reúnen enviados desde el agente local Hola para todas las utilidades y todos los niveles de gravedad de mensajes de syslog.</span><span class="sxs-lookup"><span data-stu-id="e19ff-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="e19ff-142">Puede quitar una instalación mediante la eliminación de su sección del archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e19ff-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="e19ff-143">Puede limitar los niveles de gravedad de Hola que se recopilan para una instalación determinada quitándolos de la lista.</span><span class="sxs-lookup"><span data-stu-id="e19ff-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="e19ff-144">Por ejemplo, toolimit Hola usuario facility toojust mensajes de alerta y críticos, lo haría para modificar esa sección de toohello de archivo de configuración de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e19ff-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="e19ff-145">Recopilación de datos de puertos de Syslog adicionales</span><span class="sxs-lookup"><span data-stu-id="e19ff-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="e19ff-146">agente de OMS Hola escucha los mensajes de Syslog en cliente local de hello en el puerto 25224.</span><span class="sxs-lookup"><span data-stu-id="e19ff-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="e19ff-147">Cuando se instala el agente de hello, se aplica una configuración de syslog predeterminada y se encuentra en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="e19ff-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="e19ff-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="e19ff-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="e19ff-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="e19ff-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="e19ff-150">Puede cambiar el número de puerto de hello mediante la creación de dos archivos de configuración: un archivo de configuración de FluentD y un archivo ng de rsyslog o syslog según ha instalado el demonio de Syslog de Hola.</span><span class="sxs-lookup"><span data-stu-id="e19ff-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="e19ff-151">el archivo de configuración de Hello FluentD debe ser un nuevo archivo que se encuentra en: `/etc/opt/microsoft/omsagent/conf/omsagent.d` y reemplace el valor de Hola Hola **puerto** entrada con el número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="e19ff-152">Para rsyslog, debe crear un nuevo archivo de configuración que se encuentra en: `/etc/rsyslog.d/` y reemplace Hola valor % SYSLOG_PORT % con el número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="e19ff-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="e19ff-153">Si modifica este valor en el archivo de configuración de hello `95-omsagent.conf`, se sobrescribirá al agente de Hola aplica una configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e19ff-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="e19ff-154">Hello syslog-ng config debe modificarse mediante la copia de configuración de ejemplo de Hola se muestra a continuación y agregar Hola configuración modificada personalizada toohello final del archivo de configuración de syslog ng.conf Hola ubicado en `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="e19ff-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="e19ff-155">Hacer **no** utilizar la etiqueta predeterminada de hello **% WORKSPACE_ID % _oms** o **% WORKSPACE_ID_OMS**, definir un personalizado etiqueta toohelp distinguir los cambios.</span><span class="sxs-lookup"><span data-stu-id="e19ff-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="e19ff-156">Si modifica los valores predeterminados de hello en el archivo de configuración de hello, se sobrescribirán cuando el agente de hello aplica una configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e19ff-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="e19ff-157">Después de completar los cambios de hello, Hola Syslog y Hola debe toobe reiniciar tooensure Hola configuración cambios surten efecto el servicio de agente OMS.</span><span class="sxs-lookup"><span data-stu-id="e19ff-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="e19ff-158">Propiedades de registros de Syslog</span><span class="sxs-lookup"><span data-stu-id="e19ff-158">Syslog record properties</span></span>
<span data-ttu-id="e19ff-159">Registros de syslog tienen un tipo de **Syslog** y que tienen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="e19ff-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="e19ff-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="e19ff-160">Property</span></span> | <span data-ttu-id="e19ff-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="e19ff-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e19ff-162">Equipo</span><span class="sxs-lookup"><span data-stu-id="e19ff-162">Computer</span></span> |<span data-ttu-id="e19ff-163">Equipo que Hola eventos se recopilaron de.</span><span class="sxs-lookup"><span data-stu-id="e19ff-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="e19ff-164">Facility</span><span class="sxs-lookup"><span data-stu-id="e19ff-164">Facility</span></span> |<span data-ttu-id="e19ff-165">Define la parte de hello del sistema de Hola que generó el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="e19ff-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="e19ff-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="e19ff-166">HostIP</span></span> |<span data-ttu-id="e19ff-167">Dirección IP del sistema Hola enviando mensaje de saludo.</span><span class="sxs-lookup"><span data-stu-id="e19ff-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="e19ff-168">HostName</span><span class="sxs-lookup"><span data-stu-id="e19ff-168">HostName</span></span> |<span data-ttu-id="e19ff-169">Nombre del sistema de hello enviando mensaje de saludo.</span><span class="sxs-lookup"><span data-stu-id="e19ff-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="e19ff-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="e19ff-170">SeverityLevel</span></span> |<span data-ttu-id="e19ff-171">Nivel de gravedad del evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e19ff-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="e19ff-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="e19ff-172">SyslogMessage</span></span> |<span data-ttu-id="e19ff-173">Texto del mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="e19ff-173">Text of hello message.</span></span> |
| <span data-ttu-id="e19ff-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="e19ff-174">ProcessID</span></span> |<span data-ttu-id="e19ff-175">Identificador del proceso de Hola que generó el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="e19ff-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="e19ff-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="e19ff-176">EventTime</span></span> |<span data-ttu-id="e19ff-177">Fecha y hora en que Hola eventos generó un error.</span><span class="sxs-lookup"><span data-stu-id="e19ff-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="e19ff-178">Consultas de registro con registros de Syslog</span><span class="sxs-lookup"><span data-stu-id="e19ff-178">Log queries with Syslog records</span></span>
<span data-ttu-id="e19ff-179">Hello tabla siguiente proporciona diferentes ejemplos de consultas de registro que recuperar registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="e19ff-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="e19ff-180">Consultar</span><span class="sxs-lookup"><span data-stu-id="e19ff-180">Query</span></span> | <span data-ttu-id="e19ff-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="e19ff-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e19ff-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="e19ff-182">Type=Syslog</span></span> |<span data-ttu-id="e19ff-183">Todos los registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="e19ff-183">All Syslogs.</span></span> |
| <span data-ttu-id="e19ff-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="e19ff-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="e19ff-185">Todos los registros de Syslog con gravedad de error.</span><span class="sxs-lookup"><span data-stu-id="e19ff-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="e19ff-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="e19ff-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="e19ff-187">Número de registros de Syslog por equipo.</span><span class="sxs-lookup"><span data-stu-id="e19ff-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="e19ff-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="e19ff-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="e19ff-189">Número de registros de Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="e19ff-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="e19ff-190">Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.</span><span class="sxs-lookup"><span data-stu-id="e19ff-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="e19ff-191">Consultar</span><span class="sxs-lookup"><span data-stu-id="e19ff-191">Query</span></span> | <span data-ttu-id="e19ff-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="e19ff-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e19ff-193">syslog</span><span class="sxs-lookup"><span data-stu-id="e19ff-193">Syslog</span></span> |<span data-ttu-id="e19ff-194">Todos los registros de Syslog.</span><span class="sxs-lookup"><span data-stu-id="e19ff-194">All Syslogs.</span></span> |
| <span data-ttu-id="e19ff-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="e19ff-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="e19ff-196">Todos los registros de Syslog con gravedad de error.</span><span class="sxs-lookup"><span data-stu-id="e19ff-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="e19ff-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="e19ff-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="e19ff-198">Número de registros de Syslog por equipo.</span><span class="sxs-lookup"><span data-stu-id="e19ff-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="e19ff-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="e19ff-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="e19ff-200">Número de registros de Syslog por recurso.</span><span class="sxs-lookup"><span data-stu-id="e19ff-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e19ff-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e19ff-201">Next steps</span></span>
* <span data-ttu-id="e19ff-202">Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="e19ff-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="e19ff-203">Use [campos personalizados](log-analytics-custom-fields.md) tooparse datos de registros de syslog en campos individuales.</span><span class="sxs-lookup"><span data-stu-id="e19ff-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="e19ff-204">[Configurar los agentes de Linux](log-analytics-linux-agents.md) toocollect otros tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="e19ff-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
