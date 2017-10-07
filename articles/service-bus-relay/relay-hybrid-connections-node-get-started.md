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
# <a name="get-started-with-relay-hybrid-connections"></a>Introducción a las conexiones híbridas de Relay

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Este tutorial proporciona una introducción demasiado[conexiones híbridas de Azure retransmisión](relay-what-is-it.md#hybrid-connections)y muestra cómo toouse Node.js toocreate una aplicación cliente que envía mensajes de aplicación de agente de escucha de tooa correspondiente. 

## <a name="what-will-be-accomplished"></a>Lo que se logrará

Dado que Conexiones híbridas requiere un cliente y un componente de servidor, en este tutorial crearemos dos aplicaciones de consola. Estos son los pasos de hello:

1. Crear un espacio de nombres de retransmisión, mediante Hola portal de Azure.
2. Crear una conexión híbrida usando Hola portal de Azure.
3. Escribir a un servidor de mensajes de tooreceive de aplicación de consola.
4. Escribir a un cliente toosend mensajes de la aplicación de consola.

## <a name="prerequisites"></a>Requisitos previos

1. [Node.js](https://nodejs.org/en/).
2. Una suscripción de Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Crear un espacio de nombres mediante Hola portal de Azure

Si ya tiene un espacio de nombres de retransmisión creado, saltar toohello [crear una conexión híbrida con hello portal de Azure](#2-create-a-hybrid-connection-using-the-azure-portal) sección.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Crear una conexión híbrida con hello portal de Azure

Si ya tiene una conexión híbrida creada, saltar toohello [crear una aplicación de servidor](#3-create-a-server-application-listener) sección.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Creación de una aplicación de servidor (agente de escucha)

toolisten y recibir mensajes de Hola retransmisión, se escribirá una aplicación de consola de Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Creación de una aplicación de cliente (remitente)

toosend mensajes toohello retransmisión, que se va a escribir una aplicación de consola de Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Ejecutar aplicaciones de Hola

1. Ejecutar la aplicación de servidor hello: de un tipo de símbolo del sistema de Node.js `node listener.js`.
2. Ejecutar la aplicación de cliente de hello: de un tipo de símbolo del sistema de Node.js `node sender.js`y escriba algún texto.
3. Compruebe a que el servidor hello aplicación salidas Hola texto de la consola que se escribió en la aplicación de cliente de Hola.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Ya ha creado una aplicación de Conexiones híbridas de un extremo a otro.

## <a name="next-steps"></a>Pasos siguientes:

* [Preguntas más frecuentes acerca de Relay](relay-faq.md)
* [Creación de un espacio de nombres](relay-create-namespace-portal.md)
* [Introducción a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introducción a Node](relay-hybrid-connections-node-get-started.md)

