---
title: "Introducción a las conexiones híbridas de Azure Relay en .NET | Microsoft Docs"
description: "Escriba una aplicación de consola en C# para Conexiones híbridas de Azure Relay."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="7eb3f-103">Introducción a las conexiones híbridas de Relay</span><span class="sxs-lookup"><span data-stu-id="7eb3f-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="7eb3f-104">Este tutorial proporciona una introducción a las [conexiones híbridas de Azure Relay](relay-what-is-it.md#hybrid-connections) y muestra la forma cómo usar .NET para crear una aplicación de escucha correspondiente envía mensajes a una aplicación de escucha correspondiente.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="7eb3f-105">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="7eb3f-105">What will be accomplished</span></span>
<span data-ttu-id="7eb3f-106">Dado que las conexiones híbridas requieren un cliente y un componente de servidor, se van a crear dos aplicaciones de consola en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="7eb3f-107">Estos son los pasos que se deben seguir:</span><span class="sxs-lookup"><span data-stu-id="7eb3f-107">Here are the steps:</span></span>

1. <span data-ttu-id="7eb3f-108">Creación de un espacio de nombres de Relay mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="7eb3f-109">Creación de una conexión híbrida en dicho espacio de nombres mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="7eb3f-110">Escritura de una aplicación de consola de servidor (de escucha) para recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="7eb3f-111">Escritura de una aplicación de consola de cliente (remitente) para enviar mensajes.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7eb3f-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7eb3f-112">Prerequisites</span></span>

<span data-ttu-id="7eb3f-113">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="7eb3f-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="7eb3f-114">[Visual Studio 2015 o posterior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="7eb3f-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="7eb3f-115">En los ejemplos de este tutorial se usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="7eb3f-116">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="7eb3f-117">1. Creación de un espacio de nombres mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7eb3f-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="7eb3f-118">Si ya ha creado un espacio de nombres de Relay, vaya a la sección [Creación de una conexión híbrida mediante Azure Portal](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7eb3f-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="7eb3f-119">2. Creación de una conexión híbrida mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7eb3f-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="7eb3f-120">Si ya ha creado una conexión híbrida, vaya a la sección [Creación de una aplicación de servidor](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="7eb3f-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="7eb3f-121">3. Creación de una aplicación de servidor (agente de escucha)</span><span class="sxs-lookup"><span data-stu-id="7eb3f-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="7eb3f-122">Para escuchar y recibir mensajes desde Relay, escribiremos una aplicación de consola en C# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="7eb3f-123">4. Creación de una aplicación de cliente (remitente)</span><span class="sxs-lookup"><span data-stu-id="7eb3f-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="7eb3f-124">Para enviar mensajes a Relay, escribiremos una aplicación de consola en C# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="7eb3f-125">5. Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7eb3f-125">5. Run the applications</span></span>
1. <span data-ttu-id="7eb3f-126">Ejecute la aplicación de servidor.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-126">Run the server application.</span></span>
2. <span data-ttu-id="7eb3f-127">Ejecute la aplicación de cliente y escriba algún texto.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="7eb3f-128">Asegúrese de que la consola de aplicación de servidor genera el texto que escribió en la aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="7eb3f-130">Enhorabuena, ha creado una aplicación de conexiones híbridas de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="7eb3f-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eb3f-131">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7eb3f-131">Next steps:</span></span>
* [<span data-ttu-id="7eb3f-132">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="7eb3f-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="7eb3f-133">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="7eb3f-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="7eb3f-134">Introducción a Node</span><span class="sxs-lookup"><span data-stu-id="7eb3f-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

