---
title: Uso de la API de REST para acceder a las API del servicio Azure Mobile Engagement
description: "Describe cómo usar las API de REST de Mobile Engagement para acceder a las API del servicio Azure Mobile Engagement"
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="a5136-103">Uso de REST para acceder a las API del servicio Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a5136-103">Using REST to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="a5136-104">Azure Mobile Engagement proporciona la [API de REST Azure Mobile Engagement](https://msdn.microsoft.com/library/azure/mt683754.aspx) para administrar dispositivos, campañas de cobertura e inserción, etc.</span><span class="sxs-lookup"><span data-stu-id="a5136-104">Azure Mobile Engagement provides the [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you to manage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="a5136-105">El servicio Azure Mobile Engagement se retirará en marzo de 2018 y actualmente solo está disponible para los clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="a5136-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="a5136-106">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="a5136-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="a5136-107">Si no desea usar las API de REST directamente, también proporcionamos un [archivo de Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que puede utilizar con las herramientas para generar los SDK para su idioma preferido.</span><span class="sxs-lookup"><span data-stu-id="a5136-107">If you do not want to use the REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="a5136-108">Se recomienda usar la herramienta [AutoRest](https://github.com/Azure/AutoRest) para generar el SDK a partir de nuestro archivo de Swagger.</span><span class="sxs-lookup"><span data-stu-id="a5136-108">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span> <span data-ttu-id="a5136-109">De forma similar, hemos creado un SDK para .NET que permite interactuar con estas API con un contenedor de C# sin tener que realizar la negociación de token de autenticación y la actualización usted mismo.</span><span class="sxs-lookup"><span data-stu-id="a5136-109">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="a5136-110">Vea el [ejemplo del SDK de .NET de la API del servicio](mobile-engagement-dotnet-sdk-service-api.md) para obtener información sobre cómo usar el SDK de .NET de la API.</span><span class="sxs-lookup"><span data-stu-id="a5136-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) to learn how to use the .net SDK for API</span></span>
