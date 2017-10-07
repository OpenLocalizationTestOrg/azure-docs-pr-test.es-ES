---
title: aaaAzure SDK para .NET 2.6 notas
description: "Notas de la versión de SDK de Azure para .NET 2.6"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Notas de la versión de SDK de Azure para .NET 2.6
Este documento contiene notas de la versión de Hola para hello Azure SDK para la versión 2.6. NET. 

Puede desarrollar aplicaciones de servicio de nube (PaaS) tienen como destino .NET 4.5.2 o 4.6 de .NET siempre que instalar manualmente .NET Framework de destino de hello en hello rol de servicio de nube con Azure SDK 2.6. Consulte [Instalar .NET en un rol de Servicio en la nube](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Actualizaciones de Bus de servicio
* Centros de eventos: 
  
  * Ahora permite el control de acceso dirigido cuando se envían eventos mediante la exposición de un extremo de publicador adicional para Centros de eventos.
  * Estabilidad adicional y mejora agregan la característica de bases de datos centrales de tooEvent.
  * Mayor compatibilidad para el protocolo Amqp sobre WebSocket para mensajería y Centros de eventos.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Actualizaciones de herramientas de HDInsight para Visual Studio
* **Mejora de IntelliSense**: sugerencia de metadatos remotos
  
    Las Herramientas de HDInsight para Visual Studio ahora son compatibles con la obtención de metadatos remotos cuando se edita el script de Hive. Por ejemplo, puede escribir **seleccione * FROM** y se muestran todos los nombres de tabla de Hola. Además, los nombres de columna de Hola se mostrará después de especificar una tabla.
* **Compatibilidad con el emulador de HDInsight**
  
    Ahora herramientas de HDInsight para compatibilidad de Visual Studio conectarse emulador tooHDInsight, por lo que puede desarrollar los scripts de Hive localmente sin generar ningún costo, a continuación, ejecute los scripts en los clústeres de HDInsight. 
  
    Para obtener más información, consulte demasiado[este manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Las Herramientas de HDInsight para Visual Studio admiten clústeres genéricos de Hadoop** (vista previa)
  
    Ahora HDInsight Tools para Visual Studio admiten clústeres de Hadoop genéricos, por lo que puede usar herramientas de HDInsight para Visual Studio toodo Hola a continuación:
  
  * conecta el clúster de tooyour, 
  * escribir la consulta de Hive con compatibilidad de finalización automática/IntelliSense mejorada, 
  * ver todos los trabajos de hello en el clúster con una interfaz de usuario intuitiva. 
    
    Para obtener más información, consulte demasiado[este manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Actualizaciones de Caché en rol
* **Caché en rol** se ha actualizado toouse **SDK de almacenamiento de Microsoft Azure** versión 4.3. Hasta ahora, Hola **caché en rol** estaba usando la versión 1.7 del SDK de almacenamiento de Azure.
  
    Los clientes utilizando Azure SDK 2.5 o a continuación debe actualizar tooAzure SDK 2.6 y mover toohello nueva versión de SDK de almacenamiento de Azure. 
  
    En esta versión de almacenamiento de Azure tiempo 2011-08-18 es programada toobe quitado el 1 de agosto de 2016. Llegados a este punto, las migraciones de memoria de caché en rol de Azure SDK 2.5 o por debajo de too2.6 deben ser completa. Para obtener más información sobre la retirada de hello del almacenamiento de Azure versión 2011-08-18, consulte [actualización eliminación de versión de servicio de almacenamiento de Microsoft Azure: extensión too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Estamos anunciando Hola 30 de noviembre de 2016, retirada de servicio de caché administrado de Azure y caché en rol de Azure. Se recomienda encarecidamente que migre tooAzure caché en Redis como preparación para esta retirada. Para obtener más información sobre las fechas y la guía de migración, consulte [¿Qué oferta de caché de Azure es adecuada para mí?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Herramientas del Servicio de aplicaciones de Azure
Hola siguientes elementos se actualizaron en la versión de hello Azure SDK 2.6.

* Publicación de Azure había mejorado tooinclude aplicaciones de API de Azure como un destino de implementación.
* Aplicaciones de API de aprovisionamiento a los usuarios de tooenable de funcionalidad con la creación de API App y la funcionalidad de aprovisionamiento.
* Servidor explorador cambiado tooreflect nuevo nodo servicio de aplicaciones, con aplicaciones Web, móviles y API agrupados por grupo de recursos.
* Agregue el gesto de cliente de aplicación de API de Azure agrega proyectos toomost C# que se habilitará la generación automática de las aplicaciones de API basadas en Swagger ejecutando en la suscripción de Azure de un usuario.
* Las herramientas de Aplicaciones de API y los nodos de Servicio de aplicaciones en el Explorador de servidores solo se encuentran disponibles en Visual Studio 2013. 

## <a name="azure-resource-manager-tools-updates"></a>Actualizaciones de las herramientas del Administrador de recursos de Azure
herramientas del Administrador de recursos de Azure Hola han sido actualizados tooinclude plantillas para máquinas virtuales, redes y almacenamiento. experiencia de edición de JSON de Hello ha sido actualizada tooinclude una nueva vista de esquema para plantillas y plantillas de Hola Hola capacidad tooedit con fragmentos de código JSON. Plantillas implementadas desde Visual Studio usan un script de PowerShell que se proporciona con el proyecto de hello, de manera que los cambios realizados toohello script se usará en Visual Studio.

## <a name="diagnostics-improvements-for-cloud-services"></a>Mejoras de diagnósticos para Servicios en la nube
Azure SDK 2.6 incorpora compatibilidad para recopilar los registros de diagnóstico en el emulador de proceso de Azure de Hola y transferirlos volver toodevelopment almacenamiento: Los diagnósticos se registra (incluidos los registros de seguimiento de eventos para registros de Windows (ETW), los contadores de rendimiento, infraestructura de registros de eventos de windows y de registros de seguimiento de aplicación) generado cuando se ejecuta la aplicación hello en el emulador de hello puede ser transferido toodevelopment tooverify de almacenamiento que funciona el registro de diagnósticos en el equipo local. 

Hola cuenta de almacenamiento de diagnósticos ahora puede especificarse en el archivo de configuración (.cscfg) de servicio de hello lo que sea más fáciles cuentas de almacenamiento de diagnóstico diferentes toouse para diferentes entornos. Hay algunas diferencias importantes entre la cadena de conexión de hello trabajado en Azure SDK 2.4 y Azure SDK 2.6. Para obtener más información sobre cómo ver la cadena de conexión de almacenamiento de diagnósticos de toouse hello y cómo afecta a los proyectos de [configurar diagnósticos para los servicios de nube de Azure](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Cambios drásticos
### <a name="azure-resource-manager-tools"></a>Herramientas del Administrador de recursos de Azure
* Hola **proyectos de implementación de nube** disponibles en hello Azure SDK 2.5 se cambió demasiado del tipo de proyecto**grupo de recursos de Azure**.
* **Proyectos de implementación de nube** se puede usar el tipo de proyectos creados en hello Azure SDK 2.5 en 2.6 pero se producirá un error en la plantilla de implementación Hola desde Visual Studio. Sin embargo, implementar con hello script de PowerShell seguirá funcionando como lo hacía anteriormente.  Para obtener información acerca de cómo toouse **proyectos de implementación de nube** en 2.6 leído [registrar](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Problemas conocidos
* Recopilar registros de diagnóstico en el emulador de hello requiere un sistema operativo de 64 bits. Los registros de diagnósticos no se recopilarán cuando se ejecuten en un sistema operativo de 32 bits. Esto no afecta ninguna otra funcionalidad del emulador. 
* La versión del SDK 2.6 de Azure del 29 de abril de 2015 presentaba dos problemas: 
  
  * No se pudo cargar la aplicación universal de Visual Studio 2015 cuando se instaló Azure SDK 2.6 en el equipo de Hola.
  * Depurar un proyecto de servicio de nube produciría un error en Visual Studio 2013 y Visual Studio 2015 donde Visual Studio deja de responder y se bloquea mientras se muestra un cuadro de diálogo con el mensaje de saludo "Configurar diagnósticos para emulador".
    
    Un SDK 2.6 tooAzure de actualización se publicó en 5/18/2015. versión de Hola actualizado es 2.6.30508.1601; contiene correcciones para dos problemas descritos anteriormente. Puede identificar la compilación de Hola de hello SDK desde el Panel de Control -> programas y características -> Microsoft Azure Tools para Microsoft Visual Studio 2013 – v 2.6. columna de versión de Hola mostrará el número de compilación de Hola.
    
    Si todavía se enfrentan Hola por encima de problemas, instalar Hola la versión más reciente de Hola 2.6 de Azure SDK para [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Otras referencias
[Información de retirada para hello Azure SDK para .NET y las API y soporte técnico](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

