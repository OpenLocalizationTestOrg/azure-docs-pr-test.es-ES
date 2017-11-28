---
title: "Disponibilidad de SAP HANA en máquinas virtuales de Azure (VM) aaaHigh | Documentos de Microsoft"
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
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="a64ed-103">Alta disponibilidad de SAP HANA en las máquinas virtuales (VM) de Azure</span><span class="sxs-lookup"><span data-stu-id="a64ed-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="a64ed-113">De forma local, puede usar cualquier replicación del sistema de archivos de HANA o usar almacenamiento compartido tooestablish alta disponibilidad para SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a64ed-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="a64ed-114">Actualmente solo se admite la configuración de la replicación del sistema de HANA en Azure.</span><span class="sxs-lookup"><span data-stu-id="a64ed-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="a64ed-115">La replicación de SAP HANA se realiza con un nodo maestro y al menos uno subordinado.</span><span class="sxs-lookup"><span data-stu-id="a64ed-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="a64ed-116">Toohello de cambios de datos en el nodo principal de hello son replica nodos de esclavo toohello forma sincrónica o asincrónica.</span><span class="sxs-lookup"><span data-stu-id="a64ed-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="a64ed-117">Este artículo describe cómo toodeploy hello las máquinas virtuales, configurar las máquinas virtuales de hello, instale Hola clúster framework, instalar y la configurar la replicación del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a64ed-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="a64ed-118">En configuraciones de ejemplo de Hola, el número de instancia etc. 03 de comandos de instalación y se utiliza HDB de Id. de sistema de archivos de HANA.</span><span class="sxs-lookup"><span data-stu-id="a64ed-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="a64ed-119">Hola de lectura siguientes notas de SAP y documentos en primer lugar</span><span class="sxs-lookup"><span data-stu-id="a64ed-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="a64ed-120">Nota de SAP [1928533], que incluye:</span><span class="sxs-lookup"><span data-stu-id="a64ed-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="a64ed-121">Lista de tamaños de máquina virtual de Azure que se admiten para la implementación de hello del software SAP.</span><span class="sxs-lookup"><span data-stu-id="a64ed-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="a64ed-122">Información importante sobre la capacidad para los tamaños de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a64ed-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="a64ed-123">Software de SAP admitido y combinaciones de sistema operativo y base de datos</span><span class="sxs-lookup"><span data-stu-id="a64ed-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="a64ed-124">Versión del kernel de SAP requerida para Windows y Linux en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a64ed-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="a64ed-125">La nota de SAP [2015553] enumera los requisitos previos para las implementaciones de software de SAP admitidas por SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="a64ed-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="a64ed-126">La nota de SAP [2205917] contiene configuraciones recomendadas del sistema operativo para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="a64ed-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="a64ed-127">La nota de SAP [1944799] contiene guías de SAP HANA para SUSE Linux Enterprise Server para SAP Applications</span><span class="sxs-lookup"><span data-stu-id="a64ed-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="a64ed-128">La nota de SAP [2178632] contiene información detallada sobre todas las métricas de supervisión notificadas para SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="a64ed-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="a64ed-129">Nota de SAP [2191498] Hola necesario versión del agente de Host de SAP para Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="a64ed-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="a64ed-130">La nota de SAP [2243692] incluye información acerca de las licencias de SAP en Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="a64ed-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="a64ed-131">La nota de SAP [1984787] incluye información general sobre SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="a64ed-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="a64ed-132">Nota de SAP [1999351] información adicional de solución de problemas de hello Azure extensión de supervisión mejorada para SAP.</span><span class="sxs-lookup"><span data-stu-id="a64ed-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="a64ed-133">La [WIKI de la comunidad SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene todas las notas de SAP que se necesitan para Linux.</span><span class="sxs-lookup"><span data-stu-id="a64ed-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="a64ed-134">[Planeación e implementación de Azure Virtual Machines para SAP en Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="a64ed-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="a64ed-135">[Implementación de Azure Virtual Machines para SAP en Linux (este artículo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="a64ed-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="a64ed-136">[Implementación de DBMS de Azure Virtual Machines para SAP en Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="a64ed-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="a64ed-137">[SAP HANA SR rendimiento optimizado escenario] [ suse-hana-ha-guide] guía hello contiene todos los tooset de información necesaria la replicación del sistema de SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="a64ed-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="a64ed-138">Esta guía sirve como orientación.</span><span class="sxs-lookup"><span data-stu-id="a64ed-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="a64ed-139">Implementación de Linux</span><span class="sxs-lookup"><span data-stu-id="a64ed-139">Deploying Linux</span></span>

<span data-ttu-id="a64ed-140">agente de recursos de Hola para SAP HANA se incluye en SUSE Linux Enterprise Server para aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="a64ed-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="a64ed-141">Hello Azure Marketplace contiene una imagen para SUSE Linux Enterprise Server para el 12 de las aplicaciones de SAP con BYOS (poner su propia suscripción) que puede usar máquinas virtuales de la nueva toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a64ed-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="a64ed-142">Implementación manual</span><span class="sxs-lookup"><span data-stu-id="a64ed-142">Manual Deployment</span></span>

1. <span data-ttu-id="a64ed-143">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a64ed-143">Create a Resource Group</span></span>
1. <span data-ttu-id="a64ed-144">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="a64ed-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="a64ed-145">Creación de dos cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a64ed-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="a64ed-146">Creación de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a64ed-146">Create an Availability Set</span></span>  
   <span data-ttu-id="a64ed-147">Establecimiento del dominio máximo de actualización</span><span class="sxs-lookup"><span data-stu-id="a64ed-147">Set max update domain</span></span>
1. <span data-ttu-id="a64ed-148">Creación de un equilibrador de carga (interno)</span><span class="sxs-lookup"><span data-stu-id="a64ed-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="a64ed-149">Selección de la red virtual del paso anterior</span><span class="sxs-lookup"><span data-stu-id="a64ed-149">Select VNET of step above</span></span>
1. <span data-ttu-id="a64ed-150">Creación de la máquina virtual 1</span><span class="sxs-lookup"><span data-stu-id="a64ed-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="a64ed-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="a64ed-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="a64ed-152">SLES para SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="a64ed-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="a64ed-153">Selección de la cuenta de almacenamiento 1</span><span class="sxs-lookup"><span data-stu-id="a64ed-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="a64ed-154">Selección del conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a64ed-154">Select Availability Set</span></span>  
1. <span data-ttu-id="a64ed-155">Creación de la máquina virtual 2</span><span class="sxs-lookup"><span data-stu-id="a64ed-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="a64ed-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="a64ed-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="a64ed-157">SLES para SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="a64ed-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="a64ed-158">Selección de la cuenta de almacenamiento 2</span><span class="sxs-lookup"><span data-stu-id="a64ed-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="a64ed-159">Selección del conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a64ed-159">Select Availability Set</span></span>  
1. <span data-ttu-id="a64ed-160">Incorporación de los discos de datos</span><span class="sxs-lookup"><span data-stu-id="a64ed-160">Add Data Disks</span></span>
1. <span data-ttu-id="a64ed-161">Configure el equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="a64ed-162">Creación de un grupo de direcciones IP de front-end</span><span class="sxs-lookup"><span data-stu-id="a64ed-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="a64ed-163">Abra el equilibrador de carga de hello, seleccione el grupo de direcciones IP de front-end y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="a64ed-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="a64ed-164">Escriba el nombre de Hola Hola nuevo front-end del grupo de IP (por ejemplo hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="a64ed-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="a64ed-165">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="a64ed-165">Click OK</span></span>
        1. <span data-ttu-id="a64ed-166">Después de crea nuevo grupo IP de front-end hello, anote su dirección IP</span><span class="sxs-lookup"><span data-stu-id="a64ed-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="a64ed-167">Creación de un grupo de back-end</span><span class="sxs-lookup"><span data-stu-id="a64ed-167">Create a backend pool</span></span>
        1. <span data-ttu-id="a64ed-168">Abra el equilibrador de carga de hello, seleccione grupos back-end y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="a64ed-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="a64ed-169">Escriba el nombre de Hola de nuevo grupo back-end de hello (por ejemplo hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="a64ed-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="a64ed-170">Haga clic en Agregar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a64ed-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="a64ed-171">Seleccione Hola conjunto de disponibilidad que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="a64ed-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="a64ed-172">Seleccione las máquinas virtuales del clúster de SAP HANA Hola Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="a64ed-173">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="a64ed-173">Click OK</span></span>
    1. <span data-ttu-id="a64ed-174">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="a64ed-174">Create a health probe</span></span>
       1. <span data-ttu-id="a64ed-175">Abra el equilibrador de carga de hello, seleccione sondeos de mantenimiento y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="a64ed-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="a64ed-176">Escriba el nombre de Hola de sondeo de estado nuevo de hello (por ejemplo hana-hp)</span><span class="sxs-lookup"><span data-stu-id="a64ed-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="a64ed-177">Seleccione TCP como protocolo, puerto 625**03**, y mantenga el intervalo de 5 y el umbral incorrecto 2</span><span class="sxs-lookup"><span data-stu-id="a64ed-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="a64ed-178">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="a64ed-178">Click OK</span></span>
    1. <span data-ttu-id="a64ed-179">Creación de reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="a64ed-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="a64ed-180">Abra el equilibrador de carga de hello, seleccione las reglas de equilibrio de carga y haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="a64ed-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="a64ed-181">Escriba Hola nombre de regla de equilibrador de carga nueva hello (por ejemplo hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="a64ed-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="a64ed-182">Dirección IP de Front-End Select hello, grupo back-end y estado de sondeo que ha creado anteriormente (por ejemplo hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="a64ed-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="a64ed-183">Conserve el protocolo TCP y escriba el puerto 3**03**15</span><span class="sxs-lookup"><span data-stu-id="a64ed-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="a64ed-184">Aumentar el tiempo de espera inactivo too30 minutos</span><span class="sxs-lookup"><span data-stu-id="a64ed-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="a64ed-185">**Asegúrese de que tooenable dirección IP flotante**</span><span class="sxs-lookup"><span data-stu-id="a64ed-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="a64ed-186">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="a64ed-186">Click OK</span></span>
        1. <span data-ttu-id="a64ed-187">Repita los pasos de hello anteriormente para el puerto 3**03**17</span><span class="sxs-lookup"><span data-stu-id="a64ed-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="a64ed-188">Implementación con plantilla</span><span class="sxs-lookup"><span data-stu-id="a64ed-188">Deploy with template</span></span>
<span data-ttu-id="a64ed-189">Puede usar una de las plantillas de inicio rápido de hello en github toodeploy todos los recursos necesarios.</span><span class="sxs-lookup"><span data-stu-id="a64ed-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="a64ed-190">plantilla de Hello implementa máquinas virtuales de hello, equilibrador de carga de hello, etcetera conjunto de disponibilidad. Siga estas plantillas de hello toodeploy de pasos:</span><span class="sxs-lookup"><span data-stu-id="a64ed-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="a64ed-191">Abra hello [plantilla de base de datos] [ template-multisid-db] o hello [convergente plantilla] [ template-converged] en hello Azure Portal plantilla de la base de datos de hello sólo crea Hola reglas de equilibrio de carga para una base de datos mientras que también se crea la plantilla convergente Hola Hola reglas de equilibrio de carga para un ASCS/SCS y la instancia ERS (solamente para Linux).</span><span class="sxs-lookup"><span data-stu-id="a64ed-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="a64ed-192">Si tiene pensado tooinstall un sistema basadas en SAP NetWeaver y también desea tooinstall Hola ASCS/SCS a la instancia en hello mismo máquinas, use hello [convergente plantilla][template-converged].</span><span class="sxs-lookup"><span data-stu-id="a64ed-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="a64ed-193">Escriba Hola parámetros siguientes</span><span class="sxs-lookup"><span data-stu-id="a64ed-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="a64ed-194">Identificador de sistema SAP</span><span class="sxs-lookup"><span data-stu-id="a64ed-194">Sap System Id</span></span>  
       <span data-ttu-id="a64ed-195">Especifique el sistema SAP de hello Id. de hello sistema SAP que desee tooinstall.</span><span class="sxs-lookup"><span data-stu-id="a64ed-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="a64ed-196">Hola Id. se usará como prefijo para los recursos de Hola que se implementan.</span><span class="sxs-lookup"><span data-stu-id="a64ed-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="a64ed-197">Tipo de pila (solo se aplica si usa Hola convergente plantilla)</span><span class="sxs-lookup"><span data-stu-id="a64ed-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="a64ed-198">Seleccione el tipo de pila de SAP NetWeaver Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="a64ed-199">Tipo de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="a64ed-199">Os Type</span></span>  
       <span data-ttu-id="a64ed-200">Seleccione una de las distribuciones de Linux de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="a64ed-201">En este ejemplo, seleccione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="a64ed-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="a64ed-202">Tipo de base de datos</span><span class="sxs-lookup"><span data-stu-id="a64ed-202">Db Type</span></span>  
       <span data-ttu-id="a64ed-203">Seleccione HANA</span><span class="sxs-lookup"><span data-stu-id="a64ed-203">Select HANA</span></span>
    1. <span data-ttu-id="a64ed-204">Tamaño del sistema SAP</span><span class="sxs-lookup"><span data-stu-id="a64ed-204">Sap System Size</span></span>  
       <span data-ttu-id="a64ed-205">cantidad de Hola de nuevo sistema de SAPS Hola proporcionará.</span><span class="sxs-lookup"><span data-stu-id="a64ed-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="a64ed-206">Si no estás seguro de sistema de Hola de SAPS cuántos requerirá, póngase en contacto con su socio de tecnología de SAP o integrador de sistema</span><span class="sxs-lookup"><span data-stu-id="a64ed-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="a64ed-207">Disponibilidad del sistema</span><span class="sxs-lookup"><span data-stu-id="a64ed-207">System Availability</span></span>  
       <span data-ttu-id="a64ed-208">Seleccione alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a64ed-208">Select HA</span></span>
    1. <span data-ttu-id="a64ed-209">Nombre de usuario y contraseña del administrador</span><span class="sxs-lookup"><span data-stu-id="a64ed-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="a64ed-210">Se crea un nuevo usuario que pueden ser toolog usado en la máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="a64ed-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="a64ed-211">Subred nueva o existente</span><span class="sxs-lookup"><span data-stu-id="a64ed-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="a64ed-212">Determina si es necesario crear una red virtual y subred nuevas o si se debe usar una subred existente.</span><span class="sxs-lookup"><span data-stu-id="a64ed-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="a64ed-213">Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione existente.</span><span class="sxs-lookup"><span data-stu-id="a64ed-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="a64ed-214">Identificador de subred</span><span class="sxs-lookup"><span data-stu-id="a64ed-214">Subnet Id</span></span>  
    <span data-ttu-id="a64ed-215">Id. de Hola de máquinas virtuales de hello subred toowhich Hola debe estar conectado a.</span><span class="sxs-lookup"><span data-stu-id="a64ed-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="a64ed-216">Seleccione la subred de hello de la VPN o Express Route red virtual tooconnect Hola máquina virtual tooyour en red local.</span><span class="sxs-lookup"><span data-stu-id="a64ed-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="a64ed-217">Id. de Hello suele ser algo parecido/subscriptions /`<subscription id`>/ResourceGroups /`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="a64ed-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="a64ed-218">Configuración de la alta disponibilidad de Linux</span><span class="sxs-lookup"><span data-stu-id="a64ed-218">Setting up Linux HA</span></span>

<span data-ttu-id="a64ed-219">Hola siguientes elementos tienen el prefijo cualquiera [A] - nodos tooall aplicables, toonode solo se aplica de - solo se aplica toonode 1 o [2]: [1] 2.</span><span class="sxs-lookup"><span data-stu-id="a64ed-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="a64ed-220">[A] SLES para SAP BYOS solo - repositorios de hello toouse capaz de registrar SLES toobe</span><span class="sxs-lookup"><span data-stu-id="a64ed-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="a64ed-221">[A] SLES solo para SAP BYOS: agregue el módulo de nube pública</span><span class="sxs-lookup"><span data-stu-id="a64ed-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="a64ed-222">[A] Actualice SLES</span><span class="sxs-lookup"><span data-stu-id="a64ed-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="a64ed-223">[1] Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="a64ed-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="a64ed-224">[2] Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="a64ed-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="a64ed-225">[1] Habilite el acceso de SSH</span><span class="sxs-lookup"><span data-stu-id="a64ed-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="a64ed-226">[A] Instale la extensión de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a64ed-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="a64ed-227">[A] Configure el diseño del disco</span><span class="sxs-lookup"><span data-stu-id="a64ed-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="a64ed-228">LVM</span><span class="sxs-lookup"><span data-stu-id="a64ed-228">LVM</span></span>  
    <span data-ttu-id="a64ed-229">Por lo general, se recomienda toouse LVM para volúmenes que almacenan los datos y archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="a64ed-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="a64ed-230">ejemplo de Hola siguiente supone que máquinas virtuales de hello tiene cuatro discos de datos conectados que se deben toocreate usa dos volúmenes.</span><span class="sxs-lookup"><span data-stu-id="a64ed-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="a64ed-231">Crear volúmenes físicos de todos los discos que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="a64ed-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="a64ed-232">Crear un grupo de volúmenes para los archivos de datos de hello, un grupo de volúmenes para los archivos de registro de hello y otro para el directorio compartido de Hola de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a64ed-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="a64ed-233">Crear volúmenes lógicos de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="a64ed-234">Crear los directorios de montaje de Hola y copiar Hola UUID de todos los volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="a64ed-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="a64ed-235">Crear las entradas de fstab de hello tres volúmenes lógicos</span><span class="sxs-lookup"><span data-stu-id="a64ed-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="a64ed-236">Inserte esta línea demasiado/etcetera/fstab</span><span class="sxs-lookup"><span data-stu-id="a64ed-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="a64ed-237">Montar volúmenes nuevos Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="a64ed-238">Discos sin formato</span><span class="sxs-lookup"><span data-stu-id="a64ed-238">Plain Disks</span></span>  
       <span data-ttu-id="a64ed-239">Para sistemas pequeños o de demostración, puede colocar los archivos de datos y de registro HANA en un disco.</span><span class="sxs-lookup"><span data-stu-id="a64ed-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="a64ed-240">Hello siguientes comandos crean una partición en /dev/sdc y dele formato con xfs.</span><span class="sxs-lookup"><span data-stu-id="a64ed-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="a64ed-241">Anote el Id. de Hola de /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="a64ed-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="a64ed-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="a64ed-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="a64ed-243">[A] Configure la resolución del nombre de todos los hosts</span><span class="sxs-lookup"><span data-stu-id="a64ed-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="a64ed-244">Puede usar un servidor DNS o modificar Hola/etc/hosts en todos los nodos.</span><span class="sxs-lookup"><span data-stu-id="a64ed-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="a64ed-245">Este ejemplo muestra cómo toouse Hola archivo/etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="a64ed-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="a64ed-246">Reemplace la dirección IP de Hola y el nombre de host de Hola Hola siga los comandos</span><span class="sxs-lookup"><span data-stu-id="a64ed-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="a64ed-247">Insertar Hola después líneas demasiado/etcetera/hosts.</span><span class="sxs-lookup"><span data-stu-id="a64ed-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="a64ed-248">Cambiar toomatch de dirección y el nombre de host IP hello en el entorno</span><span class="sxs-lookup"><span data-stu-id="a64ed-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="a64ed-249">[1] Instale el clúster</span><span class="sxs-lookup"><span data-stu-id="a64ed-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="a64ed-250">[2] agregar nodo toocluster</span><span class="sxs-lookup"><span data-stu-id="a64ed-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="a64ed-251">[A] cambio hacluster contraseña toohello misma contraseña</span><span class="sxs-lookup"><span data-stu-id="a64ed-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="a64ed-252">[A] configurar corosync toouse otros tipos de transporte y agregar la lista de nodos.</span><span class="sxs-lookup"><span data-stu-id="a64ed-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="a64ed-253">De lo contrario, el clúster no funcionará.</span><span class="sxs-lookup"><span data-stu-id="a64ed-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="a64ed-254">Agregar hello toohello contenido negrita el archivo siguiente.</span><span class="sxs-lookup"><span data-stu-id="a64ed-254">Add hello following bold content toohello file.</span></span>
    
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

    <span data-ttu-id="a64ed-255">A continuación, reinicie el servicio de hello corosync</span><span class="sxs-lookup"><span data-stu-id="a64ed-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="a64ed-256">[A] Instale los paquetes de alta disponibilidad de HANA</span><span class="sxs-lookup"><span data-stu-id="a64ed-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="a64ed-257">Instalación de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a64ed-257">Installing SAP HANA</span></span>

<span data-ttu-id="a64ed-258">Siga el capítulo 4 de hello [Guía de SAP HANA SR rendimiento optimizado escenario] [ suse-hana-ha-guide] tooinstall replicación del sistema de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a64ed-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="a64ed-259">[A] ejecutar hdblcm desde Hola HANA DVD</span><span class="sxs-lookup"><span data-stu-id="a64ed-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="a64ed-260">Elija la instalación -> 1</span><span class="sxs-lookup"><span data-stu-id="a64ed-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="a64ed-261">Seleccione los componentes adicionales para la instalación -> 1</span><span class="sxs-lookup"><span data-stu-id="a64ed-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="a64ed-262">Escriba la ruta de acceso de instalación [/hana/shared]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-263">Escriba el nombre del host local [..]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-264">¿Desea que el sistema de toohello de tooadd hosts adicionales?</span><span class="sxs-lookup"><span data-stu-id="a64ed-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="a64ed-265">(s/n) [n]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-266">Escriba el identificador del sistema de SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="a64ed-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="a64ed-267">Escriba el número de instancia [00]:</span><span class="sxs-lookup"><span data-stu-id="a64ed-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="a64ed-268">Número de instancia de HANA.</span><span class="sxs-lookup"><span data-stu-id="a64ed-268">HANA Instance number.</span></span> <span data-ttu-id="a64ed-269">Usar 03 si usa Hola plantilla de Azure o seguir el ejemplo de Hola anterior</span><span class="sxs-lookup"><span data-stu-id="a64ed-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="a64ed-270">Seleccione Database Mode (Modo de base de datos) / escriba el índice [1]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-271">Seleccione Uso del sistema / escriba el índice [4]:</span><span class="sxs-lookup"><span data-stu-id="a64ed-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="a64ed-272">Seleccione sistema Hola uso</span><span class="sxs-lookup"><span data-stu-id="a64ed-272">Select hello system Usage</span></span>
    * <span data-ttu-id="a64ed-273">Escriba la ubicación de los volúmenes de datos [/hana/data/HDB]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-274">Escriba la ubicación de los volúmenes de registros [/hana/log/HDB]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-275">¿Restringir la asignación de memoria máxima?</span><span class="sxs-lookup"><span data-stu-id="a64ed-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="a64ed-276">[n]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-277">Escriba el nombre de Host de certificado de Host '...' [...]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-278">Escriba la contraseña del usuario del agente de host de SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="a64ed-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="a64ed-279">Confirme la contraseña del usuario del agente de host de SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="a64ed-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="a64ed-280">Escriba la contraseña del administrador del sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="a64ed-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="a64ed-281">Confirme la contraseña del administrador del sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="a64ed-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="a64ed-282">Escriba el directorio principal del administrador de sistema [/usr/sap/HDB/home]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-283">Escriba el shell de inicio de sesión del administrador de sistema [/bin/sh]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-284">Escriba el identificador de usuario del administrador de sistema [1001]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-285">Escriba el identificador del grupo de usuarios (sapsys) [79]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-286">Escriba la contraseña del usuario (SYSTEM) de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="a64ed-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="a64ed-287">Confirme la contraseña del usuario (SYSTEM) de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="a64ed-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="a64ed-288">¿Reiniciar el sistema tras el reinicio de la máquina?</span><span class="sxs-lookup"><span data-stu-id="a64ed-288">Restart system after machine reboot?</span></span> <span data-ttu-id="a64ed-289">[n]: -> ENTRAR</span><span class="sxs-lookup"><span data-stu-id="a64ed-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="a64ed-290">¿Desea toocontinue?</span><span class="sxs-lookup"><span data-stu-id="a64ed-290">Do you want toocontinue?</span></span> <span data-ttu-id="a64ed-291">(s/n):</span><span class="sxs-lookup"><span data-stu-id="a64ed-291">(y/n):</span></span>  
  <span data-ttu-id="a64ed-292">Validar Hola resumen y escriba y toocontinue</span><span class="sxs-lookup"><span data-stu-id="a64ed-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="a64ed-293">[A] Actualice el agente de host de SAP</span><span class="sxs-lookup"><span data-stu-id="a64ed-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="a64ed-294">Descargue el archivo de agente de Host de SAP más reciente de Hola de hello [SAP Softwarecenter] [ sap-swcenter] y ejecución hello siguientes comando tooupgrade Hola agente.</span><span class="sxs-lookup"><span data-stu-id="a64ed-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="a64ed-295">Reemplace Hola ruta de acceso toohello toopoint toohello archivo que descargó.</span><span class="sxs-lookup"><span data-stu-id="a64ed-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="a64ed-296">[1] Cree la replicación de HANA (como raíz)</span><span class="sxs-lookup"><span data-stu-id="a64ed-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="a64ed-297">Ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-297">Run hello following command.</span></span> <span data-ttu-id="a64ed-298">Asegúrese de que tooreplace negrita cadenas (HDB de Id. de sistema de archivos de HANA y número de instancia 03) con valores de hello de la instalación de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="a64ed-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="a64ed-299">[A] Cree la entrada de almacén de claves (como raíz).</span><span class="sxs-lookup"><span data-stu-id="a64ed-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="a64ed-300">[1] Realice la copia de seguridad de la base de datos (como raíz).</span><span class="sxs-lookup"><span data-stu-id="a64ed-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="a64ed-301">[1] Cambie toohello sapsid usuario (por ejemplo hdbadm) y crear el sitio primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="a64ed-302">[2] Cambie toohello sapsid usuario (por ejemplo hdbadm) y crear sitio secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="a64ed-303">Configuración de la plataforma del clúster</span><span class="sxs-lookup"><span data-stu-id="a64ed-303">Configure Cluster Framework</span></span>

<span data-ttu-id="a64ed-304">Cambiar la configuración predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="a64ed-305">Ahora se Hola archivo toohello clúster de carga</span><span class="sxs-lookup"><span data-stu-id="a64ed-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="a64ed-306">sudo crm configura la actualización de carga de crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="a64ed-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="a64ed-307">Creación de un dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="a64ed-307">Create STONITH device</span></span>

<span data-ttu-id="a64ed-308">dispositivo de Hello STONITH utiliza un tooauthorize de entidad de servicio en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a64ed-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="a64ed-309">Siga estos toocreate pasos una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="a64ed-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="a64ed-310">Vaya demasiado<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="a64ed-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="a64ed-311">Hoja de Azure Active Directory Hola abierto</span><span class="sxs-lookup"><span data-stu-id="a64ed-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="a64ed-312">Vaya tooProperties y anote Hola Id. de directorio. Se trata de hello **Id. de inquilino**.</span><span class="sxs-lookup"><span data-stu-id="a64ed-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="a64ed-313">Haga clic en Registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a64ed-313">Click App registrations</span></span>
1. <span data-ttu-id="a64ed-314">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="a64ed-314">Click Add</span></span>
1. <span data-ttu-id="a64ed-315">Escriba un nombre, seleccione el tipo de aplicación "Aplicación web o API", escriba una dirección URL de inicio de sesión (por ejemplo, http://localhost) y haga clic en Crear</span><span class="sxs-lookup"><span data-stu-id="a64ed-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="a64ed-316">dirección URL de inicio de sesión de Hello no se usa y puede ser cualquier dirección URL válida</span><span class="sxs-lookup"><span data-stu-id="a64ed-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="a64ed-317">Seleccione Hola nueva aplicación y haga clic en las claves en la ficha de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="a64ed-318">Escriba una descripción para la nueva clave, seleccione "Nunca expira" y haga clic en Guardar</span><span class="sxs-lookup"><span data-stu-id="a64ed-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="a64ed-319">Anote el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-319">Write down hello Value.</span></span> <span data-ttu-id="a64ed-320">Se utiliza como hello **contraseña** para hello entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="a64ed-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="a64ed-321">Anote Hola identificador de aplicación. Se utiliza como nombre de usuario de Hola (**Id. de inicio de sesión** en estos pasos hello) de hello entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="a64ed-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="a64ed-322">Hola entidad de servicio no tiene permisos tooaccess los recursos de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a64ed-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="a64ed-323">Necesita toostart de permisos de entidad de servicio de toogive hello y detener (desasignar) todas las máquinas virtuales del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="a64ed-324">Vaya toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a64ed-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="a64ed-325">Abrir Hola a todos los módulos de recursos</span><span class="sxs-lookup"><span data-stu-id="a64ed-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="a64ed-326">Seleccione la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="a64ed-327">Haga clic en Control de acceso (IAM)</span><span class="sxs-lookup"><span data-stu-id="a64ed-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="a64ed-328">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="a64ed-328">Click Add</span></span>
1. <span data-ttu-id="a64ed-329">Seleccione el rol de hello propietario</span><span class="sxs-lookup"><span data-stu-id="a64ed-329">Select hello role Owner</span></span>
1. <span data-ttu-id="a64ed-330">Escriba Hola nombre de aplicación Hola que creó anteriormente</span><span class="sxs-lookup"><span data-stu-id="a64ed-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="a64ed-331">Haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="a64ed-331">Click OK</span></span>

<span data-ttu-id="a64ed-332">Después de editar permisos de Hola para las máquinas virtuales de hello, puede configurar dispositivos STONITH hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="a64ed-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="a64ed-333">Ahora se Hola archivo toohello clúster de carga</span><span class="sxs-lookup"><span data-stu-id="a64ed-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="a64ed-334">sudo crm configura la actualización de carga de crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="a64ed-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="a64ed-335">Creación de recursos de SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a64ed-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="a64ed-336">Ahora se Hola archivo toohello clúster de carga</span><span class="sxs-lookup"><span data-stu-id="a64ed-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="a64ed-337">sudo crm configura la actualización de carga de crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="a64ed-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="a64ed-338">Ahora se Hola archivo toohello clúster de carga</span><span class="sxs-lookup"><span data-stu-id="a64ed-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="a64ed-339">sudo crm configura la actualización de carga de crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="a64ed-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="a64ed-340">Prueba de configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="a64ed-340">Test cluster setup</span></span>
<span data-ttu-id="a64ed-341">Hola siguiente capítulo describe cómo puede probar el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="a64ed-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="a64ed-342">Todas las pruebas se supone que son raíz y maestro de SAP HANA Hola se está quedando hello saphanavm1 de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a64ed-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="a64ed-343">Prueba de vallado</span><span class="sxs-lookup"><span data-stu-id="a64ed-343">Fencing Test</span></span>

<span data-ttu-id="a64ed-344">Puede probar el programa de instalación de hello del agente de barrera de hello deshabilitando la interfaz de red de hello en el nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="a64ed-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="a64ed-345">máquina virtual de Hello ahora debe obtener reinicia o detenido según la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="a64ed-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="a64ed-346">Si establece hello stonith acción toooff, se detendrá la máquina virtual de Hola y recursos de hello están migrado toohello máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="a64ed-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="a64ed-347">Una vez que volver a iniciar máquina virtual de hello, Hola recursos de SAP HANA se producirá un error toostart como base de datos secundaria si establece AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="a64ed-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="a64ed-348">En este caso, necesita tooconfigure Hola HANA instancia secundarias mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a64ed-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="a64ed-349">Prueba de una conmutación por error manual</span><span class="sxs-lookup"><span data-stu-id="a64ed-349">Testing a manual failover</span></span>

<span data-ttu-id="a64ed-350">Puede probar una conmutación por error manual Deteniendo el servicio de marcapasos de hello en el nodo saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="a64ed-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="a64ed-351">Después de la conmutación por error de hello, puede iniciar servicio Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a64ed-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="a64ed-352">Hola recursos de SAP HANA en saphanavm1 se producirá un error toostart como base de datos secundaria si establece AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="a64ed-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="a64ed-353">En este caso, necesita tooconfigure Hola HANA instancia secundarias mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a64ed-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="a64ed-354">Prueba de una migración</span><span class="sxs-lookup"><span data-stu-id="a64ed-354">Testing a migration</span></span>

<span data-ttu-id="a64ed-355">Puede migrar el nodo principal de SAP HANA Hola ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="a64ed-356">Esto debe migrar nodo maestro de SAP HANA hello y grupo de Hola que contenga hello toosaphanavm2 de dirección IP virtual.</span><span class="sxs-lookup"><span data-stu-id="a64ed-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="a64ed-357">Hola recursos de SAP HANA en saphanavm1 se producirá un error toostart como base de datos secundaria si establece AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="a64ed-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="a64ed-358">En este caso, necesita tooconfigure Hola HANA instancia secundarias mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a64ed-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="a64ed-359">migración de Hello crea restricciones de ubicación que necesitan toobe eliminarlos de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a64ed-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="a64ed-360">También necesita toocleanup estado de Hola de recursos del nodo secundario de Hola</span><span class="sxs-lookup"><span data-stu-id="a64ed-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="a64ed-361">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a64ed-361">Next steps</span></span>
* <span data-ttu-id="a64ed-362">[Planeación e implementación de Azure Virtual Machines para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="a64ed-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="a64ed-363">[Implementación de Azure Virtual Machines para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="a64ed-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="a64ed-364">[Implementación de DBMS de Azure Virtual Machines para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="a64ed-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="a64ed-365">toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="a64ed-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
