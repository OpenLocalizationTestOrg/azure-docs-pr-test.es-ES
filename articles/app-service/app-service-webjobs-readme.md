---
title: "aaaWebJobs en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo comprueba toobuild WebJobs toorun fondo, interactuar con los servicios como el almacenamiento y el Bus de servicio y crear las tareas programadas."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a>Uso de WebJobs en Servicio de aplicaciones de Azure
En este artículo se vincula toodocumentation recursos acerca de cómo toouse WebJobs de Azure y Hola SDK de WebJobs de Azure. WebJobs de Azure proporcionan un secuencias de comandos de toorun de forma sencilla o procesos en segundo plano programas como en [aplicación del servicio de aplicaciones Web](http://go.microsoft.com/fwlink/?LinkId=529714). Puede cargar y ejecutar un archivo ejecutable como cmd, bat, exe (.NET), ps1, sh, php, py, js y jar. Estos programas se ejecutan como WebJobs según una programación (cron) o de forma continua.

Hola SDK de WebJobs resulta más fácil toouse almacenamiento de Azure. Hola SDK de WebJobs tiene un enlace y un sistema de desencadenador que funciona con almacenamiento de Blobs de Microsoft Azure, colas y tablas, así como las colas de Bus de servicio.

La creación, implementación y administración de WebJobs se realiza de manera fluida gracias al conjunto de herramientas integradas en Visual Studio. Puede crear WebJobs a partir de plantillas, así como publicarlos y administrarlos (procesos de ejecución, detención, supervisión o implementación).

panel de WebJobs de Hola Hola portal de Azure proporciona capacidades de administración eficaces que ofrecen un control total sobre la ejecución de Hola de trabajos Web, incluidas capacidad de hello tooinvoke funciones individuales dentro de trabajos Web. panel de Hola también muestra los tiempos de ejecución de función y la salida del registro.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

