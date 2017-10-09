---
title: "implementación de aaaAutomate de la aplicación de Azure con las herramientas de línea de comandos | Documentos de Microsoft"
description: "Detectar información sobre cómo puede implementar la aplicación de Azure de Hola de línea de comandos"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Automatización de la implementación de la aplicación de Azure con las herramientas de la línea de comandos
Puede automatizar la implementación de las aplicaciones de Azure con las herramientas de línea de comandos. Este artículo enumeran las herramientas disponibles y vínculos útiles de Hola que le muestran cómo toouse ellas en el flujo de trabajo de implementación. 

## <a name="msbuild"></a>Automatización de la implementación con MSBuild
Si usas hello [IDE de Visual Studio](#vs) para el desarrollo, puede usar [MSBuild](http://msbuildbook.com/) tooautomate cualquier cosa que puede hacer en el IDE. Puede configurar MSBuild toouse o [Web Deploy](#webdeploy) o [FTP o FTPS](#ftp) toocopy archivos. Web Deploy también puede automatizar muchas otras tareas relacionadas con la implementación, como implementar bases de datos.

Para obtener más información acerca de la implementación de línea de comandos con MSBuild, vea Hola recursos siguientes:

* [Implementación web de ASP.NET con Visual Studio: Implementación de línea de comandos](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Décimo argumento de una serie de tutoriales sobre tooAzure de implementación mediante Visual Studio. Muestra cómo toouse Hola toodeploy de línea de comandos después de configurar los perfiles de publicación en Visual Studio.
* [Hola interior Microsoft Build Engine: usar MSBuild y Team Foundation Build](http://msbuildbook.com/). Libro de copia de disco duro que incluye capítulos sobre cómo toouse MSBuild para la implementación.

## <a name="powershell"></a>Automatización de la implementación con Windows PowerShell
Desde [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx)puede ejecutar funciones de implementación MSBuild o FTP. Si lo hace, también puede utilizar una colección de cmdlets de Windows PowerShell que realizan toocall fácil del API de administración de hello REST de Azure.

Para obtener más información, vea Hola recursos siguientes:

* [Implementar un repositorio de GitHub de web app vinculado tooa](app-service-web-arm-from-github-provision.md)
* [Aprovisionamiento de una aplicación web con una base de datos SQL](app-service-web-arm-with-sql-database-provision.md)
* [Aprovisionamiento e implementación predecibles de microservicios en Azure](app-service-deploy-complex-application-predictably.md)
* <seg>
  [Creación de aplicaciones reales en la nube con Azure: automatizar todo](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything).</seg> Capítulo de libro electrónico que explica cómo la aplicación de ejemplo de Hola se muestra en el libro electrónico hello usa toocreate de secuencias de comandos de Windows PowerShell un Azure entorno de prueba e implementar tooit. Vea hello [recursos](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) sección para vínculos tooadditional documentación de PowerShell de Azure.
* [Usar Scripts de Windows PowerShell tooPublish tooDev y entornos de prueba](../vs-azure-tools-publishing-using-powershell-scripts.md). Cómo toouse implementación de Windows PowerShell scripts que Visual Studio genera.

## <a name="api"></a>Automatización de la implementación con la API de administración de .NET
Puede escribir código C# tooperform funciones de MSBuild o FTP para la implementación. Si lo hace, puede tener acceso a funciones de administración de sitio de tooperform API de REST de administración de Azure de Hola.

Para obtener más información, vea Hola siguientes recursos:

* [Automatizar todo el contenido con las bibliotecas de administración de Azure de Hola y. NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Introducción toohello .NET documentación de administración de API y los vínculos toomore.

## <a name="cli"></a>Implementación desde la interfaz de la línea de comandos de Azure (CLI de Azure)
Puede usar la línea de comandos de hello en Windows, Mac o Linux toodeploy máquinas mediante FTP. Si lo hace, también puede tener acceso a API de administración de Azure REST hello mediante Hola CLI de Azure.

Para obtener más información, vea Hola siguientes recursos:

* [Herramientas de línea de comandos de Azure](https://azure.microsoft.com/downloads/). Página de portal en Azure.com para obtener información sobre la herramienta de línea de comandos.

## <a name="webdeploy"></a>Implementación desde la línea de comandos de Web Deploy
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) es un software de Microsoft para tooIIS de implementación que no solo ofrece inteligente de archivos características de sincronización, pero también puede realizar o coordinar muchas otras tareas relacionadas con la implementación que no se pueden automatizar cuando se utiliza FTP. Por ejemplo, Web Deploy puede implementar una base de datos nueva o actualizaciones de base de datos junto con su aplicación web. Web Deploy también puede minimizar Hola tiempo necesario tooupdate un sitio existente porque forma inteligente puede copiar archivos modificados únicamente. Microsoft Visual Studio y Team Foundation Server ofrecen compatibilidad con Web Deploy integrados, pero también puede utilizar Web Deploy directamente desde la implementación de tooautomate de línea de comandos de Hola. Comandos de Web Deploy son muy eficaces pero Hola aprendizaje puede resultarle dificultoso.

## <a name="more-resources"></a>Más recursos
Automatización de línea toocommand otra opción de la implementación es toouse basados en cloud service como [Pulpo implementar](http://en.wikipedia.org/wiki/Octopus_Deploy). Para obtener más información, consulte [tooAzure de las aplicaciones de ASP.NET implementar sitios Web](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Para obtener más información sobre herramientas de línea de comandos, vea Hola siguientes recursos:

* [Aplicaciones web simples: implementación](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Blog de David Ebbo acerca de una herramienta escribió toomake sea más fácil toouse Web Deploy.
* [Herramienta de implementación web](http://technet.microsoft.com/library/dd568996). Documentación oficial en el sitio de Microsoft TechNet Hola. Fecha pero todavía un toostart ideal.
* [Uso de Web Deploy](http://www.iis.net/learn/publish/using-web-deploy). Documentación oficial en el sitio de Microsoft IIS.NET Hola. También fecha pero un buen lugar toostart.
* [Implementación web de ASP.NET con Visual Studio: Implementación de línea de comandos](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild es Visual Studio utilizado el motor de compilación de Hola y también se puede utilizar de hello línea de comandos toodeploy web aplicaciones tooWeb aplicaciones. Este tutorial forma parte de una serie que se refiere principalmente a la implementación de Visual Studio.

