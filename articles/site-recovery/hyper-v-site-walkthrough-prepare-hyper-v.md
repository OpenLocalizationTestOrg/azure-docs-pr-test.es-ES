---
title: "hospeda aaaPrepare Hyper-V (sin System Center VMM) para la replicación tooAzure | Documentos de Microsoft"
description: "Describe cómo se hospeda tooprepare Hyper-V para tooAzure de replicación mediante Azure Site Recovery"
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
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="44330-103">Paso 6: Preparar los hosts de Hyper-V tooAzure de replicación</span><span class="sxs-lookup"><span data-stu-id="44330-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="44330-104">Use las instrucciones de hello en este artículo tooprepare toointeract de hosts de Hyper-V con Azure Site Recovery en local.</span><span class="sxs-lookup"><span data-stu-id="44330-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="44330-105">Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="44330-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="44330-106">Preparar los hosts</span><span class="sxs-lookup"><span data-stu-id="44330-106">Prepare hosts</span></span>

- <span data-ttu-id="44330-107">Asegúrese de que los hosts de Hyper-V de hello cumplen hello [requisitos previos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="44330-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="44330-108">Asegúrese de que Hola hosts pueden obtener acceso a direcciones URL de hello necesario:</span><span class="sxs-lookup"><span data-stu-id="44330-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="44330-109">Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.</span><span class="sxs-lookup"><span data-stu-id="44330-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="44330-110">Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="44330-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="44330-111">Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).</span><span class="sxs-lookup"><span data-stu-id="44330-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="44330-112">Durante la implementación de Site Recovery, agregar hosts de Hyper-V que contienen máquinas virtuales que desea que el sitio de Hyper-V tooa tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="44330-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="44330-113">Hola proveedor de Site Recovery y el agente de servicios de recuperación se instalan en cada host.</span><span class="sxs-lookup"><span data-stu-id="44330-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="44330-114">sitio de Hello Hyper-V está registrado en hello que del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="44330-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44330-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44330-115">Next steps</span></span>

<span data-ttu-id="44330-116">Vaya demasiado[paso 7: crear un almacén](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="44330-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

