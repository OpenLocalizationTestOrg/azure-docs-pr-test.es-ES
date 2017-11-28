---
title: "Preparar el destino (tooAzure físico) | Documentos de Microsoft"
description: "Este artículo se describe cómo tooprepare su toostart de entorno de Azure replicar servidores físicos que ejecutan tooAzure de Windows o Linux."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="abef3-103">Preparar el destino (tooAzure de VMware)</span><span class="sxs-lookup"><span data-stu-id="abef3-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abef3-104">TooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="abef3-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="abef3-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="abef3-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="abef3-106">Este artículo se describe cómo tooprepare su toostart de entorno de Azure replicar servidores físicos (x 64) con Windows o Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="abef3-106">This article describes how tooprepare your Azure environment toostart replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abef3-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="abef3-107">Prerequisites</span></span>

<span data-ttu-id="abef3-108">artículo de Hello supone siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="abef3-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="abef3-109">Ha creado un tooprotect de almacén de servicios de recuperación de los servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="abef3-109">You have created a Recovery Services Vault tooprotect your physical servers.</span></span> <span data-ttu-id="abef3-110">Puede crear un almacén de servicios de recuperación de hello [portal de Azure](http://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="abef3-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="abef3-111">Tiene [configurar su entorno local](./site-recovery-set-up-physical-to-azure.md) tooreplicate tooAzure de servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="abef3-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) tooreplicate physical servers tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="abef3-112">Preparación del destino</span><span class="sxs-lookup"><span data-stu-id="abef3-112">Prepare target</span></span>

<span data-ttu-id="abef3-113">Después de completar hello **objetivo de protección de paso 1:Select** y **paso 2: preparar origen**, se toman demasiado**paso 3: destino**</span><span class="sxs-lookup"><span data-stu-id="abef3-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Preparación del destino](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="abef3-115">**Suscripción:** de hello menú desplegable, seleccione Hola suscripción que quiere tooreplicate sus servidores físicos a.</span><span class="sxs-lookup"><span data-stu-id="abef3-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your physical servers to.</span></span>
2. <span data-ttu-id="abef3-116">**Modelo de implementación:** modelo de implementación de hello seleccione (Classic o administrador de recursos)</span><span class="sxs-lookup"><span data-stu-id="abef3-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="abef3-117">En función de hello elegido el modelo de implementación, una validación se ejecuta tooensure que tienen al menos una cuenta de almacenamiento compatibles y la red virtual en tooreplicate de suscripción de destino de Hola y de conmutación por error de los servidores físicos para.</span><span class="sxs-lookup"><span data-stu-id="abef3-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your physical servers to.</span></span>

<span data-ttu-id="abef3-118">Una vez validaciones de Hola se completan correctamente, haga clic en Aceptar toogo toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="abef3-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="abef3-119">Si no tiene una cuenta de almacenamiento compatible con el Administrador de recursos o la red virtual, o quiere que tooadd más, puede hacerlo haciendo clic en hello **+ cuenta de almacenamiento** o **+ red** botones en la parte superior de Hola Hola hoja.</span><span class="sxs-lookup"><span data-stu-id="abef3-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abef3-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abef3-120">Next steps</span></span>
<span data-ttu-id="abef3-121">[Configuración de las opciones de replicación](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="abef3-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
