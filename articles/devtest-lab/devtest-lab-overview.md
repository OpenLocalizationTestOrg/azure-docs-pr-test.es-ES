---
title: Acerca de Azure DevTest Labs | Microsoft Docs
description: "Aprenda cómo DevTest Labs puede facilitar la creación, la administración y la supervisión de máquinas virtuales de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="4b40e-103">Acerca de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4b40e-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="4b40e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4b40e-104">Overview</span></span>
<span data-ttu-id="4b40e-105">Los desarrolladores y evaluadores están buscando la manera de resolver los retrasos en la creación y administración de sus entornos trasladándolos a la nube.</span><span class="sxs-lookup"><span data-stu-id="4b40e-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="4b40e-106">Azure soluciona el problema de los retrasos en el entorno y hace posible el autoservicio dentro de una estructura nueva y rentable.</span><span class="sxs-lookup"><span data-stu-id="4b40e-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="4b40e-107">Sin embargo, los desarrolladores y evaluadores necesitan aún dedicar mucho tiempo a la configuración de los entornos que se administran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4b40e-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="4b40e-108">Además, los encargados de la toma de decisiones no tienen claro cómo aprovechar la nube para maximizar sus ahorros sin agregar demasiada sobrecarga al proceso.</span><span class="sxs-lookup"><span data-stu-id="4b40e-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="4b40e-109">Azure DevTest Labs es un servicio que ayuda a los desarrolladores y evaluadores a crear rápidamente entornos de Azure al tiempo que se optimizan los recursos y se controlan los costos.</span><span class="sxs-lookup"><span data-stu-id="4b40e-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="4b40e-110">Puede probar la versión más reciente de la aplicación aprovisionando rápidamente entornos de Windows y Linux mediante plantillas y artefactos reutilizables.</span><span class="sxs-lookup"><span data-stu-id="4b40e-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="4b40e-111">Integre fácilmente la canalización de la implementación con DevTest Labs para aprovisionar entornos a petición.</span><span class="sxs-lookup"><span data-stu-id="4b40e-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="4b40e-112">Escale verticalmente las pruebas de carga mediante el aprovisionamiento de varios agentes de prueba y cree entornos previamente aprovisionados con fines de capacitación y demostración.</span><span class="sxs-lookup"><span data-stu-id="4b40e-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="4b40e-113">DevTest Labs proporciona las siguientes ventajas en la creación, la configuración y la administración de entornos de desarrollador y prueba en la nube</span><span class="sxs-lookup"><span data-stu-id="4b40e-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="4b40e-114">Autoservicio sin preocupaciones</span><span class="sxs-lookup"><span data-stu-id="4b40e-114">Worry-free self-service</span></span>
<span data-ttu-id="4b40e-115">DevTest Labs facilita el control de costos al permitirle definir directivas en el laboratorio, como el número de máquinas virtuales (VM) por usuario y el número de máquinas virtuales por laboratorio.</span><span class="sxs-lookup"><span data-stu-id="4b40e-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="4b40e-116">DevTest Labs también permite crear directivas para apagar e iniciar automáticamente las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4b40e-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="4b40e-117">Obtenga acceso rápidamente al modo "Listo para probar"</span><span class="sxs-lookup"><span data-stu-id="4b40e-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="4b40e-118">DevTest Labs le permite crear entornos ya aprovisionados con todo lo que su equipo necesita para comenzar a desarrollar y probar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4b40e-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="4b40e-119">Basta con notificar los entornos en los que se instaló la última compilación en buen estado de la aplicación y podrá empezar a trabajar de inmediato.</span><span class="sxs-lookup"><span data-stu-id="4b40e-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="4b40e-120">O bien, utilice contenedores para agilizar y simplificar aún más la creación de entornos.</span><span class="sxs-lookup"><span data-stu-id="4b40e-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="4b40e-121">Se crean una vez y se utilizan en todas partes</span><span class="sxs-lookup"><span data-stu-id="4b40e-121">Create once, use everywhere</span></span>
<span data-ttu-id="4b40e-122">Capture y comparta plantillas de entornos y artefactos dentro de su equipo u organización, todo con control de código fuente, para crear entornos de desarrollo y pruebas con facilidad.</span><span class="sxs-lookup"><span data-stu-id="4b40e-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="4b40e-123">Se integra con la cadena de herramientas existente</span><span class="sxs-lookup"><span data-stu-id="4b40e-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="4b40e-124">Aproveche complementos ya creados o nuestra API para aprovisionar entornos de desarrollo y pruebas directamente desde la herramienta de integración continua (CI), el entorno de desarrollo integrado (IDE) o la canalización de entrega de versiones que prefiera.</span><span class="sxs-lookup"><span data-stu-id="4b40e-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="4b40e-125">También puede utilizar nuestra completa herramienta de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="4b40e-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4b40e-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b40e-126">Next steps</span></span>
[<span data-ttu-id="4b40e-127">Conceptos de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4b40e-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

