---
title: "aaaGetting a trabajar con la API de generación de informes de hello Azure AD | Documentos de Microsoft"
description: "Cómo tooget iniciado con hello Azure Active Directory API de informes"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="65714-103">Introducción a hello Azure Active Directory API de informes</span><span class="sxs-lookup"><span data-stu-id="65714-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="65714-104">Azure Active Directory proporciona una variedad de informes.</span><span class="sxs-lookup"><span data-stu-id="65714-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="65714-105">datos de Hola de estos informes pueden ser muy útil tooyour aplicaciones, como sistemas SIEM, auditoría y herramientas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="65714-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="65714-106">Hello Azure AD reporting que API proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST.</span><span class="sxs-lookup"><span data-stu-id="65714-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="65714-107">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="65714-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="65714-108">Este artículo proporciona información de hello necesita tooget trabajar rápidamente con informes de hello Azure AD API.</span><span class="sxs-lookup"><span data-stu-id="65714-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="65714-109">En la siguiente sección hello, puede ver más detalles sobre el uso de Hola de auditoría y las API de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="65714-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="65714-110">Para conocer las preguntas más frecuentes, lea nuestras [Preguntas más frecuentes](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="65714-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="65714-111">En caso de problemas, [abra una incidencia de soporte técnico](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="65714-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="65714-112">Mapa de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="65714-112">Learning map</span></span>
1. <span data-ttu-id="65714-113">**Preparar** -para poder probar sus ejemplos de API, deberá hello toocomplete [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65714-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="65714-114">**Explorar** -obtener una primera impresión de hello reporting API:</span><span class="sxs-lookup"><span data-stu-id="65714-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="65714-115">Uso de ejemplos de hello para auditoría Hola API</span><span class="sxs-lookup"><span data-stu-id="65714-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="65714-116">Uso de ejemplos de hello para la API de informes de actividad de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="65714-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="65714-117">**Personalización** : cree su propia solución:</span><span class="sxs-lookup"><span data-stu-id="65714-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="65714-118">Uso de referencia de API de auditoría de Hola</span><span class="sxs-lookup"><span data-stu-id="65714-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="65714-119">Referencia de API con informe de actividad de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="65714-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="65714-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65714-120">Next Steps</span></span>
<span data-ttu-id="65714-121">Si estás toosee curiosidad todos los extremos de Azure AD Graph API disponibles, utilice este vínculo: [https://graph.windows.net/tenant-name/activities/$ metadatos? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="65714-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

