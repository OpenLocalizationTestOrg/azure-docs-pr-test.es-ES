---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="90504-101">Conexión de equipos con Linux a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90504-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="90504-102">El uso de Log Analytics permite recopilar y actuar sobre los datos generados en equipos Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="90504-103">Agregar datos recopilados de Linux a OMS permite administrar sistemas Linux y soluciones de contenedor como Docker, independientemente de dónde se encuentren los equipos, (prácticamente en cualquier lugar).</span><span class="sxs-lookup"><span data-stu-id="90504-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="90504-104">Esos orígenes de datos pueden residir en su centro de datos local como servidores físicos, en equipos virtuales en un servicio hospedado en la nube como Amazon Web Services (AWS) o Microsoft Azure, o incluso en el equipo portátil en su escritorio.</span><span class="sxs-lookup"><span data-stu-id="90504-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="90504-105">Además, OMS también recopila datos de los equipos de Windows de forma similar, por lo que es compatible con un entorno informático realmente híbrido.</span><span class="sxs-lookup"><span data-stu-id="90504-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="90504-106">Puede ver y administrar los datos de todos esos orígenes con Log Analytics en OMS con un portal de administración único.</span><span class="sxs-lookup"><span data-stu-id="90504-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="90504-107">Esto reduce la necesidad de supervisar usando varios sistemas distintos, simplifica su uso y le permite exportar cualquier dato que desee a cualquier solución de análisis de negocio o sistema que ya tenga.</span><span class="sxs-lookup"><span data-stu-id="90504-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="90504-108">Este artículo es una guía de inicio rápido que le ayudará a recopilar y administrar los datos de los equipos de Linux mediante el agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="90504-109">Si desea obtener más detalles técnicos, como la configuración del servidor proxy, información acerca de las métricas de CollectD y orígenes de datos JSON personalizados, encontrará esa información en la [información general sobre el agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) y la [documentación completa sobre el agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="90504-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="90504-110">Actualmente puede recopilar los siguientes tipos de datos de equipos Linux:</span><span class="sxs-lookup"><span data-stu-id="90504-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="90504-111">Métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="90504-111">Performance metrics</span></span>
* <span data-ttu-id="90504-112">Eventos Syslog</span><span class="sxs-lookup"><span data-stu-id="90504-112">Syslog events</span></span>
* <span data-ttu-id="90504-113">Alertas de Nagios y Zabbix</span><span class="sxs-lookup"><span data-stu-id="90504-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="90504-114">Registros, inventario y métricas de rendimiento del contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="90504-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="90504-115">Versiones de Linux compatibles</span><span class="sxs-lookup"><span data-stu-id="90504-115">Supported Linux versions</span></span>
<span data-ttu-id="90504-116">Tanto la versión x86 como la x64 son compatibles oficialmente en una variedad de distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="90504-117">Aunque también se puede ejecutar el agente de OMS para Linux en otras distribuciones que no se enumeran.</span><span class="sxs-lookup"><span data-stu-id="90504-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="90504-118">Amazon Linux 2012.09 hasta 2015.09</span><span class="sxs-lookup"><span data-stu-id="90504-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="90504-119">CentOS Linux 5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="90504-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="90504-120">Oracle Linux 5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="90504-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="90504-121">Red Hat Enterprise Linux Server 5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="90504-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="90504-122">Debian GNU/Linux 6, 7 y 8</span><span class="sxs-lookup"><span data-stu-id="90504-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="90504-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="90504-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="90504-124">SUSE Linux Enterprise Server 11 y 12</span><span class="sxs-lookup"><span data-stu-id="90504-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="90504-125">Agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="90504-125">OMS Agent for Linux</span></span>
<span data-ttu-id="90504-126">El agente de Operations Management Suite para Linux consta de varios paquetes.</span><span class="sxs-lookup"><span data-stu-id="90504-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="90504-127">El archivo de versión contiene los siguientes paquetes disponibles mediante la ejecución de la agrupación de shell con `--extract`.</span><span class="sxs-lookup"><span data-stu-id="90504-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="90504-128">**Paquete**</span><span class="sxs-lookup"><span data-stu-id="90504-128">**Package**</span></span> | <span data-ttu-id="90504-129">**Versión**</span><span class="sxs-lookup"><span data-stu-id="90504-129">**Version**</span></span> | <span data-ttu-id="90504-130">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="90504-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90504-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="90504-131">omsagent</span></span> |<span data-ttu-id="90504-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="90504-132">1.1.0</span></span> |<span data-ttu-id="90504-133">El agente de Operations Management Suite para Linux</span><span class="sxs-lookup"><span data-stu-id="90504-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="90504-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="90504-134">omsconfig</span></span> |<span data-ttu-id="90504-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="90504-135">1.1.1</span></span> |<span data-ttu-id="90504-136">Agente de configuración para el agente de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="90504-137">omi</span><span class="sxs-lookup"><span data-stu-id="90504-137">omi</span></span> |<span data-ttu-id="90504-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="90504-138">1.0.8.3</span></span> |<span data-ttu-id="90504-139">Infraestructura de administración abierta (OMI), un servidor de CIM ligero</span><span class="sxs-lookup"><span data-stu-id="90504-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="90504-140">scx</span><span class="sxs-lookup"><span data-stu-id="90504-140">scx</span></span> |<span data-ttu-id="90504-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="90504-141">1.6.2</span></span> |<span data-ttu-id="90504-142">Proveedores de CIM OMI para métricas de rendimiento del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="90504-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="90504-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="90504-143">apache-cimprov</span></span> |<span data-ttu-id="90504-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="90504-144">1.0.0</span></span> |<span data-ttu-id="90504-145">Proveedor de supervisión de rendimiento de servidor HTTP de Apache para OMI.</span><span class="sxs-lookup"><span data-stu-id="90504-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="90504-146">Solo se instala si se detecta un servidor HTTP de Apache.</span><span class="sxs-lookup"><span data-stu-id="90504-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="90504-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="90504-147">mysql-cimprov</span></span> |<span data-ttu-id="90504-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="90504-148">1.0.0</span></span> |<span data-ttu-id="90504-149">Proveedor de supervisión de rendimiento de servidor MySQL Server para OMI.</span><span class="sxs-lookup"><span data-stu-id="90504-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="90504-150">Solo se instala si se detecta un servidor MySQL/MariaDB de Apache.</span><span class="sxs-lookup"><span data-stu-id="90504-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="90504-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="90504-151">docker-cimprov</span></span> |<span data-ttu-id="90504-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="90504-152">0.1.0</span></span> |<span data-ttu-id="90504-153">Proveedor de Docker para OMI.</span><span class="sxs-lookup"><span data-stu-id="90504-153">Docker provider for OMI.</span></span> <span data-ttu-id="90504-154">Solo se instala si se detecta Docker.</span><span class="sxs-lookup"><span data-stu-id="90504-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="90504-155">Artefactos de instalación adicionales</span><span class="sxs-lookup"><span data-stu-id="90504-155">Additional installation artifacts</span></span>
<span data-ttu-id="90504-156">Después de instalar al agente de OMS para los paquetes de Linux, se aplican los siguientes cambios de configuración adicionales a todo el sistema.</span><span class="sxs-lookup"><span data-stu-id="90504-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="90504-157">Estos artefactos se quitan cuando se desinstala el paquete omsagent.</span><span class="sxs-lookup"><span data-stu-id="90504-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="90504-158">Se crea un usuario sin privilegios llamado: `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="90504-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="90504-159">Esta es la cuenta que el demonio omsagent usa para ejecutarse</span><span class="sxs-lookup"><span data-stu-id="90504-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="90504-160">Se crea un archivo "include" de sudoers en /etc/sudoers.d/omsagent Esto autoriza a omsagent a reiniciar los demonios Syslog y omsagent.</span><span class="sxs-lookup"><span data-stu-id="90504-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="90504-161">Si no se admiten directivas "incluir" de sudo en la versión instalada de sudo, estas entradas se escribirá en /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="90504-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="90504-162">Se modifica la configuración de Syslog para reenviar un subconjunto de eventos al agente.</span><span class="sxs-lookup"><span data-stu-id="90504-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="90504-163">Para más información consulte la sección sobre **configuración de recopilación de datos** a continuación</span><span class="sxs-lookup"><span data-stu-id="90504-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="90504-164">Detalles de la recopilación de datos de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-164">Linux data collection details</span></span>
<span data-ttu-id="90504-165">La siguiente tabla muestra los métodos de recolección de datos y otros detalles acerca de cómo se recopilan los datos.</span><span class="sxs-lookup"><span data-stu-id="90504-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="90504-166">de origen</span><span class="sxs-lookup"><span data-stu-id="90504-166">source</span></span> | <span data-ttu-id="90504-167">Agente directo</span><span class="sxs-lookup"><span data-stu-id="90504-167">Direct Agent</span></span> | <span data-ttu-id="90504-168">Agente de SCOM</span><span class="sxs-lookup"><span data-stu-id="90504-168">SCOM agent</span></span> | <span data-ttu-id="90504-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="90504-169">Azure Storage</span></span> | <span data-ttu-id="90504-170">¿Se necesita SCOM?</span><span class="sxs-lookup"><span data-stu-id="90504-170">SCOM required?</span></span> | <span data-ttu-id="90504-171">Datos del agente de SCOM enviados a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="90504-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="90504-172">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="90504-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="90504-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="90504-173">Zabbix</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="90504-179">1 minuto</span><span class="sxs-lookup"><span data-stu-id="90504-179">1 minute</span></span> |
| <span data-ttu-id="90504-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="90504-180">Nagios</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="90504-186">a la llegada</span><span class="sxs-lookup"><span data-stu-id="90504-186">on arrival</span></span> |
| <span data-ttu-id="90504-187">syslog</span><span class="sxs-lookup"><span data-stu-id="90504-187">syslog</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="90504-193">De Almacenamiento de Azure: 10 minutos; del agente: a la llegada</span><span class="sxs-lookup"><span data-stu-id="90504-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="90504-194">Contadores de rendimiento de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-194">Linux performance counters</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="90504-200">Mínimo de 10 segundos, según lo programado</span><span class="sxs-lookup"><span data-stu-id="90504-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="90504-201">Seguimiento de cambios</span><span class="sxs-lookup"><span data-stu-id="90504-201">change tracking</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="90504-207">Cada hora</span><span class="sxs-lookup"><span data-stu-id="90504-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="90504-208">Requisitos de paquete</span><span class="sxs-lookup"><span data-stu-id="90504-208">Package Requirements</span></span>
| <span data-ttu-id="90504-209">**Paquetes necesarios**</span><span class="sxs-lookup"><span data-stu-id="90504-209">**Required package**</span></span> | <span data-ttu-id="90504-210">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="90504-210">**Description**</span></span> | <span data-ttu-id="90504-211">**Versión mínima**</span><span class="sxs-lookup"><span data-stu-id="90504-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90504-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="90504-212">Glibc</span></span> |<span data-ttu-id="90504-213">Biblioteca GNU C</span><span class="sxs-lookup"><span data-stu-id="90504-213">GNU C library</span></span> |<span data-ttu-id="90504-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="90504-214">2.5-12</span></span> |
| <span data-ttu-id="90504-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="90504-215">Openssl</span></span> |<span data-ttu-id="90504-216">Bibliotecas OpenSSL</span><span class="sxs-lookup"><span data-stu-id="90504-216">OpenSSL libraries</span></span> |<span data-ttu-id="90504-217">0.9.8E o 1.0</span><span class="sxs-lookup"><span data-stu-id="90504-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="90504-218">Curl</span><span class="sxs-lookup"><span data-stu-id="90504-218">Curl</span></span> |<span data-ttu-id="90504-219">Cliente web de cURL</span><span class="sxs-lookup"><span data-stu-id="90504-219">cURL web client</span></span> |<span data-ttu-id="90504-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="90504-220">7.15.5</span></span> |
| <span data-ttu-id="90504-221">Python ctypes</span><span class="sxs-lookup"><span data-stu-id="90504-221">Python-ctypes</span></span> |<span data-ttu-id="90504-222">Bibliotecas de funciones</span><span class="sxs-lookup"><span data-stu-id="90504-222">function libraries</span></span> |<span data-ttu-id="90504-223">N/D</span><span class="sxs-lookup"><span data-stu-id="90504-223">n/a</span></span> |
| <span data-ttu-id="90504-224">PAM</span><span class="sxs-lookup"><span data-stu-id="90504-224">PAM</span></span> |<span data-ttu-id="90504-225">Módulos de autenticación conectables</span><span class="sxs-lookup"><span data-stu-id="90504-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="90504-226">N/D</span><span class="sxs-lookup"><span data-stu-id="90504-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="90504-227">Rsyslog o Syslog son necesarios para recopilar mensajes de Syslog.</span><span class="sxs-lookup"><span data-stu-id="90504-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="90504-228">El demonio predeterminado de Syslog en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (Sysklog) no se admite para la recopilación de eventos de Syslog.</span><span class="sxs-lookup"><span data-stu-id="90504-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="90504-229">Para recopilar datos de Syslog de esta versión de estas distribuciones, es necesario instalar configurar el demonio de Rsyslog para reemplazar Sysklog.</span><span class="sxs-lookup"><span data-stu-id="90504-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="90504-230">Instalación rápida</span><span class="sxs-lookup"><span data-stu-id="90504-230">Quick install</span></span>
<span data-ttu-id="90504-231">Ejecute los siguientes comandos para descargar omsagent, validar la suma de comprobación e instalar e incorporar el agente.</span><span class="sxs-lookup"><span data-stu-id="90504-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="90504-232">Los comandos son para 64 bits.</span><span class="sxs-lookup"><span data-stu-id="90504-232">Commands are for 64-bit.</span></span> <span data-ttu-id="90504-233">El identificador de área de trabajo y la clave principal se encuentran en el portal de OMS en **Configuración** en la pestaña **Orígenes conectados**.</span><span class="sxs-lookup"><span data-stu-id="90504-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![detalles de área de trabajo](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="90504-235">Hay una variedad de otros métodos para instalar al agente y actualizarlo.</span><span class="sxs-lookup"><span data-stu-id="90504-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="90504-236">Puede leer más sobre ellas en [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux)(Pasos para instalar el agente de OMS para Linux).</span><span class="sxs-lookup"><span data-stu-id="90504-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="90504-237">También puede ver el [tutorial en vídeo sobre Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="90504-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="90504-238">Selección del método de recopilación de datos de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="90504-239">La forma de elegir los tipos de datos que desea recopilar depende de si desea usar el portal OMS o si quier editar varios archivos de configuración directamente en los clientes de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="90504-240">Si elige usar el portal, la configuración se envía automáticamente a todos sus clientes de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="90504-241">Si necesita diferentes configuraciones para distintos clientes de Linux, tendrá que editar los archivos de cliente individualmente, o usar una alternativa como PowerShell DSC, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="90504-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="90504-242">Puede especificar los eventos de Syslog y los contadores de rendimiento que quiere recopilar mediante los archivos de configuración en los equipos de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="90504-243">*Si decide configurar la recopilación de datos editando los archivos de configuración del agente, debe deshabilitar la configuración centralizada.*</span><span class="sxs-lookup"><span data-stu-id="90504-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="90504-244">A continuación se proporcionan instrucciones para configurar la recopilación de datos en los archivos de configuración del agente, así como para deshabilitar la configuración central para todos los agentes de OMS para Linux o equipos individuales.</span><span class="sxs-lookup"><span data-stu-id="90504-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="90504-245">Deshabilitación de la administración de OMS para un equipo individual de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="90504-246">La recopilación de datos centralizada para datos de configuración se deshabilita para un equipo individual de Linux con el script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="90504-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="90504-247">Esto puede ser útil si un subconjunto de equipos debe tener una configuración especializada.</span><span class="sxs-lookup"><span data-stu-id="90504-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="90504-248">Para deshabilitar la configuración centralizada:</span><span class="sxs-lookup"><span data-stu-id="90504-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="90504-249">Para volver a habilitar la configuración centralizada:</span><span class="sxs-lookup"><span data-stu-id="90504-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="90504-250">Contadores de rendimiento de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-250">Linux performance counters</span></span>
<span data-ttu-id="90504-251">Los contadores de rendimiento de Linux son similares a los contadores de rendimiento de Windows, ambos funcionan de forma parecida.</span><span class="sxs-lookup"><span data-stu-id="90504-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="90504-252">Puede utilizar los siguientes procedimientos para agregarlos y configurarlos.</span><span class="sxs-lookup"><span data-stu-id="90504-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="90504-253">Una vez que se agregan a OMS, sus datos se recopilan cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="90504-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="90504-254">Para agregar un contador de rendimiento de Linux en OMS</span><span class="sxs-lookup"><span data-stu-id="90504-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="90504-255">Para configurar agentes de OMS para Linux mediante el portal de OMS, puede agregar contadores de rendimiento de Linux en la página Configuración, haga clic en **Datos**.</span><span class="sxs-lookup"><span data-stu-id="90504-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="90504-256">En la página **Configuración** en **Datos**, haga clic en **Contadores de rendimiento de Linux** y seleccione o escriba el nombre del contador que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="90504-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="90504-257">![Datos](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="90504-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="90504-258">Si no sabe el nombre completo del contador, puede empezar a escribir un nombre parcial y aparecerá una lista de contadores disponibles.</span><span class="sxs-lookup"><span data-stu-id="90504-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="90504-259">Cuando encuentre el contador que desea agregar, haga clic en el nombre de la lista y luego haga clic en el icono del signo más para agregarlo.</span><span class="sxs-lookup"><span data-stu-id="90504-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="90504-260">Después de agregar el contador, este aparece en la lista de contadores resaltado con una barra de color.</span><span class="sxs-lookup"><span data-stu-id="90504-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="90504-261">De forma predeterminada, la opción **Apply below configuration to my machines** (Aplicar la siguiente configuración a mis equipos) está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="90504-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="90504-262">Si desea deshabilitar el envío de datos de configuración, anule la selección.</span><span class="sxs-lookup"><span data-stu-id="90504-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="90504-263">Cuando haya terminado de modificar los contadores de rendimiento, en la parte inferior de la página, haga clic en **Guardar** para finalizar los cambios.</span><span class="sxs-lookup"><span data-stu-id="90504-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="90504-264">Los cambios de configuración realizados se envían a todos los agentes de OMS para Linux que están registrados en OMS, normalmente en un máximo de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="90504-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="90504-265">Configuración de los contadores de rendimiento de Linux en OMS</span><span class="sxs-lookup"><span data-stu-id="90504-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="90504-266">Para los contadores de rendimiento de Windows, puede elegir una instancia específica para cada contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="90504-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="90504-267">Sin embargo, para los contadores de rendimiento de Linux, cualquier instancia de un contador que elija se aplica a todos los contadores secundarios del contador primario.</span><span class="sxs-lookup"><span data-stu-id="90504-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="90504-268">La siguiente tabla muestra las instancias comunes disponibles para los contadores de rendimiento de Windows y de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="90504-269">**Nombre de la instancia**</span><span class="sxs-lookup"><span data-stu-id="90504-269">**Instance name**</span></span> | <span data-ttu-id="90504-270">**Significado**</span><span class="sxs-lookup"><span data-stu-id="90504-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="90504-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="90504-271">\_Total</span></span> |<span data-ttu-id="90504-272">Total de todas las instancias</span><span class="sxs-lookup"><span data-stu-id="90504-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="90504-273">Todas las instancias</span><span class="sxs-lookup"><span data-stu-id="90504-273">All instances</span></span> |
| <span data-ttu-id="90504-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="90504-274">(/&#124;/var)</span></span> |<span data-ttu-id="90504-275">Coincide con las instancias con nombre: / o /var</span><span class="sxs-lookup"><span data-stu-id="90504-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="90504-276">De forma similar, el intervalo de muestra que elija para un contador primario se aplica a todos sus contadores secundarios.</span><span class="sxs-lookup"><span data-stu-id="90504-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="90504-277">En otras palabras, todos los intervalos de muestra y las instancias del contador secundario están vinculadas entre sí.</span><span class="sxs-lookup"><span data-stu-id="90504-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="90504-278">Incorporación y configuración de las métricas de rendimiento con Linux</span><span class="sxs-lookup"><span data-stu-id="90504-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="90504-279">Las métricas de rendimiento que se recopilan se controlan según la configuración que aparece en /etc/opt/microsoft/omsagent/&lt;identificador de área de trabajo&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="90504-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="90504-280">Consulte [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) (Métricas de rendimiento disponibles) para ver las clases disponibles y las métricas para el agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="90504-281">Cada objeto, o categoría, de métricas de rendimiento para recopilar debe definirse en el archivo de configuración como un solo elemento `<source>` .</span><span class="sxs-lookup"><span data-stu-id="90504-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="90504-282">La sintaxis sigue el modelo siguiente.</span><span class="sxs-lookup"><span data-stu-id="90504-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="90504-283">Los parámetros configurables de este elemento son:</span><span class="sxs-lookup"><span data-stu-id="90504-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="90504-284">**Object\_name**: el nombre de objeto de la colección.</span><span class="sxs-lookup"><span data-stu-id="90504-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="90504-285">**Instance\_regex**: una *expresión regular* que define las instancias que desea recopilar.</span><span class="sxs-lookup"><span data-stu-id="90504-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="90504-286">El valor: `.*` especifica todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="90504-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="90504-287">Para recopilar métricas de procesador solamente de la instancia \_Total, puede especificar `_Total`.</span><span class="sxs-lookup"><span data-stu-id="90504-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="90504-288">Para recopilar métricas de procesamiento solamente de las instancias rond o sshd, puede especificar `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="90504-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="90504-289">**Counter\_name\_regex**: una *expresión regular* que define los contadores (para el objeto) que desea recopilar.</span><span class="sxs-lookup"><span data-stu-id="90504-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="90504-290">Para recopilar todos los contadores para el objeto, especifique: `.*`.</span><span class="sxs-lookup"><span data-stu-id="90504-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="90504-291">Para recopilar solo contadores de espacio de intercambio para el objeto de memoria, puede especificar: `.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="90504-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="90504-292">**Intervalo:**: la frecuencia con la que se recopilan los contadores del objeto.</span><span class="sxs-lookup"><span data-stu-id="90504-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="90504-293">La configuración predeterminada para las métricas de rendimiento es:</span><span class="sxs-lookup"><span data-stu-id="90504-293">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="90504-294">Habilitación de los contadores de rendimiento de MySQL mediante comandos de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="90504-295">Si se detecta en el equipo un servidor de MySQL o de MariaDB cuando se instala la agrupación de omsagent, se instalará automáticamente un proveedor de supervisión de rendimiento para el servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="90504-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="90504-296">Este proveedor se conecta al servidor MySQL o MariaDB local para exponer las estadísticas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="90504-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="90504-297">Tiene que configurar las credenciales de usuario de MySQL para que el proveedor pueda tener acceso al servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="90504-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="90504-298">Para definir una cuenta de usuario predeterminada para el servidor MySQL en localhost, utilice el siguiente ejemplo de comando.</span><span class="sxs-lookup"><span data-stu-id="90504-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="90504-299">El archivo de credenciales tiene que ser legible para la cuenta omsagent.</span><span class="sxs-lookup"><span data-stu-id="90504-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="90504-300">Se recomienda ejecutar el comando mycimprovauth como omsgent.</span><span class="sxs-lookup"><span data-stu-id="90504-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="90504-301">Como alternativa, puede especificar las credenciales necesarias de MySQL en un archivo creando el archivo: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span><span class="sxs-lookup"><span data-stu-id="90504-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="90504-302">Para más información acerca de cómo administrar las credenciales de MySQL para la supervisión a través del archivo mysql-auth, consulte [Administración de las credenciales de supervisión de MySQL en el archivo de autenticación](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="90504-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="90504-303">Consulte [Permisos necesarios de la base de datos para los contadores de rendimiento de MySQL](#database-permissions-required-for-mysql-performance-counters) para más detalles acerca de los permisos de objeto requeridos por el usuario de MySQL para recopilar datos de rendimiento de MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="90504-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="90504-304">Habilitación de los contadores de rendimiento del servidor HTTP de Apache mediante comandos de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="90504-305">Si se detecta en el equipo un servidor HTTP de Apache cuando se instala la agrupación de omsagent, se instalará automáticamente un proveedor de supervisión de rendimiento para el servidor HTTP de Apache.</span><span class="sxs-lookup"><span data-stu-id="90504-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="90504-306">Este proveedor se basa en un "módulo" de Apache que se tiene que cargar en el servidor HTTP de Apache para tener acceso a los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="90504-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="90504-307">Puede cargar el módulo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90504-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="90504-308">Para cargar el módulo de supervisión de Apache, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90504-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="90504-309">Visualización de los datos de rendimiento con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90504-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="90504-310">En el portal de Operations Management Suite, haga clic en el icono de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="90504-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="90504-311">En la barra de búsqueda, escriba `* (Type=Perf)` para ver todos los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="90504-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="90504-312">Como OMS también recopila datos del contador de rendimiento de Windows, debe restringir el alcance de los resultados de la búsqueda a los datos específicos de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="90504-313">Así en el ejemplo siguiente se muestran los datos de rendimiento específicos de un servidor Linux de ejemplo denominado Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="90504-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![servidor de ejemplo que se muestra en los resultados de búsqueda](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="90504-315">En los resultados, haga clic en **Métricas** para ver los contadores para los que se recopilaron los datos.</span><span class="sxs-lookup"><span data-stu-id="90504-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="90504-316">Se muestran los datos en tiempo real como gráficos para cada contador.</span><span class="sxs-lookup"><span data-stu-id="90504-316">Real-time data is shown as graphs for each counter.</span></span>

![Métricas](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="90504-318">syslog</span><span class="sxs-lookup"><span data-stu-id="90504-318">Syslog</span></span>
<span data-ttu-id="90504-319">Syslog es un protocolo de registro de eventos similar a los registros de eventos de Windows, ambos funcionan de forma parecida al mostrarlos en OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="90504-320">Incorporación de una nueva utilidad Syslog de Linux en OMS</span><span class="sxs-lookup"><span data-stu-id="90504-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="90504-321">En la página **Configuración** en **Datos**, haga clic en **Syslog** y escriba a la izquierda del icono del signo más el nombre de la utilidad Syslog que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="90504-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="90504-322">![Syslog de Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="90504-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="90504-323">Si no sabe el nombre completo de la utilidad, puede empezar a escribir un nombre parcial y aparecerá una lista de utilidades Syslog disponibles.</span><span class="sxs-lookup"><span data-stu-id="90504-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="90504-324">Cuando encuentre la utilidad que desea agregar, haga clic en el nombre de la lista y luego haga clic en el icono del signo más para agregarla.</span><span class="sxs-lookup"><span data-stu-id="90504-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="90504-325">Después de agregar la utilidad, esta aparece en la lista de utilidades de Syslog resaltada con una barra de color.</span><span class="sxs-lookup"><span data-stu-id="90504-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="90504-326">A continuación, seleccione los niveles de gravedad (categorías de información de la utilidad de Syslog) que se van a recopilar.</span><span class="sxs-lookup"><span data-stu-id="90504-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="90504-327">Para finalizar los cambios, haga clic en **Guardar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="90504-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="90504-328">Los cambios de configuración realizados se envían a todos los agentes de OMS para Linux que están registrados en OMS, normalmente en un máximo de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="90504-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="90504-329">Configuración de las utilidades de Syslog de Linux en Linux</span><span class="sxs-lookup"><span data-stu-id="90504-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="90504-330">Los eventos Syslog se envían desde el demonio Syslog, por ejemplo Rsyslog o Syslog-ng, a un puerto local en el que el agente está escuchando.</span><span class="sxs-lookup"><span data-stu-id="90504-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="90504-331">De forma predeterminada al puerto 25224.</span><span class="sxs-lookup"><span data-stu-id="90504-331">By default, port 25224.</span></span> <span data-ttu-id="90504-332">Cuando se instala el agente, se aplica una configuración de Syslog predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90504-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="90504-333">Esto se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="90504-333">This is found at:</span></span>

<span data-ttu-id="90504-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="90504-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="90504-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="90504-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="90504-336">La configuración predeterminada de Syslog del agente de OMS carga eventos Syslog desde todas las utilidades con una gravedad de advertencia o superior.</span><span class="sxs-lookup"><span data-stu-id="90504-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="90504-337">Si modifica la configuración de Syslog, tiene que reiniciar el demonio Syslog para que los cambios surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="90504-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="90504-338">La configuración predeterminada de Syslog para el agente de OMS para Linux para OMS es:</span><span class="sxs-lookup"><span data-stu-id="90504-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="90504-339">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="90504-339">Rsyslog</span></span>
```
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
```

#### <a name="syslog-ng"></a><span data-ttu-id="90504-340">Syslog ng</span><span class="sxs-lookup"><span data-stu-id="90504-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="90504-341">Visualización de todos los eventos de Syslog con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90504-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="90504-342">En el portal de Operations Management Suite, haga clic en el icono de **búsqueda de registros** .</span><span class="sxs-lookup"><span data-stu-id="90504-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="90504-343">En la agrupación **Log Management** (administración de registros), elija una búsqueda predefinida de Syslog y selecciónela para ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="90504-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="90504-344">Este ejemplo muestra todos los eventos de Syslog.</span><span class="sxs-lookup"><span data-stu-id="90504-344">This example shows all Syslog events.</span></span>

![Eventos de Syslog que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="90504-346">Ahora puede profundizar en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="90504-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="90504-347">Alertas de Linux</span><span class="sxs-lookup"><span data-stu-id="90504-347">Linux alerts</span></span>
<span data-ttu-id="90504-348">Si utiliza Nagios o Zabbix para administrar los equipos Linux, OMS puede recibir las alertas generadas desde esas herramientas.</span><span class="sxs-lookup"><span data-stu-id="90504-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="90504-349">Sin embargo, en la actualidad no hay ningún método para configurar los datos entrantes de la alerta usando el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="90504-350">En su lugar, tendrá que modificar un archivo de configuración para empezar a enviar alertas a OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="90504-351">Recopilación de alertas de Nagios</span><span class="sxs-lookup"><span data-stu-id="90504-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="90504-352">Para recopilar las alertas de un servidor Nagios, tiene que realizar los siguientes cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="90504-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="90504-353">Conceda al usuario **omsagent** acceso de lectura al archivo de registro Nagios (es decir, /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="90504-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="90504-354">Suponiendo que el archivo nagios.log es propiedad del grupo **nagios**, puede agregar al usuario **omsagent** al grupo **nagios**.</span><span class="sxs-lookup"><span data-stu-id="90504-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="90504-355">Modifique el archivo de configuración omsagent.conf (/etc/opt/microsoft/omsagent/&lt;identificador de área de trabajo&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="90504-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="90504-356">Asegúrese de que las entradas siguientes están presentes y no comentadas:</span><span class="sxs-lookup"><span data-stu-id="90504-356">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="90504-357">Reinicie el demonio de omsagent:</span><span class="sxs-lookup"><span data-stu-id="90504-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="90504-358">Recopilación de alertas de Zabbix</span><span class="sxs-lookup"><span data-stu-id="90504-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="90504-359">Para recopilar las alertas de un servidor Zabbix, tendrá que llevar cabo pasos similares a los que se han expuesto para Nagios, excepto que aquí tendrá que especificar un usuario y una contraseña *sin cifrar*.</span><span class="sxs-lookup"><span data-stu-id="90504-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="90504-360">No es una solución ideal, pero seguramente cambiará pronto.</span><span class="sxs-lookup"><span data-stu-id="90504-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="90504-361">Para solucionar este problema, recomendamos que cree el usuario y le conceda permiso solamente para supervisar.</span><span class="sxs-lookup"><span data-stu-id="90504-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="90504-362">Una sección de ejemplo del archivo de configuración omsagent.conf (/etc/opt/microsoft/omsagent/&lt;identificador de área de trabajo&gt;/conf/omsagent.conf) para Zabbix debería parecerse a esto:</span><span class="sxs-lookup"><span data-stu-id="90504-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="90504-363">Visualización de alertas en búsqueda de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90504-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="90504-364">Después de configurar los equipos Linux para enviar alertas a OMS, puede utilizar algunas simples consultas de búsqueda de registro para ver las alertas.</span><span class="sxs-lookup"><span data-stu-id="90504-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="90504-365">El siguiente ejemplo de consulta de búsqueda devuelve todas las alertas grabadas que se generaron.</span><span class="sxs-lookup"><span data-stu-id="90504-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="90504-366">Por ejemplo, si se produce algún tipo de problema en su infraestructura de TI, los resultados de la consulta del ejemplo siguiente podrían indicar en dónde se ha originado el problema.</span><span class="sxs-lookup"><span data-stu-id="90504-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="90504-367">Y puede fácilmente profundizar las alertas por sistema de origen para ayudarle a acotar su investigación.</span><span class="sxs-lookup"><span data-stu-id="90504-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="90504-368">La ventaja es que no tiene necesariamente que ir a varios sistemas de administración desde el principio, siempre que las alertas se envíen a OMS, puede empezar por ahí.</span><span class="sxs-lookup"><span data-stu-id="90504-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="90504-369">Visualización de todas las alertas de Nagios con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90504-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="90504-370">En el portal de Operations Management Suite, haga clic en el icono de **búsqueda de registros** .</span><span class="sxs-lookup"><span data-stu-id="90504-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="90504-371">En la barra de consulta, escriba la siguiente consulta de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="90504-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertas de Nagios que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="90504-373">Después de ver los resultados de la búsqueda, puede profundizar en los detalles adicionales como el elemento *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="90504-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="90504-374">Visualización de todas las alertas de Zabbix con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90504-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="90504-375">En el portal de Operations Management Suite, haga clic en el icono de **búsqueda de registros** .</span><span class="sxs-lookup"><span data-stu-id="90504-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="90504-376">En la barra de consulta, escriba la siguiente consulta de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="90504-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertas de Zabbix que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="90504-378">Después de ver los resultados de la búsqueda, puede profundizar en los detalles adicionales como el elemento *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="90504-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="90504-379">Compatibilidad con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="90504-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="90504-380">El agente de OMS para Linux comparte archivos binarios del agente con el agente de System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="90504-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="90504-381">Instalar al agente de OMS para Linux en un sistema que está administrado por Operations Manager actualiza los paquetes OMI y SCX en el equipo a una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="90504-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="90504-382">El agente de OMS para Linux y System Center 2012 R2 son compatibles.</span><span class="sxs-lookup"><span data-stu-id="90504-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="90504-383">Sin embargo, **System Center 2012 SP1 y las versiones anteriores no son compatibles ni están admitidas en la actualidad por el agente de OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="90504-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="90504-384">Si el agente de OMS para Linux se instala en un equipo que no está administrado actualmente por Operations Manager y posteriormente desea administrar el equipo con Operations Manager, tiene que modificar la configuración de OMI antes de detectar el equipo.</span><span class="sxs-lookup"><span data-stu-id="90504-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="90504-385">**Este paso no es necesario si está instalado el agente Operations Manager antes que el agente de OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="90504-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="90504-386">Habilitación del agente de OMS para Linux para comunicarse con Operations Manager</span><span class="sxs-lookup"><span data-stu-id="90504-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="90504-387">Editar el archivo /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="90504-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="90504-388">Asegúrese de que la línea que comienza con **httpsport =** define el puerto 1270.</span><span class="sxs-lookup"><span data-stu-id="90504-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="90504-389">Por ejemplo `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="90504-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="90504-390">Reinicie el servidor OMI:</span><span class="sxs-lookup"><span data-stu-id="90504-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="90504-391">Permisos necesarios de la base de datos para los contadores de rendimiento de MySQL</span><span class="sxs-lookup"><span data-stu-id="90504-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="90504-392">Para conceder permisos a un usuario de supervisión de MySQL, el usuario que concede el permiso tiene que tener el privilegio 'GRANT option', además del privilegio que se va a conceder.</span><span class="sxs-lookup"><span data-stu-id="90504-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="90504-393">Para que el usuario de MySQL devuelva los datos de rendimiento el usuario tendrá acceso a las siguientes consultas:</span><span class="sxs-lookup"><span data-stu-id="90504-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="90504-394">Además de estas consultas el usuario de MySQL necesita el acceso SELECT a las siguientes tablas predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="90504-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="90504-395">information_schema</span><span class="sxs-lookup"><span data-stu-id="90504-395">information_schema</span></span>
* <span data-ttu-id="90504-396">mysql</span><span class="sxs-lookup"><span data-stu-id="90504-396">mysql</span></span>

<span data-ttu-id="90504-397">Estos privilegios se pueden conceder ejecutando los siguientes comandos de concesión.</span><span class="sxs-lookup"><span data-stu-id="90504-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="90504-398">Administración de las credenciales de supervisión de MySQL en el archivo de autenticación</span><span class="sxs-lookup"><span data-stu-id="90504-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="90504-399">Las secciones siguientes le ayudan a administrar las credenciales de MySQL.</span><span class="sxs-lookup"><span data-stu-id="90504-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="90504-400">Configuración del proveedor de MySQL para OMI</span><span class="sxs-lookup"><span data-stu-id="90504-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="90504-401">El proveedor de MySQL para OMI necesita un usuario de MySQL preconfigurado y bibliotecas de cliente de MySQL instaladas para consultar la información de rendimiento y mantenimiento de la instancia de MySQL.</span><span class="sxs-lookup"><span data-stu-id="90504-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="90504-402">Archivo de autenticación de MySQL para OMI</span><span class="sxs-lookup"><span data-stu-id="90504-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="90504-403">El proveedor de MySQL OMI utiliza un archivo de autenticación para determinar la dirección de enlace y el puerto que usa la instancia de MySQL para escuchar y las credenciales que tiene que usar para recopilar métricas.</span><span class="sxs-lookup"><span data-stu-id="90504-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="90504-404">Durante la instalación el proveedor de MySQL para OMI examinará los archivos de configuración de my.cnf (ubicaciones predeterminadas) para encontrar la dirección de enlace y el puerto, y establecer parcialmente el archivo de autenticación de MySQL para OMI.</span><span class="sxs-lookup"><span data-stu-id="90504-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="90504-405">Para completar la supervisión de una instancia del servidor de MySQL, agregue un archivo de autenticación pregenerado de MySQL para OMI en el directorio correcto.</span><span class="sxs-lookup"><span data-stu-id="90504-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="90504-406">Formato del archivo de autenticación</span><span class="sxs-lookup"><span data-stu-id="90504-406">Authentication file format</span></span>
<span data-ttu-id="90504-407">El archivo de autenticación de MySQL para OMI es un archivo de texto que contiene información sobre:</span><span class="sxs-lookup"><span data-stu-id="90504-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="90504-408">Port</span><span class="sxs-lookup"><span data-stu-id="90504-408">Port</span></span>
* <span data-ttu-id="90504-409">Dirección de enlace</span><span class="sxs-lookup"><span data-stu-id="90504-409">Bind-Address</span></span>
* <span data-ttu-id="90504-410">Nombre de usuario de MySQL</span><span class="sxs-lookup"><span data-stu-id="90504-410">MySQL username</span></span>
* <span data-ttu-id="90504-411">Contraseña codificada en Base64</span><span class="sxs-lookup"><span data-stu-id="90504-411">Base64 encoded password</span></span>

<span data-ttu-id="90504-412">El archivo de autenticación de MySQL para OMI solo concede privilegios de lectura y escritura al usuario de Linux que lo generó.</span><span class="sxs-lookup"><span data-stu-id="90504-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="90504-413">Un archivo de autenticación de MySQL para OMI predeterminado contiene una instancia y un número de puerto predeterminados, dependiendo de qué información esté disponible y analizada en el archivo de configuración de MySQL que se encontró.</span><span class="sxs-lookup"><span data-stu-id="90504-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="90504-414">La instancia predeterminada es un medio para facilitar la administración de varias instancias de MySQL en un host de Linux y viene indicado por la instancia con el puerto 0.</span><span class="sxs-lookup"><span data-stu-id="90504-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="90504-415">Todas las instancias agregadas heredarán las propiedades establecidas en la instancia predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90504-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="90504-416">Por ejemplo, si se agrega la instancia de MySQL que escucha en el puerto '3308', se utilizará la dirección de enlace, el nombre de usuario y la contraseña codificada en Base64 de la instancia predeterminada para probar y supervisar la instancia que escucha en 3308.</span><span class="sxs-lookup"><span data-stu-id="90504-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="90504-417">Si la instancia en 3308 está enlazada a otra dirección y usa el mismo par de nombre de usuario y contraseña que MySQL, solo será necesario volver a especificar la dirección de enlace y las demás propiedades se heredarán.</span><span class="sxs-lookup"><span data-stu-id="90504-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="90504-418">Los ejemplos del archivo de autenticación son similares al siguiente.</span><span class="sxs-lookup"><span data-stu-id="90504-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="90504-419">Instancia predeterminada e instancia con el puerto 3308:</span><span class="sxs-lookup"><span data-stu-id="90504-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="90504-420">Instancia predeterminada e instancia con el puerto 3308 + diferente contraseña codificada en Base 64:</span><span class="sxs-lookup"><span data-stu-id="90504-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="90504-421">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="90504-421">**Property**</span></span> | <span data-ttu-id="90504-422">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="90504-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="90504-423">Port</span><span class="sxs-lookup"><span data-stu-id="90504-423">Port</span></span> |<span data-ttu-id="90504-424">Puerto representa el puerto actual en el que está escuchando la instancia de MySQL.</span><span class="sxs-lookup"><span data-stu-id="90504-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="90504-425">El puerto 0 implica que las propiedades que siguen se usan para la instancia predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90504-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="90504-426">Dirección de enlace</span><span class="sxs-lookup"><span data-stu-id="90504-426">Bind-Address</span></span> |<span data-ttu-id="90504-427">La dirección de enlace es la actual dirección de enlace de MySQL</span><span class="sxs-lookup"><span data-stu-id="90504-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="90504-428">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="90504-428">username</span></span> |<span data-ttu-id="90504-429">Este es el nombre de usuario del usuario de MySQL que desee usar para supervisar la instancia del servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="90504-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="90504-430">Contraseña codificada en Base64</span><span class="sxs-lookup"><span data-stu-id="90504-430">Base64 encoded Password</span></span> |<span data-ttu-id="90504-431">Esta es la contraseña del usuario de supervisión de MySQL codificada en Base64.</span><span class="sxs-lookup"><span data-stu-id="90504-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="90504-432">Actualización automática</span><span class="sxs-lookup"><span data-stu-id="90504-432">AutoUpdate</span></span> |<span data-ttu-id="90504-433">Cuando el proveedor de MySQL para OMI se actualiza, el proveedor volverá a examinar para detectar cambios en el archivo my.cnf y sobrescribir el archivo de autenticación de MySQL para OMI.</span><span class="sxs-lookup"><span data-stu-id="90504-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="90504-434">Establezca esta marca en verdadero o falso dependiendo de las actualizaciones necesarias para el archivo de autenticación de MySQL para OMI.</span><span class="sxs-lookup"><span data-stu-id="90504-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="90504-435">Ubicación del archivo de autenticación</span><span class="sxs-lookup"><span data-stu-id="90504-435">Authentication file location</span></span>
<span data-ttu-id="90504-436">El archivo de autenticación de MySQL para OMI se debe colocar en la siguiente ubicación con el nombre "mysql-auth":</span><span class="sxs-lookup"><span data-stu-id="90504-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="90504-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="90504-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="90504-438">El archivo (y directorio auth/omsagent) deben pertenecer al usuario omsagent.</span><span class="sxs-lookup"><span data-stu-id="90504-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="90504-439">Registros del agente</span><span class="sxs-lookup"><span data-stu-id="90504-439">Agent logs</span></span>
<span data-ttu-id="90504-440">Los registros para el agente de OMS para Linux se encuentran en:</span><span class="sxs-lookup"><span data-stu-id="90504-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="90504-441">/var/opt/microsoft/omsagent/&lt;identificador de área de trabajo&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="90504-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="90504-442">Los registros para el agente de OMS para Linux para el programa omsconfig (configuración del agente) se encuentran en:</span><span class="sxs-lookup"><span data-stu-id="90504-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="90504-443">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="90504-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="90504-444">Los registros para los componentes OMI y SCX (que proporcionan los datos de métricas de rendimiento) se encuentran en:</span><span class="sxs-lookup"><span data-stu-id="90504-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="90504-445">/var/opt/omi/log/ y /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="90504-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="90504-446">Solución de problemas del agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="90504-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="90504-447">Use la siguiente información para diagnosticar y solucionar problemas habituales.</span><span class="sxs-lookup"><span data-stu-id="90504-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="90504-448">Si la información sobre solución de problemas de esta sección no le resulta de ayuda, también puede usar los siguientes recursos para resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="90504-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="90504-449">Los clientes con soporte técnico Premier pueden registrar un caso de soporte técnico mediante [Premier](https://premier.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="90504-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="90504-450">Los clientes con contratos de soporte técnico de Azure pueden registrar casos de soporte técnico en [Azure Portal](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="90504-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="90504-451">Registre un [problema de GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues).</span><span class="sxs-lookup"><span data-stu-id="90504-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="90504-452">Obtenga ideas y cree un informe de errores en el foro de comentarios [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback).</span><span class="sxs-lookup"><span data-stu-id="90504-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="90504-453">Ubicación de registros importantes</span><span class="sxs-lookup"><span data-stu-id="90504-453">Important log locations</span></span>
| <span data-ttu-id="90504-454">Archivo</span><span class="sxs-lookup"><span data-stu-id="90504-454">File</span></span> | <span data-ttu-id="90504-455">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="90504-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="90504-456">Archivo de registro del agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="90504-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="90504-457">Archivo de registro de la configuración del agente de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="90504-458">Archivos de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="90504-458">Important configuration files</span></span>
| <span data-ttu-id="90504-459">Categoría</span><span class="sxs-lookup"><span data-stu-id="90504-459">Catergory</span></span> | <span data-ttu-id="90504-460">Ubicación del archivo</span><span class="sxs-lookup"><span data-stu-id="90504-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="90504-461">syslog</span><span class="sxs-lookup"><span data-stu-id="90504-461">Syslog</span></span> |<span data-ttu-id="90504-462">`/etc/syslog-ng/syslog-ng.conf`, `/etc/rsyslog.conf` o `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="90504-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="90504-463">Rendimiento, Nagios, Zabbix, salida de OMS y agente general</span><span class="sxs-lookup"><span data-stu-id="90504-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="90504-464">Configuraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="90504-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="90504-465">Los archivos de configuración de los contadores de rendimiento y Syslog se sobrescriben si se habilita la configuración del portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="90504-466">Puede deshabilitar la configuración en el portal de OMS (para todos los nodos) o para nodos únicos ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="90504-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="90504-467">Habilitación del registro de depuración</span><span class="sxs-lookup"><span data-stu-id="90504-467">Enable debug logging</span></span>
<span data-ttu-id="90504-468">Para habilitar el registro de depuración, puede usar el complemento de salida de OMS y la salida detallada.</span><span class="sxs-lookup"><span data-stu-id="90504-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="90504-469">Complemento de salida de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-469">OMS output plugin</span></span>
<span data-ttu-id="90504-470">FluentD permite que el complemento especifique niveles de registro para los diferentes niveles de registro de entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="90504-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="90504-471">Para especificar un nivel de registro distinto para la salida de OMS, edite la configuración del agente general en el archivo `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="90504-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="90504-472">Hacia el final del archivo de configuración, cambie la propiedad `log_level` de `info` a `debug`.</span><span class="sxs-lookup"><span data-stu-id="90504-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="90504-473">El registro de depuración permite ver cargas por lotes al servicio OMS separadas por tipo, número de elementos de datos y tiempo de envío.</span><span class="sxs-lookup"><span data-stu-id="90504-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="90504-474">*Ejemplo de registro con depuración habilitada:*</span><span class="sxs-lookup"><span data-stu-id="90504-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="90504-475">Salida detallada</span><span class="sxs-lookup"><span data-stu-id="90504-475">Verbose output</span></span>
<span data-ttu-id="90504-476">En lugar de usar el complemento de salida de OMS, también puede generar la salida de elementos de datos directamente a `stdout`, que es visible en el archivo de registro del agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="90504-477">En el archivo de configuración del agente general de OMS en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, convierta en comentario el complemento de salida de OMS agregando `#` al principio de cada línea.</span><span class="sxs-lookup"><span data-stu-id="90504-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="90504-478">Bajo el complemento de salida, quite el símbolo `#` al principio de cada línea para quitar el comentario en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="90504-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="90504-479">Los mensajes de Syslog reenviados no aparecen en el registro</span><span class="sxs-lookup"><span data-stu-id="90504-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-480">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-480">Probable causes</span></span>
* <span data-ttu-id="90504-481">La configuración aplicada al servidor Linux no permite la recopilación de las utilidades enviadas ni de los niveles de registro.</span><span class="sxs-lookup"><span data-stu-id="90504-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="90504-482">Syslog no se reenvía correctamente al servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="90504-483">El número de mensajes que se reenvía por segundo es demasiado grande para la configuración básica del agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="90504-484">Soluciones</span><span class="sxs-lookup"><span data-stu-id="90504-484">Resolutions</span></span>
* <span data-ttu-id="90504-485">Compruebe que la configuración de Syslog en el portal de OMS tenga todas las utilidades y los niveles de registro correctos.</span><span class="sxs-lookup"><span data-stu-id="90504-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="90504-486">**Portal de OMS > Configuración > Datos > Syslog**</span><span class="sxs-lookup"><span data-stu-id="90504-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="90504-487">Compruebe que los demonios de mensajería de Syslog nativos (`rsyslog`, `syslog-ng`) puedan recibir los mensajes reenviados.</span><span class="sxs-lookup"><span data-stu-id="90504-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="90504-488">Compruebe la configuración de firewall en el servidor de Syslog para asegurarse de que no se estén bloqueando los mensajes.</span><span class="sxs-lookup"><span data-stu-id="90504-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="90504-489">Simule un mensaje de Syslog enviado a OMS utilizando el comando `logger`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="90504-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="90504-490">Problemas al conectarse a OMS cuando se usa un proxy</span><span class="sxs-lookup"><span data-stu-id="90504-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-491">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-491">Probable causes</span></span>
* <span data-ttu-id="90504-492">El proxy especificado al instalar y configurar al agente es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="90504-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="90504-493">Los puntos de conexión del servicio OMS no están incluidos en la lista de permitidos en su centro de datos.</span><span class="sxs-lookup"><span data-stu-id="90504-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="90504-494">Soluciones</span><span class="sxs-lookup"><span data-stu-id="90504-494">Resolutions</span></span>
* <span data-ttu-id="90504-495">Vuelva a instalar el agente de OMS para Linux mediante el comando siguiente con la opción `-v` habilitada.</span><span class="sxs-lookup"><span data-stu-id="90504-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="90504-496">Esto permite la salida detallada del agente que se conecta a través del proxy al servicio OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="90504-497">Revise la documentación para el proxy de OMS en [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server) (Configuración del agente para usarlo con un servidor proxy HTTP).</span><span class="sxs-lookup"><span data-stu-id="90504-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="90504-498">Compruebe que los siguientes puntos de conexión del servicio OMS estén incluidos en la lista de permitidos.</span><span class="sxs-lookup"><span data-stu-id="90504-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="90504-499">Recurso del agente</span><span class="sxs-lookup"><span data-stu-id="90504-499">Agent Resource</span></span> | <span data-ttu-id="90504-500">Puertos</span><span class="sxs-lookup"><span data-stu-id="90504-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="90504-501">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="90504-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="90504-502">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="90504-502">Port 443</span></span> |
| <span data-ttu-id="90504-503">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="90504-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="90504-504">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="90504-504">Port 443</span></span> |
| <span data-ttu-id="90504-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="90504-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="90504-506">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="90504-506">Port 443</span></span> |
| <span data-ttu-id="90504-507">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="90504-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="90504-508">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="90504-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="90504-509">Se muestra un error 403 durante la incorporación</span><span class="sxs-lookup"><span data-stu-id="90504-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-510">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-510">Probable causes</span></span>
* <span data-ttu-id="90504-511">La fecha y la hora son incorrectas en el servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="90504-512">El identificador y la clave de área de trabajo usados son incorrectos.</span><span class="sxs-lookup"><span data-stu-id="90504-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="90504-513">Resolución</span><span class="sxs-lookup"><span data-stu-id="90504-513">Resolution</span></span>
* <span data-ttu-id="90504-514">Compruebe la hora en el servidor Linux con el comando `date`.</span><span class="sxs-lookup"><span data-stu-id="90504-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="90504-515">Si los datos son de 15 minutos anteriores o posteriores a la hora actual, la incorporación genera un error.</span><span class="sxs-lookup"><span data-stu-id="90504-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="90504-516">Para corregir este problema, actualice la fecha o la zona horaria del servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="90504-517">La versión más reciente del agente de OMS para Linux notifica si una diferencia horaria está causando el error de incorporación.</span><span class="sxs-lookup"><span data-stu-id="90504-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="90504-518">Repita la incorporación con el identificador y la clave de área de trabajo correctos.</span><span class="sxs-lookup"><span data-stu-id="90504-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="90504-519">Para más información, consulte [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Incorporación mediante la línea de comandos).</span><span class="sxs-lookup"><span data-stu-id="90504-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="90504-520">Aparece un error 500 o 404 en el archivo de registro después de la incorporación</span><span class="sxs-lookup"><span data-stu-id="90504-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="90504-521">Se trata de un problema conocido que se produce durante la primera carga de datos de Linux en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="90504-522">Esto no afecta a los datos que se envían ni causa otros problemas.</span><span class="sxs-lookup"><span data-stu-id="90504-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="90504-523">Puede pasar por alto los errores durante la incorporación inicial.</span><span class="sxs-lookup"><span data-stu-id="90504-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="90504-524">Los datos de Nagios no aparecen en el portal de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-525">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-525">Probable causes</span></span>
* <span data-ttu-id="90504-526">El usuario omsagent no tiene permisos para leer el archivo de registro de Nagios.</span><span class="sxs-lookup"><span data-stu-id="90504-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="90504-527">Las secciones de origen y filtro de Nagios todavía incluyen comentarios en el archivo omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="90504-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="90504-528">Soluciones</span><span class="sxs-lookup"><span data-stu-id="90504-528">Resolutions</span></span>
* <span data-ttu-id="90504-529">Agregue al usuario omsagent para leer el archivo de Nagios.</span><span class="sxs-lookup"><span data-stu-id="90504-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="90504-530">Consulte [Nagios Alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Alertas de Nagios) para más información.</span><span class="sxs-lookup"><span data-stu-id="90504-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="90504-531">En el archivo de configuración del agente de OMS general para Linux en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, asegúrese de que se hayan quitado los comentarios de **ambas** secciones, la de origen y la de filtro de Nagios, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="90504-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="90504-532">Los datos de Linux no aparecen en el portal de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-533">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-533">Probable causes</span></span>
* <span data-ttu-id="90504-534">Se produjo un error en la incorporación al servicio OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="90504-535">La conexión al servicio OMS se bloquea.</span><span class="sxs-lookup"><span data-stu-id="90504-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="90504-536">Se está haciendo la copia de seguridad de los datos del agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="90504-537">Soluciones</span><span class="sxs-lookup"><span data-stu-id="90504-537">Resolutions</span></span>
* <span data-ttu-id="90504-538">Compruebe que la incorporación al servicio OMS se hiciera correctamente; para ello, compruebe que `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="90504-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="90504-539">Repita la incorporación con la línea de comandos de omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="90504-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="90504-540">Para más información, consulte [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Incorporación mediante la línea de comandos).</span><span class="sxs-lookup"><span data-stu-id="90504-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="90504-541">Si usa un proxy, siga los pasos anteriores para solucionar problemas con un proxy.</span><span class="sxs-lookup"><span data-stu-id="90504-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="90504-542">En algunos casos, cuando el agente de OMS para Linux no puede comunicarse con el servicio OMS, la copia de seguridad de los datos del agente ocupa el tamaño de búfer total de 50 MB.</span><span class="sxs-lookup"><span data-stu-id="90504-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="90504-543">Reinicie el agente de OMS para Linux ejecutando el comando `/opt/microsoft/omsagent/bin/service_control restart`.</span><span class="sxs-lookup"><span data-stu-id="90504-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="90504-544">Este problema está corregido en el agente versión 1.1.0-28 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="90504-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="90504-545">La configuración de contador de rendimiento de Linux para Syslog no se aplica en el portal de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-546">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-546">Probable causes</span></span>
* <span data-ttu-id="90504-547">El agente de configuración en el agente de OMS para Linux no ha recuperado la configuración más reciente del portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="90504-548">No se aplicó la configuración modificada en el portal.</span><span class="sxs-lookup"><span data-stu-id="90504-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="90504-549">Soluciones</span><span class="sxs-lookup"><span data-stu-id="90504-549">Resolutions</span></span>
<span data-ttu-id="90504-550">`omsconfig` es el agente de configuración en el agente de OMS para Linux que recupera los cambios de configuración del portal de OMS cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="90504-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="90504-551">A continuación, esta configuración se aplica a los archivos de configuración del agente de OMS para Linux que se encuentran en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="90504-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="90504-552">En algunos casos, es posible que el agente de configuración del agente de OMS para Linux no pueda comunicarse con el servicio de configuración del portal y, por tanto, no se aplique la configuración más reciente.</span><span class="sxs-lookup"><span data-stu-id="90504-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="90504-553">Compruebe que el agente `omsconfig` esté instalado con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="90504-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="90504-554">`dpkg --list omsconfig` o `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="90504-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="90504-555">Si no está instalado, vuelva a instalar la versión más reciente del agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="90504-556">Compruebe que el agente `omsconfig` pueda comunicarse con el servicio OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="90504-557">Ejecute el comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`.</span><span class="sxs-lookup"><span data-stu-id="90504-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="90504-558">El comando anterior devuelve la configuración que el agente recupera del portal, incluida la configuración de Syslog, los contadores de rendimiento de Linux y los registros personalizados.</span><span class="sxs-lookup"><span data-stu-id="90504-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="90504-559">Si se produce un error con el comando anterior, ejecute el comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="90504-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="90504-560">Este comando fuerza al agente de omsconfig a comunicarse con el servicio OMS para recuperar la configuración más reciente.</span><span class="sxs-lookup"><span data-stu-id="90504-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="90504-561">Los datos de registros personalizados de Linux no aparecen en el portal de OMS</span><span class="sxs-lookup"><span data-stu-id="90504-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="90504-562">Causas probables</span><span class="sxs-lookup"><span data-stu-id="90504-562">Probable causes</span></span>
* <span data-ttu-id="90504-563">Se produjo un error en la incorporación al servicio OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="90504-564">No se ha seleccionado la configuración **Aplicar la configuración que aparece a continuación a mis máquinas con Linux**.</span><span class="sxs-lookup"><span data-stu-id="90504-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="90504-565">omsconfig no ha recuperado el registro personalizado más reciente del portal</span><span class="sxs-lookup"><span data-stu-id="90504-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="90504-566">El usuario `omsagent` no puede acceder al registro personalizado por un problema de permisos o no se encontró `omsagent`.</span><span class="sxs-lookup"><span data-stu-id="90504-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="90504-567">En este caso, verá la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="90504-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="90504-568">Se trata de un problema conocido con la condición de carrera que se corrigió en el agente de OMS para Linux versión 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="90504-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="90504-569">Soluciones</span><span class="sxs-lookup"><span data-stu-id="90504-569">Resolutions</span></span>
* <span data-ttu-id="90504-570">Compruebe que la incorporación se haya llevado a cabo correctamente; para hacerlo, determine si el archivo `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="90504-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="90504-571">Si es necesario, repita la incorporación con la línea de comandos de omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="90504-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="90504-572">Para más información, consulte [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Incorporación mediante la línea de comandos).</span><span class="sxs-lookup"><span data-stu-id="90504-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="90504-573">En el portal de OMS, en **Configuración** en la pestaña **Datos**, asegúrese de que la configuración **Aplicar la configuración que aparece a continuación a mis máquinas con Linux** esté seleccionada.</span><span class="sxs-lookup"><span data-stu-id="90504-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="90504-574">![Aplicar configuración](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="90504-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="90504-575">Compruebe que el agente `omsconfig` pueda comunicarse con el servicio OMS.</span><span class="sxs-lookup"><span data-stu-id="90504-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="90504-576">Ejecute el comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`.</span><span class="sxs-lookup"><span data-stu-id="90504-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="90504-577">El comando anterior devuelve la configuración que el agente recupera del portal, incluida la configuración de Syslog, los contadores de rendimiento de Linux y los registros personalizados.</span><span class="sxs-lookup"><span data-stu-id="90504-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="90504-578">Si se produce un error con el comando anterior, ejecute el comando `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="90504-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="90504-579">Este comando fuerza al agente de omsconfig a comunicarse con el servicio OMS y a recuperar la configuración más reciente.</span><span class="sxs-lookup"><span data-stu-id="90504-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="90504-580">El agente de OMS para Linux, en lugar de ejecutarse como un usuario `root` con privilegios, se ejecuta como el usuario `omsagent`.</span><span class="sxs-lookup"><span data-stu-id="90504-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="90504-581">En la mayoría de los casos, se deben conceder permisos explícitos al usuario para que lea determinados archivos.</span><span class="sxs-lookup"><span data-stu-id="90504-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="90504-582">Para conceder permiso al usuario `omsagent`, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="90504-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="90504-583">Agregue al usuario `omsagent` a un grupo específico con `sudo usermod -a -G <GROUPNAME> <USERNAME>`.</span><span class="sxs-lookup"><span data-stu-id="90504-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="90504-584">Concédale acceso universal de lectura al archivo necesario con `sudo chmod -R ugo+rw <FILE DIRECTORY>`.</span><span class="sxs-lookup"><span data-stu-id="90504-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="90504-585">Existe un problema conocido con la condición de carrera que se corrigió en el agente de OMS para Linux versión 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="90504-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="90504-586">Después de actualizar al agente más reciente, ejecute el siguiente comando para obtener la versión más reciente del complemento de salida:</span><span class="sxs-lookup"><span data-stu-id="90504-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="90504-587">Limitaciones conocidas</span><span class="sxs-lookup"><span data-stu-id="90504-587">Known limitations</span></span>
<span data-ttu-id="90504-588">Revise las siguientes secciones para informarse sobre las limitaciones actuales del agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="90504-589">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="90504-589">Azure Diagnostics</span></span>
<span data-ttu-id="90504-590">Para las máquinas virtuales de Linux que se ejecutan en Azure es posible que se necesiten pasos adicionales para permitir la recopilación de datos por parte de Diagnóstico de Azure y Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="90504-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="90504-591">**Versión 2.2** de la extensión de diagnósticos de Linux.</span><span class="sxs-lookup"><span data-stu-id="90504-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="90504-592">Para más información sobre la instalación y la configuración de la extensión de diagnóstico de Linux, consulte [Uso del comando de la CLI de Azure para habilitar la extensión de diagnóstico de Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="90504-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="90504-593">**Actualización de la extensión de diagnósticos de Linux de 2.0 a 2.2 ASM de la CLI de Azure:**</span><span class="sxs-lookup"><span data-stu-id="90504-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="90504-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="90504-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="90504-595">Estos ejemplos de comandos hacen referencia a un archivo denominado PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="90504-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="90504-596">El formato de ese archivo debe ser similar al del ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="90504-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="90504-597">Sysklog no se admite.</span><span class="sxs-lookup"><span data-stu-id="90504-597">Sysklog is not supported</span></span>
<span data-ttu-id="90504-598">Rsyslog o Syslog son necesarios para recopilar mensajes de Syslog.</span><span class="sxs-lookup"><span data-stu-id="90504-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="90504-599">El demonio predeterminado de Syslog en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (Sysklog) no se admite para la recopilación de eventos de Syslog.</span><span class="sxs-lookup"><span data-stu-id="90504-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="90504-600">Para recopilar datos de Syslog de esta versión de estas distribuciones, es necesario instalar configurar el demonio de Rsyslog para reemplazar Sysklog.</span><span class="sxs-lookup"><span data-stu-id="90504-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="90504-601">Para más información acerca de cómo sustituir Sysklog por Rsyslog, consulte [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM)(instalar el recién creado rsyslog RPM).</span><span class="sxs-lookup"><span data-stu-id="90504-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90504-602">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90504-602">Next Steps</span></span>
* <span data-ttu-id="90504-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) (Incorporación de soluciones de Log Analytics desde la galería de soluciones) para agregar funcionalidad y recopilar datos.</span><span class="sxs-lookup"><span data-stu-id="90504-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="90504-604">Familiarícese con las [búsquedas de registros](log-analytics-log-searches.md) para ver información detallada recopilada por soluciones.</span><span class="sxs-lookup"><span data-stu-id="90504-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="90504-605">Use los [paneles](log-analytics-dashboards.md) para guardar y mostrar sus propias búsquedas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="90504-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
