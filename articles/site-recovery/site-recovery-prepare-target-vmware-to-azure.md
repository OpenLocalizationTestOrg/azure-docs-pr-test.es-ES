---
title: "Preparación del destino (VMware a Azure) | Microsoft Docs"
description: "En este artículo se describe cómo configurar su entorno de Azure para comenzar a replicar máquinas virtuales de VMware en Azure."
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
ms.openlocfilehash: c84a775564769ddc796aa9d75add019ef1003175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="ac464-103">Preparación del destino (VMware a Azure)</span><span class="sxs-lookup"><span data-stu-id="ac464-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac464-104">VMware a Azure</span><span class="sxs-lookup"><span data-stu-id="ac464-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="ac464-105">Físico a Azure</span><span class="sxs-lookup"><span data-stu-id="ac464-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="ac464-106">En este artículo se describe cómo configurar su entorno de Azure para comenzar a replicar máquinas virtuales de VMware en Azure.</span><span class="sxs-lookup"><span data-stu-id="ac464-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac464-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ac464-107">Prerequisites</span></span>

<span data-ttu-id="ac464-108">En el artículo se da por hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac464-108">The article assumes the following:</span></span>
- <span data-ttu-id="ac464-109">Ha creado un almacén de Recovery Services para proteger sus máquinas virtuales de VMware.</span><span class="sxs-lookup"><span data-stu-id="ac464-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span></span> <span data-ttu-id="ac464-110">Puede crear un almacén de Recovery Services desde [Azure Portal](http://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="ac464-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="ac464-111">Ha [configurado el entorno local](./site-recovery-set-up-vmware-to-azure.md) para replicar máquinas virtuales de VMware en Azure.</span><span class="sxs-lookup"><span data-stu-id="ac464-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="ac464-112">Preparación del destino</span><span class="sxs-lookup"><span data-stu-id="ac464-112">Prepare target</span></span>

<span data-ttu-id="ac464-113">Después de completar el **Paso 1: Selección del objetivo de protección** y el **Paso 2: Preparación del origen**, irá al **Paso 3: Destino**.</span><span class="sxs-lookup"><span data-stu-id="ac464-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Preparación del destino](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="ac464-115">**Suscripción:** En el menú desplegable, seleccione la suscripción en la que desea replicar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ac464-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span></span>
2. <span data-ttu-id="ac464-116">**Modelo de implementación:** Seleccione el modelo de implementación (clásica o Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="ac464-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="ac464-117">Según el modelo de implementación elegido, se ejecuta una validación para asegurarse de que tiene al menos una cuenta de almacenamiento compatible y una red virtual en la conmutación de destino en la que replicar y conmutar por error las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ac464-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span></span>

<span data-ttu-id="ac464-118">Una vez completadas las validaciones correctamente, haga clic en Aceptar para ir al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ac464-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="ac464-119">Si no tiene una cuenta de almacenamiento de Resource Manager compatible o una red virtual, o le gustaría agregar más, puede hacerlo haciendo clic en los botones **+ Cuenta de almacenamiento** o **+ Red** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="ac464-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac464-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac464-120">Next steps</span></span>
<span data-ttu-id="ac464-121">[Configuración de las opciones de replicación](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="ac464-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
