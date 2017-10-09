---
title: aaaSet un entorno de desarrollo para Azure microservicios | Documentos de Microsoft
description: "Instalar en tiempo de ejecución de hello, SDK y herramientas y crear un clúster de desarrollo local. Después de completar la instalación, estará listo toobuild aplicaciones."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Preparación del entorno de desarrollo
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild y ejecute [aplicaciones de Azure Service Fabric] [ 1] en el equipo de desarrollo, instale en tiempo de ejecución de hello, SDK y herramientas. También debe tooenable ejecución de scripts de Windows PowerShell de hello incluidos en hello SDK.

## <a name="prerequisites"></a>Requisitos previos
### <a name="supported-operating-system-versions"></a>Versiones de sistemas operativos compatibles
Hola siguientes versiones de sistema operativo es compatibles para el desarrollo:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 solo incluye de forma predeterminada Windows PowerShell 2.0. Los cmdlets de PowerShell de Service Fabric requieren PowerShell 3.0 o superior. También puede [descargar Windows PowerShell 5.0] [ powershell5-download] de hello Microsoft Download Center.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Instalar Hola SDK y herramientas
### <a name="toouse-visual-studio-2017"></a>toouse 2017 de Visual Studio
Herramientas del servicio de Fabric forman parte de la carga de trabajo de hello administración y desarrollo de Azure en Visual Studio de 2017. Habilite esta carga de trabajo durante la instalación de Visual Studio.
Además, necesitará tooinstall Hola Microsoft Azure Service Fabric SDK, mediante el instalador de plataforma Web.

* [Instalar SDK del servicio de Microsoft Azure Fabric Hola][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (requiere Visual Studio 2015 Update 2 o posterior)
Para Visual Studio 2015, herramientas de Service Fabric se instalan junto con el SDK, con el instalador de plataforma Web de Hola Hola:

* [Instalar SDK del servicio de Microsoft Azure Fabric hello y herramientas][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Para instalar solamente el SDK
Si solo necesita Hola SDK, puede instalar este paquete:
* [Instalar SDK del servicio de Microsoft Azure Fabric Hola][core-sdk]

las versiones actuales de Hello son:
* SDK de Service Fabric 2.7.198
* Runtime de Service Fabric 5.7.198
* Herramientas de Service Fabric para Visual Studio 2015 1.7.50721
* Visual Studio 2017 Update 2 incluye Herramientas de Service Fabric para Visual Studio 1.6.20170504
* Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) incluye Herramientas de Service Fabric para Visual Studio 1.7.20170721

Para obtener una lista de las versiones admitidas, consulte [Compatibilidad con Service Fabric](service-fabric-support.md).

## <a name="enable-powershell-script-execution"></a>Habilitar la ejecución del script de PowerShell
Service Fabric usa scripts de Windows PowerShell para crear un clúster de desarrollo local e implementar aplicaciones desde Visual Studio. De forma predeterminada, Windows bloquea la ejecución de estos scripts. tooenable usarlas, debe modificar la directiva de ejecución de PowerShell. Abra PowerShell como administrador y escriba Hola siguiente comando:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha terminado la configuración del entorno de desarrollo, puede empezar a compilar y ejecutar aplicaciones.

* [Creación de la primera aplicación de Service Fabric en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Obtenga información acerca de cómo toodeploy y administrar aplicaciones en el clúster local](service-fabric-get-started-with-a-local-cluster.md)
* [Obtener información sobre los modelos de programación de hello: servicios de confianza y actores confiable](service-fabric-choose-framework.md)
* [Extraer del repositorio Hola Service Fabric ejemplos de código en GitHub](https://aka.ms/servicefabricsamples)
* [Visualización del clúster mediante el Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md)
* [Siga hello tooget de ruta de acceso de aprendizaje de una plataforma de toohello introducción amplia de Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Página de campaña de Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Vínculo de WebPI de VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Vínculo de WebPI de Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Vínculo de WebPI de SDK de núcleo"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
