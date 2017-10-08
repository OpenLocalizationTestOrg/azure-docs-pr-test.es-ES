---
title: "aaaManage una aplicación web en el servicio de aplicación de Azure"
description: "Tooresources de vínculos para administrar una aplicación web en el servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Administración de una aplicación web en Servicio de aplicaciones de Azure
Este tema contiene vínculos tooresources para administrar una aplicación web en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714). La administración incluye todas las tareas de Hola que mantener la aplicación web que se ejecuta sin problemas. 

Sobre Hola mientras dura una aplicación web, realizará las tareas de administración diferente, al pasar de las actualizaciones, el mantenimiento y el funcionamiento de toonormal de implementación inicial.

Muchas tareas de administración de la aplicación web pueden realizarse en hello Portal de Azure.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Antes de implementar su tooproduction de aplicación web
### <a name="choose-a-tier"></a>Elija un nivel
Servicio de aplicaciones de Azure se ofrece en cinco niveles: gratis, compartido, básico, estándar y premium. Para obtener información sobre las características de Hola y precios para cada nivel, consulte [detalles de precios](https://azure.microsoft.com/pricing/details/app-service/). 

* [Planes de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) permiten agrupar varias aplicaciones web en hello mismo nivel.
* Siempre puede [cambiar los niveles](web-sites-scale.md) después de crear su aplicación web.

### <a name="configuration"></a>Configuración
Hola de uso [Portal de Azure](https://portal.azure.com/) tooset distintas opciones de configuración. Para obtener detalles, consulte [Configuración de aplicaciones en el Servicio de aplicaciones de Azure](web-sites-configure.md). Esta es una lista de comprobación breve:

* Seleccione **versiones de tiempo de ejecución** para .NET, PHP, Java o Python, si es necesario.
* Habilitar **WebSockets** si la aplicación web usa el protocolo de WebSocket de Hola. (Se incluyen las aplicaciones que usan [ASP.NET SignalR](http://www.asp.net/signalr) o [socket.io](web-sites-nodejs-chat-app-socketio.md)).
* ¿Ejecuta trabajos web continuamente? Si es así, habilite la opción **Always On**.
* Conjunto hello **documento predeterminado**, como index.html.

En suma toothese configuración básica, puede que desee siguiente de Hola tooconfigure:

* **Capa de sockets seguros (SSL)** . toouse SSL con un nombre de dominio personalizado, debe obtener una SSL de certificados y configurar su toouse de aplicación web se. Consulte [Habilitación de HTTPS para una aplicación web en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-ssl.md).
* **Nombre de dominio personalizado.** Su aplicación web tiene automáticamente un subdominio en azurewebsites.net. Puede asociar un nombre de dominio personalizado, como contoso.com. Consulte [Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-domain.md).

Configuración específica por idioma:

* **PHP**: [configuración de PHP en Aplicaciones web del Servicio de aplicaciones de Azure](web-sites-php-configure.md).
* **Python**: [configuración de Python con Aplicaciones web del Servicio de aplicaciones de Azure](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Cuando su aplicación web está en ejecución
Mientras se ejecuta la aplicación web, desea toomake que está disponible y se escala toomeet tráfico de usuario. También puede que tenga errores de tootroubleshoot.

### <a name="monitoring"></a>Supervisión
* A través de hello Portal de Azure, también puede [agregar las métricas de rendimiento](web-sites-monitor.md) como el uso de CPU y el número de solicitudes de cliente.
* [Escalar la aplicación web](web-sites-scale.md) en tootraffic de respuesta. Dependiendo de la capa, puede escalar número de Hola de máquinas virtuales o el tamaño de Hola de instancias de máquina virtual de Hola. En hello estándar y niveles de Premium, también puede configurar escalado automático, por lo que la aplicación web se escala automáticamente, según una programación fija o en tooload de respuesta.  

### <a name="backups"></a>Copias de seguridad
* Establezca las [copias de seguridad automáticas](web-sites-backup.md) de la aplicación web. Obtenga más información sobre las copias de seguridad en [este vídeo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Obtenga información acerca de las opciones de Hola para [recuperación de la base de datos](../sql-database/sql-database-business-continuity.md) en la base de datos de SQL Azure.

### <a name="troubleshooting"></a>Solución de problemas
* Si algo va mal, puede [solución de problemas en Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), usando los registros de diagnóstico y depuración en la nube de hello activa. 
* Fuera de Visual Studio, hay varios registros de diagnóstico de toocollect maneras. Consulte [Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-enable-diagnostic-log.md).
* Para las aplicaciones Node.js, vea [cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Restauración de datos
* [Restaure](web-sites-restore.md) una aplicación web de la que se creó una copia de seguridad anteriormente.

## <a name="when-you-update-your-web-app"></a>Cuando actualiza la aplicación web
Si no ha habilitado las copias de seguridad automáticas, puede crear una [copia de seguridad manual](web-sites-backup.md).

Puede usar una [implementación de ensayo](web-sites-staged-publishing.md). Esta opción le permite publicar tooa actualizaciones implementación que se ejecuta en paralelo de ensayo con la implementación de producción. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


