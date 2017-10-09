---
title: emulador de aaaSetup express toodebug aplicaciones de servicios en la nube en Visual Studio | Documentos de Microsoft
description: "Explica cómo tooinstall Hola tooenable redistribuible de C++ Emulator Express en Visual Studio"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Usar Emulator Express aplicación de servicios de nube de toodebug en VS 2017
Este artículo se explica cómo toouse Emulator Express toodebug aplicaciones de servicios en la nube de VS de 2017.

## <a name="background-context"></a>Información contextual
Emulator Express se utiliza de forma predeterminada para la depuración de roles web y de trabajo de Cloud Services en Visual Studio. Esta configuración se especifica en la página de propiedades del proyecto de servicios en la nube de Hola.

![Apertura de las propiedades del proyecto][0]

![Emulator Express se selecciona como predeterminado][1]

Hola [Visual C++ Redistributable] [ Visual C++ Redistributable] para Visual Studio es necesario con el emulador de express. Actualmente no está instalado con hello Azure carga de trabajo. Tras F5 gestos toodebug las aplicaciones de servicios en la nube, Visual Studio podría solicitar tooinstall este componente y continúe con la depuración.

![Pregunta para instalar el paquete redistribuible de C++][2]

Haga clic en Sí tooinstall C++ Redistributable.

![Instalación del paquete redistribuible de C++][3]

Presione F5 de nuevo toolaunch las sesiones de depuración.

![Iniciar la depuración][4]

![Depuración correcta][5]

> Nota: La instalación del paquete redistribuible de Visual C++ se realiza una sola vez. Si se actualiza desde una versión anterior del SDK de Azure y ya tiene instalado Emulator Express, no se encontrará con este problema.
> 
> 

## <a name="manual-workaround"></a>Solución alternativa manual
También puede instalar hello [Visual C++ Redistributable] [ Visual C++ Redistributable] manualmente y el mismo efecto se aplicará según cómo Visual Studio instalada en el sistema.

[vcredist_x86.exe][vcredist_x86.exe]

[Vcredist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de cómo utilizar el emulador de cálculo de Azure toodebug las aplicaciones de servicios en la nube en Visual Studio: [toorun utilizar Emulator Express y depurar un servicio de nube en un equipo local][Using Emulator Express toorun and debug a cloud service on a local machine]

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
