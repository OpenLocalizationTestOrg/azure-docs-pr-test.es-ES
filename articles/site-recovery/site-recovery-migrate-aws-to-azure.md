---
title: "aaaMigrate las máquinas virtuales de AWS tooAzure | Documentos de Microsoft"
description: "Este artículo describe cómo ejecutar los equipos de toomigrate virtual en tooAzure de Amazon Web Services (AWS) con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="cd251-103">Migre máquinas virtuales de Amazon Web Services (AWS) tooAzure con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="cd251-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="cd251-104">Este artículo describe cómo toomigrate AWS Windows instancias tooAzure las máquinas virtuales con hello [Azure Site Recovery](site-recovery-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="cd251-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="cd251-105">Migración es realmente una conmutación por error de AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cd251-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="cd251-106">No se puede tooAWS de máquinas de conmutación por recuperación, y no hay replicación en curso.</span><span class="sxs-lookup"><span data-stu-id="cd251-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="cd251-107">En este artículo se describen los pasos de hello para la migración en hello portal de Azure y se basan en las instrucciones de Hola de [replicar una máquina física tooAzure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cd251-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="cd251-108">Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="cd251-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="cd251-109">Sistemas operativos compatibles</span><span class="sxs-lookup"><span data-stu-id="cd251-109">Supported operating systems</span></span>

<span data-ttu-id="cd251-110">Recuperación del sitio puede ser instancias de utilizadas toomigrate EC2 que ejecute cualquiera de los siguientes sistemas operativos de hello:</span><span class="sxs-lookup"><span data-stu-id="cd251-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="cd251-111">Windows (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="cd251-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="cd251-112">Windows Server 2008 R2 SP1 + (solo controladores de Citrix PV o de AWS PV).</span><span class="sxs-lookup"><span data-stu-id="cd251-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="cd251-113">**No se admiten las instancias que ejecutan controladores de RedHat PV**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cd251-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="cd251-114">Linux (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="cd251-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="cd251-115">Red Hat Enterprise Linux 6.7 (solo instancias virtualizadas de HVM)</span><span class="sxs-lookup"><span data-stu-id="cd251-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd251-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd251-116">Prerequisites</span></span>

<span data-ttu-id="cd251-117">Requisitos para realizar esta implementación:</span><span class="sxs-lookup"><span data-stu-id="cd251-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="cd251-118">**Servidor de configuración**: una máquina virtual de EC2 Amazon ejecuta Windows Server 2012 R2 se implementa como servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd251-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="cd251-119">De forma predeterminada, hello otros componentes de Azure Site Recovery (servidor de proceso y servidor de destino maestro) se instalan al implementar el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd251-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="cd251-120">En este artículo se describen los pasos de hello para la migración en hello portal de Azure y se basan en las instrucciones de Hola de [obtener más información](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="cd251-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="cd251-121">**Instancias de EC2**: Hola Amazon EC2 instancias de máquinas virtuales que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="cd251-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="cd251-122">Pasos de implementación</span><span class="sxs-lookup"><span data-stu-id="cd251-122">Deployment steps</span></span>

1. <span data-ttu-id="cd251-123">Cree un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cd251-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="cd251-124">Grupo de seguridad de las instancias de EC2 Hola debe tener reglas configuradas tooallow comunicación entre instancia EC2 de Hola que desea toomigrate y en el que piensa hello toodeploy servidor de configuración de instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd251-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="cd251-125">En hello mismo Amazon Virtual privada en la nube como las instancias de EC2, implemente un servidor de configuración de ASR.</span><span class="sxs-lookup"><span data-stu-id="cd251-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="cd251-126">Consulte Hola VMware / físicas tooAzure los requisitos previos para requisitos de implementación de servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="cd251-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="cd251-128">Una vez que el servidor de configuración está implementado en AWS y registrado con el almacén de servicios de recuperación, debería ver los servidores de configuración de Hola y procesos en la infraestructura de Site Recovery tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="cd251-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="cd251-130">Después de implementar el servidor de configuración de hello (podría tardar hasta too15 minustes para él tooappear), validar que puede comunicarse con máquinas virtuales de Hola que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="cd251-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="cd251-131">[Configure las opciones de replicación](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="cd251-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="cd251-132">Habilitar la replicación: habilitar la replicación de máquinas virtuales que desee toomigrate Hola.</span><span class="sxs-lookup"><span data-stu-id="cd251-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="cd251-133">Puede detectar instancias de EC2 Hola con direcciones IP privadas hello, que puede obtener desde la consola de hello EC2.</span><span class="sxs-lookup"><span data-stu-id="cd251-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="cd251-135">Una vez que se protegieron instancias Hola EC2 y Hola replicación tooAzure está completo, [ejecutar una conmutación por error de prueba](site-recovery-test-failover-to-azure.md) toovalidate rendimiento de su aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="cd251-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="cd251-137">Ejecute una conmutación por error de AWS tooAzure para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd251-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="cd251-138">Si lo desea, puede crear un plan de recuperación y ejecutar varias máquinas virtuales de una conmutación por error, toomigrate de AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cd251-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="cd251-139">[Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="cd251-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="cd251-140">Para la migración, no es necesario toocommit una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="cd251-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="cd251-141">En su lugar, selecciona la opción de completar la migración de Hola para cada máquina que desee toomigrate.</span><span class="sxs-lookup"><span data-stu-id="cd251-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="cd251-142">Hola acción de completar la migración finaliza el proceso de migración de hello, quita la replicación de la máquina de Hola y detiene la recuperación del sitio de facturación para la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd251-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="cd251-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd251-144">Next steps</span></span>

- <span data-ttu-id="cd251-145">[Preparar la replicación de máquinas migradas tooenable](site-recovery-azure-to-azure-after-migration.md) tooanother región para las necesidades de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="cd251-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="cd251-146">Empezar a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cd251-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
