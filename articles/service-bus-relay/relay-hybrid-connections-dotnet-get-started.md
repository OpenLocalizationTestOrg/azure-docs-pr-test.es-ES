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
# <a name="get-started-with-relay-hybrid-connections"></a>Introducción a las conexiones híbridas de Relay
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Este tutorial proporciona una introducción demasiado[conexiones híbridas de Azure retransmisión](relay-what-is-it.md#hybrid-connections)y muestra cómo toouse .NET toocreate una aplicación cliente que envía mensajes de aplicación de agente de escucha de tooa correspondiente. 

## <a name="what-will-be-accomplished"></a>Lo que se logrará
Dado que las conexiones híbridas requiere un cliente y un componente de servidor, tutorial Hola crea dos aplicaciones de consola. Estos son los pasos de hello:

1. Crear un espacio de nombres de retransmisión, mediante Hola portal de Azure.
2. Crear una conexión híbrida en ese espacio de nombres, mediante Hola portal de Azure.
3. Escribir mensajes de tooreceive la aplicación de una consola de servidor (agente de escucha).
4. Escribir mensajes de toosend la aplicación de una consola de cliente (remitente).

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesitará Hola siguiendo los requisitos previos:

1. [Visual Studio 2015 o posterior](http://www.visualstudio.com). ejemplos de Hello en este tutorial utiliza Visual Studio de 2017.
2. Una suscripción de Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Crear un espacio de nombres mediante Hola portal de Azure
Si ya ha creado un espacio de nombres de retransmisión, consulte el toohello [crear una conexión híbrida con hello portal de Azure](#2-create-a-hybrid-connection-using-the-azure-portal) sección.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Crear una conexión híbrida con hello portal de Azure
Si ya ha creado una conexión híbrida, saltar toohello [crear una aplicación de servidor](#3-create-a-server-application-listener) sección.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Creación de una aplicación de servidor (agente de escucha)
toolisten y recibir mensajes de Hola retransmisión, se escribirá una aplicación de consola de C# con Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Creación de una aplicación de cliente (remitente)
Retransmitir toosend mensajes toohello, que se va a escribir una aplicación de consola de C# con Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Ejecutar aplicaciones de Hola
1. Ejecute la aplicación de servidor hello.
2. Ejecute la aplicación de cliente de hello y escriba algún texto.
3. Compruebe a que el servidor hello aplicación salidas Hola texto de la consola que se escribió en la aplicación de cliente de Hola.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Enhorabuena, ha creado una aplicación de conexiones híbridas de extremo a extremo.

## <a name="next-steps"></a>Pasos siguientes:
* [Preguntas más frecuentes acerca de Relay](relay-faq.md)
* [Creación de un espacio de nombres](relay-create-namespace-portal.md)
* [Introducción a Node](relay-hybrid-connections-node-get-started.md)

