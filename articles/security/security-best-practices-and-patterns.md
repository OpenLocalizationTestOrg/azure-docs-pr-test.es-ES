---
title: Patrones y procedimientos recomendados de seguridad en Azure | Microsoft Docs
description: "El artículo proporciona una introducción acerca de los patrones y procedimientos recomendados de seguridad de Azure, así como una lista exclusiva de procedimientos recomendados de seguridad para los distintos recursos de Azure."
services: azure-security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1cbbf8dc-ea94-4a7e-8fa0-c2cb198956c5
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: terrylan
ms.openlocfilehash: 1cc0d2d1e9a62ff8531f963413ff573713d508ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="f917c-103">Patrones y procedimientos recomendados de seguridad en Azure</span><span class="sxs-lookup"><span data-stu-id="f917c-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="f917c-104">Actualmente se pueden consultar los siguientes artículos de patrones y procedimientos recomendados de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="f917c-104">We currently have the following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="f917c-105">Asegúrese de visitar este sitio periódicamente para estar al tanto de las novedades de nuestra lista actualizada de patrones y procedimientos recomendados de seguridad de Azure:</span><span class="sxs-lookup"><span data-stu-id="f917c-105">Make sure to visit this site periodically to see updates to our growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="f917c-106">Procedimientos recomendados de seguridad de la red de Azure</span><span class="sxs-lookup"><span data-stu-id="f917c-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="f917c-107">Procedimientos recomendados de cifrado y seguridad de datos en Azure</span><span class="sxs-lookup"><span data-stu-id="f917c-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="f917c-108">Procedimientos recomendados para la administración de identidades y la seguridad del control de acceso en Azure</span><span class="sxs-lookup"><span data-stu-id="f917c-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="f917c-109">Procedimientos recomendados de seguridad de Internet de las cosas</span><span class="sxs-lookup"><span data-stu-id="f917c-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="f917c-110">[Prácticas recomendadas de seguridad de IaaS de Azure] (azure-security-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="f917c-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="f917c-111">Servicios en la nube de Microsoft y seguridad de red</span><span class="sxs-lookup"><span data-stu-id="f917c-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="f917c-112">Implementing a secure hybrid network architecture in Azure (Implementación de una arquitectura de red híbrida segura en Azure)</span><span class="sxs-lookup"><span data-stu-id="f917c-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="f917c-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="f917c-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="f917c-114">Azure ofrece una plataforma segura en la que puede crear sus soluciones.</span><span class="sxs-lookup"><span data-stu-id="f917c-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="f917c-115">También proporcionamos servicios y tecnologías para proteger sus soluciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f917c-115">We also provide services and technologies to make your solutions on Azure more secure.</span></span> <span data-ttu-id="f917c-116">Debido a las numerosas opciones disponibles, muchos usuarios han expresado su interés en los procedimientos recomendados y patrones que Microsoft podría recomendar para mejorar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="f917c-116">Because of the many options available to you, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="f917c-117">Somos conscientes de su interés y por ello hemos creado una serie de documentos que describen las acciones que puede realizar dentro de un contexto adecuado y que, mejorarán la seguridad de las implementaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f917c-117">We understand your interest and have created a collection of documents that describe things you can do, given the right context, to improve the security of Azure deployments.</span></span>

<span data-ttu-id="f917c-118">En estos artículos se aborda una serie de procedimientos recomendados y patrones útiles para temas determinados.</span><span class="sxs-lookup"><span data-stu-id="f917c-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="f917c-119">Estos procedimientos recomendados y patrones se han diseñado a partir de nuestras experiencias con estas tecnologías y las experiencias de clientes como usted.</span><span class="sxs-lookup"><span data-stu-id="f917c-119">These best practices and patterns are derived from our experiences with these technologies and the experiences of customers like yourself.</span></span>

<span data-ttu-id="f917c-120">Para cada procedimiento recomendado, explicaremos:</span><span class="sxs-lookup"><span data-stu-id="f917c-120">For each best practice we strive to explain:</span></span>

* <span data-ttu-id="f917c-121">Qué es el procedimiento recomendado</span><span class="sxs-lookup"><span data-stu-id="f917c-121">What the best practice is</span></span>
* <span data-ttu-id="f917c-122">Por qué le conviene habilitar este procedimiento recomendado</span><span class="sxs-lookup"><span data-stu-id="f917c-122">Why you want to enable that best practice</span></span>
* <span data-ttu-id="f917c-123">Cuál podría ser el resultado si no habilita el procedimiento recomendado</span><span class="sxs-lookup"><span data-stu-id="f917c-123">What might be the result if you fail to enable the best practice</span></span>
* <span data-ttu-id="f917c-124">Alternativas posibles al procedimiento recomendado</span><span class="sxs-lookup"><span data-stu-id="f917c-124">Possible alternatives to the best practice</span></span>
* <span data-ttu-id="f917c-125">Cómo aprender a habilitar el procedimiento recomendado</span><span class="sxs-lookup"><span data-stu-id="f917c-125">How you can learn to enable the best practice</span></span>

<span data-ttu-id="f917c-126">Esperamos incluir muchos más artículos sobre arquitectura de seguridad de Azure y procedimientos recomendados.</span><span class="sxs-lookup"><span data-stu-id="f917c-126">We look forward to including many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="f917c-127">Si hay algún tema que le gustaría que incluyéramos, háganoslo saber en el área de discusión en la parte inferior de esta página.</span><span class="sxs-lookup"><span data-stu-id="f917c-127">If there are topics that you'd like us to include, let us know in the discussion area at the bottom of this page.</span></span>
