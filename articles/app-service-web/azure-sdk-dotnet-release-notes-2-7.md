---
title: "Notas de la versión SDK para .NET 2.7 y .NET 2.7.1 aaaAzure"
description: "Notas de la versión de SDK de Azure para .NET 2.7 y .NET 2.7.1"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Notas de la versión de SDK de Azure para .NET 2.7 y .NET 2.7.1
## <a name="overview"></a>Información general
Este documento contiene notas de la versión de Hola para hello Azure SDK para la versión 2.7. NET. 

documento de Hello también contienen notas de la versión de Hola para hello Azure SDK para .NET 2.7.1 de la versión.

Azure SDK 2.7 solo es compatible en Visual Studio 2015 y Visual Studio 2013. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) es Hola admite último SDK para Visual Studio 2012.

Para información detallada acerca de esta publicación, consulte la[ Publicación de anuncio de SDK de Azure 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) y [Publicación de anuncio de SDK de Azure 2.7.1](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>SDK de Azure para .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Mejoras en el inicio de sesión de Visual Studio de 2015
2.7 de Azure SDK para Visual Studio 2015 admite nuevas características de administración de identidad hello en Visual Studio 2015.  Esto incluye la compatibilidad para las cuentas de acceso a Azure mediante control de acceso basado en rol, proveedores de soluciones en la nube, DreamSpark y otros tipos de cuenta y suscripción.

Hola inicio de sesión mejoras incluidas con Azure SDK 2.7 solo están disponibles en Visual Studio 2015. Compatibilidad con Visual Studio 2013 se incluye en SDK de Azure 2.7.1.

### <a name="mobile-sdk"></a>SDK de dispositivos móvil
Actualizar **aplicaciones móviles** más recientes de plantillas tooreflect [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) y proceso de instalación.

### <a name="service-bus"></a>Bus de servicio
Mejoras y correcciones de errores generales. Para obtener información detallada sobre las actualizaciones y otras características, consulte notas de la versión más reciente de Hola toohello [NuGet de Bus de servicio](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>Herramientas de HDInsight
En esta versión de Hola se han realizado las siguientes actualizaciones. Estas actualizaciones se encuentran en vista previa. Para obtener más información, consulte [este blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Gráficos de Hive para Hive en trabajos de Tez
* Compatibilidad completa de IntelliSense de DML de Hive
* Compatibilidad con plantillas de Pig
* Plantillas de Storm para servicios de Azure

#### <a name="breaking-changes"></a>Cambios drásticos
* Antiguo **Storm** proyecto debe actualizarse cuando se usa esta versión de herramientas de Hola. Para más información, vea [este blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Visual Studio Web Express ya no es compatible. Para obtener más información, consulte [este blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Herramientas del Servicio de aplicaciones de Azure
En esta versión de Hola se han realizado las siguientes actualizaciones tooWeb las extensiones de herramientas. Para más información, consulte [este](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blog. 

* Compatibilidad agregada para las cuentas de DreamSpark
* Cambiar completa tooAzure herramientas realizadas toosupport Hola nuevas API de administración de recursos de Azure
* Compatibilidad con el servicio de aplicación de Azure agrega demasiado[explorador en la nube](#cloud_explorer)

#### <a name="known-issues"></a>Problemas conocidos
Nodos de ranura de implementación de aplicación Web no aparecen en el nodo de ranuras de hello en el Explorador de servidores y nodos de secundarios de ranura de implementación de aplicación Web no se cargan en el explorador en la nube. Este problema se ha resuelto y preparado para la próxima versión SDK Hola. 

### <a name="cloud_explorer"></a>Cloud Explorer para Visual Studio de 2015
2.7 de Azure SDK incluye el explorador en la nube para Visual Studio 2015 que permite tooview los recursos de Azure, inspeccionar sus propiedades y realizar acciones de desarrollador clave desde dentro de Visual Studio. 

El explorador en la nube es compatible con los siguientes de hello:

* Vistas de grupo de recursos y tipo de recurso de los recursos de Azure 
* Búsqueda de recursos por nombre (disponible en la vista de tipo de recurso)
* Compatibilidad con las suscripciones y los recursos que tienen aplicado el control de acceso basado en rol (RBAC) 
* Panel de acción integrado que muestra los recursos de desarrolladores acciones tooselected específico. Por ejemplo: asociar el depurador remoto para máquinas virtuales creadas mediante Hola pila del Administrador de recursos, ver datos de diagnóstico para máquinas virtuales etcetera.
* Panel de propiedades integrado que muestra propiedades orientadas a desarrolladores normalmente necesarias durante el desarrollo y las pruebas 
* Cambio rápido de hello cuenta toouse al enumerar los recursos (use comandos de configuración de la barra de herramientas) 
* Filtrado de suscripciones toouse al enumerar los recursos (use comandos de configuración de la barra de herramientas) 
* Vínculos profundos toohello Portal de Azure para la administración de recursos y grupos de recursos 

### <a name="azure-resource-manager-tools"></a>Herramientas del Administrador de recursos de Azure
Herramientas de administrador de recursos de Azure de Hello han sido toowork actualizada con nuevos tipos de suscripción y Control de acceso basado en roles (RBAC).  Estos cambios incluye Hola capacidad toouse nuevas cuentas de almacenamiento, además tooclassic almacenamiento, artefactos de toostore durante la implementación.  

Si usas un proyecto del grupo de recursos de Azure desde una versión anterior de hello SDK con hello 2.7 de SDK, un nuevo script de implementación es necesario toodeploy con una cuenta de almacenamiento en lugar de almacenamiento clásicos.  Se le pedirá antes de que se realizan cambios tooyour proyecto tooadd Hola nueva secuencia de comandos.  se cambiará el script anterior de Hola y deberá toomanually realice las modificaciones toohello nueva secuencia de comandos.

### <a name="storage-explorer-tools"></a>Herramientas del explorador de almacenamiento
* Compatibilidad con la visualización de los blobs de anexión. Puede obtener más información en [esta entrada de blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Soporte técnico para ver las cuentas de almacenamiento premium a través del Explorador de servidores. Explorador de servidores solo muestra los blobs en páginas para cuentas de almacenamiento premium, ya que son de tipo hello que solo se admite para las cuentas de almacenamiento premium.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Herramientas de Factoría de datos de Azure para Visual Studio
Introducción a **Herramientas de Factoría de datos de Azure** para Visual Studio. A continuación se muestran las características de hello habilitado. Para obtener más información, consulte [este blog](http://go.microsoft.com/fwlink/?LinkId=617530) .

* **En función de plantilla de creación**: seleccione la grafía de uso basados en plantillas, plantillas de movimiento de datos o toodeploy de plantillas de procesamiento de datos de una solución de integración de datos to-end y empezar a prácticas rápidamente con factoría de datos. 
* **Integración con el Explorador de soluciones para la creación e implementación de entidades de Data Factory**: cree e implemente canalizaciones y las entidades relacionadas como proyectos de Visual Studio. 
* **Integración con la vista de diagrama de interacción visual mientras se crea**: crear visualmente las canalizaciones y conjuntos de datos con la Ayuda de hello vista de diagrama. 
* **Integración con el Explorador de servidores para la exploración y la interacción con entidades ya implementadas**: aproveche Hola Explorador de servidores toobrowse ya implementado factorías de datos y entidades correspondientes. Importe una factoría de datos implementada o cualquier identidad (canalización, servicios vinculados o conjuntos de datos) en el proyecto. 
* **Edición de JSON con IntelliSense enriquecido y validación de esquema**: configure y edite de forma eficiente documentos JSON de entidades de Factoría de datos con IntelliSense enriquecido y validación de esquema 
* **Publicación de entorno de varios**: publicar canalizaciones creado toodev, prueba o entorno de producción mediante la creación de archivos de configuración independientes para cada entorno.
* **Soporte técnico de procesamiento de datos basado en Pig, Hive y .Net**: soporte técnico para scripts de Pig y Hive en el proyecto de Factoría de datos. Soporte técnico para hacer referencia al proyecto de C# para la administración de .Net Activity.

## <a name="azure-sdk-for-net-271"></a>SDK de Azure para .NET 2.7.1
Hola siguiente sección contiene las actualizaciones que se introdujeron con hello Azure SDK para .NET 2.7.1 de la versión.

### <a name="hdinsight-tools"></a>Herramientas de HDInsight
Para obtener una explicación más detallada acerca de las actualizaciones de herramientas de HDInsight, consulte [este blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Vista de operador de trabajos de Hive (nueva característica)
  
    se agregó toohelp comprender su consulta de Hive mejor, la característica de vista de operador de Hive de Hola. toosee todos los operadores de hello dentro de un vértice, haga doble clic en los vértices de Hola Hola del gráfico del trabajo. tooview más detalles acerca de un operador determinado, mantenga el mouse sobre ese operador.
* Marcador de Error de Hive (nueva característica)
  
    tooenable que tooview Hola gramaticales al instante, Hola característica Hive Error marcador se agregó. Además, los mensajes de error se han mejorado y ahora puede ver los errores gramaticales detallada al instante (hasta esta versión, era toosubmit un clúster de toohello de script de Hive y espere a que algún tiempo antes de obtener detalles sobre el mensaje de error).  
* Gráfico de topología Storm (nueva característica)
  
    La visualización es muy importante cuando se desea toosee si su topología funciona según lo previsto. En esta versión agregamos la visualización de gráficos Storm. Puede visualizar las métricas importantes de hello para la topología (por ejemplo, un color indica un rayo determinado de tiempo es "ocupado" o no). También puede hacer doble clic Hola rayo/pitorro tooview más detalles.
* Compatibilidad con clústeres de HDInsight que se crearon en hello Portal de Azure (una corrección de errores)
  
    Ahora puede usar Visual Studio tooview y enviar tooall trabajos clústeres de HDInsight con independencia de donde se crearon clúster Hola.
* Mayor compatibilidad con IntelliSense y carga más rápida de metadatos de Hive (mejora)
  
    Hemos mejorado Hola IntelliSense agregando más sugerencias de usuario descriptivo. Por ejemplo, el alias de tabla ahora también puede sugerirse en IntelliSense para que pueda escribir la consulta más fácilmente. Además, se han mejorado los metadatos de Hive Hola carga, de manera que solo se tarda varios segundos toolist todas las bases de datos de hello, tablas y columnas de la tienda de metadatos de Hive.

Para obtener una explicación más detallada acerca de las actualizaciones de herramientas de HDInsight, consulte [este blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Mejoras en Visual Studio 2013
* Azure SDK 2.7.1 permite que Visual Studio 2013 tooaccess cuentas de Azure y las suscripciones a través de Control de acceso basado en roles, los proveedores de soluciones de nube y Dreamspark.
* Con Azure SDK 2.7.1, nueva ventana de herramientas de explorador en la nube Hola ahora también está disponible en Visual Studio 2013.

### <a name="known-issues"></a>Problemas conocidos
Instalar Azure SDK 2.6 de Hola o 2.7.1 para Visual Studio Community 2013 en una no son inglés de SO mostrará una advertencia que Hola inglés y pueden que no coincidan los recursos no están en inglés de Visual Studio. Esta advertencia se puede descartar sin más preocupaciones. Solo aparecerá si la máquina de hello no contenía una instalación anterior de Visual Studio Community 2013 y está instalando Hola SDK en una no son inglés de SO. Advertencia de Hola se muestra una vez que el paquete de idioma de hello aplica Hola RTM recursos tooVisual Studio, pero antes de aplicar la actualización 4. Al descartar la advertencia Hola le permitirá toocontinue de paquete de idioma de Hola y versión completa de la actualización 4 hello aplicar de paquete de idioma de hello contenido.

Los proyectos de LightSwitch no son compatibles con esta versión. Este problema se resolverá con hello SDK siguiente de la versión.

## <a name="also-see"></a>Consulte también:
[Publicación de anuncio de SDK de Azure 2.7.1](http://go.microsoft.com/fwlink/?LinkId=623850)

[Publicación de anuncio de Azure SDK 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Información de retirada para hello Azure SDK para .NET y las API y soporte técnico](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

