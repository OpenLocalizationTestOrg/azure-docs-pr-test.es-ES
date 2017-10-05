---
title: "Introducción a la API de generación de informes de Azure AD en el portal clásico de Azure AD | Microsoft Docs"
description: "Introducción a la API de generación informes de Azure Active Directory"
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
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="b2a1b-103">Introducción a la API de generación de informes de Azure Active Directory en el portal clásico de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2a1b-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="b2a1b-104">*Esta documentación forma parte de la [guía de generación de informes de Azure Active Directory](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="b2a1b-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="b2a1b-105">Azure Active Directory proporciona una variedad de informes.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="b2a1b-106">Los datos de estos informes pueden ser muy útiles para las aplicaciones, como sistemas SIEM, auditorías y herramientas de inteligencia empresarial.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="b2a1b-107">Las API de generación de informes de Azure AD proporcionan acceso mediante programación a los datos a través de un conjunto de API de REST.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="b2a1b-108">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b2a1b-109">Este artículo proporciona la información que necesita para empezar a trabajar con las API de generación de informes de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="b2a1b-110">En la sección siguiente, puede encontrar más detalles sobre el uso de las API de auditoría e inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="b2a1b-111">Para el resto de las API, consulte el artículo de [eventos e informes de Azure AD (versión preliminar)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview).</span><span class="sxs-lookup"><span data-stu-id="b2a1b-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="b2a1b-112">Para ver preguntas, problemas o comentarios, póngase en contacto con el equipo de [ayuda de informes de AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b2a1b-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="b2a1b-113">Mapa de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="b2a1b-113">Learning map</span></span>
1. <span data-ttu-id="b2a1b-114">**Preparación** : para poder usar los ejemplos de la API, debe completar la [requisitos previos para tener acceso a la API de generación de informes de Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="b2a1b-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="b2a1b-115">**Exploración** : obtenga una primera impresión de las API de generación de informes.</span><span class="sxs-lookup"><span data-stu-id="b2a1b-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="b2a1b-116">Uso de los ejemplos de la API de auditoría</span><span class="sxs-lookup"><span data-stu-id="b2a1b-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="b2a1b-117">Uso de los ejemplos de la API de generación de informes de actividad de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="b2a1b-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="b2a1b-118">**Personalización** : cree su propia solución:</span><span class="sxs-lookup"><span data-stu-id="b2a1b-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="b2a1b-119">Uso de la referencia de la API de auditoría</span><span class="sxs-lookup"><span data-stu-id="b2a1b-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="b2a1b-120">Uso de la referencia de la API de generación de informes de actividad de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="b2a1b-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="b2a1b-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2a1b-121">Next Steps</span></span>
<span data-ttu-id="b2a1b-122">Todos los puntos de conexión disponibles de API Graph de Azure se encuentran en la página [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="b2a1b-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

