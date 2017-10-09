---
title: Hola aaaUsing tooaccess de API de REST API de servicios de Azure Mobile Engagement
description: "Describe cómo toouse Hola las API de REST de Mobile Engagement tooaccess las API de servicio de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="ca028-103">Usar tooaccess REST API de servicios de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ca028-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="ca028-104">Azure Mobile Engagement proporciona hello [API de REST de Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) automáticamente dispositivos de toomanage, las campañas de Reach/inserción etcetera.</span><span class="sxs-lookup"><span data-stu-id="ca028-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="ca028-105">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="ca028-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="ca028-106">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="ca028-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="ca028-107">Si no desea toouse hello las API de REST directamente, también proporcionamos una [archivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que puede usar con herramientas de SDK de toogenerate para su idioma preferido.</span><span class="sxs-lookup"><span data-stu-id="ca028-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="ca028-108">Se recomienda usar hello [AutoRest](https://github.com/Azure/AutoRest) toogenerate de herramientas del SDK de nuestro archivo Swagger.</span><span class="sxs-lookup"><span data-stu-id="ca028-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="ca028-109">Hemos creado un SDK para .NET de forma similar, que le permite toointeract con estas API utilizando un contenedor de C# y no tiene toodo Hola negociación del token de autenticación y actualizar usted mismo.</span><span class="sxs-lookup"><span data-stu-id="ca028-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="ca028-110">Vea [ejemplo de SDK de servicio API .NET](mobile-engagement-dotnet-sdk-service-api.md) toolearn cómo toouse Hola .net SDK de API</span><span class="sxs-lookup"><span data-stu-id="ca028-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
