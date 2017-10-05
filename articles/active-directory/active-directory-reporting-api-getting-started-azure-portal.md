---
title: "Introducción a la API de generación de informes de Azure AD | Microsoft Docs"
description: "Introducción a la API de generación informes de Azure Active Directory"
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
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="17e89-103">Introducción a la API de generación de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17e89-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="17e89-104">Azure Active Directory proporciona una variedad de informes.</span><span class="sxs-lookup"><span data-stu-id="17e89-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="17e89-105">Los datos de estos informes pueden ser muy útiles para las aplicaciones, como sistemas SIEM, auditorías y herramientas de inteligencia empresarial.</span><span class="sxs-lookup"><span data-stu-id="17e89-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="17e89-106">Las API de generación de informes de Azure AD proporcionan acceso mediante programación a los datos a través de un conjunto de API de REST.</span><span class="sxs-lookup"><span data-stu-id="17e89-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="17e89-107">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="17e89-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="17e89-108">Este artículo proporciona la información que necesita para empezar a trabajar con las API de generación de informes de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17e89-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="17e89-109">En la sección siguiente, puede encontrar más detalles sobre el uso de las API de auditoría e inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="17e89-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="17e89-110">Para conocer las preguntas más frecuentes, lea nuestras [Preguntas más frecuentes](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="17e89-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="17e89-111">En caso de problemas, [abra una incidencia de soporte técnico](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="17e89-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="17e89-112">Mapa de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="17e89-112">Learning map</span></span>
1. <span data-ttu-id="17e89-113">**Preparación** : para poder usar los ejemplos de la API, debe completar la [requisitos previos para tener acceso a la API de generación de informes de Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17e89-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="17e89-114">**Exploración** : obtenga una primera impresión de las API de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="17e89-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="17e89-115">Uso de los ejemplos de la API de auditoría</span><span class="sxs-lookup"><span data-stu-id="17e89-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="17e89-116">Uso de los ejemplos de la API de generación de informes de actividad de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="17e89-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="17e89-117">**Personalización** : cree su propia solución:</span><span class="sxs-lookup"><span data-stu-id="17e89-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="17e89-118">Uso de la referencia de la API de auditoría</span><span class="sxs-lookup"><span data-stu-id="17e89-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="17e89-119">Uso de la referencia de la API de generación de informes de actividad de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="17e89-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="17e89-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17e89-120">Next Steps</span></span>
<span data-ttu-id="17e89-121">Si tiene curiosidad por ver todos los puntos de conexión disponibles de la API Graph de Azure AD, use este vínculo: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="17e89-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

