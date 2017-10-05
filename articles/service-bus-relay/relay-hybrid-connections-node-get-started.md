---
title: "Introducción a las conexiones híbridas de Azure Relay en un nodo | Microsoft Docs"
description: "Escriba una aplicación de consola en Node.js para Conexiones híbridas de Azure Relay."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: c3bfc45969f250059988129f532edd12dfe3dcfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="b870a-103">Introducción a Conexiones híbridas de Relay</span><span class="sxs-lookup"><span data-stu-id="b870a-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="b870a-104">Este tutorial proporciona una introducción a [Conexiones híbridas de Azure Relay](relay-what-is-it.md#hybrid-connections) y muestra la forma cómo usar Node.js para crear una aplicación de escucha correspondiente envía mensajes a una aplicación de escucha correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b870a-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use Node.js to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="b870a-105">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="b870a-105">What will be accomplished</span></span>

<span data-ttu-id="b870a-106">Dado que Conexiones híbridas requiere un cliente y un componente de servidor, en este tutorial crearemos dos aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="b870a-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="b870a-107">Estos son los pasos que se deben seguir:</span><span class="sxs-lookup"><span data-stu-id="b870a-107">Here are the steps:</span></span>

1. <span data-ttu-id="b870a-108">Creación de un espacio de nombres de Relay mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b870a-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="b870a-109">Creación de una conexión híbrida mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b870a-109">Create a hybrid connection, using the Azure portal.</span></span>
3. <span data-ttu-id="b870a-110">Escritura de una aplicación de consola de servidor para recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="b870a-110">Write a server console application to receive messages.</span></span>
4. <span data-ttu-id="b870a-111">Escritura de una aplicación de consola de cliente para enviar mensajes.</span><span class="sxs-lookup"><span data-stu-id="b870a-111">Write a client console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b870a-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b870a-112">Prerequisites</span></span>

1. <span data-ttu-id="b870a-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="b870a-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="b870a-114">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b870a-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="b870a-115">1. Creación de un espacio de nombres mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b870a-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="b870a-116">Si ya tiene creado un espacio de nombres de Relay, vaya a la sección [Creación de una conexión híbrida mediante Azure Portal](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b870a-116">If you already have a Relay namespace created, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="b870a-117">2. Creación de una conexión híbrida mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b870a-117">2. Create a hybrid connection using the Azure portal</span></span>

<span data-ttu-id="b870a-118">Si ya tiene una conexión híbrida creada, vaya a la sección [Creación de una aplicación de servidor (agente de escucha)](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="b870a-118">If you already have a hybrid connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="b870a-119">3. Creación de una aplicación de servidor (agente de escucha)</span><span class="sxs-lookup"><span data-stu-id="b870a-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="b870a-120">Para escuchar y recibir mensajes desde Relay, escribiremos una aplicación de consola en Node.js.</span><span class="sxs-lookup"><span data-stu-id="b870a-120">To listen and receive messages from the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="b870a-121">4. Creación de una aplicación de cliente (remitente)</span><span class="sxs-lookup"><span data-stu-id="b870a-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="b870a-122">Para enviar mensajes a Relay, escribiremos una aplicación de consola en Node.js.</span><span class="sxs-lookup"><span data-stu-id="b870a-122">To send messages to the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="b870a-123">5. Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b870a-123">5. Run the applications</span></span>

1. <span data-ttu-id="b870a-124">Ejecute la aplicación de servidor: en un símbolo del sistema de Node.js escriba `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="b870a-124">Run the server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="b870a-125">Ejecute la aplicación de cliente: en un símbolo del sistema de Node.js escriba `node sender.js` y escriba texto.</span><span class="sxs-lookup"><span data-stu-id="b870a-125">Run the client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="b870a-126">Asegúrese de que la consola de aplicación de servidor genera el texto que escribió en la aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="b870a-126">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="b870a-128">Ya ha creado una aplicación de Conexiones híbridas de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="b870a-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b870a-129">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b870a-129">Next steps:</span></span>

* [<span data-ttu-id="b870a-130">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="b870a-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="b870a-131">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="b870a-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="b870a-132">Introducción a .NET</span><span class="sxs-lookup"><span data-stu-id="b870a-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="b870a-133">Introducción a Node</span><span class="sxs-lookup"><span data-stu-id="b870a-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

