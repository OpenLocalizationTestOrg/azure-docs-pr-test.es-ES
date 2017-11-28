---
title: "Hola aaaInstall servicio de movilidad de replicación de VMware tooAzure | Documentos de Microsoft"
description: "Este artículo describe cómo tooinstall Hola a agente del servicio de movilidad de la replicación de tooAzure de VMware con servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="b1b40-103">Paso 10: Instalar el servicio de movilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="b1b40-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="b1b40-104">Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de máquinas virtuales de VMware, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b40-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="b1b40-105">Hola servicio de movilidad captura escrituras de datos en un equipo y los reenvía toohello servidor de procesos.</span><span class="sxs-lookup"><span data-stu-id="b1b40-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="b1b40-106">Debe instalarse en cada equipo que desea tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b1b40-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="b1b40-107">Puede instalar manual de servicio de movilidad de hello, mediante una instalación de inserción desde el servidor de proceso de recuperación del sitio de hello cuando está habilitada la replicación o utilizar una herramienta de System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b1b40-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="b1b40-108">Si utiliza la instalación de inserción, servicio de Hola se instala en hello VM cuando está habilitada la replicación.</span><span class="sxs-lookup"><span data-stu-id="b1b40-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="b1b40-109">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b1b40-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="b1b40-110">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="b1b40-110">Install manually</span></span>

1. <span data-ttu-id="b1b40-111">Comprobar hello [requisitos previos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="b1b40-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="b1b40-112">Siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para la instalación manual mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1b40-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="b1b40-113">Si prefiere tooinstall desde la línea de comandos de hello, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="b1b40-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="b1b40-114">Instalar desde el servidor de procesos de Hola</span><span class="sxs-lookup"><span data-stu-id="b1b40-114">Install from hello process server</span></span>

<span data-ttu-id="b1b40-115">Si desea la instalación del servicio de movilidad toopush Hola Hola del servidor de procesos cuando se habilita la replicación para una máquina virtual, necesitará una cuenta que puede usarse por Hola proceso servidor tooaccess Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b1b40-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="b1b40-116">cuenta de Hello solo se utiliza para la instalación de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1b40-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="b1b40-117">Debe haber [creado una cuenta](vmware-walkthrough-prepare-vmware.md) que pueda usarse para la instalación de inserción.</span><span class="sxs-lookup"><span data-stu-id="b1b40-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="b1b40-118">A continuación, especificar cuenta de hello que desea toouse al configurar el origen durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b1b40-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="b1b40-119">A continuación, siga [estas instrucciones](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si desea que el servicio de movilidad de hello toopush en máquinas virtuales que ejecutan Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b1b40-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="b1b40-120">Otros métodos</span><span class="sxs-lookup"><span data-stu-id="b1b40-120">Other methods</span></span>

<span data-ttu-id="b1b40-121">Obtenga más información sobre [instalar el servicio de movilidad de hello mediante Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), o mediante [DSC de automatización de Azure](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="b1b40-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b40-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1b40-122">Next steps</span></span>

<span data-ttu-id="b1b40-123">Vaya demasiado[paso 11: habilitar la replicación](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="b1b40-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
