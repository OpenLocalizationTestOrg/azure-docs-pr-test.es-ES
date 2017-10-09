---
title: "aaaPrepare System Center VMM para Hyper-V replicación tooAzure | Documentos de Microsoft"
description: "Describe cómo servidor de System Center VMM tooprepare para tooAzure de replicación de Hyper-V, con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="e5406-103">Paso 6: Preparar servidores VMM y hosts de Hyper-V tooAzure de replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e5406-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="e5406-104">Después de configurar [componentes de Azure](vmm-to-azure-walkthrough-prepare-azure.md) para la implementación de hello, use instrucciones de hello en este servidores VMM locales de artículo tooprepare y toointeract de hosts de Hyper-V con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e5406-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="e5406-105">Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e5406-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="e5406-106">Preparar los servidores VMM</span><span class="sxs-lookup"><span data-stu-id="e5406-106">Prepare VMM servers</span></span>

- <span data-ttu-id="e5406-107">Necesita al menos un servidor VMM que cumplen los requisitos de compatibilidad de hello para la replicación de Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="e5406-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="e5406-108">Asegúrese de que ha preparado el servidor VMM de Hola para [asignación de red](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="e5406-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="e5406-109">Asegúrese de que ese servidor VMM Hola puede tener acceso a estas direcciones URL</span><span class="sxs-lookup"><span data-stu-id="e5406-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="e5406-110">Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.</span><span class="sxs-lookup"><span data-stu-id="e5406-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="e5406-111">Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="e5406-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="e5406-112">Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).</span><span class="sxs-lookup"><span data-stu-id="e5406-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="e5406-113">Durante la implementación de Site Recovery, también descarga Hola proveedor de Site Recovery e instalarlo en cada servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="e5406-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="e5406-114">servidor VMM de Hello está registrado en hello que del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="e5406-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="e5406-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5406-115">Next steps</span></span>

<span data-ttu-id="e5406-116">Vaya demasiado[paso 7: crear un almacén](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="e5406-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

