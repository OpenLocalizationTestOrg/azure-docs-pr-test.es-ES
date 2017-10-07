---
title: "Notas de la versión SDK para .NET 2.5.1 aaaAzure"
description: "Notas de la versión de SDK de Azure para .NET 2.5.1."
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Notas de la versión de SDK de Azure para .NET 2.5.1.
Este documento contiene notas de la versión de Hola para hello Azure SDK para .NET 2.5.1 de la versión. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Notas de la versión de SDK de Azure para .NET 2.5.1.
siguiente Hola es nuevas características y actualizaciones de hello Azure SDK para .NET 2.5.1.

* Nuevas características/escenarios relacionados con demasiado**Web Tools Extensions**. 
  
  * Sitios Web de Azure era tooAzure ha cambiado el nombre de servicio de aplicaciones. Para obtener más información, vea [Servicios de aplicaciones de Azure y servicios de Azure existentes](../app-service-web/app-service-changes-existing-services.md).
  * Se ha agregado soporte técnico de Azure (vista previa) de aplicaciones de API para que los clientes pueden publicar proyectos ASP.NET como aplicaciones de API y, a continuación, usar hello Agregar > gesto de cliente de aplicación de API de Azure en código C# proyectos toogenerate basado en la estructura de Hola de hello implementado API App. 
  * nodo de sitios Web de Hello en el Explorador de servidores está en desuso en lugar de nodo de servicio de aplicaciones de Azure de hello, que incluye compatibilidad para la agrupación de aplicaciones de API de Azure, aplicaciones móviles y aplicaciones Web basada en el grupo de recursos.
  * Se ha agregado compatibilidad con Azure de aplicaciones móviles (versión preliminar) para que los clientes pueden crear nuevos proyectos de aplicaciones móviles, agregar controladores de aplicaciones móviles, publicar proyectos de Hola y depurar aplicaciones de forma remota.
  * Agregar > gesto de cliente de aplicación de API de Azure ahora es compatible con los archivos locales de Swagger JSON, por lo que pueden usar los desarrolladores de Web API NuGets de terceros como Swashbuckle toogenerate Swagger o crear de forma manual. De esta manera, los desarrolladores de cliente pueden utilizar tooconsume de características de generación de código de hello cualquier extremo de Swagger en proyectos de C#. 
  * Aplicación Web y API App cuadros de diálogo publicación han concepto de Portal de Azure de hello toosupport mejorada de agrupación de recursos y selección/creación de grupos de recursos de Azure y planes de servicio de aplicaciones se representan en hello Web App y API App aprovisionamiento cuadro de diálogo nuevo. 
  * Nodos de explorador de servidores de aplicación de API de Azure proporcionan toohello vínculos que vínculo de aplicaciones de API de profundidad de hello Portal de Azure, así como otras características, como la transmisión por secuencias de registro y la depuración remota.
    
    Para saber los problemas conocidos y las limitaciones actuales del SDK de Azure para .NET 2.5.1 consulte [esta](app-service-release-notes.md#known_issues_2_5_1) sección más adelante.
* Nuevas características/escenarios relacionados con demasiado**HDInsight Tools** en Visual Studio están habilitadas en esta versión. 
  
  * Validación local de los scripts de hive. Si hay algún error en la secuencia de comandos, haga clic en botón de script de Hola validar en hello toosee de barra de herramientas. 
  * Mejora de la depuración de los trabajos de Hive. Ahora puede depurar los trabajos de Hive mediante el acceso a los registros de hilo en Visual Studio. Si la aplicación tiene problemas de rendimiento, la investigación los registros de hilo proporcionará información útil.
  * (Vista previa pública) Finalización automática de palabra clave y compatibilidad con IntelliSense para Hive. toohelp crear scripts de Hive, HDInsight Tools para Visual Studio agrega la finalización automática de palabra clave y compatibilidad con IntelliSense para Hive.
  * Compatibilidad con Storm. Ahora puede usar herramientas de HDInsight para Visual Studio toodevelop Storm topologías/Spouts/tornillos en C#. A continuación, puede enviar hello desarrollado clúster de Storm tooa de topología y ver el estado de topología/rayo/pitorro Hola. Puede usar los registros de sistema y cliente inicie sesión tootroubleshoot los aluvión topologías/tornillos/Spouts. También puede utilizar los activos existentes de JAVA en Storm en HDInsight.
    
    Para obtener más información, consulte [Introducción al uso de las herramientas de Hadoop de HDInsight para Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Problemas y limitaciones conocidos del SDK de Azure para .NET 2.5.1
* Las aplicaciones de la API de Azure están visibles como un destino de implementación para las aplicaciones móviles. Aplicaciones Web debe ser único destino de Hola para aplicaciones móviles hasta una versión posterior. 
* Puede dar lugar a Azure App API aprovisionamiento correcto pero de forma intermitente producirá un error tooupdate Hola progreso en la ventana de actividad del servicio de aplicación de Azure de hello. Solución alternativa es toocheck estado de API de Azure nueva aplicación de Hola Hola Portal de Azure. 
* La experiencia de Archivo > Nuevo proyecto > Aplicación de la API > F5 produce un error HTTP porque no existe default/index.html. Solución alternativa es toomanually examinar toohello/api/valores URL. 
* De forma intermitente, los iconos del explorador de servidores aparecen planos. Si reinicia el VS se resuelve este problema. 
* Si se produce una excepción durante el aprovisionamiento de aplicación Web o API App (por ejemplo, errores de cuota excedida o nombre duplicado de puerta de enlace de aplicación de API de Azure), aparecen errores de hello en texto sin formato JSON. 
* Problemas intermitentes de la creación del proyecto cuando Application Insights se activa en el momento de creación del proyecto.
* En ocasiones, Hola genera código de cliente de aplicación de API de Azure carece de espacios de nombres, será necesario toobe incluyen manualmente (o importa automáticamente a través de las indicaciones de Visual Studio) para toocompile de código. 
* Proyectos de aplicación móvil deben ser publicado tooweb aplicaciones, pero debe seleccionar un sitio que ha creado como una aplicación móvil en hello Portal de Azure ya que los proyectos de aplicación móvil requieren una base de datos. 
* página de inicio de Hola para aplicaciones móviles utiliza el término de Hola "servicio móvil" en lugar de "aplicaciones móviles" 
* Creación del proyecto de aplicación móvil puede tardar minutos toocreate de tooa. 
* Durante la API App aprovisionamiento (en algunos casos) error vuelve a estar del Hola reflejar el API de Azure que los permisos de hello no se pudieron establecer correctamente, mientras Hola API App se ha aprovisionado correctamente y está listo para su uso. Puede establecer manualmente los permisos mediante Hola Portal de Azure.
* Application Insights no es compatible con plantillas de aplicación de la API y plantillas de la aplicación móvil.
* Los proyectos de aplicación de la API no pueden usarse junto con los proyectos de servicio en la nube.
* Las plantillas de proyecto de la aplicación de la API solo están disponibles en C#.
* Solo se admite el consumo de API App a través del menú contextual de Hola "Agregar de cliente de aplicación de API de Azure" en C#.

