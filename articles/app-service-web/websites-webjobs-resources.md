---
title: "recursos de documentación de WebJobs de aaaAzure"
description: "Recomienda recursos para aprender cómo toouse WebJobs de Azure y Hola SDK de WebJobs de Azure."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Recursos de documentación de WebJobs de Azure
## <a name="overview"></a>Información general
Este tema contiene vínculos a recursos toodocumentation acerca de cómo toouse WebJobs de Azure y Hola SDK de WebJobs de Azure. WebJobs de Azure proporcionan un secuencias de comandos de toorun de forma sencilla o programas como en segundo plano procesos en el contexto de Hola de un [aplicación de servicio de aplicaciones web, una aplicación de API o aplicación móvil](../app-service/app-service-value-prop-what-is.md). Puede cargar y ejecutar un archivo ejecutable como cmd, bat, exe (.NET), ps1, sh, php, py, js y jar. Estos programas se ejecutan como WebJobs según una programación (cron) o de forma continua.

Hola propósito de hello [SDK de WebJobs](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) es código de hello toosimplify que se escribe para las tareas comunes que puede realizar un trabajo Web, como procesamiento de imágenes, procesamiento de colas, agregación de RSS, mantenimiento del archivo y enviar mensajes de correo electrónico. Hola SDK de WebJobs tiene características integradas para trabajar con el almacenamiento de Azure y Bus de servicio, para programar tareas y control de errores y para muchos otros escenarios comunes. Además, ha diseñado toobe extensible y no hay un [repositorio de código abierto para las extensiones](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Las funciones de Azure](../azure-functions/functions-overview.md) (actualmente en versión preliminar) se basa en una versión de Hola SDK de WebJobs que funciona con C# script, Node.js y otros lenguajes. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

La creación, implementación y administración de WebJobs se realiza de manera fluida gracias al conjunto de herramientas integradas en Visual Studio. Puede crear WebJobs a partir de plantillas, así como publicarlos y administrarlos (procesos de ejecución, detención, supervisión o depuración). 

panel de WebJobs de Hola Hola portal de Azure proporciona capacidades de administración eficaces que ofrecen un control total sobre la ejecución de Hola de trabajos Web, incluidas capacidad de hello tooinvoke funciones individuales dentro de trabajos Web. panel de Hola también muestra los tiempos de ejecución de función y la salida del registro. 

## <a name="getstarted"></a>Introducción a los trabajos Web y Hola SDK de WebJobs
* [Introducción tooAzure trabajos Web](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Azure WebJobs are awesome and you should start using them right now! (¡Los WebJobs de Azure son impresionantes y debería comenzar a usarlos ya!) (¡Los WebJobs de Azure son impresionantes y debería comenzar a usarlos ya!)](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Blog publicado por Troy Hunt.)
* [Características de WebJobs de Azure](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [¿Qué es hello SDK de WebJobs](websites-dotnet-webjobs-sdk.md)
* [Orientación sobre trabajos en segundo plano: Microsoft Patterns and Practices](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Anuncio de Hola 1.1.0 RTM de Microsoft Azure SDK de WebJobs](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Empezar a trabajar con hello SDK de WebJobs de Azure](websites-dotnet-webjobs-sdk-get-started.md)
* [¿Cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [¿Cómo toouse Azure blob storage con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Cómo toouse de Bus de servicio de Azure con Hola SDK de WebJobs](websites-dotnet-webjobs-sdk-service-bus.md)
* [Referencia rápida del SDK de WebJobs de Azure (descarga de PDF)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Documentación de configuración de WebJobs en GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Vídeos
  * [Los trabajos Web y Hola SDK de WebJobs](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Serie de vídeos de WebJobs de Azure en Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Presentación del conjunto de herramientas de WebJobs de Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Herramientas de WebJobs y depuración remota](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Azure WebJobs Update with Pranav Rastogi - Extensibility in Release 1.1 (Actualización de WebJobs de Azure con Pranav Rastogi: Extensibilidad en la versión 1.1)](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Vea también Hola siguientes secciones [implementar trabajos Web](#deploy) y [pruebas y depuración de trabajos Web](#debug).

## <a name="deploy"></a>Implementación de WebJobs
* [Cómo tooDeploy WebJobs de Azure con Visual Studio](websites-dotnet-deploy-webjobs.md)
* [¿Cómo uso de WebJobs de toodeploy Hola Portal de Azure](web-sites-create-web-jobs.md)
* [Habilitación de la línea de comandos o entrega continua de WebJobs de Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Implementar un tooAzure de aplicación de consola .NET mediante trabajos Web de GIT](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Implementar un tooAzure de F # WebJob](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Deploying custom services as Azure Webjobs (Implementación de servicios  personalizados como Webjobs de Azure](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Vídeos
  * [Presentación del conjunto de herramientas de WebJobs de Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Herramientas de WebJobs y depuración remota](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Programación de WebJobs
* [Hello Azure trabajo Web cuadro de diálogo Agregar](websites-dotnet-deploy-webjobs.md#configure)
* [Crear un trabajo Web programado en hello Portal de Azure](web-sites-create-web-jobs.md#CreateScheduled)
* [Enlazar un tooa de trabajo de programador trabajo Web](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Programación de WebJobs de Azure con expresiones cron](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Programación de cada función de trabajo Web con hello TimerTrigger de SDK de WebJobs](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Prueba y depuración de WebJobs
* [Nuevas características para desarrolladores y depuración de WebJobs de Azure en Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Hola de vista panel de WebJobs](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Cómo registros toowrite con SDK de WebJobs de Hola y verlos en el panel de Hola](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [WebJobs de depuración remota](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [¿Quién escribió ese blob?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Código interactivo en hello en la nube de hospedaje](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Agregar seguimiento tooAzure trabajos Web](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Supervisión, diagnóstico y solución de problemas de Almacenamiento de Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Vídeos
  * [Herramientas de WebJobs y depuración remota](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Escalado de WebJobs
* [Escalado de su aplicación web con Sitios web de Azure](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Arquitectura de aplicaciones web de gran escala listas para los negocios](https://channel9.msdn.com/Events/Build/2014/3-626). Portadas ajuste de escala de las aplicaciones web con trabajos Web, incluidos Hola SDK de WebJobs.
* Vídeos
  * [Escalado horizontal de WebJobs](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Recursos adicionales de WebJobs
* [Entrada de blog sobre disponibilidad general de WebJobs de Azure por Magnus Mårtensson](http://magnusmartensson.com/azure-webjobs-ga)
* [Ejecución de WebJobs de PowerShell en Sitios web de Azure](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Recepción de notificación cuando se completen los WebJobs desencadenados en Azure](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Directiva sencilla de retención de copia de seguridad de sitio web con WebJobs](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Sitios web y Servicios en la nube de Microsoft Azure lentos en la primera solicitud](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Muestra cómo toouse WebJobs toosimulate Hola característica AlwaysOn que solo está disponible para el nivel de precios estándar Hola.
* [Cierre estable de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Para obtener información sobre el cierre estable de SDK de WebJobs, consulte [Cierre estable](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
* [Automatización de las copias de seguridad con Azure WebJobs y AzCopy](http://markjbrown.com/azure-webjobs-azcopy/)
* Vídeos
  * [Vídeos de WebJobs de Azure por Magnus Mårtensson](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Serie de vídeos de WebJobs de Azure en Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Recursos adicionales de SDK de WebJobs
* [Notas de la versión del SDK de WebJobs](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [Código fuente del SDK de WebJobs](https://github.com/Azure/azure-webjobs-sdk)
* [El código fuente de las extensiones de SDK de WebJobs](https://github.com/Azure/azure-webjobs-sdk-extensions), con [modelo de extensibilidad de guía detallada toohello](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [Código fuente del script del SDK de WebJobs](https://github.com/Azure/azure-webjobs-sdk-script/) (utilizado para [Azure Functions](../azure-functions/functions-overview.md))
* [Uso de almacenamiento de tooAzure de trabajo Web tooupload FREB archivos Hola SDK de WebJobs](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Hospedaje de webjobs de Azure fuera de Azure, con hello registro ventajas de un Azure hospedado trabajo Web](http://bypassion.dk/?p=510)
* [Creación de una herramienta de importación de datos con WebJobs de Azure](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Información general sobre Funciones de Azure](../azure-functions/functions-overview.md)
* Vídeos
  * [Serie de vídeos de WebJobs de Azure en Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Aplicaciones de WebJob de ejemplo
* [Aplicaciones de ejemplo proporcionadas por el equipo de WebJobs de hello en GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Aplicación Web de Azure simple con WebJobs Backend con hello SDK de WebJobs](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Muestra el uso de WebJobs programados y controlados por eventos. Consulte el blog de hello [volver a generar hello SiteMonitR mediante el SDK de WebJobs de Azure](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogs
* [Blog sobre Azure](/blog)
* [Blog de Amit Apple](http://blog.amitapple.com/) Se centra en los trabajos Web (no Hola SDK).
* [Blog de Magnus Mårtensson](http://magnusmartensson.com/)

## <a name="gethelp"></a>Ayuda de WebJobs
* [StackOverflow para WebJobs](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow para hello SDK de WebJobs](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow para Funciones de Azure](http://stackoverflow.com/questions/tagged/azure-functions)
* [Foro de Azure y ASP.NET](http://forums.asp.net/1247.aspx)
* [Foro de aplicaciones web del Servicio de aplicaciones de Azure](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Sitio para el usuario de Aplicaciones web de Azure](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Utilice hello hashtag #AzureWebJobs.
* [Report a WebJobs bug or issue (Notificar un problema o error de WebJobs)](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

