---
title: "Preparar los hosts de Hyper-V (sin System Center VMM) para la replicación en Azure | Microsoft Docs"
description: "Describe cómo preparar los hosts de Hyper-V para la replicación en Azure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="4fb57-103">Paso 6: preparación de los hosts de Hyper-V para la replicación en Azure</span><span class="sxs-lookup"><span data-stu-id="4fb57-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="4fb57-104">Siga las instrucciones de este artículo para preparar los hosts de Hyper-V local para interactuar con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4fb57-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="4fb57-105">Cuando haya terminado de leer este artículo, publique cualquier comentario o pregunta que tenga en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4fb57-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="4fb57-106">Preparar los hosts</span><span class="sxs-lookup"><span data-stu-id="4fb57-106">Prepare hosts</span></span>

- <span data-ttu-id="4fb57-107">Asegúrese de que los hosts de Hyper-V cumplen los [requisitos previos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="4fb57-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="4fb57-108">Asegúrese de que los hosts pueden acceder a las direcciones URL necesarias:</span><span class="sxs-lookup"><span data-stu-id="4fb57-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="4fb57-109">Si tiene reglas de firewall basadas en direcciones IP, asegúrese de que permitan la comunicación con Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb57-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="4fb57-110">Permita los [intervalos IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y el puerto HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="4fb57-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="4fb57-111">Permita los intervalos de direcciones IP correspondientes a la región de Azure de su suscripción y del oeste de EE. UU. (se usan para Access Control y para Identity Management).</span><span class="sxs-lookup"><span data-stu-id="4fb57-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="4fb57-112">Durante la implementación de Site Recovery, se agregan hosts de Hyper-V que contienen las máquinas virtuales que desea replicar en un sitio de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4fb57-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="4fb57-113">El proveedor de Site Recovery y el agente de Recovery Services se instalan en cada host.</span><span class="sxs-lookup"><span data-stu-id="4fb57-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="4fb57-114">Se registra el sitio de Hyper-V en el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4fb57-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fb57-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4fb57-115">Next steps</span></span>

<span data-ttu-id="4fb57-116">Vaya al [paso 7: Creación de un almacén](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="4fb57-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

