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
# <a name="service-fabric-on-linux"></a>Service Fabric en Azure
vista previa de Hola de Service Fabric en Linux permite toobuild, implementar y administrar las aplicaciones de alta disponibilidad, altamente escalables en Linux tal como haría en Windows. los marcos de trabajo de Service Fabric de Hello (servicios de confianza y actores confiable) están disponibles en Java en Linux en suma tooC # (.NET Core).  Puede compilar igualmente [servicios ejecutables invitados](service-fabric-deploy-existing-app.md) con cualquier lenguaje o marco. Además, vista previa de hello también admite la organización de los contenedores de Docker. Contenedores de docker pueden ejecutar archivos ejecutables de invitado o servicios de Service Fabric nativos, que utilizan los marcos de trabajo de Service Fabric Hola.

Service Fabric en Linux es conceptualmente equivalente tooService Fabric en Windows (excepto para obtener información específica del sistema operativo y la compatibilidad con lenguajes de programación). Por lo tanto, la mayoría de nuestras [documentación existente](http://aka.ms/servicefabricdocs) se aplica en ayudar a familiarizarse con la tecnología de Hola.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Sistemas operativos y lenguajes de programación compatibles
Hola limitado preview admite Hola la creación de desarrollo de un solo cuadro además clústeres clústeres de máquina toomulti en Azure ejecutando Ubuntu Server 16.04. admite la vista previa Hola Hola Reliable Actors y Hola marcos de trabajo de servicios sin estado confiables en Java y C# en los archivos ejecutables de suma tooguest y orquestar contenedores de Docker.  

> [!NOTE]
> Reliable Collections aún no es compatible con Linux. No se admiten clústeres solo stand-sólo un cuadro y clústeres de varios equipos de Linux de Azure se admiten en la vista previa de Hola.
>
>


## <a name="supported-tooling"></a>Herramientas compatibles
vista previa de Hello admite la interacción con el clúster de Hola a través de la CLI de tejido de servicio. Para los desarrolladores de Java, se proporciona integración con Eclipse y Yeoman mediante compatibilidad de Eclipse en Linux y OSX. Hola integración OSX utiliza una VM Linux bajo el paraguas de Hola a través de vagrant. Para los desarrolladores de C#, la integración con Yeoman se proporciona plantillas de aplicación toogenerate.

## <a name="next-steps"></a>Pasos siguientes

* Familiarizarse con hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) y [servicios confiables](service-fabric-reliable-services-introduction.md) marcos de trabajo de programación
* [Prepare your development environment on Linux](service-fabric-get-started-linux.md)
* [Prepare your development environment on OSX](service-fabric-get-started-mac.md)
* [Create your first Service Fabric Java application on Linux](service-fabric-create-your-first-linux-application-with-java.md)
* [Setup Service Fabric continuous integration and deployment with Jenkins and GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md) (Configurar la integración continua y la implementación de Service Fabric con Jenkins y GitHub)
* [Diferencias entre Service Fabric para Windows y para Linux](service-fabric-linux-windows-differences.md)
