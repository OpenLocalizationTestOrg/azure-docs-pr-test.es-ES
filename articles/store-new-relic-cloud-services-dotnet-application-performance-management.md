---
title: aaaUsing New Relic con Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toomanage de servicio de New Relic y supervisar la aplicación de Azure."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="1cae6-103">Administración del rendimiento de la aplicación New Relic en Azure</span><span class="sxs-lookup"><span data-stu-id="1cae6-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="1cae6-104">Puede agregar desempeño de talla mundial de New Relic supervisión tooyour aplicaciones hospedadas de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cae6-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="1cae6-105">Junto con las completas funcionalidades de supervisión, solución de problemas y ajuste de las aplicaciones de Azure, también cumple los requisitos para obtener un precio con descuento en productos de New Relic utilizando Azure.</span><span class="sxs-lookup"><span data-stu-id="1cae6-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="1cae6-106">¿Qué es New Relic?</span><span class="sxs-lookup"><span data-stu-id="1cae6-106">What is New Relic?</span></span>
<span data-ttu-id="1cae6-107">Con [productos de New Relic](https://newrelic.com/products), puede resolver los errores de aplicación, adelantarse a posibles problemas y comprender las prestaciones de Hola de todo el entorno.</span><span class="sxs-lookup"><span data-stu-id="1cae6-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="1cae6-108">Es toosave diseñada que tiempo a la hora de identificar y diagnosticar problemas de rendimiento y coloca la información de hello necesita toosolve estos problemas a su alcance.</span><span class="sxs-lookup"><span data-stu-id="1cae6-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="1cae6-109">Nueva Relic pistas Hola cargar tiempo y el rendimiento de las transacciones de web, servidor de Hola y exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1cae6-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="1cae6-110">Muestra el tiempo transcurrido en base de datos de hello, analiza las consultas lentas y solicitudes web, proporciona el tiempo de actividad de supervisión y alertas, las excepciones de aplicación realiza un seguimiento y mucho más.</span><span class="sxs-lookup"><span data-stu-id="1cae6-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="1cae6-111">Precio especial</span><span class="sxs-lookup"><span data-stu-id="1cae6-111">Special pricing</span></span>
<span data-ttu-id="1cae6-112">Nueva Relic estándar es tooAzure libre a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1cae6-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="1cae6-113">New Relic Pro se ofrece en función del tamaño de instancia de Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="1cae6-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="1cae6-114">Para obtener más información, vea hello [página New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) en hello Azure Marketplace o póngase en contacto con New Relic (sales@newrelic.com) para los precios de nivel de empresa.</span><span class="sxs-lookup"><span data-stu-id="1cae6-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="1cae6-115">Los clientes de Azure reciben una suscripción de prueba de dos semanas de nuevo Relic Pro al implementar agente de New Relic Hola.</span><span class="sxs-lookup"><span data-stu-id="1cae6-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="1cae6-116">Registrarse para usar almacén de Azure Hola de New Relic</span><span class="sxs-lookup"><span data-stu-id="1cae6-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="1cae6-117">New Relic se integra perfectamente con los roles web y de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cae6-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="1cae6-118">Puede de forma rápida y fácilmente Regístrese para New Relic directamente desde Hola tienda de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cae6-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="1cae6-119">Para obtener instrucciones, consulte hello [instrucciones de inicio de sesión de almacenamiento de Azure](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) de New Relic.</span><span class="sxs-lookup"><span data-stu-id="1cae6-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="1cae6-120">Consulta de los datos</span><span class="sxs-lookup"><span data-stu-id="1cae6-120">View your data</span></span>
<span data-ttu-id="1cae6-121">Cuando se haya suscrito, puede sacar partido de las increíbles funcionalidades de supervisión de análisis basados en datos y supervisión de aplicaciones de New Relic.</span><span class="sxs-lookup"><span data-stu-id="1cae6-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="1cae6-122">toocheck rendimiento de la aplicación en New Relic:</span><span class="sxs-lookup"><span data-stu-id="1cae6-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="1cae6-123">En hello Portal de Azure, seleccione Administrar.</span><span class="sxs-lookup"><span data-stu-id="1cae6-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="1cae6-124">Inicie sesión con el correo electrónico y la contraseña de la cuenta de New Relic.</span><span class="sxs-lookup"><span data-stu-id="1cae6-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="1cae6-125">Seleccionar la aplicación de hello aplicación índice tooview datos de la de la aplicación en hello [página de información general APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="1cae6-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="1cae6-126">Uso de New Relic con Azure</span><span class="sxs-lookup"><span data-stu-id="1cae6-126">Using New Relic with Azure</span></span>
<span data-ttu-id="1cae6-127">Para obtener más información sobre cómo utilizar New Relic y Azure, visite el [sitio de documentación de New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), incluidas las siguientes secciones:</span><span class="sxs-lookup"><span data-stu-id="1cae6-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="1cae6-128">New Relic for .NET</span><span class="sxs-lookup"><span data-stu-id="1cae6-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="1cae6-129">Instrument a .NET Worker Role on Azure Cloud service</span><span class="sxs-lookup"><span data-stu-id="1cae6-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="1cae6-130">New Relic para la plataforma de nube de Microsoft Azure Hola</span><span class="sxs-lookup"><span data-stu-id="1cae6-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="1cae6-131">New Relic para hello servicios de aplicaciones de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1cae6-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="1cae6-132">New Relic/Azure troubleshooting</span><span class="sxs-lookup"><span data-stu-id="1cae6-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

