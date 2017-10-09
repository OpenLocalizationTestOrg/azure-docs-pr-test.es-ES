---
title: "tutorial de actualización de aplicación de tejido de aaaService | Documentos de Microsoft"
description: "Este artículo le guía a través de la experiencia de Hola de implementar una aplicación de Service Fabric, cambiar el código de hello y efectuando una actualización mediante Visual Studio."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Tutorial sobre la actualización de aplicaciones de Service Fabric con Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure Service Fabric simplifica el proceso de Hola de actualización de aplicaciones de nube asegurándose de que se actualizan solo servicios cambiados y que se supervisa el estado de aplicaciones a lo largo del proceso de actualización de Hola. También revierte automáticamente toohello de versión anterior ante problemas para la aplicación hello. Las actualizaciones de aplicaciones de Service Fabric son *tiempo de inactividad cero*, ya que se puede actualizar la aplicación hello sin ningún tiempo de inactividad. Este tutorial trata cómo toocomplete una actualización gradual desde Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Paso 1: Crear y publicar el ejemplo de Hola a objetos visuales
En primer lugar, descargue hello [objetos visuales](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) aplicación de GitHub. A continuación, compilar y publicar la aplicación hello con el botón secundario en el proyecto de aplicación de hello, **VisualObjects**y seleccionando hello **publicar** comando en el elemento de menú de hello Service Fabric.

![Menú contextual para una aplicación de Service Fabric][image1]

Seleccionar **publicar** , se abrirá un ventana emergente, y puede establecer hello **elegir como destino profile** demasiado**PublishProfiles\Local.xml**. ventana Hello debe ser una similar Hola siguientes antes de hacer clic **publicar**.

![Publicación de una aplicación de Service Fabric][image2]

Ahora puede hacer clic en **publicar** en el cuadro de diálogo de Hola. Puede usar [Service Fabric Explorer tooview Hola clúster y Hola una aplicación](service-fabric-visualizing-your-cluster.md). Hola aplicación objetos visuales tiene un servicio web que vaya escribiendo tooby [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) en la barra de direcciones de hello del explorador.  Debería ver los 10 objetos visuales flotantes desplazarse en la pantalla de bienvenida.

**Nota:** si implementar demasiado`Cloud.xml` perfil (Azure Service Fabric), aplicación hello, a continuación, debe estar disponible en **http://{ServiceFabricName}. {} Region}.cloudapp.Azure.com:8081/visualobjects/**. Asegúrese de que tiene `8081/TCP` configurado en hello equilibrador de carga (encontrar Hola equilibrador de carga en hello mismo grupo de recursos como instancia de Service Fabric hello).

## <a name="step-2-update-hello-visual-objects-sample"></a>Paso 2: Actualizar la muestra de Hola a objetos visuales
Observará que con la versión de Hola que se implementó en el paso 1, los objetos visuales de hello no giran. Vamos a actualizar esta tooone de aplicación donde los objetos visuales de hello girar.

Seleccione hello VisualObjects.ActorService proyecto dentro de hello VisualObjects solución y abrir hello **VisualObjectActor.cs** archivo. Dentro de ese archivo, vaya toohello método `MoveObject`, comente `visualObject.Move(false)`y quitar el comentario `visualObject.Move(true)`. Este cambio en el código gira objetos Hola después de la actualización de servicio de Hola.  **Ahora puede compilar (no recompilación) Hola solución**, qué compilaciones Hola modificación proyectos. Si selecciona *volver a generar todo*, tiene tooupdate Hola versiones para todos los proyectos de Hola.

También es necesario tooversion nuestra aplicación. versión de hello toomake cambia una vez que haga doble clic en hello **VisualObjects** proyecto, puede usar Visual Studio hello **editar manifiesto versiones** opción. Al seleccionar esta opción abre cuadro de diálogo de Hola de versiones como se indica a continuación:

![Cuadro de diálogo de control de versiones][image3]

Actualizar versiones de Hola para hello modificaron proyectos y sus paquetes de código, junto con la aplicación de hello tooversion 2.0.0. Después de realizar cambios de hello, manifiesto Hola debería ser similar siguiente de hello (negrita partes Mostrar cambios de hello):

![Actualización de versiones][image4]

herramientas de Visual Studio Hola pueden hacer resúmenes automática de versiones al seleccionar **actualizar automáticamente la aplicación y las versiones de servicio**. Si usa [SemVer](http://www.semver.org), se necesita especificar el código de hello tooupdate y se selecciona la opción solo si esa versión del paquete de configuración.

Guardar los cambios de Hola y compruebe ahora hello **actualización Hola aplicación** cuadro.

## <a name="step-3--upgrade-your-application"></a>Paso 3: Actualizar la aplicación
Familiarícese con hello [parámetros de actualización de la aplicación](service-fabric-application-upgrade-parameters.md) hello y [proceso de actualización](service-fabric-application-upgrade.md) tooget un buen conocimiento de saludo diversos actualizan parámetros, los tiempos de espera y criterios de mantenimiento que puede se aplica. En este tutorial, criterio de evaluación de mantenimiento de servicio de Hola se establece toohello predeterminada (modo no supervisado). Puede configurar estas opciones mediante la selección **configurar opciones de actualización** y, a continuación, modificar los parámetros de hello según sea necesario.

Ahora estamos todas las aplicaciones de conjunto toostart Hola actualización seleccionando **publicar**. Esta opción actualiza su tooversion aplicación 2.0.0, en el que girar objetos Hola. Service Fabric actualiza un dominio de actualización a la vez (algunos objetos se actualizan en primer lugar, seguida de otras personas) y servicio de hello siga siendo accesible durante la actualización de Hola. El servicio de acceso toohello puede comprobarse a través del cliente (explorador).  

Ahora, como hello continúa de actualización de aplicación, puede supervisarla con Service Fabric Explorer, mediante el uso de hello **las actualizaciones en curso** ficha en aplicaciones de Hola.

En unos minutos, se deben actualizar todos los dominios de actualización (completado) y Hola ventana de salida de Visual Studio también debe indicar que la actualización Hola se completa. Y debería encontrar que *todos los* ahora va a rotar objetos visuales de hello en la ventana del explorador.

Puede desee tootry cambio de versiones de Hola y mover de versión 2.0.0 tooversion 3.0.0 como un ejercicio o incluso de versión 2.0.0 volver tooversion 1.0.0. Practicar con los tiempos de espera y toomake de directivas de mantenimiento usted mismo familiarizados con ellos. Al implementar tooan Azure clúster según opone tooa local del clúster, los parámetros de hello usa pueden tener toodiffer. Se recomienda establecer los tiempos de espera de hello manera conservadora.

## <a name="next-steps"></a>Pasos siguientes
[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.

Puede controlar cómo se actualiza una aplicación usando [parámetros de actualización](service-fabric-application-upgrade-parameters.md).

Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).

Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).

Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
