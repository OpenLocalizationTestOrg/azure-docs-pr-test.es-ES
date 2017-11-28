---
title: "aaaReplicate física tooAzure de servidores con Azure Site Recovery local | Documentos de Microsoft"
description: "Proporciona información general de los pasos de hello para la replicación de las cargas de trabajo que se ejecutan en local tooAzure de servidores físicos de Windows/Linux con hello servicio Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="2d8bd-103">Replicar servidores físicos tooAzure con Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2d8bd-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="2d8bd-104">Este artículo proporciona información general de hello pasos necesarios tooreplicate local Windows/Linux servidores físicos tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="2d8bd-105">Paso 1: revisión de la arquitectura y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2d8bd-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="2d8bd-106">Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello deberá tooset la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="2d8bd-107">Vaya demasiado[paso 1: revisar la arquitectura de Hola](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="2d8bd-108">Paso 2: revisión de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2d8bd-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="2d8bd-109">Asegúrese de que tiene requisitos previos de hello en su lugar para cada componente de implementación:</span><span class="sxs-lookup"><span data-stu-id="2d8bd-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="2d8bd-110">**Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="2d8bd-111">**Componentes locales de Site Recovery**: necesita una máquina que ejecute componentes locales de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="2d8bd-112">**Replicar máquinas**: servidores que desea tooreplicate necesitan toocomply con local y requisitos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="2d8bd-113">Vaya demasiado[paso 2: revisar los requisitos previos y limitaciones](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="2d8bd-114">Paso 3: planeamiento de la capacidad</span><span class="sxs-lookup"><span data-stu-id="2d8bd-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="2d8bd-115">Si está realizando una implementación completa debe toofigure qué recursos de replicación que se necesita.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="2d8bd-116">Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="2d8bd-117">Vaya demasiado[paso 3: planear la capacidad](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="2d8bd-118">Paso 4: planeamiento de las redes</span><span class="sxs-lookup"><span data-stu-id="2d8bd-118">Step 4: Plan networking</span></span>

<span data-ttu-id="2d8bd-119">Debe toodo algunos planeación tooensure que máquinas virtuales de Azure son toonetworks conectado después de producirse la conmutación por error, y que disponen de hello derecho de direcciones IP de una red.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="2d8bd-120">Vaya demasiado[paso 4: planear las redes](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="2d8bd-121">Paso 5: preparación de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="2d8bd-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="2d8bd-122">Antes de empezar hay que configurar las redes y el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="2d8bd-123">Vaya demasiado[paso 5: preparar Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="2d8bd-124">Paso 6: Configurar un almacén</span><span class="sxs-lookup"><span data-stu-id="2d8bd-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="2d8bd-125">Configurar una tooorchestrate de almacén de servicios de recuperación y administrar la replicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="2d8bd-126">Al configurar el almacén de hello, especifique qué desea tooreplicate, y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="2d8bd-127">Vaya demasiado[paso 6: configurar un almacén](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="2d8bd-128">Paso 7: Configurar los valores de origen y destino</span><span class="sxs-lookup"><span data-stu-id="2d8bd-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="2d8bd-129">Configurar las opciones para el origen de Hola y sitio (Azure) de destino.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="2d8bd-130">Configuración de código fuente incluye ejecutando el programa de instalación unificada tooinstall componentes de Site Recovery de hello locales.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="2d8bd-131">Vaya demasiado[paso 7: configurar el origen de Hola y de destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="2d8bd-132">Paso 8: Configurar una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="2d8bd-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="2d8bd-133">Configurar una directiva toospecify cómo físico de servidores deben replicar.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="2d8bd-134">Vaya demasiado[paso 8: configurar una directiva de replicación](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="2d8bd-135">Paso 9: Instalar el servicio de movilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="2d8bd-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="2d8bd-136">servicio de movilidad de Hello debe estar instalado en cada servidor que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="2d8bd-137">Hay unos tooset formas servicio hello, con la instalación de inserción o extracción.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="2d8bd-138">Vaya demasiado[paso 9: instalar el servicio de movilidad de Hola](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="2d8bd-139">Paso 10: habilitación de la replicación</span><span class="sxs-lookup"><span data-stu-id="2d8bd-139">Step 10: Enable replication</span></span>

<span data-ttu-id="2d8bd-140">Después de hello Mobility service se ejecuta en un servidor, puede habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="2d8bd-141">Después de habilitar esta opción, se produce la replicación inicial de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="2d8bd-142">Vaya demasiado[paso 10: habilitar la replicación](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="2d8bd-143">Paso 11: ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="2d8bd-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="2d8bd-144">Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="2d8bd-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="2d8bd-145">Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="2d8bd-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

