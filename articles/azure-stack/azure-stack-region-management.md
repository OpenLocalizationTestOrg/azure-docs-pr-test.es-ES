---
title: "administración de aaaRegion en la pila de Azure | Documentos de Microsoft"
description: "Introducción a la administración de regiones en Azure Stack."
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="b6248-103">Administración de regiones en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b6248-103">Region management in Azure Stack</span></span>
<span data-ttu-id="b6248-104">Pila de Azure tiene el concepto de Hola de regiones, que son entidades lógicas que consta de los recursos de hardware de Hola que componen la infraestructura de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="b6248-104">Azure Stack has hello concept of regions, which are logical entities comprised of hello hardware resources that make up hello Azure Stack infrastructure.</span></span> <span data-ttu-id="b6248-105">Dentro de la administración de la región, puede buscar todos los recursos que son necesario toosuccessfully funcionan del ciclo de vida de infraestructura de hello pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6248-105">Inside Region management, you can find all resources that are required toosuccessfully operate hello Azure Stack infrastructure lifecycle.</span></span>

<span data-ttu-id="b6248-106">Hola Kit de desarrollo de pila de Azure es una implementación de un único nodo y es igual a una región.</span><span class="sxs-lookup"><span data-stu-id="b6248-106">hello Azure Stack Development Kit is a single-node deployment, and equals one region.</span></span> <span data-ttu-id="b6248-107">Si configura otra instancia del programa Hola Kit de desarrollo de pila de Azure en hardware independiente, esta instancia es una región diferente.</span><span class="sxs-lookup"><span data-stu-id="b6248-107">If you set up another instance of hello Azure Stack Development Kit on separate hardware, this instance is a different region.</span></span>

## <a name="information-available-through-hello-region-management-tile"></a><span data-ttu-id="b6248-108">Información disponible a través del icono de administración de la región de Hola</span><span class="sxs-lookup"><span data-stu-id="b6248-108">Information available through hello Region Management tile</span></span>
<span data-ttu-id="b6248-109">Pila de Azure tiene un conjunto de capacidades de administración de región disponibles en hello **administración región** icono.</span><span class="sxs-lookup"><span data-stu-id="b6248-109">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="b6248-110">Este icono es administrador de la nube de tooa disponible en panel predeterminado de hello en el portal del Administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6248-110">This tile is available tooa cloud administrator on hello default dashboard in hello administrator portal.</span></span> <span data-ttu-id="b6248-111">A través de este icono, puede supervisar y actualizar su región de Azure Stack y sus componentes, que son específicos de cada región.</span><span class="sxs-lookup"><span data-stu-id="b6248-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![icono de administración de región de Hola](media/azure-stack-manage-region/image1.png)

 <span data-ttu-id="b6248-113">Si hace clic en una región en el icono de administración de región de hello, puede tener acceso a Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b6248-113">If you click a region in hello Region management tile, you can access hello following information:</span></span>

  ![Descripción de los paneles en la hoja de administración de región de Hola](media/azure-stack-manage-region/image2.png)

1. <span data-ttu-id="b6248-115">**menú de recursos de Hello**.</span><span class="sxs-lookup"><span data-stu-id="b6248-115">**hello resource menu**.</span></span> <span data-ttu-id="b6248-116">Aquí, puede tener acceso a áreas de administración de infraestructuras específicas y ver y administrar los recursos de inquilino como son las cuentas de almacenamiento y las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="b6248-116">Here, you can access specific infrastructure management areas, and view and manage tenant resources such as storage accounts and virtual networks.</span></span>

2. <span data-ttu-id="b6248-117">**Alertas**.</span><span class="sxs-lookup"><span data-stu-id="b6248-117">**Alerts**.</span></span> <span data-ttu-id="b6248-118">Este icono muestra las alertas de todo el sistema y proporciona detalles sobre cada una.</span><span class="sxs-lookup"><span data-stu-id="b6248-118">This tile lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="b6248-119">**Actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="b6248-119">**Updates**.</span></span> <span data-ttu-id="b6248-120">En este icono, puede ver la versión actual de Hola de su infraestructura de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6248-120">In this tile, you can view hello current version of your Azure Stack infrastructure.</span></span>

4. <span data-ttu-id="b6248-121">**Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="b6248-121">**Resource providers**.</span></span> <span data-ttu-id="b6248-122">Proveedores de recursos es Hola lugar toomanage Hola inquilino la funcionalidad que ofrece Hola componentes necesarios toorun pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6248-122">Resource providers is hello place toomanage hello tenant functionality offered by hello components required toorun Azure Stack.</span></span> <span data-ttu-id="b6248-123">Cada proveedor de recursos viene con una experiencia administrativa.</span><span class="sxs-lookup"><span data-stu-id="b6248-123">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="b6248-124">Esta experiencia puede incluir las alertas de proveedor específico de hello, métricas y otro proveedor de recursos de toohello específico de las capacidades de administración.</span><span class="sxs-lookup"><span data-stu-id="b6248-124">This experience can include alerts for hello specific provider, metrics, and other management capabilities specific toohello resource provider.</span></span>
 
5. <span data-ttu-id="b6248-125">**Infrastructure roles** (Roles de infraestructura).</span><span class="sxs-lookup"><span data-stu-id="b6248-125">**Infrastructure roles**.</span></span> <span data-ttu-id="b6248-126">Los roles de infraestructura son Hola componentes necesarios toorun pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6248-126">Infrastructure roles are hello components necessary toorun Azure Stack.</span></span> <span data-ttu-id="b6248-127">Solo roles de infraestructura de Hola que dependen de las alertas se muestran.</span><span class="sxs-lookup"><span data-stu-id="b6248-127">Only hello infrastructure roles that report alerts are listed.</span></span> <span data-ttu-id="b6248-128">Haciendo clic en un rol, puede ver alertas de hello asociadas con el rol específico de hello e instancias de rol de Hola donde se ejecuta este rol.</span><span class="sxs-lookup"><span data-stu-id="b6248-128">By clicking a role, you can view hello alerts associated with hello specific role and hello role instances where this role is running.</span></span> <span data-ttu-id="b6248-129">Aunque hay Hola capacidad toostart, reiniciar, o cerrar una instancia de rol de infraestructura, realice **no** hacer esto en un entorno de kit de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b6248-129">Although there is hello capability toostart, restart, or shut down an infrastructure role instance, do **not** do this in a development kit environment.</span></span> <span data-ttu-id="b6248-130">Estas opciones están diseñadas únicamente para un entorno de varios nodos, donde hay más de una instancia de rol por rol de infraestructura.</span><span class="sxs-lookup"><span data-stu-id="b6248-130">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="b6248-131">Al reiniciar una instancia de rol (especialmente AzS-Xrp01) en el kit de desarrollo de hello provoca inestabilidad del sistema.</span><span class="sxs-lookup"><span data-stu-id="b6248-131">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6248-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6248-132">Next steps</span></span>
[<span data-ttu-id="b6248-133">Supervisar el estado y las alertas en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b6248-133">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)

[<span data-ttu-id="b6248-134">Administrar las actualizaciones en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b6248-134">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)






