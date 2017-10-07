---
title: "una implementación de aplicación de SAP NetWeaver de varios nivel con Azure Site Recovery aaaProtect | Documentos de Microsoft"
description: "Este artículo describe cómo tooprotect SAP NetWeaver las implementaciones de aplicaciones con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a><span data-ttu-id="4f000-103">Protección de la implementación de una aplicación SAP NetWeaver de niveles múltiples mediante Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="4f000-103">Protect a multi-tier SAP NetWeaver application deployment using Azure Site Recovery</span></span>

<span data-ttu-id="4f000-104">La mayor parte de las implementaciones SAP grandes y medianas incluyen algún tipo de solución de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="4f000-104">Most large and medium-sized SAP deployments have some form of Disaster Recovery solution.</span></span>  <span data-ttu-id="4f000-105">importancia de Hola de sólido y probar soluciones de recuperación ante desastres ha aumentado a medida que más negocio principal son procesos pase tooapplications como SAP.</span><span class="sxs-lookup"><span data-stu-id="4f000-105">hello importance of robust and testable Disaster Recovery solutions has increased as more core business processes are moved tooapplications such as SAP.</span></span>  <span data-ttu-id="4f000-106">Azure Site Recovery ha sido probadas y se integra con aplicaciones de SAP y excede las capacidades de Hola de mayoría soluciones de recuperación ante desastres local, en un menor costo total de propiedad (TCO) de soluciones de la competencia.</span><span class="sxs-lookup"><span data-stu-id="4f000-106">Azure Site Recovery has been tested and integrated with SAP applications, and exceeds hello capabilities of most on-premises Disaster Recovery solutions, at a lower total cost of ownership (TCO) than competing solutions.</span></span>
<span data-ttu-id="4f000-107">Con Azure Site Recovery, puede:</span><span class="sxs-lookup"><span data-stu-id="4f000-107">With Azure Site Recovery you can:</span></span>
* <span data-ttu-id="4f000-108">Habilitar la protección de aplicaciones de SAP NetWeaver y no es de producción NetWeaver que se ejecutan de forma local, replicando tooAzure de componentes.</span><span class="sxs-lookup"><span data-stu-id="4f000-108">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running on-premises, by replicating components tooAzure.</span></span>
* <span data-ttu-id="4f000-109">Habilitar la protección de aplicaciones de SAP NetWeaver y no es de producción NetWeaver ejecuta Azure, mediante la replicación de componentes tooanother centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f000-109">Enable protection of SAP NetWeaver and non-NetWeaver Production applications running Azure, by replicating components tooanother Azure datacenter.</span></span>
* <span data-ttu-id="4f000-110">Simplificar la migración a la nube, mediante el uso de Site Recovery toomigrate su tooAzure de implementación de SAP.</span><span class="sxs-lookup"><span data-stu-id="4f000-110">Simplify cloud migration, by using Site Recovery toomigrate your SAP deployment tooAzure.</span></span>
* <span data-ttu-id="4f000-111">Simplificar las actualizaciones de los proyectos SAP, las pruebas y la creación de prototipos, mediante la creación de una clon en producción a petición para probar las aplicaciones SAP.</span><span class="sxs-lookup"><span data-stu-id="4f000-111">Simplify SAP project upgrades, testing, and prototyping, by creating a production clone on-demand for testing SAP applications.</span></span>

<span data-ttu-id="4f000-112">Este artículo describe cómo tooprotect SAP NetWeaver las implementaciones de aplicaciones mediante [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f000-112">This article describes how tooprotect SAP NetWeaver application deployments using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="4f000-113">Este artículo tratan los procedimientos recomendados de Hola para proteger una implementación de SAP NetWeaver de tres niveles en Azure mediante la replicación tooanother centro de datos de Azure con Azure Site Recovery, Hola admitida escenarios y configuraciones, y cómo tooperform las conmutaciones por error, las pruebas las conmutaciones por error (recuperación ante desastres) y las conmutaciones por error real.</span><span class="sxs-lookup"><span data-stu-id="4f000-113">This article covers hello best practices for protecting a three-tier SAP NetWeaver deployment on Azure by replicating tooanother Azure datacenter using Azure Site Recovery, hello supported scenarios and configurations, and how tooperform failovers, both test failovers (disaster recovery drills) and actual failovers.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4f000-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f000-114">Prerequisites</span></span>
<span data-ttu-id="4f000-115">Antes de empezar, asegúrese de que comprende siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="4f000-115">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="4f000-116">Replicar una máquina virtual tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f000-116">Replicating a virtual machine tooAzure</span></span>](azure-to-azure-walkthrough-enable-replication.md)
2. <span data-ttu-id="4f000-117">Cómo demasiado[el diseño de una red de recuperación](site-recovery-azure-to-azure-networking-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="4f000-117">How too[design a recovery network](site-recovery-azure-to-azure-networking-guidance.md)</span></span>
3. [<span data-ttu-id="4f000-118">Realizar una tooAzure de conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="4f000-118">Doing a test failover tooAzure</span></span>](azure-to-azure-walkthrough-test-failover.md)
4. [<span data-ttu-id="4f000-119">Realizar una conmutación por error tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f000-119">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="4f000-120">Cómo demasiado[replicar un controlador de dominio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="4f000-120">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="4f000-121">Cómo demasiado[replicar SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="4f000-121">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4f000-122">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="4f000-122">Supported scenarios</span></span>
<span data-ttu-id="4f000-123">Con Azure Site Recovery se puede implementar una solución de recuperación ante desastres para hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f000-123">With Azure Site Recovery you can implement a disaster recovery solution for hello following scenarios:</span></span>
* <span data-ttu-id="4f000-124">Sistemas SAP que se ejecutan en un centro de datos Azure replicar tooanother centro de datos de Azure (Azure a Azure DR), como la arquitectura [aquí](https://aka.ms/asr-a2a-architecture).</span><span class="sxs-lookup"><span data-stu-id="4f000-124">SAP systems running in one Azure datacenter replicating tooanother Azure datacenter (Azure-to-Azure DR), as architected [here](https://aka.ms/asr-a2a-architecture).</span></span>
* <span data-ttu-id="4f000-125">Sistemas SAP que se ejecutan en servidores de VMWare (o físico) replicación sitio tooa recuperación ante desastres en un centro de datos Azure (VMware a Azure DR), lo que requiere algunos componentes adicionales como la arquitectura local [aquí](https://aka.ms/asr-v2a-architecture).</span><span class="sxs-lookup"><span data-stu-id="4f000-125">SAP systems running on VMWare (or Physical) servers on-premises replicating tooa DR site in an Azure datacenter (VMware-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-v2a-architecture).</span></span>
* <span data-ttu-id="4f000-126">Sistemas SAP que se ejecutan en Hyper-V continúa con la replicación sitio tooa recuperación ante desastres en un centro de datos Azure (Hyper-V a Azure DR), lo que requiere algunos componentes adicionales como la arquitectura local [aquí](https://aka.ms/asr-h2a-architecture).</span><span class="sxs-lookup"><span data-stu-id="4f000-126">SAP systems running on Hyper-V on-premises replicating tooa DR site in an Azure datacenter (Hyper-V-to-Azure DR), which requires some additional components as architected [here](https://aka.ms/asr-h2a-architecture).</span></span>

<span data-ttu-id="4f000-127">Este documento usa las capacidades de recuperación ante desastres de hello primera mayúsculas - Azure a Azure DR - toodemonstrate Azure Site Recovery SAP.</span><span class="sxs-lookup"><span data-stu-id="4f000-127">This document uses hello first case - Azure-to-Azure DR - toodemonstrate Azure Site Recovery's SAP disaster recovery capabilities.</span></span> <span data-ttu-id="4f000-128">Replicación de Azure Site Recovery sea independiente de la aplicación, se describe el proceso de hello es toohold esperado para otros escenarios, así.</span><span class="sxs-lookup"><span data-stu-id="4f000-128">As Azure Site Recovery replication is application agnostic, hello process described is expected toohold for other scenarios as well.</span></span>

### <a name="required-foundation-services"></a><span data-ttu-id="4f000-129">Servicios básicos requeridos</span><span class="sxs-lookup"><span data-stu-id="4f000-129">Required foundation services</span></span>
<span data-ttu-id="4f000-130">Este escenario de documentación todos está implementado con hello después servicios foundation implementados:</span><span class="sxs-lookup"><span data-stu-id="4f000-130">This documentation scenario all been deployed with hello following foundation services deployed:</span></span>
* <span data-ttu-id="4f000-131">Red de privada virtual (VPN) ExpressRoute o de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="4f000-131">ExpressRoute or Site-to-Site Virtual Private Network (VPN)</span></span>
* <span data-ttu-id="4f000-132">Al menos un servidor DNS y un controlador de dominio de Active Directory se ejecutan en Azure</span><span class="sxs-lookup"><span data-stu-id="4f000-132">At least one Active Directory Domain Controller and DNS server running in Azure</span></span>

<span data-ttu-id="4f000-133">Se recomienda que la infraestructura de hello anterior toodeploying anterior establecido Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4f000-133">It is recommended that hello infrastructure above is established prior toodeploying Azure Site Recovery.</span></span>


## <a name="typical-sap-application-deployment"></a><span data-ttu-id="4f000-134">Implementación típica de la aplicación SAP</span><span class="sxs-lookup"><span data-stu-id="4f000-134">Typical SAP application deployment</span></span>
<span data-ttu-id="4f000-135">Los clientes de SAP grandes normalmente implementan entre 6 too20 las aplicaciones SAP individuales.</span><span class="sxs-lookup"><span data-stu-id="4f000-135">Large SAP customers usually deploy between 6 too20 individual SAP applications.</span></span>  <span data-ttu-id="4f000-136">La mayoría de estas aplicaciones se basa en los motores de hello ABAP de SAP NetWeaver o Java.</span><span class="sxs-lookup"><span data-stu-id="4f000-136">Most of these applications are based on hello SAP NetWeaver ABAP or Java engines.</span></span>  <span data-ttu-id="4f000-137">Sirviendo de soporte para estas aplicaciones NetWeaver básicas se encuentran muchos motores menores e independientes SAP específicos que no son NetWeaver y, por lo general, algunas aplicaciones que no son SAP.</span><span class="sxs-lookup"><span data-stu-id="4f000-137">Supporting these core NetWeaver applications are many smaller specific non-NetWeaver SAP standalone engines and typically some non-SAP applications.</span></span>  

<span data-ttu-id="4f000-138">Es crítico tooinventory que se ejecuta en un modo de implementación de hello horizontal y toodetermine (nivel 2 o 3 niveles), versiones, revisiones de todas las aplicaciones de SAP de hello, renovación de tamaños, las tasas y requisitos de persistencia en disco.</span><span class="sxs-lookup"><span data-stu-id="4f000-138">It is critical tooinventory all hello SAP applications running in a landscape and toodetermine hello deployment mode (either 2-tier or 3-tier), versions, patches, sizes, churn rates, and disk persistence requirements.</span></span>

![Modelo de implementación](./media/site-recovery-sap/sap-typical-deployment.png)

<span data-ttu-id="4f000-140">capa de persistencia de base de datos de SAP de Hello debe protegerse mediante herramientas nativas de DBMS hello como AlwaysOn de SQL Server, Oracle DataGuard o replicación del sistema de archivos de HANA.</span><span class="sxs-lookup"><span data-stu-id="4f000-140">hello SAP Database persistence layer should be protected via hello native DBMS tools such as SQL Server AlwaysOn, Oracle DataGuard, or HANA System Replication.</span></span> <span data-ttu-id="4f000-141">nivel de cliente de Hello no también está protegido por Azure Site Recovery, pero es importante tooconsider temas que afectan a esta capa como retraso de propagación de DNS, seguridad y acceso remoto toohello centro de datos de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="4f000-141">hello client layer is also not protected by Azure Site Recovery, but it is important tooconsider topics that impact this layer such as DNS Propagation delay, security and remote access toohello DR datacenter.</span></span>

<span data-ttu-id="4f000-142">Azure Site Recovery es hello recomendada soluciones de nivel de aplicación Hola, incluidos (A) SCS.</span><span class="sxs-lookup"><span data-stu-id="4f000-142">Azure Site Recovery is hello recommended solution for hello application layer, including (A)SCS.</span></span> <span data-ttu-id="4f000-143">Otras aplicaciones, como aplicaciones SAP NetWeaver y las aplicaciones de SAP no forman parte del programa Hola general SAP entorno de implementación y también debería estar protegida con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4f000-143">Other applications such as non-NetWeaver SAP applications and non-SAP applications form part of hello overall SAP deployment environment and should also be protected with Azure Site Recovery.</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="4f000-144">Replicación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="4f000-144">Replicate virtual machines</span></span>
<span data-ttu-id="4f000-145">Siga [esta guía](azure-to-azure-walkthrough-enable-replication.md) toostart replicar todas Hola toohello de máquinas virtuales de aplicación de SAP Azure centro de datos de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="4f000-145">Follow [this guidance](azure-to-azure-walkthrough-enable-replication.md) toostart replicating all hello SAP application virtual machines toohello Azure DR datacenter.</span></span>

<span data-ttu-id="4f000-146">Si usa una dirección IP estática, puede especificar Hola IP que desee Hola tootake de máquina virtual en la sección de tarjetas de interfaz de red de hello en configuración de red y proceso.</span><span class="sxs-lookup"><span data-stu-id="4f000-146">If you are using a static IP, you can specify hello IP that you want hello virtual machine tootake in hello Network interface cards section in Compute and Network settings.</span></span>

![IP de destino](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="4f000-148">Creación de un plan de recuperación</span><span class="sxs-lookup"><span data-stu-id="4f000-148">Creating a recovery plan</span></span>
<span data-ttu-id="4f000-149">Un plan de recuperación permite secuenciación Hola conmutación por error de distintos niveles de una aplicación de varios niveles, por lo tanto, mantener la coherencia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f000-149">A recovery plan allows sequencing hello failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="4f000-150">Siga los pasos de hello descritos [aquí](site-recovery-create-recovery-plans.md) al crear un plan de recuperación para una aplicación web de varios niveles.</span><span class="sxs-lookup"><span data-stu-id="4f000-150">Follow hello steps described [here](site-recovery-create-recovery-plans.md) while creating a recovery plan for a multi-tier web application.</span></span>

### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="4f000-151">Agregar plan de recuperación de toohello de secuencias de comandos</span><span class="sxs-lookup"><span data-stu-id="4f000-151">Adding scripts toohello recovery plan</span></span>
<span data-ttu-id="4f000-152">Quizás necesite toodo ciertas operaciones sobre Hola conmutación por error de máquinas virtuales de Azure post/prueba de conmutación por error para su toofunction aplicaciones correctamente.</span><span class="sxs-lookup"><span data-stu-id="4f000-152">You may need toodo some operations on hello Azure virtual machines post failover/test failover for your applications toofunction correctly.</span></span> <span data-ttu-id="4f000-153">Puede automatizar la operación de conmutación por error de post hello como actualizar entrada DNS y el cambio de enlaces y las conexiones, agregando los scripts correspondientes en el plan de recuperación de hello tal y como se describe en [este artículo](site-recovery-create-recovery-plans.md#add-scripts).</span><span class="sxs-lookup"><span data-stu-id="4f000-153">You can automate hello post failover operation such as updating DNS entry, and changing bindings and connections, by adding corresponding scripts in hello recovery plan as described in [this article](site-recovery-create-recovery-plans.md#add-scripts).</span></span>

### <a name="dns-update"></a><span data-ttu-id="4f000-154">Actualización de DNS</span><span class="sxs-lookup"><span data-stu-id="4f000-154">DNS update</span></span>
<span data-ttu-id="4f000-155">Si Hola DNS está configurado para la actualización dinámica de DNS, entonces máquinas virtuales normalmente se haya actualizado Hola DNS con la dirección IP de hello nuevo una vez que se inician.</span><span class="sxs-lookup"><span data-stu-id="4f000-155">If hello DNS is configured for dynamic DNS update, then virtual machines usually update hello DNS with hello new IP once they start.</span></span> <span data-ttu-id="4f000-156">Si desea que tooadd un tooupdate paso explícito DNS con hello nuevas direcciones IP de máquinas virtuales de hello, a continuación, agregue esto [tooupdate IP en DNS de script](https://aka.ms/asr-dns-update) como una acción posterior en grupos de planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4f000-156">If you want tooadd an explicit step tooupdate DNS with hello new IPs of hello virtual machines then add this [script tooupdate IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

## <a name="example-azure-to-azure-deployment"></a><span data-ttu-id="4f000-157">Ejemplo de implementación de Azure a Azure</span><span class="sxs-lookup"><span data-stu-id="4f000-157">Example Azure-to-Azure deployment</span></span>
<span data-ttu-id="4f000-158">Se representa en diagrama de hello siguiente escenario de recuperación ante desastres de Azure en Azure de Azure Site Recovery de hello:</span><span class="sxs-lookup"><span data-stu-id="4f000-158">In hello diagram below hello Azure Site Recovery Azure-to-Azure DR scenario is depicted:</span></span>
* <span data-ttu-id="4f000-159">Centro de datos principal se encuentra en Singapur (Asia Sureste de Azure) de Hola y Hola centro de datos de recuperación ante desastres es Hong Kong (Azure Asia oriental).</span><span class="sxs-lookup"><span data-stu-id="4f000-159">hello Primary Datacenter is in Singapore (Azure South-East Asia) and hello DR datacenter is Hong Kong (Azure East Asia).</span></span>  <span data-ttu-id="4f000-160">En este escenario, se proporciona una alta disponibilidad local al tener en Singapur dos máquinas virtuales que ejecutan SQL Server AlwaysOn en modo sincrónico.</span><span class="sxs-lookup"><span data-stu-id="4f000-160">In this scenario, local High Availability is provided by having two VMs running SQL Server AlwaysOn in Synchronous mode in Singapore.</span></span>
* <span data-ttu-id="4f000-161">Hola ASCS de recurso compartido de archivo puede ser usado tooprovide alta disponibilidad para hello SAP puntos de error únicos.</span><span class="sxs-lookup"><span data-stu-id="4f000-161">hello File Share ASCS can be used tooprovide HA for hello SAP single points of failure.</span></span> <span data-ttu-id="4f000-162">ASCS de recurso compartido de archivos no requiere un disco compartido de clúster y no son necesarias las aplicaciones como SIOS.</span><span class="sxs-lookup"><span data-stu-id="4f000-162">File Share ASCS does not require a cluster shared disk, and applications such as SIOS are not required.</span></span>
* <span data-ttu-id="4f000-163">Protección de recuperación ante desastres para capa de DBMS Hola se logra mediante la replicación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="4f000-163">DR protection for hello DBMS layer is achieved using Asynchronous replication.</span></span>
* <span data-ttu-id="4f000-164">Este escenario muestra "simétrico DR": usar un término toodescribe una solución de recuperación ante desastres que es una réplica exacta de producción, por lo tanto, Hola solución de recuperación ante desastres de SQL Server tiene alta disponibilidad local.</span><span class="sxs-lookup"><span data-stu-id="4f000-164">This scenario shows “symmetrical DR” – a term used toodescribe a DR solution that is an exact replica of production, therefore hello DR SQL Server solution has local High Availability.</span></span> <span data-ttu-id="4f000-165">no es obligatorio para la capa de base de datos de Hola Hola usar DR simétrico y muchos clientes aprovechan la flexibilidad de Hola de las implementaciones de nube toobuild un nodo de disponibilidad alta local rápidamente después de un evento de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="4f000-165">hello use of symmetrical DR is not mandatory for hello Database layer, and many customers leverage hello flexibility of cloud deployments toobuild a local High Availability Node quickly after a DR event.</span></span>
* <span data-ttu-id="4f000-166">diagrama de Hello muestra hello ASCS de SAP NetWeaver y nivel de servidor de aplicación replicada por Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4f000-166">hello diagram depicts hello SAP NetWeaver ASCS and Application server layer replicated by Azure Site Recovery.</span></span>

![Escenario de replicación](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="4f000-168">Realización de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="4f000-168">Doing a test failover</span></span>
<span data-ttu-id="4f000-169">Siga [esta guía](azure-to-azure-walkthrough-test-failover.md) toodo una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="4f000-169">Follow [this guidance](azure-to-azure-walkthrough-test-failover.md) toodo a test failover.</span></span>

1.  <span data-ttu-id="4f000-170">Vaya tooAzure portal y seleccione el almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4f000-170">Go tooAzure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="4f000-171">Haga clic en el plan de recuperación de hello creado para aplicaciones de SAP (s).</span><span class="sxs-lookup"><span data-stu-id="4f000-171">Click on hello recovery plan created for SAP applications(s).</span></span>
3.  <span data-ttu-id="4f000-172">Haga clic en 'Probar conmutación por error'.</span><span class="sxs-lookup"><span data-stu-id="4f000-172">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="4f000-173">Seleccione el punto de recuperación y el proceso de conmutación por error de prueba de red virtual de Azure toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="4f000-173">Select recovery point and Azure virtual network toostart hello test failover process.</span></span>
5.  <span data-ttu-id="4f000-174">Una vez que el entorno secundario hello es hacia arriba, puede realizar sus validaciones.</span><span class="sxs-lookup"><span data-stu-id="4f000-174">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="4f000-175">Después de completar las validaciones de hello, haga clic en 'Conmutación por error de limpieza prueba' y conmutación por error de tooclean Hola entorno.</span><span class="sxs-lookup"><span data-stu-id="4f000-175">Once hello validations are complete, click on ‘Cleanup test failover’ and tooclean hello failover environment.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="4f000-176">Realización de una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="4f000-176">Doing a failover</span></span>
<span data-ttu-id="4f000-177">Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="4f000-177">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="4f000-178">Vaya tooAzure portal y seleccione el almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4f000-178">Go tooAzure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="4f000-179">Haga clic en el plan de recuperación de hello creado para aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="4f000-179">Click on hello recovery plan created for SAP application(s).</span></span>
3.  <span data-ttu-id="4f000-180">Haga clic en 'Conmutación por error'.</span><span class="sxs-lookup"><span data-stu-id="4f000-180">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="4f000-181">Seleccione el proceso de conmutación por error de Hola de toostart de punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4f000-181">Select recovery point toostart hello failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f000-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f000-182">Next steps</span></span>
<span data-ttu-id="4f000-183">Más información acerca de cómo crear una solución de recuperación ante desastres para las implementaciones SAP NetWeaver con Azure Site Recovery en [estas notas del producto](http://aka.ms/asr-sap).</span><span class="sxs-lookup"><span data-stu-id="4f000-183">Learn more about building a disaster recovery solution for SAP NetWeaver deployments using Azure Site Recovery in [this whitepaper](http://aka.ms/asr-sap).</span></span> <span data-ttu-id="4f000-184">Hola notas del producto también artículo incluye recomendaciones para distintas arquitecturas SAP, listas de aplicaciones compatibles y los tipos VM para SAP en Azure y describen los posibles planes de pruebas para la solución de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="4f000-184">hello whitepaper also discusses recommendations for different SAP architectures, lists supported applications and VM types for SAP on Azure, and describes possible testing plans for your disaster recovery solution.</span></span>

<span data-ttu-id="4f000-185">Obtenga más información sobre la [replicación de otras cargas de trabajo](site-recovery-workload.md) con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4f000-185">Learn more about [replicating other workloads](site-recovery-workload.md) using Site Recovery.</span></span>