---
title: "aaaGet a trabajar con las conexiones híbridas de retransmisión de Azure en .NET | Documentos de Microsoft"
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
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="3fba0-103">Introducción a las conexiones híbridas de Relay</span><span class="sxs-lookup"><span data-stu-id="3fba0-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="3fba0-104">Este tutorial proporciona una introducción demasiado[conexiones híbridas de Azure retransmisión](relay-what-is-it.md#hybrid-connections)y muestra cómo toouse .NET toocreate una aplicación cliente que envía mensajes de aplicación de agente de escucha de tooa correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3fba0-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="3fba0-105">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="3fba0-105">What will be accomplished</span></span>
<span data-ttu-id="3fba0-106">Dado que las conexiones híbridas requiere un cliente y un componente de servidor, tutorial Hola crea dos aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="3fba0-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="3fba0-107">Estos son los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3fba0-107">Here are hello steps:</span></span>

1. <span data-ttu-id="3fba0-108">Crear un espacio de nombres de retransmisión, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fba0-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="3fba0-109">Crear una conexión híbrida en ese espacio de nombres, mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fba0-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="3fba0-110">Escribir mensajes de tooreceive la aplicación de una consola de servidor (agente de escucha).</span><span class="sxs-lookup"><span data-stu-id="3fba0-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="3fba0-111">Escribir mensajes de toosend la aplicación de una consola de cliente (remitente).</span><span class="sxs-lookup"><span data-stu-id="3fba0-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fba0-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3fba0-112">Prerequisites</span></span>

<span data-ttu-id="3fba0-113">toocomplete este tutorial, necesitará Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="3fba0-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="3fba0-114">[Visual Studio 2015 o posterior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="3fba0-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="3fba0-115">ejemplos de Hello en este tutorial utiliza Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="3fba0-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="3fba0-116">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3fba0-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="3fba0-117">1. Crear un espacio de nombres mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3fba0-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="3fba0-118">Si ya ha creado un espacio de nombres de retransmisión, consulte el toohello [crear una conexión híbrida con hello portal de Azure](#2-create-a-hybrid-connection-using-the-azure-portal) sección.</span><span class="sxs-lookup"><span data-stu-id="3fba0-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="3fba0-119">2. Crear una conexión híbrida con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3fba0-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="3fba0-120">Si ya ha creado una conexión híbrida, saltar toohello [crear una aplicación de servidor](#3-create-a-server-application-listener) sección.</span><span class="sxs-lookup"><span data-stu-id="3fba0-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="3fba0-121">3. Creación de una aplicación de servidor (agente de escucha)</span><span class="sxs-lookup"><span data-stu-id="3fba0-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="3fba0-122">toolisten y recibir mensajes de Hola retransmisión, se escribirá una aplicación de consola de C# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fba0-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="3fba0-123">4. Creación de una aplicación de cliente (remitente)</span><span class="sxs-lookup"><span data-stu-id="3fba0-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="3fba0-124">Retransmitir toosend mensajes toohello, que se va a escribir una aplicación de consola de C# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fba0-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="3fba0-125">5. Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="3fba0-125">5. Run hello applications</span></span>
1. <span data-ttu-id="3fba0-126">Ejecute la aplicación de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="3fba0-126">Run hello server application.</span></span>
2. <span data-ttu-id="3fba0-127">Ejecute la aplicación de cliente de hello y escriba algún texto.</span><span class="sxs-lookup"><span data-stu-id="3fba0-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="3fba0-128">Compruebe a que el servidor hello aplicación salidas Hola texto de la consola que se escribió en la aplicación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3fba0-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="3fba0-130">Enhorabuena, ha creado una aplicación de conexiones híbridas de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="3fba0-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fba0-131">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3fba0-131">Next steps:</span></span>
* [<span data-ttu-id="3fba0-132">Preguntas más frecuentes acerca de Relay</span><span class="sxs-lookup"><span data-stu-id="3fba0-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="3fba0-133">Creación de un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="3fba0-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="3fba0-134">Introducción a Node</span><span class="sxs-lookup"><span data-stu-id="3fba0-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

