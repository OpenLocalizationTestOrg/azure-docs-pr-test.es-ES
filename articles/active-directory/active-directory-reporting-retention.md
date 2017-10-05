---
title: "Directivas de retención de informes de Azure Active Directory | Microsoft Docs"
description: "Directivas de retención de datos de informes en Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="c16eb-103">Directivas de retención de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c16eb-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="c16eb-104">Este tema proporciona respuestas a las preguntas más frecuentes en relación a la retención de datos de los distintos informes de actividad de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c16eb-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="c16eb-105">**P: ¿Cómo puede empezar la recopilación de datos de actividad?**</span><span class="sxs-lookup"><span data-stu-id="c16eb-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="c16eb-106">**R:**</span><span class="sxs-lookup"><span data-stu-id="c16eb-106">**A:**</span></span>

| <span data-ttu-id="c16eb-107">Edición de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c16eb-107">Azure AD Edition</span></span> | <span data-ttu-id="c16eb-108">Inicio de la recopilación</span><span class="sxs-lookup"><span data-stu-id="c16eb-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="c16eb-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="c16eb-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="c16eb-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="c16eb-110">Azure AD Premium P2</span></span> | <span data-ttu-id="c16eb-111">Al suscribirse a una suscripción</span><span class="sxs-lookup"><span data-stu-id="c16eb-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="c16eb-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="c16eb-112">Azure AD Free</span></span> | <span data-ttu-id="c16eb-113">La primera vez que abra la [hoja de Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) o use las [API de informes](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="c16eb-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="c16eb-114">**P: ¿Cuándo estarán disponibles los datos de actividad en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="c16eb-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="c16eb-115">**R:**</span><span class="sxs-lookup"><span data-stu-id="c16eb-115">**A:**</span></span>

- <span data-ttu-id="c16eb-116">**Inmediatamente**: si ya ha estado trabajando con informes en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c16eb-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="c16eb-117">**Dentro de 2 horas**: si no ha activado la generación de informes en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c16eb-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="c16eb-118">**P: ¿Cómo puede empezar la recopilación de señales de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="c16eb-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="c16eb-119">**R:** En el caso de las señales de seguridad, el proceso de recopilación se inicia cuando decide usar Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="c16eb-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="c16eb-120">**P: ¿Durante cuánto tiempo se almacenan los datos recopilados?**</span><span class="sxs-lookup"><span data-stu-id="c16eb-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="c16eb-121">**R:**</span><span class="sxs-lookup"><span data-stu-id="c16eb-121">**A:**</span></span>

<span data-ttu-id="c16eb-122">**Informes de actividad**</span><span class="sxs-lookup"><span data-stu-id="c16eb-122">**Activity reports**</span></span>    

| <span data-ttu-id="c16eb-123">Informe</span><span class="sxs-lookup"><span data-stu-id="c16eb-123">Report</span></span>                 | <span data-ttu-id="c16eb-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="c16eb-124">Azure AD Free</span></span> | <span data-ttu-id="c16eb-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="c16eb-125">Azure AD Premium P1</span></span> | <span data-ttu-id="c16eb-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="c16eb-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="c16eb-127">Auditoría de directorio</span><span class="sxs-lookup"><span data-stu-id="c16eb-127">Directory Audit</span></span>        | <span data-ttu-id="c16eb-128">7 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-128">7 days</span></span>        | <span data-ttu-id="c16eb-129">30 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-129">30 days</span></span>             | <span data-ttu-id="c16eb-130">30 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-130">30 days</span></span>             |
| <span data-ttu-id="c16eb-131">Actividad de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="c16eb-131">Sign-in Activity</span></span>       | <span data-ttu-id="c16eb-132">7 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-132">7 days</span></span>        | <span data-ttu-id="c16eb-133">30 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-133">30 days</span></span>             | <span data-ttu-id="c16eb-134">30 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-134">30 days</span></span>             |

<span data-ttu-id="c16eb-135">**Señales de seguridad**</span><span class="sxs-lookup"><span data-stu-id="c16eb-135">**Security Signals**</span></span>

| <span data-ttu-id="c16eb-136">Informe</span><span class="sxs-lookup"><span data-stu-id="c16eb-136">Report</span></span>         | <span data-ttu-id="c16eb-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="c16eb-137">Azure AD Free</span></span> | <span data-ttu-id="c16eb-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="c16eb-138">Azure AD Premium P1</span></span> | <span data-ttu-id="c16eb-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="c16eb-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="c16eb-140">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="c16eb-140">Users at risk</span></span>  | <span data-ttu-id="c16eb-141">7 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-141">7 days</span></span>        | <span data-ttu-id="c16eb-142">30 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-142">30 days</span></span>             | <span data-ttu-id="c16eb-143">90 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-143">90 days</span></span>             |
| <span data-ttu-id="c16eb-144">Inicios de sesión no seguros</span><span class="sxs-lookup"><span data-stu-id="c16eb-144">Risky sign-ins</span></span> | <span data-ttu-id="c16eb-145">7 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-145">7 days</span></span>        | <span data-ttu-id="c16eb-146">30 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-146">30 days</span></span>             | <span data-ttu-id="c16eb-147">90 días</span><span class="sxs-lookup"><span data-stu-id="c16eb-147">90 days</span></span>             |

---