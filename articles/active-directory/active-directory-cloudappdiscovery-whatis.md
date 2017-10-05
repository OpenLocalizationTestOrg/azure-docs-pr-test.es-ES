---
title: "Búsqueda de aplicaciones en la nube no administradas con Cloud App Discovery | Microsoft Docs"
description: "Ofrece información sobre la búsqueda y la administración de aplicaciones con Cloud App Discovery, sobre cuáles son los beneficios y sobre cómo funciona."
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="8d3d9-104">Búsqueda de aplicaciones de nube no administradas con Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="8d3d9-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="8d3d9-105">Información general</span><span class="sxs-lookup"><span data-stu-id="8d3d9-105">Overview</span></span>
<span data-ttu-id="8d3d9-106">En las empresas modernas, los departamentos de TI a menudo no son conscientes de todas las aplicaciones en la nube que usan los miembros de su organización para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="8d3d9-107">Es fácil ver por qué a los administradores les podría preocupar el acceso no autorizado a datos corporativos, la posible pérdida de datos y otros riesgos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="8d3d9-108">Esta falta de conciencia puede hacer que un plan para tratar estos riesgos de seguridad parezca abrumador.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="8d3d9-109">Cloud App Discovery es una característica de Azure Active Directory (AD) Premium que permite detectar aplicaciones de nube usadas por las personas de su organización.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="8d3d9-110">**Con Cloud App Discovery, puede:**</span><span class="sxs-lookup"><span data-stu-id="8d3d9-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="8d3d9-111">Encuentre las aplicaciones de nube que se están usando y mida ese uso por el número de usuarios, el volumen de tráfico o el número de solicitudes web a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="8d3d9-112">Identificar a los usuarios que están usando una aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="8d3d9-113">Exporte datos para análisis sin conexión.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="8d3d9-114">Lleve estas aplicaciones bajo el control de TI y habilite el inicio de sesión único para la administración de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="8d3d9-115">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="8d3d9-115">How it works</span></span>
1. <span data-ttu-id="8d3d9-116">Los agentes de uso de aplicaciones se instalan en los equipos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="8d3d9-117">La información de uso de aplicaciones que capturan los agentes se envía a través de un canal seguro y cifrado al servicio Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="8d3d9-118">El servicio Cloud App Discovery evalúa los datos y genera informes.</span><span class="sxs-lookup"><span data-stu-id="8d3d9-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Diagrama de Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="8d3d9-120">Para empezar con Cloud App Discovery, vea [Introducción a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="8d3d9-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="8d3d9-121">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="8d3d9-121">Related articles</span></span>
* [<span data-ttu-id="8d3d9-122">Consideraciones de seguridad y privacidad de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="8d3d9-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="8d3d9-123">Guía de implementación de la directiva de grupo de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="8d3d9-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="8d3d9-124">Guía de implementación de System Center de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="8d3d9-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="8d3d9-125">Configuración del registro de Cloud App Discovery para servidores proxy con puertos personalizados</span><span class="sxs-lookup"><span data-stu-id="8d3d9-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="8d3d9-126">Registro de cambios del agente de Cloud App Discovery </span><span class="sxs-lookup"><span data-stu-id="8d3d9-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="8d3d9-127">Preguntas más frecuentes de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="8d3d9-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="8d3d9-128">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d3d9-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

