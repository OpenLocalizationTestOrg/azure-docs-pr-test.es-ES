---
title: "aaaAn aplicación de Proxy de aplicación tarda demasiado tooload | Documentos de Microsoft"
description: "Solucionar problemas de rendimiento de carga de página con hello Proxy de aplicación de Azure AD"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="35154-103">Una aplicación de Proxy de aplicación tarda demasiado tooload</span><span class="sxs-lookup"><span data-stu-id="35154-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="35154-104">En este artículo le ayudarán a toounderstand ¿por qué una aplicación de Proxy de aplicación de Azure AD puede tardar un tooload mucho tiempo y qué puede hacer tooresolve este problema.</span><span class="sxs-lookup"><span data-stu-id="35154-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="35154-105">Información general</span><span class="sxs-lookup"><span data-stu-id="35154-105">Overview</span></span>
<span data-ttu-id="35154-106">Si están trabajando sus aplicaciones y ver una latencia elevada, puede haber algunos ajustes menores en la topología de red que puede considerar la velocidad de hello tooimprove.</span><span class="sxs-lookup"><span data-stu-id="35154-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="35154-107">Para obtener una evaluación de diferentes topologías, vea hello [documento de consideraciones de red](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="35154-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="35154-108">Si estas consideraciones no le sirven de ayuda, desgraciadamente ahora no disponemos de otras recomendaciones de optimización del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="35154-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="35154-109">Como Hola servicio Proxy de aplicación expande toomore centros de datos que pueden ser tooyou más cercano, latencia de toosee mejorado, puede iniciar directamente.</span><span class="sxs-lookup"><span data-stu-id="35154-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="35154-110">centros de la lista completa de hello toosee de datos de Azure, puede ver hello [página de prueba de latencia](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="35154-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="35154-111">Hello centros de datos con el servicio de Proxy de aplicación Hola pueden encontrarse con hello [herramienta de prueba de puertos de conector](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="35154-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="35154-112">Comentarios sobre las ubicaciones de los centros de datos de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="35154-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="35154-113">Puede haber centros de datos de Azure que todavía no incluyen el Proxy de aplicación pero conducirían mejora de gran latencia tooa para usted.</span><span class="sxs-lookup"><span data-stu-id="35154-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="35154-114">ubicación en el centro de datos de Hello < aadapfeedback@microsoft.com > por lo que podemos usar su tooplan comentarios tal y como se expanda.</span><span class="sxs-lookup"><span data-stu-id="35154-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="35154-115">Estamos trabajando en algunas capacidades adicionales que le ayudan a mejorar la latencia de Hola para los inquilinos que ven actualmente largas latencias y estar seguro de documentación de tooshare una vez disponibles.</span><span class="sxs-lookup"><span data-stu-id="35154-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35154-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35154-116">Next steps</span></span>
[<span data-ttu-id="35154-117">Trabajo con servidores proxy locales existentes</span><span class="sxs-lookup"><span data-stu-id="35154-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
