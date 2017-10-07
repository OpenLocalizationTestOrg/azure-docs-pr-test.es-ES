---
title: "aaaGet a trabajar con las conexiones híbridas de Azure retransmisión en nodo | Documentos de Microsoft"
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
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="1be31-103">Introducción a las conexiones híbridas de Relay</span><span class="sxs-lookup"><span data-stu-id="1be31-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="1be31-104">Este tutorial proporciona una introducción demasiado[conexiones híbridas de Azure retransmisión](relay-what-is-it.md#hybrid-connections)y muestra cómo toouse Node.js toocreate una aplicación cliente que envía mensajes de aplicación de agente de escucha de tooa correspondiente.</span><span class="sxs-lookup"><span data-stu-id="1be31-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="1be31-105">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="1be31-105">What will be accomplished</span></span>

<span data-ttu-id="1be31-106">Dado que Conexiones híbridas requiere un cliente y un componente de servidor, en este tutorial crearemos dos aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="1be31-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="1be31-107">Estos son los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="1be31-107">Here are hello steps:</span></span>

1. <span data-ttu-id="1be31-108">Crear un espacio de nombres de retransmisión, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1be31-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="1be31-109">Crear una conexión híbrida usando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1be31-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="1be31-110">Escribir a un servidor de mensajes de tooreceive de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="1be31-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="1be31-111">Escribir a un cliente toosend mensajes de la aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="1be31-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1be31-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1be31-112">Prerequisites</span></span>

1. <span data-ttu-id="1be31-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="1be31-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="1be31-114">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1be31-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="1be31-115">1. Crear un espacio de nombres mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1be31-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="1be31-116">Si ya tiene un espacio de nombres de retransmisión creado, saltar toohello [crear una conexión híbrida con hello portal de Azure](#2-create-a-hybrid-connection-using-the-azure-portal) sección.</span><span class="sxs-lookup"><span data-stu-id="1be31-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="1be31-117">2. Crear una conexión híbrida con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1be31-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="1be31-118">Si ya tiene una conexión híbrida creada, saltar toohello [crear una aplicación de servidor](#3-create-a-server-application-listener) sección.</span><span class="sxs-lookup"><span data-stu-id="1be31-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="1be31-119">3. Creación de una aplicación de servidor (agente de escucha)</span><span class="sxs-lookup"><span data-stu-id="1be31-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="1be31-120">toolisten y recibir mensajes de Hola retransmisión, se escribirá una aplicación de consola de Node.js.</span><span class="sxs-lookup"><span data-stu-id="1be31-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="1be31-121">4. Creación de una aplicación de cliente (remitente)</span><span class="sxs-lookup"><span data-stu-id="1be31-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="1be31-122">toosend mensajes toohello retransmisión, que se va a escribir una aplicación de consola de Node.js.</span><span class="sxs-lookup"><span data-stu-id="1be31-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="1be31-123">5. Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="1be31-123">5. Run hello applications</span></span>

1. <span data-ttu-id="1be31-124">Ejecutar la aplicación de servidor hello: de un tipo de símbolo del sistema de Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="1be31-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="1be31-125">Ejecutar la aplicación de cliente de hello: de un tipo de símbolo del sistema de Node.js `node sender.js`y escriba algún texto.</span><span class="sxs-lookup"><span data-stu-id="1be31-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="1be31-126">Compruebe a que el servidor hello aplicación salidas Hola texto de la consola que se escribió en la aplicación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be31-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="1be31-128">Ya ha creado una aplicación de Conexiones híbridas de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="1be31-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="1be31-129">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1be31-129">Next steps:</span></span>

* [<span data-ttu-id="1be31-130">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="1be31-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="1be31-131">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="1be31-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="1be31-132">Introducción a .NET</span><span class="sxs-lookup"><span data-stu-id="1be31-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="1be31-133">Introducción a Node</span><span class="sxs-lookup"><span data-stu-id="1be31-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

