---
title: aaaFinding no administrada de aplicaciones en la nube con Cloud App Discovery | Documentos de Microsoft
description: "Proporciona información sobre cómo buscar y administrar aplicaciones con Cloud App Discovery, ¿cuáles son las ventajas de Hola y cómo funciona."
services: active-directory
keywords: cloud app discovery, administrar aplicaciones
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="b10fe-104">Búsqueda de aplicaciones de nube no administradas con Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="b10fe-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="b10fe-105">Información general</span><span class="sxs-lookup"><span data-stu-id="b10fe-105">Overview</span></span>
<span data-ttu-id="b10fe-106">En las empresas modernas, los departamentos de TI a menudo no son conscientes de las aplicaciones de nube de Hola que los miembros de su organización utilizan toodo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="b10fe-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="b10fe-107">Es fácil toosee ¿por qué los administradores tendrían preocupado datos toocorporate de acceso no autorizado, posible pérdida de datos y otros riesgos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b10fe-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="b10fe-108">Esta falta de conciencia puede hacer que un plan para tratar estos riesgos de seguridad parezca abrumador.</span><span class="sxs-lookup"><span data-stu-id="b10fe-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="b10fe-109">Cloud App Discovery es una característica de Premium de Azure Active Directory (AD) que permite que las aplicaciones de nube toodiscover que se utilizan los usuarios de hello en su organización.</span><span class="sxs-lookup"><span data-stu-id="b10fe-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="b10fe-110">**Con Cloud App Discovery, puede:**</span><span class="sxs-lookup"><span data-stu-id="b10fe-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="b10fe-111">Buscar aplicaciones que se va a usar en la nube de Hola y medir ese uso por número de usuarios, volumen de tráfico o número de aplicación de toohello de las solicitudes web.</span><span class="sxs-lookup"><span data-stu-id="b10fe-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="b10fe-112">Identificar a los usuarios de Hola que usan una aplicación.</span><span class="sxs-lookup"><span data-stu-id="b10fe-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="b10fe-113">Exporte datos para análisis sin conexión.</span><span class="sxs-lookup"><span data-stu-id="b10fe-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="b10fe-114">Lleve estas aplicaciones bajo el control de TI y habilite el inicio de sesión único para la administración de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b10fe-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="b10fe-115">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="b10fe-115">How it works</span></span>
1. <span data-ttu-id="b10fe-116">Los agentes de uso de aplicaciones se instalan en los equipos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b10fe-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="b10fe-117">información de uso de aplicación Hola capturada los agentes de Hola se envía a través de un servicio de detección de aplicaciones de canal seguro y cifrado toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="b10fe-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="b10fe-118">Hola servicio Cloud App Discovery evalúa los datos de Hola y genera informes.</span><span class="sxs-lookup"><span data-stu-id="b10fe-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Diagrama de Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="b10fe-120">tooget a trabajar con Cloud App Discovery, vea [introducción con Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="b10fe-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="b10fe-121">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="b10fe-121">Related articles</span></span>
* [<span data-ttu-id="b10fe-122">Consideraciones de seguridad y privacidad de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="b10fe-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="b10fe-123">Guía de implementación de la directiva de grupo de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="b10fe-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="b10fe-124">Guía de implementación de System Center de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="b10fe-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="b10fe-125">Configuración del registro de Cloud App Discovery para servidores proxy con puertos personalizados</span><span class="sxs-lookup"><span data-stu-id="b10fe-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="b10fe-126">Registro de cambios del agente de Cloud App Discovery </span><span class="sxs-lookup"><span data-stu-id="b10fe-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="b10fe-127">Preguntas más frecuentes de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="b10fe-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="b10fe-128">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b10fe-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

