---
title: "seguridad de aaaIntegrate en los diseños arquitectónicos Azure | Documentos de Microsoft"
description: " En este artículo le ayudará a comprender la arquitectura de servicios y aplicaciones de hello en Azure toomake sea más fácil seguridad toointegrate en diseño e implementación. "
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
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="b0762-103">Arquitectura de aplicaciones en Azure</span><span class="sxs-lookup"><span data-stu-id="b0762-103">Application architecture on Azure</span></span>
<span data-ttu-id="b0762-104">toohelp proteger sus soluciones basadas en la nube en Microsoft Azure, una base sólida arquitectura es fundamental.</span><span class="sxs-lookup"><span data-stu-id="b0762-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="b0762-105">De un buen conocimiento de la arquitectura de aplicaciones y servicios pueden sacar provecho arquitectos, diseñadores e implementadores.</span><span class="sxs-lookup"><span data-stu-id="b0762-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="b0762-106">Este conocimiento atractivos le ayuda a comprender todos los componentes de Hola de sus soluciones basadas en la nube y que sea más fácil de seguridad toointegrate en todos los aspectos de su diseño e implementación.</span><span class="sxs-lookup"><span data-stu-id="b0762-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="b0762-107">Nos hemos Hola siguientes toohelp se con su arquitectura investigaciones y diseños de:</span><span class="sxs-lookup"><span data-stu-id="b0762-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="b0762-108">Infografías de arquitectura</span><span class="sxs-lookup"><span data-stu-id="b0762-108">Architectural infographics</span></span>
* <span data-ttu-id="b0762-109">Proyectos de arquitectura</span><span class="sxs-lookup"><span data-stu-id="b0762-109">Architectural blueprints</span></span>
* <span data-ttu-id="b0762-110">Conjunto de símbolos empresariales y de nube</span><span class="sxs-lookup"><span data-stu-id="b0762-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="b0762-111">Plantilla de Visio de proyectos 3D</span><span class="sxs-lookup"><span data-stu-id="b0762-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="b0762-112">Infografías de arquitectura</span><span class="sxs-lookup"><span data-stu-id="b0762-112">Architectural infographics</span></span>
<span data-ttu-id="b0762-113">Microsoft publica varios pósteres e infografías relacionados con la arquitectura.</span><span class="sxs-lookup"><span data-stu-id="b0762-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="b0762-114">Entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="b0762-114">They include:</span></span>

* [<span data-ttu-id="b0762-115">Creación de aplicaciones en la nube para el mundo real</span><span class="sxs-lookup"><span data-stu-id="b0762-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="b0762-116">Escalación de aplicaciones con Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="b0762-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="b0762-117">Proyectos de arquitectura</span><span class="sxs-lookup"><span data-stu-id="b0762-117">Architectural blueprints</span></span>
<span data-ttu-id="b0762-118">Microsoft publica un conjunto de alto nivel [proyectos arquitectónicos](http://aka.ms/azblueprints) que muestra cómo toobuild determinados tipos de sistemas que utilizan productos de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0762-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="b0762-119">Cada proyecto incluye:</span><span class="sxs-lookup"><span data-stu-id="b0762-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="b0762-120">Un archivo plano 2D basado en Visio 2003 que puede descargar y modificar</span><span class="sxs-lookup"><span data-stu-id="b0762-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="b0762-121">Perspectiva 3D coloridos PDF archivo toointroduce Hola plano que no requiere herramientas audiencias técnicas</span><span class="sxs-lookup"><span data-stu-id="b0762-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="b0762-122">Vídeo que le guía a través de la versión de Hola 3D</span><span class="sxs-lookup"><span data-stu-id="b0762-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="b0762-123">Conjunto de símbolos empresariales y de nube</span><span class="sxs-lookup"><span data-stu-id="b0762-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="b0762-124">[Ver Hola Visio y símbolos entrenamiento vídeo](http://aka.ms/CnESymbolsVideo) y, a continuación, [descargar hello en la nube y el símbolo de Enterprise conjunto](http://aka.ms/CnESymbols) toohelp crear materiales técnicos que describen Azure, Windows Server, SQL Server y mucho más.</span><span class="sxs-lookup"><span data-stu-id="b0762-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="b0762-125">Puede utilizar símbolos de hello en diagramas de arquitectura, material de aprendizaje, presentaciones, hojas de datos, infografías, notas del producto y libros de terceros incluso si Hola libreta trenes personas toouse productos de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0762-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="b0762-126">Sin embargo, no están pensados para su uso en interfaces de usuario.</span><span class="sxs-lookup"><span data-stu-id="b0762-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="b0762-127">Plantilla de Visio de proyectos 3D</span><span class="sxs-lookup"><span data-stu-id="b0762-127">3D blueprint Visio template</span></span>
<span data-ttu-id="b0762-128">Hola versiones 3D de hello [planos de la arquitectura de Microsoft](http://aka.ms/azblueprints) se crearon inicialmente en una herramienta de terceros.</span><span class="sxs-lookup"><span data-stu-id="b0762-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="b0762-129">Una nueva plantilla de Visio 2013 (y versiones posteriores) incluida el 5 de agosto de 2015 como parte de un [Curso de certificación de arquitectura de Microsoft distribuido en EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="b0762-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="b0762-130">plantilla de Hello también está disponible fuera de curso Hola.</span><span class="sxs-lookup"><span data-stu-id="b0762-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="b0762-131">[Ver el vídeo de aprendizaje de hello](http://aka.ms/3dBlueprintTemplateVideo) primero para que sepa lo que puede hacer</span><span class="sxs-lookup"><span data-stu-id="b0762-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="b0762-132">Descargar hello [Microsoft plantilla de Visio plano 3d](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="b0762-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="b0762-133">Descargar hello [en la nube y los símbolos de Enterprise](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse con plantilla 3D Hola</span><span class="sxs-lookup"><span data-stu-id="b0762-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
