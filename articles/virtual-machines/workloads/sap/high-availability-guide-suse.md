---
title: Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver en SUSE Linux Enterprise Server para SAP Applications | Microsoft Docs
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
ms.openlocfilehash: 16e09797926f29bc18cb05671c986c74f9c2d4f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="55b5c-103">Alta disponibilidad para SAP NetWeaver en máquinas virtuales de Azure en SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="55b5c-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="55b5c-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="55b5c-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="55b5c-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="55b5c-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="55b5c-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="55b5c-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="55b5c-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="55b5c-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="55b5c-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="55b5c-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="55b5c-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="55b5c-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="55b5c-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="55b5c-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="55b5c-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="55b5c-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="55b5c-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="55b5c-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="55b5c-113">En este artículo se describe cómo implementar y configurar las máquinas virtuales, instalar la plataforma del clúster e instalar un sistema SAP NetWeaver 7.50 de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="55b5c-113">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="55b5c-114">En las configuraciones, comandos de instalación, etc. de ejemplo, se usa el número de instancia 00 de ASCS, el número de instancia 02 de ERS y NWS del identificador de sistema de SAP.</span><span class="sxs-lookup"><span data-stu-id="55b5c-114">In the example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="55b5c-115">Los nombres de los recursos (por ejemplo, máquinas virtuales, redes virtuales) en el ejemplo se da por sentado que usó la [plantilla convergente][template-converged] con NWS del identificador de sistema de SAP para crear los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-115">The names of the resources (for example virtual machines, virtual networks) in the example assume that you have used the [converged template][template-converged] with SAP system ID NWS to create the resources.</span></span>

<span data-ttu-id="55b5c-116">Lea primero las notas y los documentos de SAP siguientes:</span><span class="sxs-lookup"><span data-stu-id="55b5c-116">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="55b5c-117">Nota de SAP [1928533], que incluye:</span><span class="sxs-lookup"><span data-stu-id="55b5c-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="55b5c-118">La lista de tamaños de máquina virtual de Azure que se admiten para la implementación del software de SAP</span><span class="sxs-lookup"><span data-stu-id="55b5c-118">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="55b5c-119">Información importante sobre la capacidad para los tamaños de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="55b5c-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="55b5c-120">Software de SAP admitido y combinaciones de sistema operativo y base de datos</span><span class="sxs-lookup"><span data-stu-id="55b5c-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="55b5c-121">Versión del kernel de SAP requerida para Windows y Linux en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="55b5c-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="55b5c-122">La nota de SAP [2015553] enumera los requisitos previos para las implementaciones de software de SAP admitidas por SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b5c-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="55b5c-123">La nota de SAP [2205917] contiene configuraciones recomendadas del sistema operativo para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="55b5c-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="55b5c-124">La nota de SAP [1944799] contiene guías de SAP HANA para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="55b5c-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="55b5c-125">La nota de SAP [2178632] contiene información detallada sobre todas las métricas de supervisión notificadas para SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b5c-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="55b5c-126">La nota de SAP [2191498] incluye la versión de SAP Host Agent necesaria para Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b5c-126">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="55b5c-127">La nota de SAP [2243692] incluye información acerca de las licencias de SAP en Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="55b5c-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="55b5c-128">La nota de SAP [1984787] incluye información general sobre SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="55b5c-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="55b5c-129">La nota de SAP [1999351] contiene más soluciones de problemas de la extensión de supervisión mejorada de Azure para SAP.</span><span class="sxs-lookup"><span data-stu-id="55b5c-129">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="55b5c-130">La [WIKI de la comunidad SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene todas las notas de SAP que se necesitan para Linux.</span><span class="sxs-lookup"><span data-stu-id="55b5c-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="55b5c-131">[Planeación e implementación de Azure Virtual Machines para SAP en Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="55b5c-132">[Implementación de Azure Virtual Machines para SAP en Linux (este artículo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="55b5c-133">[Implementación de DBMS de Azure Virtual Machines para SAP en Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="55b5c-134">[Escenario de rendimiento optimizado para la replicación del sistema de SAP HANA][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="55b5c-135">La guía contiene toda la información necesaria para configurar la replicación local del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="55b5c-135">The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="55b5c-136">Esta guía sirve como orientación.</span><span class="sxs-lookup"><span data-stu-id="55b5c-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="55b5c-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] (Almacenamiento NFS de alta disponibilidad con DRBD y Pacemaker) La guía contiene toda la información necesaria para configurar un servidor NFS de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="55b5c-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] The guide contains all required information to set up a highly available NFS server.</span></span> <span data-ttu-id="55b5c-138">Esta guía sirve como orientación.</span><span class="sxs-lookup"><span data-stu-id="55b5c-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="55b5c-139">Información general</span><span class="sxs-lookup"><span data-stu-id="55b5c-139">Overview</span></span>

<span data-ttu-id="55b5c-140">Para lograr alta disponibilidad, SAP NetWeaver requiere un servidor NFS.</span><span class="sxs-lookup"><span data-stu-id="55b5c-140">To achieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="55b5c-141">El servidor NFS está configurado en un clúster distinto y lo pueden usar varios sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="55b5c-141">The NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Información general sobre la alta disponibilidad de SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="55b5c-143">El servidor NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS y la base de datos SAP HANA usan direcciones IP virtuales y nombre de host virtual.</span><span class="sxs-lookup"><span data-stu-id="55b5c-143">The NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and the SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="55b5c-144">En Azure, se requiere un equilibrador de carga para usar una dirección IP virtual.</span><span class="sxs-lookup"><span data-stu-id="55b5c-144">On Azure, a load balancer is required to use a virtual IP address.</span></span> <span data-ttu-id="55b5c-145">En la lista siguiente se muestra la configuración del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="55b5c-145">The following list shows the configuration of the load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="55b5c-146">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="55b5c-146">NFS Server</span></span>
* <span data-ttu-id="55b5c-147">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-147">Frontend configuration</span></span>
  * <span data-ttu-id="55b5c-148">Dirección IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="55b5c-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="55b5c-149">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-149">Backend configuration</span></span>
  * <span data-ttu-id="55b5c-150">Se conecta a interfaces de red principales de todas las máquinas que deben ser parte del clúster NFS</span><span class="sxs-lookup"><span data-stu-id="55b5c-150">Connected to primary network interfaces of all virtual machines that should be part of the NFS cluster</span></span>
* <span data-ttu-id="55b5c-151">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="55b5c-151">Probe Port</span></span>
  * <span data-ttu-id="55b5c-152">Puerto 61000</span><span class="sxs-lookup"><span data-stu-id="55b5c-152">Port 61000</span></span>
* <span data-ttu-id="55b5c-153">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="55b5c-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="55b5c-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-154">2049 TCP</span></span> 
  * <span data-ttu-id="55b5c-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="55b5c-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="55b5c-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="55b5c-156">(A)SCS</span></span>
* <span data-ttu-id="55b5c-157">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-157">Frontend configuration</span></span>
  * <span data-ttu-id="55b5c-158">Dirección IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="55b5c-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="55b5c-159">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-159">Backend configuration</span></span>
  * <span data-ttu-id="55b5c-160">Se conecta a interfaces de red principales de todas las máquinas que deben ser parte del clúster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-160">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="55b5c-161">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="55b5c-161">Probe Port</span></span>
  * <span data-ttu-id="55b5c-162">Puerto 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="55b5c-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="55b5c-163">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="55b5c-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="55b5c-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="55b5c-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="55b5c-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="55b5c-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="55b5c-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="55b5c-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="55b5c-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="55b5c-171">ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-171">ERS</span></span>
* <span data-ttu-id="55b5c-172">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-172">Frontend configuration</span></span>
  * <span data-ttu-id="55b5c-173">Dirección IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="55b5c-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="55b5c-174">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-174">Backend configuration</span></span>
  * <span data-ttu-id="55b5c-175">Se conecta a interfaces de red principales de todas las máquinas que deben ser parte del clúster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-175">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="55b5c-176">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="55b5c-176">Probe Port</span></span>
  * <span data-ttu-id="55b5c-177">Puerto 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="55b5c-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="55b5c-178">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="55b5c-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="55b5c-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="55b5c-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="55b5c-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="55b5c-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="55b5c-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-183">SAP HANA</span></span>
* <span data-ttu-id="55b5c-184">Configuración de front-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-184">Frontend configuration</span></span>
  * <span data-ttu-id="55b5c-185">Dirección IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="55b5c-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="55b5c-186">Configuración de back-end</span><span class="sxs-lookup"><span data-stu-id="55b5c-186">Backend configuration</span></span>
  * <span data-ttu-id="55b5c-187">Se conecta a interfaces de red principales de todas las máquinas que deben ser parte del clúster HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-187">Connected to primary network interfaces of all virtual machines that should be part of the HANA cluster</span></span>
* <span data-ttu-id="55b5c-188">Puerto de sondeo</span><span class="sxs-lookup"><span data-stu-id="55b5c-188">Probe Port</span></span>
  * <span data-ttu-id="55b5c-189">Puerto 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="55b5c-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="55b5c-190">Reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="55b5c-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="55b5c-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="55b5c-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="55b5c-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="55b5c-193">Configuración de un servidor NFS de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="55b5c-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="55b5c-194">Implementación de Linux</span><span class="sxs-lookup"><span data-stu-id="55b5c-194">Deploying Linux</span></span>

<span data-ttu-id="55b5c-195">Azure Marketplace contiene una imagen de SUSE Linux Enterprise Server para SAP Applications 12 que puede usar para implementar nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="55b5c-195">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span>
<span data-ttu-id="55b5c-196">Para implementar todos los recursos necesarios, puede usar una de las plantillas de inicio rápido de github.</span><span class="sxs-lookup"><span data-stu-id="55b5c-196">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="55b5c-197">La plantilla implementa las máquinas virtuales, el equilibrador de carga, el conjunto de disponibilidad, etc. Siga estos pasos para implementar la plantilla:</span><span class="sxs-lookup"><span data-stu-id="55b5c-197">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="55b5c-198">Abra la [plantilla del servidor de archivos SAP][template-file-server] en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="55b5c-198">Open the [SAP file server template][template-file-server] in the Azure portal</span></span>   
1. <span data-ttu-id="55b5c-199">Escriba los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="55b5c-199">Enter the following parameters</span></span>
   1. <span data-ttu-id="55b5c-200">Prefijo de recurso</span><span class="sxs-lookup"><span data-stu-id="55b5c-200">Resource Prefix</span></span>  
      <span data-ttu-id="55b5c-201">Escriba el prefijo que desea usar.</span><span class="sxs-lookup"><span data-stu-id="55b5c-201">Enter the prefix you want to use.</span></span> <span data-ttu-id="55b5c-202">El valor se usa como prefijo de los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="55b5c-202">The value is used as a prefix for the resources that are deployed.</span></span>
   2. <span data-ttu-id="55b5c-203">Tipo de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="55b5c-203">Os Type</span></span>  
      <span data-ttu-id="55b5c-204">Seleccione una de las distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="55b5c-204">Select one of the Linux distributions.</span></span> <span data-ttu-id="55b5c-205">En este ejemplo, seleccione SLES 12</span><span class="sxs-lookup"><span data-stu-id="55b5c-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="55b5c-206">Nombre de usuario y contraseña del administrador</span><span class="sxs-lookup"><span data-stu-id="55b5c-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="55b5c-207">Se crea un usuario nuevo que se puede usar para iniciar sesión en la máquina.</span><span class="sxs-lookup"><span data-stu-id="55b5c-207">A new user is created that can be used to log on to the machine.</span></span>
   4. <span data-ttu-id="55b5c-208">Identificador de subred</span><span class="sxs-lookup"><span data-stu-id="55b5c-208">Subnet Id</span></span>  
      <span data-ttu-id="55b5c-209">El identificador de la subred a la que deben conectarse las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="55b5c-209">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="55b5c-210">Deje el valor en blanco si quiere crear una nueva red virtual o seleccione la subred de la VPN o la red virtual de Express Route para conectar la máquina virtual a la red local.</span><span class="sxs-lookup"><span data-stu-id="55b5c-210">Leave empty if you want to create a new virtual network or select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="55b5c-211">El identificador suele tener este aspecto /subscriptions/**&lt;id. de suscripción&gt;**/resourceGroups/**&lt;nombre del grupo de recursos&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nombre de red virtual&gt;**/subnets/**&lt;nombre de subred&gt;**</span><span class="sxs-lookup"><span data-stu-id="55b5c-211">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="55b5c-212">Instalación</span><span class="sxs-lookup"><span data-stu-id="55b5c-212">Installation</span></span>

<span data-ttu-id="55b5c-213">Los elementos siguientes tienen el prefijo **[A]**: aplicable a todos los nodos, **[1]**: aplicable solo al nodo 1 o **[2]**: aplicable solo al nodo 2.</span><span class="sxs-lookup"><span data-stu-id="55b5c-213">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="55b5c-214">**[A]** Actualice SLES</span><span class="sxs-lookup"><span data-stu-id="55b5c-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="55b5c-215">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="55b5c-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="55b5c-216">**[2]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="55b5c-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="55b5c-217">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="55b5c-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="55b5c-218">**[A]** Instale la extensión de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="55b5c-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="55b5c-219">**[A]** Configure la resolución nombres de host</span><span class="sxs-lookup"><span data-stu-id="55b5c-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="55b5c-220">Puede usar un servidor DNS o modificar /etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-220">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="55b5c-221">En este ejemplo se muestra cómo utilizar el archivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="55b5c-221">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="55b5c-222">Reemplace la dirección IP y el nombre de host en los siguientes comandos</span><span class="sxs-lookup"><span data-stu-id="55b5c-222">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="55b5c-223">Inserte las siguientes líneas en /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="55b5c-223">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="55b5c-224">Cambie la dirección IP y el nombre de host para que coincida con su entorno</span><span class="sxs-lookup"><span data-stu-id="55b5c-224">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="55b5c-225">**[1]** Instale el clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="55b5c-226">**[2]** Agregue un nodo al clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-226">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="55b5c-227">**[A]** Haga que la contraseña de hacluster coincida</span><span class="sxs-lookup"><span data-stu-id="55b5c-227">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="55b5c-228">**[A]** Configure corosync para usar otro tipo de transporte y agregue nodelist.</span><span class="sxs-lookup"><span data-stu-id="55b5c-228">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="55b5c-229">De lo contrario, el clúster no funcionará.</span><span class="sxs-lookup"><span data-stu-id="55b5c-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="55b5c-230">Agregue el siguiente contenido en negrita al archivo.</span><span class="sxs-lookup"><span data-stu-id="55b5c-230">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="55b5c-231">Después, reinicie el servicio corosync</span><span class="sxs-lookup"><span data-stu-id="55b5c-231">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="55b5c-232">**[A]** Instale los componentes de drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="55b5c-233">**[A]** Cree una partición para el dispositivo drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-233">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="55b5c-234">**[A]** Cree configuraciones de LVM</span><span class="sxs-lookup"><span data-stu-id="55b5c-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="55b5c-235">**[A]** Cree el dispositivo drbd NFS</span><span class="sxs-lookup"><span data-stu-id="55b5c-235">**[A]** Create the NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="55b5c-236">Inserte la configuración del nuevo dispositivo drbd y salga</span><span class="sxs-lookup"><span data-stu-id="55b5c-236">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="55b5c-237">Cree el dispositivo drbd e inícielo</span><span class="sxs-lookup"><span data-stu-id="55b5c-237">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="55b5c-238">**[1]** Omita la sincronización inicial</span><span class="sxs-lookup"><span data-stu-id="55b5c-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="55b5c-239">**[1]** Establezca el nodo principal</span><span class="sxs-lookup"><span data-stu-id="55b5c-239">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="55b5c-240">**[1]** Espere hasta que se sincronicen los nuevos dispositivos drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-240">**[1]** Wait until the new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="55b5c-241">**[1]** Cree sistemas de archivos en los dispositivos drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-241">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="55b5c-242">Configuración de la plataforma del clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="55b5c-243">**[1]** Cambie la configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="55b5c-243">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="55b5c-244">**[1]** Agregue el dispositivo drbd NFS a la configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-244">**[1]** Add the NFS drbd device to the cluster configuration</span></span>

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

1. <span data-ttu-id="55b5c-245">**[1]** Cree el servidor NFS</span><span class="sxs-lookup"><span data-stu-id="55b5c-245">**[1]** Create the NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="55b5c-246">**[1]** Cree los recursos del sistema de archivos NFS</span><span class="sxs-lookup"><span data-stu-id="55b5c-246">**[1]** Create the NFS File System resources</span></span>

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

1. <span data-ttu-id="55b5c-247">**[1]** Cree las exportaciones NFS</span><span class="sxs-lookup"><span data-stu-id="55b5c-247">**[1]** Create the NFS exports</span></span>

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

1. <span data-ttu-id="55b5c-248">**[1]** Cree un recurso IP virtual y sondeo de mantenimiento para el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="55b5c-248">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="55b5c-249">Creación de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-249">Create STONITH device</span></span>

<span data-ttu-id="55b5c-250">El dispositivo STONITH usa una entidad de servicio para la autorización de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="55b5c-250">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="55b5c-251">Siga estos pasos para crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="55b5c-251">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="55b5c-252">Vaya a <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="55b5c-252">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="55b5c-253">Abra la hoja Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55b5c-253">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="55b5c-254">Vaya a Propiedades y anote el identificador del directorio.</span><span class="sxs-lookup"><span data-stu-id="55b5c-254">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="55b5c-255">Se trata del **id. de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="55b5c-255">This is the **tenant id**.</span></span>
1. <span data-ttu-id="55b5c-256">Haga clic en Registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="55b5c-256">Click App registrations</span></span>
1. <span data-ttu-id="55b5c-257">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="55b5c-257">Click Add</span></span>
1. <span data-ttu-id="55b5c-258">Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear</span><span class="sxs-lookup"><span data-stu-id="55b5c-258">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="55b5c-259">La dirección URL de inicio de sesión no se usa y puede ser cualquier dirección URL válida</span><span class="sxs-lookup"><span data-stu-id="55b5c-259">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="55b5c-260">Seleccione la nueva aplicación y haga clic en las llaves de la pestaña Configuración</span><span class="sxs-lookup"><span data-stu-id="55b5c-260">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="55b5c-261">Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar</span><span class="sxs-lookup"><span data-stu-id="55b5c-261">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="55b5c-262">Anote el valor.</span><span class="sxs-lookup"><span data-stu-id="55b5c-262">Write down the Value.</span></span> <span data-ttu-id="55b5c-263">Se utiliza como **contraseña** para la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="55b5c-263">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="55b5c-264">Anote el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55b5c-264">Write down the Application Id.</span></span> <span data-ttu-id="55b5c-265">Se utiliza como nombre de usuario (**Id. de inicio de sesión** en los pasos siguientes) de la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="55b5c-265">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="55b5c-266">La entidad de servicio no tiene permiso para tener acceso a los recursos de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="55b5c-266">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="55b5c-267">Debe concedérselos para iniciar y detener (desasignar) todas las máquinas virtuales del clúster.</span><span class="sxs-lookup"><span data-stu-id="55b5c-267">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="55b5c-268">Vaya a https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="55b5c-268">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="55b5c-269">Abra la hoja Todos los recursos</span><span class="sxs-lookup"><span data-stu-id="55b5c-269">Open the All resources blade</span></span>
1. <span data-ttu-id="55b5c-270">Seleccione la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="55b5c-270">Select the virtual machine</span></span>
1. <span data-ttu-id="55b5c-271">Haga clic en Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="55b5c-271">Click Access control (IAM)</span></span>
1. <span data-ttu-id="55b5c-272">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="55b5c-272">Click Add</span></span>
1. <span data-ttu-id="55b5c-273">Seleccione el rol de propietario</span><span class="sxs-lookup"><span data-stu-id="55b5c-273">Select the role Owner</span></span>
1. <span data-ttu-id="55b5c-274">Escriba el nombre de la aplicación que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="55b5c-274">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="55b5c-275">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="55b5c-275">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="55b5c-276">**[1]** Cree los dispositivos STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-276">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="55b5c-277">Después de editar los permisos para las máquinas virtuales, puede configurar los dispositivos STONITH en el clúster.</span><span class="sxs-lookup"><span data-stu-id="55b5c-277">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="55b5c-278">**[1]** Habilite el uso de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-278">**[1]** Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="55b5c-279">Configuración de (A)SCS</span><span class="sxs-lookup"><span data-stu-id="55b5c-279">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="55b5c-280">Implementación de Linux</span><span class="sxs-lookup"><span data-stu-id="55b5c-280">Deploying Linux</span></span>

<span data-ttu-id="55b5c-281">Azure Marketplace contiene una imagen de SUSE Linux Enterprise Server para SAP Applications 12 que puede usar para implementar nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="55b5c-281">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span> <span data-ttu-id="55b5c-282">La imagen de Marketplace contiene el agente de recursos para SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="55b5c-282">The marketplace image contains the resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="55b5c-283">Para implementar todos los recursos necesarios, puede usar una de las plantillas de inicio rápido de github.</span><span class="sxs-lookup"><span data-stu-id="55b5c-283">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="55b5c-284">La plantilla implementa las máquinas virtuales, el equilibrador de carga, el conjunto de disponibilidad, etc. Siga estos pasos para implementar la plantilla:</span><span class="sxs-lookup"><span data-stu-id="55b5c-284">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="55b5c-285">Abra la [plantilla ASCS/SCS de varios SID][template-multisid-xscs] o la [plantilla convergente][template-converged] en Azure Portal. La plantilla ASCS/SCS solo crea las reglas de equilibrio de carga para las instancias ASCS/SCS y ERS (solo Linux) de SAP NetWeaver, mientras que la plantilla convergente también crea las reglas de equilibrio de carga para una base de datos (por ejemplo, Microsoft SQL Server o SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="55b5c-285">Open the [ASCS/SCS Multi SID template][template-multisid-xscs] or the [converged template][template-converged] on the Azure portal The ASCS/SCS template only creates the load-balancing rules for the SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas the converged template also creates the load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="55b5c-286">Si tiene previsto instalar un sistema basado en SAP NetWeaver y desea instalar la base de datos en las mismas máquinas, use la [plantilla convergente][template-converged].</span><span class="sxs-lookup"><span data-stu-id="55b5c-286">If you plan to install an SAP NetWeaver based system and you also want to install the database on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="55b5c-287">Escriba los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="55b5c-287">Enter the following parameters</span></span>
   1. <span data-ttu-id="55b5c-288">Prefijo de recurso (solo la plantilla de varios ASCS/SCS de varios SID)</span><span class="sxs-lookup"><span data-stu-id="55b5c-288">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="55b5c-289">Escriba el prefijo que desea usar.</span><span class="sxs-lookup"><span data-stu-id="55b5c-289">Enter the prefix you want to use.</span></span> <span data-ttu-id="55b5c-290">El valor se usa como prefijo de los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="55b5c-290">The value is used as a prefix for the resources that are deployed.</span></span>
   3. <span data-ttu-id="55b5c-291">Identificador del sistema SAP (solo la plantilla convergente)</span><span class="sxs-lookup"><span data-stu-id="55b5c-291">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="55b5c-292">Escriba el identificador del sistema SAP que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="55b5c-292">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="55b5c-293">El identificador se usa como prefijo de los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="55b5c-293">The Id is used as a prefix for the resources that are deployed.</span></span>
   4. <span data-ttu-id="55b5c-294">Tipo de pila</span><span class="sxs-lookup"><span data-stu-id="55b5c-294">Stack Type</span></span>  
      <span data-ttu-id="55b5c-295">Seleccione el tipo de la pila de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="55b5c-295">Select the SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="55b5c-296">Tipo de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="55b5c-296">Os Type</span></span>  
      <span data-ttu-id="55b5c-297">Seleccione una de las distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="55b5c-297">Select one of the Linux distributions.</span></span> <span data-ttu-id="55b5c-298">En este ejemplo, seleccione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="55b5c-298">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="55b5c-299">Tipo de base de datos</span><span class="sxs-lookup"><span data-stu-id="55b5c-299">Db Type</span></span>  
      <span data-ttu-id="55b5c-300">Seleccione HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-300">Select HANA</span></span>
   7. <span data-ttu-id="55b5c-301">Tamaño del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="55b5c-301">Sap System Size</span></span>  
      <span data-ttu-id="55b5c-302">La cantidad de SAPS que proporciona el sistema nuevo.</span><span class="sxs-lookup"><span data-stu-id="55b5c-302">The amount of SAPS the new system provides.</span></span> <span data-ttu-id="55b5c-303">Si no está seguro de cuántos SAPS necesita el sistema, consulte con el integrador de sistemas o el asociado tecnológico de SAP</span><span class="sxs-lookup"><span data-stu-id="55b5c-303">If you are not sure how many SAPS the system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="55b5c-304">Disponibilidad del sistema</span><span class="sxs-lookup"><span data-stu-id="55b5c-304">System Availability</span></span>  
      <span data-ttu-id="55b5c-305">Seleccione alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="55b5c-305">Select HA</span></span>
   9. <span data-ttu-id="55b5c-306">Nombre de usuario y contraseña del administrador</span><span class="sxs-lookup"><span data-stu-id="55b5c-306">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="55b5c-307">Se crea un usuario nuevo que se puede usar para iniciar sesión en la máquina.</span><span class="sxs-lookup"><span data-stu-id="55b5c-307">A new user is created that can be used to log on to the machine.</span></span>
   10. <span data-ttu-id="55b5c-308">Identificador de subred</span><span class="sxs-lookup"><span data-stu-id="55b5c-308">Subnet Id</span></span>  
   <span data-ttu-id="55b5c-309">El identificador de la subred a la que deben conectarse las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="55b5c-309">The ID of the subnet to which the virtual machines should be connected to.</span></span>  <span data-ttu-id="55b5c-310">Deje el valor en blanco si desea crear una red virtual nueva o seleccione la misma subred que usó o creó como parte de la implementación del servidor NFS.</span><span class="sxs-lookup"><span data-stu-id="55b5c-310">Leave empty if you want to create a new virtual network or select the same subnet that you used or created as part of the NFS server deployment.</span></span> <span data-ttu-id="55b5c-311">El identificador suele tener este aspecto /subscriptions/**&lt;id. de suscripción&gt;**/resourceGroups/**&lt;nombre del grupo de recursos&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nombre de red virtual&gt;**/subnets/**&lt;nombre de subred&gt;**</span><span class="sxs-lookup"><span data-stu-id="55b5c-311">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="55b5c-312">Instalación</span><span class="sxs-lookup"><span data-stu-id="55b5c-312">Installation</span></span>

<span data-ttu-id="55b5c-313">Los elementos siguientes tienen el prefijo **[A]**: aplicable a todos los nodos, **[1]**: aplicable solo al nodo 1 o **[2]**: aplicable solo al nodo 2.</span><span class="sxs-lookup"><span data-stu-id="55b5c-313">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="55b5c-314">**[A]** Actualice SLES</span><span class="sxs-lookup"><span data-stu-id="55b5c-314">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="55b5c-315">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="55b5c-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="55b5c-316">**[2]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="55b5c-316">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="55b5c-317">**[1]** Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="55b5c-317">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="55b5c-318">**[A]** Instale la extensión de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="55b5c-318">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="55b5c-319">**[A]** Actualice los agentes de recursos de SAP</span><span class="sxs-lookup"><span data-stu-id="55b5c-319">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="55b5c-320">Se requiere una revisión del paquete de agentes de recursos para usar la configuración nueva, que es la que describe este artículo.</span><span class="sxs-lookup"><span data-stu-id="55b5c-320">A patch for the resource-agents package is required to use the new configuration, that is described in this article.</span></span> <span data-ttu-id="55b5c-321">Puede usar el comando siguiente para comprobar si la revisión ya está instalada</span><span class="sxs-lookup"><span data-stu-id="55b5c-321">You can check, if the patch is already installed with the following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="55b5c-322">La salida debe ser similar a</span><span class="sxs-lookup"><span data-stu-id="55b5c-322">The output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="55b5c-323">Si el comando grep no encuentra el parámetro IS_ERS, necesita instalar la revisión que aparece en [la página de descarga de SUSE](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="55b5c-323">If the grep command does not find the IS_ERS parameter, you need to install the patch listed on [the SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="55b5c-324">**[A]** Configure la resolución nombres de host</span><span class="sxs-lookup"><span data-stu-id="55b5c-324">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="55b5c-325">Puede usar un servidor DNS o modificar /etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-325">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="55b5c-326">En este ejemplo se muestra cómo utilizar el archivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="55b5c-326">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="55b5c-327">Reemplace la dirección IP y el nombre de host en los siguientes comandos</span><span class="sxs-lookup"><span data-stu-id="55b5c-327">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="55b5c-328">Inserte las siguientes líneas en /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="55b5c-328">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="55b5c-329">Cambie la dirección IP y el nombre de host para que coincida con su entorno</span><span class="sxs-lookup"><span data-stu-id="55b5c-329">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="55b5c-330">**[1]** Instale el clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-330">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="55b5c-331">**[2]** Agregue un nodo al clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-331">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="55b5c-332">**[A]** Haga que la contraseña de hacluster coincida</span><span class="sxs-lookup"><span data-stu-id="55b5c-332">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="55b5c-333">**[A]** Configure corosync para usar otro tipo de transporte y agregue nodelist.</span><span class="sxs-lookup"><span data-stu-id="55b5c-333">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="55b5c-334">De lo contrario, el clúster no funcionará.</span><span class="sxs-lookup"><span data-stu-id="55b5c-334">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="55b5c-335">Agregue el siguiente contenido en negrita al archivo.</span><span class="sxs-lookup"><span data-stu-id="55b5c-335">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="55b5c-336">Después, reinicie el servicio corosync</span><span class="sxs-lookup"><span data-stu-id="55b5c-336">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="55b5c-337">**[A]** Instale los componentes de drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-337">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="55b5c-338">**[A]** Cree una partición para el dispositivo drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-338">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="55b5c-339">**[A]** Cree configuraciones de LVM</span><span class="sxs-lookup"><span data-stu-id="55b5c-339">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="55b5c-340">**[A]** Cree el dispositivo drbd SCS</span><span class="sxs-lookup"><span data-stu-id="55b5c-340">**[A]** Create the SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="55b5c-341">Inserte la configuración del nuevo dispositivo drbd y salga</span><span class="sxs-lookup"><span data-stu-id="55b5c-341">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="55b5c-342">Cree el dispositivo drbd e inícielo</span><span class="sxs-lookup"><span data-stu-id="55b5c-342">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="55b5c-343">**[A]** Cree el dispositivo drbd ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-343">**[A]** Create the ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="55b5c-344">Inserte la configuración del nuevo dispositivo drbd y salga</span><span class="sxs-lookup"><span data-stu-id="55b5c-344">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="55b5c-345">Cree el dispositivo drbd e inícielo</span><span class="sxs-lookup"><span data-stu-id="55b5c-345">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="55b5c-346">**[1]** Omita la sincronización inicial</span><span class="sxs-lookup"><span data-stu-id="55b5c-346">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="55b5c-347">**[1]** Establezca el nodo principal</span><span class="sxs-lookup"><span data-stu-id="55b5c-347">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="55b5c-348">**[1]** Espere hasta que se sincronicen los nuevos dispositivos drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-348">**[1]** Wait until the new drbd devices are synchronized</span></span>

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

1. <span data-ttu-id="55b5c-349">**[1]** Cree sistemas de archivos en los dispositivos drbd</span><span class="sxs-lookup"><span data-stu-id="55b5c-349">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="55b5c-350">Configuración de la plataforma del clúster</span><span class="sxs-lookup"><span data-stu-id="55b5c-350">Configure Cluster Framework</span></span>

<span data-ttu-id="55b5c-351">**[1]** Cambie la configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="55b5c-351">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="55b5c-352">Preparación de la instalación de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="55b5c-352">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="55b5c-353">**[A]** Cree los directorios compartidos</span><span class="sxs-lookup"><span data-stu-id="55b5c-353">**[A]** Create the shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="55b5c-354">**[A]** Configure autofs</span><span class="sxs-lookup"><span data-stu-id="55b5c-354">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="55b5c-355">Cree un archivo con</span><span class="sxs-lookup"><span data-stu-id="55b5c-355">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="55b5c-356">Reinicie autofs para montar los recursos compartidos nuevos</span><span class="sxs-lookup"><span data-stu-id="55b5c-356">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="55b5c-357">**[A]** Configure el archivo de intercambio</span><span class="sxs-lookup"><span data-stu-id="55b5c-357">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="55b5c-358">Reinicie el agente para activar el cambio</span><span class="sxs-lookup"><span data-stu-id="55b5c-358">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="55b5c-359">Instalación de SAP NetWeaver ASCS/ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-359">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="55b5c-360">**[1]** Cree un recurso IP virtual y sondeo de mantenimiento para el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="55b5c-360">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

   <span data-ttu-id="55b5c-361">Asegúrese de que el estado del clúster sea el correcto y que se iniciaron todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-361">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="55b5c-362">No es importante en qué nodo se ejecutan los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-362">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="55b5c-363">**[1]** Instale SAP NetWeaver ASCS</span><span class="sxs-lookup"><span data-stu-id="55b5c-363">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="55b5c-364">Instale SAP NetWeaver ASCS como raíz en el primer nodo mediante un nombre de host virtual que se asigna a la dirección IP de la configuración de front-end del equilibrador de carga para ASCS, por ejemplo, <b>nws-ascs</b>, <b>10.0.0.10</b> y el número de instancia que usó para el sondeo del equilibrador de carga, por ejemplo, <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="55b5c-364">Install SAP NetWeaver ASCS as root on the first node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and the instance number that you used for the probe of the load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="55b5c-365">Puede usar el parámetro de sapinst SAPINST_REMOTE_ACCESS_USER para permitir que un usuario no raíz se conecta a sapinst.</span><span class="sxs-lookup"><span data-stu-id="55b5c-365">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="55b5c-366">**[1]** Cree un recurso IP virtual y sondeo de mantenimiento para el equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="55b5c-366">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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
   # Do you still want to commit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="55b5c-367">Asegúrese de que el estado del clúster sea el correcto y que se iniciaron todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-367">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="55b5c-368">No es importante en qué nodo se ejecutan los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-368">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="55b5c-369">**[2]** Instale SAP NetWeaver ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-369">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="55b5c-370">Instale SAP NetWeaver ERS como raíz en el segundo nodo mediante un nombre de host virtual que se asigna a la dirección IP de la configuración de front-end del equilibrador de carga para ERS, por ejemplo, <b>nws-ers</b>, <b>10.0.0.11</b> y el número de instancia que usó para el sondeo del equilibrador de carga, por ejemplo, <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="55b5c-370">Install SAP NetWeaver ERS as root on the second node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and the instance number that you used for the probe of the load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="55b5c-371">Puede usar el parámetro de sapinst SAPINST_REMOTE_ACCESS_USER para permitir que un usuario no raíz se conecta a sapinst.</span><span class="sxs-lookup"><span data-stu-id="55b5c-371">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="55b5c-372">Use SWPM SP 20 PL 05 o superior.</span><span class="sxs-lookup"><span data-stu-id="55b5c-372">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="55b5c-373">Las versiones inferiores no establecen correctamente los permisos y se producirá un error de instalación.</span><span class="sxs-lookup"><span data-stu-id="55b5c-373">Lower versions do not set the permissions correctly and the installation will fail.</span></span>
   > 

1. <span data-ttu-id="55b5c-374">**[1]** Adapte los perfiles de instancias ASCS/SCS y ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-374">**[1]** Adapt the ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="55b5c-375">Perfil ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="55b5c-375">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change the restart command to a start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add the keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="55b5c-376">Perfil ERS</span><span class="sxs-lookup"><span data-stu-id="55b5c-376">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="55b5c-377">**[A]** Configure la conexión persistente</span><span class="sxs-lookup"><span data-stu-id="55b5c-377">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="55b5c-378">La comunicación entre el servidor de aplicaciones de SAP NetWeaver y ASCS/SCS se enruta a través de un equilibrador de carga de software.</span><span class="sxs-lookup"><span data-stu-id="55b5c-378">The communication between the SAP NetWeaver application server and the ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="55b5c-379">El equilibrador de carga desconecta las conexiones inactivas después de un tiempo de expiración que se puede configurar.</span><span class="sxs-lookup"><span data-stu-id="55b5c-379">The load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="55b5c-380">Para evitar esto, debe establecer un parámetro en el perfil de SAP NetWeaver ASCS/SCS y cambiar la configuración del sistema Linux.</span><span class="sxs-lookup"><span data-stu-id="55b5c-380">To prevent this you need to set a parameter in the SAP NetWeaver ASCS/SCS profile and change the Linux system settings.</span></span> <span data-ttu-id="55b5c-381">Consulte la [nota de SAP 1410736][1410736] para más información.</span><span class="sxs-lookup"><span data-stu-id="55b5c-381">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="55b5c-382">El parámetro del perfil ASCS/SCS enque/encni/set_so_keepalive ya se agregó en el último paso.</span><span class="sxs-lookup"><span data-stu-id="55b5c-382">The ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in the last step.</span></span>

   <pre><code> 
   # Change the Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="55b5c-383">**[A]** Configure los usuarios de SAP después de la instalación</span><span class="sxs-lookup"><span data-stu-id="55b5c-383">**[A]** Configure the SAP users after the installation</span></span>
 
   <pre><code>
   # Add sidadm to the haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="55b5c-384">**[1]** Agregue los servicios SAP de ASCS y ERS al archivo sapservice</span><span class="sxs-lookup"><span data-stu-id="55b5c-384">**[1]** Add the ASCS and ERS SAP services to the sapservice file</span></span>

   <span data-ttu-id="55b5c-385">Agregue la entrada del servicio ASCS al segundo nodo y copie la entrada del servicio ERS al primer nodo.</span><span class="sxs-lookup"><span data-stu-id="55b5c-385">Add the ASCS service entry to the second node and copy the ERS service entry to the first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="55b5c-386">**[1]** Cree los recursos de clúster de SAP</span><span class="sxs-lookup"><span data-stu-id="55b5c-386">**[1]** Create the SAP cluster resources</span></span>

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

   <span data-ttu-id="55b5c-387">Asegúrese de que el estado del clúster sea el correcto y que se iniciaron todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-387">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="55b5c-388">No es importante en qué nodo se ejecutan los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-388">It is not important on which node the resources are running.</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="55b5c-389">Creación de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-389">Create STONITH device</span></span>

<span data-ttu-id="55b5c-390">El dispositivo STONITH usa una entidad de servicio para la autorización de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="55b5c-390">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="55b5c-391">Siga estos pasos para crear una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="55b5c-391">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="55b5c-392">Vaya a <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="55b5c-392">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="55b5c-393">Abra la hoja Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55b5c-393">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="55b5c-394">Vaya a Propiedades y anote el identificador del directorio.</span><span class="sxs-lookup"><span data-stu-id="55b5c-394">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="55b5c-395">Se trata del **id. de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="55b5c-395">This is the **tenant id**.</span></span>
1. <span data-ttu-id="55b5c-396">Haga clic en Registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="55b5c-396">Click App registrations</span></span>
1. <span data-ttu-id="55b5c-397">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="55b5c-397">Click Add</span></span>
1. <span data-ttu-id="55b5c-398">Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear</span><span class="sxs-lookup"><span data-stu-id="55b5c-398">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="55b5c-399">La dirección URL de inicio de sesión no se usa y puede ser cualquier dirección URL válida</span><span class="sxs-lookup"><span data-stu-id="55b5c-399">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="55b5c-400">Seleccione la nueva aplicación y haga clic en las llaves de la pestaña Configuración</span><span class="sxs-lookup"><span data-stu-id="55b5c-400">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="55b5c-401">Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar</span><span class="sxs-lookup"><span data-stu-id="55b5c-401">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="55b5c-402">Anote el valor.</span><span class="sxs-lookup"><span data-stu-id="55b5c-402">Write down the Value.</span></span> <span data-ttu-id="55b5c-403">Se utiliza como **contraseña** para la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="55b5c-403">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="55b5c-404">Anote el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55b5c-404">Write down the Application Id.</span></span> <span data-ttu-id="55b5c-405">Se utiliza como nombre de usuario (**Id. de inicio de sesión** en los pasos siguientes) de la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="55b5c-405">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="55b5c-406">La entidad de servicio no tiene permiso para tener acceso a los recursos de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="55b5c-406">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="55b5c-407">Debe concedérselos para iniciar y detener (desasignar) todas las máquinas virtuales del clúster.</span><span class="sxs-lookup"><span data-stu-id="55b5c-407">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="55b5c-408">Vaya a https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="55b5c-408">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="55b5c-409">Abra la hoja Todos los recursos</span><span class="sxs-lookup"><span data-stu-id="55b5c-409">Open the All resources blade</span></span>
1. <span data-ttu-id="55b5c-410">Seleccione la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="55b5c-410">Select the virtual machine</span></span>
1. <span data-ttu-id="55b5c-411">Haga clic en Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="55b5c-411">Click Access control (IAM)</span></span>
1. <span data-ttu-id="55b5c-412">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="55b5c-412">Click Add</span></span>
1. <span data-ttu-id="55b5c-413">Seleccione el rol de propietario</span><span class="sxs-lookup"><span data-stu-id="55b5c-413">Select the role Owner</span></span>
1. <span data-ttu-id="55b5c-414">Escriba el nombre de la aplicación que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="55b5c-414">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="55b5c-415">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="55b5c-415">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="55b5c-416">**[1]** Cree los dispositivos STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-416">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="55b5c-417">Después de editar los permisos para las máquinas virtuales, puede configurar los dispositivos STONITH en el clúster.</span><span class="sxs-lookup"><span data-stu-id="55b5c-417">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="55b5c-418">**[1]** Habilite el uso de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-418">**[1]** Enable the use of a STONITH device</span></span>

<span data-ttu-id="55b5c-419">Habilite el uso de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="55b5c-419">Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="55b5c-420">Instalar la base de datos</span><span class="sxs-lookup"><span data-stu-id="55b5c-420">Install database</span></span>

<span data-ttu-id="55b5c-421">En este ejemplo, hay una replicación del sistema SAP HANA instalada y configurada.</span><span class="sxs-lookup"><span data-stu-id="55b5c-421">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="55b5c-422">SAP HANA se ejecutará en el mismo clúster que SAP NetWeaver ASCS/SCS y ERS.</span><span class="sxs-lookup"><span data-stu-id="55b5c-422">SAP HANA will run in the same cluster as the SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="55b5c-423">También puede instalar SAP HANA en un clúster dedicado.</span><span class="sxs-lookup"><span data-stu-id="55b5c-423">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="55b5c-424">Consulte [Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure][sap-hana-ha] para más información.</span><span class="sxs-lookup"><span data-stu-id="55b5c-424">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="55b5c-425">Preparación de la instalación de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-425">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="55b5c-426">Por lo general, se recomienda usar LVM para volúmenes de almacén de datos y archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="55b5c-426">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="55b5c-427">Con fines de prueba, también puede elegir almacenar los datos y el archivo de registro directamente en un disco sin formato.</span><span class="sxs-lookup"><span data-stu-id="55b5c-427">For testing purposes, you can also choose to store the data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="55b5c-428">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="55b5c-428">**[A]** LVM</span></span>  
   <span data-ttu-id="55b5c-429">En el ejemplo siguiente se supone que las máquinas virtuales tienen cuatro discos de datos conectados que se deben usar para crear dos volúmenes.</span><span class="sxs-lookup"><span data-stu-id="55b5c-429">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
   
   <span data-ttu-id="55b5c-430">Cree volúmenes físicos de todos los discos que desee usar.</span><span class="sxs-lookup"><span data-stu-id="55b5c-430">Create physical volumes for all disks that you want to use.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="55b5c-431">Cree un grupo de volúmenes para los archivos de datos, un grupo de volúmenes para los archivos de registro y otro para el directorio compartido de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-431">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="55b5c-432">Cree los volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="55b5c-432">Create the logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="55b5c-433">Cree los directorios de montaje y copie el UUID de todos los volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="55b5c-433">Create the mount directories and copy the UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="55b5c-434">Cree entradas de autofs para los tres volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="55b5c-434">Create autofs entries for the three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="55b5c-435">Inserte esta línea en sudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="55b5c-435">Insert this line to sudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="55b5c-436">Monte los volúmenes nuevos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-436">Mount the new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="55b5c-437">**[A]** Discos sin formatos</span><span class="sxs-lookup"><span data-stu-id="55b5c-437">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="55b5c-438">Para sistemas pequeños o de demostración, puede colocar los archivos de datos y de registro HANA en un disco.</span><span class="sxs-lookup"><span data-stu-id="55b5c-438">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="55b5c-439">Con los siguientes comandos se crea una partición en /dev/sdc y con formato xfs.</span><span class="sxs-lookup"><span data-stu-id="55b5c-439">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down the id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="55b5c-440">Inserte esta línea en /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="55b5c-440">Insert this line to /etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="55b5c-441">Cree el directorio de destino y monte el disco.</span><span class="sxs-lookup"><span data-stu-id="55b5c-441">Create the target directory and mount the disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="55b5c-442">Instalación de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-442">Installing SAP HANA</span></span>

<span data-ttu-id="55b5c-443">Los siguientes pasos se basan en el capítulo 4 de la [Guía del escenario de rendimiento optimizado para la replicación del sistema de SAP HANA][suse-hana-ha-guide] para instalar la replicación del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="55b5c-443">The following steps are based on chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span> <span data-ttu-id="55b5c-444">Léalo antes de seguir con la instalación.</span><span class="sxs-lookup"><span data-stu-id="55b5c-444">Please read it before you continue the installation.</span></span>

1. <span data-ttu-id="55b5c-445">**[A]** Ejecute hdblcm desde el DVD de HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-445">**[A]** Run hdblcm from the HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="55b5c-446">**[A]** Actualice el agente de host de SAP</span><span class="sxs-lookup"><span data-stu-id="55b5c-446">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="55b5c-447">Descargue el archivo más reciente del agente de host de SAP desde [SAP Softwarecenter][sap-swcenter] y ejecute el siguiente comando para actualizar el agente.</span><span class="sxs-lookup"><span data-stu-id="55b5c-447">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="55b5c-448">Reemplace la ruta de acceso al archivo para que apunte al archivo que descargó.</span><span class="sxs-lookup"><span data-stu-id="55b5c-448">Replace the path to the archive to point to the file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path to SAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="55b5c-449">**[1]** Cree la replicación de HANA (como raíz)</span><span class="sxs-lookup"><span data-stu-id="55b5c-449">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="55b5c-450">Ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="55b5c-450">Run the following command.</span></span> <span data-ttu-id="55b5c-451">Asegúrese de reemplazar las cadenas en negrita (HDB de Id. de sistema de HANA y número de instancia 03) con los valores de la instalación de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="55b5c-451">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="55b5c-452">**[A]** Cree la entrada de almacén de claves (como raíz)</span><span class="sxs-lookup"><span data-stu-id="55b5c-452">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="55b5c-453">**[1]** Realice la copia de seguridad de la base de datos (como raíz)</span><span class="sxs-lookup"><span data-stu-id="55b5c-453">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="55b5c-454">**[1]** Cambie al usuario sapsid HANA y cree el sitio principal</span><span class="sxs-lookup"><span data-stu-id="55b5c-454">**[1]** Switch to the HANA sapsid user and create the primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="55b5c-455">**[2]** Cambie al usuario sapsid HANA y cree el sitio secundario</span><span class="sxs-lookup"><span data-stu-id="55b5c-455">**[2]** Switch to the HANA sapsid user and create the secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="55b5c-456">**[1]** Creación de recursos de clúster de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-456">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="55b5c-457">Primero, cree la topología.</span><span class="sxs-lookup"><span data-stu-id="55b5c-457">First, create the topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number and HANA system id
   
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
   
   <span data-ttu-id="55b5c-458">A continuación, cree los recursos de HANA.</span><span class="sxs-lookup"><span data-stu-id="55b5c-458">Next, create the HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
    
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

   <span data-ttu-id="55b5c-459">Asegúrese de que el estado del clúster sea el correcto y que se iniciaron todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-459">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="55b5c-460">No es importante en qué nodo se ejecutan los recursos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-460">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="55b5c-461">**[1]** Instale la instancia de base de datos de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="55b5c-461">**[1]** Install the SAP NetWeaver database instance</span></span>

   <span data-ttu-id="55b5c-462">Instale la instancia de base de datos de SAP NetWeaver como raíz con un nombre de host virtual que se asigna a la dirección IP de la configuración front-end del equilibrador de carga para la base de datos, por ejemplo, <b>nws-db</b> y <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="55b5c-462">Install the SAP NetWeaver database instance as root using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="55b5c-463">Puede usar el parámetro de sapinst SAPINST_REMOTE_ACCESS_USER para permitir que un usuario no raíz se conecta a sapinst.</span><span class="sxs-lookup"><span data-stu-id="55b5c-463">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="55b5c-464">Instalación del servidor de aplicaciones de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="55b5c-464">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="55b5c-465">Siga estos pasos para instalar un servidor de aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="55b5c-465">Follow these steps to install an SAP application server.</span></span> <span data-ttu-id="55b5c-466">En los pasos siguientes se supone que instala el servidor de aplicaciones en un servidor distinto de los servidores ASCS/SCS y HANA.</span><span class="sxs-lookup"><span data-stu-id="55b5c-466">The steps bellow assume that you install the application server on a server different from the ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="55b5c-467">De lo contrario, no se necesitan algunos de los pasos que aparecen a continuación (como configurar la resolución de nombres de host).</span><span class="sxs-lookup"><span data-stu-id="55b5c-467">Otherwise some of the steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="55b5c-468">Configure la resolución de nombres de host</span><span class="sxs-lookup"><span data-stu-id="55b5c-468">Setup host name resolution</span></span>    
   <span data-ttu-id="55b5c-469">Puede usar un servidor DNS o modificar /etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="55b5c-469">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="55b5c-470">En este ejemplo se muestra cómo utilizar el archivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="55b5c-470">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="55b5c-471">Reemplace la dirección IP y el nombre de host en los siguientes comandos</span><span class="sxs-lookup"><span data-stu-id="55b5c-471">Replace the IP address and the hostname in the following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="55b5c-472">Inserte las siguientes líneas en /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="55b5c-472">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="55b5c-473">Cambie la dirección IP y el nombre de host para que coincida con su entorno</span><span class="sxs-lookup"><span data-stu-id="55b5c-473">Change the IP address and hostname to match your environment</span></span>    
    
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of the application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="55b5c-474">Cree el directorio sapmnt</span><span class="sxs-lookup"><span data-stu-id="55b5c-474">Create the sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="55b5c-475">Configure autofs</span><span class="sxs-lookup"><span data-stu-id="55b5c-475">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="55b5c-476">Cree un nuevo archivo con</span><span class="sxs-lookup"><span data-stu-id="55b5c-476">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="55b5c-477">Reinicie autofs para montar los recursos compartidos nuevos</span><span class="sxs-lookup"><span data-stu-id="55b5c-477">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="55b5c-478">Configure el archivo de intercambio</span><span class="sxs-lookup"><span data-stu-id="55b5c-478">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="55b5c-479">Reinicie el agente para activar el cambio</span><span class="sxs-lookup"><span data-stu-id="55b5c-479">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="55b5c-480">Instale el servidor de aplicaciones de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="55b5c-480">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="55b5c-481">Instale un servidor de aplicaciones de SAP NetWeaver principal o adicional.</span><span class="sxs-lookup"><span data-stu-id="55b5c-481">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="55b5c-482">Puede usar el parámetro de sapinst SAPINST_REMOTE_ACCESS_USER para permitir que un usuario no raíz se conecta a sapinst.</span><span class="sxs-lookup"><span data-stu-id="55b5c-482">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="55b5c-483">Actualice el almacenamiento seguro de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="55b5c-483">Update SAP HANA secure store</span></span>

   <span data-ttu-id="55b5c-484">Actualice el almacenamiento seguro de SAP HANA que apunte al nombre virtual de la configuración de la replicación del sistema SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="55b5c-484">Update the SAP HANA secure store to point to the virtual name of the SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="55b5c-485">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55b5c-485">Next steps</span></span>
* <span data-ttu-id="55b5c-486">[Planeación e implementación de Azure Virtual Machines para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-486">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="55b5c-487">[Implementación de Azure Virtual Machines para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-487">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="55b5c-488">[Implementación de DBMS de Azure Virtual Machines para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="55b5c-488">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="55b5c-489">Para obtener información sobre cómo establecer la alta disponibilidad y planear la recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [Alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes)](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="55b5c-489">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="55b5c-490">Para información sobre cómo establecer la alta disponibilidad y planear la recuperación ante desastres de SAP HANA en máquinas virtuales de Azure, consulte [Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="55b5c-490">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>