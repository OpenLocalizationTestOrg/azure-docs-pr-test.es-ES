---
title: "aaaGetting a trabajar con la API informes de hello Azure AD en el portal clásico de hello Azure AD | Documentos de Microsoft"
description: "Cómo tooget iniciado con hello Azure Active Directory API de informes"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="5da7a-103">Introducción a hello Azure Active Directory API de informes en el portal clásico de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da7a-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="5da7a-104">*Este tema forma parte del programa Hola a [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="5da7a-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="5da7a-105">Azure Active Directory proporciona una variedad de informes.</span><span class="sxs-lookup"><span data-stu-id="5da7a-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="5da7a-106">datos de Hola de estos informes pueden ser muy útil tooyour aplicaciones, como sistemas SIEM, auditoría y herramientas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="5da7a-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="5da7a-107">Hello Azure AD reporting que API proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST.</span><span class="sxs-lookup"><span data-stu-id="5da7a-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="5da7a-108">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="5da7a-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="5da7a-109">Este artículo proporciona información de hello necesita tooget trabajar rápidamente con informes de hello Azure AD API.</span><span class="sxs-lookup"><span data-stu-id="5da7a-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="5da7a-110">En la siguiente sección hello, puede ver más detalles sobre el uso de Hola de auditoría y las API de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5da7a-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="5da7a-111">Para todas las demás API, vea hello [events(preview) e informes de Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artículo.</span><span class="sxs-lookup"><span data-stu-id="5da7a-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="5da7a-112">Para ver preguntas, problemas o comentarios, póngase en contacto con el equipo de [ayuda de informes de AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5da7a-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="5da7a-113">Mapa de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="5da7a-113">Learning map</span></span>
1. <span data-ttu-id="5da7a-114">**Preparar** -para poder probar sus ejemplos de API, deberá hello toocomplete [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5da7a-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="5da7a-115">**Explorar** -obtener una primera impresión de hello reporting API:</span><span class="sxs-lookup"><span data-stu-id="5da7a-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="5da7a-116">Uso de ejemplos de hello para auditoría Hola API</span><span class="sxs-lookup"><span data-stu-id="5da7a-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="5da7a-117">Uso de ejemplos de hello para la API de informes de actividad de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="5da7a-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="5da7a-118">**Personalización** : cree su propia solución:</span><span class="sxs-lookup"><span data-stu-id="5da7a-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="5da7a-119">Uso de referencia de API de auditoría de Hola</span><span class="sxs-lookup"><span data-stu-id="5da7a-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="5da7a-120">Referencia de API con informe de actividad de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="5da7a-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="5da7a-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5da7a-121">Next Steps</span></span>
<span data-ttu-id="5da7a-122">Si estás toosee curiosidad todos Hola extremos disponibles de la API de Azure AD Graph desplazándose demasiado[https://graph.windows.net/tenant-name/reports/$ metadatos? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="5da7a-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

