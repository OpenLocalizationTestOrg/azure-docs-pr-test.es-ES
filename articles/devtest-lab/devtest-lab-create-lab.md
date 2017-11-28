---
title: "aaaCreate un laboratorio de prácticas de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Creación de un laboratorio en Azure DevTest Labs para máquinas virtuales"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="302fd-103">Creación de un laboratorio con Laboratorios de desarrollo y pruebas de Azure</span><span class="sxs-lookup"><span data-stu-id="302fd-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="302fd-104">Una práctica de laboratorios de desarrollo y pruebas de Azure es la infraestructura de Hola que abarca el proceso de un grupo de recursos, como máquinas virtuales (VM), que permite una mejor administrar esos recursos especificando los límites y cuotas.</span><span class="sxs-lookup"><span data-stu-id="302fd-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="302fd-105">Este artículo le guiará por el proceso de Hola de creación de un laboratorio mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="302fd-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="302fd-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="302fd-106">Prerequisites</span></span>
<span data-ttu-id="302fd-107">toocreate un laboratorio, debe:</span><span class="sxs-lookup"><span data-stu-id="302fd-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="302fd-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="302fd-108">An Azure subscription.</span></span> <span data-ttu-id="302fd-109">toolearn acerca de las opciones de compra de Azure, consulte [cómo toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) o [un mes evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="302fd-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="302fd-110">Debe ser propietario de Hola de laboratorio de hello suscripción toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="302fd-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="302fd-111">Pasos toocreate un laboratorio de prácticas de desarrollo y pruebas de Azure</span><span class="sxs-lookup"><span data-stu-id="302fd-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="302fd-112">Hola siguientes pasos muestra cómo toouse Hola toocreate portal Azure un laboratorio de prácticas de desarrollo y pruebas de Azure.</span><span class="sxs-lookup"><span data-stu-id="302fd-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="302fd-113">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="302fd-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="302fd-114">En menú principal de hello en el lado izquierdo de hello, seleccione **más servicios** (final Hola de hello lista).</span><span class="sxs-lookup"><span data-stu-id="302fd-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Opción del menú Más servicios](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="302fd-116">En lista de hello de servicios disponibles, **laboratorios de desarrollo y pruebas**.</span><span class="sxs-lookup"><span data-stu-id="302fd-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="302fd-117">En hello **laboratorios de desarrollo y pruebas** hoja, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="302fd-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Incorporación de un laboratorio](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="302fd-119">En hello **crear un laboratorio de desarrollo y pruebas** hoja:</span><span class="sxs-lookup"><span data-stu-id="302fd-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="302fd-120">Escriba un **nombre de laboratorio** para laboratorio nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="302fd-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="302fd-121">Seleccione hello **suscripción** tooassociate con laboratorio Hola.</span><span class="sxs-lookup"><span data-stu-id="302fd-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="302fd-122">Seleccione un **ubicación** en el laboratorio de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="302fd-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="302fd-123">Seleccione **apagado automático** toospecify si desea tooenable - y definir parámetros de Hola para - Hola automática apagar de máquinas virtuales del laboratorio Hola todos los.</span><span class="sxs-lookup"><span data-stu-id="302fd-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="302fd-124">Hello apagado automático es principalmente un ahorro de costos característica mediante el cual puede especificar cuándo desea Hola VM tooautomatically apagarse.</span><span class="sxs-lookup"><span data-stu-id="302fd-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="302fd-125">Puede cambiar la configuración de cierre automáticamente después de crear el laboratorio de hello siguiendo los pasos de Hola que se describen en el artículo de hello, [administrar todas las directivas para un laboratorio de prácticas de desarrollo y pruebas de Azure](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="302fd-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="302fd-126">Seleccione **tooDashboard Pin** si desea un acceso directo de hello tooappear de laboratorio en el panel del portal Hola.</span><span class="sxs-lookup"><span data-stu-id="302fd-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="302fd-127">Seleccione **opciones de automatización** tooget Azure Resource Manager plantillas para la automatización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="302fd-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="302fd-128">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="302fd-128">Select **Create**.</span></span> <span data-ttu-id="302fd-129">Después de seleccionar **crear**, hello **laboratorios de desarrollo y pruebas** muestra hoja.</span><span class="sxs-lookup"><span data-stu-id="302fd-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="302fd-130">Puede supervisar Hola estado del proceso de creación de laboratorio de hello, inspeccionando hello **notificaciones** área.</span><span class="sxs-lookup"><span data-stu-id="302fd-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="302fd-131">Una vez completado, actualización Hola página toosee Hola recién creado del laboratorio lista Hola de laboratorios.</span><span class="sxs-lookup"><span data-stu-id="302fd-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Creación de una hoja de laboratorio](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="302fd-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="302fd-133">Next steps</span></span>
<span data-ttu-id="302fd-134">Una vez que haya creado el laboratorio, incluimos algunos tooconsider de pasos siguiente:</span><span class="sxs-lookup"><span data-stu-id="302fd-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="302fd-135">[Laboratorio de acceso seguro tooa](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="302fd-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="302fd-136">[Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)</span><span class="sxs-lookup"><span data-stu-id="302fd-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="302fd-137">[Creación de una plantilla de laboratorio](devtest-lab-create-template.md)</span><span class="sxs-lookup"><span data-stu-id="302fd-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="302fd-138">[Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)</span><span class="sxs-lookup"><span data-stu-id="302fd-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="302fd-139">[Agregar una máquina virtual con el laboratorio de artefactos tooa](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="302fd-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

