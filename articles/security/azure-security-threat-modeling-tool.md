---
title: Microsoft Threat Modeling Tool (Azure) | Microsoft Docs
description: "página principal de Microsoft Threat Modeling Tool, que contiene información acerca de cómo empezar a usar la herramienta, lo que incluye el proceso de modelado de amenazas"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 6e26b0af2a16a872c8e02b736e24019b47ed5780
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="65a24-103">Microsoft Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="65a24-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="65a24-104">Threat Modeling Tool es un elemento básico del Ciclo de vida de desarrollo de seguridad (SDL) de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="65a24-104">The Threat Modeling Tool is a core element of the Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="65a24-105">Permite a los arquitectos de software identificar y mitigar los posibles problemas de seguridad en una fase temprana, cuando son relativamente sencillos y poco costosos de resolver.</span><span class="sxs-lookup"><span data-stu-id="65a24-105">It allows software architects to identify and mitigate potential security issues early, when they are relatively easy and cost-effective to resolve.</span></span> <span data-ttu-id="65a24-106">En consecuencia, reduce en gran medida el costo total de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="65a24-106">As a result, it greatly reduces the total cost of development.</span></span> <span data-ttu-id="65a24-107">Además, hemos diseñado la herramienta pensando en expertos no relacionados con la seguridad, lo que facilita el modelado de amenazas para todos los programadores, ya que se proporcionan instrucciones claras sobre cómo crear y analizar los modelos de amenazas.</span><span class="sxs-lookup"><span data-stu-id="65a24-107">Also, we designed the tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="65a24-108">La herramienta permite a cualquier persona:</span><span class="sxs-lookup"><span data-stu-id="65a24-108">The tool enables anyone to:</span></span>

* <span data-ttu-id="65a24-109">Comunicar el diseño de seguridad de sus sistemas</span><span class="sxs-lookup"><span data-stu-id="65a24-109">Communicate about the security design of their systems</span></span>
* <span data-ttu-id="65a24-110">Analizar los diseños de posibles problemas de seguridad con una metodología probada</span><span class="sxs-lookup"><span data-stu-id="65a24-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="65a24-111">Sugerir y administrar mitigaciones para problemas de seguridad</span><span class="sxs-lookup"><span data-stu-id="65a24-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="65a24-112">Estas son algunas funcionalidades e innovaciones de herramientas, solo por nombrar algunas:</span><span class="sxs-lookup"><span data-stu-id="65a24-112">Here are some tooling capabilities and innovations, just to name a few:</span></span>

* <span data-ttu-id="65a24-113">**Automatización:** instrucciones y comentarios en el dibujo de un modelo.</span><span class="sxs-lookup"><span data-stu-id="65a24-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="65a24-114">**STRIDE por elemento:** análisis guiado de amenazas y mitigaciones.</span><span class="sxs-lookup"><span data-stu-id="65a24-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="65a24-115">**Informes:** actividades de seguridad y de prueba en la fase de comprobación.</span><span class="sxs-lookup"><span data-stu-id="65a24-115">**Reporting:** Security activities and testing in the verification phase</span></span>
* <span data-ttu-id="65a24-116">**Metodología única:** permite a los usuarios visualizar y comprender mejor las amenazas.</span><span class="sxs-lookup"><span data-stu-id="65a24-116">**Unique Methodology:** Enables users to better visualize and understand threats</span></span>
* <span data-ttu-id="65a24-117">**Diseñadas para desarrolladores y centradas en el software:** muchos enfoques están centrados en recursos o atacantes.</span><span class="sxs-lookup"><span data-stu-id="65a24-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="65a24-118">Estamos centrados en el software.</span><span class="sxs-lookup"><span data-stu-id="65a24-118">We are centered on software.</span></span> <span data-ttu-id="65a24-119">Nos basamos en actividades con las que todos los arquitectos y desarrolladores de software están familiarizados, como dibujar imágenes para la arquitectura de su software.</span><span class="sxs-lookup"><span data-stu-id="65a24-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="65a24-120">**Centradas en el análisis de diseño:** el término "modelado de amenazas" puede hacer referencia a un requisito o a una técnica de análisis de diseño.</span><span class="sxs-lookup"><span data-stu-id="65a24-120">**Focused on Design Analysis:** The term "threat modeling" can refer to either a requirements or a design analysis technique.</span></span> <span data-ttu-id="65a24-121">A veces, hace referencia a una compleja combinación de ambas.</span><span class="sxs-lookup"><span data-stu-id="65a24-121">Sometimes, it refers to a complex blend of the two.</span></span> <span data-ttu-id="65a24-122">El enfoque de SDL de Microsoft para el modelado de amenazas es una técnica de análisis de diseño prioritaria.</span><span class="sxs-lookup"><span data-stu-id="65a24-122">The Microsoft SDL approach to threat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="65a24-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65a24-123">Next steps</span></span>

<span data-ttu-id="65a24-124">La tabla siguiente contiene vínculos importantes para ayudarle a comenzar con Threat Modeling Tool:</span><span class="sxs-lookup"><span data-stu-id="65a24-124">The table below contains important links to get you started with the Threat Modeling Tool:</span></span>

| <span data-ttu-id="65a24-125">Paso</span><span class="sxs-lookup"><span data-stu-id="65a24-125">Step</span></span>  | <span data-ttu-id="65a24-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="65a24-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="65a24-127">**1**</span><span class="sxs-lookup"><span data-stu-id="65a24-127">**1**</span></span> | [<span data-ttu-id="65a24-128">Descarga de Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="65a24-128">Download the Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="65a24-129">**2**</span><span class="sxs-lookup"><span data-stu-id="65a24-129">**2**</span></span> | [<span data-ttu-id="65a24-130">Lea nuestra guía de introducción</span><span class="sxs-lookup"><span data-stu-id="65a24-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="65a24-131">**3**</span><span class="sxs-lookup"><span data-stu-id="65a24-131">**3**</span></span> | [<span data-ttu-id="65a24-132">Conozca las características</span><span class="sxs-lookup"><span data-stu-id="65a24-132">Get familiar with the features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="65a24-133">**4**</span><span class="sxs-lookup"><span data-stu-id="65a24-133">**4**</span></span> | [<span data-ttu-id="65a24-134">Obtenga información acerca de las categorías de amenaza generadas</span><span class="sxs-lookup"><span data-stu-id="65a24-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="65a24-135">**5**</span><span class="sxs-lookup"><span data-stu-id="65a24-135">**5**</span></span> | [<span data-ttu-id="65a24-136">Busque las mitigaciones a amenazas generadas</span><span class="sxs-lookup"><span data-stu-id="65a24-136">Find mitigations to generated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="65a24-137">Recursos</span><span class="sxs-lookup"><span data-stu-id="65a24-137">Resources</span></span>

<span data-ttu-id="65a24-138">A continuación encontrará algunos artículos antiguos que siguen siendo pertinentes para el modelado de amenazas de hoy en día:</span><span class="sxs-lookup"><span data-stu-id="65a24-138">Here are a few older articles still relevant to threat modeling today:</span></span>

* [<span data-ttu-id="65a24-139">Artículo sobre la importancia del modelado de amenazas</span><span class="sxs-lookup"><span data-stu-id="65a24-139">Article on the Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="65a24-140">Aprendizaje publicado por Trustworthy Computing</span><span class="sxs-lookup"><span data-stu-id="65a24-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="65a24-141">Consulte lo que han hecho algunos expertos de Threat Modeling Tool:</span><span class="sxs-lookup"><span data-stu-id="65a24-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="65a24-142">Threats Manager</span><span class="sxs-lookup"><span data-stu-id="65a24-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="65a24-143">Blog de seguridad de Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="65a24-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)