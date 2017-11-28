---
title: aaaMicrosoft herramienta de modelado de amenazas - Azure | Documentos de Microsoft
description: "página principal de Microsoft amenaza para la herramienta de modelado, que contiene información sobre cómo empezar a usar la herramienta de hello, incluidos el proceso de modelo de amenazas Hola Hola"
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
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="aa4b0-103">Microsoft Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="aa4b0-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="aa4b0-104">Hola herramienta de modelado de amenazas es un elemento básico del saludo del ciclo de vida de desarrollo de seguridad (SDL) de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="aa4b0-105">Permite que el software arquitectos tooidentify y mitigar los posibles problemas de seguridad al principio, cuando están tooresolve relativamente sencilla y rentable.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="aa4b0-106">Como resultado, reduce en gran medida el costo total de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="aa4b0-107">Además, se han diseñado herramienta Hola con expertos en seguridad no en mente, facilitar el modelado de amenazas para todos los programadores al proporcionar instrucciones claras sobre cómo crear y analizar los modelos de amenazas.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="aa4b0-108">herramienta de Hello permite que cualquier persona:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="aa4b0-109">Comunicar la existencia de diseño de seguridad de Hola de sus sistemas</span><span class="sxs-lookup"><span data-stu-id="aa4b0-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="aa4b0-110">Analizar los diseños de posibles problemas de seguridad con una metodología probada</span><span class="sxs-lookup"><span data-stu-id="aa4b0-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="aa4b0-111">Sugerir y administrar mitigaciones para problemas de seguridad</span><span class="sxs-lookup"><span data-stu-id="aa4b0-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="aa4b0-112">Estas son algunas funcionalidades de herramientas y las innovaciones, simplemente tooname algunos:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="aa4b0-113">**Automatización:** instrucciones y comentarios en el dibujo de un modelo.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="aa4b0-114">**STRIDE por elemento:** análisis guiado de amenazas y mitigaciones.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="aa4b0-115">**Informes:** actividades de seguridad y de prueba en la fase de comprobación de Hola</span><span class="sxs-lookup"><span data-stu-id="aa4b0-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="aa4b0-116">**Metodología única:** toobetter de usuarios permite visualizar y comprender las amenazas</span><span class="sxs-lookup"><span data-stu-id="aa4b0-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="aa4b0-117">**Diseñadas para desarrolladores y centradas en el software:** muchos enfoques están centrados en recursos o atacantes.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="aa4b0-118">Estamos centrados en el software.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-118">We are centered on software.</span></span> <span data-ttu-id="aa4b0-119">Nos basamos en actividades con las que todos los arquitectos y desarrolladores de software están familiarizados, como dibujar imágenes para la arquitectura de su software.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="aa4b0-120">**Se centra en el análisis de diseño:** Hola término "modelo de amenazas" puede hacer referencia tooeither requisitos o una técnica de análisis de diseño.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="aa4b0-121">A veces, hace referencia tooa blend complejas de hello dos.</span><span class="sxs-lookup"><span data-stu-id="aa4b0-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="aa4b0-122">modelado de toothreat de enfoque de Hello SDL de Microsoft es una técnica de análisis de diseño tiene el foco</span><span class="sxs-lookup"><span data-stu-id="aa4b0-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4b0-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aa4b0-123">Next steps</span></span>

<span data-ttu-id="aa4b0-124">tabla de Hello siguiente contiene tooget vínculos importantes que se partió Hola herramienta de modelado de amenazas:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="aa4b0-125">Paso</span><span class="sxs-lookup"><span data-stu-id="aa4b0-125">Step</span></span>  | <span data-ttu-id="aa4b0-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="aa4b0-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="aa4b0-127">**1**</span><span class="sxs-lookup"><span data-stu-id="aa4b0-127">**1**</span></span> | [<span data-ttu-id="aa4b0-128">Descargar la herramienta de modelado de amenazas de Hola</span><span class="sxs-lookup"><span data-stu-id="aa4b0-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="aa4b0-129">**2**</span><span class="sxs-lookup"><span data-stu-id="aa4b0-129">**2**</span></span> | [<span data-ttu-id="aa4b0-130">Lea nuestra guía de introducción</span><span class="sxs-lookup"><span data-stu-id="aa4b0-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="aa4b0-131">**3**</span><span class="sxs-lookup"><span data-stu-id="aa4b0-131">**3**</span></span> | [<span data-ttu-id="aa4b0-132">Familiarizarse con las características de Hola</span><span class="sxs-lookup"><span data-stu-id="aa4b0-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="aa4b0-133">**4**</span><span class="sxs-lookup"><span data-stu-id="aa4b0-133">**4**</span></span> | [<span data-ttu-id="aa4b0-134">Obtenga información acerca de las categorías de amenaza generadas</span><span class="sxs-lookup"><span data-stu-id="aa4b0-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="aa4b0-135">**5**</span><span class="sxs-lookup"><span data-stu-id="aa4b0-135">**5**</span></span> | [<span data-ttu-id="aa4b0-136">Buscar las mitigaciones toogenerated amenazas</span><span class="sxs-lookup"><span data-stu-id="aa4b0-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="aa4b0-137">Recursos</span><span class="sxs-lookup"><span data-stu-id="aa4b0-137">Resources</span></span>

<span data-ttu-id="aa4b0-138">Estas son algunas anteriores artículos toothreat siendo pertinente modelado hoy en día:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="aa4b0-139">Artículo en hello importancia del modelo de amenazas</span><span class="sxs-lookup"><span data-stu-id="aa4b0-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="aa4b0-140">Aprendizaje publicado por Trustworthy Computing</span><span class="sxs-lookup"><span data-stu-id="aa4b0-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="aa4b0-141">Consulte lo que han hecho algunos expertos de Threat Modeling Tool:</span><span class="sxs-lookup"><span data-stu-id="aa4b0-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="aa4b0-142">Threats Manager</span><span class="sxs-lookup"><span data-stu-id="aa4b0-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="aa4b0-143">Blog de seguridad de Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="aa4b0-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)