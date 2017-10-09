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
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="779c9-103">Usar Emulator Express aplicación de servicios de nube de toodebug en VS 2017</span><span class="sxs-lookup"><span data-stu-id="779c9-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="779c9-104">Este artículo se explica cómo toouse Emulator Express toodebug aplicaciones de servicios en la nube de VS de 2017.</span><span class="sxs-lookup"><span data-stu-id="779c9-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="779c9-105">Información contextual</span><span class="sxs-lookup"><span data-stu-id="779c9-105">Background context</span></span>
<span data-ttu-id="779c9-106">Emulator Express se utiliza de forma predeterminada para la depuración de roles web y de trabajo de Cloud Services en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="779c9-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="779c9-107">Esta configuración se especifica en la página de propiedades del proyecto de servicios en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="779c9-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Apertura de las propiedades del proyecto][0]

![Emulator Express se selecciona como predeterminado][1]

<span data-ttu-id="779c9-110">Hola [Visual C++ Redistributable] [ Visual C++ Redistributable] para Visual Studio es necesario con el emulador de express.</span><span class="sxs-lookup"><span data-stu-id="779c9-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="779c9-111">Actualmente no está instalado con hello Azure carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="779c9-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="779c9-112">Tras F5 gestos toodebug las aplicaciones de servicios en la nube, Visual Studio podría solicitar tooinstall este componente y continúe con la depuración.</span><span class="sxs-lookup"><span data-stu-id="779c9-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Pregunta para instalar el paquete redistribuible de C++][2]

<span data-ttu-id="779c9-114">Haga clic en Sí tooinstall C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="779c9-114">Click Yes tooinstall C++ Redistributable.</span></span>

![Instalación del paquete redistribuible de C++][3]

<span data-ttu-id="779c9-116">Presione F5 de nuevo toolaunch las sesiones de depuración.</span><span class="sxs-lookup"><span data-stu-id="779c9-116">Press F5 again toolaunch debugging sessions.</span></span>

![Iniciar la depuración][4]

![Depuración correcta][5]

> <span data-ttu-id="779c9-119">Nota: La instalación del paquete redistribuible de Visual C++ se realiza una sola vez.</span><span class="sxs-lookup"><span data-stu-id="779c9-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="779c9-120">Si se actualiza desde una versión anterior del SDK de Azure y ya tiene instalado Emulator Express, no se encontrará con este problema.</span><span class="sxs-lookup"><span data-stu-id="779c9-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="779c9-121">Solución alternativa manual</span><span class="sxs-lookup"><span data-stu-id="779c9-121">Manual workaround</span></span>
<span data-ttu-id="779c9-122">También puede instalar hello [Visual C++ Redistributable] [ Visual C++ Redistributable] manualmente y el mismo efecto se aplicará según cómo Visual Studio instalada en el sistema.</span><span class="sxs-lookup"><span data-stu-id="779c9-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="779c9-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="779c9-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="779c9-124">[Vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="779c9-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="779c9-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="779c9-125">Next Steps</span></span>
<span data-ttu-id="779c9-126">Más información acerca de cómo utilizar el emulador de cálculo de Azure toodebug las aplicaciones de servicios en la nube en Visual Studio: [toorun utilizar Emulator Express y depurar un servicio de nube en un equipo local][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="779c9-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

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
