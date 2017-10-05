---
title: "Configuración de Emulator Express para depurar aplicaciones de Cloud Services en Visual Studio | Microsoft Docs"
description: "Explica cómo instalar el paquete redistribuible de C++ para habilitar Emulator Express en Visual Studio"
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="b7047-103">Uso de Emulator Express para depurar una aplicación de Cloud Services en VS 2017</span><span class="sxs-lookup"><span data-stu-id="b7047-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="b7047-104">Este artículo explica cómo usar Emulator Express para depurar aplicaciones de Cloud Services en VS 2017.</span><span class="sxs-lookup"><span data-stu-id="b7047-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="b7047-105">Información contextual</span><span class="sxs-lookup"><span data-stu-id="b7047-105">Background context</span></span>
<span data-ttu-id="b7047-106">Emulator Express se utiliza de forma predeterminada para la depuración de roles web y de trabajo de Cloud Services en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7047-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="b7047-107">Esta configuración se especifica en la página de propiedades del proyecto de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="b7047-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Apertura de las propiedades del proyecto][0]

![Emulator Express se selecciona como predeterminado][1]

<span data-ttu-id="b7047-110">El [Visual C++ Redistributable] [ Visual C++ Redistributable] para Visual Studio es necesario con el emulador de express.</span><span class="sxs-lookup"><span data-stu-id="b7047-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="b7047-111">Actualmente no está instalado con la carga de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7047-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="b7047-112">Al presionar F5 para depurar las aplicaciones de Cloud Services, Visual Studio preguntará por la instalación de este componente y continuará con la depuración.</span><span class="sxs-lookup"><span data-stu-id="b7047-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Pregunta para instalar el paquete redistribuible de C++][2]

<span data-ttu-id="b7047-114">Haga click en Sí para instalar el paquete redistribuible de C++.</span><span class="sxs-lookup"><span data-stu-id="b7047-114">Click Yes to install C++ Redistributable.</span></span>

![Instalación del paquete redistribuible de C++][3]

<span data-ttu-id="b7047-116">Presione F5 de nuevo para iniciar sesiones de depuración.</span><span class="sxs-lookup"><span data-stu-id="b7047-116">Press F5 again to launch debugging sessions.</span></span>

![Iniciar la depuración][4]

![Depuración correcta][5]

> <span data-ttu-id="b7047-119">Nota: La instalación del paquete redistribuible de Visual C++ se realiza una sola vez.</span><span class="sxs-lookup"><span data-stu-id="b7047-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="b7047-120">Si se actualiza desde una versión anterior del SDK de Azure y ya tiene instalado Emulator Express, no se encontrará con este problema.</span><span class="sxs-lookup"><span data-stu-id="b7047-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="b7047-121">Solución alternativa manual</span><span class="sxs-lookup"><span data-stu-id="b7047-121">Manual workaround</span></span>
<span data-ttu-id="b7047-122">También puede instalar el [Visual C++ Redistributable] [ Visual C++ Redistributable] manualmente y el mismo efecto se aplicará según cómo Visual Studio instalada en el sistema.</span><span class="sxs-lookup"><span data-stu-id="b7047-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="b7047-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="b7047-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="b7047-124">[Vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="b7047-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7047-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7047-125">Next Steps</span></span>
<span data-ttu-id="b7047-126">Más información sobre cómo usar el emulador de cálculo de Azure para depurar las aplicaciones de servicios en la nube en Visual Studio: [utilizar Emulator Express para ejecutar y depurar un servicio de nube en un equipo local][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="b7047-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
