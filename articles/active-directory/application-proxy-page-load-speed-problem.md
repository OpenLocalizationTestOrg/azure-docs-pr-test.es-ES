---
title: "Tiempo excesivo de carga de una aplicación con el proxy de aplicación | Microsoft Docs"
description: "Solución de problemas de rendimiento de carga de páginas con el Proxy de aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="9f4ce-103">Tiempo excesivo de carga de una aplicación con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="9f4ce-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="9f4ce-104">Este artículo le ayudará a entender por qué una aplicación con Proxy de aplicación de Azure AD puede tardar mucho tiempo en cargar y lo que puede hacer para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="9f4ce-105">Información general</span><span class="sxs-lookup"><span data-stu-id="9f4ce-105">Overview</span></span>
<span data-ttu-id="9f4ce-106">Si sus aplicaciones funcionan, pero ve una latencia elevada, puede haber algunos ajustes menores en la topología de red que puede realizar para mejorar la velocidad.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="9f4ce-107">Para una evaluación de diferentes topologías, consulte el [documento de consideraciones de red](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="9f4ce-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="9f4ce-108">Si estas consideraciones no le sirven de ayuda, desgraciadamente ahora no disponemos de otras recomendaciones de optimización del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="9f4ce-109">Como el servicio de Proxy de aplicación se expande a otros centros de datos que le resulten más cercanos, podría empezar a ver directamente una mejora en la latencia.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="9f4ce-110">Para ver la lista completa de los centros de datos de Azure, consulte la [página de prueba de latencia](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="9f4ce-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="9f4ce-111">Con la [herramienta de prueba de los puertos del conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) encontrará los centros de datos con el servicio de Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="9f4ce-112">Comentarios sobre las ubicaciones de los centros de datos de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="9f4ce-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="9f4ce-113">Puede haber centros de datos de Azure que todavía no incluyan el Proxy de aplicación, pero que le supongan una mejora importante de la latencia.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="9f4ce-114">Envíe la ubicación del centro de datos a <aadapfeedback@microsoft.com> para que podamos implementar sus comentarios en los planes de expansión.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="9f4ce-115">Estamos trabajando en algunas funcionalidades adicionales que ayuden a mejorar la latencia de los inquilinos que actualmente experimentan largas latencias; compartiremos la documentación en cuanto esté disponible.</span><span class="sxs-lookup"><span data-stu-id="9f4ce-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f4ce-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f4ce-116">Next steps</span></span>
[<span data-ttu-id="9f4ce-117">Trabajo con servidores proxy locales existentes</span><span class="sxs-lookup"><span data-stu-id="9f4ce-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
