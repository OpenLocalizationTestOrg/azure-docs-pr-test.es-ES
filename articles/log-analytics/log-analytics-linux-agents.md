---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="e3fbd-101">Conectar su tooLog de equipos Linux análisis</span><span class="sxs-lookup"><span data-stu-id="e3fbd-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="e3fbd-102">El uso de Log Analytics permite recopilar y actuar sobre los datos generados en equipos Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="e3fbd-103">Agregar datos recopilados de Linux tooOMS permite toomanage sistemas de Linux y soluciones de contenedor como Docker, independientemente de dónde estén ubicados los equipos, prácticamente en cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="e3fbd-104">Orígenes de datos pueden residir en su centro de datos local como servidores físicos, equipos virtuales en un servicio hospedado en la nube como Amazon Web Services (AWS) o Microsoft Azure, o incluso Hola portátil en su escritorio.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="e3fbd-105">Además, OMS también recopila datos de los equipos de Windows de forma similar, por lo que es compatible con un entorno informático realmente híbrido.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="e3fbd-106">Puede ver y administrar los datos de todos esos orígenes con Log Analytics en OMS con un portal de administración único.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="e3fbd-107">Esto reduce la necesidad de hello toomonitor con muchos sistemas distintos, hace que resulte fácil tooconsume y que puede exportar cualquier dato que quiera toowhatever solución de análisis de negocios o sistema que ya tiene.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="e3fbd-108">Este artículo es una guía de inicio rápido que le ayudará a recopilar y administrar los datos de los equipos Linux mediante Hola agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="e3fbd-109">Si desea obtener más detalles técnicos, como la configuración del servidor proxy, información acerca de las métricas de CollectD y orígenes de datos JSON personalizados, encontrará esa información en la [información general sobre el agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) y la [documentación completa sobre el agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="e3fbd-110">Actualmente, puede recopilar Hola siguientes tipos de datos de los equipos Linux:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="e3fbd-111">Métricas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e3fbd-111">Performance metrics</span></span>
* <span data-ttu-id="e3fbd-112">Eventos Syslog</span><span class="sxs-lookup"><span data-stu-id="e3fbd-112">Syslog events</span></span>
* <span data-ttu-id="e3fbd-113">Alertas de Nagios y Zabbix</span><span class="sxs-lookup"><span data-stu-id="e3fbd-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="e3fbd-114">Registros, inventario y métricas de rendimiento del contenedor de Docker</span><span class="sxs-lookup"><span data-stu-id="e3fbd-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="e3fbd-115">Versiones de Linux compatibles</span><span class="sxs-lookup"><span data-stu-id="e3fbd-115">Supported Linux versions</span></span>
<span data-ttu-id="e3fbd-116">Tanto la versión x86 como la x64 son compatibles oficialmente en una variedad de distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="e3fbd-117">Sin embargo, también puede ejecutar Hola agente de OMS para Linux en otras distribuciones que no aparece.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="e3fbd-118">Amazon Linux 2012.09 hasta 2015.09</span><span class="sxs-lookup"><span data-stu-id="e3fbd-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="e3fbd-119">CentOS Linux 5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="e3fbd-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="e3fbd-120">Oracle Linux 5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="e3fbd-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="e3fbd-121">Red Hat Enterprise Linux Server 5, 6 y 7</span><span class="sxs-lookup"><span data-stu-id="e3fbd-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="e3fbd-122">Debian GNU/Linux 6, 7 y 8</span><span class="sxs-lookup"><span data-stu-id="e3fbd-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="e3fbd-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="e3fbd-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="e3fbd-124">SUSE Linux Enterprise Server 11 y 12</span><span class="sxs-lookup"><span data-stu-id="e3fbd-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="e3fbd-125">Agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-125">OMS Agent for Linux</span></span>
<span data-ttu-id="e3fbd-126">Hola agente de Operations Management Suite para Linux consta de varios paquetes.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="e3fbd-127">archivo de la versión Hello contiene Hola después de paquetes, disponibles mediante la agrupación de shell Hola ejecución con `--extract`.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="e3fbd-128">**Paquete**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-128">**Package**</span></span> | <span data-ttu-id="e3fbd-129">**Versión**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-129">**Version**</span></span> | <span data-ttu-id="e3fbd-130">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3fbd-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="e3fbd-131">omsagent</span></span> |<span data-ttu-id="e3fbd-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e3fbd-132">1.1.0</span></span> |<span data-ttu-id="e3fbd-133">Hola agente de Operations Management Suite para Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="e3fbd-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="e3fbd-134">omsconfig</span></span> |<span data-ttu-id="e3fbd-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e3fbd-135">1.1.1</span></span> |<span data-ttu-id="e3fbd-136">Agente de configuración para hello agente de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="e3fbd-137">omi</span><span class="sxs-lookup"><span data-stu-id="e3fbd-137">omi</span></span> |<span data-ttu-id="e3fbd-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="e3fbd-138">1.0.8.3</span></span> |<span data-ttu-id="e3fbd-139">Infraestructura de administración abierta (OMI), un servidor de CIM ligero</span><span class="sxs-lookup"><span data-stu-id="e3fbd-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="e3fbd-140">scx</span><span class="sxs-lookup"><span data-stu-id="e3fbd-140">scx</span></span> |<span data-ttu-id="e3fbd-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="e3fbd-141">1.6.2</span></span> |<span data-ttu-id="e3fbd-142">Proveedores de CIM OMI para métricas de rendimiento del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e3fbd-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="e3fbd-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="e3fbd-143">apache-cimprov</span></span> |<span data-ttu-id="e3fbd-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e3fbd-144">1.0.0</span></span> |<span data-ttu-id="e3fbd-145">Proveedor de supervisión de rendimiento de servidor HTTP de Apache para OMI.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="e3fbd-146">Solo se instala si se detecta un servidor HTTP de Apache.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="e3fbd-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="e3fbd-147">mysql-cimprov</span></span> |<span data-ttu-id="e3fbd-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e3fbd-148">1.0.0</span></span> |<span data-ttu-id="e3fbd-149">Proveedor de supervisión de rendimiento de servidor MySQL Server para OMI.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="e3fbd-150">Solo se instala si se detecta un servidor MySQL/MariaDB de Apache.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="e3fbd-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="e3fbd-151">docker-cimprov</span></span> |<span data-ttu-id="e3fbd-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="e3fbd-152">0.1.0</span></span> |<span data-ttu-id="e3fbd-153">Proveedor de Docker para OMI.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-153">Docker provider for OMI.</span></span> <span data-ttu-id="e3fbd-154">Solo se instala si se detecta Docker.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="e3fbd-155">Artefactos de instalación adicionales</span><span class="sxs-lookup"><span data-stu-id="e3fbd-155">Additional installation artifacts</span></span>
<span data-ttu-id="e3fbd-156">Después de instalar el agente de OMS de Hola para paquetes de Linux, hello siguientes cambios de configuración adicionales de todo el sistema se aplican.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="e3fbd-157">Estos artefactos se quitan cuando se desinstala el paquete de hello omsagent.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="e3fbd-158">Se crea un usuario sin privilegios llamado: `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="e3fbd-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="e3fbd-159">Se trata de hello cuenta hello omsagent daemon se ejecuta como</span><span class="sxs-lookup"><span data-stu-id="e3fbd-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="e3fbd-160">Se crea un archivo "include" de sudoers en /etc/sudoers.d/omsagent este autoriza a omsagent toorestart Hola syslog y omsagent daemons.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="e3fbd-161">Si no se admiten directivas "incluir" de sudo en la versión de Hola instalada de sudo, estas entradas se escribirán demasiado/etcetera/sudoers.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="e3fbd-162">configuración de syslog de Hello es tooforward modificado un subconjunto de agente de toohello de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="e3fbd-163">Para obtener más información, vea hello **configurar la recopilación de datos** sección más adelante</span><span class="sxs-lookup"><span data-stu-id="e3fbd-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="e3fbd-164">Detalles de la recopilación de datos de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-164">Linux data collection details</span></span>
<span data-ttu-id="e3fbd-165">Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="e3fbd-166">de origen</span><span class="sxs-lookup"><span data-stu-id="e3fbd-166">source</span></span> | <span data-ttu-id="e3fbd-167">Agente directo</span><span class="sxs-lookup"><span data-stu-id="e3fbd-167">Direct Agent</span></span> | <span data-ttu-id="e3fbd-168">Agente de SCOM</span><span class="sxs-lookup"><span data-stu-id="e3fbd-168">SCOM agent</span></span> | <span data-ttu-id="e3fbd-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e3fbd-169">Azure Storage</span></span> | <span data-ttu-id="e3fbd-170">¿Se necesita SCOM?</span><span class="sxs-lookup"><span data-stu-id="e3fbd-170">SCOM required?</span></span> | <span data-ttu-id="e3fbd-171">Datos del agente de SCOM enviados a través del grupo de administración</span><span class="sxs-lookup"><span data-stu-id="e3fbd-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="e3fbd-172">Frecuencia de recopilación</span><span class="sxs-lookup"><span data-stu-id="e3fbd-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e3fbd-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="e3fbd-173">Zabbix</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="e3fbd-179">1 minuto</span><span class="sxs-lookup"><span data-stu-id="e3fbd-179">1 minute</span></span> |
| <span data-ttu-id="e3fbd-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="e3fbd-180">Nagios</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="e3fbd-186">a la llegada</span><span class="sxs-lookup"><span data-stu-id="e3fbd-186">on arrival</span></span> |
| <span data-ttu-id="e3fbd-187">syslog</span><span class="sxs-lookup"><span data-stu-id="e3fbd-187">syslog</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="e3fbd-193">De Almacenamiento de Azure: 10 minutos; del agente: a la llegada</span><span class="sxs-lookup"><span data-stu-id="e3fbd-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="e3fbd-194">Contadores de rendimiento de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-194">Linux performance counters</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="e3fbd-200">Mínimo de 10 segundos, según lo programado</span><span class="sxs-lookup"><span data-stu-id="e3fbd-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="e3fbd-201">Seguimiento de cambios</span><span class="sxs-lookup"><span data-stu-id="e3fbd-201">change tracking</span></span> |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="e3fbd-207">Cada hora</span><span class="sxs-lookup"><span data-stu-id="e3fbd-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="e3fbd-208">Requisitos de paquete</span><span class="sxs-lookup"><span data-stu-id="e3fbd-208">Package Requirements</span></span>
| <span data-ttu-id="e3fbd-209">**Paquetes necesarios**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-209">**Required package**</span></span> | <span data-ttu-id="e3fbd-210">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-210">**Description**</span></span> | <span data-ttu-id="e3fbd-211">**Versión mínima**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3fbd-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="e3fbd-212">Glibc</span></span> |<span data-ttu-id="e3fbd-213">Biblioteca GNU C</span><span class="sxs-lookup"><span data-stu-id="e3fbd-213">GNU C library</span></span> |<span data-ttu-id="e3fbd-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="e3fbd-214">2.5-12</span></span> |
| <span data-ttu-id="e3fbd-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="e3fbd-215">Openssl</span></span> |<span data-ttu-id="e3fbd-216">Bibliotecas OpenSSL</span><span class="sxs-lookup"><span data-stu-id="e3fbd-216">OpenSSL libraries</span></span> |<span data-ttu-id="e3fbd-217">0.9.8E o 1.0</span><span class="sxs-lookup"><span data-stu-id="e3fbd-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="e3fbd-218">Curl</span><span class="sxs-lookup"><span data-stu-id="e3fbd-218">Curl</span></span> |<span data-ttu-id="e3fbd-219">Cliente web de cURL</span><span class="sxs-lookup"><span data-stu-id="e3fbd-219">cURL web client</span></span> |<span data-ttu-id="e3fbd-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="e3fbd-220">7.15.5</span></span> |
| <span data-ttu-id="e3fbd-221">Python ctypes</span><span class="sxs-lookup"><span data-stu-id="e3fbd-221">Python-ctypes</span></span> |<span data-ttu-id="e3fbd-222">Bibliotecas de funciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-222">function libraries</span></span> |<span data-ttu-id="e3fbd-223">N/D</span><span class="sxs-lookup"><span data-stu-id="e3fbd-223">n/a</span></span> |
| <span data-ttu-id="e3fbd-224">PAM</span><span class="sxs-lookup"><span data-stu-id="e3fbd-224">PAM</span></span> |<span data-ttu-id="e3fbd-225">Módulos de autenticación conectables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="e3fbd-226">N/D</span><span class="sxs-lookup"><span data-stu-id="e3fbd-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="e3fbd-227">Rsyslog o syslog-ng es necesario toocollect mensajes de syslog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="e3fbd-228">demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="e3fbd-229">toocollect datos de syslog de esta versión de las distribuciones, Hola rsyslog daemon debe estar instalado y configurado tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="e3fbd-230">Instalación rápida</span><span class="sxs-lookup"><span data-stu-id="e3fbd-230">Quick install</span></span>
<span data-ttu-id="e3fbd-231">Ejecute hello después comandos toodownload hello omsagent, validar la suma de comprobación de hello, a continuación, instalar y agente de Hola incorporar.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="e3fbd-232">Los comandos son para 64 bits.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-232">Commands are for 64-bit.</span></span> <span data-ttu-id="e3fbd-233">Hello Id. de área de trabajo y la clave principal se encuentran en el portal de OMS de hello en **configuración** en hello **orígenes conectados** ficha.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![detalles de área de trabajo](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="e3fbd-235">Hay una variedad de otro métodos tooinstall Hola agente y actualizarlo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="e3fbd-236">Puede obtener más información sobre estos en [Hola de pasos tooinstall agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="e3fbd-237">También puede ver hello [Azure tutorial en vídeo](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="e3fbd-238">Selección del método de recopilación de datos de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="e3fbd-239">Cómo elegir Hola tipos de datos que lo haría con like toocollect depende de si desea que el portal de OMS toouse Hola o si prefiere editar varios archivos de configuración directamente en los clientes de Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="e3fbd-240">Si decide que el portal de hello toouse, configuración de Hola se envía automáticamente tooall los clientes de Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="e3fbd-241">Si necesita diferentes configuraciones para distintos clientes de Linux, se necesita archivos de cliente de tooedit individualmente o usar una alternativa como PowerShell DSC, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="e3fbd-242">Puede especificar los eventos de syslog de Hola y contadores de rendimiento que desea que toocollect mediante archivos de configuración en los equipos Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="e3fbd-243">*Si ha elegido tooconfigure la recopilación de datos mediante la edición de archivos de configuración del agente, debe deshabilitar la configuración centralizada Hola.*</span><span class="sxs-lookup"><span data-stu-id="e3fbd-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="e3fbd-244">Se proporcionan instrucciones a continuación de la recopilación de datos de tooconfigure en del agente de hello archivos de configuración, así como toodisable configuración central en todos los agentes de OMS para Linux o en equipos individuales.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="e3fbd-245">Deshabilitación de la administración de OMS para un equipo individual de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="e3fbd-246">Recopilación de datos centralizado para los datos de configuración está deshabilitada para un equipo individual de Linux con hello script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="e3fbd-247">Esto puede ser útil si un subconjunto de equipos debe tener una configuración especializada.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="e3fbd-248">toodisable configuración centralizada:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="e3fbd-249">Habilitar toore configuración centralizada:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="e3fbd-250">Contadores de rendimiento de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-250">Linux performance counters</span></span>
<span data-ttu-id="e3fbd-251">Contadores de rendimiento de Linux son los contadores de rendimiento tooWindows similar: ambos funcionan de forma similar.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="e3fbd-252">Puede usar hello siguiendo los procedimientos tooadd y configurarlos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="e3fbd-253">Una vez que se agregan tooOMS, se recopilan datos para estos cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="e3fbd-254">tooadd un contador de rendimiento de Linux en OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="e3fbd-255">tooconfigure agentes de OMS para Linux mediante el portal de OMS hello, puede agregar contadores de rendimiento de Linux en la página de configuración de hello, haga clic en **datos**.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="e3fbd-256">En hello **configuración** página en **datos** , haga clic en **contadores de rendimiento de Linux** y, a continuación, seleccionar o escribir nombre hello del contador de Hola que desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="e3fbd-257">![Datos](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="e3fbd-258">Si no sabe el nombre completo de hello del contador de hello, puede empezar a escribir un nombre parcial y aparecerá una lista de contadores disponibles.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="e3fbd-259">Cuando encuentre el contador de Hola que desee tooadd, haga clic en nombre de hello en lista de hello y, a continuación, haga clic en hello más hello de icono tooadd contador.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="e3fbd-260">Después de agregar el contador de hello, aparece en la lista de Hola de contadores, resaltado con una barra coloreada.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="e3fbd-261">De forma predeterminada, Hola **aplicar máquinas toomy de configuración siguientes** opción está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="e3fbd-262">Si desea toodisable enviar datos de configuración, desactive la selección de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="e3fbd-263">Cuando haya terminado de modificar los contadores de rendimiento, en parte inferior de Hola de página de Hola haga clic en **guardar** toofinalize los cambios.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="e3fbd-264">cambios de configuración de Hola que haya hecho, a continuación, se envían tooall Hola agentes de OMS para Linux registrados con OMS, normalmente en 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="e3fbd-265">Configuración de los contadores de rendimiento de Linux en OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="e3fbd-266">Para los contadores de rendimiento de Windows, puede elegir una instancia específica para cada contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="e3fbd-267">Sin embargo, para los contadores de rendimiento de Linux, cualquier instancia de un contador que elija aplica tooall contadores de secundarios de contador de hello primario.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="e3fbd-268">Hello tabla siguiente muestran instancias comunes Hola contadores de rendimiento de Linux y Windows tooboth disponible.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="e3fbd-269">**Nombre de la instancia**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-269">**Instance name**</span></span> | <span data-ttu-id="e3fbd-270">**Significado**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="e3fbd-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="e3fbd-271">\_Total</span></span> |<span data-ttu-id="e3fbd-272">Total de todas las instancias de Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="e3fbd-273">Todas las instancias</span><span class="sxs-lookup"><span data-stu-id="e3fbd-273">All instances</span></span> |
| <span data-ttu-id="e3fbd-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-274">(/&#124;/var)</span></span> |<span data-ttu-id="e3fbd-275">Coincide con las instancias con nombre: / o /var</span><span class="sxs-lookup"><span data-stu-id="e3fbd-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="e3fbd-276">De igual forma, intervalo de muestra de Hola que elija para un contador primario aplica tooall los contadores secundarios.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="e3fbd-277">En otras palabras, todas las instancias y los intervalos de muestra de contador de hello secundarios están unidos entre sí.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="e3fbd-278">Incorporación y configuración de las métricas de rendimiento con Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="e3fbd-279">Toocollect de las métricas de rendimiento se controlan mediante la configuración de hello en/etcetera/opt/microsoft/omsagent/&lt;Id. de área de trabajo&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="e3fbd-280">Vea [métricas de rendimiento disponibles](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) para las clases disponibles y las métricas para hello agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="e3fbd-281">Cada objeto o categoría de toocollect de las métricas de rendimiento debe definirse en el archivo de configuración de hello como una sola `<source>` elemento.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="e3fbd-282">sintaxis de Hello sigue siguiente patrón de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="e3fbd-283">Hola parámetros configurables de este elemento son:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="e3fbd-284">**Objeto\_nombre**: nombre de objeto de hello para la recopilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="e3fbd-285">**Instancia\_regex**: un *expresión regular* definir qué toocollect de instancias.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="e3fbd-286">Hola valor: `.*` especifica todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="e3fbd-287">métricas de procesador toocollect para solo hello \_instancia Total, podría especificar `_Total`.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="e3fbd-288">métricas de procesador toocollect solo hello instancias crond o sshd, puede especificar: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="e3fbd-289">**Contador\_nombre\_regex**: un *expresión regular* definir qué toocollect contadores (para el objeto de hello).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="e3fbd-290">toocollect todos los contadores para el objeto de hello, especifique: `.*`.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="e3fbd-291">toocollect solo intercambio contadores de espacio para el objeto de memoria de hello, puede especificar:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="e3fbd-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="e3fbd-292">**Intervalo:**: Hola la frecuencia con que Hola se recopilan los contadores del objeto.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="e3fbd-293">configuración predeterminada de Hola para las métricas de rendimiento es:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-293">hello default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="e3fbd-294">Habilitación de los contadores de rendimiento de MySQL mediante comandos de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="e3fbd-295">Si el servidor MySQL o MariaDB se detecta en el equipo de hello cuando se instala el paquete de hello omsagent, se instala automáticamente un proveedor de MySQL Server de supervisión de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="e3fbd-296">Este proveedor conecta el estadísticas de rendimiento para tooexpose el local servidor MySQL/MariaDB toohello.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="e3fbd-297">Tendrá que tooconfigure credenciales de usuario de MySQL para que hello proveedor pueda acceder Hola MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="e3fbd-298">toodefine una predeterminado cuenta de usuario de MySQL server de hello en localhost, Hola use el ejemplo de comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="e3fbd-299">archivo de credenciales de Hello debe ser legible por cuenta de hello omsagent.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="e3fbd-300">Se recomienda ejecutar comando de hello mycimprovauth como omsgent.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="e3fbd-301">Como alternativa, puede especificar Hola requiere credenciales de MySQL en un archivo, mediante la creación de archivo hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Para obtener más información acerca de cómo administrar las credenciales de MySQL para la supervisión a través del archivo mysql-auth de hello, consulte [MySQL administrar credenciales en el archivo de autenticación de hello de supervisión](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="e3fbd-302">Vea [permisos necesarios para los contadores de rendimiento de MySQL de la base de datos](#database-permissions-required-for-mysql-performance-counters) para obtener más información acerca de los permisos de objeto requeridos por toocollect de usuario de MySQL de hello datos de rendimiento del servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="e3fbd-303">Habilitación de los contadores de rendimiento del servidor HTTP de Apache mediante comandos de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="e3fbd-304">Si se detecta servidor HTTP Apache en el equipo de hello cuando se instala el paquete de hello omsagent, se instala automáticamente un proveedor para el servidor HTTP Apache de supervisión de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="e3fbd-305">Este proveedor se basa en un "módulo" Apache que debe cargarse en hello servidor HTTP Apache orden tooaccess los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="e3fbd-306">Puede cargar el módulo de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="e3fbd-307">toounload Hola supervisión módulo Apache, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="e3fbd-308">datos de rendimiento de tooview con análisis de registros</span><span class="sxs-lookup"><span data-stu-id="e3fbd-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="e3fbd-309">En el portal de Operations Management Suite hello, haga clic en el icono de búsqueda de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="e3fbd-310">En la barra de búsqueda de hello, escriba `* (Type=Perf)` tooview todos los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="e3fbd-311">Dado que OMS también recopila datos del contador de rendimiento de Windows, debe acotar Hola datos tooLinux específicos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="e3fbd-312">Por lo tanto, hello en el ejemplo siguiente se mostraría servidor rendimiento datos específicos tooan ejemplo Linux denominado Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![servidor de ejemplo que se muestra en los resultados de búsqueda](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="e3fbd-314">En los resultados de hello, puede hacer clic en **métricas** contadores de hello tooview que se recopilaron datos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="e3fbd-315">Se muestran los datos en tiempo real como gráficos para cada contador.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-315">Real-time data is shown as graphs for each counter.</span></span>

![Métricas](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="e3fbd-317">syslog</span><span class="sxs-lookup"><span data-stu-id="e3fbd-317">Syslog</span></span>
<span data-ttu-id="e3fbd-318">Syslog es un protocolo similar tooWindows registros de eventos de registro de eventos: ambos funcionan de forma parecida al mostrarse en OMS.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="e3fbd-319">tooadd una nueva utilidad syslog de Linux en OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="e3fbd-320">En hello **configuración** página en **datos** , haga clic en **Syslog** y, a continuación, toohello izquierda del icono de más hello, escriba Hola nombre de utilidad syslog de Hola que desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="e3fbd-321">![Syslog de Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="e3fbd-322">Si no sabe el nombre completo de Hola de utilidad de hello, puede empezar a escribir un nombre parcial y aparecerá una lista de las utilidades syslog disponibles.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="e3fbd-323">Cuando encuentre la utilidad syslog de hello desea tooadd, haga clic en nombre de hello en lista de hello y, a continuación, haga clic en hello más hello de icono tooadd utilidad syslog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="e3fbd-324">Después de agregar aparece en la lista de Hola de utilidad de hello, resaltado con una barra de color.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="e3fbd-325">A continuación, seleccione los niveles de gravedad de hello (categorías de información de la utilidad syslog) que desea toocollect.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="e3fbd-326">En la parte inferior de Hola de página de hello haga clic en **guardar** toofinalize los cambios.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="e3fbd-327">cambios de configuración de Hola que haya hecho, a continuación, se envían tooall Hola agentes de OMS para Linux registrados con OMS, normalmente en 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="e3fbd-328">Configuración de las utilidades de Syslog de Linux en Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="e3fbd-329">Eventos de syslog se envían desde el demonio de syslog hello, por ejemplo rsyslog o syslog-ng, puerto local tooa ese Hola agente está escuchando.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="e3fbd-330">De forma predeterminada al puerto 25224.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-330">By default, port 25224.</span></span> <span data-ttu-id="e3fbd-331">Cuando se instala el agente de hello, se aplica una configuración de syslog predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="e3fbd-332">Esto se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-332">This is found at:</span></span>

<span data-ttu-id="e3fbd-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="e3fbd-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="e3fbd-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="e3fbd-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="e3fbd-335">configuración de syslog de agente OMS de Hello predeterminado carga eventos syslog desde todas las utilidades con una gravedad de advertencia o superior.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="e3fbd-336">Si modifica la configuración de syslog hello, debe reiniciar el demonio de syslog Hola Hola cambios tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="e3fbd-337">Hola syslog configuración predeterminada para hello agente de OMS para Linux para OMS es:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="e3fbd-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="e3fbd-338">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="e3fbd-339">Syslog ng</span><span class="sxs-lookup"><span data-stu-id="e3fbd-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="e3fbd-340">tooview todos los eventos de Syslog con análisis de registros</span><span class="sxs-lookup"><span data-stu-id="e3fbd-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="e3fbd-341">En el portal de Operations Management Suite hello, haga clic en hello **Log Search** icono.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="e3fbd-342">Hola **administración de registros** agrupación, elija una búsqueda de syslog predefinida y, a continuación, seleccione una toorun.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="e3fbd-343">Este ejemplo muestra todos los eventos de Syslog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-343">This example shows all Syslog events.</span></span>

![Eventos de Syslog que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="e3fbd-345">Ahora puede profundizar en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="e3fbd-346">Alertas de Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-346">Linux alerts</span></span>
<span data-ttu-id="e3fbd-347">Si usa Nagios o Zabbix toomanage los equipos Linux, a continuación, OMS puede recibir alertas de hello generadas desde esas herramientas.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="e3fbd-348">Sin embargo, no hay actualmente ningún método tooconfigure datos entrantes de alerta mediante el portal de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="e3fbd-349">En su lugar, deberá tooedit un tooOMS envío de alertas de configuración archivo toostart.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="e3fbd-350">Recopilación de alertas de Nagios</span><span class="sxs-lookup"><span data-stu-id="e3fbd-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="e3fbd-351">toocollect las alertas de un servidor Nagios, debe hello toomake después de los cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="e3fbd-352">Usuario de hello GRANT **omsagent** archivo de registro de acceso de lectura toohello Nagios (es decir, /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="e3fbd-353">Suponiendo que el archivo de hello nagios.log es propiedad de grupo hello **nagios** , puede agregar el usuario hello **omsagent** toohello **nagios** grupo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="e3fbd-354">Modificar el archivo de hello omsagent.confconfiguration (/ etcetera/opt/microsoft/omsagent/&lt;Id. de área de trabajo&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="e3fbd-355">Asegúrese de hello siguiendo las entradas está presentes y no comentadas:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="e3fbd-356">Reiniciar el demonio omsagent hello:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="e3fbd-357">Recopilación de alertas de Zabbix</span><span class="sxs-lookup"><span data-stu-id="e3fbd-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="e3fbd-358">toocollect las alertas de un servidor Zabbix, se llevarán a cabo similar toothose pasos anteriores para Nagios, salvo que deberá toospecify un usuario y una contraseña en *borre el texto*.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="e3fbd-359">No es una solución ideal, pero seguramente cambiará pronto.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="e3fbd-360">tooaddress este problema, recomendamos que cree el usuario de Hola y conceder permiso toomonitor solo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="e3fbd-361">Una sección de ejemplo de archivo de configuración de hello omsagent.conf (/ etcetera/opt/microsoft/omsagent/&lt;Id. de área de trabajo&gt;/conf/omsagent.conf) para Zabbix debe ser similar a la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="e3fbd-362">Visualización de alertas en búsqueda de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e3fbd-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="e3fbd-363">Después de haber configurado el tooOMS de las alertas de toosend de equipos Linux, puede usar alertas de Hola de tooview consultas de búsqueda de registro simples unos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="e3fbd-364">Hello siguiente ejemplo de consulta de búsqueda devuelve todas las alertas de hello registrado que se generaron.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="e3fbd-365">Por ejemplo, si se produce algún tipo de problema en su infraestructura de TI, a continuación, resultados para hello siguiente ejemplo de consulta podría indicar dónde puede originarse problema Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="e3fbd-366">Y puede rastrear fácilmente en las alertas de toohello por toohelp de sistema de origen estrecha la investigación.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="e3fbd-367">Hello ventaja es que no tiene necesariamente toogo toovarious los sistemas de administración de inicio de hello, siempre que las alertas se envíen tooOMS, puede empezar por ahí.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="e3fbd-368">tooview Nagios todas las alertas con análisis de registros</span><span class="sxs-lookup"><span data-stu-id="e3fbd-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="e3fbd-369">En el portal de Operations Management Suite hello, haga clic en hello **Log Search** icono.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="e3fbd-370">En la barra de consulta de hello, escriba Hola después de consulta de búsqueda</span><span class="sxs-lookup"><span data-stu-id="e3fbd-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertas de Nagios que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="e3fbd-372">Después de ver los resultados de búsqueda de hello, puede profundizar en los detalles adicionales, como *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="e3fbd-373">tooview todas las alertas de Zabbix con análisis de registros</span><span class="sxs-lookup"><span data-stu-id="e3fbd-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="e3fbd-374">En el portal de Operations Management Suite hello, haga clic en hello **Log Search** icono.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="e3fbd-375">En la barra de consulta de hello, escriba Hola después de consulta de búsqueda</span><span class="sxs-lookup"><span data-stu-id="e3fbd-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertas de Zabbix que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="e3fbd-377">Después de ver los resultados de búsqueda de hello, puede profundizar en los detalles adicionales, como *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="e3fbd-378">Compatibilidad con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="e3fbd-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="e3fbd-379">Hola agente de OMS para Linux comparte archivos binarios del agente con el agente de System Center Operations Manager de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="e3fbd-380">Instalar Hola agente de OMS para Linux en un sistema administrado por Operations Manager actualizaciones Hola paquetes OMI y SCX versión más reciente de hello equipo tooa.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="e3fbd-381">Hola agente de OMS para Linux y System Center 2012 R2 son compatibles.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="e3fbd-382">Sin embargo, **System Center 2012 SP1 y versiones anteriores no son actualmente compatibles con hello agente de OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="e3fbd-383">Si Hola agente de OMS para Linux está instalado tooa equipo que no está administrado actualmente por Operations Manager y posteriormente desea toomanage equipo de hello con Operations Manager, debe modificar configuración de OMI Hola antes de detectar el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="e3fbd-384">**Este paso no es necesario si el agente de Operations Manager Hola está instalado antes de hello agente de OMS para Linux.**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="e3fbd-385">Hola tooenable agente de OMS para Linux toocommunicate con Operations Manager</span><span class="sxs-lookup"><span data-stu-id="e3fbd-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="e3fbd-386">Editar Hola archivo /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="e3fbd-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="e3fbd-387">Asegúrese de que Hola línea que comienza con **httpsport =** define Hola puerto 1270.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="e3fbd-388">Por ejemplo `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="e3fbd-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="e3fbd-389">Reinicie el servidor de OMI de hello:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="e3fbd-390">Permisos necesarios de la base de datos para los contadores de rendimiento de MySQL</span><span class="sxs-lookup"><span data-stu-id="e3fbd-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="e3fbd-391">toogrant usuario de supervisión de MySQL de permisos tooa, debe tener concediendo al usuario Hola Hola privilegio 'GRANT option', así como tener concedido el privilegio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="e3fbd-392">En orden para el usuario de MySQL hello tooreturn rendimiento datos Hola usuario necesita tener acceso toohello las siguientes consultas:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="e3fbd-393">Además usuario de MySQL toothese consultas Hola requiere toohello acceso exclusivo siguientes tablas predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="e3fbd-394">information_schema</span><span class="sxs-lookup"><span data-stu-id="e3fbd-394">information_schema</span></span>
* <span data-ttu-id="e3fbd-395">mysql</span><span class="sxs-lookup"><span data-stu-id="e3fbd-395">mysql</span></span>

<span data-ttu-id="e3fbd-396">Estos privilegios se pueden conceder ejecutando Hola siguientes comandos de concesión.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="e3fbd-397">Administrar credenciales en el archivo de autenticación de hello de supervisión de MySQL</span><span class="sxs-lookup"><span data-stu-id="e3fbd-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="e3fbd-398">Hola siguientes secciones lo administra las credenciales de MySQL.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="e3fbd-399">Configurar Hola proveedor de OMI de MySQL</span><span class="sxs-lookup"><span data-stu-id="e3fbd-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="e3fbd-400">Hola proveedor de OMI de MySQL necesita un usuario de MySQL preconfigurado e instala las bibliotecas de cliente de MySQL en información de rendimiento y mantenimiento de pedidos tooquery Hola de instancia de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="e3fbd-401">Archivo de autenticación de MySQL para OMI</span><span class="sxs-lookup"><span data-stu-id="e3fbd-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="e3fbd-402">Proveedor de OMI de MySQL usa un toodetermine del archivo de autenticación qué instancia de MySQL Hola dirección de enlace y el puerto está escuchando en así como las credenciales toouse toogather métricas.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="e3fbd-403">Durante el saludo de instalación de OMI de MySQL proveedor examinará los archivos de configuración my.cnf de MySQL (ubicaciones predeterminadas) para la dirección de enlace y puerto parcialmente conjunto hello y archivo de autenticación de OMI de MySQL.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="e3fbd-404">toocomplete la supervisión de una instancia del servidor MySQL, agregue un archivo de autenticación de OMI de MySQL pregenerado en el directorio correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="e3fbd-405">Formato del archivo de autenticación</span><span class="sxs-lookup"><span data-stu-id="e3fbd-405">Authentication file format</span></span>
<span data-ttu-id="e3fbd-406">Hola archivo de autenticación de OMI de MySQL es un archivo de texto que contiene información sobre:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="e3fbd-407">Port</span><span class="sxs-lookup"><span data-stu-id="e3fbd-407">Port</span></span>
* <span data-ttu-id="e3fbd-408">Dirección de enlace</span><span class="sxs-lookup"><span data-stu-id="e3fbd-408">Bind-Address</span></span>
* <span data-ttu-id="e3fbd-409">Nombre de usuario de MySQL</span><span class="sxs-lookup"><span data-stu-id="e3fbd-409">MySQL username</span></span>
* <span data-ttu-id="e3fbd-410">Contraseña codificada en Base64</span><span class="sxs-lookup"><span data-stu-id="e3fbd-410">Base64 encoded password</span></span>

<span data-ttu-id="e3fbd-411">Hola archivo de autenticación de OMI de MySQL solo concede privilegios de usuario de Linux toohello de lectura/escritura que lo generó.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="e3fbd-412">Un archivo de autenticación de OMI de MySQL predeterminado contiene una instancia predeterminada y un número de puerto según la información disponible y analizada desde Hola que se encontró el archivo de configuración de MySQL.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="e3fbd-413">instancia predeterminada de Hello es un toomake significa administrar varias instancias de MySQL en un host Linux y se indica mediante la instancia de hello con el puerto 0.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="e3fbd-414">Todas las instancias agregadas heredarán propiedades establecidas en la instancia predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="e3fbd-415">Por ejemplo, si se agrega la instancia de MySQL que escucha en el puerto '3308', dirección de enlace, nombre de usuario y contraseña codificada en Base64 de instancia predeterminada de Hola se puede tootry usado y supervisar la instancia de hello escucha en 3308.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="e3fbd-416">Si instancia hello en 3308 está enlazado tooanother dirección y usa Hola el mismo nombre de usuario de MySQL y par de contraseña solo Hola volver a especificar de Hola se necesita la dirección de enlace y hello otras propiedades se heredarán.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="e3fbd-417">Hola autenticación ejemplos de archivos de siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="e3fbd-418">Instancia predeterminada e instancia con el puerto 3308:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="e3fbd-419">Instancia predeterminada e instancia con el puerto 3308 + diferente contraseña codificada en Base 64:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="e3fbd-420">**Propiedad**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-420">**Property**</span></span> | <span data-ttu-id="e3fbd-421">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e3fbd-422">Port</span><span class="sxs-lookup"><span data-stu-id="e3fbd-422">Port</span></span> |<span data-ttu-id="e3fbd-423">El puerto representa Hola Hola de puerto actual instancia de MySQL está escuchando.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="e3fbd-424">puerto de Hello 0 implica que se usan las propiedades de hello siguientes para la instancia predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="e3fbd-425">Dirección de enlace</span><span class="sxs-lookup"><span data-stu-id="e3fbd-425">Bind-Address</span></span> |<span data-ttu-id="e3fbd-426">Hola dirección de enlace es Hola actual MySQL dirección de enlace</span><span class="sxs-lookup"><span data-stu-id="e3fbd-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="e3fbd-427">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="e3fbd-427">username</span></span> |<span data-ttu-id="e3fbd-428">Este nombre de usuario de Hola de usuario de MySQL Hola desea instancia del servidor de MySQL de toouse toomonitor Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="e3fbd-429">Contraseña codificada en Base64</span><span class="sxs-lookup"><span data-stu-id="e3fbd-429">Base64 encoded Password</span></span> |<span data-ttu-id="e3fbd-430">Esta es la contraseña de Hola Hola MySQL supervisión del usuario de codificada en Base64.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="e3fbd-431">Actualización automática</span><span class="sxs-lookup"><span data-stu-id="e3fbd-431">AutoUpdate</span></span> |<span data-ttu-id="e3fbd-432">Cuando se actualiza el proveedor de OMI de MySQL Hola Hola proveedor a examinar los cambios en el archivo my.cnf de hello y sobrescribir el archivo de autenticación de OMI de MySQL Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="e3fbd-433">Establecer este indicador tootrue o false, según las actualizaciones necesarias toohello OMI de MySQL archivo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="e3fbd-434">Ubicación del archivo de autenticación</span><span class="sxs-lookup"><span data-stu-id="e3fbd-434">Authentication file location</span></span>
<span data-ttu-id="e3fbd-435">Hola archivo de autenticación de OMI de MySQL debe ser había ubicado en hello ubicación siguiente y con el nombre "mysql-auth":</span><span class="sxs-lookup"><span data-stu-id="e3fbd-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="e3fbd-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="e3fbd-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="e3fbd-437">archivo Hello (y el directorio auth/omsagent) debería pertenecer al usuario omsagent de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="e3fbd-438">Registros del agente</span><span class="sxs-lookup"><span data-stu-id="e3fbd-438">Agent logs</span></span>
<span data-ttu-id="e3fbd-439">registros de Hola para hello agente de OMS para Linux está en:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="e3fbd-440">/var/opt/microsoft/omsagent/&lt;identificador de área de trabajo&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="e3fbd-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="e3fbd-441">registros de Hola para hello agente de OMS para Linux para el programa omsconfig (configuración del agente) está en:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="e3fbd-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="e3fbd-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="e3fbd-443">Los registros de componentes OMI y SCX hello (que proporcionan datos de métricas de rendimiento) está en:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="e3fbd-444">/var/opt/omi/log/ y /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="e3fbd-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="e3fbd-445">Solución de problemas de hello agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="e3fbd-446">Usar hello después toodiagnose de información y solucionar problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="e3fbd-447">Si ninguno de hello, solución de problemas de información de esta sección le ayuda a, también puede usar Hola después recursos toohelp resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="e3fbd-448">Los clientes con soporte técnico Premier pueden registrar un caso de soporte técnico mediante [Premier](https://premier.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="e3fbd-449">Los clientes con contratos de soporte técnico de Azure pueden registrarse casos de soporte técnico hello [portal de Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="e3fbd-450">Registre un [problema de GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="e3fbd-451">Foro de comentarios para ideas y un informe de errores de toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="e3fbd-452">Ubicación de registros importantes</span><span class="sxs-lookup"><span data-stu-id="e3fbd-452">Important log locations</span></span>
| <span data-ttu-id="e3fbd-453">Archivo</span><span class="sxs-lookup"><span data-stu-id="e3fbd-453">File</span></span> | <span data-ttu-id="e3fbd-454">Ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="e3fbd-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="e3fbd-455">Archivo de registro del agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="e3fbd-456">Archivo de registro de la configuración del agente de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="e3fbd-457">Archivos de configuración importantes</span><span class="sxs-lookup"><span data-stu-id="e3fbd-457">Important configuration files</span></span>
| <span data-ttu-id="e3fbd-458">Categoría</span><span class="sxs-lookup"><span data-stu-id="e3fbd-458">Catergory</span></span> | <span data-ttu-id="e3fbd-459">Ubicación del archivo</span><span class="sxs-lookup"><span data-stu-id="e3fbd-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="e3fbd-460">syslog</span><span class="sxs-lookup"><span data-stu-id="e3fbd-460">Syslog</span></span> |<span data-ttu-id="e3fbd-461">`/etc/syslog-ng/syslog-ng.conf`, `/etc/rsyslog.conf` o `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="e3fbd-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="e3fbd-462">Rendimiento, Nagios, Zabbix, salida de OMS y agente general</span><span class="sxs-lookup"><span data-stu-id="e3fbd-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="e3fbd-463">Configuraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="e3fbd-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="e3fbd-464">Los archivos de configuración de los contadores de rendimiento y Syslog se sobrescriben si se habilita la configuración del portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="e3fbd-465">Puede deshabilitar la configuración de hello Portal de OMS (para todos los nodos) o para los nodos únicos ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="e3fbd-466">Habilitación del registro de depuración</span><span class="sxs-lookup"><span data-stu-id="e3fbd-466">Enable debug logging</span></span>
<span data-ttu-id="e3fbd-467">depuración de tooenable registro, puede utilizar el complemento de salida de hello OMS y un resultado detallado.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="e3fbd-468">Complemento de salida de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-468">OMS output plugin</span></span>
<span data-ttu-id="e3fbd-469">FluentD permite Hola complemento toospecify niveles de registro para los niveles de registro diferente para las entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="e3fbd-470">toospecify un nivel de registro diferente para la salida OMS, editar configuración de agente general de Hola Hola `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` archivo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="e3fbd-471">Cerca de la parte inferior de Hola Hola del archivo de configuración, cambiar hello `log_level` propiedad de `info` demasiado`debug`.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

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

<span data-ttu-id="e3fbd-472">El registro de depuración permite toosee por lotes cargas toohello servicio de OMS separado por tipo, el número de elementos de datos y el tiempo que tarda toosend.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="e3fbd-473">*Ejemplo de registro con depuración habilitada:*</span><span class="sxs-lookup"><span data-stu-id="e3fbd-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="e3fbd-474">Salida detallada</span><span class="sxs-lookup"><span data-stu-id="e3fbd-474">Verbose output</span></span>
<span data-ttu-id="e3fbd-475">En lugar de usar el complemento de salida de hello OMS, también puede generar elementos de datos directamente demasiado`stdout`, que es visible en hello agente de OMS para el archivo de registro de Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="e3fbd-476">En el archivo de configuración de agente general de OMS de hello en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comente Hola OMS salida complemento agregando un `#` delante de cada línea.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="e3fbd-477">A continuación Hola complemento de salida, quitar comentario Hola Hola pasos de la sección quitando hello `#` símbolos al principio de Hola de cada línea.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="e3fbd-478">Mensajes de Syslog reenviados no aparecen en el registro de hello</span><span class="sxs-lookup"><span data-stu-id="e3fbd-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-479">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-479">Probable causes</span></span>
* <span data-ttu-id="e3fbd-480">Hola configuración aplicada toohello Linux servidor no permita la recopilación de instalaciones de hello enviado o niveles de registro</span><span class="sxs-lookup"><span data-stu-id="e3fbd-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="e3fbd-481">Syslog no reenviar correctamente toohello Linux server</span><span class="sxs-lookup"><span data-stu-id="e3fbd-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="e3fbd-482">número de Hola de mensajes que se le reenvían por segundo es demasiado grande para la configuración básica de Hola de hello agente de OMS para Linux toohandle</span><span class="sxs-lookup"><span data-stu-id="e3fbd-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e3fbd-483">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-483">Resolutions</span></span>
* <span data-ttu-id="e3fbd-484">Compruebe que la configuración de Hola Hola Portal de OMS de Syslog tiene todas las instalaciones de Hola y niveles de registro correcto de Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="e3fbd-485">**Portal de OMS &gt; Configuración &gt; Datos &gt; Syslog**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="e3fbd-486">Compruebe que syslog nativo daemons de mensajería (`rsyslog`, `syslog-ng`) es tooreceive capaz de mensajes de saludo reenviado</span><span class="sxs-lookup"><span data-stu-id="e3fbd-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="e3fbd-487">Compruebe la configuración de firewall en los que no se bloquean los mensajes de Hola Syslog server tooensure</span><span class="sxs-lookup"><span data-stu-id="e3fbd-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="e3fbd-488">Simular un tooOMS de mensaje de Syslog mediante hello `logger` comando: por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="e3fbd-489">Problemas de conexión tooOMS cuando usa un proxy</span><span class="sxs-lookup"><span data-stu-id="e3fbd-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-490">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-490">Probable causes</span></span>
* <span data-ttu-id="e3fbd-491">proxy Hola especificó al instalar y configurar el agente de Hola es incorrecto</span><span class="sxs-lookup"><span data-stu-id="e3fbd-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="e3fbd-492">los puntos de conexión de servicio de OMS de Hello no son whitelistested en su centro de datos</span><span class="sxs-lookup"><span data-stu-id="e3fbd-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e3fbd-493">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-493">Resolutions</span></span>
* <span data-ttu-id="e3fbd-494">Reinstalar Hola agente de OMS para Linux mediante el siguiente comando con la opción de Hola de hello `-v` habilitado.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="e3fbd-495">Esto permite que un resultado detallado del agente de hello conexión a través de proxy de hello toohello servicio de OMS.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="e3fbd-496">Revise la documentación de hello para el proxy OMS en [configurar agente de Hola para su uso con un servidor proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="e3fbd-497">Compruebe que Hola siguiendo los puntos de conexión de servicio de OMS están en la lista blanca</span><span class="sxs-lookup"><span data-stu-id="e3fbd-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="e3fbd-498">Recurso del agente</span><span class="sxs-lookup"><span data-stu-id="e3fbd-498">Agent Resource</span></span> | <span data-ttu-id="e3fbd-499">Puertos</span><span class="sxs-lookup"><span data-stu-id="e3fbd-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="e3fbd-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e3fbd-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="e3fbd-501">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="e3fbd-501">Port 443</span></span> |
| <span data-ttu-id="e3fbd-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e3fbd-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="e3fbd-503">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="e3fbd-503">Port 443</span></span> |
| <span data-ttu-id="e3fbd-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="e3fbd-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="e3fbd-505">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="e3fbd-505">Port 443</span></span> |
| <span data-ttu-id="e3fbd-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="e3fbd-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="e3fbd-507">Puerto 443</span><span class="sxs-lookup"><span data-stu-id="e3fbd-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="e3fbd-508">Se muestra un error 403 durante la incorporación</span><span class="sxs-lookup"><span data-stu-id="e3fbd-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-509">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-509">Probable causes</span></span>
* <span data-ttu-id="e3fbd-510">Hola fecha y hora no son correctos en el servidor Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="e3fbd-511">Hola Id. de área de trabajo y la clave de área de trabajo utilizados son incorrectas</span><span class="sxs-lookup"><span data-stu-id="e3fbd-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="e3fbd-512">Resolución</span><span class="sxs-lookup"><span data-stu-id="e3fbd-512">Resolution</span></span>
* <span data-ttu-id="e3fbd-513">Comprobar tiempo de hello en el servidor Linux con hello `date` comando.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="e3fbd-514">Si Hola datos están superior o inferior a 15 minutos de hello hora actual, incorporación produce un error.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="e3fbd-515">toocorrect, actualizar la fecha de Hola o zona horaria del servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="e3fbd-516">versión más reciente de Hola de hello agente de OMS para Linux le notifica si una diferencia de tiempo está causando el error de incorporación</span><span class="sxs-lookup"><span data-stu-id="e3fbd-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="e3fbd-517">Realizar la incorporación RE mediante Hola correcto de Id. de área de trabajo y la clave de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="e3fbd-518">Vea [incorporación mediante la línea de comandos de hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="e3fbd-519">Aparecerá un error 500 o error 404 en archivo de registro de hello después de la incorporación</span><span class="sxs-lookup"><span data-stu-id="e3fbd-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="e3fbd-520">Se trata de un problema conocido que se produce durante el saludo primera carga de datos de Linux en un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="e3fbd-521">Esto no afecta a los datos que se envían ni causa otros problemas.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="e3fbd-522">Puede pasar por alto los errores de hello cuando inicialmente la incorporación.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="e3fbd-523">Datos de Nagios no aparezcan en hello Portal de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-524">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-524">Probable causes</span></span>
* <span data-ttu-id="e3fbd-525">Hola omsagent usuario no tiene permisos tooread de archivo de registro de Nagios Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="e3fbd-526">Hola Nagios origen y las secciones del filtro todavía incluyen comentarios en archivo de hello omsagent.conf</span><span class="sxs-lookup"><span data-stu-id="e3fbd-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e3fbd-527">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-527">Resolutions</span></span>
* <span data-ttu-id="e3fbd-528">Agregar usuario omsagent de Hola en orden tooread del archivo de Nagios Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="e3fbd-529">Consulte [Nagios Alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Alertas de Nagios) para más información.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="e3fbd-530">En hello agente de OMS para el archivo de configuración general de Linux en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, asegúrese de que **ambos** Hola Nagios secciones de origen y de filtro tienen comentarios quitados, toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="e3fbd-531">Los datos de Linux no aparecen en el Portal de OMS Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-532">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-532">Probable causes</span></span>
* <span data-ttu-id="e3fbd-533">Error de servicio de OMS de incorporación toohello</span><span class="sxs-lookup"><span data-stu-id="e3fbd-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="e3fbd-534">Toohello de conexión que se bloquea el servicio de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="e3fbd-535">Hola agente de OMS para los datos de Linux es copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="e3fbd-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e3fbd-536">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-536">Resolutions</span></span>
* <span data-ttu-id="e3fbd-537">Comprobar que toohello incorporación servicio de OMS se realizó correctamente comprobando que hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="e3fbd-538">Realizar la incorporación RE mediante Hola omsadmin.sh línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="e3fbd-539">Vea [incorporación mediante la línea de comandos de hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="e3fbd-540">Si utiliza a un proxy, use anterior de pasos para solucionar problemas de proxy de Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="e3fbd-541">En algunos casos, cuando Hola agente de OMS para Linux no puede comunicarse con servicio de OMS, Hola datos en hello agente son toohello de copia de seguridad de tamaño de búfer lleno de 50 MB.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="e3fbd-542">Reinicie Hola agente de OMS para Linux mediante la ejecución de hello `/opt/microsoft/omsagent/bin/service_control restart` comando.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="e3fbd-543">Este problema está corregido en el agente versión 1.1.0-28 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="e3fbd-544">Configuración de contador de rendimiento de Syslog Linux no se aplica en el portal de OMS Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-545">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-545">Probable causes</span></span>
* <span data-ttu-id="e3fbd-546">agente de configuración de Hola Hola agente de OMS para Linux no recuperado configuración más reciente de Hola Hola portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="e3fbd-547">Hello configuración modificada en el portal de hello no se aplicaron</span><span class="sxs-lookup"><span data-stu-id="e3fbd-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e3fbd-548">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-548">Resolutions</span></span>
<span data-ttu-id="e3fbd-549">`omsconfig`es el agente de configuración de Hola Hola agente de OMS para Linux que recupera los cambios de configuración del portal de OMS cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="e3fbd-550">Esta configuración es aplicado toohello agente de OMS para archivos de configuración de Linux que se encuentra en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="e3fbd-551">En algunos casos, hello agente de OMS para el agente de configuración de Linux no sea capaz de toocommunicate con el servicio de configuración del portal de hello resultante en la configuración más reciente no se aplican.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="e3fbd-552">Compruebe que hello `omsconfig` agente se instala con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="e3fbd-553">`dpkg --list omsconfig` o `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="e3fbd-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="e3fbd-554">Si no está instalado, volver a instalar versión más reciente de Hola de hello agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="e3fbd-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="e3fbd-555">Compruebe que hello `omsconfig` agente pueda comunicarse con hello servicio de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="e3fbd-556">Ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando</span><span class="sxs-lookup"><span data-stu-id="e3fbd-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="e3fbd-557">Hello comando anterior devuelve Hola configuración que el agente recupera del portal de hello, incluida la configuración de Syslog, los contadores de rendimiento de Linux y los registros personalizados</span><span class="sxs-lookup"><span data-stu-id="e3fbd-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="e3fbd-558">Si se produce un error en el comando hello arriba, ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="e3fbd-559">Este comando fuerza hello omsconfig agente toocommunicate con la configuración más reciente de hello OMS servicio tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="e3fbd-560">Los datos de registro personalizados de Linux no aparecen en hello Portal de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="e3fbd-561">Causas probables</span><span class="sxs-lookup"><span data-stu-id="e3fbd-561">Probable causes</span></span>
* <span data-ttu-id="e3fbd-562">Error del servicio de incorporación tooOMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="e3fbd-563">Hola **Hola aplicar después configuración toomy servidores Linux** no se ha seleccionado la configuración</span><span class="sxs-lookup"><span data-stu-id="e3fbd-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="e3fbd-564">omsconfig no ha recogido de registro personalizada más reciente de Hola desde el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="e3fbd-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="e3fbd-565">Hola `omsagent` uso es registro personalizado de hello tooaccess no se puede debido a problemas de permisos de tooa o `omsagent` no se encontró.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="e3fbd-566">En este caso, verá Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="e3fbd-567">Se trata de un problema conocido con hello condición de carrera que se corrigió en hello agente de OMS para Linux versión 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="e3fbd-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="e3fbd-568">Soluciones</span><span class="sxs-lookup"><span data-stu-id="e3fbd-568">Resolutions</span></span>
* <span data-ttu-id="e3fbd-569">Compruebe que ha incorporado, ha sido correctamente mediante la determinación de si hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` archivo existe.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="e3fbd-570">Si fuera necesario, incorporar con línea de comandos de omsadmin.sh de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="e3fbd-571">Vea [incorporación mediante la línea de comandos de hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="e3fbd-572">En hello en el Portal de OMS, **configuración** en hello **datos** , asegúrese de que hello **Hola aplicar después configuración toomy servidores Linux** está seleccionada</span><span class="sxs-lookup"><span data-stu-id="e3fbd-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="e3fbd-573">![Aplicar configuración](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="e3fbd-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="e3fbd-574">Compruebe que hello `omsconfig` agente pueda comunicarse con hello servicio de OMS</span><span class="sxs-lookup"><span data-stu-id="e3fbd-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="e3fbd-575">Ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando</span><span class="sxs-lookup"><span data-stu-id="e3fbd-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="e3fbd-576">Hello comando anterior devuelve Hola configuración que el agente recupera del Hola Portal, incluida la configuración de Syslog, los contadores de rendimiento de Linux y los registros personalizados</span><span class="sxs-lookup"><span data-stu-id="e3fbd-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="e3fbd-577">Si se produce un error en el comando hello arriba, ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="e3fbd-578">Este comando fuerza hello omsconfig agente toocommunicate con el servicio OMS y recuperar la configuración más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="e3fbd-579">En lugar de hello agente de OMS para ejecutarse como un usuario con privilegios de usuario de Linux `root`, Hola agente de OMS para Linux se ejecuta como hello `omsagent` usuario.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="e3fbd-580">En la mayoría de los casos, debe tener permiso explícito concedidos usuario toohello en orden tooread determinados archivos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="e3fbd-581">permiso de toogrant demasiado`omsagent` usuario, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="e3fbd-582">Agregar hello `omsagent` grupo específico de usuarios tooa con`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="e3fbd-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="e3fbd-583">Conceder acceso de lectura universal toohello archivo necesario con`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="e3fbd-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="e3fbd-584">Hay un problema conocido con la condición de carrera que se corrigió en hello agente de OMS para Linux versión 1.1.0-217 Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="e3fbd-585">Después de actualizar el agente de toohello más reciente, ejecute hello después de la versión más reciente Hola de comando tooget de complemento de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="e3fbd-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="e3fbd-586">Limitaciones conocidas</span><span class="sxs-lookup"><span data-stu-id="e3fbd-586">Known limitations</span></span>
<span data-ttu-id="e3fbd-587">Revise Hola después toolearn secciones sobre las limitaciones actuales de hello agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="e3fbd-588">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="e3fbd-588">Azure Diagnostics</span></span>
<span data-ttu-id="e3fbd-589">Para las máquinas virtuales de Linux ejecuta en Azure, pasos adicionales pueden ser tooallow requiere recopilación de datos mediante Diagnósticos de Azure y Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="e3fbd-590">**Versión 2.2** de hello extensión de diagnósticos para Linux es necesaria para la compatibilidad con hello agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="e3fbd-591">Para obtener más información sobre cómo instalar y configurar Hola extensión de diagnósticos para Linux, consulte [usar tooenable de comando de CLI de Azure de hello extensión de diagnóstico de Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="e3fbd-592">**Actualización de hello extensión de diagnósticos de Linux de 2.0 too2.2 ASM de la CLI de Azure:**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="e3fbd-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="e3fbd-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="e3fbd-594">Estos ejemplos de comandos hacen referencia a un archivo denominado PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="e3fbd-595">formato Hola de ese archivo debe parecerse al siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="e3fbd-596">Sysklog no se admite.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-596">Sysklog is not supported</span></span>
<span data-ttu-id="e3fbd-597">Rsyslog o syslog-ng es necesario toocollect mensajes de syslog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="e3fbd-598">demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="e3fbd-599">toocollect datos de syslog de esta versión de las distribuciones, Hola rsyslog daemon debe estar instalado y configurado tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="e3fbd-600">Para obtener más información sobre cómo sustituir sysklog por rsyslog, consulte [instalar Hola recién creado rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="e3fbd-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3fbd-601">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e3fbd-601">Next Steps</span></span>
* <span data-ttu-id="e3fbd-602">[Adición de soluciones de análisis de registros desde la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad y recopilar datos.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="e3fbd-603">Familiarizarse con [búsquedas de registro](log-analytics-log-searches.md) tooview detallada información recopilada por soluciones.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="e3fbd-604">Use [paneles](log-analytics-dashboards.md) toosave y mostrar busca en su propio personalizado.</span><span class="sxs-lookup"><span data-stu-id="e3fbd-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
