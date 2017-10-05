---
title: "Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure | Microsoft Docs"
description: "Establezca alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="283b9-103">Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure</span><span class="sxs-lookup"><span data-stu-id="283b9-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="283b9-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="283b9-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="283b9-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="283b9-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="283b9-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="283b9-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="283b9-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="283b9-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="283b9-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="283b9-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="283b9-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="283b9-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="283b9-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="283b9-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="283b9-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="283b9-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="283b9-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="283b9-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="283b9-113">Localmente, puede usar la replicación del sistema de HANA o el almacenamiento compartido para establecer la alta disponibilidad para SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="283b9-114">Actualmente solo se admite la configuración de la replicación del sistema de HANA en Azure.</span><span class="sxs-lookup"><span data-stu-id="283b9-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="283b9-115">La replicación de SAP HANA se realiza con un nodo maestro y al menos uno subordinado.</span><span class="sxs-lookup"><span data-stu-id="283b9-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="283b9-116">Los cambios en los datos del nodo maestro se replican en los subordinados de forma sincrónica o asincrónica.</span><span class="sxs-lookup"><span data-stu-id="283b9-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="283b9-117">En este artículo se describe cómo implementar las máquinas virtuales, configurarlas, instalar la plataforma del clúster, e instalar y configurar la replicación del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="283b9-118">En las configuraciones de ejemplo, los comandos de instalación, etc., se usa el número de instancia 03 y el HDB del Id. del sistema de HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="283b9-119">Lea primero las notas y los documentos de SAP siguientes:</span><span class="sxs-lookup"><span data-stu-id="283b9-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="283b9-120">Nota de SAP [1928533], que incluye:</span><span class="sxs-lookup"><span data-stu-id="283b9-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="283b9-121">La lista de tamaños de máquina virtual de Azure que se admiten para la implementación del software de SAP</span><span class="sxs-lookup"><span data-stu-id="283b9-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="283b9-122">Información importante sobre la capacidad para los tamaños de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="283b9-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="283b9-123">Software de SAP admitido y combinaciones de sistema operativo y base de datos</span><span class="sxs-lookup"><span data-stu-id="283b9-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="283b9-124">Versión del kernel de SAP requerida para Windows y Linux en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="283b9-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="283b9-125">La nota de SAP [2015553] enumera los requisitos previos para las implementaciones de software de SAP admitidas por SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="283b9-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="283b9-126">La nota de SAP [2205917] contiene configuraciones recomendadas del sistema operativo para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="283b9-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="283b9-127">La nota de SAP [1944799] contiene guías de SAP HANA para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="283b9-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="283b9-128">La nota de SAP [2178632] contiene información detallada sobre todas las métricas de supervisión notificadas para SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="283b9-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="283b9-129">La nota de SAP [2191498] incluye la versión de SAP Host Agent necesaria para Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="283b9-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="283b9-130">La nota de SAP [2243692] incluye información acerca de las licencias de SAP en Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="283b9-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="283b9-131">La nota de SAP [1984787] incluye información general sobre SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="283b9-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="283b9-132">La nota de SAP [1999351] contiene más soluciones de problemas de la extensión de supervisión mejorada de Azure para SAP.</span><span class="sxs-lookup"><span data-stu-id="283b9-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="283b9-133">La [WIKI de la comunidad SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene todas las notas de SAP que se necesitan para Linux.</span><span class="sxs-lookup"><span data-stu-id="283b9-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="283b9-134">[Planeación e implementación de Azure Virtual Machines para SAP en Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="283b9-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="283b9-135">[Implementación de Azure Virtual Machines para SAP en Linux (este artículo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="283b9-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="283b9-136">[Implementación de DBMS de Azure Virtual Machines para SAP en Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="283b9-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="283b9-137">[Escenario de rendimiento optimizado para la replicación del sistema de SAP HANA][suse-hana-ha-guide] La guía contiene toda la información necesaria para configurar la replicación local del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="283b9-138">Esta guía sirve como orientación.</span><span class="sxs-lookup"><span data-stu-id="283b9-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="283b9-139">Implementación de Linux</span><span class="sxs-lookup"><span data-stu-id="283b9-139">Deploying Linux</span></span>

<span data-ttu-id="283b9-140">El agente de recursos para SAP HANA se incluye en SUSE Linux Enterprise Server para SAP Applications.</span><span class="sxs-lookup"><span data-stu-id="283b9-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="283b9-141">Azure Marketplace contiene una imagen de SUSE Linux Enterprise Server para SAP Applications 12 con BYOS ("traiga su propia suscripción") que puede usar para implementar nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="283b9-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="283b9-142">Implementación manual</span><span class="sxs-lookup"><span data-stu-id="283b9-142">Manual Deployment</span></span>

1. <span data-ttu-id="283b9-143">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="283b9-143">Create a Resource Group</span></span>
1. <span data-ttu-id="283b9-144">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="283b9-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="283b9-145">Creación de dos cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="283b9-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="283b9-146">Creación de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="283b9-146">Create an Availability Set</span></span>  
   <span data-ttu-id="283b9-147">Establecimiento del dominio máximo de actualización</span><span class="sxs-lookup"><span data-stu-id="283b9-147">Set max update domain</span></span>
1. <span data-ttu-id="283b9-148">Creación de un equilibrador de carga (interno)</span><span class="sxs-lookup"><span data-stu-id="283b9-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="283b9-149">Selección de la red virtual del paso anterior</span><span class="sxs-lookup"><span data-stu-id="283b9-149">Select VNET of step above</span></span>
1. <span data-ttu-id="283b9-150">Creación de la máquina virtual 1</span><span class="sxs-lookup"><span data-stu-id="283b9-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="283b9-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="283b9-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="283b9-152">SLES para SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="283b9-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="283b9-153">Selección de la cuenta de almacenamiento 1</span><span class="sxs-lookup"><span data-stu-id="283b9-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="283b9-154">Selección del conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="283b9-154">Select Availability Set</span></span>  
1. <span data-ttu-id="283b9-155">Creación de la máquina virtual 2</span><span class="sxs-lookup"><span data-stu-id="283b9-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="283b9-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="283b9-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="283b9-157">SLES para SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="283b9-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="283b9-158">Selección de la cuenta de almacenamiento 2</span><span class="sxs-lookup"><span data-stu-id="283b9-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="283b9-159">Selección del conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="283b9-159">Select Availability Set</span></span>  
1. <span data-ttu-id="283b9-160">Incorporación de los discos de datos</span><span class="sxs-lookup"><span data-stu-id="283b9-160">Add Data Disks</span></span>
1. <span data-ttu-id="283b9-161">Configuración del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="283b9-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="283b9-162">Creación de un grupo de direcciones IP de front-end</span><span class="sxs-lookup"><span data-stu-id="283b9-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="283b9-163">Abra el equilibrador de carga, seleccione el grupo de direcciones IP de front-end y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="283b9-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="283b9-164">Escriba el nombre del nuevo grupo de direcciones IP de front-end (por ejemplo, hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="283b9-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="283b9-165">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="283b9-165">Click OK</span></span>
        1. <span data-ttu-id="283b9-166">Una vez creado el nuevo grupo de direcciones IP de front-end, anote la dirección IP</span><span class="sxs-lookup"><span data-stu-id="283b9-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="283b9-167">Creación de un grupo de back-end</span><span class="sxs-lookup"><span data-stu-id="283b9-167">Create a backend pool</span></span>
        1. <span data-ttu-id="283b9-168">Abra el equilibrador de carga, seleccione los grupos de back-end y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="283b9-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="283b9-169">Escriba el nombre del nuevo grupo de back-end (por ejemplo, hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="283b9-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="283b9-170">Haga clic en Agregar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="283b9-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="283b9-171">Seleccione el conjunto de disponibilidad que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="283b9-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="283b9-172">Seleccione las máquinas virtuales del clúster de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="283b9-173">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="283b9-173">Click OK</span></span>
    1. <span data-ttu-id="283b9-174">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="283b9-174">Create a health probe</span></span>
       1. <span data-ttu-id="283b9-175">Abra el equilibrador de carga, seleccione los sondeos de estado y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="283b9-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="283b9-176">Escriba el nombre del sondeo de estado nuevo (por ejemplo hana-hp)</span><span class="sxs-lookup"><span data-stu-id="283b9-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="283b9-177">Seleccione TCP como protocolo, puerto 625**03**, y mantenga el intervalo de 5 y el umbral incorrecto 2</span><span class="sxs-lookup"><span data-stu-id="283b9-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="283b9-178">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="283b9-178">Click OK</span></span>
    1. <span data-ttu-id="283b9-179">Creación de reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="283b9-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="283b9-180">Abra el equilibrador de carga, seleccione las reglas de equilibrio de carga y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="283b9-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="283b9-181">Escriba el nombre de la nueva regla del equilibrador de carga (por ejemplo, hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="283b9-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="283b9-182">Seleccione la dirección IP de front-end, el grupo de back-end y el sondeo de estado que creó anteriormente (por ejemplo, hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="283b9-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="283b9-183">Conserve el protocolo TCP y escriba el puerto 3**03**15</span><span class="sxs-lookup"><span data-stu-id="283b9-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="283b9-184">Aumente el tiempo de espera de inactividad a 30 minutos</span><span class="sxs-lookup"><span data-stu-id="283b9-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="283b9-185">**Asegúrese de habilitar la dirección IP flotante**</span><span class="sxs-lookup"><span data-stu-id="283b9-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="283b9-186">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="283b9-186">Click OK</span></span>
        1. <span data-ttu-id="283b9-187">Repita los pasos anteriores para el puerto 3**03**17</span><span class="sxs-lookup"><span data-stu-id="283b9-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="283b9-188">Implementación con plantilla</span><span class="sxs-lookup"><span data-stu-id="283b9-188">Deploy with template</span></span>
<span data-ttu-id="283b9-189">Para implementar todos los recursos necesarios, puede usar una de las plantillas de inicio rápido de github.</span><span class="sxs-lookup"><span data-stu-id="283b9-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="283b9-190">La plantilla implementa las máquinas virtuales, el equilibrador de carga, el conjunto de disponibilidad, etc. Siga estos pasos para implementar la plantilla:</span><span class="sxs-lookup"><span data-stu-id="283b9-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="283b9-191">Abra la [plantilla de base de datos][template-multisid-db] o la [plantilla combinada][template-converged] en Azure Portal. La plantilla de la base de datos solo crea las reglas de equilibrio de carga para una base de datos, mientras que la plantilla combinada también crea las reglas de equilibrio de carga para instancias ASCS/SCS y ERS (solamente para Linux).</span><span class="sxs-lookup"><span data-stu-id="283b9-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="283b9-192">Si tiene previsto instalar un sistema basado en SAP NetWeaver y desea instalar la instancia ASCS/SCS en las mismas máquinas, use la [plantilla combinada][template-converged].</span><span class="sxs-lookup"><span data-stu-id="283b9-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="283b9-193">Escriba los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="283b9-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="283b9-194">Identificador de sistema SAP</span><span class="sxs-lookup"><span data-stu-id="283b9-194">Sap System Id</span></span>  
       <span data-ttu-id="283b9-195">Escriba el identificador del sistema SAP que se va a instalar.</span><span class="sxs-lookup"><span data-stu-id="283b9-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="283b9-196">El identificador se utilizará como prefijo para los recursos que se implementen.</span><span class="sxs-lookup"><span data-stu-id="283b9-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="283b9-197">Tipo de pila (solo si usa la plantilla combinada)</span><span class="sxs-lookup"><span data-stu-id="283b9-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="283b9-198">Seleccione el tipo de la pila de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="283b9-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="283b9-199">Tipo de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="283b9-199">Os Type</span></span>  
       <span data-ttu-id="283b9-200">Seleccione una de las distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="283b9-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="283b9-201">En este ejemplo, seleccione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="283b9-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="283b9-202">Tipo de base de datos</span><span class="sxs-lookup"><span data-stu-id="283b9-202">Db Type</span></span>  
       <span data-ttu-id="283b9-203">Seleccione HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-203">Select HANA</span></span>
    1. <span data-ttu-id="283b9-204">Tamaño del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="283b9-204">Sap System Size</span></span>  
       <span data-ttu-id="283b9-205">La cantidad de SAPS que proporcionará el sistema nuevo.</span><span class="sxs-lookup"><span data-stu-id="283b9-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="283b9-206">Si no está seguro de cuántos SAPS necesitará el sistema, consulte con el integrador de sistemas o el socio tecnológico de SAP.</span><span class="sxs-lookup"><span data-stu-id="283b9-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="283b9-207">Disponibilidad del sistema</span><span class="sxs-lookup"><span data-stu-id="283b9-207">System Availability</span></span>  
       <span data-ttu-id="283b9-208">Seleccione alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="283b9-208">Select HA</span></span>
    1. <span data-ttu-id="283b9-209">Nombre de usuario y contraseña del administrador</span><span class="sxs-lookup"><span data-stu-id="283b9-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="283b9-210">Se crea un usuario nuevo que se puede usar para iniciar sesión en la máquina.</span><span class="sxs-lookup"><span data-stu-id="283b9-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="283b9-211">Subred nueva o existente</span><span class="sxs-lookup"><span data-stu-id="283b9-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="283b9-212">Determina si es necesario crear una red virtual y subred nuevas o si se debe usar una subred existente.</span><span class="sxs-lookup"><span data-stu-id="283b9-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="283b9-213">Si ya tiene una red virtual conectada a la red local, seleccione la existente.</span><span class="sxs-lookup"><span data-stu-id="283b9-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="283b9-214">Identificador de subred</span><span class="sxs-lookup"><span data-stu-id="283b9-214">Subnet Id</span></span>  
    <span data-ttu-id="283b9-215">El identificador de la subred a la que deben conectarse las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="283b9-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="283b9-216">Seleccione la subred de la VPN o la red virtual de Express Route para conectar la máquina virtual a la red local.</span><span class="sxs-lookup"><span data-stu-id="283b9-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="283b9-217">Generalmente, el identificador tiene un aspecto similar al siguiente: /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`>.</span><span class="sxs-lookup"><span data-stu-id="283b9-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="283b9-218">Configuración de la alta disponibilidad de Linux</span><span class="sxs-lookup"><span data-stu-id="283b9-218">Setting up Linux HA</span></span>

<span data-ttu-id="283b9-219">Los elementos siguientes tienen el prefijo [A]: aplicable a todos los nodos, [1]: aplicable solo al nodo 1 o [2]: aplicable solo al nodo 2.</span><span class="sxs-lookup"><span data-stu-id="283b9-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="283b9-220">[A] SLES solo para SAP BYOS: registre SLES para usar los repositorios</span><span class="sxs-lookup"><span data-stu-id="283b9-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="283b9-221">[A] SLES solo para SAP BYOS: agregue el módulo de nube pública</span><span class="sxs-lookup"><span data-stu-id="283b9-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="283b9-222">[A] Actualice SLES</span><span class="sxs-lookup"><span data-stu-id="283b9-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="283b9-223">[1] Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="283b9-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="283b9-224">[2] Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="283b9-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="283b9-225">[1] Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="283b9-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="283b9-226">[A] Instale la extensión de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="283b9-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="283b9-227">[A] Configure el diseño del disco</span><span class="sxs-lookup"><span data-stu-id="283b9-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="283b9-228">LVM</span><span class="sxs-lookup"><span data-stu-id="283b9-228">LVM</span></span>  
    <span data-ttu-id="283b9-229">Por lo general, se recomienda utilizar LVM para volúmenes de almacén de datos y archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="283b9-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="283b9-230">En el ejemplo siguiente se supone que las máquinas virtuales tienen cuatro discos de datos asociados que se deben usar para crear dos volúmenes.</span><span class="sxs-lookup"><span data-stu-id="283b9-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="283b9-231">Cree volúmenes físicos de todos los discos que desee usar.</span><span class="sxs-lookup"><span data-stu-id="283b9-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="283b9-232">Cree un grupo de volúmenes para los archivos de datos, un grupo de volúmenes para los archivos de registro y otro para el directorio compartido de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="283b9-233">Cree los volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="283b9-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="283b9-234">Cree los directorios de montaje y copie el UUID de todos los volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="283b9-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="283b9-235">Cree entradas de fstab para los tres volúmenes lógicos.</span><span class="sxs-lookup"><span data-stu-id="283b9-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="283b9-236">Inserte esta línea en /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="283b9-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="283b9-237">Monte los volúmenes nuevos.</span><span class="sxs-lookup"><span data-stu-id="283b9-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="283b9-238">Discos sin formato</span><span class="sxs-lookup"><span data-stu-id="283b9-238">Plain Disks</span></span>  
       <span data-ttu-id="283b9-239">Para sistemas pequeños o de demostración, puede colocar los archivos de datos y de registro HANA en un disco.</span><span class="sxs-lookup"><span data-stu-id="283b9-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="283b9-240">Con los siguientes comandos se crea una partición en /dev/sdc y con formato xfs.</span><span class="sxs-lookup"><span data-stu-id="283b9-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="283b9-241">Anote el identificador de /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="283b9-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="283b9-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="283b9-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="283b9-243">[A] Configure la resolución del nombre de todos los hosts</span><span class="sxs-lookup"><span data-stu-id="283b9-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="283b9-244">Puede usar un servidor DNS o modificar /etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="283b9-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="283b9-245">En este ejemplo se muestra cómo utilizar el archivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="283b9-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="283b9-246">Reemplace la dirección IP y el nombre de host en los siguientes comandos</span><span class="sxs-lookup"><span data-stu-id="283b9-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="283b9-247">Inserte las siguientes líneas en /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="283b9-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="283b9-248">Cambie la dirección IP y el nombre de host para que coincida con su entorno</span><span class="sxs-lookup"><span data-stu-id="283b9-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="283b9-249">[1] Instale el clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="283b9-250">[2] Agregue un nodo al clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="283b9-251">[A] Haga que la contraseña de hacluster coincida</span><span class="sxs-lookup"><span data-stu-id="283b9-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="283b9-252">[A] Configure corosync para usar otro tipo de transporte y agregue nodelist.</span><span class="sxs-lookup"><span data-stu-id="283b9-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="283b9-253">De lo contrario, el clúster no funcionará.</span><span class="sxs-lookup"><span data-stu-id="283b9-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="283b9-254">Agregue el siguiente contenido en negrita al archivo.</span><span class="sxs-lookup"><span data-stu-id="283b9-254">Add the following bold content to the file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="283b9-255">Después, reinicie el servicio corosync</span><span class="sxs-lookup"><span data-stu-id="283b9-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="283b9-256">[A] Instale los paquetes de alta disponibilidad de HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="283b9-257">Instalación de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-257">Installing SAP HANA</span></span>

<span data-ttu-id="283b9-258">Siga el capítulo 4 de la [Guía del escenario de rendimiento optimizado para la replicación del sistema de SAP HANA][suse-hana-ha-guide] para instalar la replicación del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="283b9-259">[A] Ejecute hdblcm desde el DVD de HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="283b9-260">Elija la instalación -> 1</span><span class="sxs-lookup"><span data-stu-id="283b9-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="283b9-261">Seleccione los componentes adicionales para la instalación -> 1</span><span class="sxs-lookup"><span data-stu-id="283b9-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="283b9-262">Escriba la ruta de acceso de instalación [/hana/shared]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-263">Escriba el nombre del host local [..]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-264">¿Desea agregar hosts adicionales al sistema?</span><span class="sxs-lookup"><span data-stu-id="283b9-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="283b9-265">(s/n) [n]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-266">Escriba el identificador del sistema de SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="283b9-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="283b9-267">Escriba el número de instancia [00]:</span><span class="sxs-lookup"><span data-stu-id="283b9-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="283b9-268">Número de instancia de HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-268">HANA Instance number.</span></span> <span data-ttu-id="283b9-269">Use 03 si usó la plantilla de Azure o siguió el ejemplo anterior</span><span class="sxs-lookup"><span data-stu-id="283b9-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="283b9-270">Seleccione Database Mode (Modo de base de datos) / escriba el índice [1]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-271">Seleccione Uso del sistema / escriba el índice [4]:</span><span class="sxs-lookup"><span data-stu-id="283b9-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="283b9-272">Seleccione el uso del sistema</span><span class="sxs-lookup"><span data-stu-id="283b9-272">Select the system Usage</span></span>
    * <span data-ttu-id="283b9-273">Escriba la ubicación de los volúmenes de datos [/hana/data/HDB]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-274">Escriba la ubicación de los volúmenes de registros [/hana/log/HDB]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-275">¿Restringir la asignación de memoria máxima?</span><span class="sxs-lookup"><span data-stu-id="283b9-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="283b9-276">[n]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-277">Escriba el nombre del host del certificado para el host "..."</span><span class="sxs-lookup"><span data-stu-id="283b9-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="283b9-278">[...]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-279">Escriba la contraseña del usuario del agente de host de SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="283b9-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="283b9-280">Confirme la contraseña del usuario del agente de host de SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="283b9-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="283b9-281">Escriba la contraseña del administrador del sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="283b9-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="283b9-282">Confirme la contraseña del administrador del sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="283b9-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="283b9-283">Escriba el directorio principal del administrador de sistema [/usr/sap/HDB/home]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-284">Escriba el shell de inicio de sesión del administrador de sistema [/bin/sh]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-285">Escriba el identificador de usuario del administrador de sistema [1001]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-286">Escriba el identificador del grupo de usuarios (sapsys) [79]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-287">Escriba la contraseña del usuario (SYSTEM) de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="283b9-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="283b9-288">Confirme la contraseña del usuario (SYSTEM) de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="283b9-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="283b9-289">¿Reiniciar el sistema tras el reinicio de la máquina?</span><span class="sxs-lookup"><span data-stu-id="283b9-289">Restart system after machine reboot?</span></span> <span data-ttu-id="283b9-290">[n]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="283b9-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="283b9-291">¿Desea continuar?</span><span class="sxs-lookup"><span data-stu-id="283b9-291">Do you want to continue?</span></span> <span data-ttu-id="283b9-292">(s/n):</span><span class="sxs-lookup"><span data-stu-id="283b9-292">(y/n):</span></span>  
  <span data-ttu-id="283b9-293">Valide el resumen y escriba s para continuar</span><span class="sxs-lookup"><span data-stu-id="283b9-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="283b9-294">[A] Actualice el agente de host de SAP</span><span class="sxs-lookup"><span data-stu-id="283b9-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="283b9-295">Descargue el archivo más reciente del agente de host de SAP desde [SAP Softwarecenter][sap-swcenter] y ejecute el siguiente comando para actualizar el agente.</span><span class="sxs-lookup"><span data-stu-id="283b9-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="283b9-296">Reemplace la ruta de acceso al archivo para que apunte al archivo que descargó.</span><span class="sxs-lookup"><span data-stu-id="283b9-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="283b9-297">[1] Cree la replicación de HANA (como raíz)</span><span class="sxs-lookup"><span data-stu-id="283b9-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="283b9-298">Ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="283b9-298">Run the following command.</span></span> <span data-ttu-id="283b9-299">Asegúrese de reemplazar las cadenas en negrita (HDB de Id. de sistema de HANA y número de instancia 03) con los valores de la instalación de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="283b9-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="283b9-300">[A] Cree la entrada de almacén de claves (como raíz).</span><span class="sxs-lookup"><span data-stu-id="283b9-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="283b9-301">[1] Realice la copia de seguridad de la base de datos (como raíz).</span><span class="sxs-lookup"><span data-stu-id="283b9-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="283b9-302">[1] Cambie al usuario sapsid (por ejemplo, hdbadm) y cree el sitio principal.</span><span class="sxs-lookup"><span data-stu-id="283b9-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="283b9-303">[2] Cambie al usuario sapsid (por ejemplo, hdbadm) y cree el sitio secundario.</span><span class="sxs-lookup"><span data-stu-id="283b9-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="283b9-304">Configuración de la plataforma del clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-304">Configure Cluster Framework</span></span>

<span data-ttu-id="283b9-305">Cambie la configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="283b9-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="283b9-306">ahora cargaremos el archivo en el clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-306">now we load the file to the cluster</span></span>
<span data-ttu-id="283b9-307">sudo crm configura la actualización de carga de crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="283b9-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="283b9-308">Creación de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="283b9-308">Create STONITH device</span></span>

<span data-ttu-id="283b9-309">El dispositivo STONITH usa una entidad de servicio para la autorización de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="283b9-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="283b9-310">Para crear una entidad de servicio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="283b9-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="283b9-311">Vaya a <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="283b9-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="283b9-312">Abra la hoja Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="283b9-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="283b9-313">Vaya a Propiedades y anote el identificador del directorio.</span><span class="sxs-lookup"><span data-stu-id="283b9-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="283b9-314">Se trata del **id. de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="283b9-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="283b9-315">Haga clic en Registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="283b9-315">Click App registrations</span></span>
1. <span data-ttu-id="283b9-316">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="283b9-316">Click Add</span></span>
1. <span data-ttu-id="283b9-317">Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear</span><span class="sxs-lookup"><span data-stu-id="283b9-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="283b9-318">La dirección URL de inicio de sesión no se usa y puede ser cualquier dirección URL válida</span><span class="sxs-lookup"><span data-stu-id="283b9-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="283b9-319">Seleccione la nueva aplicación y haga clic en las llaves de la pestaña Configuración</span><span class="sxs-lookup"><span data-stu-id="283b9-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="283b9-320">Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar</span><span class="sxs-lookup"><span data-stu-id="283b9-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="283b9-321">Anote el valor.</span><span class="sxs-lookup"><span data-stu-id="283b9-321">Write down the Value.</span></span> <span data-ttu-id="283b9-322">Se utiliza como **contraseña** para la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="283b9-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="283b9-323">Anote el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="283b9-323">Write down the Application Id.</span></span> <span data-ttu-id="283b9-324">Se utiliza como nombre de usuario (**Id. de inicio de sesión** en los pasos siguientes) de la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="283b9-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="283b9-325">La entidad de servicio no tiene permiso para tener acceso a los recursos de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="283b9-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="283b9-326">Debe concedérselos para iniciar y detener (desasignar) todas las máquinas virtuales del clúster.</span><span class="sxs-lookup"><span data-stu-id="283b9-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="283b9-327">Vaya a https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="283b9-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="283b9-328">Abra la hoja Todos los recursos</span><span class="sxs-lookup"><span data-stu-id="283b9-328">Open the All resources blade</span></span>
1. <span data-ttu-id="283b9-329">Seleccione la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="283b9-329">Select the virtual machine</span></span>
1. <span data-ttu-id="283b9-330">Haga clic en Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="283b9-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="283b9-331">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="283b9-331">Click Add</span></span>
1. <span data-ttu-id="283b9-332">Seleccione el rol de propietario</span><span class="sxs-lookup"><span data-stu-id="283b9-332">Select the role Owner</span></span>
1. <span data-ttu-id="283b9-333">Escriba el nombre de la aplicación que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="283b9-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="283b9-334">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="283b9-334">Click OK</span></span>

<span data-ttu-id="283b9-335">Después de editar los permisos para las máquinas virtuales, puede configurar los dispositivos STONITH en el clúster.</span><span class="sxs-lookup"><span data-stu-id="283b9-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="283b9-336">ahora cargaremos el archivo en el clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-336">now we load the file to the cluster</span></span>
<span data-ttu-id="283b9-337">sudo crm configura la actualización de carga de crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="283b9-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="283b9-338">Creación de recursos de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="283b9-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="283b9-339">ahora cargaremos el archivo en el clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-339">now we load the file to the cluster</span></span>
<span data-ttu-id="283b9-340">sudo crm configura la actualización de carga de crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="283b9-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="283b9-341">ahora cargaremos el archivo en el clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-341">now we load the file to the cluster</span></span>
<span data-ttu-id="283b9-342">sudo crm configura la actualización de carga de crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="283b9-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="283b9-343">Prueba de configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="283b9-343">Test cluster setup</span></span>
<span data-ttu-id="283b9-344">En el capítulo siguiente se describe cómo se puede probar la configuración.</span><span class="sxs-lookup"><span data-stu-id="283b9-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="283b9-345">En todas las pruebas se supone que es la raíz y el sistema SAP HANA maestro lo que se ejecuta en la máquina virtual saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="283b9-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="283b9-346">Prueba de vallado</span><span class="sxs-lookup"><span data-stu-id="283b9-346">Fencing Test</span></span>

<span data-ttu-id="283b9-347">Puede probar la configuración del agente de vallado si deshabilita la interfaz de red en el nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="283b9-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="283b9-348">Ahora, la máquina virtual debería reiniciarse o detenerse, en función de la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="283b9-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="283b9-349">Si estableció la acción stonith en off (desactivar), la máquina virtual se detendrá y los recursos se migrarán a la máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="283b9-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="283b9-350">Cuando reinicie la máquina virtual, se producirá un error al iniciarse el recurso de SAP HANA como secundario si estableció AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="283b9-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="283b9-351">En este caso, debe configurar la instancia de HANA como secundaria mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="283b9-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="283b9-352">Prueba de una conmutación por error manual</span><span class="sxs-lookup"><span data-stu-id="283b9-352">Testing a manual failover</span></span>

<span data-ttu-id="283b9-353">Para probar una conmutación por error manual, detenga el servicio de marcapasos en el nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="283b9-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="283b9-354">Después de la conmutación por error, puede reiniciar el servicio.</span><span class="sxs-lookup"><span data-stu-id="283b9-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="283b9-355">Si estableció AUTOMATED_REGISTER = "false", se producirá un error al iniciarse el recurso de SAP HANA en saphanavm1 como secundario.</span><span class="sxs-lookup"><span data-stu-id="283b9-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="283b9-356">En este caso, debe configurar la instancia de HANA como secundaria mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="283b9-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="283b9-357">Prueba de una migración</span><span class="sxs-lookup"><span data-stu-id="283b9-357">Testing a migration</span></span>

<span data-ttu-id="283b9-358">Puede migrar el nodo principal de SAP HANA al ejecutar el siguiente comando</span><span class="sxs-lookup"><span data-stu-id="283b9-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="283b9-359">Esto debe migrar el nodo principal de SAP HANA y el grupo que contiene la dirección IP virtual a saphanavm2.</span><span class="sxs-lookup"><span data-stu-id="283b9-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="283b9-360">Si estableció AUTOMATED_REGISTER = "false", se producirá un error al iniciarse el recurso de SAP HANA en saphanavm1 como secundario.</span><span class="sxs-lookup"><span data-stu-id="283b9-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="283b9-361">En este caso, debe configurar la instancia de HANA como secundaria mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="283b9-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="283b9-362">La migración crea restricciones de ubicación que deben eliminarse de nuevo.</span><span class="sxs-lookup"><span data-stu-id="283b9-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="283b9-363">También debe limpiar el estado del recurso de nodo secundario</span><span class="sxs-lookup"><span data-stu-id="283b9-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="283b9-364">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="283b9-364">Next steps</span></span>
* <span data-ttu-id="283b9-365">[Planeación e implementación de Azure Virtual Machines para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="283b9-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="283b9-366">[Implementación de Azure Virtual Machines para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="283b9-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="283b9-367">[Implementación de DBMS de Azure Virtual Machines para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="283b9-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="283b9-368">Para obtener información sobre cómo establecer la alta disponibilidad y planear la recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [Alta disponibilidad y recuperación ante desastres de SAP HANA en Azure (instancias grandes)](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="283b9-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
