---
title: "configuración de aaaUsing PM2 para Node.js en la aplicación Web de Azure en Linux | Documentos de Microsoft"
description: "Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure"
keywords: azure app service, aplic. web, nodejs, pm2, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Si establece tooNode.js de pila de aplicación hello para la aplicación Web de Azure en Linux, obtendrá Hola opción tooset un archivo de inicio de Node.js como se muestra en hello después de imagen:

![Establecer un archivo de inicio de Node.js][1]

Puede usar esta opción toodo uno de hello siguientes tareas:

* Especifique el script de inicio de hello para la aplicación Node.js (por ejemplo: /bin/server.js).
* Especificar Hola PM2 toouse de archivo de configuración de la aplicación Node.js (por ejemplo: /foo/process.json).
  
  > [!NOTE]
  > Si desea que su toorestart de procesos de Node.js automáticamente cuando se modifican determinados archivos, use configuración de PM2 Hola. En caso contrario, la aplicación no se reiniciará cuando recibe notificaciones de cambio (por ejemplo, cuando cambia el código de aplicación).
  > 
  > 

Puede comprobar hello Node.js [Procesar documentación archivos](http://pm2.keymetrics.io/docs/usage/application-declaration/) para todas las opciones de Hola, pero aquí te mostramos un ejemplo de lo que puede usar como el archivo process.json:

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

Toonote aspectos importantes en esta configuración son:

* propiedad de "script" Hola especifica la secuencia de comandos de inicio de la aplicación.
* propiedad de "instancias" Hello especifica cuántas instancias de hello nodo proceso toolaunch. Si está ejecutando la aplicación en máquinas virtuales más grandes que tienen varios núcleos, es una buena idea toomaximize los recursos estableciendo un valor más alto aquí.
* Hola "inspeccionar" matriz especifica todos los archivos que desee toorestart el proceso del nodo de Hola para cuando cambian.
* Para "watch_options" Hola, actualmente debe toospecify "usePolling" como true debido a la manera de hello que está montado el contenido de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
* [¿Qué es Web App on Linux de Azure?](app-service-linux-intro.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
