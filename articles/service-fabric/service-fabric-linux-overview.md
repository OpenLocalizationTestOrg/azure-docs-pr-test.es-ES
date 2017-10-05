---
title: Azure Service Fabric en Linux | Microsoft Docs
description: "Los clústeres de Service Fabric admiten Linux y Java, lo que significa que podrá implementar y hospedar aplicaciones de Service Fabric escritas en Java y C# para Linux."
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
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="4b832-103">Service Fabric en Azure</span><span class="sxs-lookup"><span data-stu-id="4b832-103">Service Fabric on Linux</span></span>
<span data-ttu-id="4b832-104">La versión preliminar de Service Fabric en Linux permite compilar, implementar y administrar aplicaciones de alta disponibilidad y escalabilidad en ese entorno de la misma forma que en Windows.</span><span class="sxs-lookup"><span data-stu-id="4b832-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="4b832-105">Los marcos de Service Fabric (Reliable Services y Reliable Actors) se encuentran disponibles en Java en Linux, además de en C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="4b832-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="4b832-106">Puede compilar igualmente [servicios ejecutables invitados](service-fabric-deploy-existing-app.md) con cualquier lenguaje o marco.</span><span class="sxs-lookup"><span data-stu-id="4b832-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="4b832-107">Además, la vista previa también admite contenedores de Docker de organización.</span><span class="sxs-lookup"><span data-stu-id="4b832-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="4b832-108">Los contenedores de Docker pueden ejecutar archivos ejecutables invitados o servicios de Service Fabric nativos que utilizan los marcos de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4b832-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="4b832-109">Service Fabric en Linux es conceptualmente equivalente a Service Fabric en Windows (excepto las características del sistema operativo y la compatibilidad con lenguajes de programación).</span><span class="sxs-lookup"><span data-stu-id="4b832-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="4b832-110">Por lo tanto, la mayoría de nuestra [documentación actual](http://aka.ms/servicefabricdocs) tiene como objetivo ayudarlo a familiarizarse con la tecnología.</span><span class="sxs-lookup"><span data-stu-id="4b832-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="4b832-111">Sistemas operativos y lenguajes de programación compatibles</span><span class="sxs-lookup"><span data-stu-id="4b832-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="4b832-112">La versión preliminar limitada admite la creación de clústeres de desarrollo one-box, así como clústeres de varias máquinas en Azure con Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="4b832-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="4b832-113">La vista previa es compatible con los marcos de Reliable Actors y Reliable Stateless Services en Java y C#, además de los archivos ejecutables invitados y los contenedores de Docker de organización.</span><span class="sxs-lookup"><span data-stu-id="4b832-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="4b832-114">Reliable Collections aún no es compatible con Linux.</span><span class="sxs-lookup"><span data-stu-id="4b832-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="4b832-115">No son compatibles tampoco los clústeres independientes: solo se admiten clústeres one box y de varios equipos de Linux de Azure en la vista previa.</span><span class="sxs-lookup"><span data-stu-id="4b832-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="4b832-116">Herramientas compatibles</span><span class="sxs-lookup"><span data-stu-id="4b832-116">Supported tooling</span></span>
<span data-ttu-id="4b832-117">La versión preliminar admite la interacción con el clúster a través de la CLI de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4b832-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="4b832-118">Para los desarrolladores de Java, se proporciona integración con Eclipse y Yeoman mediante compatibilidad de Eclipse en Linux y OSX.</span><span class="sxs-lookup"><span data-stu-id="4b832-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="4b832-119">La integración de OSX utiliza una máquina virtual de Linux de forma interna mediante vagrant.</span><span class="sxs-lookup"><span data-stu-id="4b832-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="4b832-120">Para los desarrolladores de C#, se proporciona integración con Yeoman para generar plantillas de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b832-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b832-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b832-121">Next steps</span></span>

* <span data-ttu-id="4b832-122">Familiarícese con los marcos de programación de [Reliable Actors](service-fabric-reliable-actors-introduction.md) y [Reliable Services](service-fabric-reliable-services-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4b832-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="4b832-123">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="4b832-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="4b832-124">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="4b832-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="4b832-125">Create your first Service Fabric Java application on Linux</span><span class="sxs-lookup"><span data-stu-id="4b832-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="4b832-126">[Setup Service Fabric continuous integration and deployment with Jenkins and GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md) (Configurar la integración continua y la implementación de Service Fabric con Jenkins y GitHub)</span><span class="sxs-lookup"><span data-stu-id="4b832-126">[Setup Service Fabric continuous integration and deployment with Jenkins and GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)</span></span>
* [<span data-ttu-id="4b832-127">Diferencias entre Service Fabric para Windows y para Linux</span><span class="sxs-lookup"><span data-stu-id="4b832-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
