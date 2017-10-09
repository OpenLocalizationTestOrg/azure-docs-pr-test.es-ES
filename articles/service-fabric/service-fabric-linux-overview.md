---
title: aaaAzure Service Fabric en Linux | Documentos de Microsoft
description: "Los clústeres de Service Fabric admiten Linux y Java, lo que significa que sea capaz de toodeploy y aplicaciones de Service Fabric host escritas en Java y C# en Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="7f284-103">Service Fabric en Azure</span><span class="sxs-lookup"><span data-stu-id="7f284-103">Service Fabric on Linux</span></span>
<span data-ttu-id="7f284-104">vista previa de Hola de Service Fabric en Linux permite toobuild, implementar y administrar las aplicaciones de alta disponibilidad, altamente escalables en Linux tal como haría en Windows.</span><span class="sxs-lookup"><span data-stu-id="7f284-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="7f284-105">los marcos de trabajo de Service Fabric de Hello (servicios de confianza y actores confiable) están disponibles en Java en Linux en suma tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="7f284-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="7f284-106">Puede compilar igualmente [servicios ejecutables invitados](service-fabric-deploy-existing-app.md) con cualquier lenguaje o marco.</span><span class="sxs-lookup"><span data-stu-id="7f284-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="7f284-107">Además, vista previa de hello también admite la organización de los contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="7f284-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="7f284-108">Contenedores de docker pueden ejecutar archivos ejecutables de invitado o servicios de Service Fabric nativos, que utilizan los marcos de trabajo de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="7f284-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="7f284-109">Service Fabric en Linux es conceptualmente equivalente tooService Fabric en Windows (excepto para obtener información específica del sistema operativo y la compatibilidad con lenguajes de programación).</span><span class="sxs-lookup"><span data-stu-id="7f284-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="7f284-110">Por lo tanto, la mayoría de nuestras [documentación existente](http://aka.ms/servicefabricdocs) se aplica en ayudar a familiarizarse con la tecnología de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f284-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="7f284-111">Sistemas operativos y lenguajes de programación compatibles</span><span class="sxs-lookup"><span data-stu-id="7f284-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="7f284-112">Hola limitado preview admite Hola la creación de desarrollo de un solo cuadro además clústeres clústeres de máquina toomulti en Azure ejecutando Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="7f284-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="7f284-113">admite la vista previa Hola Hola Reliable Actors y Hola marcos de trabajo de servicios sin estado confiables en Java y C# en los archivos ejecutables de suma tooguest y orquestar contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="7f284-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="7f284-114">Reliable Collections aún no es compatible con Linux.</span><span class="sxs-lookup"><span data-stu-id="7f284-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="7f284-115">No se admiten clústeres solo stand-sólo un cuadro y clústeres de varios equipos de Linux de Azure se admiten en la vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f284-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="7f284-116">Herramientas compatibles</span><span class="sxs-lookup"><span data-stu-id="7f284-116">Supported tooling</span></span>
<span data-ttu-id="7f284-117">vista previa de Hello admite la interacción con el clúster de Hola a través de la CLI de tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="7f284-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="7f284-118">Para los desarrolladores de Java, se proporciona integración con Eclipse y Yeoman mediante compatibilidad de Eclipse en Linux y OSX.</span><span class="sxs-lookup"><span data-stu-id="7f284-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="7f284-119">Hola integración OSX utiliza una VM Linux bajo el paraguas de Hola a través de vagrant.</span><span class="sxs-lookup"><span data-stu-id="7f284-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="7f284-120">Para los desarrolladores de C#, la integración con Yeoman se proporciona plantillas de aplicación toogenerate.</span><span class="sxs-lookup"><span data-stu-id="7f284-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f284-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f284-121">Next steps</span></span>

* <span data-ttu-id="7f284-122">Familiarizarse con hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) y [servicios confiables](service-fabric-reliable-services-introduction.md) marcos de trabajo de programación</span><span class="sxs-lookup"><span data-stu-id="7f284-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="7f284-123">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="7f284-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="7f284-124">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="7f284-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="7f284-125">Create your first Service Fabric Java application on Linux</span><span class="sxs-lookup"><span data-stu-id="7f284-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="7f284-126">[Setup Service Fabric continuous integration and deployment with Jenkins and GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md) (Configurar la integración continua y la implementación de Service Fabric con Jenkins y GitHub)</span><span class="sxs-lookup"><span data-stu-id="7f284-126">[Setup Service Fabric continuous integration and deployment with Jenkins and GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)</span></span>
* [<span data-ttu-id="7f284-127">Diferencias entre Service Fabric para Windows y para Linux</span><span class="sxs-lookup"><span data-stu-id="7f284-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
