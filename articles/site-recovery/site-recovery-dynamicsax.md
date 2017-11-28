---
title: "una implementación de Dynamics AX de varios nivel con Azure Site Recovery aaaReplicate | Documentos de Microsoft"
description: "Este artículo se describe cómo tooreplicate y proteger con Azure Site Recovery de Dynamics AX"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="1bc58-103">Replicación de una aplicación Dynamics AX de niveles múltiples mediante Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1bc58-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="1bc58-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1bc58-104">Overview</span></span>


<span data-ttu-id="1bc58-105">Microsoft Dynamics AX es una solución ERP más popular de hello entre el proceso de toostandardized de las empresas en diferentes ubicaciones, administrar recursos y simplificar el cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="1bc58-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="1bc58-106">Considerando las aplicación hello es organización tooan críticos del negocio es muy importante toobe seguro de que si un desastre, aplicación debe estar activados y ejecutándose en un tiempo mínimo.</span><span class="sxs-lookup"><span data-stu-id="1bc58-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="1bc58-107">En la actualidad, la aplicación Microsoft Dynamics AX no tiene integrada ninguna funcionalidad de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="1bc58-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="1bc58-108">Microsoft Dynamics AX consta de muchos componentes de servidor como base de datos de servidor de objetos de aplicación, Active Directory (AD), SQL Server, SharePoint Server, recuperación de desastres de Reporting Server etc. toomanage Hola de cada uno de estos componentes manualmente es no solo costosa también propensas a errores.</span><span class="sxs-lookup"><span data-stu-id="1bc58-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="1bc58-109">En este artículo se explica en detalle cómo crear una solución de recuperación ante desastres para la aplicación Dynamics AX mediante [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1bc58-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="1bc58-110">También se describen las conmutaciones por error planeadas, no planeadas o de prueba con el plan de recuperación de un solo clic, las configuraciones admitidas y los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="1bc58-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="1bc58-111">La solución de recuperación ante desastres de Azure Site Recovery está totalmente probada, certificada y recomendada por Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="1bc58-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="1bc58-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1bc58-112">Prerequisites</span></span>

<span data-ttu-id="1bc58-113">La implementación de recuperación ante desastres para aplicaciones de Dynamics AX con Azure Site Recovery requiere Hola siguiendo los requisitos previos completados.</span><span class="sxs-lookup"><span data-stu-id="1bc58-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="1bc58-114">• Se ha instalado una implementación local de Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="1bc58-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="1bc58-115">• Se ha creado un almacén de Azure Recovery Services en una suscripción de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1bc58-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="1bc58-116">• Si Azure es el sitio de recuperación, ejecutar herramienta de evaluación de preparación de máquina Virtual de Azure de hello en tooensure de máquinas virtuales que sean compatibles con máquinas virtuales de Azure y servicios de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1bc58-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="1bc58-117">Compatibilidad de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1bc58-117">Site Recovery support</span></span>

<span data-ttu-id="1bc58-118">A fin de Hola de creación de este artículo, se utilizaron máquinas virtuales VMware con 2012R3 de Dynamics AX en Windows Server 2012 R2 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1bc58-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="1bc58-119">Como la replicación de recuperación de sitios es independiente de la aplicación, se proporcionan recomendaciones de hello aquí son toohold esperado en los escenarios siguientes también.</span><span class="sxs-lookup"><span data-stu-id="1bc58-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="1bc58-120">Origen y destino</span><span class="sxs-lookup"><span data-stu-id="1bc58-120">Source and target</span></span>

<span data-ttu-id="1bc58-121">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="1bc58-121">**Scenario**</span></span> | <span data-ttu-id="1bc58-122">**sitio secundario tooa**</span><span class="sxs-lookup"><span data-stu-id="1bc58-122">**tooa secondary site**</span></span> | <span data-ttu-id="1bc58-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="1bc58-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="1bc58-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="1bc58-124">**Hyper-V**</span></span> | <span data-ttu-id="1bc58-125">Sí</span><span class="sxs-lookup"><span data-stu-id="1bc58-125">Yes</span></span> | <span data-ttu-id="1bc58-126">Sí</span><span class="sxs-lookup"><span data-stu-id="1bc58-126">Yes</span></span>
<span data-ttu-id="1bc58-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="1bc58-127">**VMware**</span></span> | <span data-ttu-id="1bc58-128">Sí</span><span class="sxs-lookup"><span data-stu-id="1bc58-128">Yes</span></span> | <span data-ttu-id="1bc58-129">Sí</span><span class="sxs-lookup"><span data-stu-id="1bc58-129">Yes</span></span>
<span data-ttu-id="1bc58-130">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="1bc58-130">**Physical server**</span></span> | <span data-ttu-id="1bc58-131">Sí</span><span class="sxs-lookup"><span data-stu-id="1bc58-131">Yes</span></span> | <span data-ttu-id="1bc58-132">Sí</span><span class="sxs-lookup"><span data-stu-id="1bc58-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="1bc58-133">Habilitar la recuperación ante desastres de la aplicación Dynamics AX mediante Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1bc58-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="1bc58-134">Proteger la aplicación Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="1bc58-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="1bc58-135">Cada componente de hello Dynamics AX necesidades toobe protegido tooenable Hola aplicación completa replicación y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="1bc58-136">En esta sección se describe:</span><span class="sxs-lookup"><span data-stu-id="1bc58-136">This section covers:</span></span>

<span data-ttu-id="1bc58-137">**1. Protección de Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1bc58-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="1bc58-138">**2. Protección del nivel de SQL**</span><span class="sxs-lookup"><span data-stu-id="1bc58-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="1bc58-139">**3. Protección de los niveles de aplicación y web**</span><span class="sxs-lookup"><span data-stu-id="1bc58-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="1bc58-140">**4. Configuración de red**</span><span class="sxs-lookup"><span data-stu-id="1bc58-140">**4. Networking configuration**</span></span>

<span data-ttu-id="1bc58-141">**5. Plan de recuperación**</span><span class="sxs-lookup"><span data-stu-id="1bc58-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="1bc58-142">1. Configuración de la replicación de DNS y AD</span><span class="sxs-lookup"><span data-stu-id="1bc58-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="1bc58-143">Active Directory es necesario en el sitio de recuperación ante desastres de Hola para toofunction de aplicación de Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="1bc58-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="1bc58-144">Hay dos opciones recomendadas basándose en complejidad Hola Hola del local del entorno de cliente.</span><span class="sxs-lookup"><span data-stu-id="1bc58-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="1bc58-145">**Opción 1**</span><span class="sxs-lookup"><span data-stu-id="1bc58-145">**Option 1**</span></span>

<span data-ttu-id="1bc58-146">Si el cliente hello tiene un número pequeño de aplicaciones y un controlador de dominio para su toda sitio local y se se conmuta por error todo el sitio Hola juntas, a continuación, se recomienda utilizar la replicación de ASR tooreplicate Hola DC máquina toosecondary sitio ( es aplicable para el sitio tooSite y tooAzure de sitio).</span><span class="sxs-lookup"><span data-stu-id="1bc58-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="1bc58-147">**Opción 2**</span><span class="sxs-lookup"><span data-stu-id="1bc58-147">**Option 2**</span></span>

<span data-ttu-id="1bc58-148">Si cliente hello tiene un gran número de aplicaciones y ejecuta un bosque de Active Directory y conmutará pocas aplicaciones a la vez, se recomienda configurar un controlador de dominio adicional en el sitio de recuperación ante desastres de hello (sitio secundario o en Azure).</span><span class="sxs-lookup"><span data-stu-id="1bc58-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="1bc58-149">Consulte demasiado[guía complementaria sobre la realización de un controlador de dominio disponible en el sitio de recuperación ante desastres](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1bc58-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="1bc58-150">Para el resto de este documento, supondremos que habrá un controlador de dominio disponible en el sitio de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="1bc58-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="1bc58-151">2. Configuración de la replicación de SQL Server</span><span class="sxs-lookup"><span data-stu-id="1bc58-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="1bc58-152">Consulte la Guía de toocompanion para orientación técnica detallada sobre Hola recomendada la opción para proteger [nivel SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1bc58-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="1bc58-153">3. Habilitar la protección del cliente de Dynamics AX y las máquinas virtuales de AOS</span><span class="sxs-lookup"><span data-stu-id="1bc58-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="1bc58-154">Realizar la configuración de Azure Site Recovery pertinentes en función de si se implementan máquinas virtuales de hello en [Hyper-V](site-recovery-hyper-v-site-to-azure.md) o en [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="1bc58-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="1bc58-155">Tooconfigure de frecuencia coherente de bloqueo recomendado es de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="1bc58-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="1bc58-156">Hola por debajo de instantánea muestra el estado de protección de Hola de máquinas virtuales de componente de Dynamics en escenario de protección 'TooAzure de sitio de VMware'.</span><span class="sxs-lookup"><span data-stu-id="1bc58-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="1bc58-157">![Elementos protegidos ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="1bc58-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="1bc58-158">4. Configuración de red</span><span class="sxs-lookup"><span data-stu-id="1bc58-158">4. Configure Networking</span></span>
<span data-ttu-id="1bc58-159">Configuración de procesos de máquina virtual y configuración de red</span><span class="sxs-lookup"><span data-stu-id="1bc58-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="1bc58-160">Cliente AX hello y las máquinas virtuales de AOS configurar configuración de red en Azure Site Recovery para que redes de VM de hello obtener toohello adjunto red de recuperación ante desastres apropiado después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1bc58-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="1bc58-161">Asegúrese de red de recuperación ante desastres de Hola para estos niveles es enrutable toohello nivel de SQL.</span><span class="sxs-lookup"><span data-stu-id="1bc58-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="1bc58-162">Puede seleccionar Hola VM Hola replica configuración de red de elementos tooconfigure Hola tal y como se muestra en la instantánea de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="1bc58-163">Para los servidores AOS seleccione conjunto de disponibilidad correcta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc58-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="1bc58-164">Si está usando una dirección IP estática y luego especifique Hola IP que desee Hola tootake de máquina virtual en hello **IP de destino** campo ![configuración de red](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="1bc58-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="1bc58-165">5. Creación de un plan de recuperación</span><span class="sxs-lookup"><span data-stu-id="1bc58-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="1bc58-166">Puede crear un plan de recuperación en proceso de conmutación por error de Azure Site Recovery tooautomate Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc58-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="1bc58-167">Agregar capa de aplicación y de nivel web Hola Plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="1bc58-168">Ordénelas en grupos diferentes, por lo Hola front-end cierre antes de nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="1bc58-169">Seleccionar almacén de Azure Site Recovery de hello en su suscripción y haga clic en el icono de planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="1bc58-170">Haga clic en Plan de recuperación y especifique un nombre.</span><span class="sxs-lookup"><span data-stu-id="1bc58-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="1bc58-171">Seleccione hello 'Source' y 'Target'.</span><span class="sxs-lookup"><span data-stu-id="1bc58-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="1bc58-172">destino de Hello puede ser el sitio secundario o de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc58-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="1bc58-173">Si elige Azure, debe especificar el modelo de implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="1bc58-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Creación del plan de recuperación](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="1bc58-175">Seleccione Hola AOS y el plan de recuperación de toohello de máquinas virtuales de cliente y haga clic en ✓.</span><span class="sxs-lookup"><span data-stu-id="1bc58-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="1bc58-176">![Crear plan de recuperación](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="1bc58-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plan de recuperación](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="1bc58-178">Puede personalizar el plan de recuperación de Hola para aplicación de Dynamics AX mediante la adición de varios pasos tal como se detalla a continuación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="1bc58-179">Hola por encima de instantánea muestra hello el plan de recuperación completo después de agregar todos los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc58-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="1bc58-180">*Pasos:*</span><span class="sxs-lookup"><span data-stu-id="1bc58-180">*Steps:*</span></span>

<span data-ttu-id="1bc58-181">*1. Pasos de conmutación por error de SQL Server*</span><span class="sxs-lookup"><span data-stu-id="1bc58-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="1bc58-182">Consulte demasiado['Solución de recuperación ante desastres de SQL Server'](site-recovery-sql.md) guía complementaria para obtener más información acerca de servidor de tooSQL concreto de pasos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="1bc58-183">*2. Conmutación por error el grupo 1: Conmutar por error las máquinas virtuales de hello AOS*</span><span class="sxs-lookup"><span data-stu-id="1bc58-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="1bc58-184">Asegúrese de que el punto de recuperación de hello seleccionado es lo más cerca posible toohello de base de datos PIT pero no con antelación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="1bc58-185">*3. Script: Equilibrador de carga del complemento (solo E-A)* agregar una secuencia de comandos (a través de la automatización de Azure) después del grupo de AOS VM aparece tooadd un tooit de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1bc58-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="1bc58-186">Puede usar una secuencia de comandos toodo esta tarea.</span><span class="sxs-lookup"><span data-stu-id="1bc58-186">You can use a script toodo this task.</span></span> <span data-ttu-id="1bc58-187">Consulte el artículo [cómo tooadd equilibrador de carga para recuperación ante desastres de aplicación de varios niveles](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="1bc58-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="1bc58-188">*4. Grupo de conmutación por error 2: Conmutar por error cliente AX hello las máquinas virtuales.*</span><span class="sxs-lookup"><span data-stu-id="1bc58-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="1bc58-189">Conmutar por error el nivel de web de hello las máquinas virtuales como parte del plan de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc58-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="1bc58-190">Realización de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="1bc58-190">Doing a test failover</span></span>

<span data-ttu-id="1bc58-191">Consulte too'AD DR Solution ' y 'Solución de recuperación ante desastres de SQL Server' las guías complementarias para consideraciones específicas tooAD y SQL server respectivamente durante la conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="1bc58-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="1bc58-192">Vaya tooAzure portal y seleccione el almacén de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1bc58-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="1bc58-193">Haga clic en el plan de recuperación de hello creado para Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="1bc58-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="1bc58-194">Haga clic en Probar conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1bc58-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="1bc58-195">Seleccione el proceso de conmutación por error de prueba de hello red virtual toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc58-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="1bc58-196">Una vez que el entorno secundario hello es hacia arriba, puede realizar sus validaciones.</span><span class="sxs-lookup"><span data-stu-id="1bc58-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="1bc58-197">Después de completar las validaciones de hello, puede seleccionar 'Validaciones completar' y entorno de conmutación por error de prueba de Hola se borrarán.</span><span class="sxs-lookup"><span data-stu-id="1bc58-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="1bc58-198">Siga [esta guía](site-recovery-test-failover-to-azure.md) toodo una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="1bc58-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="1bc58-199">Realización de una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="1bc58-199">Doing a failover</span></span>

1.  <span data-ttu-id="1bc58-200">Vaya tooAzure portal y seleccione el almacén de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1bc58-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="1bc58-201">Haga clic en el plan de recuperación de hello creado para Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="1bc58-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="1bc58-202">Haga clic en Conmutación por error y seleccione Conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1bc58-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="1bc58-203">Seleccionar red de destino de Hola y haga clic en el proceso de conmutación por error ✓ toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="1bc58-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="1bc58-204">Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1bc58-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="1bc58-205">Realización de una conmutación por recuperación</span><span class="sxs-lookup"><span data-stu-id="1bc58-205">Perform a Failback</span></span>

<span data-ttu-id="1bc58-206">Consulte too'SQL solución de recuperación ante desastres del servidor ' guía complementaria de consideraciones específicas tooSQL server durante la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="1bc58-207">Vaya tooAzure portal y seleccione el almacén de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1bc58-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="1bc58-208">Haga clic en el plan de recuperación de hello creado para Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="1bc58-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="1bc58-209">Haga clic en Conmutación por error y seleccione Conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1bc58-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="1bc58-210">Haga clic en Cambiar dirección.</span><span class="sxs-lookup"><span data-stu-id="1bc58-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="1bc58-211">Seleccione opciones adecuadas de hello - sincronización de datos y las opciones de creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="1bc58-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="1bc58-212">Haga clic en el proceso ✓ toostart hello 'Conmutación por recuperación'.</span><span class="sxs-lookup"><span data-stu-id="1bc58-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="1bc58-213">Siga [estas directrices](site-recovery-failback-azure-to-vmware.md) cuando realice una conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="1bc58-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="1bc58-214">Resumen</span><span class="sxs-lookup"><span data-stu-id="1bc58-214">Summary</span></span>
<span data-ttu-id="1bc58-215">Con Azure Site Recovery, puede crear un plan completo de recuperación ante desastres automatizado para su aplicación Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="1bc58-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="1bc58-216">Se puede iniciar la conmutación por error de hello en segundos desde cualquier lugar en Hola eventos de interrupción y poner la aplicación hello en ejecución en minutos.</span><span class="sxs-lookup"><span data-stu-id="1bc58-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc58-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bc58-217">Next steps</span></span>
<span data-ttu-id="1bc58-218">Lectura [¿qué cargas de trabajo se debe proteger?](site-recovery-workload.md) toolearn más sobre la protección de cargas de trabajo empresariales con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1bc58-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
