---
title: "Integración de la seguridad en diseños de arquitectura de Azure | Microsoft Docs"
description: " Este artículo le ayudará a comprender la arquitectura de aplicaciones y servicios en Azure para facilitar la integración de características de seguridad en el diseño y la implementación. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 91e46d690d3e7c298bc3b4020cc383ca99c43c4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="2ebda-103">Arquitectura de aplicaciones en Azure</span><span class="sxs-lookup"><span data-stu-id="2ebda-103">Application architecture on Azure</span></span>
<span data-ttu-id="2ebda-104">Para ayudar a proteger sus soluciones basadas en la nube en Microsoft Azure, es esencial contar con unos sólidos fundamentos en materia de arquitectura.</span><span class="sxs-lookup"><span data-stu-id="2ebda-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="2ebda-105">De un buen conocimiento de la arquitectura de aplicaciones y servicios pueden sacar provecho arquitectos, diseñadores e implementadores.</span><span class="sxs-lookup"><span data-stu-id="2ebda-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="2ebda-106">Estos conocimientos básicos lo ayudarán a comprender todos los componentes de sus soluciones basadas en la nube y facilitarán la integración de características de seguridad en todos los aspectos del diseño y la implementación.</span><span class="sxs-lookup"><span data-stu-id="2ebda-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="2ebda-107">Los siguientes recursos pueden resultarle útiles para sus investigaciones y diseños de arquitectura:</span><span class="sxs-lookup"><span data-stu-id="2ebda-107">We have the following to help you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="2ebda-108">Infografías de arquitectura</span><span class="sxs-lookup"><span data-stu-id="2ebda-108">Architectural infographics</span></span>
* <span data-ttu-id="2ebda-109">Proyectos de arquitectura</span><span class="sxs-lookup"><span data-stu-id="2ebda-109">Architectural blueprints</span></span>
* <span data-ttu-id="2ebda-110">Conjunto de símbolos empresariales y de nube</span><span class="sxs-lookup"><span data-stu-id="2ebda-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="2ebda-111">Plantilla de Visio de proyectos 3D</span><span class="sxs-lookup"><span data-stu-id="2ebda-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="2ebda-112">Infografías de arquitectura</span><span class="sxs-lookup"><span data-stu-id="2ebda-112">Architectural infographics</span></span>
<span data-ttu-id="2ebda-113">Microsoft publica varios pósteres e infografías relacionados con la arquitectura.</span><span class="sxs-lookup"><span data-stu-id="2ebda-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="2ebda-114">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="2ebda-114">They include:</span></span>

* [<span data-ttu-id="2ebda-115">Creación de aplicaciones en la nube para el mundo real</span><span class="sxs-lookup"><span data-stu-id="2ebda-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="2ebda-116">Escalación de aplicaciones con Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="2ebda-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="2ebda-117">Proyectos de arquitectura</span><span class="sxs-lookup"><span data-stu-id="2ebda-117">Architectural blueprints</span></span>
<span data-ttu-id="2ebda-118">Microsoft publica un conjunto de [proyectos de arquitectura](http://aka.ms/azblueprints) de alto nivel que muestran cómo crear tipos específicos de sistemas con productos de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2ebda-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="2ebda-119">Cada proyecto incluye:</span><span class="sxs-lookup"><span data-stu-id="2ebda-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="2ebda-120">Un archivo plano 2D basado en Visio 2003 que puede descargar y modificar</span><span class="sxs-lookup"><span data-stu-id="2ebda-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="2ebda-121">Un colorido archivo PDF en perspectiva 3D para presentar el proyecto a un público menos técnico</span><span class="sxs-lookup"><span data-stu-id="2ebda-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span></span>
* <span data-ttu-id="2ebda-122">Un vídeo que le guía a través de la versión 3D</span><span class="sxs-lookup"><span data-stu-id="2ebda-122">Video that walks through the 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="2ebda-123">Conjunto de símbolos empresariales y de nube</span><span class="sxs-lookup"><span data-stu-id="2ebda-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="2ebda-124">[Vea el vídeo de entrenamiento de Visio y de los símbolos](http://aka.ms/CnESymbolsVideo), y [descargue el conjunto de símbolos empresariales y en la nube](http://aka.ms/CnESymbols) para ayudarle a crear materiales técnicos que describen Azure, Windows Server, SQL Server, etc.</span><span class="sxs-lookup"><span data-stu-id="2ebda-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="2ebda-125">Puede utilizar los símbolos en diagramas de arquitectura, materiales de entrenamiento, presentaciones, hojas de datos, infografía, notas del producto e incluso en libros de terceros si estos entrenan a personas para usar los productos de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2ebda-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span></span> <span data-ttu-id="2ebda-126">Sin embargo, no están pensados para su uso en interfaces de usuario.</span><span class="sxs-lookup"><span data-stu-id="2ebda-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="2ebda-127">Plantilla de Visio de proyectos 3D</span><span class="sxs-lookup"><span data-stu-id="2ebda-127">3D blueprint Visio template</span></span>
<span data-ttu-id="2ebda-128">Las versiones 3D de los [Proyectos de arquitectura de Microsoft](http://aka.ms/azblueprints) se crearon inicialmente en una herramienta de terceros.</span><span class="sxs-lookup"><span data-stu-id="2ebda-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="2ebda-129">Una nueva plantilla de Visio 2013 (y versiones posteriores) incluida el 5 de agosto de 2015 como parte de un [Curso de certificación de arquitectura de Microsoft distribuido en EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="2ebda-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="2ebda-130">La plantilla también está disponible fuera del curso.</span><span class="sxs-lookup"><span data-stu-id="2ebda-130">The template is also available outside the course.</span></span>

* <span data-ttu-id="2ebda-131">[Ver el vídeo de entrenamiento](http://aka.ms/3dBlueprintTemplateVideo) primero para saber lo que puede hacer</span><span class="sxs-lookup"><span data-stu-id="2ebda-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="2ebda-132">Descargar la [plantilla de Visio de proyectos 3D de Microsoft](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="2ebda-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="2ebda-133">Descargar los [símbolos de nube y empresariales](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) para utilizar con la plantilla 3D</span><span class="sxs-lookup"><span data-stu-id="2ebda-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span></span>
