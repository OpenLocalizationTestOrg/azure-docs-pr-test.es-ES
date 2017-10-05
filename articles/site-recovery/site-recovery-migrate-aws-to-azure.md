---
title: "Migración de máquinas virtuales de AWS a Azure| Microsoft Docs"
description: "En este artículo se describe cómo migrar máquinas virtuales que se están ejecutando en Amazon Web Services (AWS) en Azure con Azure Site Recovery."
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
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="0dd2b-103">Migrar máquinas virtuales de Amazon Web Services (AWS) a Azure con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0dd2b-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="0dd2b-104">En este artículo se describe cómo migrar instancias de AWS Windows a máquinas virtuales de Azure con el servicio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dd2b-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="0dd2b-105">La migración es realmente una conmutación por error de AWS a Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="0dd2b-106">No podrá conmutar por recuperación máquinas en AWS y no habrá ninguna replicación en curso.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="0dd2b-107">En este artículo se describen los pasos necesarios para realizar la migración en Azure Portal; se basan en las instrucciones para [replicar una máquina física en Azure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0dd2b-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="0dd2b-108">Publique cualquier comentario o pregunta que tenga en la parte inferior de este artículo, o bien en el [foro de Servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="0dd2b-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="0dd2b-109">Sistemas operativos compatibles</span><span class="sxs-lookup"><span data-stu-id="0dd2b-109">Supported operating systems</span></span>

<span data-ttu-id="0dd2b-110">Site Recovery puede usarse para migrar instancias de EC2 que se ejecuten en cualquiera de los siguientes sistemas operativos:</span><span class="sxs-lookup"><span data-stu-id="0dd2b-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="0dd2b-111">Windows (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="0dd2b-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="0dd2b-112">Windows Server 2008 R2 SP1 + (solo controladores de Citrix PV o de AWS PV).</span><span class="sxs-lookup"><span data-stu-id="0dd2b-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="0dd2b-113">**No se admiten las instancias que ejecutan controladores de RedHat PV**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0dd2b-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="0dd2b-114">Linux (solo 64 bits)</span><span class="sxs-lookup"><span data-stu-id="0dd2b-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="0dd2b-115">Red Hat Enterprise Linux 6.7 (solo instancias virtualizadas de HVM)</span><span class="sxs-lookup"><span data-stu-id="0dd2b-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dd2b-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0dd2b-116">Prerequisites</span></span>

<span data-ttu-id="0dd2b-117">Requisitos para realizar esta implementación:</span><span class="sxs-lookup"><span data-stu-id="0dd2b-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="0dd2b-118">**Servidor de configuración**: una máquina virtual de Amazon EC2 que ejecute Windows Server 2012 R2 implementada como servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="0dd2b-119">De forma predeterminada, los demás componentes de Azure Site Recovery (el servidor de procesos y el servidor de destino maestro) se instalan al implementar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="0dd2b-120">En este artículo se describen los pasos necesarios para realizar la migración en Azure Portal; se basan en las instrucciones para [obtener más información](site-recovery-components.md).</span><span class="sxs-lookup"><span data-stu-id="0dd2b-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="0dd2b-121">**Instancias de EC2**: las instancias de máquinas virtuales Amazon EC2 que quiere migrar.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="0dd2b-122">Pasos de implementación</span><span class="sxs-lookup"><span data-stu-id="0dd2b-122">Deployment steps</span></span>

1. <span data-ttu-id="0dd2b-123">Cree un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="0dd2b-124">El grupo de seguridad de las instancias de EC2 debe tener reglas configuradas para permitir la comunicación entre la instancia de EC2 que se va a migrar y la instancia en la que se planea implementar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="0dd2b-125">En la misma nube privada virtual de Amazon que las instancias de EC2, implemente un servidor de configuración ASR.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="0dd2b-126">Consulte los requisitos previos de VMWare y Physical de Azure para obtener los requisitos de implementación del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="0dd2b-128">Una vez implementado el servidor de configuración en AWS y después de registrarlo con el almacén de Recovery Services, debería ver el servidor de configuración y el de procesos en la infraestructura de Site Recovery como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0dd2b-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="0dd2b-130">Después de implementar el servidor de configuración (puede tardar en aparecer hasta 15 minutos), valide que se puede comunicar con las máquinas virtuales que quiere migrar.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="0dd2b-131">[Configure las opciones de replicación](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="0dd2b-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="0dd2b-132">Habilite la replicación: Habilite la replicación para las máquinas virtuales que desea migrar.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="0dd2b-133">Puede detectar las instancias EC2 con las direcciones IP privada que se pueden obtener desde la consola EC2.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="0dd2b-135">Una vez que se han protegido las instancias de EC2 y se ha completado la replicación en Azure, [ejecute una conmutación por error de prueba](site-recovery-test-failover-to-azure.md) para validar el rendimiento de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="0dd2b-137">Ejecute una conmutación por error desde AWS a Azure para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="0dd2b-138">Si lo desea, puede crear un plan de recuperación y ejecutar una conmutación por error para migrar varias máquinas virtuales desde AWS a Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="0dd2b-139">[Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="0dd2b-140">Para la migración, no es necesario ejecutar una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="0dd2b-141">En su lugar, seleccione la opción Completar migración de cada máquina que desea migrar.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="0dd2b-142">La acción Completar migración termina el proceso de migración, quita la replicación de la máquina y se detiene la facturación de la máquina en Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="0dd2b-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dd2b-144">Next steps</span></span>

- <span data-ttu-id="0dd2b-145">[Preparación de máquinas migradas para habilitar la replicación](site-recovery-azure-to-azure-after-migration.md) en otra región para cubrir las necesidades de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="0dd2b-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="0dd2b-146">Empezar a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="0dd2b-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
