---
title: "Máquinas virtuales alta disponibilidad para SAP NetWeaver en SUSE Linux Enterprise Server para aplicaciones de SAP aaaAzure | Documentos de Microsoft"
description: "Guía de alta disponibilidad para SAP NetWeaver en SUSE Linux Enterprise Server para SAP Applications"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="cac26-103">Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="cac26-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="cac26-113">Este artículo describe cómo configurar las máquinas virtuales de hello toodeploy hello las máquinas virtuales, instalar el marco de trabajo de clúster de Hola e instalar un sistema SAP NetWeaver 7.50 alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cac26-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="cac26-114">En configuraciones de ejemplo de Hola, etcetera mediante comandos de instalación. se usa el número de instancia 00 de ASCS, el número de instancia 02 de ERS y NWS del identificador de sistema de SAP.</span><span class="sxs-lookup"><span data-stu-id="cac26-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="cac26-115">Hello nombres de recursos de hello (por ejemplo, las máquinas virtuales, redes virtuales) en el ejemplo de Hola se asume que ha utilizado hello [convergente plantilla] [ template-converged] con recursos SAP sistema identificador NWS toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="cac26-116">Hola de lectura siguientes notas de SAP y documentos en primer lugar</span><span class="sxs-lookup"><span data-stu-id="cac26-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="cac26-117">Nota de SAP [1928533], que incluye:</span><span class="sxs-lookup"><span data-stu-id="cac26-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="cac26-118">Lista de tamaños de máquina virtual de Azure que se admiten para la implementación de hello del software SAP.</span><span class="sxs-lookup"><span data-stu-id="cac26-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="cac26-119">Información importante sobre la capacidad para los tamaños de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="cac26-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="cac26-120">Software de SAP admitido y combinaciones de sistema operativo y base de datos</span><span class="sxs-lookup"><span data-stu-id="cac26-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="cac26-121">Versión del kernel de SAP requerida para Windows y Linux en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cac26-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="cac26-122">La nota de SAP [2015553] enumera los requisitos previos para las implementaciones de software de SAP admitidas por SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="cac26-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="cac26-123">La nota de SAP [2205917] contiene configuraciones recomendadas del sistema operativo para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="cac26-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cac26-124">La nota de SAP [1944799] contiene guías de SAP HANA para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="cac26-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="cac26-125">La nota de SAP [2178632] contiene información detallada sobre todas las métricas de supervisión notificadas para SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="cac26-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="cac26-126">Nota de SAP [2191498] Hola necesario versión del agente de Host de SAP para Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="cac26-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="cac26-127">La nota de SAP [2243692] incluye información acerca de las licencias de SAP en Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="cac26-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="cac26-128">La nota de SAP [1984787] incluye información general sobre SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="cac26-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="cac26-129">Nota de SAP [1999351] información adicional de solución de problemas de hello Azure extensión de supervisión mejorada para SAP.</span><span class="sxs-lookup"><span data-stu-id="cac26-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="cac26-130">La [WIKI de la comunidad SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene todas las notas de SAP que se necesitan para Linux.</span><span class="sxs-lookup"><span data-stu-id="cac26-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="cac26-131">[Planeación e implementación de Azure Virtual Machines para SAP en Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="cac26-132">[Implementación de Azure Virtual Machines para SAP en Linux (este artículo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="cac26-133">[Implementación de DBMS de Azure Virtual Machines para SAP en Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="cac26-134">[Escenario de rendimiento optimizado para la replicación del sistema de SAP HANA][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="cac26-135">Guía de Hello contiene todos los tooset de información necesaria la replicación del sistema de SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="cac26-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="cac26-136">Esta guía sirve como orientación.</span><span class="sxs-lookup"><span data-stu-id="cac26-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="cac26-137">[Alta el almacenamiento de NFS disponible con DRBD y marcapasos] [ suse-drbd-guide] guía hello contiene todos los tooset de la información necesaria de un servidor NFS de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cac26-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="cac26-138">Esta guía sirve como orientación.</span><span class="sxs-lookup"><span data-stu-id="cac26-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="cac26-139">Información general</span><span class="sxs-lookup"><span data-stu-id="cac26-139">Overview</span></span>

<span data-ttu-id="cac26-140">tooachieve la alta disponibilidad, SAP NetWeaver requiere un servidor NFS.</span><span class="sxs-lookup"><span data-stu-id="cac26-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="cac26-141">servidor NFS de Hello está configurado en un clúster diferente y puede usarse en varios sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="cac26-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Información general sobre la alta disponibilidad de SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="cac26-143">Hola servidor NFS, SAP NetWeaver ASCS, SCS de SAP NetWeaver, SAP NetWeaver ERS y base de datos de SAP HANA Hola usar nombre del host virtual y direcciones IP virtuales.</span><span class="sxs-lookup"><span data-stu-id="cac26-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="cac26-144">En Azure, un equilibrador de carga es toouse requiere una dirección IP virtual.</span><span class="sxs-lookup"><span data-stu-id="cac26-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="cac26-145">Hello lista siguiente muestra configuración Hola Hola de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="cac26-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="cac26-146">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="cac26-146">NFS Server</span></span>
* <span data-ttu-id="cac26-147">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="cac26-147">Frontend configuration</span></span>
  * <span data-ttu-id="cac26-148">Dirección IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="cac26-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="cac26-149">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="cac26-149">Backend configuration</span></span>
  * <span data-ttu-id="cac26-150">Conectado tooprimary interfaces de red de todas las máquinas virtuales que deben formar parte del clúster NFS de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="cac26-151">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="cac26-151">Probe Port</span></span>
  * <span data-ttu-id="cac26-152">Puerto 61000</span><span class="sxs-lookup"><span data-stu-id="cac26-152">Port 61000</span></span>
* <span data-ttu-id="cac26-153">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="cac26-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="cac26-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-154">2049 TCP</span></span> 
  * <span data-ttu-id="cac26-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="cac26-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="cac26-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="cac26-156">(A)SCS</span></span>
* <span data-ttu-id="cac26-157">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="cac26-157">Frontend configuration</span></span>
  * <span data-ttu-id="cac26-158">Dirección IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="cac26-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="cac26-159">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="cac26-159">Backend configuration</span></span>
  * <span data-ttu-id="cac26-160">Interfaces de red conectados tooprimary de todas las máquinas virtuales que deben formar parte del clúster de hello (A) SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="cac26-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="cac26-161">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="cac26-161">Probe Port</span></span>
  * <span data-ttu-id="cac26-162">Puerto 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="cac26-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="cac26-163">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="cac26-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="cac26-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cac26-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cac26-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cac26-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cac26-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="cac26-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="cac26-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="cac26-171">ERS</span><span class="sxs-lookup"><span data-stu-id="cac26-171">ERS</span></span>
* <span data-ttu-id="cac26-172">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="cac26-172">Frontend configuration</span></span>
  * <span data-ttu-id="cac26-173">Dirección IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="cac26-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="cac26-174">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="cac26-174">Backend configuration</span></span>
  * <span data-ttu-id="cac26-175">Interfaces de red conectados tooprimary de todas las máquinas virtuales que deben formar parte del clúster de hello (A) SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="cac26-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="cac26-176">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="cac26-176">Probe Port</span></span>
  * <span data-ttu-id="cac26-177">Puerto 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="cac26-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="cac26-178">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="cac26-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="cac26-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="cac26-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="cac26-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="cac26-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="cac26-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-183">SAP HANA</span></span>
* <span data-ttu-id="cac26-184">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="cac26-184">Frontend configuration</span></span>
  * <span data-ttu-id="cac26-185">Dirección IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="cac26-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="cac26-186">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="cac26-186">Backend configuration</span></span>
  * <span data-ttu-id="cac26-187">Conectado tooprimary interfaces de red de todas las máquinas virtuales que debe formar parte del clúster HANA Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="cac26-188">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="cac26-188">Probe Port</span></span>
  * <span data-ttu-id="cac26-189">Puerto 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="cac26-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="cac26-190">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="cac26-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="cac26-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="cac26-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="cac26-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="cac26-193">Configuración de un servidor NFS de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="cac26-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="cac26-194">Implementación de Linux</span><span class="sxs-lookup"><span data-stu-id="cac26-194">Deploying Linux</span></span>

<span data-ttu-id="cac26-195">Hello Azure Marketplace contiene una imagen para SUSE Linux Enterprise Server para el 12 de las aplicaciones de SAP que puede usar máquinas virtuales de la nueva toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cac26-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="cac26-196">Puede usar una de las plantillas de inicio rápido de hello en github toodeploy todos los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="cac26-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="cac26-197">plantilla de Hello implementa máquinas virtuales de hello, equilibrador de carga de hello, etcetera conjunto de disponibilidad. Siga estas plantillas de hello toodeploy de pasos:</span><span class="sxs-lookup"><span data-stu-id="cac26-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="cac26-198">Abra hello [plantilla de servidor de archivos SAP] [ template-file-server] Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cac26-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="cac26-199">Escriba Hola parámetros siguientes</span><span class="sxs-lookup"><span data-stu-id="cac26-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="cac26-200">Prefijo de recurso</span><span class="sxs-lookup"><span data-stu-id="cac26-200">Resource Prefix</span></span>  
      <span data-ttu-id="cac26-201">Escriba el prefijo Hola desea toouse.</span><span class="sxs-lookup"><span data-stu-id="cac26-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="cac26-202">valor de Hola se usa como prefijo para los recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="cac26-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="cac26-203">Tipo de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="cac26-203">Os Type</span></span>  
      <span data-ttu-id="cac26-204">Seleccione una de las distribuciones de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="cac26-205">En este ejemplo, seleccione SLES 12</span><span class="sxs-lookup"><span data-stu-id="cac26-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="cac26-206">Nombre de usuario y contraseña del administrador</span><span class="sxs-lookup"><span data-stu-id="cac26-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="cac26-207">Se crea un nuevo usuario que pueden ser toolog usado en la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="cac26-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="cac26-208">Identificador de subred</span><span class="sxs-lookup"><span data-stu-id="cac26-208">Subnet Id</span></span>  
      <span data-ttu-id="cac26-209">Id. de Hola de máquinas virtuales de hello subred toowhich Hola debe estar conectado a.</span><span class="sxs-lookup"><span data-stu-id="cac26-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="cac26-210">Deje en blanco si desea toocreate una nueva red virtual o seleccione subred hello de la VPN o Express Route red virtual tooconnect Hola máquina virtual tooyour en red local.</span><span class="sxs-lookup"><span data-stu-id="cac26-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="cac26-211">Id. de Hello suele ser algo parecido/subscriptions /**&lt;Id. de suscripción&gt;**/ResourceGroups /**&lt;nombre del grupo de recursos&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nombre de red virtual&gt;**/subnets/**&lt;nombre de subred&gt;**</span><span class="sxs-lookup"><span data-stu-id="cac26-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="cac26-212">Instalación</span><span class="sxs-lookup"><span data-stu-id="cac26-212">Installation</span></span>

<span data-ttu-id="cac26-213">Hello elementos siguientes tienen el prefijo cualquiera **[A]** -nodos tooall aplicables, **[1]** -solo es aplicable toonode 1 o **[2]** -solo es aplicable toonode 2.</span><span class="sxs-lookup"><span data-stu-id="cac26-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="cac26-214">**[A]** Actualice SLES</span><span class="sxs-lookup"><span data-stu-id="cac26-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="cac26-215">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="cac26-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="cac26-216">**[2]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="cac26-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="cac26-217">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="cac26-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="cac26-218">**[A]** Instale la extensión de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="cac26-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="cac26-219">**[A]** Configure la resolución nombres de host</span><span class="sxs-lookup"><span data-stu-id="cac26-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="cac26-220">Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="cac26-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cac26-221">Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cac26-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cac26-222">Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos</span><span class="sxs-lookup"><span data-stu-id="cac26-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="cac26-223">Insertar Hola después líneas demasiado/etcetera/hosts.</span><span class="sxs-lookup"><span data-stu-id="cac26-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cac26-224">Cambiar toomatch de dirección y el nombre de host IP hello en el entorno</span><span class="sxs-lookup"><span data-stu-id="cac26-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="cac26-225">**[1]** Instale el clúster</span><span class="sxs-lookup"><span data-stu-id="cac26-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="cac26-226">**[2]**  Agregar nodo toocluster</span><span class="sxs-lookup"><span data-stu-id="cac26-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="cac26-227">**[A]**  Cambio hacluster contraseña toohello misma contraseña</span><span class="sxs-lookup"><span data-stu-id="cac26-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="cac26-228">**[A]**  Configurar corosync toouse otros tipos de transporte y agregar la lista de nodos.</span><span class="sxs-lookup"><span data-stu-id="cac26-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="cac26-229">De lo contrario, el clúster no funcionará.</span><span class="sxs-lookup"><span data-stu-id="cac26-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="cac26-230">Agregar hello toohello contenido negrita el archivo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cac26-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="cac26-231">A continuación, reinicie el servicio de hello corosync</span><span class="sxs-lookup"><span data-stu-id="cac26-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="cac26-232">**[A]** Instale los componentes de drbd</span><span class="sxs-lookup"><span data-stu-id="cac26-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="cac26-233">**[A]**  Crear una partición para el dispositivo de hello drbd</span><span class="sxs-lookup"><span data-stu-id="cac26-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="cac26-234">**[A]** Cree configuraciones de LVM</span><span class="sxs-lookup"><span data-stu-id="cac26-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="cac26-235">**[A]**  Dispositivo drbd de crear Hola NFS</span><span class="sxs-lookup"><span data-stu-id="cac26-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="cac26-236">Insertar la configuración de hello para el nuevo dispositivo de drbd Hola y de salida</span><span class="sxs-lookup"><span data-stu-id="cac26-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="cac26-237">Crear un dispositivo de hello drbd e inícielo</span><span class="sxs-lookup"><span data-stu-id="cac26-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="cac26-238">**[1]** Omita la sincronización inicial</span><span class="sxs-lookup"><span data-stu-id="cac26-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="cac26-239">**[1]**  Conjunto Hola el nodo principal</span><span class="sxs-lookup"><span data-stu-id="cac26-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="cac26-240">**[1]**  Espere hasta que se sincronizan los nuevos dispositivos de drbd Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="cac26-241">**[1]**  Crear sistemas de archivos en hello drbd dispositivos</span><span class="sxs-lookup"><span data-stu-id="cac26-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="cac26-242">Configuración de la plataforma del clúster</span><span class="sxs-lookup"><span data-stu-id="cac26-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="cac26-243">**[1]**  Cambiar la configuración predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cac26-244">**[1]**  Configuración del clúster agregar Hola NFS drbd dispositivo toohello</span><span class="sxs-lookup"><span data-stu-id="cac26-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cac26-245">**[1]**  Servidor NFS que crear Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cac26-246">**[1]**  Crear recursos de sistema de archivos NFS Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cac26-247">**[1]**  Crear exportaciones NFS de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="cac26-248">**[1]**  Crear un recurso de IP virtual y un sondeo de estado de equilibrador de carga interno de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cac26-249">Creación de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-249">Create STONITH device</span></span>

<span data-ttu-id="cac26-250">dispositivo de Hello STONITH utiliza un tooauthorize de entidad de servicio en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cac26-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="cac26-251">Siga estos toocreate pasos una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="cac26-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="cac26-252">Vaya demasiado<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cac26-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="cac26-253">Hoja de Azure Active Directory Hola abierto</span><span class="sxs-lookup"><span data-stu-id="cac26-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="cac26-254">Vaya tooProperties y anote Hola Id. de directorio. Se trata de hello **Id. de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="cac26-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="cac26-255">Haga clic en Registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cac26-255">Click App registrations</span></span>
1. <span data-ttu-id="cac26-256">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="cac26-256">Click Add</span></span>
1. <span data-ttu-id="cac26-257">Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear</span><span class="sxs-lookup"><span data-stu-id="cac26-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cac26-258">dirección URL de inicio de sesión de Hello no se usa y puede ser cualquier dirección URL válida</span><span class="sxs-lookup"><span data-stu-id="cac26-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cac26-259">Seleccione Hola nueva aplicación y haga clic en las claves en la ficha de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="cac26-260">Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar</span><span class="sxs-lookup"><span data-stu-id="cac26-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cac26-261">Anote el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-261">Write down hello Value.</span></span> <span data-ttu-id="cac26-262">Se utiliza como hello **contraseña** para hello entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="cac26-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="cac26-263">Anote Hola identificador de aplicación. Se utiliza como nombre de usuario de Hola (**Id. de inicio de sesión** en estos pasos hello) de hello entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="cac26-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="cac26-264">Hola entidad de servicio no tiene permisos tooaccess los recursos de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cac26-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="cac26-265">Necesita toostart de permisos de entidad de servicio de toogive hello y detener (desasignar) todas las máquinas virtuales del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="cac26-266">Vaya toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cac26-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="cac26-267">Abrir Hola a todos los módulos de recursos</span><span class="sxs-lookup"><span data-stu-id="cac26-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="cac26-268">Seleccione la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="cac26-269">Haga clic en Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="cac26-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cac26-270">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="cac26-270">Click Add</span></span>
1. <span data-ttu-id="cac26-271">Seleccione el rol de hello propietario</span><span class="sxs-lookup"><span data-stu-id="cac26-271">Select hello role Owner</span></span>
1. <span data-ttu-id="cac26-272">Escriba Hola nombre de aplicación Hola que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="cac26-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="cac26-273">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="cac26-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="cac26-274">**[1]**  Crear dispositivos de hello STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="cac26-275">Después de editar permisos de Hola para las máquinas virtuales de hello, puede configurar dispositivos STONITH hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="cac26-276">**[1]**  Habilitar el uso de Hola de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="cac26-277">Configuración de (A)SCS</span><span class="sxs-lookup"><span data-stu-id="cac26-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="cac26-278">Implementación de Linux</span><span class="sxs-lookup"><span data-stu-id="cac26-278">Deploying Linux</span></span>

<span data-ttu-id="cac26-279">Hello Azure Marketplace contiene una imagen para SUSE Linux Enterprise Server para el 12 de las aplicaciones de SAP que puede usar máquinas virtuales de la nueva toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cac26-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="cac26-280">imagen de marketplace de Hello contiene a agente de recursos de Hola para SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="cac26-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="cac26-281">Puede usar una de las plantillas de inicio rápido de hello en github toodeploy todos los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="cac26-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="cac26-282">plantilla de Hello implementa máquinas virtuales de hello, equilibrador de carga de hello, etcetera conjunto de disponibilidad. Siga estas plantillas de hello toodeploy de pasos:</span><span class="sxs-lookup"><span data-stu-id="cac26-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="cac26-283">Abra hello [plantilla ASCS/SCS múltiples SID] [ template-multisid-xscs] o hello [convergente plantilla] [ template-converged] en plantilla solo de Hola Hola portal Azure ASCS/SCS crea reglas de equilibrio de carga de hello hello ASCS/SCS de SAP NetWeaver y instancias ERS (solamente para Linux), mientras que la plantilla convergente hello también crea reglas de equilibrio de carga de Hola para una base de datos (por ejemplo Microsoft SQL Server o SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="cac26-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="cac26-284">Si tiene pensado tooinstall un sistema basadas en SAP NetWeaver y también desea base de datos de tooinstall hello en Hola mismo máquinas, use hello [convergente plantilla][template-converged].</span><span class="sxs-lookup"><span data-stu-id="cac26-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="cac26-285">Escriba Hola parámetros siguientes</span><span class="sxs-lookup"><span data-stu-id="cac26-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="cac26-286">Prefijo de recurso (solo la plantilla de varios ASCS/SCS de varios SID)</span><span class="sxs-lookup"><span data-stu-id="cac26-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="cac26-287">Escriba el prefijo Hola desea toouse.</span><span class="sxs-lookup"><span data-stu-id="cac26-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="cac26-288">valor de Hola se usa como prefijo para los recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="cac26-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="cac26-289">Identificador del sistema SAP (solo la plantilla convergente)</span><span class="sxs-lookup"><span data-stu-id="cac26-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="cac26-290">Especifique el sistema SAP de hello Id. de hello sistema SAP que desee tooinstall.</span><span class="sxs-lookup"><span data-stu-id="cac26-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="cac26-291">Hola identificador se usa como prefijo para los recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="cac26-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="cac26-292">Tipo de pila</span><span class="sxs-lookup"><span data-stu-id="cac26-292">Stack Type</span></span>  
      <span data-ttu-id="cac26-293">Seleccione el tipo de pila de SAP NetWeaver Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="cac26-294">Tipo de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="cac26-294">Os Type</span></span>  
      <span data-ttu-id="cac26-295">Seleccione una de las distribuciones de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="cac26-296">En este ejemplo, seleccione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="cac26-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="cac26-297">Tipo de base de datos</span><span class="sxs-lookup"><span data-stu-id="cac26-297">Db Type</span></span>  
      <span data-ttu-id="cac26-298">Seleccione HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-298">Select HANA</span></span>
   7. <span data-ttu-id="cac26-299">Tamaño del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="cac26-299">Sap System Size</span></span>  
      <span data-ttu-id="cac26-300">proporciona la cantidad de Hola de nuevo sistema de SAPS Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="cac26-301">Si no estás seguro de cuántos SAPS Hola sistema requiere, póngase en contacto con su socio de tecnología de SAP o integrador de sistema</span><span class="sxs-lookup"><span data-stu-id="cac26-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="cac26-302">Disponibilidad del sistema</span><span class="sxs-lookup"><span data-stu-id="cac26-302">System Availability</span></span>  
      <span data-ttu-id="cac26-303">Seleccione alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="cac26-303">Select HA</span></span>
   9. <span data-ttu-id="cac26-304">Nombre de usuario y contraseña del administrador</span><span class="sxs-lookup"><span data-stu-id="cac26-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="cac26-305">Se crea un nuevo usuario que pueden ser toolog usado en la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="cac26-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="cac26-306">Identificador de subred</span><span class="sxs-lookup"><span data-stu-id="cac26-306">Subnet Id</span></span>  
   <span data-ttu-id="cac26-307">Id. de Hola de máquinas virtuales de hello subred toowhich Hola debe estar conectado a.</span><span class="sxs-lookup"><span data-stu-id="cac26-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="cac26-308">Deje en blanco si desea toocreate una nueva red virtual o seleccione Hola la misma subred que utilizan o se crea como parte de la implementación de servidor NFS de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="cac26-309">Id. de Hello suele ser algo parecido/subscriptions /**&lt;Id. de suscripción&gt;**/ResourceGroups /**&lt;nombre del grupo de recursos&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nombre de red virtual&gt;**/subnets/**&lt;nombre de subred&gt;**</span><span class="sxs-lookup"><span data-stu-id="cac26-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="cac26-310">Instalación</span><span class="sxs-lookup"><span data-stu-id="cac26-310">Installation</span></span>

<span data-ttu-id="cac26-311">Hello elementos siguientes tienen el prefijo cualquiera **[A]** -nodos tooall aplicables, **[1]** -solo es aplicable toonode 1 o **[2]** -solo es aplicable toonode 2.</span><span class="sxs-lookup"><span data-stu-id="cac26-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="cac26-312">**[A]** Actualice SLES</span><span class="sxs-lookup"><span data-stu-id="cac26-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="cac26-313">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="cac26-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="cac26-314">**[2]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="cac26-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="cac26-315">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="cac26-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="cac26-316">**[A]** Instale la extensión de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="cac26-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="cac26-317">**[A]** Actualice los agentes de recursos de SAP</span><span class="sxs-lookup"><span data-stu-id="cac26-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="cac26-318">Una revisión para el paquete de agentes de recursos de hello es nueva configuración de Hola de toouse necesarios, que se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cac26-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="cac26-319">Puede comprobar, si ya está instalada la revisión Hola con hello siguiente comando</span><span class="sxs-lookup"><span data-stu-id="cac26-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="cac26-320">salida de Hello debe ser similar a</span><span class="sxs-lookup"><span data-stu-id="cac26-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="cac26-321">Si el comando grep de hello no encuentra el parámetro IS_ERS hello, necesita revisión de hello tooinstall aparece en [página de descarga de hello SUSE](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="cac26-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="cac26-322">**[A]** Configure la resolución nombres de host</span><span class="sxs-lookup"><span data-stu-id="cac26-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="cac26-323">Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="cac26-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cac26-324">Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cac26-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cac26-325">Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos</span><span class="sxs-lookup"><span data-stu-id="cac26-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="cac26-326">Insertar Hola después líneas demasiado/etcetera/hosts.</span><span class="sxs-lookup"><span data-stu-id="cac26-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cac26-327">Cambiar toomatch de dirección y el nombre de host IP hello en el entorno</span><span class="sxs-lookup"><span data-stu-id="cac26-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="cac26-328">**[1]** Instale el clúster</span><span class="sxs-lookup"><span data-stu-id="cac26-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="cac26-329">**[2]**  Agregar nodo toocluster</span><span class="sxs-lookup"><span data-stu-id="cac26-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="cac26-330">**[A]**  Cambio hacluster contraseña toohello misma contraseña</span><span class="sxs-lookup"><span data-stu-id="cac26-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="cac26-331">**[A]**  Configurar corosync toouse otros tipos de transporte y agregar la lista de nodos.</span><span class="sxs-lookup"><span data-stu-id="cac26-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="cac26-332">De lo contrario, el clúster no funcionará.</span><span class="sxs-lookup"><span data-stu-id="cac26-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="cac26-333">Agregar hello toohello contenido negrita el archivo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cac26-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="cac26-334">A continuación, reinicie el servicio de hello corosync</span><span class="sxs-lookup"><span data-stu-id="cac26-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="cac26-335">**[A]** Instale los componentes de drbd</span><span class="sxs-lookup"><span data-stu-id="cac26-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="cac26-336">**[A]**  Crear una partición para el dispositivo de hello drbd</span><span class="sxs-lookup"><span data-stu-id="cac26-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="cac26-337">**[A]** Cree configuraciones de LVM</span><span class="sxs-lookup"><span data-stu-id="cac26-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="cac26-338">**[A]**  Dispositivo drbd de crear Hola SCS</span><span class="sxs-lookup"><span data-stu-id="cac26-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="cac26-339">Insertar la configuración de hello para el nuevo dispositivo de drbd Hola y de salida</span><span class="sxs-lookup"><span data-stu-id="cac26-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="cac26-340">Crear un dispositivo de hello drbd e inícielo</span><span class="sxs-lookup"><span data-stu-id="cac26-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="cac26-341">**[A]**  Dispositivo de crear Hola ERS drbd</span><span class="sxs-lookup"><span data-stu-id="cac26-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="cac26-342">Insertar la configuración de hello para el nuevo dispositivo de drbd Hola y de salida</span><span class="sxs-lookup"><span data-stu-id="cac26-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="cac26-343">Crear un dispositivo de hello drbd e inícielo</span><span class="sxs-lookup"><span data-stu-id="cac26-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="cac26-344">**[1]** Omita la sincronización inicial</span><span class="sxs-lookup"><span data-stu-id="cac26-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="cac26-345">**[1]**  Conjunto Hola el nodo principal</span><span class="sxs-lookup"><span data-stu-id="cac26-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="cac26-346">**[1]**  Espere hasta que se sincronizan los nuevos dispositivos de drbd Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="cac26-347">**[1]**  Crear sistemas de archivos en hello drbd dispositivos</span><span class="sxs-lookup"><span data-stu-id="cac26-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="cac26-348">Configuración de la plataforma del clúster</span><span class="sxs-lookup"><span data-stu-id="cac26-348">Configure Cluster Framework</span></span>

<span data-ttu-id="cac26-349">**[1]**  Cambiar la configuración predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="cac26-350">Preparación de la instalación de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cac26-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="cac26-351">**[A]**  Hola de crear los directorios compartidos</span><span class="sxs-lookup"><span data-stu-id="cac26-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="cac26-352">**[A]** Configure autofs</span><span class="sxs-lookup"><span data-stu-id="cac26-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="cac26-353">Cree un archivo con</span><span class="sxs-lookup"><span data-stu-id="cac26-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="cac26-354">Reinicie nuevos recursos compartidos autofs toomount Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="cac26-355">**[A]** Configure el archivo de intercambio</span><span class="sxs-lookup"><span data-stu-id="cac26-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="cac26-356">Reiniciar Hola agente tooactivate Hola cambios</span><span class="sxs-lookup"><span data-stu-id="cac26-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="cac26-357">Instalación de SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="cac26-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="cac26-358">**[1]**  Crear un recurso de IP virtual y un sondeo de estado de equilibrador de carga interno de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="cac26-359">Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="cac26-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cac26-360">No es importante en qué recursos de Hola de nodo se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="cac26-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="cac26-361">**[1]** Instale SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="cac26-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="cac26-362">Instalar ASCS de SAP NetWeaver como raíz en el primer nodo de hello mediante un nombre de host virtual que se asigna la dirección IP de toohello de configuración de front-end de equilibrador de carga de Hola para hello ASCS por ejemplo <b>nws ascs</b>, <b>10.0.0.10</b>y número de instancia de Hola que usó para la sonda de Hola Hola de equilibrador de carga por ejemplo <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="cac26-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="cac26-363">Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.</span><span class="sxs-lookup"><span data-stu-id="cac26-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="cac26-364">**[1]**  Crear un recurso de IP virtual y un sondeo de estado de equilibrador de carga interno de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="cac26-365">Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="cac26-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cac26-366">No es importante en qué recursos de Hola de nodo se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="cac26-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="cac26-367">**[2]** Instale SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="cac26-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="cac26-368">Instalar ERS de SAP NetWeaver como raíz en el segundo nodo de hello mediante un nombre de host virtual que se asigna la dirección IP de toohello de configuración de front-end de equilibrador de carga de Hola para hello ERS por ejemplo <b>nws ers</b>, <b>10.0.0.11</b> y el número de instancia de Hola que usó para la sonda de Hola Hola de equilibrador de carga por ejemplo <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="cac26-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="cac26-369">Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.</span><span class="sxs-lookup"><span data-stu-id="cac26-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="cac26-370">Use SWPM SP 20 PL 05 o superior.</span><span class="sxs-lookup"><span data-stu-id="cac26-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="cac26-371">Las versiones inferiores no establece permisos de hello correctamente y se producirá un error en la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="cac26-372">**[1]**  Adaptar Hola ASCS/SCS y ERS instancia perfiles</span><span class="sxs-lookup"><span data-stu-id="cac26-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="cac26-373">Perfil ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="cac26-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="cac26-374">Perfil ERS</span><span class="sxs-lookup"><span data-stu-id="cac26-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="cac26-375">**[A]** Configure la conexión persistente</span><span class="sxs-lookup"><span data-stu-id="cac26-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="cac26-376">la comunicación entre el servidor de aplicaciones de SAP NetWeaver de Hola y Hola ASCS/SCS Hola se enruta a través de un equilibrador de carga de software.</span><span class="sxs-lookup"><span data-stu-id="cac26-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="cac26-377">equilibrador de carga de Hello desconecta las conexiones inactivas tras un tiempo de espera configurable.</span><span class="sxs-lookup"><span data-stu-id="cac26-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="cac26-378">tooprevent esto necesita tooset un parámetro en el perfil de SAP NetWeaver ASCS/SCS de Hola y cambiar la configuración de sistema de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="cac26-379">Consulte la [nota de SAP 1410736][1410736] para más información.</span><span class="sxs-lookup"><span data-stu-id="cac26-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="cac26-380">Hola ASCS/SCS perfil parámetro enque/encni/set_so_keepalive ya se agregó en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="cac26-381">**[A]**  Configurar usuarios SAP de hello después de la instalación de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="cac26-382">**[1]**  Agregar ASCS y SAP ERS servicios toohello sapservice archivo hello</span><span class="sxs-lookup"><span data-stu-id="cac26-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="cac26-383">Agregar nodo de segundo de hello ASCS servicio entry toohello y copia Hola ERS servicio entrada toohello primer nodo.</span><span class="sxs-lookup"><span data-stu-id="cac26-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="cac26-384">**[1]**  Crear recursos de clúster de hello SAP</span><span class="sxs-lookup"><span data-stu-id="cac26-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="cac26-385">Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="cac26-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cac26-386">No es importante en qué recursos de Hola de nodo se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="cac26-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="cac26-387">Creación de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-387">Create STONITH device</span></span>

<span data-ttu-id="cac26-388">dispositivo de Hello STONITH utiliza un tooauthorize de entidad de servicio en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cac26-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="cac26-389">Siga estos toocreate pasos una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="cac26-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="cac26-390">Vaya demasiado<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="cac26-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="cac26-391">Hoja de Azure Active Directory Hola abierto</span><span class="sxs-lookup"><span data-stu-id="cac26-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="cac26-392">Vaya tooProperties y anote Hola Id. de directorio. Se trata de hello **Id. de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="cac26-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="cac26-393">Haga clic en Registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cac26-393">Click App registrations</span></span>
1. <span data-ttu-id="cac26-394">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="cac26-394">Click Add</span></span>
1. <span data-ttu-id="cac26-395">Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear</span><span class="sxs-lookup"><span data-stu-id="cac26-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="cac26-396">dirección URL de inicio de sesión de Hello no se usa y puede ser cualquier dirección URL válida</span><span class="sxs-lookup"><span data-stu-id="cac26-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="cac26-397">Seleccione Hola nueva aplicación y haga clic en las claves en la ficha de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="cac26-398">Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar</span><span class="sxs-lookup"><span data-stu-id="cac26-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="cac26-399">Anote el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-399">Write down hello Value.</span></span> <span data-ttu-id="cac26-400">Se utiliza como hello **contraseña** para hello entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="cac26-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="cac26-401">Anote Hola identificador de aplicación. Se utiliza como nombre de usuario de Hola (**Id. de inicio de sesión** en estos pasos hello) de hello entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="cac26-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="cac26-402">Hola entidad de servicio no tiene permisos tooaccess los recursos de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cac26-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="cac26-403">Necesita toostart de permisos de entidad de servicio de toogive hello y detener (desasignar) todas las máquinas virtuales del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="cac26-404">Vaya toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cac26-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="cac26-405">Abrir Hola a todos los módulos de recursos</span><span class="sxs-lookup"><span data-stu-id="cac26-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="cac26-406">Seleccione la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="cac26-407">Haga clic en Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="cac26-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="cac26-408">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="cac26-408">Click Add</span></span>
1. <span data-ttu-id="cac26-409">Seleccione el rol de hello propietario</span><span class="sxs-lookup"><span data-stu-id="cac26-409">Select hello role Owner</span></span>
1. <span data-ttu-id="cac26-410">Escriba Hola nombre de aplicación Hola que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="cac26-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="cac26-411">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="cac26-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="cac26-412">**[1]**  Crear dispositivos de hello STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="cac26-413">Después de editar permisos de Hola para las máquinas virtuales de hello, puede configurar dispositivos STONITH hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="cac26-414">**[1]**  Habilitar el uso de Hola de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="cac26-415">Habilitar el uso de Hola de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="cac26-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="cac26-416">Instalar la base de datos</span><span class="sxs-lookup"><span data-stu-id="cac26-416">Install database</span></span>

<span data-ttu-id="cac26-417">En este ejemplo, hay una replicación del sistema SAP HANA instalada y configurada.</span><span class="sxs-lookup"><span data-stu-id="cac26-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="cac26-418">SAP HANA se ejecutará en el mismo clúster según hello ASCS/SCS de SAP NetWeaver y ERS de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="cac26-419">También puede instalar SAP HANA en un clúster dedicado.</span><span class="sxs-lookup"><span data-stu-id="cac26-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="cac26-420">Consulte [Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure][sap-hana-ha] para más información.</span><span class="sxs-lookup"><span data-stu-id="cac26-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="cac26-421">Preparación de la instalación de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="cac26-422">Por lo general, se recomienda usar LVM para volúmenes de almacén de datos y archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="cac26-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="cac26-423">Para realizar pruebas, también puede elegir los archivos de registro y datos de hello toostore directamente en un disco sin formato.</span><span class="sxs-lookup"><span data-stu-id="cac26-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="cac26-424">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="cac26-424">**[A]** LVM</span></span>  
   <span data-ttu-id="cac26-425">ejemplo de Hola siguiente supone que máquinas virtuales de hello tiene cuatro discos de datos conectados que se deben toocreate usa dos volúmenes.</span><span class="sxs-lookup"><span data-stu-id="cac26-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="cac26-426">Crear volúmenes físicos de todos los discos que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="cac26-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="cac26-427">Crear un grupo de volúmenes para los archivos de datos de hello, un grupo de volúmenes para los archivos de registro de hello y otro para el directorio compartido de Hola de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="cac26-428">Crear volúmenes lógicos de Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="cac26-429">Crear los directorios de montaje de Hola y copiar Hola UUID de todos los volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="cac26-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="cac26-430">Crear las entradas de autofs de hello tres volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="cac26-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="cac26-431">Inserte esta línea toosudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="cac26-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="cac26-432">Montar volúmenes nuevos Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="cac26-433">**[A]** Discos sin formatos</span><span class="sxs-lookup"><span data-stu-id="cac26-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="cac26-434">Para sistemas pequeños o de demostración, puede colocar los archivos de datos y de registro HANA en un disco.</span><span class="sxs-lookup"><span data-stu-id="cac26-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="cac26-435">Hello siguientes comandos crean una partición en /dev/sdc y dele formato con xfs.</span><span class="sxs-lookup"><span data-stu-id="cac26-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="cac26-436">Insertar este too/etc/auto.direct línea</span><span class="sxs-lookup"><span data-stu-id="cac26-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="cac26-437">Crear el directorio de destino de Hola y montar el disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="cac26-438">Instalación de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-438">Installing SAP HANA</span></span>

<span data-ttu-id="cac26-439">Hello pasos siguientes se basan capítulo 4 de hello [Guía de SAP HANA SR rendimiento optimizado escenario] [ suse-hana-ha-guide] tooinstall replicación del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cac26-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="cac26-440">Por favor, lea antes de continuar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="cac26-441">**[A]**  Ejecutar hdblcm desde Hola HANA DVD</span><span class="sxs-lookup"><span data-stu-id="cac26-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="cac26-442">**[A]** Actualice el agente de host de SAP</span><span class="sxs-lookup"><span data-stu-id="cac26-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="cac26-443">Descargue el archivo de agente de Host de SAP más reciente de Hola de hello [SAP Softwarecenter] [ sap-swcenter] y ejecución hello siguientes comando tooupgrade Hola agente.</span><span class="sxs-lookup"><span data-stu-id="cac26-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="cac26-444">Reemplace Hola ruta de acceso toohello toopoint toohello archivo que descargó.</span><span class="sxs-lookup"><span data-stu-id="cac26-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="cac26-445">**[1]** Cree la replicación de HANA (como raíz)</span><span class="sxs-lookup"><span data-stu-id="cac26-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="cac26-446">Ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-446">Run hello following command.</span></span> <span data-ttu-id="cac26-447">Asegúrese de que tooreplace negrita cadenas (HDB de Id. de sistema de archivos de HANA y número de instancia 03) con valores de hello de la instalación de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="cac26-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="cac26-448">**[A]** Cree la entrada de almacén de claves (como raíz)</span><span class="sxs-lookup"><span data-stu-id="cac26-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="cac26-449">**[1]** Realice la copia de seguridad de la base de datos (como raíz)</span><span class="sxs-lookup"><span data-stu-id="cac26-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="cac26-450">**[1]**  Cambiar de usuario de toohello HANA sapsid y crear el sitio primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="cac26-451">**[2]**  Cambiar de usuario de toohello HANA sapsid y crear sitio secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="cac26-452">**[1]** Creación de recursos de clúster de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="cac26-453">En primer lugar, cree la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="cac26-454">A continuación, cree Hola recursos HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="cac26-455">Asegúrese de que el estado del clúster hello es correcto y que se hayan iniciado todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="cac26-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="cac26-456">No es importante en qué recursos de Hola de nodo se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="cac26-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="cac26-457">**[1]**  Instancia de base de datos de SAP NetWeaver de Hola de instalación</span><span class="sxs-lookup"><span data-stu-id="cac26-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="cac26-458">Instancia de base de datos de SAP NetWeaver instalación hello como raíz con un nombre de host virtual que se asigna como dirección IP de toohello de configuración de front-end de equilibrador de carga de Hola para base de datos de hello <b>nws db</b> y <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="cac26-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="cac26-459">Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.</span><span class="sxs-lookup"><span data-stu-id="cac26-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="cac26-460">Instalación del servidor de aplicaciones de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cac26-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="cac26-461">Siga estos tooinstall pasos un servidor de aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="cac26-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="cac26-462">Hola pasos siguientes se supone que instalar servidores HANA y servidor de aplicaciones de hello en un servidor distinto de hello ASCS/SCS.</span><span class="sxs-lookup"><span data-stu-id="cac26-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="cac26-463">En caso contrario, no son necesarios algunos pasos de hello debajo (por ejemplo, configurar la resolución de nombres de host).</span><span class="sxs-lookup"><span data-stu-id="cac26-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="cac26-464">Configure la resolución de nombres de host</span><span class="sxs-lookup"><span data-stu-id="cac26-464">Setup host name resolution</span></span>    
   <span data-ttu-id="cac26-465">Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="cac26-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="cac26-466">Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="cac26-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="cac26-467">Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos</span><span class="sxs-lookup"><span data-stu-id="cac26-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="cac26-468">Insertar Hola después líneas demasiado/etcetera/hosts.</span><span class="sxs-lookup"><span data-stu-id="cac26-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="cac26-469">Cambiar toomatch de dirección y el nombre de host IP hello en el entorno</span><span class="sxs-lookup"><span data-stu-id="cac26-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="cac26-470">Crear el directorio de hello sapmnt</span><span class="sxs-lookup"><span data-stu-id="cac26-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="cac26-471">Configure autofs</span><span class="sxs-lookup"><span data-stu-id="cac26-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="cac26-472">Cree un nuevo archivo con</span><span class="sxs-lookup"><span data-stu-id="cac26-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="cac26-473">Reinicie nuevos recursos compartidos autofs toomount Hola</span><span class="sxs-lookup"><span data-stu-id="cac26-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="cac26-474">Configure el archivo de intercambio</span><span class="sxs-lookup"><span data-stu-id="cac26-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="cac26-475">Reiniciar Hola agente tooactivate Hola cambios</span><span class="sxs-lookup"><span data-stu-id="cac26-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="cac26-476">Instale el servidor de aplicaciones de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="cac26-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="cac26-477">Instale un servidor de aplicaciones de SAP NetWeaver principal o adicional.</span><span class="sxs-lookup"><span data-stu-id="cac26-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="cac26-478">Puede usar hello sapinst parámetro SAPINST_REMOTE_ACCESS_USER tooallow una toosapinst tooconnect de usuario no es de raíz.</span><span class="sxs-lookup"><span data-stu-id="cac26-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="cac26-479">Actualice el almacenamiento seguro de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="cac26-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="cac26-480">Hola de actualización segura de SAP HANA almacenar toopoint toohello nombre virtual del programa de instalación de replicación del sistema de SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="cac26-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="cac26-481">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cac26-481">Next steps</span></span>
* <span data-ttu-id="cac26-482">[Planeación e implementación de Azure Virtual Machines para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="cac26-483">[Implementación de Azure Virtual Machines para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="cac26-484">[Implementación de DBMS de Azure Virtual Machines para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="cac26-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="cac26-485">toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cac26-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="cac26-486">toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en máquinas virtuales de Azure, vea [disponibilidad alta de SAP HANA en máquinas virtuales de Azure (VM)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="cac26-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
